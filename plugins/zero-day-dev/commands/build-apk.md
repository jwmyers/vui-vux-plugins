---
name: build-apk
description: Build APK for Board hardware deployment
allowed-tools: "*"
argument-hint: [output-path]
---

# Build APK

Build the Zero-Day Attack APK for Android/Board deployment.

## Process

1. Verify build settings are correct for Board hardware:

   - Platform: Android
   - Scripting Backend: IL2CPP
   - Target Architecture: ARM64
   - API Level: 33

2. Guide user through Unity build process:

   - Open File > Build Settings (or Build Profiles in Unity 6)
   - Ensure Android platform selected
   - Click Build

3. If output path provided, use that location. Otherwise default to `Builds/ZeroDayAttack.apk`

4. Report build status

## Build Settings Reference

Required configuration:

- **Platform**: Android
- **Minimum API Level**: Android 13 (API 33)
- **Scripting Backend**: IL2CPP
- **Target Architecture**: ARM64 only
- **Application ID**: com.earplay.zerodayattack

## Notes

- Unity must be open with the project loaded
- Build process runs within Unity Editor
- Check Unity Console for any build errors
- Ensure Android SDK is properly configured
