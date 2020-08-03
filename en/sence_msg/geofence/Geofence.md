### Geofence

#### Get the scene geofencing SDK

```
ITuyaSecuritySceneSdk mTuyaSecuritySceneSdk = TuyaOptimusSdk.getManager(ITuyaSecuritySceneSdk.class)
```

#### Upload mobile device information

###### Interface Description

```java
void uploadDeviceInfo(String deviceId,String deviceName,ITuyaResultCallback<Boolean> callback);
```

###### Parameter Description

| parameter  | Description                     |
| :--------- | ------------------------------- |
| deviceId   | Mobile unique identification id |
| deviceName | Phone device name               |
| callback   | Get the result callback         |

###### Sample code

```java
mTuyaSecuritySceneSdk.newGeofenceInstance(10000L).uploadDeviceInfo("phone id","phone name", new             ITuyaResultCallback<Boolean>() {
         @Override
         public void onSuccess(Boolean result) {
             //do something
        }

         @Override
         public void onError(String errorCode, String errorMessage) {
             //do something
         }
 });
```

#### Set frequently used phones

###### Interface Description

```java
void setCommonlyUsedDevice(String deviceId, ITuyaResultCallback<Boolean> callback);
```

###### Parameter Description

| parameter | Description                     |
| --------- | ------------------------------- |
| deviceId  | Mobile unique identification id |
| callback  | Get the result callback         |

###### Sample code

```java
mTuyaSecuritySceneSdk.newGeofenceInstance(location id).setCommonlyUsedDevice("phone id", new                        ITuyaResultCallback<Boolean>() {
            @Override
            public void onSuccess(Boolean result) {
                //do something
            }

            @Override
            public void onError(String errorCode, String errorMessage) {
                //do something
            }
});
```

#### Save information about geofencing

###### FenceMessageBean parameter description

| parameter | Description                       |
| --------- | --------------------------------- |
| lon       | Current family longitude          |
| lat       | Current family latitude           |
| title     | Current home location information |
| radius    | Current home geofence radius      |

###### Interface Description

```java
void recordInitialDeviceStatus(FenceMessageBean fenceMessageBean,
                               ITuyaResultCallback<Boolean> callback);
```

###### Parameter Description

| parameter        | Description                                      |
| ---------------- | ------------------------------------------------ |
| fenceMessageBean | Information about geofencing home initialization |
| callback         | Get the result callback                          |

###### Sample code

```java
FenceMessageBean fenceMessage = new FenceMessageBean("location lat","location lon","location info","location radius");
mTuyaSecuritySceneSdk.newGeofenceInstance(location id).recordInitialDeviceStatus(fenceMessage, new ITuyaResultCallback<Boolean>() {
            @Override
            public void onSuccess(Boolean result) {

            }

            @Override
            public void onError(String errorCode, String errorMessage) {

            }
        });
```

#### Mobile phone leaves or enters the geofence

###### Interface Description

```java
void processDeviceInfo(String deviceId, String homeId, Boolean isLeaving, ITuyaResultCallback<Boolean> callback);
```

###### Parameter Description

| parameter | Description                                          |
| --------- | ---------------------------------------------------- |
| deviceId  | Mobile unique identification id                      |
| homeId    | The homeId of the family that triggered the geofence |
| isLeaving | Is it away from home                                 |
| callback  | Get the result callback                              |

###### Sample code

```java
  mTuyaSecuritySceneSdk.newGeofenceInstance(location id).processDeviceInfo("phone id", "locaiton genfence id", false, new ITuyaResultCallback<Boolean>() {
            @Override
            public void onSuccess(Boolean result) {

            }

            @Override
            public void onError(String errorCode, String errorMessage) {

            }
        });
```

#### Query all home geofences based on device id

###### Interface Description

```java
void getHomeByIds(String deviceId,ITuyaResultCallback<ArrayList<FenceDetailBean>> callback);
```

###### Entry description

| parameter | Description                               |
| --------- | ----------------------------------------- |
| deviceId  | Unique identification id of mobile device |
| callback  | Get result callback                       |

###### Return to FenceDetailBean description

| parameter | Types of         | Description                                                  |
| --------- | ---------------- | ------------------------------------------------------------ |
| enable    | Int              | Whether to open 1 open 0 close                               |
| homeId    | String           | Family id                                                    |
| data      | FenceMessageBean | Family latitude and longitude radius and location information |

###### Return parameter description of FenceMessageBean

| parameter | Description                       |
| --------- | --------------------------------- |
| lon       | Current family longitude          |
| lat       | Current family latitude           |
| title     | Current home location information |
| radius    | Current home geofence radius      |

###### Sample code

```java
mTuyaSecuritySceneSdk.newGeofenceInstance(location id).getHomeByIds("phone id", new ITuyaResultCallback<ArrayList<FenceDetailBean>>() {
            @Override
            public void onSuccess(ArrayList<FenceDetailBean> result) {

            }

            @Override
            public void onError(String errorCode, String errorMessage) {

            }
        });
```

#### Switch geofencing based on family id

###### Interface Description

```java
void switchGeoFence(String homeId, Integer fenceStatus, ITuyaResultCallback<Boolean> callback);
```

###### Parameter Description

| parameter   | Description                      |
| ----------- | -------------------------------- |
| homeId      | Family id                        |
| fenceStatus | Whether to open 1: open 0: close |
| callback    | Get result callback              |

###### Sample code

```java
mTuyaSecuritySceneSdk.newGeofenceInstance(location id).switchGeoFence("location id", 1, new ITuyaResultCallback<Boolean>() {
            @Override
            public void onSuccess(Boolean result) {

            }

            @Override
            public void onError(String errorCode, String errorMessage) {

            }
        });
```

#### Switch home geofencing service

###### Interface Description

```java
void switchGeoService(Integer geoStatus, ITuyaResultCallback<Boolean> callback);
```

###### Parameter Description

| parameter | Description                                             |
| --------- | ------------------------------------------------------- |
| geoStatus | Whether to open the geofencing service 1: open 0: close |
| callback  | Get result callback                                     |

###### Sample code

```java
mTuyaSecuritySceneSdk.newGeofenceInstance(locaiton id).switchGeoService(1, new ITuyaResultCallback<Boolean>() {
            @Override
            public void onSuccess(Boolean result) {

            }

            @Override
            public void onError(String errorCode, String errorMessage) {

            }
        });
```

#### Get home geofencing service status

###### Interface Description

```java
void getGeoServiceStatus(ITuyaResultCallback<Boolean> callback);
```

###### Parameter Description

| parameter | Description         |
| --------- | ------------------- |
| callback  | Get result callback |

###### Sample code

```java
mTuyaSecuritySceneSdk.newGeofenceInstance(location id).getGeoServiceStatus(new ITuyaResultCallback<Boolean>() {
            @Override
            public void onSuccess(Boolean result) {

            }

            @Override
            public void onError(String errorCode, String errorMessage) {

            }
        });
```

#### Acquire family members who can participate in family geofencing

###### Interface Description

```java
void getGeoFenceMemberList(ITuyaResultCallback<ArrayList<FenceMemberBean>> callback);
```

###### Parameter Description

| parameter | Description         |
| --------- | ------------------- |
| callback  | Get result callback |

###### Back to FenceMemberBean description

| parameter   | Types of | Description                          |
| ----------- | -------- | ------------------------------------ |
| mobile      | String   | phone number                         |
| email       | String   | mailbox                              |
| nickname    | String   | nickname                             |
| uid         | Stirng   | Member identification unique id      |
| username    | Stirng   | username                             |
| isEffective | Int      | Whether to participate in geofencing |

###### Sample code

```java
mTuyaSecuritySceneSdk.newGeofenceInstance(location id).getGeoFenceMemberList(new ITuyaResultCallback<ArrayList<FenceMemberBean>>() {
            @Override
            public void onSuccess(ArrayList<FenceMemberBean> result) {

            }

            @Override
            public void onError(String errorCode, String errorMessage) {

            }
        });
```

#### Get location switch status

###### Interface Description

```java
void getGeoFenceDetailStatus(ITuyaResultCallback<Boolean> callback);
```

###### Parameter Description

| parameter | Description         |
| --------- | ------------------- |
| callback  | Get result callback |

###### Sample code

```java
mTuyaSecuritySceneSdk.newGeofenceInstance(locaiton id).getGeoFenceDetailStatus(new ITuyaResultCallback<Boolean>() {
            @Override
            public void onSuccess(Boolean result) {

            }

            @Override
            public void onError(String errorCode, String errorMessage) {

            }
        });
```

#### Get geofence details

###### Interface Description

```java
void getHomeGeoFencingData(ITuyaResultCallback<FenceDetailBean> callback);
```

###### Parameter Description

| parameter | Description         |
| --------- | ------------------- |
| callback  | Get result callback |

###### FenceDetailBean return parameter description

| parameter | Types of         | Description                               |
| --------- | ---------------- | ----------------------------------------- |
| enable    | int              | Whether to enable home geofence           |
| homeId    | String           | Family ID                                 |
| data      | FenceMessageBean | Family latitude and longitude information |

###### FenceMessageBean return parameter description

| parameter | Description                       |
| --------- | --------------------------------- |
| lon       | Current family longitude          |
| lat       | Current family latitude           |
| title     | Current home location information |
| radius    | Current home geofence radius      |

###### Sample code

```java
mTuyaSecuritySceneSdk.newGeofenceInstance(locatoin id).getHomeGeoFencingData(new ITuyaResultCallback<FenceDetailBean>() {
            @Override
            public void onSuccess(FenceDetailBean result) {

            }

            @Override
            public void onError(String errorCode, String errorMessage) {

            }
        });
```

#### Switch whether users participate in geofencing

###### Interface Description

```java
void toggleMemberGeoFence(Integer isEffective, String uid, ITuyaResultCallback<Boolean> callback);
```

###### Parameter Description

| parameter   | Description                                             |
| ----------- | ------------------------------------------------------- |
| isEffective | Whether the user joins the home geofence Open 1 Close 0 |
| uid         | Unique user id                                          |
| callback    | Get result callback                                     |

###### Example description

```java
mTuyaSecuritySceneSdk.newGeofenceInstance(家庭id).toggleMemberGeoFence(1, "user id", new ITuyaResultCallback<Boolean>() {
            @Override
            public void onSuccess(Boolean result) {

            }

            @Override
            public void onError(String errorCode, String errorMessage) {

            }
        });
```

#### Delete user's mobile device

###### Interface Description

```java
void deleteDevice(String deviceId, ITuyaResultCallback<Boolean> callback);
```

###### Parameter Description

| parameter | Description                            |
| --------- | -------------------------------------- |
| deviceId  | Unique identification of mobile device |
| callback  | Get result callback                    |

###### Example description

```java
mTuyaSecuritySceneSdk.newGeofenceInstance(家庭id).deleteDevice("phone id", new ITuyaResultCallback<Boolean>() {
            @Override
            public void onSuccess(Boolean result) {

            }

            @Override
            public void onError(String errorCode, String errorMessage) {

            }
        });
```

#### Get phone list

###### Interface Description

```java
 void getDeviceList(ITuyaResultCallback<ArrayList<GeofenceDeviceBean>> callback);
```

###### Parameter Description

| parameter | Description         |
| --------- | ------------------- |
| callback  | Get result callback |

###### Reference GeofenceDeviceBean description

| parameter | Types of | Description                                                  |
| --------- | -------- | ------------------------------------------------------------ |
| active    | int      | Whether the machine has been used to determine the geofence basis 1 is 0 no |
| name      | String   | Phone name                                                   |
| uuid      | String   | Unique identification of mobile device                       |

###### Example description

```java
mTuyaSecuritySceneSdk.newGeofenceInstance(location id).getDeviceList(new ITuyaResultCallback<ArrayList<GeofenceDeviceBean>>() {
                @Override
                public void onSuccess(ArrayList<GeofenceDeviceBean> result) {

                }

                @Override
                public void onError(String errorCode, String errorMessage) {

                }
            });
```