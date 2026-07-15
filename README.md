# SiteWatch — Mobile App Project (Capacitor)

This folder wraps the SiteWatch web app (`www/index.html`) into real native
Android and iOS app projects using Capacitor. It is NOT a finished APK/IPA —
compiling native binaries requires Android Studio / Xcode (or a CI runner
with access to Google's/Apple's servers), which this sandbox's network does
not allow. Everything up to that final compile step is done for you.

## What's included
- `www/index.html` — the SiteWatch app (same as the standalone HTML file)
- `android/` — full Android Studio project, ready to open and build
- `ios/` — full Xcode project, ready to open and build
- `.github/workflows/android-build.yml` — GitHub Action that builds a debug
  APK automatically and lets you download it, no local install needed

## Fastest path: get an APK without installing anything
1. Create a new GitHub repo and push this folder to it.
2. GitHub will run the included Action automatically. Go to the repo's
   **Actions** tab, open the latest run, and download the `SiteWatch-debug-apk`
   artifact once it finishes (a few minutes).
3. Transfer the `.apk` to an Android phone and open it to install (you may
   need to allow "Install unknown apps" for your file manager/browser).

## Building Android locally (Android Studio)
1. Install [Android Studio](https://developer.android.com/studio).
2. Open the `android/` folder as a project.
3. Let Gradle sync, then Build > Build Bundle(s)/APK(s) > Build APK(s).
4. Find the APK in `android/app/build/outputs/apk/debug/`.
5. For a signed release build (for Play Store), use Build > Generate Signed Bundle/APK.

## Building iOS locally (requires a Mac)
1. Install [Xcode](https://apps.apple.com/us/app/xcode/id497799835) (Mac only — Apple doesn't allow iOS builds on Windows/Linux).
2. Run `npx cap open ios` from this folder, or open `ios/App/App.xcworkspace` directly in Xcode.
3. Select your Apple Developer team under Signing & Capabilities (a free Apple ID works for testing on your own device; the App Store requires a paid Apple Developer account).
4. Plug in an iPhone (or use the simulator) and hit Run, or Product > Archive to produce an .ipa for TestFlight/App Store.

## Making changes to the app
Edit `www/index.html` (it's the same single-file app), then run:
```
npx cap sync
```
This copies your changes into both the `android/` and `ios/` native projects.

## App identity
- Name: SiteWatch
- Bundle/package ID: com.sitewatch.app
(Both can be changed in `capacitor.config.json` and re-synced.)
