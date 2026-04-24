# Channel Types

Channels provide logical multiplexing within a single connection. Each packet is tagged with a channel that determines its purpose and default reliability.

| Code | Name | Default Reliability | Description |
|------|------|---------------------|-------------|
| 0 | Broadcast | Reliable | Server-wide broadcast messages |
| 1 | Acceleration | Unreliable | Accelerometer sensor data (x, y, z) |
| 2 | Touch | Unreliable | Touch input data (multi-touch) |
| 3 | Message | Reliable | RPC invocations (`BMInvoke`) |
| 4 | String | Reliable | String literal messages |
| 5 | Bytes | Reliable | Raw byte chunks (e.g., control scheme transfer) |
| 6 | Gyro | Unreliable | Gyroscope sensor data (x, y, z) |
| 7 | Orientation | Unreliable | Orientation quaternion data (x, y, z, w) |
| 8 | DPad | Reliable | D-Pad directional input (x, y) |

## Notes

- Channels with **Unreliable** default reliability are typically high-frequency sensor data. These can be sent over UDP to minimize latency at the cost of potential packet loss. This never happens with Flash games because they don't support UDP transport.
- The default reliability can be overridden for certain packets. For example, a game can request reliable touch and sensor delivery via `setReliabilityForTouch(x,y)` where x and y can be any combination of 1 (ReliableUnordered) or 2 (ReliableOrdered). The first value sets it for touches while the second sets it for sensors.
- The **Message** channel (3) carries all RPC traffic: registry operations, session commands, and game-specific invocations.
