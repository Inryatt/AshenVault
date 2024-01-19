Unzip .apk.
There's a 'lib' folder with libraries for different architectures.

Do 'strings' on arm lib to see if there's presence of dynamically or statically linked function headers.

There's static linked headers, for example:

```java
(Ljava/lang/String;)Ljavax/crypto/SecretKeyFactory;
generateSecret
(Ljava/security/spec/KeySpec;)Ljavax/crypto/SecretKey;
javax/crypto/Cipher
(Ljava/lang/String;)Ljavax/crypto/Cipher;
init
(ILjava/security/Key;Ljava/security/SecureRandom;)V
``` 

Opened it up on Ghidra, and imported the Data types:

![[Pasted image 20230303172555.png]]
(Open File Archive)
After, located the function `JNI_OnLoad` and changed the type of the pointer argument to JNIEnv*. (because that's always it.)

![[Pasted image 20230303172658.png]]
There's a 'registerNatives' function, and passed to it is probably the function itself.
Opening it, we find what's probably the function mapping (pictured below what it should be):
```java
typedef struct {  
    char *name;  
    char *signature;  
    void *fnPtr;  
} JNINativeMethod; 
```

In the decompiled code we have:

```C
/* registerNatives(_JNIEnv*) */

void registerNatives(_JNIEnv *param_1)

{
  undefined *local_14;
  char *local_10;
  code *local_c;
  
  local_14 = &DAT_0001503b;
  local_10 = "(Ljava/lang/String;)V";
  local_c = native_setAppkey + 1;
  registerNativeMethods(param_1,nativeClassForJni,(JNINativeMethod *)&local_14,1);
  return;
}

```


In here, we can make an educated guess on whats the struct:
```java
typedef struct {  
    char *name;  
    char *signature;  
    void *fnPtr;  
} JNINativeMethod; 
```

Changing names and types accordingly:
```c

/* registerNatives(_JNIEnv*) */

void registerNatives(_JNIEnv *param_1)

{
  char *name;
  char *signature;
  code *fnPtr;
  
  name = "a";
  signature = "(Ljava/lang/String;)V";
  fnPtr = native_setAppkey + 1;
  registerNativeMethods(param_1,nativeClassForJni,(JNINativeMethod *)&name,1);
  return;
}```

**Function Signature: (Ljava/land/String;)V**
function:void  setAppkey(String somestring)

And this is the library function that's imported:
```c

void native_setAppkey(int *param_1,undefined4 param_2,undefined4 param_3)

{
  _jobject *p_Var1;
  int iVar2;
  undefined4 uVar3;
  _jmethodID *p_Var4;
  undefined4 uVar5;
  _jmethodID *p_Var6;
  char *__src;
  undefined4 uVar7;
  _JNIEnv a_Stack_224 [4];
  em aeStack_220 [4];
  char acStack_21c [512];
  int local_1c;
  
  local_1c = __stack_chk_guard;
  p_Var1 = (_jobject *)su::f(a_Stack_224,(char *)param_1);
  if (p_Var1 == (_jobject *)0x0) {
    __android_log_print(4,"LOG15","context is null");
  }
  else {
    iVar2 = em::a(aeStack_220,(_JNIEnv *)param_1,p_Var1);
    if (iVar2 != 1) {
      uVar3 = su::r((su *)a_Stack_224,(_JNIEnv *)param_1,p_Var1);
      p_Var4 = (_jmethodID *)(**(code **)(*param_1 + 0x18))(param_1,"android/content/Intent");
      uVar5 = (**(code **)(*param_1 + 0x84))(param_1,p_Var4,"<init>","(Ljava/lang/String;)V");
      p_Var6 = (_jmethodID *)_JNIEnv::NewObject((_jclass *)param_1,p_Var4,uVar5,uVar3);
      memset(acStack_21c,0,0x200);
      strcat(acStack_21c,"#0#");
      __src = (char *)FUN_00012426(param_1,param_3);
      strcat(acStack_21c,__src);
      uVar5 = _JNIEnv::NewStringUTF((char *)param_1);
      uVar7 = (**(code **)(*param_1 + 0x84))
                        (param_1,p_Var4,"putExtra",
                         "(Ljava/lang/String;Ljava/lang/String;)Landroid/content/Intent;");
      uVar3 = _JNIEnv::CallObjectMethod((_jobject *)param_1,p_Var6,uVar7,uVar3,uVar5);
      uVar5 = (**(code **)(*param_1 + 0x7c))(param_1,p_Var1);
      uVar5 = (**(code **)(*param_1 + 0x84))
                        (param_1,uVar5,"sendBroadcast","(Landroid/content/Intent;)V");
      _JNIEnv::CallVoidMethod((_jobject *)param_1,(_jmethodID *)p_Var1,uVar5,uVar3);
    }
  }
  if (local_1c != __stack_chk_guard) {
                    /* WARNING: Subroutine does not return */
    __stack_chk_fail();
  }
  return;
}

```
(key generator rançoso)
