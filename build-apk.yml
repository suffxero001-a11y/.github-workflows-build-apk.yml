name: Build SUFF-TRONICS Android APK

on:
  workflow_dispatch:
  push:
    paths:
      - 'SUFF_TRONICS_BUSINESS_MANAGER_Android_Project.zip'
      - '.github/workflows/build-apk.yml'

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Get project files
        uses: actions/checkout@v4

      - name: Install Java 17
        uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: '17'

      - name: Install Android SDK
        uses: android-actions/setup-android@v4
        with:
          packages: 'platform-tools platforms;android-35 build-tools;35.0.0'

      - name: Install Gradle 8.9
        uses: gradle/actions/setup-gradle@v4
        with:
          gradle-version: '8.9'
          cache-provider: basic

      - name: Extract Android project
        run: unzip -q SUFF_TRONICS_BUSINESS_MANAGER_Android_Project.zip -d extracted

      - name: Build debug APK
        working-directory: extracted/SUFF_TRONICS_BUSINESS_MANAGER
        run: gradle --no-daemon assembleDebug

      - name: Save APK for download
        uses: actions/upload-artifact@v4
        with:
          name: SUFF-TRONICS-Business-Manager-APK
          path: extracted/SUFF_TRONICS_BUSINESS_MANAGER/app/build/outputs/apk/debug/app-debug.apk
          if-no-files-found: error
          retention-days: 14
