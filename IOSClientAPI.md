Following APIs should work on Android NativeDriver.

# [IosNativeDriver](http://code.google.com/p/nativedriver/source/browse/trunk/iphone/Client/src/com/google/iphone/testing/nativedriver/client/IosNativeDriver.java) #

The main class of iOS NativeDriver. Provides access to the iOS application.

| `findElement(By by)` | Find the first `WebElement` using the given method. |
|:---------------------|:----------------------------------------------------|
| `findElements(By by)` | Find all elements within the current page using the given method. |
or resuming existing activities. 
| `getTitle()`         | The title of the current page.                      |
| `manage().timeouts().implicitlyWait(long time, TimeUnit unit)` | Specifies the amount of time the driver should wait when searching for an element if it is not immediately present. |
| `quit()`             | Quits this driver session.                          |

# WebElement #

WebElement represents an native element in the application UI. This class is defined in original WebDriver library.

| `clear()` | If this element is a text entry element, this will clear the value. |
|:----------|:--------------------------------------------------------------------|
| `click()` | Click this element.                                                 |
| `findElement(By by)` | Find the first `WebElement` within the current context using the given method. |
| `findElements(By by)` | Find all elements within the current context using the given method. |
| `getAttribute(String name)` | Get the value of a the given attribute of the element.              |
| `getText()` | Get the visible text of the element.                                |
| `isDisplayed()` | Is this element displayed or not?                                   |
| `isEnabled()` | Is the element currently enabled or not?                            |
| `isSelected()` | Determine whether or not this element is selected or not.           |
| `sendKeys(CharSequence... keysToSend)` | Use this method to simulate typing into an element, which may set its value. |
| `submit()` | Simulate typing enter key.                                          |

# [By](http://code.google.com/p/nativedriver/source/browse/trunk/iphone/Client/src/com/google/iphone/testing/nativedriver/client/By.java) #

`findElement` and `findElements` can take `By` object. `text`, `partialText` and `placeholder` are the special method for native applications.

| `text(String text)` | Matches all elements whose `getText` method return the given value. |
|:--------------------|:--------------------------------------------------------------------|
| `partialText(String text)` | Matches all elements whose `getText` method returns a string which contains or equals the given string. |
| `placeholder(String text)` | Matches text field elements whose placeholder text is the given value. |
| `id(String id)`     | Matches all elements whose accessibility label is the given value.<br>You have to <a href='https://groups.google.com/group/nativedriver-users/browse_thread/thread/7c35d95bc3738b5c'>enable accessibility on your simulator</a>. <br>
<tr><td> <code>className(String className)</code> </td><td> Matches all elements whose class name is the given value.           </td></tr></tbody></table>

<h1>[ClassNames](http://code.google.com/p/nativedriver/source/browse/trunk/iphone/Client/src/com/google/iphone/testing/nativedriver/client/ClassNames.java) #

You can use these constant for `By.className`.

| `BUTTON` |
|:---------|
| `LABEL`  |
| `SWITCH` |
| `TEXT_FIELD` |
| `TEXT_VIEW` |
| `WEBVIEW` |