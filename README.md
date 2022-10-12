# cordova-plugin-google-signin

Cordova plugin for integrating Sign in with Google in Android &amp; iOS app. 
It is updated to the latest Google Signin SDK on iOS `6.1` with support for M1 chip.

Based on https://github.com/russmedia-digital/cordova-plugin-google-signin with Firebase removed and Client IDs renamed and rationalised.

## Description

The plugin allows you to authenticate users with Sign in with Google on iOS and Android. 
The API allows you to get email, display name, profile picture url, user id and idToken.
Android additionally supports One Tap Login.

## Installation

### Google Cloud console: Oauth Requests

Go to https://console.cloud.google.com/apis/credentials/consent and select your project at the top if need be.
Then select "External" and fill out the details on the next page.

### Google Cloud console: credentials

Go to https://console.cloud.google.com/apis/credentials and select your project at the top if need be.
Create "Web application", "Android" and "IOS" OAuth 2.0 Client IDs.

### Web application credentials

Once created, copy the Client ID to use as the SERVER_CLIENT_ID.

Your app can pass a received "id_token" to the server for it to use with this Client ID.

### Android app credentials

Register app by providing the package name, nickname and SHA-1 key. 
The package name should be the same you used during creation of the Cordova project. 
If you're not aware about the package name or have modified it, open the android project in Android Studio and note the applicationId from app module's build.gradle file.

You can get the SHA-1 key using the following command, debug SHA-1:

    keytool -list -v -alias <your-key-name> -keystore <path-to-production-keystore>

For the debug keystore, you can use the below command (default password is "android"):

    keytool -list -v -alias androiddebugkey -keystore ~/.android/debug.keystore

You'll need to add the SHA-1 for the release keystore for the production build to work. Use the above commmand by replacing the path to your release keystore file.

### iOS App credentials

Provide the bundle ID for the app and the name.
The Bundle ID should be the same you used during creation of the cordova project. 
In case you're not aware or have modified it, you can find the bundle ID by opening the iOS project in Xcode.

Once created, copy the Client ID and use it as IOSAPP_CLIENT_ID.
The Client ID can also be found in the plist file.

The plist file should be downloaded and saved as `GoogleService-Info.plist`.


## Install the plugin in your cordova project

You should have the value for the SERVER_CLIENT_ID and IOSAPP_CLIENT_ID handy before you install the plugin.
SERVER_CLIENT_ID is the server-side "Web application" Client ID.
IOSAPP_CLIENT_ID is the "iOS" app Client ID. The Android Client ID is not needed.

    cordova plugin add https://github.com/Freegle/cordova-plugin-google-signin --save --variable SERVER_CLIENT_ID="serverclientid" --variable IOSAPP_CLIENT_ID="iosappclientid"

## Usage

```javascript
cordova.plugins.GoogleSignInPlugin.signIn(
  function (authData) {
    // {
    //   "status": "success",
    //   "message": {
    //     "id": "",
    //     "display_name": "",
    //     "email": "",
    //     "photo_url": "",
    //     "id_token": ""
    //   }
    // }
    console.log(authData);
  },
  function (error) {
    console.error(error);
  }
);

cordova.plugins.GoogleSignInPlugin.isSignedIn(
  function (success) {
    console.log(success);
  },
  function (error) {
    console.error(error);
  }
);

cordova.plugins.GoogleSignInPlugin.signOut(
  function (success) {
    console.log(success);
  },
  function (error) {
    console.error(error);
  }
);

// Android only
cordova.plugins.GoogleSignInPlugin.oneTapLogin(
  function (success) {
    // {
    //   "status": "success",
    //   "message": {
    //     "id": "",
    //     "display_name": "",
    //     "email": "",
    //     "photo_url": "",
    //     "id_token": ""
    //   }
    // }
    console.log(success);
  },
  function (error) {
    console.error(error);
  }
);
```
