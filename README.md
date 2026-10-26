# OpenImmersive
![OpenImmersive logo, representing a pair of red/blue anaglyphic glasses](OpenImmersiveApp/Media/openimmersive-logo.png)

_A free and open source spatial & immersive video player for the Apple Vision Pro._

Maintained by [Anthony Maës](https://www.linkedin.com/in/portemantho/) & [Acute Immersive](https://acuteimmersive.com/), derived from [Spatial Player](https://github.com/mikeswanson/SpatialPlayer/) by [Mike Swanson](https://blog.mikeswanson.com/). See the [announcement on Medium](https://medium.com/@portemantho/openimmersive-the-free-and-open-source-immersive-video-player-a37f69556d16)!

Because of significant interest in filmmakers for Immersive Video in the early days of the Apple Vision Pro, many developers have built their own players, often derived from Mike's open-source Spatial Player.

OpenImmersive aims to provide this community with a more complete player, with playback controls, error handling, media loading from HLS streaming and from the local photo gallery. The project and code are intentionally kept as concise as possible to find the right balance between turnkey readiness and modifiability.

## Features
* The xcode project contains **OpenImmersiveApp**, the visionOS app, which depends on **OpenImmersiveLib**, an easy-to-integrate Swift package that lives on its own github repository: [https://github.com/acuteimmersive/openimmersivelib](https://github.com/acuteimmersive/openimmersivelib)
* **This player supports immersive and spatial videos in MV-HEVC, AIVU, Side-by-Side and Over-Under formats.**
* Load a video from various sources: photo gallery, local files/documents, HLS streaming playlist URL, or by dragging a video onto the window.
* Control playback with Play/Pause buttons, +15/-15 second buttons, and an interactable scrubber in an auto-dismiss control panel.
* Select resolution/bandwidth and audio track when streaming videos.
* Play AIV with full spatial audio support!
* Add your custom UI panels to the player like the timecode readout built into the app.

## Requirements
* macOS with Xcode 26 or later
* for on-device testing: visionOS 26.0 or later

## Usage
- Clone the repo
- Open the project in Xcode
- Update the signing settings (select the correct development team)
- Select the build target (visionOS Simulator or Apple Vision Pro)
- Run (⌘R)

Or install the app from the [visionOS AppStore](https://apps.apple.com/us/app/openimmersive/id6737087083).

## Integrate OpenImmersive in your project
- Open your visionOS app in xcode.
- Go to File > Add Package Dependencies...
- Copy-paste the repo URL `github.com/acuteimmersive/openimmersivelib` in the search bar at the top right of the popup.
- Click Add Package, and use `import OpenImmersive` to use the lib's classes and structs in your app.

## Contributions
While this project aims to remain relatively concise and lightweight to allow for modifiability, the community could use improvements and new features. Contributions are greatly appreciated!

### Desired improvements:
- Subtitles support
- Improved Spatial Audio support
- Format auto detection from HLS manifest
- SharePlay support

Special thanks to [Zachary Handshoe](https://www.linkedin.com/in/zachary-handshoe/) from [SpatialGen](https://spatialgen.com/) & [Raphael Dobers](https://github.com/rdotrifork) for their contributions.
Special thanks to [SINTEF](https://www.sintef.no/) and [Gassco](https://gassco.eu/) for supporting development.

## MVC MKV playback

With the MVC-enabled OpenImmersiveLib version, **Open from Files** accepts Blu-ray
MVC `.mkv`/`.mk3d` files, and **Enter Stream URL** accepts seekable HTTP(S) MKV
resources. Select MVC explicitly for URLs without a filename extension. The player
uses a rectangular stereo screen; its options panel provides embedded audio-track
selection and eye swapping. Existing HLS, spatial, SBS/over-under and AIV playback
keep their existing paths.

The app permits unencrypted **local-network** HTTP media and requests local-network
access. Remote services should use HTTPS. Servers must return valid byte ranges;
there is no full-file download fallback. SMB and UPnP discovery are not included.

MVC acceptance initially targets M5 Vision Pro. Supported input is progressive,
8-bit, 4:2:0 Blu-ray MVC within 1920×1088, with channel-based PCM output; Atmos/DTS:X
objects, subtitles and general 2D MKV playback are not supported. See the library's
MVC documentation for hardware validation status and native dependency notices.

For integration testing, temporarily point the Xcode package dependency at your
OpenImmersiveLib fork's integration commit (or use a local package override). Do
not include a personal fork override in an upstream app PR. Merge/release the
library support before raising the app's minimum library version.
