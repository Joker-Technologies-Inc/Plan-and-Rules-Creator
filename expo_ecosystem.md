# Expo Ecosystem Overview

## 1. Expo Framework

Expo provides a managed and bare workflow on top of React Native,
enabling app development with or without native code customization.

### Managed Workflow

-   Zero native code needed
-   Install native APIs with `expo install`
-   Configure via `app.json`

### Bare Workflow

-   Full native control
-   Still supports Expo modules and EAS services

------------------------------------------------------------------------

## 2. Expo Modules & APIs

Expo includes 100+ ready-to-use native modules such as: - Camera -
Notifications - Audio & Video - Sensors - SecureStore - Location -
FileSystem - ImagePicker - Fonts - Splash Screen - Haptics - Crypto

These modules offer unified APIs that work across iOS, Android, and
sometimes Web.

------------------------------------------------------------------------

## 3. Expo Tooling

### Expo CLI

Command-line tools for running and managing apps:

    npx expo start
    npx expo prebuild
    npx expo install

### Expo Go

-   Scan QR code to preview app instantly
-   No building required during development

### Expo Router

A file‑based navigation system similar to Next.js.

Example structure:

    app/
     ├─ index.js
     ├─ settings.js
     └─ profile/
         └─ [id].js

### Expo DevTools

A browser dashboard for logs, devices, and project controls.

### Snack

An online editor to run React Native code instantly at
https://snack.expo.dev.

------------------------------------------------------------------------

## 4. Expo Application Services (EAS)

### EAS Build

Cloud builds for: - iOS `.ipa` (no Mac required) - Android `.aab` /
`.apk`

Supports: - Development builds - Preview builds - Production builds

### EAS Submit

Uploads built binaries to: - App Store Connect - Google Play Console

### EAS Update

Push over-the-air (OTA) updates to users: - Fix UI - Update logic -
Deploy JS changes No rebuild required.

### EAS Device

Manage iOS device registration for testing.

### EAS Metadata

Store and manage App Store / Play Store metadata from config.

------------------------------------------------------------------------

## 5. Community & Extras

-   Third-party modules optimized for Expo (Firebase, RevenueCat,
    Sentry, OneSignal, etc.)
-   Expo config plugins to extend native behavior
-   UI kits compatible with Expo (NativeBase, Tamagui, RN Paper, Expo
    UI)

------------------------------------------------------------------------

## Summary Table

  Category             Includes
  -------------------- ---------------------------------------------------
  **Framework**        Managed + Bare workflows, Expo SDK
  **Modules**          Camera, Notifications, Sensors, SecureStore, etc.
  **Tooling**          Expo CLI, Expo Go, Expo Router, Snack
  **Cloud Services**   EAS Build, Update, Submit, Device, Metadata
  **Community**        Config plugins, UI libraries, third‑party modules

------------------------------------------------------------------------

## Conclusion

The Expo ecosystem provides a complete stack for building modern mobile
apps with React Native---covering development, native APIs, builds, OTA
updates, and store deployment. It simplifies all stages of app creation
while remaining flexible for advanced native needs.
