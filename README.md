PBC Translate
=======

PBC Translate (https://github.com/talmai/Plumble) is forked from the Pumble project
(https://github.com/acomminos/Plumble). All changes are available at the github.com repository.

Plumble is a robust GPLv3 Mumble client for Android that uses the [Jumble](https://github.com/Morlunk/Jumble)
protocol implementation.

Building on GNU/Linux
---------------------
    git submodule update --init --recursive
    ./gradlew assembleDebug

Changes required to build
---------------------
In plumble/libraries/Jumble/src/main/jni/Application.mk:

```
APP_ABI := all
APP_STL := c++_static
```

In plumble/libraries/Jumble/build.gradle:

```
android {
    compileSdkVersion 21

    defaultConfig {
    ...
        minSdkVersion 16
        targetSdkVersion 26
    }
}
```

In plumble/libraries/Jumble/src/main/AndroidManifest.xml:

```
<manifest ...>
    <uses-sdk
        android:minSdkVersion="16"
        android:targetSdkVersion="26"/>
...
</manifest>
```

If either of the following errors pop-up:

```
No toolchains found in the NDK toolchains folder for ABI with prefix mips64el-linux-android
No toolchains found in the NDK toolchains folder for ABI with prefix mipsel-linux-android
```

It may be due to the fact that the latest NDK removed support for mips abi,
and earler version of android gradle plugin still check for the existance of mips toolchain. Upgrade your gradle plugin to 3.5
and create the missing folder structure to fool Android Studio. The easiest way would be to symbolic link:

```
# on Mac
cd  ~/Library/Android/sdk/ndk-bundle/toolchains
ln -s aarch64-linux-android-4.9 mips64el-linux-android
ln -s arm-linux-androideabi-4.9 mipsel-linux-android
```