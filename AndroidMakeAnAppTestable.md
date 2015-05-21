## Making an Android App Testable with NativeDriver ##

The Android NativeDriver (AND) works as instrumentation in your app. It starts a Jetty server on the device which listens for WebDriver JSON protocol requests. In order to make an application run this instrumentation, and respond to these WebDriver requests:

<ol>
<li>Link <b>server-standalone.jar</b> to your application (if you already have an eclipse Android project for your test target, right click the project, Build Path -> Configure Build Path... -> Libraries -> Add JARs or Add External JARs). If you have not built the <b>server-standalone.jar</b> file yet, follow the steps under <i>Build the NativeDriver libraries</i> in the <a href='http://code.google.com/p/nativedriver/wiki/GettingStartedAndroid'>Getting Started</a> documentation.</li>
<li>In the app's <b>AndroidManifest.xml</b> file, add the following elements in the <code>&lt;manifest&gt;</code> element:<br>
<pre><code>  &lt;instrumentation android:targetPackage="{app_package_name}"<br>
   android:name="com.google.android.testing.nativedriver.server.ServerInstrumentation" /&gt;<br>
  &lt;uses-permission android:name="android.permission.INTERNET" /&gt;<br>
  &lt;uses-permission android:name="android.permission.WAKE_LOCK" /&gt;<br>
  &lt;uses-permission android:name="android.permission.DISABLE_KEYGUARD" /&gt;<br>
</code></pre>
The first element enables the instrumentation against your application. <code>{app_package_name}</code> is the name of the package as specified by the manifest element's package attribute. The other lines are permissions to enable testing by AND:<br>
<ul>
<li><code>INTERNET</code> - allows the Jetty server to start and listen for web requests. If this is missing, the <a href='https://code.google.com/p/nativedriver/source/browse/trunk/android/src/com/google/android/testing/nativedriver/server/ServerInstrumentation.java'>ServerInstrumentation</a> cannot start all.</li>
<li><code>WAKE_LOCK</code> - allows AND to hold a wake lock, which prevents the screen from sleeping and locking as a result of inactivity. This is optional.</li>
<li><code>DISABLE_KEYGUARD</code> - allows AND to disable the screen lock when the ServerInstrumentation starts. This is optional.</li>
</ul>
If the optional permissions are omitted, you may have to interact with the device manually to by-pass the key guard or  wake up the device.</li>
<li>Build the application apk and install it to the device.</li>
<li>Start the instrumentation by running this at the command line:<br>
<pre><code>adb shell am instrument {app_package_name}/com.google.android.testing.nativedriver.server.ServerInstrumentation<br>
</code></pre>
</li>
<li>Enable port forwarding with this command:<br>
<pre><code>adb forward tcp:54129 tcp:54129<br>
</code></pre>
</li>
<li>
You can confirm that the instrumentation is started by running <code>adb logcat</code> and looking for a line like this:<br>
<pre><code>I/com.google.android.testing.nativedriver.server.ServerInstrumentation(  273): Jetty started on port 54129<br>
</code></pre>
</li>
</ol>
After following these steps you can run a NativeDriver test on the emulator host machine, or the machine connected to the device. For a sample test, see one of the <a href='https://code.google.com/p/nativedriver/source/browse/#svn%2Ftrunk%2Fandroid%2Ftest%2Fcom%2Fgoogle%2Fandroid%2Ftesting%2Fnativedriver'>JUnit sample tests</a>. The test code must be linked to **client-standalone.jar**.