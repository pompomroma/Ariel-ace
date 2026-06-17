# Ariel ACE — 3D RPG Prototype

A self-contained 3D RPG movement/camera prototype with **dual control schemes** for PC and mobile.
A blocky humanoid avatar runs across a sunset field, filmed from a high **over-the-right-shoulder**
third-person camera, with a faithful run-cycle animation and a swirling dust/wind effect.

Built with [Three.js](https://threejs.org/) (loaded from a CDN). **No build step, no npm, no asset
files** — everything is procedural and lives in a single `index.html`.

## Run it on Replit

1. Create a **blank** Replit project.
2. Add these two files (paste their contents):
   - `index.html`
   - `.replit`
3. Press **Run**. Replit serves the static site and the game appears in the webview.

> The `.replit` file runs `python3 -m http.server 8000` (Python 3 ships with Replit).
> If a particular repl has no Python, add a `replit.nix` containing:
> ```nix
> { pkgs }: { deps = [ pkgs.python3 ]; }
> ```

## Run it locally

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

Any static file server works; you can also just open `index.html` in a modern browser.

## Controls

### PC
- **WASD** — move (camera-relative).
- **Click** the screen to capture the mouse, then **move the mouse** to look around (pointer lock — no button needed). **Esc** releases.
- **Shift** — sprint.

### Mobile / touch
- **Left half** — touch and drag to spawn a **dynamic joystick**; drag direction/distance controls movement direction and speed.
- **Right half** — drag to rotate the camera (look).
- Move and look work **simultaneously** (multi-touch).

## How it works

- **Camera-relative movement ("yank"):** the look controls rotate the camera yaw, and the movement
  input is transformed by that yaw each frame — so turning the camera re-aims "forward" and pulls the
  avatar's heading with it.
- **Over-the-right-shoulder camera:** the look-at anchor is offset to the right of the view and raised
  to the avatar's upper body; the camera follows smoothly.
- **Run animation:** a single phase drives contralateral arm/leg swing, a vertical bounce at twice the
  stride frequency, a forward lean, and subtle shoulder/head counter-rotation — blended with an idle
  breathing pose when standing still.

## Requirements

A modern browser with **WebGL**. The game shows a friendly message if WebGL is unavailable or if the
Three.js library cannot be fetched.
