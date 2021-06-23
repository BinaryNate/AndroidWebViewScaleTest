# Android WebView Scale Test

Reproduces an issue where [WebView.setInitialScale()](https://developer.android.com/reference/android/webkit/WebView#setInitialScale(int)) is not working correctly with the new 91.0.4472.101 update of the System WebView. The issue is that the initial scale set with setInitialScale() is used for the first page load, but it's not used for subsequent pages loaded with loadUrl(). Instead, subsequent pages are zoomed in with a larger scale.

Details for reproducing the issue:

- MainActivity.java calls setInitialScale(100) at the start of the app to set the scale to 100%, and the initial page loaded (https://google.com) correctly uses the scale of 100%.

- If you press the "⋮" menu button and press "Load youtube.com", the app will call `webView.loadUrl("https://youtube.com")`, and the webview will load youtube.com with an incorrect, zoomed scale. The `WebViewClient.onScaleChanged()` method indicates that the scale changed to 2.75 (275%).

- If instead you restart the app and then navigate to youtube.com through Google, then the correct scale of 100% will be used.

- Device used for testing: Pixel 3 with Android 11
