---
title: Security & Reliability
description: Encryption, backup, recovery
---

# Security & Reliability

## Encryption

- Use proper data encryption for sensitive information.
- Encrypt at rest (e.g. flutter_secure_storage for credentials).
- Use HTTPS for network; never log sensitive data.

## Backup

- Implement data backup mechanisms.
- Support export/import for user data.
- Consider cloud backup where applicable.

## Recovery

- Implement data recovery mechanisms.
- Handle corrupt or invalid data gracefully.
- Provide restore from backup option when possible.
