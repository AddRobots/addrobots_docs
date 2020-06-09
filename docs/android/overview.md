## Android Application

The standard Android application supplied by AddRobots lives in a public repo. https://github.com/AddRobots/addrobots_android. We made this repo public so that it's clear what's going on inside. It also provides the opportunity for the larger community to improve the application through fixes or features.

We anticipate for the majority of robot tasks this application will service your needs since mainly it does a few things:

- Detect devices and register them with the cloud
- Shuttle commands and data to/from the motion control running in the cloud
- (Eventually) Update the firmware of devices connected to USB

In the rare cases where you have a specialized task that requires a localized behavior the standard application does not provide,  you can use this project as a starting point for your own effort.

#### Application Build

We build the application using Android Studio and we build every merge to the master branch at CircleCI. The build and publish process is beyond the scope of this documentation, though building from Android Studio is standard and straight-forward and the CI/CD build/test/publish process is mostly learnable from the CircleCI config file.