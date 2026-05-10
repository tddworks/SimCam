# SimCam

Stream your MacBook camera into the iOS Simulator in real time. Build camera features without a physical device.

```
MacBook camera ─▶ SimCam (menu bar) ─▶ iOS Simulator ─▶ any AVCaptureDevice client
```

## Why

The iOS Simulator has no camera. Any iOS code path that opens `AVCaptureDevice` — QR scanners, photo capture, AR previews, anything reading an `AVCaptureSession` — fails or renders black. Teams paper over this with stub images or build-and-install-to-device loops, both of which kill iteration speed.

SimCam gives the simulator a live frame feed from the host Mac's camera. Zero extra hardware, no device builds, integrates with the same `AVFoundation` mental model your production code expects on real devices.

## Install

1. Download **`SimCam 1.0.0.dmg`** from the [latest release](https://github.com/tddworks/SimCam/releases/latest).
2. Open the DMG and drag **SimCam** to `/Applications`.
3. Launch SimCam. The menu bar item appears.

> First launch will prompt for camera access. SimCam never sends video off your Mac.

## Use

1. Click the SimCam menu bar item.
2. Pick a camera from the **Cameras** list.
3. Click **Start Streaming**.
4. Open any iOS Simulator and launch your app — calls to `AVCaptureDevice` now return live frames from your Mac camera.

If your iOS app was already running before you started streaming, SimCam shows a **Reopen** prompt — tap it and SimCam will relaunch the app so it picks up the camera.

### Display controls

- **Fit / Fill** — Fit shows the whole frame (WYSIWYG, photo-style apps); Fill crops to fill the preview (selfie/social apps).
- **Mirror On / Off** — flip horizontally for selfie-style preview.

Both apply live; no restart needed.

## Requirements

- macOS 14 (Sonoma) or later
- Xcode 26 with the iOS 26.4 Simulator runtime *(tested)*

Older Xcode and iOS Simulator versions are not supported.

## How it works

SimCam ships a small dylib that gets injected into iOS Simulator processes via `DYLD_INSERT_LIBRARIES`. The dylib hooks `AVCaptureDevice` so that any sim app's camera path receives BGRA frames published by the host Mac app. Frames travel over a shared-memory file (the iOS Simulator bind-mounts the host's `/private/tmp`), so the path is zero-copy and sub-millisecond.

No network, no per-app configuration, no tweaks to your iOS source.

## Privacy

- Video stays on your Mac. SimCam does not open any network sockets for frame data.
- The macOS camera permission prompt at first launch is the only TCC interaction.
- Open source — read the source if you want to verify.

## Troubleshooting

**The iOS app shows a black preview.**
The app was launched before you hit Start Streaming. Use the **Reopen** prompt in the SimCam HUD, or quit and relaunch the app from the simulator.

**SimCam says "Blocked".**
Either no camera is selected, or no iOS simulator is booted. The HUD names the gap and the fix.

**Camera access denied.**
Open *System Settings → Privacy & Security → Camera* and toggle SimCam on.

## License

MIT — see [LICENSE](LICENSE).
