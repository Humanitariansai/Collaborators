# February 2025 Monthly Report

## 1. Flutter Environment Setup
- Installed Flutter SDK and Xcode, and configured the development environment specifically for iOS.
- Created the first Flutter app using `CupertinoApp` with a basic “Hello World” screen.
- Explored the Flutter project structure and successfully tested the app on a physical iPhone device.

## 2. Flutter UI Foundations and Navigation
- Built the foundational app structure with `CupertinoApp`, `CupertinoPageScaffold`, and implemented tab navigation.
- Used `CupertinoTabBar` to enable switching between key pages: Home, Profile, and Settings.
- Managed dynamic states in the app using `StatefulWidget` (e.g., counter functionality).
- Handled routing and navigation with Flutter’s `Navigator` widget.

## 3. Multi-Screen UI Development & Interactivity
- Designed and implemented multiple app screens, including Counter, Notes, and Profile, using Cupertino UI components.
- Integrated user input handling with `CupertinoTextField` and managed page transitions using `CupertinoNavigationBar` and buttons.
- Developed interactive features such as editing and saving user profile data via `TextEditingController`.

## 4. Integration of Real-Time Music Data and Audio Playback
- Fetched real-time music data from the iTunes API using the `http` package.
- Displayed fetched music information in a list format.
- Implemented dynamic search functionality using `CupertinoSearchTextField`.
- Loaded album artwork thumbnails efficiently using `CachedNetworkImage`.
- Added audio playback capabilities with the `audioplayers` package, including play/pause controls and proper state management.

## 5. Notes App with Local Persistence
- Developed a fully functional Notes app with Cupertino styling.
- Enabled users to add, view, and delete notes.
- Used the `sqflite` package to create and manage a local SQLite database (`notes.db`) containing a notes table.
- Ensured persistence of notes across app restarts.
- Handled text input focus and management with `CupertinoTextField`.

## 6. Flutter Face Detection Project Setup
- Initialized a new Flutter project focused on face detection using Google’s ML Kit.
- Structured the app following clean architecture principles and implemented state management with the BLoC pattern.
- Added necessary dependencies: `camera`, `google_mlkit_face_detection`, `flutter_bloc`, `image_picker`, and `lottie`.
- Faced iOS-specific CocoaPods issues, including “Podfile.lock not in sync” and missing file errors, resolved through `flutter clean` and re-installing pods.

## 7. Camera Integration and Initial Face Detection Attempts
- Implemented the camera screen using the front camera for image capture.
- Set up BLoC events and states to manage image capture and face detection flows.
- Observed that ML Kit consistently returned “No face detected” despite faces being present in images.
- Modified face detection logic to use `InputImage.fromFile()` for improved metadata handling.
- Added detailed logging to verify image capture paths and processing flow.
- Despite correct camera initialization, detection failure persisted on iOS.

## 8. Advanced Debugging of Face Detection Failures
- Manually provided detailed `InputImageData` including rotation, image size, and image format (e.g., nv21).
- Increased image resolution and added delays after capturing images to ensure files were saved correctly before processing.
- Encountered exceptions related to invalid enum usage, confirming ML Kit was not recognizing faces properly.

## 9. iOS Environment and Dependency Management
- Fully removed and reinstalled CocoaPods.
- Re-linked all plugins and verified the iOS build environment.
- Confirmed that TensorFlow Lite and ML Kit initialized properly but still returned zero face detections.
- Decided to pivot approach by exploring real-time face detection using camera image streams instead of still images for potentially better accuracy.

## 10. Continued Debugging and Project Refinements
- Captured device sensor orientation and preview size from the `CameraController` to improve metadata accuracy.
- Refactored BLoC to accept image, size, and rotation data, passing these to the detection repository.
- Upgraded `google_mlkit_face_detection` dependency from version ^0.9.0 to ^0.13.1 for improved iOS compatibility.
- Updated iOS deployment target from 12.0 to 14.0 in the Podfile and resolved related CocoaPods version conflicts.
- Performed clean rebuilds of the iOS workspace using `flutter clean`, `flutter pub get`, and `pod install --repo-update`.

## 11. Current Status and Next Steps
- Integrated rotation and camera preview size into the ML Kit detection pipeline with `InputImageData`.
- Despite upgrades and environment fixes, face detection still returned zero results on iOS.
- Ongoing debugging and testing to identify root causes of detection failure.
- Planning to implement real-time face detection using camera image stream to potentially overcome current limitations.