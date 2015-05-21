## Requirements ##
<ul>
<li>Android SDK 2.2 or later - <a href='http://developer.android.com/sdk/index.html'>download</a></li>
<li>Eclipse version 3.5 or later (Eclipse IDE for Java Developers recommended) - <a href='http://www.eclipse.org/downloads/'>
download</a></li>
<li>Android Development Toolkit (ADT) plug-in - <a href='http://developer.android.com/sdk/eclipse-adt.html#installing'>Installing ADT</a></li>
<li>Ant - <a href='http://ant.apache.org/bindownload.cgi'>download</a></li>
<li>JDK 1.6 or later - <a href='http://www.oracle.com/technetwork/java/javase/downloads/jdk-6u25-download-346242.html'>download</a></li>
</ul>

After installing the Android SDK, you may want to put the platform-tools directory in your PATH environment variable, so you can run `adb` easily.

## Build the NativeDriver libraries ##
Check-out the repository with SVN if you have not done so already:
```
$ svn checkout https://nativedriver.googlecode.com/svn/trunk nativedriver --username {Google account e-mail address}
```
The repository that will be downloaded is organized in this manner:
```
nativedriver
  |
  |__android
  |     |__src
  |     |__sample-aut (sample app under test)
  |     |__test (sample test cases that test the sample app under test)
  |
  |__third_party (all the dependencies we need)
```
Next use `ant` to build the NativeDriver libraries:
```
$ cd nativedriver/android
$ ant
```

<p>The libraries are built and stored in the nativedriver/android/build directory:</p>
<ul>
<li><b>server-standalone.jar</b> - this should be linked to your Android application, and runs on the Android device (or emulator). This is the NativeDriver server, and listens for requests to automate the application, such as “start an activity” or “click a UI element”</li>
<li><b>client-standalone.jar</b> - this should be linked to the test, which is the NativeDriver client. It implements a WebDriver API which communicates with the server.</li>
</ul>

These two jar packages are represented by the yellow and green components below - yellow is code that is reused from Selenium WebDriver. Green is original code from NativeDriver.

<img src='http://nativedriver.googlecode.com/files/AndroidNativeDriverArchitecture.png' />

## Import the NativeDriver Sample Projects Into Eclipse ##
<ol>
<li>Start Eclipse</li>
<li>Click the <i>File -> Import...</i> menu item.</li>
<li>Select <i>Existing Projects into Workspace</i> in the <i>General</i> category and click <i>Next</i></li>
<li>Click <i>Select root directory</i> and then click <i>Browse...</i></li>
<li>Open the <code>nativedriver/android/sample-aut/simplelayouts</code> directory in the repository you downloaded</li>
<li>Confirm your screen looks like the below image and click Finish. Repeat the import process for the <code>nativedriver/android/test</code> directory.<br>
<img src='http://nativedriver.googlecode.com/files/ImportingSimplelayouts.png' />
</li>
</ol>

<p>The <code>android-test</code> project you imported contains sample tests written with Android NativeDriver that also serve to test Android NativeDriver itself. The <code>simplelayouts</code> project is an Android app that the sample tests run against.</p>

## Install the simplelayouts app to your device (or emulator) ##

One easy way to do this is to run the app from Eclipse by right-clicking on the `simplelayouts` project, then selecting _Run As->Android Application_.

You can also run this command:
```
adb install nativedriver/android/sample-aut/simplelayouts/bin/simplelayouts.apk
```

## Prepare the Android device to receive NativeDriver requests ##
In the future these steps should be done through code, maybe using an extended `AdbConnection` class. For now, this part must be done manually:

<ol>
<li>At a command-prompt, run this command:<br>
<pre><code>adb shell am instrument com.google.android.testing.nativedriver.simplelayouts/com.google.android.testing.nativedriver.server.ServerInstrumentation<br>
</code></pre>
This restarts the app with instrumentation enabled. The NativeDriver <code>ServerInstrumentation</code> class listens for requests to drive the app on a device port in a JSON Wire Protocol, which is almost identical to <a href='http://code.google.com/p/selenium/wiki/JsonWireProtocol'>that protocol used by Selenium WebDriver</a>
</li>
<li>Enable port forwarding to bind the device port to a port on your PC. This allows the NativeDriver client to communicate with the device through a normal TCP connection.<br>
<pre><code>adb forward tcp:54129 tcp:54129<br>
</code></pre>
You can confirm that the instrumentation is started by running <code>adb logcat</code> and looking for a line like this:<br>
<pre><code>I/com.google.android.testing.nativedriver.server.ServerInstrumentation(  273): Jetty started on port 54129<br>
</code></pre>
</li>
</ol>

## Run the tests ##
<ol>
<li>Right-click one of the three test classes in the <code>android-test</code> project</li>
<li>Select <i>Run As->JUnit Test</i>.</li>
<li>Specify the <i>Eclipse JUnit Launcher</i> as the <i>Preferred Launcher</i>.</li>
<li>Watch the device screen to see the magic!</li>
</ol>