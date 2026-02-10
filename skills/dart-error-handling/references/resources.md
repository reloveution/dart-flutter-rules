---
title: Resource Cleanup
description: Close sinks, avoid leaks
---

# Resource Cleanup

## Close Sinks

- Close sinks (StreamController, IOSink) after use.
- Call `close()` in dispose or when done.
- Ensure cleanup runs even on error paths.

## Leaks

- Prevent resource leaks.
- Don't leave subscriptions, file handles, or connections open.
- Use try-finally or `await for` with proper disposal.
