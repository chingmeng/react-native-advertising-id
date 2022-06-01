
# react-native-advertising-id
[![npm version](https://badge.fury.io/js/react-native-advertising-id.svg)](https://badge.fury.io/js/react-native-advertising-id)

Consistent access to Advertising Id (AAID/GAID and IDFA) for Android and iOS on React Native.

## TOC

- [react-native-advertising-id](#react-native-advertising-id)
  - [TOC](#toc)
  - [Getting started](#getting-started)
    - [Manual installation (If auto-linking not available)](#manual-installation-if-auto-linking-not-available)
      - [iOS](#ios)
      - [Android](#android)
      - [Post Installation](#post-installation)
  - [Usage](#usage)
    - [OTHERS ISSUES](#others-issues)

## Getting started

`$ npm install react-native-advertising-id --save`

`$ react-native link react-native-advertising-id` // If you are under RN 0.60.0 below where auto-linking not born yet.

### Manual installation (If auto-linking not available)

#### iOS 

1. In XCode, in the project navigator, right click `Libraries` ➜ `Add Files to [your project's name]`
2. Go to `node_modules` ➜ `react-native-advertising-id` and add `RNAdvertisingId.xcodeproj`
3. In XCode, in the project navigator, select your project. Add `libRNAdvertisingId.a` to your project's `Build Phases` ➜ `Link Binary With Libraries`
4. Run your project (`Cmd+R`)<

#### Android

1. Open up `android/app/src/main/java/[...]/MainActivity.java`
  - Add `import info.applike.advertisingid.RNAdvertisingIdPackage;` to the imports at the top of the file
  - Add `new RNAdvertisingIdPackage()` to the list returned by the `getPackages()` method
2. Append the following lines to `android/settings.gradle`:
    ```gradle
    include ':react-native-advertising-id'
    project(':react-native-advertising-id').projectDir = new File(rootProject.projectDir, 	'../node_modules/react-native-advertising-id/android')
    ```
3. Insert the following lines inside the dependencies block in `android/app/build.gradle`:
    ```gradle
      compile project(':react-native-advertising-id')
    ```

#### Post Installation
 Update your `mainfest.xml` and add in your Admob app id (Yes, for later version, you need admob app id):
```xml
<manifest>
    <application>
    <meta-data
            android:name="com.google.android.gms.ads.APPLICATION_ID"
            android:value="ca-app-pub-3940256099942544~3347511713"/> // This is sample-id for testing only, don't use it in PRODUCTION!!! You will get banned for life!
    </application>
</manifest>

```

## Usage
`react-native-advertising-id` module provides a method `getAdvertisingId()` that returns a Promise.
This resolves in an object containing `advertisingId` as a string representing the GAID/AAID or IDFA depending on the platform, and `isLimitAdTrackingEnabled` indicating wether the user opted to restrict the usage of his AdvertisingId or not. (Note: If enabled on iOS, advertisingId will result in an empty string).
```javascript
import RNAdvertisingId from 'react-native-advertising-id';

  RNAdvertisingId.getAdvertisingId()
    .then(response => {
      this.setState({
        advertisingId: response.advertisingId,
        isLimitAdTrackingEnabled: response.isLimitAdTrackingEnabled,
      });
    })
    .catch(error => console.error(error));
```
  
### OTHERS ISSUES

https://groups.google.com/g/google-admob-ads-sdk/c/fmbPnkUCIe8