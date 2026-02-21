# APEX cam (Nextgen2026)

Android camera app that records high-speed video at **240 FPS** or **120 FPS**.

## What it does

- Records first (no visible live preview while recording)
- Saves the MP4 to device storage (MediaStore) under `Movies/Pro240Camera/`
- Writes a sidecar JSON metadata file (same base name) containing FPS, timestamp, ISO, shutter
- Allows playback in-app (Media3/ExoPlayer) and opening in the gallery

## Controls

- FPS: 240 / 120
- Resolution: 1920×1080 / 1280×720 / 640×480 (filtered by device support)
- ISO: manual sensor sensitivity
- Shutter: manual exposure time in microseconds (µs)

## Build / Run

1. Open this folder in Android Studio.
2. Let Gradle sync (Android Studio will prompt to download the required Android Gradle Plugin / Gradle).
3. Run the `app` configuration on a device that supports high-speed video.

## Install Android SDK (Windows)

Recommended (easiest): install **Android Studio**.

1. Android Studio → **More Actions** → **SDK Manager**.
2. Install:
	- **Android SDK Platform 34** (or latest)
	- **Android SDK Build-Tools**
	- **Android SDK Platform-Tools**
3. Note the SDK location shown (commonly: `C:\Users\<you>\AppData\Local\Android\Sdk`).

Android Studio will typically create/update a `local.properties` file automatically with:

`sdk.dir=C:\\Users\\<you>\\AppData\\Local\\Android\\Sdk`

For this machine, your SDK is at:

`C:\Users\santh\AppData\Local\Android\Sdk`

To make `adb` available in terminals, add this to your **PATH**:

`C:\Users\santh\AppData\Local\Android\Sdk\platform-tools`

After updating PATH, open a NEW terminal and verify:

`adb --version`

Optional environment variables (helps some tools):

- `ANDROID_SDK_ROOT=C:\Users\santh\AppData\Local\Android\Sdk`
- `ANDROID_HOME=C:\Users\santh\AppData\Local\Android\Sdk`

Optional (command line): You can also install the “Android SDK Command-line Tools” and use `sdkmanager`, but Android Studio’s SDK Manager is the simplest.

If you want to build from the command line / VS Code tasks:

- Generate a Gradle wrapper (once): `gradle wrapper` (requires Gradle available in your PATH), or use Android Studio to run the `wrapper` task.
- Then run: `./gradlew.bat assembleDebug`

Generating wrapper from Android Studio (if `gradle` isn’t on PATH):

1. Android Studio → **View → Tool Windows → Gradle**.
2. In the Gradle tool window: `Pro240Camera` → `Tasks` → `build setup` → `wrapper`.
3. Double-click `wrapper`.

This will create `gradlew.bat` / `gradlew` and the wrapper files so VS Code tasks work.

Videos save to `Movies/Pro240Camera/` and the JSON metadata sidecar is saved alongside it.

## Build APK output

- Debug APK: `./gradlew.bat assembleDebug`
	- Output: `app/build/outputs/apk/debug/app-debug.apk`
- Release APK (requires signing): `./gradlew.bat assembleRelease`
	- Output: `app/build/outputs/apk/release/app-release.apk`

From Android Studio you can also use **Build → Build Bundle(s) / APK(s) → Build APK(s)**.

## Device support notes

High-speed capture (120/240fps) depends heavily on the device camera HAL.
If 240fps at 1080p is not supported on your device, pick a smaller resolution or 120fps.


