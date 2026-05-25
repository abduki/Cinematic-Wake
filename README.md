# Cinematic-Wake
OLED-safe cinematic sleep and wake utility for Windows. Features smooth multi-monitor fading, customizable ambient modes, and an aggressive, multi-strategy smart media detector to prevent unwanted dimming during video and audio playback.
Here is a short repository description and a comprehensive `README.md` file crafted directly from your script's architecture and features.

### GitHub Repository Description

**Short description for the "About" section of your repo:**

> OLED-safe cinematic sleep and wake utility for Windows. Features smooth multi-monitor fading, customizable ambient modes, and an aggressive, multi-strategy smart media detector to prevent unwanted dimming during video and audio playback.

---
# CinematicWake v3.0 

**OLED-safe cinematic sleep & wake for Windows.** CinematicWake replaces the abrupt Windows screen shutoff with smooth, customizable fade-outs and fade-ins. It is designed to protect OLED screens while offering a premium aesthetic. It features a robust smart media detection system that ensures your screen never goes to sleep while you are watching a video or listening to music—even if the media player fails to register standard Windows wake locks.

---

## Key Features

* **Cinematic Transitions:** Custom easing curves (Linear, Ease-In, Ease-Out, Sine) for smooth fade-ins and fade-outs across all connected monitors.
* **Aggressive Smart Media Detection:** A three-tier strategy to prevent sleeping during media playback:
  1. **WASAPI Audio Monitoring:** Uses PowerShell/CoreAudio to detect active audio streams from known browsers and media players (Chrome, VLC, Spotify, etc.).
  2. **Window Title Heuristics:** Scans foreground and background window titles for media indicators (e.g., "YouTube", "▶", ".mkv").
  3. **Powercfg Fallback:** Detects standard system wake locks.
* **Ambient Mode:** A pulsing screen saver mode that can be scheduled or triggered after a specific idle time to prevent OLED burn-in without fully turning off the display.
* **Smart Scheduling:** Define specific hours for CinematicWake or Ambient Mode to be active.
* **Multi-Monitor Support:** Automatically detects and scales black overlays across all active displays.
* **Global Hotkeys (work in progress):** Instantly force sleep or pause the application using customizable keyboard shortcuts.
* **Audio Cues:** Optional generated sine-wave tones for sleep and wake events.

---

## Prerequisites

* **Operating System:** Windows 10 / 11
* **Python:** Python 3.8+
* **Dependencies:**
  * `pystray` (for the system tray icon)
  * `Pillow` (for system tray icon generation)

Install the required packages via pip:
```bash
pip install pystray Pillow

```

---

## Installation & Usage

1. Clone the repository:
```bash
git clone [https://github.com/yourusername/CinematicWake.git](https://github.com/yourusername/CinematicWake.git)
cd CinematicWake

```

2. Run the script:
```bash
python cinematic_wake.py

```

3. The application will start silently and sit in your system tray. Right-click the tray icon to access settings, pause the app, or exit.

*(Note: To run completely silently in the background without a console window, run it using `pythonw.exe` or compile it to a `.exe` using PyInstaller).*

---

## ⚙️ Configuration

CinematicWake generates a configuration file at `~/.cinematic_wake.json` upon first run. You can edit this file directly or via the planned UI.

### Core Settings

| Setting | Default | Description |
| --- | --- | --- |
| `idle_minutes` | `5` | Minutes of inactivity before the screen fades to sleep. |
| `prevent_sleep_media` | `true` | Enables smart media detection to block sleep during playback. |
| `fade_in_ms` / `fade_out_ms` | `1000` / `1500` | Duration of the fade animations in milliseconds. |
| `overlay_color` | `#000000` | Hex code for the overlay color (useful for custom colored sleep). |
| `fade_curve` | `ease_in_out` | Animation style (`linear`, `ease_in`, `ease_out`, `ease_in_out`, `sine`). |
| `show_countdown` | `true` | Displays a visual countdown on screen before fading to black. |

### Ambient Mode Settings

| Setting | Default | Description |
| --- | --- | --- |
| `ambient_mode` | `false` | Enables a pulsing screen mode instead of full black. |
| `ambient_min_alpha` | `0.85` | The lowest opacity the screen will pulse to. |
| `ambient_speed_s` | `8.0` | The duration in seconds of one full ambient pulse cycle. |
| `ambient_schedule_enabled` | `false` | Enables ambient mode only during a specific time window. |

---

## ⌨️ Default Hotkeys
//(work in progress)
* **Force Sleep:** `Win + Alt + L` (Customizable via `hotkey_sleep` and `hotkey_mods`)
* **Pause/Resume App:** `Win + Alt + P` (Customizable via `hotkey_pause` and `hotkey_mods`)

```
