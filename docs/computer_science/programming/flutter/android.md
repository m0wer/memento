---
title: Flutter Android
date: 2022-01-16
author: m0wer
---

# Configuration

## build.gradle

### Automatic version code generation from version name

If you use semantic versioning and you don't want to increment the version code
manually, replace the  related config from `android/app/build.gradle` with:

```java
def flutterVersionName = localProperties.getProperty('flutter.versionName')
if (flutterVersionName == null) {
    flutterVersionName = '1.0.0'
}

def semanticVersion = flutterVersionName.split('\\+')
def versionCore = semanticVersion[0]
def build = semanticVersion.length >= 2 ? semanticVersion[1].toInteger() : 0
def (major, minor, patch) = versionCore.tokenize('.').collect{it.toInteger()}
def flutterVersionCode = 1000000 * major + 10000 * minor + 100 * patch + build
```

Then whenever `pubspec.yaml` `version` veriable changes and you build an APK or
appbundle, the version code will be generated from it.

Examples (version name -> version code):

* `1.2.0` -> `1020000`
* `3.0.1+99` -> `3000199`
