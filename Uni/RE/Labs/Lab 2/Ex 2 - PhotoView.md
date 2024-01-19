strings on lib/arm64-v8a:
```bash
└─$ strings liboc_helper.so | grep ^Java
Java_com_mbv_a_sdklibrary_manager_JniManager_nativeApkpaper
Java_com_mbv_a_sdklibrary_manager_JniManager_nativeApktype
Java_com_mbv_a_sdklibrary_manager_JniManager_nativeCallback
Java_com_mbv_a_sdklibrary_manager_JniManager_nativeDxs
Java_com_mbv_a_sdklibrary_manager_JniManager_nativeEncrytionkey
Java_com_mbv_a_sdklibrary_manager_JniManager_nativeEncrytionkeyhash
Java_com_mbv_a_sdklibrary_manager_JniManager_nativeIsappsflyers
Java_com_mbv_a_sdklibrary_manager_JniManager_nativeOffe
Java_com_mbv_a_sdklibrary_manager_JniManager_nativeRepo
Java_com_mbv_a_sdklibrary_manager_JniManager_nativeSendinfos
Java_com_mbv_a_sdklibrary_manager_JniManager_nativeSendinstall
Java_com_mbv_a_sdklibrary_manager_JniManager_nativeServicelist
Java_com_mbv_a_sdklibrary_manager_JniManager_nativeUrls
Java_com_mbv_a_sdklibrary_manager_JniManager_nativesend
                                                            

``` 
These are dynamically linked.


in ghidra, the functions are all there easy to find. 
The nativesend is particularly interesting:
```c

void Java_com_mbv_a_sdklibrary_manager_JniManager_nativesend
               (long *param_1,undefined8 param_2,undefined8 param_3,undefined8 param_4)

{
  _jmethodID *p_Var1;
  undefined8 uVar2;
  _jmethodID *p_Var3;
  long lVar4;
  
  p_Var1 = (_jmethodID *)(**(code **)(*param_1 + 0x30))(param_1,"android/telephony/SmsManager");
  if (p_Var1 != (_jmethodID *)0x0) {
    uVar2 = (**(code **)(*param_1 + 0x388))
                      (param_1,p_Var1,"getDefault","()Landroid/telephony/SmsManager;");
    p_Var3 = (_jmethodID *)_JNIEnv::CallStaticObjectMethod((_jclass *)param_1,p_Var1,uVar2);
    lVar4 = (**(code **)(*param_1 + 0x108))
                      (param_1,p_Var1,"sendTextMessage",
                       "(Ljava/lang/String;Ljava/lang/String;Ljava/lang/String;Landroid/app/PendingI ntent;Landroid/app/PendingIntent;)V"
                      );
    if (lVar4 != 0) {
      _JNIEnv::CallVoidMethod((_jobject *)param_1,p_Var3,lVar4,param_3,0,param_4,0,0);
      return;
    }
  }
  return;
}

```

this sends sms :)




