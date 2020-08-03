### Event binding

#### Get the scene event binding SDK

```
ITuyaSecuritySceneSdk mTuyaSecuritySceneSdk = TuyaOptimusSdk.getManager(ITuyaSecuritySceneSdk.class)
```

#### Get a list of sensing devices

###### Interface example

```java
void getSensorList(ITuyaResultCallback<Map<String, SensorBean>> callback);
```

###### Parameter Description

| parameter | Description         |
| --------- | ------------------- |
| callback  | Get result callback |

###### Return to SensorBean parameter description

| parameter   | Types of         | Description       |
| ----------- | ---------------- | ----------------- |
| deviceId    | String           | Device id         |
| actionInfos | CameraStatusBean | Bound camera list |

###### Return to CameraStatusBean parameter description

| parameter | Types of | Description                                             |
| --------- | -------- | ------------------------------------------------------- |
| entityId  | String   | Camera device id                                        |
| type      | int      | Camera binding type 1: binding picture 2: binding video |

###### Example description

```java
mTuyaSecuritySceneSdk.newEventRecordingInstance(room id).getSensorList(new ITuyaResultCallback<Map<String, SensorBean>>() {
            @Override
            public void onSuccess(Map<String, SensorBean> result) {

            }

            @Override
            public void onError(String errorCode, String errorMessage) {

            }
        });
```

#### Get the list of bound cameras

###### Interface Description

```java
void getLinkedCameras(String sensorId, ITuyaResultCallback<SensorBean> callback);
```

###### Parameter Description

| parameter | Description         |
| --------- | ------------------- |
| sensorId  | Device id           |
| callback  | Get result callback |

###### Return to SensorBean parameter description

| parameter   | Types of         | Description       |
| ----------- | ---------------- | ----------------- |
| deviceId    | String           | Device id         |
| actionInfos | CameraStatusBean | Bound camera list |

###### Return to CameraStatusBean parameter description

| parameter | Types of | Description                                             |
| --------- | -------- | ------------------------------------------------------- |
| entityId  | String   | Camera device id                                        |
| type      | int      | Camera binding type 1: binding picture 2: binding video |

###### Example description

```java
mTuyaSecuritySceneSdk.newEventRecordingInstance(room id).getLinkedCameras(device id, new ITuyaResultCallback<SensorBean>() {
            @Override
            public void onSuccess(SensorBean result) {

            }

            @Override
            public void onError(String errorCode, String errorMessage) {

            }
        });
```

#### Binding camera

###### Interface Description

```java
void linkCamera(String sensorId, ArrayList<CameraStatusBean> cameraInfos, ITuyaResultCallback<String> callback);
```

###### Parameter Description

| parameter   | Description         |
| ----------- | ------------------- |
| sensorId    | Sensor device id    |
| cameraInfos | Select camera list  |
| callback    | Get result callback |

###### Sample code

```java
mTuyaSecuritySceneSdk.newEventRecordingInstance(room id).linkCamera("device id", [camera type], new ITuyaResultCallback<String>() {
            @Override
            public void onSuccess(String result) {

            }

            @Override
            public void onError(String errorCode, String errorMessage) {

            }
        });
```

#### Get the list of cameras bound to cloud storage

###### Interface Description

```java
void getStorageBindCameraList(List<String> cameraIds, ITuyaResultCallback<ArrayList<String>> callback);
```

###### Parameter Description

| parameter | Description         |
| --------- | ------------------- |
| cameraIds | All camera id       |
| callback  | Get result callback |

###### Reference description

This interface returns the list of cameras that have been bound to cloud storage. Only cameras bound to cloud storage support linked video

###### Interface example

```java
mTuyaSecuritySceneSdk.newEventRecordingInstance(room id).getStorageBindCameraList([camera ids], new ITuyaResultCallback<String>() {
            @Override
            public void onSuccess(String result) {

            }

            @Override
            public void onError(String errorCode, String errorMessage) {

            }
        });
```