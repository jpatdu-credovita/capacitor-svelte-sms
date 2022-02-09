# Sending SMS on a Capacitor Android app

This is an application to demo the [cordova-sms-plugin](https://github.com/cordova-sms/cordova-sms-plugin/) in Capacitor, using the Svelte JS framework.

It specifically demonstrates sending SMS with no-intent on Android. This means that when the `sendSms()` function is called, instead of the default behavior of the SMS app appearing, the app will send the SMS in the background.

This requires the `SEND_SMS` and `READ_PHONE_STATE` permissions in AndroidManifest.xml