# Haelthy Scan 🧾🔍

A modern Flutter app scaffold integrating Firebase Auth, product lookup,
and barcode scanning with clean architecture and Provider state management.

## Overview

Haelthy Scan is a cross-platform Flutter application built with Dart
3.9 that showcases authentication, product data fetching, and barcode
scanning capabilities. It uses Firebase for identity, OpenFoodFacts for
product information, and follows recommended Flutter lints and
structure.

## Features ✨

- 🔐 Authentication: Email/Password and Google Sign-In via Firebase.
- 📷 Barcode Scanning: Fast camera-based scanning with permission handling.
- 🥫 Product Lookup: Names, images, brands from OpenFoodFacts.
- ✨ Smart UI: Animated bottom navigation and responsive layouts.
- 🧠 State Management: Simple, predictable app state using Provider.
- 🌐 Networking: Robust HTTP via Dio (interceptors, retries).
- 🖼️ Image Caching: Smooth product images with cached_network_image.
- 🖥️📱🕸️ Multi-platform: Android, iOS, Web, Linux, macOS, Windows.

### User Flow Highlights 🚶‍♂️ → 📷 → 🥫
- Sign in (Email/Google) → Home → Scan a barcode → View product details.
- Cached images and lightweight state keep interactions snappy.

## Tech Stack 🧩

- Flutter SDK with Dart 3.9
- Firebase Core/Auth
- Google Sign-In
- Provider
- Dio
- OpenFoodFacts
- Permission Handler
- Cached Network Image
- Animated Bottom Navigation Bar

Full list in [pubspec.yaml](pubspec.yaml).

## Project Structure 🗂️

- App entrypoint: [lib/main.dart](lib/main.dart)
- Firebase config: [lib/firebase_options.dart](lib/firebase_options.dart)
- Modules: [lib/modules/](lib/modules)
- Providers: [lib/providers/](lib/providers)
- Services: [lib/service/](lib/service)
- UI: [lib/views/](lib/views)
- Lints: [analysis_options.yaml](analysis_options.yaml)

## Prerequisites ✅

- Flutter SDK installed and in PATH
- Dart SDK 3.9+ (managed by Flutter)
- A configured Firebase project

Verify setup:

```bash
flutter --version
dart --version
```

## Setup ⚙️

1) Install packages and generate platform files:

```bash
flutter pub get
```

2) Configure Firebase (if not already):

- Ensure `flutterfire` has been run to generate
	[lib/firebase_options.dart](lib/firebase_options.dart).
- Android: place `google-services.json` at
	[android/app/google-services.json](android/app/google-services.json).
- iOS/macOS: add `GoogleService-Info.plist` to platform Runner targets as
	applicable.
- Web: confirm `firebase.json` and web configuration.

Helpful guide: https://firebase.google.com/docs/flutter/setup

3) Platform permissions (for camera/barcode):

- Android: review and adjust [android/app/src/main/AndroidManifest.xml](android/app/src/main/AndroidManifest.xml)
	for camera permissions.
- iOS: add camera usage description to Info.plist in
	[ios/Runner/Info.plist](ios/Runner/Info.plist).

## Running ▶️

Start the app on a connected device or emulator:

```bash
# Android
flutter run -d android

# iOS (on macOS with Xcode)
flutter run -d ios

# Web
flutter run -d chrome

# Linux/macOS/Windows (as supported)
flutter run -d linux
flutter run -d macos
flutter run -d windows
```

## Useful Commands 🧰

```bash
# Clean build outputs and fetch packages
flutter clean && flutter pub get

# Analyze with Flutter lints
flutter analyze

# Run tests (if present)
flutter test

# List connected devices
flutter devices
```

## Code Quality 🧹

- Linting rules configured via [analysis_options.yaml](analysis_options.yaml)
	using `flutter_lints`.
- Prefer immutable widgets and small, composable components.
- Keep business logic in services/providers; UI in views/widgets.

## Configuration Notes 🗝️

- Environment secrets (Firebase keys) are managed by platform config files
	and `firebase_options.dart`. Avoid committing private keys beyond required
	client-side configs.
- Assets are loaded from [assets/](assets) as declared in
	[pubspec.yaml](pubspec.yaml).

## Troubleshooting 🛠️

- If packages fail to resolve, run:

```bash
flutter clean && flutter pub get
```

- For Firebase initialization errors, confirm:
	- [lib/firebase_options.dart](lib/firebase_options.dart) exists and matches
		your Firebase project.
	- Platform config files are in expected locations.

- Camera/barcode issues:
	- Verify runtime permissions and manifest/Info.plist entries.
	- Test on a physical device for camera access.

## Contributing 🤝

Pull requests and suggestions are welcome. Please keep changes focused,
linted, and consistent with the existing structure.

