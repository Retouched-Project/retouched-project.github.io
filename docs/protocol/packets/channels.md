# Channels

The `channel` field in [`BMPacket`](bm-packet.md) provides logical multiplexing within a single connection. Each channel is associated with a specific type of payload and a default reliability mode.

See the [Channel Types Reference Table](../../reference/channel-types.md) for the complete list of values.

## Purpose

Channels serve two functions:

1. **Payload routing**: The channel value tells the receiver what type of message to expect in the packet's `message` field.
2. **Reliability selection**: Each channel has a default reliability mode that determines whether the packet is sent over TCP or UDP. See [Reliability Modes](../../reference/reliability-modes.md) for details.

## Per-Channel Sequence Numbers

Each channel maintains its own independent sequence counter. When a packet is sent on a given channel, the sequence number is drawn from that channel's counter, not a shared global counter. This allows the receiver to detect gaps or reordering within a specific data stream without interference from traffic on other channels.

## Common Patterns

- **Channel 3 (Message)** is used for all RPC traffic (`BMInvoke`). This includes registry operations, session setup, sensor configuration, and game-specific method calls. Always reliable.
- **Channel 5 (Bytes)** is used for `BMByteChunk` transfers, such as delivering the control scheme XML from the game host to the controller. Always reliable.
- **Channel 0 (Broadcast)** is used for Ping/Echo keep-alive traffic.
- **Sensor channels** (1, 2, 6, 7) carry high-frequency input data and default to unreliable (UDP) transport, though this can be overridden.