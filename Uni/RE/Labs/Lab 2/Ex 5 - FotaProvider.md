To start, opened apk up with jadx(-gui).
Opened AndroidManifest.xml to look for the mainactivity/entrypoint, as well for any clues to what the app is doing.


```xml
<service android:name="com.adups.fota.sysoper.MyApplication">  
        <service android:name="com.adups.fota.sysoper.SysService">  
            <intent-filter>  
                <action android:name="android.intent.action.AdupsFota.SysService"/>  
            </intent-filter>  
        </service>
<service android:name="com.adups.fota.sysoper.TaskService"/>  
        <receiver android:label="WriteCommandReceiver" android:name="com.adups.fota.sysoper.WriteCommandReceiver">  
            <intent-filter>  
                <action android:name="android.intent.action.AdupsFota.WriteCommandReceiver"/>  
                <action android:name="android.intent.action.AdupsFota.OperReceiver"/>  
            </intent-filter>  
        </receiver>  
        <receiver android:name="com.adups.fota.sysoper.TaskReceiver">  
            <intent-filter>  
                <action android:name="android.net.conn.CONNECTIVITY_CHANGE"/>  
                <action android:name="android.intent.action.ACTION_POWER_CONNECTED"/>  
            </intent-filter>  
            <intent-filter>  
                <action android:name="android.intent.action.PACKAGE_ADDED"/>  
                <action android:name="android.intent.action.PACKAGE_REMOVED"/>  
                <action android:name="android.intent.action.PACKAGE_REPLACED"/>  
                <data android:scheme="package"/>  
            </intent-filter>  
        </receiver>
```

this seems some kind of task scheduler -- might receive orders to execute stuff that can be exploited?

Search for
### Runtime.exec()
> Found in file 'b.class', line 56


```java
 Process exec = Runtime.getRuntime().exec(str);  
            BufferedOutputStream bufferedOutputStream = new BufferedOutputStream(exec.getOutputStream());  
            BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(exec.getInputStream()));  
            Iterator it = arrayList.iterator();  
            while (it.hasNext()) {  
                bufferedOutputStream.write((String.valueOf((String) it.next()) + " 2>&1\n").getBytes());  
            }  
            bufferedOutputStream.write("exit\n".getBytes());  
            bufferedOutputStream.flush();  
            while (true) {  
                String readLine = bufferedReader.readLine();  
                if (readLine == null) {  
                    break;  
                }  
                arrayList2.add(readLine);  
            }  
            exec.waitFor();

```


This gets a command, str, and executes it, (throwing out the stderr data), writing it to output stream. Then it reads the input.

This method is again called on line 455 (renamed from 'a' to 'execCommand')
```java
ArrayList execCommand = execCommand("/system/bin/sh", arrayList); 
```

This is part of a larger method, here below:

```java
    public static boolean i() {  
        String str = System.getenv("PATH");  
        ArrayList arrayList = new ArrayList();  
        String[] split = str.split(":");  
        for (int i = 0; i < split.length; i++) {  
            arrayList.add("ls -l " + split[i] + "/su");  
        }  
        ArrayList execCommand = execCommand("/system/bin/sh", arrayList);  
        String str2 = "";  
        for (int i2 = 0; i2 < execCommand.size(); i2++) {  
            str2 = String.valueOf(str2) + ((String) execCommand.get(i2));  
        }  
        return str2.contains("-rwsr-sr-x root     root");  
    }
```


Heres what it does (+/-):
- Gets PATH
- Splits path into its sections
- creates the strings 'ls -l' \<section> '/su'
- executes these, looking for the presence of ''-rwsr-sr-x root     root" in the output

What this does in practice is look for the location of the /su binary in the system, and in PATH, **AND WITH THE SUID BIT SET, which can later be used to execute privileged instructions.**

This belongs to dataeye package, is defined in com.dataeye.c.b and is called in com.dataeye.c.r.


### System

Found in file WriteCommandReceiver.
the function onReceive seems to receive a command, inside an action with the key 'cmd'. The command is then split on spaces and passed as an argument to another function. However, this function couldn't be correctly decompiled and as such we must look at simple and smali code to understand what it does.

- The string is passed as argument to a ProcessBuilder, which according to java documentation:
> This class is used to create operating system processes.


	- r0: BAOS - a string
	- r2: ByteArrayOutputStream (basically a string buffer.)
	- r3: Processbuilder
	- r4: ProcessBuilder Error Stream
	- r5: Processbuilder after init (start)
	- r8: string array

This class is present in the Manifest, exposing two intents.

``` xml
<receiver android:label="WriteCommandReceiver" android:name="com.adups.fota.sysoper.WriteCommandReceiver">
            <intent-filter>
                <action android:name="android.intent.action.AdupsFota.WriteCommandReceiver"/>
                <action android:name="android.intent.action.AdupsFota.OperReceiver"/>
            </intent-filter>
</receiver>
        ```


### Exported Service

```xml
   <service android:label="AppService" android:name="com.dataeye.channel.DCAppService" android:persistent="true" android:exported="true" android:process=":de_service">  
            <intent-filter android:priority="1000">  
                <action android:name="com.dataeye.channel.action.INVOKE_SERVICE"/>  
            </intent-filter>  
        </service>
```

this AppService is exported and can be acessed/Called by other applications, providing an entrypoint.


### OperReceiver
This is an intent that's on the manifest. the function that catches this (onReceive) will run a command. :c
