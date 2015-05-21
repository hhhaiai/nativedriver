Following APIs should work on Android NativeDriver.

# [AndroidNativeDriverBuilder](http://code.google.com/p/nativedriver/source/browse/trunk/android/src/com/google/android/testing/nativedriver/client/AndroidNativeDriverBuilder.java) #

Use this class to build AndroidNativeDriver.

| `build()` | Build `AndroidNativeDriver` with specified settings. |
|:----------|:-----------------------------------------------------|
| `withAdbConnection(AdbConnection adbConnection)` | Build with specified `AdbConnection`.                |
| `withCommandExecutor(CommandExecutor commandExecutor)` | Build with specified `CommandExecutor`.              |
| `withDefaultServer()` | Build with default server ( http://localhost:54129/hub ). |
| `withServer(URL url)` | Build with specified server URL.                     |

# [AndroidNativeDriver](http://code.google.com/p/nativedriver/source/browse/trunk/android/src/com/google/android/testing/nativedriver/client/AndroidNativeDriver.java) #

The main class of Android NativeDriver. Provides access to the Android application.

| `close()` | Close every associated window. |
|:----------|:-------------------------------|
| `findElement(By by)` | Find the first `WebElement` using the given method. |
| `findElements(By by)` | Find all elements within the current page using the given method. |
| `get(String url)` | Start a new activity either in a new task or the current task. The URL should be in following format:<br><code>and-activity://&lt;Activity class name&gt;</code> <br>
<tr><td> <code>getCurrentUrl()</code> </td><td> Returns a string that looks like a URL that describes the current activity.<br> Each running activity is assigned a unique URL, so the URL can be used to detect the starting of new activities or resuming existing activities. </td></tr>
<tr><td> <code>getKeyboard().sendKeys(CharSequence... keysToSend)</code> </td><td> Sends key events.              </td></tr>
<tr><td> <code>getKeyboard().pressKey(Keys keyToPress)</code> </td><td> Sends a press key event.       </td></tr>
<tr><td> <code>getKeyboard().releaseKey(Keys keyToRelease)</code> </td><td> Sends a release key event.     </td></tr>
<tr><td> <code>getOrientation()</code> </td><td> Returns the current screen orientation of the device. </td></tr>
<tr><td> <code>getScreenshotAs(OutputType&lt;X&gt; target)</code> </td><td> Capture the screenshot and store it in the specified location.<br>Driver should be set up with <code>AdbConnection</code>. </td></tr>
<tr><td> <code>getTitle()</code> </td><td> The title of the current page. </td></tr>
<tr><td> <code>manage().timeouts().implicitlyWait(long time, TimeUnit unit)</code> </td><td> Specifies the amount of time the driver should wait when searching for an element if it is not immediately present. </td></tr>
<tr><td> <code>navigate().back()</code> </td><td> Sends BACK key event.          </td></tr>
<tr><td> <code>navigate().toActivity(String activityClass)</code> </td><td> Same as <code>startActivity(String activityClass)</code> </td></tr>
<tr><td> <code>quit()</code> </td><td> Quits this driver, closing every associated window. </td></tr>
<tr><td> <code>rotate(ScreenOrientation orientation)</code> </td><td> Changes the orientation of the device. </td></tr>
<tr><td> <code>startActivity(String activityClass)</code> </td><td> Start a new activity either in a new task or the current task. Same as <code>get("and-activity://" + activityClass)</code>. </td></tr></tbody></table>

<h1>WebElement</h1>

WebElement represents an native element in the application UI. This class is defined in original WebDriver library.<br>
<br>
<table><thead><th> <code>clear()</code> </th><th> If this element is a text entry element, this will clear the value. </th></thead><tbody>
<tr><td> <code>click()</code> </td><td> Click this element.                                                 </td></tr>
<tr><td> <code>findElement(By by)</code> </td><td> Find the first <code>WebElement</code> within the current context using the given method. </td></tr>
<tr><td> <code>findElements(By by)</code> </td><td> Find all elements within the current context using the given method. </td></tr>
<tr><td> <code>getLocation() </code> </td><td> Where on the page is the top left-hand corner of the rendered element?<br> <b>(not working for now)</b> </td></tr>
<tr><td> <code>getSize()</code> </td><td> What is the width and height of the rendered element?<br> <b>(not working for now)</b> </td></tr>
<tr><td> <code>getText()</code> </td><td> Get the text of this element.                                       </td></tr>
<tr><td> <code>isDisplayed()</code> </td><td> Is this element displayed or not?<br> <b>(not working for now)</b>  </td></tr>
<tr><td> <code>isEnabled()</code> </td><td> Is the element currently enabled or not?                            </td></tr>
<tr><td> <code>isSelected()</code> </td><td> Determine whether or not this element is selected or not.<br> <b>(not working for now)</b> </td></tr>
<tr><td> <code>sendKeys(CharSequence... keysToSend)</code> </td><td> Use this method to simulate typing into an element, which may set its value. </td></tr></tbody></table>

<h1><a href='http://code.google.com/p/nativedriver/source/browse/trunk/android/src/com/google/android/testing/nativedriver/common/AndroidNativeBy.java'>AndroidNativeBy</a></h1>

<code>findElement</code> and <code>findElements</code> can take <code>AndroidNativeBy</code> object. <code>text</code> and <code>partialText</code> are the special method for native applications.<br>
<br>
<table><thead><th> <code>text(String text)</code> </th><th> Matches all elements whose <code>getText</code> method return the given value. </th></thead><tbody>
<tr><td> <code>partialText(String text)</code> </td><td> Matches all elements whose <code>getText</code> method returns a string which contains or equals the given string. </td></tr>
<tr><td> <code>id(String id)</code>     </td><td> Matches all elements whose id is the given value.                              </td></tr>
<tr><td> <code>className(String className)</code> </td><td> Matches all elements whose class name is the given value.                      </td></tr></tbody></table>

<h1><a href='http://code.google.com/p/nativedriver/source/browse/trunk/android/src/com/google/android/testing/nativedriver/client/ClassNames.java'>ClassNames</a></h1>

You can use these constant for <code>By.className</code>.<br>
<br>
<table><thead><th> <code>BUTTON</code> </th></thead><tbody>
<tr><td> <code>CHECKBOX</code> </td></tr>
<tr><td> <code>CHECKED_TEXT_VIEW</code> </td></tr>
<tr><td> <code>EDIT_TEXT</code> </td></tr>
<tr><td> <code>RADIO_BUTTON</code> </td></tr>
<tr><td> <code>TEXT_VIEW</code> </td></tr>
<tr><td> <code>TOGGLE_BUTTON</code> </td></tr>
<tr><td> <code>VIEW</code>   </td></tr>
<tr><td> <code>WEBVIEW</code> </td></tr></tbody></table>

<h1><a href='http://code.google.com/p/nativedriver/source/browse/trunk/android/src/com/google/android/testing/nativedriver/common/AndroidKeys.java'>AndroidKeys</a></h1>

You can emulate clicking hard keys with sending these special keys via <code>sendKeys</code>.<br>
<br>
<table><thead><th> <code>ALT_LEFT</code> </th></thead><tbody>
<tr><td> <code>ALT_RIGHT</code> </td></tr>
<tr><td> <code>BACK</code>     </td></tr>
<tr><td> <code>DEL</code>      </td></tr>
<tr><td> <code>DPAD_DOWN</code> </td></tr>
<tr><td> <code>DPAD_LEFT</code> </td></tr>
<tr><td> <code>DPAD_RIGHT</code> </td></tr>
<tr><td> <code>DPAD_UP</code>  </td></tr>
<tr><td> <code>ENTER</code>    </td></tr>
<tr><td> <code>HOME</code>     </td></tr>
<tr><td> <code>MENU</code>     </td></tr>
<tr><td> <code>SEARCH</code>   </td></tr>
<tr><td> <code>SHIFT_LEFT</code> </td></tr>
<tr><td> <code>SHIFT_RIGHT</code> </td></tr>
<tr><td> <code>SYM</code>      </td></tr>