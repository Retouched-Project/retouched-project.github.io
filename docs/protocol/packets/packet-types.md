# Packet Types

The `packetType` field in [`BMPacket`](bm-packet.md) determines how the packet should be handled by the receiver.

See the [Packet Types Reference Table](../../reference/packet-types.md) for the complete list of values.

## Behavior

### Data (0)

The default packet type of all application traffic. The receiver looks up the sender by `deviceId` and dispatches the packet to the corresponding device handler. If no matching device is found, the packet is dropped.

### Ping (1)

A latency probe. The receiver changes the `packetType` to Echo (3) and sends the packet back as-is, preserving the original `timestamp`. This allows the sender to calculate the round-trip time.

### Ack (2)

A connection acknowledgment sent by the game host to the controller in response to a `deviceConnectRequested` relay. The `message` field contains an `AckPacket` (class ID 9), which carries two nested objects: a `Device` (the game host's identity) and a `BMAddress` (the game host's connection address and ports). Upon receiving an Ack, the controller registers the game host as connected and establishes the direct connection.

### Echo (3)

The response to a `Ping`. Contains the original `timestamp` from the `Ping`, allowing the sender to calculate RTT by comparing against the current time.

### Analysis (4)

Presumably intended for performance or diagnostic metrics. Not observed in normal protocol operation.

### KeepAlive (5)

A heartbeat signal sent to maintain the connection. No response is expected.