android-referrer-plugin
=======================

This plugin captures the referrer value passed when an android app is installed from a webpage and stores it in the applications shared preferences for later retrieval. 

You'll typically want to use the [AppPreferences plugin](https://github.com/8zrealestate/AppPreferences) to pull the referrer value into your phonegap app for your javascript code to manipulate.

## Purpose

This plugin lets your app display different behavior based on where it was installed from.  If you have a sports app, for example, and want to use the same codebase, but brand the app differently for different teams, you can use this plugin to capture whether the app was installed from the Denver Broncos or Washington Redskins page, and skin the app appropriately.

Don't forget when using this plugin that if an app is installed directly from Google Play, this plugin will not execute--the intent will never fire.

## Install

This plugin uses [plugman](https://github.com/apache/cordova-plugman)

`cordova plugins add https://github.com/8zrealestate/android-referrer-plugin`

## Usage

To use this plugin, add `&referrer=xyz` to app install links on your webpages.  For example: 
```
http://market.android.com/details?id=com.yourid.here&referrer=textinreferrer
market://details?id=com.yourid.here&referrer=textinreferrer
```

The value in the referrer text (`textinreferrer` above) will be stored as a string in your apps shared preferences object, under the key `referrer`.

To test that the install referrer event is received by the plugin in your emulator:

run `adb shell` and then 

```
am broadcast -a com.android.vending.INSTALL_REFERRER \
-n <your package here>/com.eightz.mobile.cordova.plugin.android.referrer.Receiver \
--es "referrer" "textinreferrer"
```


## Limits

* I don't know how long a referrer string can be.
* I believe the referrer string can contain any characters that are valid in URL query strings, but don't think that ampersands are allowed.  For example: `&referrer=foo&bar` would result in a captured `referrer` of `foo`
* If you are trying to be compatible with the `app-argument` text in Apple smart banners, be aware that `app-argument` text block is [required to be a url](http://developer.apple.com/library/ios/#documentation/AppleApplications/Reference/SafariWebContent/PromotingAppswithAppBanners/PromotingAppswithAppBanners.html).

