---
name: flutter-security
description: Security best practices for Flutter apps. Use when storing credentials, validating input, securing network/API, or preventing XSS.
---

# Flutter Security

## Overview

Data protection, secure storage, input validation, secure communication.

## Reference Files

- [storage.md](references/storage.md) - Sensitive data, API keys, tokens
- [validation-sanitization.md](references/validation-sanitization.md) - Input validation, XSS prevention
- [network-session.md](references/network-session.md) - HTTPS, session, certificate pinning
- [logging.md](references/logging.md) - What not to log

## Quick Reference

- **Storage:** Flutter Secure Storage for keys, tokens, credentials — never SharedPreferences/plain text
- **Input:** Validate client + server; sanitize before display (XSS)
- **Network:** HTTPS always; certificate pinning for critical APIs
- **Session:** Proper session management, token refresh
- **Logs:** Never log passwords, tokens, personal data
