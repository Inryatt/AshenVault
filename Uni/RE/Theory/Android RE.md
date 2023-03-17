Dicas:
> - lookout for exported:true in Manifest :) good for sniffing around 
> - Look for Launcher activity no manifest
> - bytecode to smali is always possible but not as easy to understand;
> 	 bytecode to java code may be gibberish :(
> 	 


Jadx -> Decompile from DEX to Java code/smali 
apktool -> static analysis on apk, extract DEX and recreated Android.Manifest
objdump -> dump asm for compiled binaries

## The JVM

Java bytecode -> stack based machine


## P1
iterative report, identify everything done,
id inputs, outputs and results and methodologu
map out app functionality not just hunt down vulns.

ctt app uses sth called cordova (lite reactnative)
if electron -> use zap to sniff app n grab what you can



# Entrypoints

### Manifest:
- Launcher Activity
- Services (Background activity)
- Broadcast Receivers
- Exported activities/services (components)
	- Código exposto
- ! Application Subclass
	- (Special Android subclass called "application")
	- Permite manter estado.
	- Executado quando corrido e serve para inicializar coisas como chaves :)
	- serve pa instanciar singletons, p ex


## Native Applications
- Apps developed for os' native language/frameworks.
- Usually compiled to bytecode & packaged with the resources.

- **Native Platform Code - Java Native Interfaces** 
	- when we need faster stuff :>
	- Allows to load native, faster, lower level shared libraries. (C)
	- harder to reverse
	- must have implementations built for each architecture it's supposed to run on
	- explicit calls must be made to use the libraries and *these are entrypoints.* Java must load the libraries before they can be used.

**JNI Args**
The method name / header must be correct.
JNIEnv is the first argument for any JNI method -- This is a pointer :)

Easily spotted with the keyword **native.**

**JNI Dynamic Linking**
It just works as long as a fixed naming template is used.

**JNI Static Linking**
Can have any name (can be obfuscated) but must be done manually.
Most viable -> rev the library blob



## Dynamic Analysis

Frida - tool to interact with running app.

Things to look at:
- logs
- network analysis
- app inputs/outputs



### Network MITM

- Packet Dumps
	- sniff network traffic (packets) with wireshark
	- good to analyze clear-text apis
	- passive observing
- Traffic flows
	- run app with a proxy (like burp) to intercept traffic
	- can inject CA certs
	- active observing (MITM attack)
	- aims to trick app
	- **tool**: Mitmproxy


