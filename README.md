# ESRC Heart SDK for JavaScript

[![Platform](https://img.shields.io/badge/platform-JAVASCRIPT-orange.svg)](https://github.com/esrc-official/ESRC-Heart-SDK-JavaScript)
[![Languages](https://img.shields.io/badge/language-JAVASCRIPT-orange.svg)](https://github.com/esrc-official/ESRC-Heart-SDK-JavaScript)
[![Commercial License](https://img.shields.io/badge/License-Commercial-brightgreen.svg)](https://github.com/esrc-official/ESRC-Heart-SDK-JavaScript/blob/master/LICENSE.md)

## Table of contents

  1. [About ESRC Heart SDK](#about-esrc-heart-sdk)
  1. [Install ESRC Heart SDK](#install-esrc-heart-sdk)
  1. [Making your first recognition](#making-your-first-recognition)

<br />

## About ESRC Heart SDK

Through our **ESRC Heart SDK** for JavaScript, you can efficiently integrate real-time recognition of heart response and emotions into your mobile app. This and other pages in the Getting Started provide the ESRC Heart SDK’s structure and installation steps, then goes through the preliminary steps of implementing the ESRC Heart SDK in your own project.

<!-- ### Supported browsers

| Browser|Supported versions|
| :---: | :--- |
| Internet Explorer | 10 or higher |
| Edge | 13 or higher |
| Chrome | 16 or higher |
| Firefox | 11 or higher |
| Safari | 7 or higher |
| Opera | 12.1 or higher |
| iOS Safari | 7 or higher |
| Android Browser | 4.4 (Kitkat) or higher |  -->

### Key functions

|Function|Description|
|---|---|
|Measurement Environment Analysis| Analyze measurement environment including brightness. |
|Face Detection| Detect a single face using a front camera on mobile. |
|Heart Rate Estimation| Estimate heart rate from facial color variations and head movements caused by heartbeat using Remote Photoplethysmography and Ballistocardiography. |
|Heart Rate Variability Analysis| Extract 19 variables of heart rate variability reflecting autonomic nervous system activity from the accumulated heart rates. |
|Engagement Recognition| Recognize engagement level from balance of autonomic nervous system by heart rate variability analysis. |


### Try the sample app

Our sample app has the core features of the ESRC Heart SDK. Download the app from our [GitHub repository](https://github.com/esrc-official/ESRC-Heart-JavaScript) to get an idea of what you can build with the actual SDK and start building in your project.

> Note: The fastest way to see our ESRC Heart SDK in action is to build your app on top of our sample app. Make sure to change the application ID of the sample app to your own.


## Install ESRC Heart SDK

This page provides a step-by-step guide that demonstrates how to build and configure an in-app bio-analysis using the ESRC Heart SDK.

### Step 1: Download and install the ESRC Heart SDK

If you're familiar with using external libraries or SDKs, installing the ESRC Heart SDK is simple. You can install the ESRC Face SDK with package manager `npm` by entering the command below on the command line.

- **Npm**

> Node: To use npm to install the ESRC Heart SDK, Node.js must be first installed on your system.

```bash
$ npm install @esrc/heart (request to npm server)
```

Install via `Npm` and import like below in your `JavaScript` file.

```javascript
// Define a global variable 'Module' with a method 'onLoadedESRC'
Module = {
    onLoadedESRC() {
        // do somthing...
    }
}
// Load '@esrc/heart' assinging the value to the global variable 'ESRC'
require("@esrc/heart");
```

### Step 2: Download and install the assets

Download the `assets` file from our [GitHub repository](https://github.com/esrc-official/ESRC-Heart-SDK-JavaScript/tree/master/assets). Copy the downloaded assets file into your project directory.

## Making your first recognition

The ESRC Heart SDK simplifies vision features into an effortless and straightforward process. To recognize your facial expression, do the following steps:

This page provides a step-by-step guide that demonstrates how to build and configure an in-app bio-analysis using ESRC Heart SDK. License key can be received by requesting by the email: **esrc@esrc.co.kr**.

### Step 1: Initialize the ESRC Heart SDK

Initialization binds the ESRC Heart SDK to JavaScript, thereby allowing it to use a camera in your mobile. To the `initWithApplicationId()` method, pass the **App ID** of your ESRC application to initialize the ESRC Heart SDK and the **ESRCLicenseHandler** to received callback for validation of the App ID.

```javascript
// Initialize ESRC
ESRC.initWithApplicationId("APP_ID", (isValid) => {
    if (isValid) {
        // Application ID is valid, so do somthing...
    } 
});
```

> Note: The `ESRC.initWithApplicationId()` method must be called once across your web app. It is recommended to initialize the ESRC Heart SDK in the `onLoadedESRC()` method of the Application instance.

### Step 2: Start the ESRC Heart SDK

Start the ESRC Heart SDK to recognize your facial expression. To the `start()` method, pass the `ESRCProperty` to select analysis modules and the `ESRCHandler` to handle the results. You should implement the callback method of `ESRCHandler` interface. So, you can receive the results of face, heart rate, heart rate variability and emotion. Please refer to **[sample app](https://github.com/esrc-official/ESRC-Heart-JavaScript)**.

```javascript
// Initialize property
var property = new ESRCType.ESRCProperty(
    true,  // Whether analyze measurement environment or not.
    true,  // Whether detect face or not.
    true,  // Whether estimate remote hr or not.
    true,  // Whether analyze HRV or not. If enableRemoteHR is false, it is also automatically set to false.
    true  // Whether recognize engagement or not. If enableRemoteHR is false, it is also automatically set to false.
);

// Initialize handler
var handler = new ESRCHandler();
handler.onAnalyzeMeasureEnv = function(measureEnv) {
    // do something...
}
handler.onDetectedFace = function(face) {
    // do something...
}
handler.didChangedProgressRatioOnRemoteHR = function(progressRatio) {
    // do something...
}
handler.onEstimatedRemoteHR = function(remoteHR) {
    // do something...
}
handler.didChangedProgressRatioOnHRV = function(progressRatio) {
    // do something...
}
handler.onAnalyzedHRV = function(hrv) {
    // do something...
}
handler.onRecognizedEngagement = function(engagement) {
    // do something...
}
// Start ESRC
ESRC.start(property, handler);
```

### Step 3: Feed the ESRC Heart SDK

Feed `ESRCType.ESRCMat` on the ESRC Heart SDK. To the `feed()` method, pass the `ESRCType.ESRCMat` image received using a camera in real-time. Please do it at 10 fps or higher.

```javascript
ESRC.feed(ESRCMat);
```

### Step 4: Stop the ESRC Heart SDK

When your app is not use the camera or destroyed, stop the ESRC Heart SDK.

```javascript
ESRC.stop()
```


## Changelogs

### v0.1.5 (JUNE 28, 2022)

If you want to check the record of other versions, go to [Change Log](https://github.com/esrc-official/ESRC-Heart-SDK-JavaScript/blob/master/CHANGELOG.md).

- Initial draft.