# Hand Control WebApp

Full-screen browser-based hand tracking that drives your PC — click, move, scroll, and swipe using only hand gestures. No installs needed (just a browser).

Forked and heavily modified from [collidingScopes/threejs-handtracking-101](https://github.com/collidingScopes/threejs-handtracking-101).

## How It Works

```
Webcam → MediaPipe (WASM) → Gesture Detection → WebSocket → Local Connector → pyautogui
```

- Everything runs **client-side in the browser** — your video never leaves your machine
- MediaPipe WASM tracks 21 hand landmarks per hand at 30+ FPS
- Gestures are sent via WebSocket to a lightweight Python bridge that drives pyautogui

## Gestures

| Gesture | Action |
|---------|--------|
| **Move hand** → cursor follows index finger | Mouse movement |
| **Pinch thumb + index** | Left click |
| **Pinch thumb + middle** | Right click |
| **Open palm (held)** | Wake / engage |
| **Fist** | Disengage / pause |
| **Swipe left/right** | Navigate (back/forward or tab switch) |
| **Press `F`** | Toggle fullscreen |
| **Click button ⛶** | Toggle fullscreen |

## Quick Start

### 1. Serve the webapp
```bash
python3 -m http.server 8080
```
Then open `http://localhost:8080` in Chrome/Firefox/Edge.

### 2. Start the local connector (for PC control)
```bash
pip install websockets pyautogui
python3 local_connector.py
```

The webapp auto-connects to `ws://127.0.0.1:8124`.

### 3. Standalone mode (no connector needed)
The webapp works as a hand tracking visualizer without the connector. You just won't get cursor/click feedback on your desktop.

## Project Structure
```
index.html          — Main webapp (single file, all logic inlined)
local_connector.py  — Python WebSocket server → pyautogui bridge
```

## License
MIT — original by collidingScopes / stereoDrift
