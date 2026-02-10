# Deep Linking Setup

## Overview

Deep links allow users to navigate directly to specific screens in your app from external sources like:
- Web links
- Push notifications
- Other apps
- Email links

## Platform Configuration

### Android

**Step 1: Add to `AndroidManifest.xml`**

For App Links (recommended):
```xml
<manifest>
  <application>
    <activity android:name=".MainActivity">
      <intent-filter android:autoVerify="true">
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data
          android:scheme="https"
          android:host="yourapp.com" />
      </intent-filter>
    </activity>
  </application>
</manifest>
```

For custom scheme:
```xml
<intent-filter>
  <action android:name="android.intent.action.VIEW" />
  <category android:name="android.intent.category.DEFAULT" />
  <category android:name="android.intent.category.BROWSABLE" />
  <data android:scheme="myapp" />
</intent-filter>
```

**Step 2: Verify App Links (for https scheme)**
Create `https://yourapp.com/.well-known/assetlinks.json`:
```json
[{
  "relation": ["delegate_permission/common.handle_all_urls"],
  "target": {
    "namespace": "android_app",
    "package_name": "com.example.yourapp",
    "sha256_cert_fingerprints": ["YOUR_SHA256_FINGERPRINT"]
  }
}]
```

**Step 3: Test**
```bash
adb shell am start -W -a android.intent.action.VIEW -d "https://yourapp.com/path"
```

### iOS

**Step 1: Add to `ios/Runner/Info.plist`**

Universal Links (recommended):
```xml
<key>com.apple.developer.associated-domains</key>
<array>
  <string>applinks:yourapp.com</string>
</array>
```

Custom scheme:
```xml
<key>CFBundleURLTypes</key>
<array>
  <dict>
    <key>CFBundleURLName</key>
    <string>com.example.yourapp</string>
    <key>CFBundleURLSchemes</key>
    <array>
      <string>myapp</string>
    </array>
  </dict>
</array>
```

**Step 2: Verify Universal Links**
Upload Apple App Site Association file to `https://yourapp.com/.well-known/apple-app-site-association`:
```json
{
  "applinks": {
    "apps": [],
    "details": [
      {
        "appIDs": ["TEAMID.com.example.yourapp"],
        "components": [
          {
            "/": "/path/to/*",
            "comment": "Matches anything under /path/to/"
          }
        ]
      }
    ]
  }
}
```

**Step 3: Test**
```bash
xcrun simctl openurl booted "https://yourapp.com/path"
```

## Flutter Configuration

### Using go_router (Recommended)

```dart
final _router = GoRouter(
  routes: [
    GoRoute(path: '/', builder: (context, state) => HomeScreen()),
    GoRoute(path: '/details/:id', builder: (context, state) {
      final id = state.pathParameters['id'];
      return DetailsScreen(id: id!);
    }),
    GoRoute(path: '/product/:productId', builder: (context, state) {
      final productId = state.pathParameters['productId'];
      return ProductScreen(productId: productId!);
    }),
  ],
);
```

go_router automatically handles deep links when configured correctly.

### Using Navigator (Not Recommended)

```dart
MaterialApp(
  initialRoute: '/',
  routes: {
    '/': (context) => HomeScreen(),
    '/details/:id': (context) {
      final id = ModalRoute.of(context)!.settings.arguments as String;
      return DetailsScreen(id: id);
    },
  },
);
```

**Limitations:**
- Always pushes new routes (can't replace stack)
- No browser forward button on web
- Limited customization

## Web Deep Linking

Web apps handle deep links automatically. Choose URL strategy:

### Hash Strategy (Default)
```dart
// No setup needed
// URLs: https://example.com/#/path/to/screen
```

### Path Strategy
```dart
import 'package:flutter_web_plugins/url_strategy.dart';

void main() {
  usePathUrlStrategy();
  runApp(MyApp());
}
// URLs: https://example.com/path/to/screen
```

Configure web server to rewrite all routes to `index.html`. See [web-navigation.md](web-navigation.md).

## Testing Deep Links

### Android Emulator
```bash
adb shell am start -W -a android.intent.action.VIEW -d "myapp://product/123"
```

### iOS Simulator
```bash
xcrun simctl openurl booted "myapp://product/123"
```

### Web
Simply navigate to the URL in the browser.

## Troubleshooting

### Deep link not opening app
- Check intent filters (Android) / Info.plist (iOS)
- Verify scheme matches exactly
- Test with explicit URL

### Web 404 errors
- Configure web server for SPA
- Use hash strategy if server config not possible

### Route not found
- Ensure GoRouter path matches deep link
- Check for trailing slashes differences
- Verify parameter extraction logic

### Security warnings
- Use App Links / Universal Links instead of custom schemes
- Verify SSL certificates
- Validate deep link data
