# react-native-ux-cam

[![npm](https://img.shields.io/npm/v/react-native-ux-cam.svg)](https://www.npmjs.com/package/react-native-ux-cam)
[![npm](https://img.shields.io/npm/dt/react-native-ux-cam.svg)](https://www.npmjs.com/package/react-native-ux-cam)
[![npm](https://img.shields.io/npm/l/react-native-ux-cam.svg)](https://github.com/negativetwelve/react-native-ux-cam/blob/master/LICENSE)
[![CircleCI branch](https://img.shields.io/circleci/project/github/negativetwelve/react-native-ux-cam/master.svg)](https://circleci.com/gh/negativetwelve/react-native-ux-cam)

React Native wrapper for [UXCam](https://uxcam.com).

## Setup

```bash
# Yarn
yarn add react-native-ux-cam

# NPM
npm install --save react-native-ux-cam
```

### iOS with react-native and Cocoapods

Add the following to your Podfile:

```ruby
pod 'react-native-ux-cam', path: "../node_modules/react-native-ux-cam"
```

Then run:

```bash
pod install
```

### Android

1.
Go to `android/settings.gradle`
add `include ':react-native-ux-cam'`
and on the following line add `project(':react-native-ux-cam').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-ux-cam/android')` 

2.
Go to `android/app/build.gradle`
add `compile project(':react-native-ux-cam')` under dependencies

3.
Go to `android/app/src/main/java/com/terravion/dbug/MainApplication.java`
add `import com.rnuxcam.rnuxcam.UXCamPackage;`
and `new UXCamPackage(),`

4.
Add the following to your file `android/app/build.gradle` (or add the maven url to your existing repositories section):

```gradle
allprojects {
    // All of React Native (JS, Obj-C sources, Android binaries) is installed from npm
    maven { url "$rootDir/../node_modules/react-native/android" }
    maven { url "http://sdk.uxcam.com/android/" }
}
```

5.
And add this to your file `android/app/src/main/AndroidManifest.xml`, inside your `<application>` tag:

```xml
<service android:name="com.uxcam.service.HttpPostService"/>
```

## Usage

```js
// Import UXCam.
import UXCam from 'react-native-ux-cam';

// Initialize using your app key.
UXCam.startWithKey(key);

// Tag a screen.
UXCam.tagScreenName('my screen');

// Tag a user.
UXCam.tagUserName('John Doe');

// Add a custom tag with properties.
UXCam.addTag('logged-in', {
  isLoggedIn: true,
  isAwesome: true,
});

// Mark a session as a favorite.
UXCam.markSessionAsFavorite();

// Get the url for the current user. Useful for connecting to other
// analytics services. Note, this method is async and returns a promise.
const currentUserUrl = await UXCam.urlForCurrentUser();

// Get the url for the current session. Note, this method is also async.
const currentSessionUrl = await UXCam.urlForCurrentSession();

// Hide a sensitive screen.
UXCam.occludeSensitiveScreen(true);

// Unhide a sensitive screen.
UXCam.occludeSensitiveScreen(false);

// Stop recording and upload data manually.
UXCam.stopApplicationAndUploadData();

// To start a new recording:
UXCam.restartSession();
```

If a method is missing from the official SDK, please send a PR!
