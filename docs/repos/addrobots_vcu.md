# AddRobots_VCU

## Build Instructions

This is a pretty much a standard Android Studio project with two modules: `app` and `openCVLibrary	`. The project requires Android Studio's NDK native plugin, so you will need to use Android Studio 2.2+ and install the NDK libraries from the Android Studio SDK Manager.

### OpenCV

We started the project with the OpenCV module into an Android project: [OpenCV4Android](http://docs.opencv.org/2.4/doc/tutorials/introduction/android_binary_package/O4A_SDK.html), but then heavily modified it to fully build the core OpenCV C/C++ library entirely within Android Studio. OpenCV4Android is in java and it requires OpenCV shared libraries for the relevant target CPU platform. Normally, you'd have to build these libraries separately and add them to the project. This project now builds these libraries directly from the OpenCV code during the normal Gradle build. This means, as long as the OpenCV main code is in a directory that's peered to this project, it will build these libraries using CMake and NDK directly from within the Android Studio project build with no manual intervention. (Tho' it takes a long time to build these libraries!) Whatever version of OpenCV you have in the peer directory, Android Studio will build it for you. (We've built 3.1.0, 3.2.0 and 3.3.0 and anticipate it will be easy to continue to upgrade OpenCV at any time.)

The way to organize this is:

	AndroidStudioProjects
		opencv <-- opencv 3.3.0 main project directly from github
		addrobots_vcu <-- directly from the github repo

Gradle in Android Studio can't deal with absolute paths, so you really need a structure like this one above, where the OpenCV main C/C++ source project is relative to the VCU project.

### cmake

The build from Android Studio will invoke a setup file `android.toolchain.cmake`, but this file is not correct to build OpenCV! There is a modified version of this file in the openCVLibrary submodule. Unfortunately, this file requires some knowledge of where it's installed, and for this reason, if you haven't used the directory structure from above, it will not be correct. The standard `android.toolchain.cmake` is sooo close, but it's not quite there yet (Google has been improving it a lot, and now it's just a handful of changes to make it work - hopefull they can make it work 100% with the standard file they ship with Android Studio NDK/CMake.)
                           
## Build Organization Improvements/Goals 
* Get Gradle Plugin/RuleSource to accept absolute paths, so that we can put the FFmpeg (and later OpenCV) repos whenever we want. (e.g. ~/git).
* Use NDK to also natively build OpenCV from the raw git repo so that we can debug the sources.
* Generalize the AutotoolsPlugin class so that it works with *any* autotools-based project.
* Clean-up various messes. It's hard to know best practices in this part of Gradle and with the Android plugin since it's still somewhat new.
