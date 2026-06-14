[README.md](https://github.com/user-attachments/files/28924261/README.md)
# DocuMaster Pro

A professional Android document management application built with Flutter. Combines document scanning, OCR, PDF editing, file management, format conversion, image editing, and AI-powered features into a single comprehensive tool.

## Features

### 1. Document Scanner
- Camera capture with real-time preview
- Automatic edge detection with visual overlay
- Multi-page scanning with reordering
- Image filters: Color, Grayscale, Black & White, Auto-Enhance, Shadow Removal
- Perspective correction
- Save as PDF or individual images

### 2. OCR (Text Recognition)
- Extract text from scanned documents and images
- Multi-language support: English, Romanian, Hungarian, German, Italian
- Search within recognized text
- Copy and export extracted text (TXT, PDF, DOCX)
- Confidence scoring

### 3. PDF Editor
- Merge, split, reorder, rotate, delete pages
- Compress PDFs with quality levels
- Encrypt/decrypt with password protection
- Add watermarks and page numbers
- Real-time PDF viewer with thumbnail navigation

### 4. PDF Annotation
- Highlight, underline, strike-through text
- Freehand drawing on pages
- Add text boxes, comments, sticky notes
- Digital signature pad
- Color picker and stroke width controls

### 5. File Manager
- Browse files by type (PDF, DOCX, XLSX, PPTX, TXT, MD, CSV, JSON, XML, HTML, Images)
- Create folders, rename, copy, move, delete
- Grid and list view modes
- Sort by name, date, size, type
- Search with filters
- Share files

### 6. Document Converters
- Image to PDF
- PDF to Images
- Word/Excel/PowerPoint to PDF
- Text to PDF
- PDF to Text

### 7. Image Editor
- Crop, resize, rotate
- Adjust brightness, contrast
- Sharpen images
- Format conversion (JPEG, PNG, BMP, WebP)
- Image compression
- Background removal (edge detection)
- Undo/redo history (20 states)

### 8. AI Features
- Summarize PDFs
- Translate documents (EN, RO, HU, DE, IT)
- Explain selected text
- Extract tables from PDFs
- Generate document titles and tags
- Chat with PDF documents

### 9. Search System
- Global search across file names, PDF contents, OCR text, tags
- Recent search history
- Filtered search by content type

### 10. Security
- Biometric authentication (fingerprint/face)
- PIN code protection
- AES-256 encrypted storage
- Secure local database

### 11. Cloud Integration
- Google Drive support
- Dropbox support (framework)
- OneDrive support (framework)
- Optional cloud synchronization

### 12. User Interface
- Material Design 3
- Dark/Light/System themes
- Tablet support with adaptive layouts
- Smooth animations
- Bottom navigation with 6 tabs

## Architecture

```
lib/
├── main.dart                    # Entry point
├── app.dart                     # MaterialApp with theme
├── injection.dart               # Dependency injection (GetIt)
├── config/                      # App configuration
│   ├── constants.dart           # App constants
│   ├── routes.dart              # GoRouter navigation
│   ├── theme.dart               # Light/Dark themes
│   └── extensions.dart          # Dart extensions
├── core/                        # Core utilities
│   ├── errors/                  # Exceptions & Failures
│   ├── usecases/                # Base use case
│   ├── utils/                   # File, date, encryption, permissions
│   └── widgets/                 # Shared widgets
├── data/                        # Data layer
│   ├── datasources/local/       # SQLite DAOs, secure storage, biometrics
│   ├── datasources/remote/      # Cloud APIs (Drive, Dropbox, OneDrive)
│   ├── models/                  # Data models (DTOs)
│   └── repositories/            # Repository implementations
├── domain/                      # Domain layer
│   ├── entities/                # Business entities
│   ├── repositories/            # Repository interfaces
│   └── usecases/                # Use cases (scanner, ocr, pdf, files, ai, auth, cloud)
├── presentation/                # Presentation layer
│   ├── blocs/                   # BLoCs/Cubits for each feature
│   ├── pages/                   # Screens for each feature
│   └── widgets/                 # Page-specific widgets
└── services/                    # Platform services
    ├── pdf_service.dart
    ├── ocr_service.dart
    ├── image_processing_service.dart
    ├── ai_service.dart
    └── thumbnail_service.dart
```

**Architecture Pattern:** Clean Architecture + MVVM + Repository Pattern
**State Management:** flutter_bloc (Cubit)
**Dependency Injection:** GetIt
**Database:** SQLite (sqflite)
**Navigation:** GoRouter

## Prerequisites

- Flutter SDK 3.2.0 or higher
- Dart SDK 3.2.0 or higher
- Android Studio / VS Code
- Android SDK (API 24-34)
- JDK 17

## Setup Instructions

### 1. Install Flutter
```bash
# Verify Flutter installation
flutter doctor

# Enable Flutter desktop support (optional)
flutter config --enable-android
```

### 2. Clone and Setup
```bash
# Navigate to project directory
cd documaster_pro

# Get dependencies
flutter pub get

# For injectable code generation (optional - DI is already manually configured)
# flutter pub run build_runner build --delete-conflicting-outputs
```

### 3. Android Configuration

#### Local Properties
Create `android/local.properties`:
```properties
sdk.dir=/path/to/your/android/sdk
flutter.sdk=/path/to/your/flutter/sdk
```

#### Signing Configuration (Release)
For release builds, configure signing in `android/app/build.gradle`:
```gradle
android {
    signingConfigs {
        release {
            storeFile file("release-key.jks")
            storePassword "your-password"
            keyAlias "your-alias"
            keyPassword "your-password"
        }
    }
}
```

### 4. Google Sign-In Setup (for Google Drive)
1. Create a project in [Google Cloud Console](https://console.cloud.google.com/)
2. Enable Google Drive API
3. Create OAuth 2.0 credentials (Android client)
4. Add your SHA-1 fingerprint
5. Download `google-services.json` and place in `android/app/`
6. Update `android/app/build.gradle` with your application ID

### 5. Run the App
```bash
# Run in debug mode
flutter run

# Run on specific device
flutter run -d <device-id>

# Run in release mode
flutter run --release
```

## Building APK/AAB

### Debug APK
```bash
flutter build apk --debug
```
Output: `build/app/outputs/flutter-apk/app-debug.apk`

### Release APK
```bash
flutter build apk --release
```
Output: `build/app/outputs/flutter-apk/app-release.apk`

### App Bundle (for Play Store)
```bash
flutter build appbundle --release
```
Output: `build/app/outputs/bundle/release/app-release.aab`

### Split APKs per ABI
```bash
flutter build apk --split-per-abi --release
```
Outputs separate APKs for arm64-v8a, armeabi-v7a, x86_64

## Project Statistics

- **Total Dart Files:** 213+
- **Lines of Code:** 20,000+
- **Modules:** 6 (Scanner, PDF Editor, File Manager, Image Editor, AI, Security)
- **Screens:** 25+
- **Use Cases:** 60+
- **Architecture Layers:** 4 (Presentation, Domain, Data, Core)

## Dependencies

### Core
- `flutter_bloc` - State management
- `get_it` - Dependency injection
- `go_router` - Navigation
- `sqflite` - SQLite database
- `flutter_secure_storage` - Encrypted preferences
- `shared_preferences` - Local settings

### UI
- `adaptive_theme` - Theme management
- `google_fonts` - Typography
- `shimmer` - Loading skeletons
- `flutter_slidable` - Swipe actions
- `flutter_speed_dial` - FAB menu
- `flutter_staggered_grid_view` - Grid layouts

### Document & PDF
- `syncfusion_flutter_pdf` - PDF manipulation
- `syncfusion_flutter_pdfviewer` - PDF viewing
- `pdf` - PDF generation

### Camera & OCR
- `camera` - Camera access
- `google_mlkit_text_recognition` - OCR engine
- `image` - Image processing
- `image_cropper` - Image cropping
- `photo_view` - Image zoom/pan

### File System
- `path_provider` - App directories
- `file_picker` - File selection
- `permission_handler` - Runtime permissions
- `open_filex` - Open with system apps
- `share_plus` - File sharing

### Cloud & Auth
- `google_sign_in` - Google authentication
- `googleapis` - Google APIs
- `local_auth` - Biometric authentication

### Charts & Visualization
- `fl_chart` - Charts and graphs

## Permissions

The app requires the following Android permissions:
- `CAMERA` - Document scanning
- `READ_EXTERNAL_STORAGE` - File access
- `WRITE_EXTERNAL_STORAGE` - File saving
- `USE_BIOMETRIC` / `USE_FINGERPRINT` - Biometric auth
- `INTERNET` - Cloud sync and AI features
- `ACCESS_NETWORK_STATE` - Network detection

## Database Schema

### Tables
1. **documents** - Document metadata and file info
2. **folders** - Folder hierarchy
3. **scan_sessions** - Scanning sessions
4. **scan_pages** - Individual scan pages
5. **ocr_results** - OCR text results
6. **annotations** - PDF annotations
7. **cloud_accounts** - Connected cloud providers
8. **app_settings** - Application settings
9. **conversion_jobs** - File conversion tracking

## Contributing

1. Fork the repository
2. Create a feature branch
3. Follow Clean Architecture patterns
4. Write tests for new features
5. Submit a pull request

## License

This project is for educational and development purposes.

## Support

For issues and feature requests, please refer to the project documentation or contact the development team.

---

**DocuMaster Pro** - Professional Document Management for Android
Built with Flutter
