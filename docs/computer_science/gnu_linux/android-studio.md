---
title: Android Studio
date: 2018-05-17
tags: [ 'android', 'ide' ]
---

# Android Studio

## Debug

### Building gradle stuck/frozen

It's a weird trouble with internet, follow this instructions:

1. Download a new version of gradle, such as gradle-4.3-all.zip, etc., and put
   the file in your AS Gradle location (Mac: go to the Application folder and
   open the package of AS, and put the new gradle in the Gradle folder. PS: If
   your new gradle version folder is not found, then you can create it on your
   own.Windows: like the previous two answers);
1. Disconnect your Wifi or LAN;
1. Open Android Studio 3.0 as usual;
1. DO NOT OPEN YOUR PROJECT IMMEDIATELY, TURN TO THE PREFERENCE PART FIRST;
1. GO TO THE GRADLE PART, DO THE SETTINGS AND SWITCH THE OFFLINE MODE ON;
1. Open the project you want to open;
1. Let AS to index the file and modify the gradle.properties when it is still
   indexing.
1. Turn on you Wifi or LAN, and AS will download the missing file. ATTENTION:
   DO NOT MODIFY YOUR ANDROID MANIFEST OR OTHER FILES WHEN DOWNLOADING
1. Close AS and reopen the project. And everything will be fine. :-)

**Note**: To switch offline mode on (Configure -> Preferences -> search for
   gradle -> then check the work offline radio button) Also when everything is
   done uncheck the offline radio button otherwise errors may occur.

[stackoverflow](https://stackoverflow.com/questions/47110696/android-studio-3-0-stuck-at-building-gradle-project-info)
