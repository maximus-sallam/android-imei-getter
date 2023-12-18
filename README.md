# android-imei-getter
Simple non-GUI app to help getting the device IMEI over ADB.

## Usage:

```bash
# install application
adb install imeigetter.apk

# an app start is required to register the broadcast receiver, so we start the main activity here
adb shell am start -n com.saschahuth.imeigetter/.MainActivity

# send the broadcast to receive the result
adb shell am broadcast -a com.saschahuth.imeigetter.GET_IMEI
# output will be something like:
# Broadcast completed: result=0, data="000000000000000", where "data" is the IMEI

# uninstall application
adb uninstall com.saschahuth.imeigetter
```

Note: This is an irresponsible implementation, as it allows any app on the device to query for the IMEI or MEID. You should add android:permission="android.permission.READ_PRIVILEGED_PHONE_STATE" to the receiver in order to close this security hole, since that permission is required by getDeviceId, and the android shell will already have been granted this permission by default.

Note: Older API levels only require READ_PHONE_STATE instead of READ_PRIVILEGED_PHONE_STATE in order to call getDeviceId, but READ_PRIVILEGED_PHONE_STATE is safer and should work as far back as Android 4.0. Using only READ_PHONE_STATE will leave a security hole open for Android 10 and later.
