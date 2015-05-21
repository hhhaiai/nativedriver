## WARNING ##

**NativeDriver is only for the testing purpose.**

NativeDriver uses private API. Do not use this library in the production codes.

## Requirements ##
<ul>
<li>Xcode 4</li>
<li>Eclipse version 3.5 or later (Eclipse IDE for Java Developers recommended) - <a href='http://www.eclipse.org/downloads/'>
download</a></li>
<li>Ant - <a href='http://ant.apache.org/bindownload.cgi'>download</a></li>
<li>JDK 1.6 or later - <a href='http://www.oracle.com/technetwork/java/javase/downloads/jdk-6u25-download-346242.html'>download</a></li>
</ul>

## Check-out the NativeDriver libraries ##
Check-out the repository with SVN if you have not done so already:
```
$ svn checkout https://nativedriver.googlecode.com/svn/trunk nativedriver --username {Google account e-mail address}
```
The repository that will be downloaded is organized in this manner:
```
nativedriver
  |
  |__iphone
  |     |__Classes (server codes)
  |     |__Client (client codes)
  |     |__NativeDriver.xcodeproj (Xcode project of server)
  |     |__SampleApp (sample app under test)
  |     |__Tests (unit tests for server codes)
  |     |__ThirdParty (Objective-C dependencies we need)
  |
  |__third_party (Java dependencies we need)
```

## Build and run SampleApp app on your emulator ##

Open nativedriver/SampleApp/SampleApp.xcodeproj with Xcode. This application have already finished the NativeDriver configurations.
Run **Automation** target on **iPhone 4.3 Simulator**.

## Build client library ##
Use `ant` to build the NativeDriver client library:
```
$ cd nativedriver/iphone/Client
$ ant
```

<p><b>ios-client-standalone.jar</b> is built and stored in the nativedriver/iphone/Client/build directory. This should be linked to the test, which is the NativeDriver client. It implements a WebDriver API which communicates with the server.</p>

## Import sample test case into Eclipse ##

<ol>
<li>Start Eclipse</li>
<li>Click the <i>File -> Import...</i> menu item.</li>
<li>Select <i>Existing Projects into Workspace</i> in the <i>General</i> category and click <i>Next</i></li>
<li>Click <i>Select root directory</i> and then click <i>Browse...</i></li>
<li>Open the <code>nativedriver/iphone/Client/test</code> directory in the repository you downloaded</li>
<li>Click Finish.</li>
</ol>

<p>The <code>ios-test</code> project you imported contains sample tests written with iOS NativeDriver.</p>

## Run the test ##

<ol>
<li>Right-click <code>NativeDriverTest</code> class in the <code>ios-test</code> project</li>
<li>Select <i>Run As->JUnit Test</i>.</li>
<li>Specify the <i>Eclipse JUnit Launcher</i> as the <i>Preferred Launcher</i>.</li>
<li>Watch the emulator to see the application automatically moving!</li>
</ol>