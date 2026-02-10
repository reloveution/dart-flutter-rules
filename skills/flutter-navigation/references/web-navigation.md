# Web Navigation

## URL Strategies

Flutter web supports two URL strategies for navigation:

### Hash Strategy (Default)

**URL format:** `https://example.com/#/path/to/screen`

**Advantages:**
- No server configuration needed
- Works with all web servers
- Simple setup

**Disadvantages:**
- URLs look less professional
- Share URLs contain hash

**Setup:**
```dart
// No setup required - this is the default
void main() {
  runApp(MyApp());
}
```

### Path Strategy

**URL format:** `https://example.com/path/to/screen`

**Advantages:**
- Clean, professional URLs
- Better for SEO
- More user-friendly for sharing

**Disadvantages:**
- Requires server configuration
- More complex setup

**Setup:**
```dart
import 'package:flutter_web_plugins/url_strategy.dart';

void main() {
  usePathUrlStrategy();
  runApp(MyApp());
}
```

**Required `pubspec.yaml`:**
```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_web_plugins:
    sdk: flutter
```

## Server Configuration

### General SPA Rewrite Rules

All web servers must rewrite requests to `index.html` for path-based routing:

**Nginx:**
```nginx
location / {
  try_files $uri $uri/ /index.html;
}
```

**Apache (.htaccess):**
```apache
<IfModule mod_rewrite.c>
  RewriteEngine On
  RewriteBase /
  RewriteRule ^index\.html$ - [L]
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteRule . /index.html [L]
</IfModule>
```

**Firebase Hosting:**
```json
{
  "hosting": {
    "public": "build/web",
    "rewrites": [
      {
        "source": "**",
        "destination": "/index.html"
      }
    ],
    "cleanUrls": true
  }
}
```

**Vercel (vercel.json):**
```json
{
  "rewrites": [
    { "source": "/(.*)", "destination": "/index.html" }
  ]
}
```

**Netlify (_redirects file):**
```
/* /index.html 200
```

## Browser History API Integration

When using go_router or Router API, Flutter integrates with browser History API automatically:

### Forward/Back Buttons
- Browser back button works automatically
- Browser forward button works automatically
- History state is managed by go_router

### URL Updates
- URL updates when navigating
- Deep links work from external sources
- Bookmarks link to correct state

## Testing Web Navigation

### Local Development
```bash
flutter run -d chrome
# Path strategy works automatically with Flutter dev server
```

### Production
1. Build web app:
   ```bash
   flutter build web
   ```

2. Configure server with SPA rewrite rules

3. Test URLs:
   - `https://yourdomain.com/`
   - `https://yourdomain.com/details/123`
   - `https://yourdomain.com/product/456`

### Common Issues

**404 errors on navigation:**
- Configure SPA rewrite rules on server
- Check file paths are correct

**Hash still appearing:**
- Ensure `usePathUrlStrategy()` called before `runApp()`
- Check `flutter_web_plugins` is in dependencies

**Browser back button not working:**
- Use go_router instead of Navigator
- Ensure Router API is configured

## Hosting at Non-Root Path

If hosting app at subdirectory (e.g., `https://example.com/myapp/`):

### Update base href in web/index.html
```html
<base href="/myapp/">
```

### GoRouter configuration
```dart
GoRouter(
  initialLocation: '/myapp/',
  routes: [
    GoRoute(path: '/myapp/', builder: (context, state) => HomeScreen()),
    GoRoute(path: '/myapp/details', builder: (context, state) => DetailsScreen()),
  ],
);
```

## Performance Tips

1. **Use lazy loading** for route code splitting:
   ```dart
   GoRoute(
     path: '/heavy-screen',
     builder: (context, state) => HeavyScreen(),
     pageBuilder: (context, state) => MaterialPage(
       key: state.pageKey,
       child: HeavyScreen(),
     ),
   )
   ```

2. **Preload routes** for better UX:
   ```dart
   // Preload in background
   WidgetsBinding.instance.addPostFrameCallback((_) {
     GoRouter.of(context).preloadRoutes();
   });
   ```

3. **Minimize route parameters** - prefer query params for optional data

## Accessibility

- Ensure keyboard navigation works
- Test with screen readers
- Provide meaningful page titles
- Use semantic HTML when possible
