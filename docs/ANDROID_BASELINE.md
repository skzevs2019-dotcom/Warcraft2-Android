# Android baseline: upstream Stratagus port

## Source inspected

Repository: https://github.com/drodin/Stratagus
Branch: `android`
Inspected files:
- `android/app/build.gradle`
- `android/settings.gradle`
- `android/app/src/main/AndroidManifest.xml`
- `android/app/src/main/java/com/drodin/stratagus/StartMenu.java`
- `android/app/src/main/java/com/drodin/stratagus/MySDLActivity.java`
- root `CMakeLists.txt`

## Confirmed facts from the inspected source

- The Android application module uses Android Gradle Plugin 7.2.2.
- It declares compile SDK 32, NDK 23.2.8568313, CMake 3.22.1, min SDK 16 and target SDK 32.
- The native CMake target is `stratagus`.
- The launcher activity is `StartMenu`; gameplay is hosted by SDL activity `MySDLActivity`.
- The manifest forces landscape orientation.
- The start screen has a ZIP import flow. It extracts the selected archive into the app's private files directory and searches for `scripts/stratagus.lua`.
- The user must currently supply an already prepared Wargus data ZIP; the Android app does not itself convert the original Warcraft II archives into Wargus data.
- The current launcher does not automatically import the original Warcraft II archive and does not provide a verified first-run converter.

## Implications for this project

The existing Android port is a useful starting point, but it does not yet meet the requested workflow. The first integration milestone is to automate or clearly guide the conversion of a legally owned Warcraft II copy into Wargus data, then feed the resulting archive to the existing import/extraction path.

Do not claim first-run conversion, Russian localization, music playback, touch improvements, autosave, or Android 13 compatibility until implemented and tested.

## Build configuration note

The upstream Android Gradle files are old (AGP 7.2.2, compile/target SDK 32). Android 13 is API 33. A compatibility and target-SDK update will need a separate tested change; do not blindly upgrade Gradle, AGP, NDK, or CMake without checking the native dependencies.
