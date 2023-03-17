Possible Entrypoints:

### Exported=true

This receiver was found:
```xml
<receiver android:name="com.facebook.CampaignTrackingReceiver" android:permission="android.permission.INSTALL_PACKAGES" android:exported="true">  
            <intent-filter>  
                <action android:name="com.android.vending.INSTALL_REFERRER"/>  
            </intent-filter>  
        </receiver>
        ```

The code defined in `com.facebook.CampaignTrackingReceiver` receives the `"com.android.vending.INSTALL_REFERRER"` intent.

```java
public final class CampaignTrackingReceiver extends BroadcastReceiver {  
    static final String INSTALL_REFERRER = "referrer";  
  
    @Override // android.content.BroadcastReceiver  
    public void onReceive(Context context, Intent intent) {  
        String stringExtra = intent.getStringExtra("referrer");  
        if (stringExtra == null || !stringExtra.startsWith("fb")) {  
            return;  
        }  
        AppEventsLogger.setInstallReferrer(intent.getStringExtra("referrer"));  
    }
```

This intent should have a `referrer` field, which must be a string starting with `fb`.
Then, the InstallReferrer will be set to what's on the `referrer`  value.

This is later accessed by 
```java
  
    /* JADX INFO: Access modifiers changed from: package-private */  
    public static String getInstallReferrer() {  
        return FacebookSdk.getApplicationContext().getSharedPreferences("com.facebook.sdk.appEventPreferences", 0).getString("install_referrer", null);  
    }```


