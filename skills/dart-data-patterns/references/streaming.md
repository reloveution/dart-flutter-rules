---
title: Real-time & Streaming
description: Streams for live data updates
---

# Real-time & Streaming

## Streams

- Use streams for real-time data updates.
- Expose `Stream<T>` from repositories for reactive data.
- Combine with StreamBuilder, Bloc, Riverpod stream providers in Flutter.

## Use Cases

- WebSocket messages
- Database change streams (e.g. drift watch)
- Periodic polling with broadcast streams
- Live query results

## Best Practices

- Cancel subscriptions in dispose.
- Handle stream errors and completion.
- Use broadcast streams when multiple listeners needed.
