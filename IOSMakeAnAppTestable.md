# Making An iOS App Testable with NativeDriver #

To drive your iOS application, you should link NativeDriver library into your application. NativeDriver will listen port 3001 in your application and respond to WebDriver requests.

You can make your application testable with following steps.

## 1. Import iPhoneNativeDriver project into your project ##

First of all, you should import NativeDriver project into your project so that you can set target dependency and linkage settings.

1.1. Open your project in Xcode. Select your project and click "Add Files to ..." in the context menu.

<img src='http://nativedriver.googlecode.com/files/IosMakeTestable01.png' />

1.2. Select "NativeDriver.xcodeproj" and click "Add" button.

<img src='http://nativedriver.googlecode.com/files/IosMakeTestable02.png' />

## 2. Add header search path ##

We will call NativeDriver from your `main.m` to start server. `NDNativeDriver.h` should be in header search paths.

2.1. Select target in your project. You can create new target to run NativeDriver automation.

2.2. Open "Build Settings" tab for the target.

2.3. Add path to nativedriver/iphone/Classes to "Header Search Paths".

<img src='http://nativedriver.googlecode.com/files/IosMakeTestable03.png' />

## 3. Add linker flags ##

NativeDriver library uses Objective-C categories feature. To prevent linker to removing necessary object, you should add some linker flags.

3.1. Add `"-ObjC"` and `"-all_load"` to "Other Linker Flags".

<img src='http://nativedriver.googlecode.com/files/IosMakeTestable04.png' />

## 4. Add target dependencies ##

Add target dependency so that NativeDriver will be built before building your app.

4.1. Open Build Phases tab.

<img src='http://nativedriver.googlecode.com/files/IosMakeTestable05.png' />

4.2. Add `"NativeDriver"` to "Target Dependencies".

<img src='http://nativedriver.googlecode.com/files/IosMakeTestable06.png' />

## 5. Add frameworks to link with ##

You should link NativeDriver and related frameworks into your project.

5.1. Add `"libNativeDriver.a"`, `"libCocoaHTTPServer.a"`, `"CFNetwork.framework"`, and `"libstdc++.dylib"` to "Link Binary With Libraries".

<img src='http://nativedriver.googlecode.com/files/IosMakeTestable07.png' />

## 6. Add codes to start NativeDriver ##

NativeDriver will start with `[NativeDriver start]` message. You can add this message in `main.m`.
NativeDriver works only in testing purpose. You can define "Preprocessor Macros" in the build settings.

6.1. import `"NDNativeDriver.h"` and call `[NDNativeDriver start];` in `main.m`.

<img src='http://nativedriver.googlecode.com/files/IosMakeTestable08.png' />