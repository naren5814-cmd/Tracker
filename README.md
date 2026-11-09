# TNPSC Study Tracker (Android / Flutter)

An offline-first Flutter starter project with:
- Local SQLite storage (study sessions, timetable, tests, settings)
- Start / pause / resume / end study timer
- Daily dashboard and study target
- Custom schedule slots
- Test score entry and history
- Subject-wise and weekly analytics
- Weekly report screen
- Dark / light / system theme
- Native Android home-screen widget scaffold
- Sunday 10 PM weekly notification schedule (local device time)

## Requirements
- Flutter stable SDK (3.24+ recommended)
- Android Studio + Android SDK
- JDK 17
- Android device or emulator

## Run
1. Extract the project.
2. Open terminal in this folder.
3. Run:
   ```bash
   flutter doctor
   flutter pub get
   flutter create . --platforms=android
   ```
4. Confirm package namespace/applicationId is `com.example.tnpsc_study_tracker`.
5. Keep the supplied `MainActivity.kt`, `StudyWidgetProvider.kt`, manifest, XML widget layout and widget info. If `flutter create .` overwrites Android files, restore the supplied files.
6. Run:
   ```bash
   flutter run
   ```

## Build APK
Debug:
```bash
flutter build apk --debug
```
Release:
```bash
flutter build apk --release
```
APK output:
`build/app/outputs/flutter-apk/app-release.apk`

For Play Store / distributable production use, configure your own signing key and test on a physical device.

## Important implementation notes
This is a functional starter, not yet a fully hardened production release:
- Timer is saved to SQLite, but active-session recovery and true background timer behavior should be completed before relying on it for long sessions. Keep the app alive while a session is running in this first build.
- Weekly notification is scheduled locally at Sunday 10 PM. Android may delay inexact alarms due to battery optimization. For exact delivery, request exact-alarm access and implement a native rescheduling receiver; Android does not guarantee exact timing otherwise.
- The weekly report screen calculates the current Monday–Sunday period. A production version should persist a generated weekly snapshot and create/share a PNG/PDF automatically at the scheduled time.
- Widget scaffold is a native Android RemoteViews widget. It currently reads a cached value from native shared preferences; wire the Flutter DB totals into the channel payload and call widget refresh after every session. The starter refresh channel is in place.
- Local-only storage means uninstalling the app can delete data. Export/restore backup should be added before production use.
- Add automated tests, accessibility checks, migration strategy and device-specific testing before release.

## Project layout
```
lib/main.dart
android/app/src/main/AndroidManifest.xml
android/app/src/main/kotlin/com/example/tnpsc_study_tracker/MainActivity.kt
android/app/src/main/kotlin/com/example/tnpsc_study_tracker/StudyWidgetProvider.kt
android/app/src/main/res/layout/study_widget.xml
android/app/src/main/res/xml/study_widget_info.xml
```
