# Packet Types

The packet type field in `BMPacket` indicates the purpose of the packet.

| Code | Name | Description |
|------|------|-------------|
| 0 | Data | Application data payload (the default for all game traffic) |
| 1 | Ping | Latency probe sent by one peer, expects an Echo in response |
| 2 | Ack | Acknowledgment of a received connection request |
| 3 | Echo | Response to a Ping packet |
| 4 | Analysis | Performance/diagnostic metrics |
| 5 | KeepAlive | Connection liveness signal, no response expected |

## Notes

- Nearly all protocol traffic uses **Data** (0). The other types are for connection health and diagnostics.
- **Ping** packets are responded to with **Echo**. The original Android app measured round-trip time using timestamps embedded in the Ping payload. The same **Ping** packet is sent back as an **Echo** packet type.
- **Ack** is used with `AckPacket` (class ID 9). The game sends an Ack after receiving a connection request relayed through the server. This is not to be confused with a TCP ACK.
- **KeepAlive** is fire-and-forget. It keeps NAT mappings alive and detects dead connections via timeout, but does not require a response.
