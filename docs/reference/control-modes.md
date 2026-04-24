# Control Modes

Control modes determine what the controller app displays to the user. The game sets the control mode via the `SetControlMode` RPC.

| Ordinal | Name | Description |
|---------|------|-------------|
| 0 | GAME | The main gameplay mode. The controller renders the control scheme UI (buttons, D-Pad, touch surface) and sends input to the game. |
| 1 | TEXT | Text input mode. The controller shows a keyboard and sends typed text to the game. An optional `startString` pre-populates the input field. |
| 2 | NAV | Navigation mode. The controller shows a simplified navigation interface (back, home, select). |
| 3 | WAIT | Waiting/lobby mode. The controller shows a "waiting for game" screen. This is the default mode set when connecting or when the game is loading. |

## Notes

- The default mode on connection is **GAME** (0) once the control scheme has been parsed and rendered.
- The game can switch modes at any time by sending `SetControlMode` with the ordinal and an optional string parameter (only meaningful for **TEXT** mode).
- When the game disconnects or the controller loses connection, the controller reverts to **WAIT** mode.
