# Integrate SDK

# Preparation for Integration

### (1) Create Project

Build your project in the Android Studio.

### (2) Configure the build.gradle

Add the following codes to the build.gradle file.

```groovy
defaultConfig {
    ndk {
        abiFilters "armeabi-v7a"
    }
   }
    dependencies {
        implementation 'com.alibaba:fastjson:1.1.67.android'
        implementation 'com.squareup.okhttp3:okhttp-urlconnection:3.12.3'
        implementation 'org.eclipse.paho:org.eclipse.paho.client.mqttv3:1.2.0'
        
    }
    
repositories {
    mavenLocal()
    jcenter()
    google()
}

```


> **[Note]**
>
> * The Wiser Smart sdk solely supports the platform of armeabi-v7a architecture by default. 
> * After version 3.11.0, the so libraries of armeabi-v7a, arm64-v8a, armeabi platforms have been integrated into sdk. Please remove the relevant so-banks of sdk manually placed in the local, and use the default provided by sdk.

### (3) Integrated security image

Click the download button to download the security image.

![](./images/download_t_s.png)

Rename the downloaded security image to "t_s.bmp" and move it to the assets/ folder in the project directory.

![](./images/addt_s.png)

### (4) Set the AndroidManifest.xml

Set appkey and appSecret in the AndroidManifest.xml file, and configure corresponding permissions, etc.

```xml

<meta-data
	android:name="WISER_SMART_APPKEY"
	android:value="Appkey" />
<meta-data
	android:name="WISER_SMART_SECRET"
	android:value="AppSecret" />
```
### (5) Aliasing Configuration

Arrange aliasing configuration in corresponding proguard-rules.pro files. 

```bash 
#fastJson
-keep class com.alibaba.fastjson.**{*;}
-dontwarn com.alibaba.fastjson.**

#mqtt
-keep class org.eclipse.paho.client.mqttv3.** { *; }
-dontwarn org.eclipse.paho.client.mqttv3.**

-dontwarn okio.**
-dontwarn rx.**
-dontwarn javax.annotation.**
-keep class com.squareup.okhttp.** { *; }
-keep interface com.squareup.okhttp.** { *; }
-keep class okio.** { *; }
-dontwarn com.squareup.okhttp.**

-keep class com.wiser.**{*;}
-dontwarn com.wiser.**

```



## Use the SDK function in codes

The WiserHomeSdk is the outbound interface of the Smart Home, and the operations include network configuration, initiation, control, room, group and ZigBee.

### (1) Initiate Wiser Smart sdk in the Application

**[Description]**

It is used to initiate components of communication services, etc.

**[Example Codes]**
```java
public class WiserSmartApp extends Application {
    @Override
    public void onCreate() {
        super.onCreate();
        WiserHomeSdk.init(this);
    }

}
```

**Note:**

The appId and appSecret need to be configured in the AndroidManifest.xml file or the build environment or the codes. 

### (2) Logout of the Wiser Smart Cloud connection

The following interface needs to be invoked to log out of the App. 
```java
WiserHomeSdk.onDestroy();
```

### (3) Monitor the invalidity of registered session 

**[Description]**

Because of abnormality or long-time absence of operation for 45 or more days, the session will become invalid, and user has to log out of the App and log in again to obtain the session. 

**[Method Invocation]**

```java
// Monitor the invalidity of session.
WiserHomeSdk.setOnNeedLoginListener(INeedLoginListener needLoginListener);
```
**[Callback]**

```java
needLoginListener.onNeedLogin(Context context);
```
**[Example Codes]**
```java
public class WiserSmartApp extends Application {

        @Override
        public void onCreate() {
            super.onCreate();
            // Register in the App.
  			  WiserHomeSdk.setOnNeedLoginListener(new INeedLoginListener(){
     		  @Override
      		  public void onNeedLogin(Context context) {

      		  }
    });
```
[**Note**]

> - In case of this kind of callback, please go to the login page and require the user to log in again. 

### (4) Use Debug mode

In the debug mode, you can enable the sdk log switch to view more log information and help you locate the problem quickly. It is recommended to turn off the log switch in release mode.

```java
WiserHomeSdk.setDebugMode(true);
```
