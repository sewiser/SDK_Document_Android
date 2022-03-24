# Integrate SDK

### Create Project

Build your project in the Android Studio.

### Configure the build.gradle

Add the following codes to the build.gradle file.

```groovy
android {
    defaultConfig {
        ndk {
            abiFilters "armeabi-v7a", "arm64-v8a"
        }
    }
    packagingOptions {
        pickFirst 'lib/*/libc++_shared.so' // multi aar has such so, should pick first.
    }
}
dependencies {
    implementation 'com.alibaba:fastjson:1.1.67.android'
    implementation 'com.squareup.okhttp3:okhttp-urlconnection:3.14.9'

    // Wiser Home's current latest release version:
    // add wiser lib
}

repositories {
    mavenLocal()
    jcenter()
    google()
}

```



> * **The Wiser Smart sdk solely supports the platform of armeabi-v7a architecture by default. Developer may refer to the [GitHub](https://github.com/TuyaInc/wisersmart_home_android_sdk/tree/master/so_libs) if you need other platforms.**
> * **After version 3.11.0, the so libraries of armeabi-v7a, arm64-v8a, armeabi platforms have been integrated into sdk. Please remove the relevant so-banks of sdk manually placed in the local, and use the default provided by sdk.**

### Integrated security image

Click the download button to download the security image.

![](./img/ecce9536-0afa-4509-879b-78038990003a.png)

Rename the downloaded security image to "t_s.bmp" and move it to the assets/ folder in the project directory.

![](./img/16e6be1c-16e3-4b84-b575-f093d90daa23.png)

### Set the AndroidManifest.xml

Set appkey and appSecret in the AndroidManifest.xml file, and configure corresponding permissions, etc.

```xml
<meta-data
	android:name="WISER_SMART_APPKEY"
	android:value="Appkey" />
<meta-data
	android:name="WISER_SMART_SECRET"
	android:value="AppSecret" />
```
### Proguard Configuration

please add this proguard configuration to proguard-rules.pro files.

```bash
#fastJson
-keep class com.alibaba.fastjson.**{*;}
-dontwarn com.alibaba.fastjson.**

#mqtt
-keep class com.wiser.smart.mqttclient.mqttv3.** { *; }
-dontwarn com.wiser.smart.mqttclient.mqttv3.**

#OkHttp3
-keep class okhttp3.** { *; }
-keep interface okhttp3.** { *; }
-dontwarn okhttp3.**

-keep class okio.** { *; }
-dontwarn okio.**

-keep class com.wiser.**{*;}
-dontwarn com.wiser.**

```



## Use the SDK function in codes

The WiserHomeSdk is the outbound interface of the Smart Home, and the operations include network configuration, initiation, control, room, group and ZigBee.

### Initiate SDK in the Application

**Description**

It is used to initiate components of communication services, etc.

**Example**

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

```java
WiserHomeSdk.init(Application application, String appkey, String appSerect)
```



### Logout of the Wiser Smart Cloud connection

The following interface needs to be invoked to log out of the App.
```java
WiserHomeSdk.onDestroy();
```

### Monitor the invalidity of registered session

**Description**

Because of abnormality or long-time absence of operation for 45 or more days, the session will become invalid, and user has to log out of the App and log in again to obtain the session.

**Declaration**

```java
// Monitor the invalidity of session.
WiserHomeSdk.setOnNeedLoginListener(INeedLoginListener needLoginListener);

needLoginListener.onNeedLogin(Context context);
```
**Example**

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

> **[info] Note**
>
> - In case of this kind of callback, please go to the login page and require the user to log in again.

### Debug mode

In the debug mode, you can enable the sdk log switch to view more log information and help you locate the problem quickly. It is recommended to turn off the log switch in release mode.

```java
WiserHomeSdk.setDebugMode(true);
```
