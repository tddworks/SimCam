# SimCam

Stream your MacBook camera into the iOS Simulator in real time. Build camera features without a physical device.

## Why

The iOS Simulator has no camera. Any iOS app that opens `AVCaptureDevice` — QR scanners, photo capture, AR previews, live filters — fails or shows black. Teams paper over this with stub images or build-and-install loops, both of which kill iteration speed.

SimCam gives the simulator a live camera feed from your Mac. No extra hardware, no device builds.

## Install

1. Download **`SimCam-1.0.0.dmg`** from the [latest release](https://github.com/tddworks/SimCam/releases/latest).
2. Open the DMG and drag **SimCam** to `/Applications`.
3. Launch SimCam. The menu bar item appears.

> First launch will prompt for camera access. Video stays on your Mac.

## Use

1. Click the SimCam menu bar item.
2. Pick a camera from the **Cameras** list.
3. Click **Start Streaming**.
4. Open any iOS Simulator and launch your app — your Mac camera shows up live.

If your iOS app was already running before you started streaming, SimCam shows a **Reopen** prompt — tap it and SimCam will relaunch the app so it picks up the camera.

### Display controls

- **Fit / Fill** — Fit shows the whole frame (photo-style apps); Fill crops to fill the preview (selfie/social apps).
- **Mirror On / Off** — flip horizontally for selfie-style preview.

Both apply live; no restart needed.

## Requirements

- macOS 14 (Sonoma) or later, Apple Silicon
- Xcode 26 with the iOS 26.4 Simulator runtime *(tested)*

## Privacy

- Video stays on your Mac.
- The macOS camera permission prompt at first launch is the only system-level interaction.

## Troubleshooting

**The iOS app shows a black preview.**
The app was launched before you hit Start Streaming. Use the **Reopen** prompt in the SimCam HUD, or quit and relaunch the app from the simulator.

**SimCam says "Blocked".**
Either no camera is selected, or no iOS simulator is booted. The HUD names the gap and the fix.

**Camera access denied.**
Open *System Settings → Privacy & Security → Camera* and toggle SimCam on.
