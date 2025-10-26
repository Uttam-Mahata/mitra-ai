# Logging Guidelines for Mitra AI Flutter App

## Overview

This document outlines the logging practices for the Mitra AI Flutter application.

## Logging Approach

### ✅ Use `debugPrint()` for debug logging

Instead of using `print()` for debugging, always use `debugPrint()` from Flutter's foundation library.

```dart
// ❌ DON'T DO THIS
print('User logged in: $userId');

// ✅ DO THIS
debugPrint('User logged in: $userId');
```

### Import Statement

Add this import at the top of your Dart file:

```dart
import 'package:flutter/foundation.dart';
```

## Why debugPrint() instead of print()?

1. **Throttling**: `debugPrint()` automatically throttles output to avoid dropping messages in Flutter's console.

2. **Performance**: In production/release builds, `debugPrint()` can be completely stripped out when combined with proper build configuration.

3. **Flutter Standard**: It's the officially recommended approach by the Flutter team.

4. **Better UX**: Prevents console flooding in development mode.

## When to Use debugPrint()

- Development debugging
- Temporary troubleshooting
- Non-critical informational messages
- Error context during development

## When NOT to Use debugPrint()

- User-facing error messages (use proper error handling)
- Production logging (consider using a proper logging package like `logger`)
- Sensitive information (credentials, tokens, personal data)

## Migration

All existing `print()` statements in the codebase have been replaced with `debugPrint()` as of commit `7d7f0de`.

## Future Considerations

For production logging, consider implementing a proper logging solution like:
- `logger` package for structured logging
- Firebase Crashlytics for crash reporting
- Sentry for error tracking

## References

- [Flutter debugPrint documentation](https://api.flutter.dev/flutter/foundation/debugPrint.html)
- [Flutter logging best practices](https://flutter.dev/docs/testing/errors)
