---
name: dart-resource-management
description: Resource lifecycle and disposal for Dart/Flutter. Use when managing Timer (cancel in dispose), StreamController, subscriptions, animations, network cancellation, file/DB handles, native resources, or preventing memory leaks.
---

# Dart Resource Management

## Overview

Resource lifecycle: Timer, subscriptions, streams, animations, network, files, DB, native resources, app lifecycle.

## Reference Files

See detailed documentation for each topic:

- [timer.md](references/timer.md) - Timer vs Future.delayed, cancellation
- [subscriptions-dispose.md](references/subscriptions-dispose.md) - Cancel, nullify
- [stream-controllers.md](references/stream-controllers.md) - Close in dispose
- [images-database-files.md](references/images-database-files.md) - Images, DB, file handles
- [network-animations-futures.md](references/network-animations-futures.md) - Network cancel, animations, pending futures
- [native-resources.md](references/native-resources.md) - Camera, sensors
- [scoping-lifecycle.md](references/scoping-lifecycle.md) - Scoping, pause/resume/dispose
- [memory.md](references/memory.md) - Memory monitoring

## Quick Reference

- **Timer:** Use Timer; cancel in dispose; nullify after cancel
- **Subscriptions:** Cancel in dispose; nullify variable
- **StreamController:** Close in dispose
- **Animations:** Dispose controllers and tickers
- **Network:** Cancel requests when widget disposed
- **Futures:** Check mounted; avoid completing for disposed widgets
- **Scope:** Match resource lifetime to owner scope
