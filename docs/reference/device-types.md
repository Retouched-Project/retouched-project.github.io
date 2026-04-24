# Device Types

Device types identify the role and platform of each participant in the protocol.

| Code | Name | Role | Description |
|------|------|------|-------------|
| 0 | Any | - | Wildcard, matches any device type |
| 1 | Unity | Host | Unity game host |
| 2 | IPhone | Controller | iOS controller app |
| 3 | Flash | Host | Flash (SWF) game host |
| 4 | Android | Controller | Android controller app |
| 5 | Native | Host | Native game host (C/C++) |
| 6 | Palm | Controller | Palm/webOS controller app |
| 7 | Server | Infrastructure | Registry server |

## Roles

- **Host**: A game that accepts controller connections. The server broadcasts host information to controllers via `onHostConnected` / `onList`.
- **Controller**: A mobile app that connects to a game and sends input. Controllers are not broadcast to other controllers.
- **Infrastructure**: The registry server itself. Not broadcast to anyone.
