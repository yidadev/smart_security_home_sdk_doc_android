- # 1. Integrate SDK

  ## 1.1. Create Project

  Create a new project in Android Studio.

  ## 1.2. Configure build.gradle

  Add the dependencies downloaded in the integration preparation to the build.gradle file.

  ```groovy
  defaultConfig {
      ndk {
          abiFilters "armeabi-v7a"
      }
   }
      dependencies {
          implementation 'com.alibaba:fastjson:1.1.67.android'
          implementation 'com.squareup.okhttp3:okhttp-urlconnection:3.12.3'
          implementation 'com.tuya.smart:tuyasmart-security-basesdk:2.1.0-rc.1'
          implementation 'com.tuya.smart:optimus:1.0.1'
          annotationProcessor 'com.tuya.smart:optimus-compiler:1.0.0'
      }
  ```

  Add jcenter() and Tuya external warehouse to the build.gradle file in the root directory

  ```groovy
  repositories {
      jcenter()
      maven {
          url "https://maven-other.tuya.com/repository/maven-releases/"
      }
  }
  ```

  Tips

  - The SDK of Tuya Smart version before 3.10.0 only supports armeabi-v7a by default.
  - After version 3.11.0, armeabi-v7a and arm64-v8a have been integrated into the SDK. Please remove the relevant so library of the SDK manually placed locally and use the one provided in the SDK.
  - If you integrate the new version of the so library. Please remove the libraries manually integrated in the previous version to prevent conflicts or problems caused by inconsistent code versions
  - If you need other platforms, you can go to [GitHub to](https://github.com/TuyaInc/tuyasmart_home_android_sdk/tree/master/so_libs) get it.
  - The security SDK already contains all the functions of homeSDK, and there is no need to introduce'com.tuya.smart:tuyasmart:xxx' in the integration of Tuya services such as ipc and network distribution.

###1.1.3 Integrated into a safe picture

Click "Download Safe Picture"-"Safe Picture Download" to download the safe picture.

![img](https://tuyainc.github.io/tuyasmart_home_android_sdk_doc/en/resource/images/download_t_s.png)

Rename the downloaded security image to "t_s.bmp" and move it to the assets/ folder in the project directory.

![img](https://tuyainc.github.io/tuyasmart_home_android_sdk_doc/en/resource/images/addt_s.png)

###  1.1.4. Set the AndroidManifest.xml

Set appkey and appSecret in the AndroidManifest.xml file, and configure corresponding permissions, etc.

```xml
<meta-data
    android:name="TUYA_SMART_APPKEY"
    android:value="Appkey" />
<meta-data
    android:name="TUYA_SMART_SECRET"
    android:value="AppSecret" />
```

### 1.1.5. Proguard Configuration

please add this proguard configuration to proguard-rules.pro files.

```bash
#fastJson
-keep class com.alibaba.fastjson.**{*;}
-dontwarn com.alibaba.fastjson.**

#mqtt
-keep class com.tuya.smart.mqttclient.mqttv3.** { *; }
-dontwarn com.tuya.smart.mqttclient.mqttv3.**

#OkHttp3
-keep class okhttp3.** { *; }
-keep interface okhttp3.** { *; }
-dontwarn okhttp3.**

-keep class okio.** { *; }
-dontwarn okio.**

-keep class com.tuya.**{*;}
-dontwarn com.tuya.**
```

## 1.2. Use the SDK function in codes

The TuyaHomeSdk is the outbound interface of the Smart Home, and the operations include network configuration, initiation, control, room, group and ZigBee.

### 1.2.1. Initiate SDK in the Application

**Description**

It is used to initiate components of communication services, etc.

**Example**

```java
public class TuyaSmartApp extends Application {
    @Override
    public void onCreate() {
        super.onCreate();
        TuyaHomeSdk.init(this);
        TuyaOptimusSdk.init(this);
    }
}
```

**Note:**

The appId and appSecret need to be configured in the AndroidManifest.xml file or the build environment or the codes.

```java
TuyaHomeSdk.init(Application application, String appkey, String appSerect)
```

### 1.2.2. Logout of the Tuya Smart Cloud connection

The following interface needs to be invoked to log out of the App.

```java
TuyaHomeSdk.onDestroy();
```

### 1.2.3. Monitor the invalidity of registered session

**Description**

Because of abnormality or long-time absence of operation for 45 or more days, the session will become invalid, and user has to log out of the App and log in again to obtain the session.

**Declaration**

```java
// Monitor the invalidity of session.
TuyaHomeSdk.setOnNeedLoginListener(INeedLoginListener needLoginListener);

needLoginListener.onNeedLogin(Context context);
```

**Example**

```java
public class TuyaSmartApp extends Application {

        @Override
        public void onCreate() {
            super.onCreate();
            // Register in the App.
                TuyaHomeSdk.setOnNeedLoginListener(new INeedLoginListener(){
               @Override
                public void onNeedLogin(Context context) {

                }
    });
```

> **[info] Note**
>
> - In case of this kind of callback, please go to the login page and require the user to log in again.

###  1.2.4. Debug mode

In the debug mode, you can enable the sdk log switch to view more log information and help you locate the problem quickly. It is recommended to turn off the log switch in release mode.

```java
TuyaHomeSdk.setDebugMode(true);
```

