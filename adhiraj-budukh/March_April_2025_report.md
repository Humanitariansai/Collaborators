# March–April 2025 Monthly Report

---

## 1. Development Environment Setup & Initial Flutter Project Work

- Installed **Android Studio Meerkat 2024.3.1**, carefully ensuring all necessary Flutter and Dart plugins were properly installed and configured.
- Imported and successfully ran the Flutter "Hello World" project within Android Studio, deploying and testing it on a physical iOS device using Xcode integration.
- Configured Android Studio with the correct Flutter SDK path, validated device recognition, and set up wireless iPhone deployment to streamline development and testing workflows.

---

## 2. Face Detection Project Initialization & Early Challenges

- Imported the `face_detection_clean` Flutter project into Android Studio and thoroughly verified all dependencies listed in `pubspec.yaml` for compatibility and version correctness.
- Encountered consistent face detection failures traced back to incorrect image metadata, particularly rotation and size parameters that ML Kit requires for accurate detection.
- Identified front camera mirroring as a probable cause of metadata mismatch, triggering further investigation into image processing logic to properly handle mirrored input.

---

## 3. Image Metadata Handling & Dependency Conflict Resolution

- Updated the face detection pipeline to support front camera mirroring by leveraging the Flutter `image` package for image manipulation and metadata correction.
- Discovered version conflicts between dependencies `image ^4.5.4` and `lottie ^2.7.0`, which initially caused build errors and runtime incompatibilities.
- Resolved the conflicts by aligning dependency versions and applying platform-specific conditional logic within `FaceDetectorRepository` to flip images horizontally, ensuring they meet ML Kit's input expectations on both iOS and Android platforms.

---

## 4. Dependency Upgrades & iOS Deployment Configuration

- Migrated ML Kit face detection dependency to the latest stable version `google_mlkit_face_detection: ^0.13.1`, enabling use of advanced features such as `InputImage.fromFile()`.
- Updated the iOS deployment target to version **15.5** within the Podfile and Xcode Build Settings to comply with updated ML Kit iOS compatibility requirements.
- While successful builds were achieved within Xcode, persistent **code signing failures** arose during `flutter run` executions from Android Studio and CLI, specifically citing failures to codesign `Flutter.framework`.

---

## 5. Code Signing Issue Investigation & Resolution Efforts

- Applied multiple remediation strategies including `flutter clean`, `pod install`, re-archiving the app, and meticulously reviewing Code Sign on Copy settings in the Embed Frameworks phase of the Xcode build.
- Verified all provisioning profiles, signing identities, and device registrations were current and correctly configured.
- Confirmed that builds run successfully through Xcode but consistently fail during CLI/Android Studio runs, indicating a discrepancy between the build environments.
- Currently exploring manual code signing methods and scripts for `Flutter.framework` to resolve these discrepancies and enable smooth development iteration.

---

## 6. Bimride Platform Data Migration & Backend Integration

- Initiated data migration processes to transition user and asset records into the new Bimride site environment.
- Refined transformation logic to handle complex data formats and relationships, resolving inconsistencies that arose during initial migration phases.
- Explored Bimride’s backend architecture deeply, focusing on API endpoints, database schema, and integration points to ensure smooth data flow.
- Reconfigured Android Studio project settings to troubleshoot and mitigate recurring face detection failures observed during integration.
- Performed quality assurance checks on migrated datasets to verify accuracy, integrity, and completeness.
- Investigated backend response patterns to ensure compatibility with Bimride’s updated deployment structure.
- Coordinated batch uploads for efficient bulk data migration, minimizing downtime and user impact.
- Conducted comprehensive hands-on testing of Bimride workflows from a user interaction perspective to identify and resolve UI/UX bottlenecks.
- Implemented precise image metadata adjustments in the ML Kit pipeline to enhance face recognition reliability.
- Fine-tuned migration scripts to support additional data models and complex relational mappings between entities.
- Mapped out key functional changes between legacy and updated Bimride systems, documenting discrepancies and transition strategies.
- Debugged camera input handling extensively, optimizing image capture and preprocessing steps to improve face detection accuracy.
- Completed thorough verification of all migrated datasets and submitted detailed logs and reports for internal team review.
- Compiled a comprehensive summary of new learnings related to Bimride’s technology stack, deployment workflows, and user flow improvements.
- Documented the current status of the Android Studio ML Kit face detection blocker, detailing challenges encountered and proposing a clear set of next steps for resolution.

---

## 7. Android Studio Configuration & ML Kit Integration Challenges

- Continued to explore backend structure and key modules of the updated Bimride platform to ensure full understanding of system dependencies and data flow.
- Progressed with ongoing data cleanup and transformation to ensure seamless migration continuity.
- Identified and documented compatibility issues with Android Studio setup on the current development device, impacting build stability and face detection performance.
- Recorded and analyzed initial errors encountered during ML Kit integration, including permission handling, SDK mismatches, and runtime exceptions.
- Migrated an initial set of user and asset records to the new Bimride system as a proof-of-concept for broader migration.
- Investigated necessary SDKs and dependencies required to support ML Kit face detection on Android and iOS platforms.
- Engaged with community support forums, official documentation, and issue trackers to troubleshoot blockers and identify best practices.
- Validated migrated data entries, cross-checked schema consistency, and ensured data integrity post-migration.
- Explored the front-end user flow of the new Bimride site to understand user interactions and optimize future development efforts.
- Attempted fixes for Android Studio build issues related to camera permissions, updating configuration files and AndroidManifest entries.
- Finalized initial migration scripts and performed batch testing to ensure robustness and performance.
- Compiled a detailed summary of blockers related to Android Studio environment and ML Kit integration for team discussion and escalation.
- Consolidated learnings on Bimride’s architecture and user workflows to aid future onboarding and development efforts.

---

## 8. Content Writing & SEO Article Development

- Conducted comprehensive topic research on 24-hour taxi services and airport transportation in Barbados to ensure accurate and relevant content.
- Analyzed formatting, tone, and structure of existing reference articles to align style and ensure consistency across new content.
- Compiled a detailed list of essential SEO keywords, ensuring alignment with client and search engine optimization requirements for the initial article.
- Drafted the outline and main sections of the article titled **“24 Hour Barbados Taxi Service Including Airport Transfers”**, focusing on clarity and reader engagement.
- Wrote a compelling introduction and conclusion, naturally incorporating all required keywords to maximize SEO impact.
- Edited content to ensure uniqueness, improve logical flow, and maintain an accurate 1000-word count.
- Conducted keyword research and analyzed user queries for the second article covering Uber and airport taxi services in Barbados.
- Developed a structured draft discussing Uber alternatives, local taxi options, and booking methods near the airport.
- Verified that target keywords such as **“Uber Taxi Service Number Barbados”** were effectively included without keyword stuffing.
- Finalized the article **“Uber In Barbados Airport Taxi Service Number Near Me”** with detailed formatting, SEO optimization, and clarity refinements.
- Reviewed both articles to ensure originality, correct phrasing, and no overlap in structure or keyword usage.
- Proofread for grammar, readability, and ensured mobile-friendly formatting for all content.
- Prepared a detailed breakdown of daily tasks aligned with article deliverables for timesheet submission accuracy.
- Organized article drafts and saved them in Word and HTML formats for easy client sharing and future publishing.
- Documented keyword placement strategy and metadata suggestions to support ongoing SEO efforts and content marketing plans.

---

## Summary and Next Steps

- Significant progress made in configuring Flutter and Android Studio environments for iOS and Android development, despite challenges with code signing and build inconsistencies.
- Continued refinement of ML Kit face detection integration, focusing on image metadata correction, front camera mirroring, and dependency version alignment.
- Advanced Bimride data migration efforts with successful batch uploads, backend integration, and thorough QA checks.
- Identified and escalated multiple Android Studio and ML Kit blockers requiring team collaboration and possible external support.
- Delivered two fully SEO-optimized articles with comprehensive keyword research, content drafting, editing, and formatting aligned to client expectations.
- Upcoming focus will be on resolving remaining code signing issues, finalizing ML Kit face detection integration, continuing Bimride migration, and initiating new content projects.
