VideoEnabledWebView
===================

Android's WebView and WebChromeClient class extensions that enable fully working, cross-device, HTML5 video support in Android 2.2 (API level 8) onwards. Actively maintained and tested up to Android 4.4 (API level 19) with its new Chromium webview.

Motivation
----------

Android's default WebView doesn't work well with HTML5 videos (i.e. the _&lt;video&gt;_ tag). Unlike iOS's UIWebView, which is similar to a Safari tab with respect to video handling, Android's implementation is far from how a Chrome tab behaves. API level fragmentation and manufacturer customizations, which usually include video player related UI changes, only add up to the mess. Things that don't work consistently across devices include:
- Videos not even playing.
- Videos not playing in-line.
- Videos not displaying any status indicator while loading.
- Videos not going full-screen.
- Videos not automatically exiting full-screen when they end.
- Videos not playing for the second time.

VideoEnabledWebView and VideoEnabledWebChromeClient are two handy extension classes that come to help deal with these issues. I originally wrote them for my personal use, but they got a lot of attention in [StackOverflow](http://stackoverflow.com/a/16179544/423171), and that's the reason they are now here. Contributions are appreciated.

How to use it
-------------

For a working example, download the whole repository and open it with __Android Studio__. Do not use the Open Project option, use __Import Project__.

As you can see in the example project, you first need to include __VideoEnabledWebView.java__ and __VideoEnabledWebChromeClient.java__ classes into your project. Second, you need to carefully read both classes' comments, as they are fully documented with javadoc and include very important information on how to use them correctly based on your needs.

VideoEnabledWebChromeClient can be used alone if you do not require the functionality that VideoEnabledWebView adds, although you need to include both classes anyway in order to compile. On the other side, __VideoEnabledWebView must always rely on a VideoEnabledWebChromeClient__.

Finally, you need to define all the views that you will be using in your layout files, and provide the relevant references in the classes' constructors.

Common issues check-list
------------------------

1. Remember to declare the __internet permission__ in AndroidManifest.xml if you are using the WebView to access remote content: `<uses-permission android:name="android.permission.INTERNET" />`
2. Remember to enable __hardware acceleration__ in AndroidManifest.xml for in-line videos to work in API level 11. The field will have no effect in earlier API levels: `android:hardwareAccelerated="true"`
3. Remember to __initialize the VideoEnabledWebChromeClient__ and link it with the VideoEnabledWebView. Follow the example in ExampleActivity.java.
4. Remember to override your Activity's __onBackPressed()__ and pass the event to the VideoEnabledWebChromeClient. Follow the example in ExampleActivity.java. 
5. Remember to specify and/or programmatically inflate the __videoLayout__, __nonVideoLayout__, and, optionally, __loadingView__. Follow the example in ExampleActivity.java and the xml layout files in res/layout.
6. If you are using __ProGuard__, remember to add the fully qualified name of the Javascript interface to the rules file: `-keepclassmembers class name.cpr.VideoEnabledWebView$JavascriptInterface { public *; }`
