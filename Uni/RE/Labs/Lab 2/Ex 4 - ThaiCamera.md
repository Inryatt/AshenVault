To start, opened apk up with jadx(-gui).
Opened AndroidManifest.xml to look for the mainactivity/entrypoint, as well for any clues to what the app is doing.

**Suspicious Permissions:**
```<uses-permission android:name="android.permission.SEND_SMS"/> ```
 > why does a camera app need to send sms?
 
``<uses-permission android:name="com.google.android.c2dm.permission.RECEIVE"/> ``
> why does a camera app need to receive cloud messages? (C2DM)

``<uses-permission android:name="com.cp.camera.permission.C2D_MESSAGE"/>``

`<action android:name="com.warmtel.smsg.service.IMICHAT"/>

  
                <action android:name="com.google.android.c2dm.intent.RECEIVE"/>  
                <action android:name="com.google.android.c2dm.intent.REGISTRATION"/>



App has 3 activities:
 - Loading (Entry Point from Launcher)
 - CameraActivity
 - ShareActivity
 and then two Facebook Activities.

by opening Launcher:
    public static final String SENT_SMS_ACTION = "SENT_HUGE_SMS_ACTION";
sus

So the app when clicked on wil open to the activity Loading, where it will, sneakily, send a VIDEO sms. It asks for permissions and if denied will ask again. It checks if the phone is outdated (sdk<23) to se if it needs to ask permissions or can bypass that step.

It checks if a specific entry ("videoShare") exists in SharedPreferences in order to see if the SMS has been sent previously, in order to send it only once, possibly to avoid detection.