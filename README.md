# MoonBoard

MoonBoard is an experimental Android game-streaming client based on
[Moonlight for Android](https://github.com/moonlight-stream/moonlight-android).
It preserves Moonlight's familiar PC discovery, pairing, streaming, and input
features, and adds a Google Cardboard VR mode that places the streamed screen
in a head-tracked virtual scene.

> [!WARNING]
> MoonBoard is experimental. VR rendering, camera picture-in-picture, and
> device-specific decoder behavior may vary. Back up important data and report
> reproducible problems through the repository's issue tracker.

## Highlights

- Stream games, applications, and the host desktop from a compatible PC.
- Connect to supported NVIDIA GameStream hosts or
  [Sunshine](https://github.com/LizardByte/Sunshine).
- Discover hosts on the local network or add them manually.
- Stream with controller, keyboard, mouse, touchscreen, and supported stylus
  input. Controller support depends on the Android device and connected
  hardware.
- Choose streaming resolution, frame rate, bitrate, video format, audio, and
  other client settings supported by the device and host.
- Use the optional Google Cardboard VR path to view the stream on a virtual
  screen with head tracking.
- Adjust the VR screen distance, size, and curvature, and show an optional
  skybox.
- Optionally show the device's rear camera as a picture-in-picture panel in VR.
- Control VR scene settings from a browser on another device on the local
  network.

## Requirements

- Android 8.0 (API 26) or newer.
- A compatible streaming host running a supported GameStream implementation
  or Sunshine.
- A reliable network between the Android device and host. Ethernet for the PC
  and a strong 5 GHz Wi-Fi connection for the Android device are recommended.
- For VR: a Cardboard-compatible viewer and a device with working motion
  sensors. A physical controller is optional; head tracking and touchscreen
  interaction are used by the VR scene controls.
- For camera PiP: a rear camera and permission to use it. Camera PiP is optional
  and disabled by default.

MoonBoard keeps the existing Android application ID so builds signed with the
matching key can update the existing app installation. The visible app name is
MoonBoard.

## Set up streaming

### Sunshine

1. Install Sunshine on the host PC using the
   [official releases](https://github.com/LizardByte/Sunshine/releases).
2. Complete the initial setup in Sunshine's web interface.
3. Make sure the PC and Android device can communicate over the network.
4. Open MoonBoard. Select the discovered PC, or add its address manually.
5. Pair when prompted by entering the displayed PIN in Sunshine's web
   interface.
6. Select a host application or the desktop to begin streaming.

### NVIDIA GameStream

On compatible NVIDIA hosts that still provide GameStream, enable GameStream in
the host software's SHIELD settings. Discover or add the PC in MoonBoard and
complete pairing by entering the displayed PIN on the host. GameStream
availability depends on the installed NVIDIA software and host configuration;
Sunshine is an alternative host.

For help with manual host setup, Internet streaming, host-side controllers, or
custom applications, see the
[Moonlight setup guide](https://github.com/moonlight-stream/moonlight-docs/wiki).

## VR mode

Enable VR in the app's preferences before starting a stream. The VR renderer
shows the stream on a virtual display and applies Cardboard's per-eye view and
lens distortion. The preferences let you adjust screen distance, size, and
curvature; an optional skybox can fill the background. Available curvature
presets include flat, cinema-style, and gaming-monitor shapes.

The center crosshair indicates gaze direction. Aim at a panel's colored title
bar, press and hold the phone's touchscreen, and turn your head to reposition
the desktop or camera PiP panel. Release to drop the panel. When lens
adjustments are unlocked, horizontal single-finger movement adjusts alignment
and a two-finger pinch changes lens scale. Lens lock prevents accidental lens
adjustments.

See the [VR controls guide](docs/VR_CONTROLS.md) for the interaction steps.

### Camera picture-in-picture

Enable camera PiP in preferences and grant camera permission when Android asks.
The rear-camera image is rendered as a separate movable panel. Disabling PiP or
revoking permission stops camera use. The camera feature is optional and does
not affect normal streaming.

### Browser control panel

When VR mode is enabled, MoonBoard starts an HTTPS control service on port
`8555`. On a device connected to the same reachable network, open:

```text
https://<android-device-ip>:8555/
```

The service uses an app-generated, self-signed certificate, so the browser may
show a certificate warning. Use the control panel only on a network you trust;
anyone who can reach the service may be able to change VR scene settings. The
service can be stopped from its Android foreground notification.

## Build from source

### Prerequisites

- JDK 21 for the Gradle build.
- Android SDK with platform/build tools for API 34.
- Android NDK `27.0.12077973`.
- Git with submodule support.

Initialize the Cardboard SDK submodule before opening or building the project:

```sh
git submodule update --init --recursive
```

Build the VR debug variant from the repository root:

```sh
./gradlew :app:assembleVrModeDebug
```

The APK is written under `app/build/outputs/apk/vrMode/debug/`. To include the
optional x86_64 ABI in addition to arm64-v8a, pass the existing Gradle property:

```sh
./gradlew :app:assembleVrModeDebug -PincludeX64
```

The CI workflow builds the VR debug variant with JDK 21 and the Android SDK.
Release signing is not configured automatically for local builds. Do not commit
keystores, passwords, or signing credentials.

## Project layout

| Path | Purpose |
| --- | --- |
| `app/src/main/java/com/limelight/Game.java` | Streaming activity and selection of the normal or VR surface. |
| `app/src/main/java/com/limelight/vr/` | Cardboard renderer, camera manager, and browser control service. |
| `app/src/main/java/com/limelight/preferences/` | Stream and VR preference loading. |
| `app/src/main/jni/vr/` | Native renderer, Cardboard integration, and JNI bridge. |
| `vendor/cardboard/` | Cardboard SDK git submodule; do not modify it as part of MoonBoard changes. |
| `docs/VR_CONTROLS.md` | VR reticle, panel movement, and lens interaction guide. |

## Reporting problems

When reporting an issue, include:

- Android device model and Android version.
- Host operating system, GPU, and host software/version.
- Whether the problem occurs in VR, normal mode, or both.
- Streaming resolution, frame rate, codec, and relevant app settings.
- Steps to reproduce and relevant logs, with private network details and
  credentials removed.

## Project origin and attribution

MoonBoard is derived from Moonlight for Android. Original Moonlight contributors
include:

- [Cameron Gutman](https://github.com/cgutman)
- [Diego Waxemberg](https://github.com/dwaxemberg)
- [Aaron Neyer](https://github.com/Aaronneyer)
- [Andrew Hennessy](https://github.com/yetanothername)

Moonlight was started by students at [Case Western Reserve
University](https://case.edu/) during MHacks. MoonBoard fork contributions are
maintained by Yasurolled, with development assisted by GitHub Copilot.

Copyright (C) 2026 Yasurolled for MoonBoard fork contributions. Original
Moonlight and third-party copyright notices remain applicable to their
respective work. See [LICENSE.txt](LICENSE.txt) for the repository's license.
