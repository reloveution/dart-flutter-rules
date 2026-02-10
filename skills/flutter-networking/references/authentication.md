# Authentication

## Overview

Complete guide for implementing authentication in Flutter HTTP requests.

## Authentication Methods

### Bearer Token (JWT)

Most common for REST APIs using JWT (JSON Web Tokens):

```dart
import 'dart:io';

Future<Album> fetchAlbum(String token) async {
  final response = await http.get(
    Uri.parse('https://api.example.com/albums/1'),
    headers: {HttpHeaders.authorizationHeader: 'Bearer $token'},
  );

  if (response.statusCode == 200) {
    return Album.fromJson(jsonDecode(response.body));
  } else {
    throw Exception('Failed to load album');
  }
}
```

### Basic Authentication

```dart
import 'dart:convert';

String basicAuthHeader(String username, String password) {
  final credentials = '$username:$password';
  return 'Basic ${base64Encode(utf8.encode(credentials))}';
}

Future<Album> fetchAlbum(String username, String password) async {
  final response = await http.get(
    Uri.parse('https://api.example.com/albums/1'),
    headers: {
      HttpHeaders.authorizationHeader: basicAuthHeader(username, password),
    },
  );

  if (response.statusCode == 200) {
    return Album.fromJson(jsonDecode(response.body));
  } else {
    throw Exception('Failed to load album');
  }
}
```

### API Key

```dart
Future<Album> fetchAlbum(String apiKey) async {
  final response = await http.get(
    Uri.parse('https://api.example.com/albums/1'),
    headers: {'X-API-Key': apiKey},
  );

  if (response.statusCode == 200) {
    return Album.fromJson(jsonDecode(response.body));
  } else {
    throw Exception('Failed to load album');
  }
}
```

## Token Storage

### Using shared_preferences

Add to `pubspec.yaml`:

```yaml
dependencies:
  shared_preferences: ^2.5.4
```

Store and retrieve tokens:

```dart
import 'package:shared_preferences/shared_preferences.dart';

class TokenStorage {
  static const String _tokenKey = 'auth_token';

  Future<void> saveToken(String token) async {
    final prefs = await SharedPreferences.getInstance();
    await prefs.setString(_tokenKey, token);
  }

  Future<String?> getToken() async {
    final prefs = await SharedPreferences.getInstance();
    return prefs.getString(_tokenKey);
  }

  Future<void> clearToken() async {
    final prefs = await SharedPreferences.getInstance();
    await prefs.remove(_tokenKey);
  }
}
```

### Using flutter_secure_storage

For more secure storage:

```yaml
dependencies:
  flutter_secure_storage: ^10.0.0
```

```dart
import 'package:flutter_secure_storage/flutter_secure_storage.dart';

class SecureTokenStorage {
  final _storage = const FlutterSecureStorage();
  static const String _tokenKey = 'auth_token';

  Future<void> saveToken(String token) async {
    await _storage.write(key: _tokenKey, value: token);
  }

  Future<String?> getToken() async {
    return await _storage.read(key: _tokenKey);
  }

  Future<void> clearToken() async {
    await _storage.delete(key: _tokenKey);
  }
}
```

## Authenticated HTTP Client

### Wrapper Class

```dart
import 'dart:io';
import 'package:http/http.dart' as http;

class AuthenticatedHttpClient {
  final TokenStorage _tokenStorage;

  AuthenticatedHttpClient(this._tokenStorage);

  Future<http.Response> get(String url) async {
    final token = await _tokenStorage.getToken();
    if (token == null) {
      throw UnauthorizedException();
    }

    return await http.get(
      Uri.parse(url),
      headers: {HttpHeaders.authorizationHeader: 'Bearer $token'},
    );
  }

  Future<http.Response> post(
    String url, {
    Map<String, String>? headers,
    Object? body,
  }) async {
    final token = await _tokenStorage.getToken();
    if (token == null) {
      throw UnauthorizedException();
    }

    return await http.post(
      Uri.parse(url),
      headers: {
        HttpHeaders.authorizationHeader: 'Bearer $token',
        ...?headers,
      },
      body: body,
    );
  }

  Future<http.Response> put(
    String url, {
    Map<String, String>? headers,
    Object? body,
  }) async {
    final token = await _tokenStorage.getToken();
    if (token == null) {
      throw UnauthorizedException();
    }

    return await http.put(
      Uri.parse(url),
      headers: {
        HttpHeaders.authorizationHeader: 'Bearer $token',
        ...?headers,
      },
      body: body,
    );
  }

  Future<http.Response> delete(String url) async {
    final token = await _tokenStorage.getToken();
    if (token == null) {
      throw UnauthorizedException();
    }

    return await http.delete(
      Uri.parse(url),
      headers: {HttpHeaders.authorizationHeader: 'Bearer $token'},
    );
  }
}

class UnauthorizedException implements Exception {
  final String message;
  UnauthorizedException([this.message = 'Unauthorized']);

  @override
  String toString() => message;
}
```

## Token Refresh

### Refresh Token Pattern

```dart
class AuthManager {
  final TokenStorage _tokenStorage;
  final http.Client _client;

  String? _accessToken;
  String? _refreshToken;

  AuthManager(this._tokenStorage, this._client);

  Future<String> getAccessToken() async {
    if (_accessToken != null && !_isTokenExpired(_accessToken)) {
      return _accessToken!;
    }

    return await _refreshAccessToken();
  }

  bool _isTokenExpired(String token) {
    // Decode JWT and check expiration
    return false;
  }

  Future<String> _refreshAccessToken() async {
    final response = await _client.post(
      Uri.parse('https://api.example.com/auth/refresh'),
      headers: {'Content-Type': 'application/json'},
      body: jsonEncode({'refreshToken': _refreshToken}),
    );

    if (response.statusCode == 200) {
      final data = jsonDecode(response.body) as Map<String, dynamic>;
      _accessToken = data['accessToken'] as String;
      _refreshToken = data['refreshToken'] as String;

      await _tokenStorage.saveToken(_accessToken!);
      return _accessToken!;
    } else {
      throw Exception('Failed to refresh token');
    }
  }

  Future<void> logout() async {
    await _tokenStorage.clearToken();
    _accessToken = null;
    _refreshToken = null;
  }
}
```

### Interceptor Pattern

```dart
class AuthenticatedClient extends http.BaseClient {
  final http.Client _inner;
  final AuthManager _authManager;

  AuthenticatedClient(this._inner, this._authManager);

  @override
  Future<http.StreamedResponse> send(http.BaseRequest request) async {
    final token = await _authManager.getAccessToken();
    request.headers['Authorization'] = 'Bearer $token';

    final response = await _inner.send(request);

    if (response.statusCode == 401) {
      await _authManager.refreshAccessToken();
      final newToken = await _authManager.getAccessToken();

      request.headers['Authorization'] = 'Bearer $newToken';
      return await _inner.send(request);
    }

    return response;
  }
}
```

## Login Flow

### Complete Login Example

```dart
import 'dart:convert';

class AuthService {
  final http.Client _client;
  final TokenStorage _tokenStorage;

  AuthService(this._client, this._tokenStorage);

  Future<User> login(String email, String password) async {
    final response = await _client.post(
      Uri.parse('https://api.example.com/auth/login'),
      headers: {'Content-Type': 'application/json'},
      body: jsonEncode({
        'email': email,
        'password': password,
      }),
    );

    if (response.statusCode == 200) {
      final data = jsonDecode(response.body) as Map<String, dynamic>;
      final token = data['token'] as String;
      final user = User.fromJson(data['user'] as Map<String, dynamic>);

      await _tokenStorage.saveToken(token);
      return user;
    } else if (response.statusCode == 401) {
      throw InvalidCredentialsException();
    } else {
      throw Exception('Login failed');
    }
  }

  Future<void> logout() async {
    await _tokenStorage.clearToken();
  }
}

class User {
  final int id;
  final String email;
  final String name;

  User({required this.id, required this.email, required this.name});

  factory User.fromJson(Map<String, dynamic> json) {
    return User(
      id: json['id'] as int,
      email: json['email'] as String,
      name: json['name'] as String,
    );
  }
}

class InvalidCredentialsException implements Exception {
  @override
  String toString() => 'Invalid email or password';
}
```

## OAuth2

### OAuth2 Flow

```dart
class OAuth2Service {
  final http.Client _client;
  final TokenStorage _tokenStorage;

  OAuth2Service(this._client, this._tokenStorage);

  Future<String> authenticate(
    String clientId,
    String clientSecret,
    String code,
    String redirectUri,
  ) async {
    final response = await _client.post(
      Uri.parse('https://oauth.example.com/token'),
      headers: {'Content-Type': 'application/x-www-form-urlencoded'},
      body: {
        'grant_type': 'authorization_code',
        'client_id': clientId,
        'client_secret': clientSecret,
        'code': code,
        'redirect_uri': redirectUri,
      },
    );

    if (response.statusCode == 200) {
      final data = jsonDecode(response.body) as Map<String, dynamic>;
      final token = data['access_token'] as String;
      await _tokenStorage.saveToken(token);
      return token;
    } else {
      throw Exception('OAuth authentication failed');
    }
  }
}
```

## Best Practices

1. **Store tokens securely** - Use flutter_secure_storage for sensitive tokens
2. **Refresh tokens** - Implement token refresh before expiration
3. **Handle 401 errors** - Automatically retry with refreshed token
4. **Clear tokens on logout** - Remove stored tokens when user logs out
5. **Use HTTPS** - Never send tokens over unencrypted connections
6. **Token rotation** - Rotate refresh tokens for better security
7. **Scope tokens** - Use minimal required scopes
8. **Error handling** - Provide clear error messages for authentication failures
