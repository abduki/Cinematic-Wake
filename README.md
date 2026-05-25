# Cinematic-Wake

OLED-safe cinematic sleep and wake utility for Windows. Features smooth multi-monitor fading, customizable ambient modes, and an aggressive, multi-strategy smart media detector to prevent unwanted dimming during video and audio playback.

---

## Overview

CinematicWake replaces the abrupt Windows screen shutoff with smooth, customizable fade-outs and fade-ins. It is designed to protect OLED screens while offering a premium aesthetic. It features a robust smart media detection system that ensures your screen never goes to sleep while you are watching a video or listening to music—even if the media player fails to register standard Windows wake locks.

## Key Features

* **Cinematic Transitions:** Custom easing curves (Linear, Ease-In, Ease-Out, Sine) for smooth fade-ins and fade-outs across all connected monitors.
* **Aggressive Smart Media Detection:** A multi-tier strategy to prevent sleeping during media playback:
1. **Windows Media API (SMTC):** Uses native Windows System Media Transport Controls to detect active media (Spotify, browsers, streaming apps) universally.
2. **WASAPI Audio Monitoring:** Uses PowerShell/CoreAudio to detect active audio streams from known processes.
3. **Window Title Heuristics:** Scans window titles for media indicators.
4. **Powercfg Fallback:** Detects standard system wake locks.


* **Ambient Mode:** A pulsing screen saver mode that can be scheduled or triggered after a specific idle time to prevent OLED burn-in without fully turning off the display.
* **Smart Scheduling:** Define specific hours for CinematicWake or Ambient Mode to be active.
* **Multi-Monitor Support:** Automatically detects and scales black overlays across all active displays.
* **Global Hotkeys:** Force sleep or pause the application using customizable keyboard shortcuts.
* **Audio Cues:** Optional generated sine-wave tones for sleep and wake events.

## Prerequisites

* **Operating System:** Windows 10 / 11
* **Python:** Python 3.8+
* **Dependencies:**
* `pystray`
* `Pillow`
* `winsdk`



Install the required packages via pip:

```bash
pip install pystray Pillow winsdk

```

## Installation & Usage

1. Clone the repository:

```bash
git clone https://github.com/yourusername/CinematicWake.git
cd CinematicWake

```

2. Run the script:

```bash
python cinematic_wake.py

```

3. The application will start silently and sit in your system tray. Right-click the tray icon to access settings, pause the app, or exit.

*Note: To run completely silently in the background without a console window, run it using `pythonw.exe`.*

4. To compile as an executable:

```bash
pyinstaller --noconsole --onefile cinematic_wake.py

```

## Configuration

CinematicWake generates a configuration file at `~/.cinematic_wake.json` upon first run.

### Core Settings

| Setting | Default | Description |
| --- | --- | --- |
| `idle_minutes` | `5` | Minutes of inactivity before the screen fades to sleep. |
| `prevent_sleep_media` | `true` | Enables smart media detection to block sleep during playback. |
| `fade_in_ms` | `1000` | Duration of the fade-in animation in milliseconds. |
| `fade_out_ms` | `1500` | Duration of the fade-out animation in milliseconds. |
| `overlay_color` | `#000000` | Hex code for the overlay color. |
| `fade_curve` | `ease_in_out` | Animation style (`linear`, `ease_in`, `ease_out`, `ease_in_out`, `sine`). |
| `show_countdown` | `true` | Displays a visual countdown before fading. |

### Ambient Mode Settings

| Setting | Default | Description |
| --- | --- | --- |
| `ambient_mode` | `false` | Enables a pulsing screen mode instead of full black. |
| `ambient_min_alpha` | `0.85` | The lowest opacity the screen will pulse to. |
| `ambient_speed_s` | `8.0` | The duration in seconds of one full pulse cycle. |
| `ambient_schedule_enabled` | `false` | Enables ambient mode only during a specific time window. |

## Hotkeys

* **Force Sleep:** `Win + Alt + L`
* **Pause/Resume App:** `Win + Alt + P`

## License

no licence
