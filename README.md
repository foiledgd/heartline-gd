# Heartline

A standalone Windows app that connects a Bluetooth heart-rate monitor to a customizable overlay in Geometry Dash.

**Version 1.5.0 · Windows x64 · Geometry Dash 2.2081**

## Features

- **24 overlay designs** with transparent backgrounds.
- **16 colour palettes** and custom heart, accent, and text colours.
- Live BPM previews and a heart animation that speeds up with your heart rate.
- Adjustable spacing, size, position, opacity, and pulse strength.
- Automatic Geometry Dash detection through running processes and Steam libraries.
- All overlay controls in the app, with preferences saved between sessions.
- One executable with the Geode mod and desktop overlay built in.
- No account, subscription, or cloud service required.

## Getting started

You only need **`Heartline.exe`** to run the app. No loose mod files, Python, .NET, or separate Visual C++ runtime installation are required.

1. Close Geometry Dash and any older copy of Heartline.
2. Open `Heartline.exe` and click **Connect GD**.
3. Turn on Bluetooth, wake or wear your monitor, select it, and click **Connect**.
4. Choose an overlay and adjust it in the **Design**, **Layout**, and **Options** tabs.
5. Open Geometry Dash. Keep Heartline running while you play; minimizing it is fine.

If GD is not found, open the game and try **Connect GD** again. **… → Locate GD manually** is available for installations outside the detected locations. Close GD before installing or updating the Geode mod.

## Geode and standalone overlay modes

| Mode | How it works | Requirements and limits |
| --- | --- | --- |
| Geode | Installs the mod embedded in the EXE and renders inside the game. | Built for GD 2.2081 and Geode 5.11.2. Supports exclusive fullscreen and gameplay-only visibility. |
| Desktop overlay | Draws a transparent, click-through overlay over the foreground GD window. | Works without Geode in windowed or borderless mode. Does not support exclusive fullscreen or gameplay-only visibility. |

Heartline selects the desktop overlay when Geode is not detected. Nothing else needs to be downloaded. This mode hides when GD is minimized or another app is in the foreground.

The Geode package keeps the filename `kamil.pulsoid_heart.geode` so it replaces earlier versions. Overlay settings are controlled in Heartline; the mod has no description page or settings panel in Geode.

## Customize your overlay

| Tab | Controls |
| --- | --- |
| **Design** | Overlay style, palette, custom colours, and automatic BPM text colours. |
| **Layout** | Size, heart/text spacing, horizontal and vertical position, opacity, and pulse strength. |
| **Options** | Show/hide the overlay, animation, heart and number visibility, stacked layout, hide when offline, gameplay-only visibility, Demo mode, and heart-colour threshold. |

Size ranges from **50–200%**. Heart/text spacing ranges from **0–80 overlay units**.

### Designs

Pixel, Clean, Outline, Neon, Ring, Minimal, Arcade, Pixel Outline, Crystal, Dual Tone, Orbit, Radar, Crosshair, Spark, Wings, Crown, Pulse Line, Cyber, Ribbon, Double Ring, Circuit, Glitch, Aurora, and Halo.

### Live readings and previews

Every gallery preview follows the connected monitor's current BPM. Before a live reading arrives, the app shows a labelled **PREVIEW**. Demo mode is separate and labels the game overlay **DEMO**. Example values are never published as live sensor readings.

The animation follows the reported BPM: **60 BPM = one pulse per second**, **120 BPM = two**. It does not reproduce the exact timing of individual measured beats. Automatic colour changes are decorative.

## Supported monitors

Heartline is designed for Bluetooth LE monitors that expose the standard **Heart Rate service (`180D`)** and **Heart Rate Measurement characteristic (`2A37`)**. This includes the Polar H10 and other monitors using that standard.

Your PC needs a Bluetooth LE adapter. Proprietary-only watches and ANT+-only sensors cannot connect directly. A device having Bluetooth alone does not guarantee compatibility.

## Troubleshooting

| Problem | Try this |
| --- | --- |
| Monitor is missing | Wake it, check its battery, and scan again. Try **… → Show all Bluetooth devices**. |
| Windows pairing fails | Try **Connect** directly first. If the monitor requires pairing, use **… → Pair selected device**. |
| Connection fails | Close other active sensor connections on phones, watches, or fitness apps. Click the status line for details. |
| BPM stops updating | Check sensor contact and battery. Heartline clears the live number after reported contact loss or 15 seconds without a usable reading. Reconnect if necessary. |
| BPM appears in the app but not GD | Enable **Show overlay**. With Geode, click **Connect GD** while the game is closed, then restart GD. Without Geode, use windowed or borderless mode and bring GD to the foreground. |
| Mod installation is blocked | Your Windows account needs write access to the game's `geode/mods` folder. Heartline does not elevate itself to administrator. |

Use **… → Copy status** when reporting connection issues. Include your Windows version, monitor model, app version, and whether you are using Geode or the desktop overlay.

## Local operation and performance

Bluetooth work runs on a background thread outside Geometry Dash. The Geode mod reads a small local shared-memory feed at 10 Hz, with animation updates capped at 30 Hz. This keeps Bluetooth operations off the game's main thread; actual FPS impact has not been measured.

Heartline does not upload readings or save heart-rate history. Preferences are stored in:

```text
%LOCALAPPDATA%\Heartline\settings.ini
```

Closing Heartline disconnects the monitor and removes the desktop overlay. Turning off the overlay or enabling Demo does not disconnect the monitor.

## Build from source

The prebuilt EXE does not need build tools. To rebuild, use an **x64 Developer PowerShell** with Git, Python 3, CMake, the Geode CLI, and the Visual Studio C++ tools installed.

From the source folder, run:

```powershell
.\Build-Windows.ps1
```

The script builds the mod and embeds it into `build-companion/Release/Heartline.exe`. It does not install anything into your game. See `BUILD.md` in the source package for exact prerequisites, pinned dependencies, and validation commands.

## Testing status

The app and mod compile successfully. Automated checks cover heart-rate packets, shared-memory message validation, artwork bounds, pulse timing, Steam library parsing, the startup manifest, and the embedded mod package.

**Actual Windows startup, physical Bluetooth connections, installation on a gaming PC, in-game rendering, and FPS impact still need runtime testing.** See `VALIDATION.txt` in the source package for details.

## Uninstall

Close Heartline and GD, delete `Heartline.exe`, and remove `kamil.pulsoid_heart.geode` from `geode/mods` if installed. To remove saved preferences too, delete `%LOCALAPPDATA%\Heartline`.

## License

MIT. Keep the copyright and license notice in `LICENSE` when redistributing the project. Dependency notices are included in `THIRD_PARTY_LICENSES.txt`.
