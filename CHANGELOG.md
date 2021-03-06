##3.1.11 (2014-05-22)

Features:
  - Added missing callback options for `steroids.layers.popAll()`, adding `onTransitionStarted` and onTransitionEnd`. iOS only.

Bugfixes:
  - Certain APIs (such as `steroids.layers.popAll()`) no longer give errors if called without callbacks.

##3.1.10 (2014-05-21)

Support for the Initial View; `steroids.getApplicationState`, `steroids.screen.rotate` and native UI events are no longer secret features; bugfixes.

Features:
  - `steroids.initialView.show()` and `steroids.initialView.dismiss()` for showing/dismissing the Initial View.
  - `steroids.modal.hideAll()` to hide all currently open modals. (**BREAKING:** replaces secret `steroids.modal.closeAll()` introduced in 3.1.9.)
  - `steroids.getApplicationState()` returns the application state including all preloaded webviews, tabs, modals and drawer controllers.
  - New `steroids.screen.rotate` API that allows for the device orientation to be set programatically.
  - Register event listeners for the new native UI events with `steroids.drawers.on()`, `steroids.layers.on()`, `steroids.tabBar.on()`, `steroids.modal.on()` and `steroids.view.on()` (event listeners are unregistered with the `.off()` functions).
  - Setting the `window.AG_allowedRotationsDefaults` array before `steroids.js` is loaded will override the WebView default `steroids.view.setAllowedRotations([0])` with the given array.

Bugfixes:
  - `steroids.modal.show()` actually uses `navigationBar` property (as documented) instead of deprecated `hidesNavigationBar` property.
  - **BREAKING:** Fixed typo'd `steroids.drawers.update` parameter to be `stretchDrawer`, not `strechDrawer`.

Changes:
- Deprecated `steroids.view.rotateTo()`, use `steroids.screen.rotate()` instead.

Internal stuff:
 - New iOS JavaScriptCore bridge - more awesome, faster and etc.

##3.1.9 (2014-05-06)

New drawers, set background image for a WebView, use unfiltered images for navigation bar buttons, open modals with navigation bar, bugfixes. All updates in v3.1.9 are iOS-only.

Features:
 - `steroids.views.WebView.setBackgroundImage` to set a background image for a WebView.
 - `steroids.buttons.NavigationBarButton` now supports the `imageAsOriginal` property, allowing you to use an image for a navigation bar button without applying Apple's color filter on it.
 - `steroids.modal.show` now has a `navigationBar` property; setting it to `true` will open the modal with the navigation bar displayed.

Changes:
  - `steroids.drawers` is completely reworked on the native side, with support for drawers on both sides, more open gestures, different animations for displaying the drawer and more:
    - New API method `steroids.drawers.update` for updating/setting the WebViews used for drawers as well as drawer options. See the API docs for all the goodies!
    - `steroids.drawers.hide` now supports replacing the center view as part of the API call.
    - **BREAKING:** `steroids.drawers.show` is now only used to display drawers that have been set up with `steroids.drawers.update`, and cannot be used to initialize the drawer anymore.
    - **BREAKING:** `steroids.drawers.defaultAnimations` changed to include four default animation types: slide, slide and scale, swinging door and parallax.
    - **BREAKING:** `steroids.drawers.hideAll` deprecated.
    - `steroids.drawers.enableGesture` and `steroids.drawers.disableGesture` are deprecated (though they should still work), use `steroids.drawers.update` and `options.openGestures` and `options.closeGestures` instead.

Changes:
  - `setAllowedRotations` now has a default of `[0]` instead of `[]` for new WebViews. This can be overridden by setting a `window.AG_allowedRotationsDefaults` variable before Steroids.js is loaded.

Secret features:
  - `steroids.getApplicationState()` returns the application state including all preloaded webviews, tabs, modals and drawer controllers.
  - `steroids.modal.closeAll()` closes all currently open modals.
  - New `steroids.screen.rotate` API that allows for the device orientation to be set programatically. Examples: `steroids.screen.rotate("portrait")`, `steroids.screen.rotate("landscapeLeft")`.
  - New native UI events for `steroids.drawers`, `steroids.layers`, `steroids.tabBar`, `steroids.modal` and `steroids.views.WebView`

Internal stuff:
 - New iOS JavaScriptCore bridge - more awesome, faster and etc.

##3.1.8 (2014-04-03)

Various new APIs for iOS, multiple consecutive modals supported, navigation bar in modals supported.

Features:
  - Navigation bar can now be used in modal windows also.
  - Multiple modal windows are supported.
  - `steroids.view.navigationBar.setAppearance` to change the global color/background image settings of the navigation bar
  - `steroids.statusBar.onTap` event listener for triggering a function when the status bar is tapped.
  - `steroids.Animation` has new `onAnimationStarted` and `onAnimationEnded` callbacks.
  - `steroids.view.navigationBar.update` has a new `backButton` parameter for setting a custom button to replace the native back button.
  - `steroids.view.displayLoading` to show `loading.html` programmatically.
  - `steroids.tabBar.currentTab.update` functions like `steroids.tabBar.update` for the currently active tab.
  - `steroids.view.updateKeyboard` with support for showing/hiding the keyboard accessory bar on a per-view basis.
  - `steroids.view.navigationBar.setAppearance` changes navigation bar appearance.

Secret features:
  - `steroids.app.getNSUserDefaults()` returns current NSUserDefaults in iOS.

##3.1.7 (2014-03-05)

Secret features:
  - `steroids.logger.log(msg)` for new logging feature, messages readable in `steroids.logger.messages`
  - `steroids.logger.queue.startFlushing(ms)` flushes logs to `steroids cli` + `.stopFlushing()`
  - `steroids.app.host.getURL()` returns (async) the (base) URL that was used to download the app (e.g. machine that has `steroids connect` running)
  - `steroids.view.rotateTo(deg)` rotates current view to deg somehow, someday
  - `steroids.device.platform` namespace and `steroids.device.platform.getName()` to determine the platform (e.g. "ios", "android", "tizen")
  - `steroids.app.getMode()` returns "standalone" if the build is an ad-hoc or production build. Otherwise returns "scanner".
  - `steroids.logger` automatically sends logs to Steroids CLI when running as a scanner.

Bugfixes:
  - Fixed a bug with the OAuth2 modal show (thanks @zeopix!)

##3.1.6 (2014-02-27)
Added methods for setting tab bar badges and programmatically selecting a tab. Added support for replacing the layer stack with a WebView already in the layer stack. Added a parameter to disable animation for modal screen show/hide.

New API methods requires Scanner v3.1.3.

Features:
  - `steroids.tabBar.update` now supports setting a badge for a tab.
  - `steroids.layers.replace` can now target preloaded WebViews that already exist in the layer stack.
  - `steroids.modal.show` and `steroids.modal.hide` now have a `disableAnimation` parameter to show/hide the modal screen immediately, without an animation.
  - Added `steroids.tabBar.selectTab(index)` for programmatically setting the active tab.

Bugfixes:
  - Fixed an issue where `window.postMessage` gave false error messages on Android.

##3.1.5 (2014-02-10)
Bugfix for `steroids.view.navigationBar.update`.

Bugfixes:
  - `steroids.view.navigationBar.update` no longer gives an error regarding undefined button callbacks when updating buttons only on one side.

##3.1.4 (2014-02-10)

New `steroids.view.navigationBar.update` API on iOS (deprecates `steroids.view.navigationBar.setButtons` on iOS), added option to animate showing/hiding navigation bar, programmatic show/hide of splashscreen, deprecated methods removed.

Features:
  - Support for updating navigation bar contents (title, title image, buttons) per webview with `steroids.view.navigationBar.update` on iOS.
  - Support for showing and hiding navigation bar with animation using `animated` option on iOS.
  - Support for showing and hiding splashscreen programmatically with `steroids.splashscreen.show` and `steroids.splashscreen.hide` on iOS.

Changes:
  - Removed deprecated `steroids.view.bounceShadow`.
  - Deprecated and removed `steroids.layers.array`.

##3.1.3 (2014-01-02)

Programmatic updating of tab bar icons and titles with `steroids.tabBar.update`.

Features:
  - Adds support for updating tab titles and icons to new ones with `steroids.tabBar.update`.

Changes:
  - Removed deprecated `steroids.XHR`.

## 3.1.2 (2013-12-18)

Fixed to work in Tizen Web Simulator.

Bugfixes:
  - Use TizenBridge if window.tizen is defined.

## 3.1.1 (2013-12-16)

Fixed `visibilitychange` firing twice on iOS, Steroids Analytics API to record analytics events

Bugfixes:
  - `visibilitychange` events no longer fire twice on iOS.

Features:
  - `steroids.analytics.track` records analytics events (iOS-only).

## 3.1.0 (2013-12-04)

Support for unloading preloaded webviews, show/hide tab bar, show/hide status bar.

Features:
  - `sterois.views.WebView.prototype.unload` to unload preloaded webView from memory (iOS)
  - `steroids.statusBar.hide` and `steroids.statusBar.show` to hide and show the native status bar (iOS)
  - `steroids.tabBar.hide` and `steroids.tabBar.show` to hide and show the native tab bar (iOS)

Changes:
  - `steroids.views.webView` constructor supports `id` parameter (defaults to `location` if not given)

## 2.7.11 (2013-11-15)

Tab improvements, navigation bar bugfixes

Features:
  - Adds support for tabBar parameter in steroids.layers.push

Bugfixes:
  - Fixes the issue Android right button not showing.
  - Navigation bar title image and image buttons now wait for the Steroids `ready` event internally.

## 2.7.10 (2013-10-17)

Multiple navigation bar buttons, ability to hide the back button.

Features:
  - `steroids.view.navigationBar.setButtons()` API expanded, see the [API docs](http://docs.appgyver.com/en/edge/steroids_Steroids%20Native%20UI_steroids.view.navigationBar_navigationBar.setButtons.md.html#steroids.view.navigationBar.setButtons) for more information
    - Hide/show the back button.
    - Multiple buttons on the left and right side of the navigation bar.
    - Buttons can use images or text.

## 2.7.9 (2013-10-14)

Initial Tizen support.

Features:
  - TizenBridge for handling API calls and auto-refresh of client on Tizen devices.

## 2.7.8 (2013-09-27)

Grunt tasks updated to latest Node.js version, support for images in navigation bar (iOS only)

Changes:
  - Added support for images in navigation bar with steroids.view.navigationBar.show({titleImagePath: imagePath})
  - Cleaned up and updated `grunt` tasks to support Node.js 0.10.x/0.11.x

## 2.7.7 (2013-08-21)

Fixed a bug that prevented Steroids API calls from functioning on certain Android versions.

Bugfixes:
  - WebBridge is no longer erroneously used instead of NativeBridge (affected certain Android versions)

## 2.7.6 (2013-08-19)

SQLite API no longer experimental

Changes:
  - steroids.data.SQLiteDB.createTable supports defining columns as an object

## 2.7.5 (2013-08-08)

Experimental EventSource support for refreshing browser when project is changed

Changes:
  - WebBridge polls steroids npm for changes and refreshes

## 2.7.4 (2013-08-08)

Expirimental SQLite API and browser support

Changes:
  - steroids.data.SQLliteDB secret APIs
  - Experimental support for browser debugging

## 2.7.3 (2013-08-02)

Experimental TouchDB API

Changes:
  - steroids.data.TouchDB secret APIs

## 2.7.2 (2013-07-12)

Bugfixes:
  - fixed rare issue with websocket state handling

## 2.7.1 (2013-06-04)

Sleep modes and layer stack replacing

Changes:
  - steroids.layers.replace all layers with a preloaded webview
  - steroids.device.disableSleep - prevent device's screen from sleeping
  - steroids.device.enableSleep - allow device's screen to sleep

## 2.7.0 (2013-06-03)

Public beta release

## 0.7.1 (2013-05-07)

Tuned drawers animations.

Changes:
 - Left drawer animation is snappier

## 0.7.0 (2013-05-06)

Version bumb to 0.7.x indicate dependency on new Scanner.

## 0.6.2 (2013-05-02)

Drawers.

Features:
  - steroids.drawers namespace with methods for managing drawers.

## 0.6.1 (2013-04-08)

Reset changelog.

Bugfixes:
  - API calls were broken in 0.6.0, release process failure.

