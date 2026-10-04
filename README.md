# MoonBoard

> [!WARNING]  
> This is experimental software in early stage of development. Please report issues you encounter.

MoonBoard is a fork of [Moonlight for Android](https://github.com/moonlight-stream/moonlight-android) that adds virtual reality support via Google Cardboard.

[Moonlight for Android](https://moonlight-stream.org) is an open source client for NVIDIA GameStream and [Sunshine](https://github.com/LizardByte/Sunshine)([F-Droid](https://f-droid.org/packages/com.limelight)).

Moonlight for Android will allow you to stream your full collection of games from your Windows PC to your Android device,
whether in your own home or over the internet.

## About the fork

Transforms stream into two lenses for virtual reality. Screen is visible in static VR scene.
Fork offers extensive customization options for screen curvature and size.
The PiP (Picture-In-Picture) can be enabled in settings for seeing world around you in gogles.

It also offers remote controller via WebUI. Can be accessed via <mobile-ip>:8555/ from other mobile device for intuitive touch gestures.

VR mode requires Android 8.0 (API 26) or newer. A centered reticle is shown while streaming. Press and hold the phone's touchscreen while aiming the reticle at a panel's colored title bar, then move your head to drag the desktop or camera PiP panel; release to drop it. When lens adjustments are unlocked, single-finger horizontal swipes move the lens and two-finger pinches change its scale. See the [VR controls guide](docs/VR_CONTROLS.md) for details.

## Authors

Original Moonlight-Android app authors:

* [Cameron Gutman](https://github.com/cgutman)  
* [Diego Waxemberg](https://github.com/dwaxemberg)  
* [Aaron Neyer](https://github.com/Aaronneyer)  
* [Andrew Hennessy](https://github.com/yetanothername)

Moonlight is the work of students at [Case Western](http://case.edu) and was
started as a project at [MHacks](http://mhacks.org).

MoonBoard fork contributions:

* Yasurolled

Copyright (C) 2026 Yasurolled for MoonBoard fork contributions. Original
Moonlight and third-party copyright notices remain applicable to their
respective work. Development of MoonBoard has been assisted by GitHub Copilot.

The existing Android application ID is retained so MoonBoard can update
existing installations.
