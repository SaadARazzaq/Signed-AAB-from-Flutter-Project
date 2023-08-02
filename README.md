# Generating a Signed Android App Bundle (AAB) from a Flutter Project

This guide will walk you through the process of creating a signed Android App Bundle (AAB) for your Flutter project. The AAB is a publishing format required for uploading your app to the Google Play Store. Follow these steps to ensure your app is properly signed and ready for distribution.

![image](https://github.com/SaadARazzaq/Signed-AAB-from-Flutter-Project/assets/123338307/204b7d3f-653f-4fd6-b110-e5147ead3785)


## Introduction

The Android App Bundle (AAB) is a publishing format that contains all the code and resources needed to build your app. Google Play then generates optimized APKs for each device configuration from the AAB. Here's how to create one for your Flutter app.

## Prerequisites

- [Flutter](https://flutter.dev/docs/get-started/install) installed on your system.
- Any IDE [Android Studio](https://flutter.dev/docs/get-started/install) / [VS Code](https://flutter.dev/docs/get-started/install) installed on your system.
- Basic familiarity with the command line.

## Steps

### Step 1: Create a Keystore

A Keystore is a secure container for your app's digital certificates. It's used to sign your app. Open a terminal at your project's root directory and run:

```bash
keytool -genkey -v -keystore your_keystore_name.jks -keyalg RSA -keysize 2048 -validity 10000 -alias your_alias_name
