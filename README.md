# Generating a Signed Android App Bundle (AAB) from a Flutter Project

This guide will walk you through the process of creating a signed Android App Bundle (AAB) for your Flutter project. The AAB is a publishing format required for uploading your app to the Google Play Store. Follow these steps to ensure your app is properly signed and ready for distribution.

![image](https://github.com/SaadARazzaq/Signed-AAB-from-Flutter-Project/assets/123338307/204b7d3f-653f-4fd6-b110-e5147ead3785)


## Introduction

The Android App Bundle (AAB) is a publishing format that contains all the code and resources needed to build your app. Google Play then generates optimized APKs for each device configuration from the AAB. Here's how to create one for your Flutter app.

## Prerequisites

- [Flutter](https://flutter.dev/docs/get-started/install) installed on your system.
- Specific IDEs such as [Android Studio](https://developer.android.com/studio) / [VS Code](https://code.visualstudio.com/download) installed on your system.
- Basic familiarity with the command line.

## Steps

### Step 1: Create a Keystore

A Keystore is a secure container for your app's digital certificates. It's used to sign your app. Open a terminal at your project's root directory and run:

```bash
keytool -genkey -v -keystore <your_keystore_name>.jks -keyalg RSA -keysize 2048 -validity 10000 -alias <your_alias_name>
```
You'll be prompted to set passwords and provide information. Keep these secure!

### Step 2: Configure Key Properties

1. In your project's `android` directory, create a file named `key.properties`.
2. Add the following lines, replacing placeholders with your values:

```bash
storePassword=your_keystore_password
keyPassword=your_key_password
keyAlias=your_alias_name
storeFile=../../your_keystore_name.jks
```

**Ensure `storeFile` points to the correct path. If the given `storeFile=../../your_keystore_name.jks` throws errors and build fails for somehow, then change to original path of jks file. i.e. `C:/Folder/path_of_jks`. The syntax must be as I have given and not like default `C:\Folder\path_of_jks` as it may give errors sometimes** 

### Step 3: Modify app/build.gradle

1. Open `[project]/android/app/build.gradle`
2. Add the following code at the top of the file:

```bash
def keystoreProperties = new Properties()
def keystorePropertiesFile = rootProject.file('key.properties')
if (keystorePropertiesFile.exists()) {
    keystoreProperties.load(new FileInputStream(keystorePropertiesFile))
}
```
In the same file Inside the `android` block, add the signing configuration:

```bash
signingConfigs {
    release {
        keyAlias keystoreProperties['keyAlias']
        keyPassword keystoreProperties['keyPassword']
        storeFile keystoreProperties['storeFile'] ? file(keystoreProperties['storeFile']) : null
        storePassword keystoreProperties['storePassword']
    }
}

buildTypes {
    release {
        signingConfig signingConfigs.release
    }
}
```

And Remove the following:

```bash
buildTypes {
   release {
       // TODO: Add your own signing config for the release build.
      // Signing with the debug keys for now,
       // so `flutter run --release` works.
     signingConfig signingConfigs.debug
   }
}
```

### Step 4: Build the AAB

In your terminal, run the following commands:

```bash
flutter clean
flutter pub get
flutter build appbundle
```

### Results

You've successfully generated a signed Android App Bundle (AAB) for your Flutter project. The AAB is ready for deployment to the Google Play Store!🎉

### Additional Resources

Visit [Official Documentation Website](https://developer.android.com/guide/app-bundle) for more insights!
