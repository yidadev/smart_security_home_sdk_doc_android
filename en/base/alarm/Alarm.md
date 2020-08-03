### Alarm

#### Obtain the arm and disarm SDK

```java
ITuyaSecurityBaseSdk mTuyaSecurityBaseSdk = TuyaOptimusSdk.getManager(ITuyaSecurityBaseSdk.class)
```

##### HomeInfoBean field information

| Field          | Types of | description                                 |
| -------------- | -------- | ------------------------------------------- |
| homeId         | String   | Family ID                                   |
| mode           | int      | Home Armed and Disarmed State               |
| alarmState     | int      | Family alarm status (0: normal; 1: alarm)   |
| alarmVoice     | int      | Home alarm sound status (0: mute; 1: alarm) |
| alarmCountdown | long     | Alarm countdown                             |

##### AlarmActionBean field information

| Field  | Types of | description                                  |
| ------ | -------- | -------------------------------------------- |
| action | String   | Alarm operation description                  |
| type   | int      | Alarm operation (0: disarm; 1: cancel alarm) |

##### EmergencyContactBean field information

| Field        | Types of | description      |
| ------------ | -------- | ---------------- |
| areaCode     | String   | Area code        |
| phone        | String   | telephone number |
| contractName | String   | Contact name     |

##### MonitorServiceStateBean field information

| Field | Types of | description                                                  |
| ----- | -------- | ------------------------------------------------------------ |
| state | int      | Service status (0: Not Set; 1: Self Monitoring; 2: Pro Monitoring) |

##### CountDownBean field information

| Field         | Types of | description  |
| ------------- | -------- | ------------ |
| deadline      | long     | deadline     |
| currentMillis | long     | current time |

##### AlarmMessageBean field information

| Field              | Types of | description                  |
| ------------------ | -------- | ---------------------------- |
| alarmId            | String   | Alarm ID                     |
| state              | int      | Message status               |
| homeId             | String   | Family ID                    |
| msgId              | String   | Message ID                   |
| msgContent         | String   | Message content              |
| msgTitle           | String   | Message title                |
| productType        | String   | Equipment category           |
| productId          | String   | Equipment category ID        |
| monitoringDeadline | long     | MC center deadline           |
| type               | String   | alarm type                   |
| typeDesc           | String   | Alarm type description       |
| gmtCreate          | long     | Creation time                |
| deviceIds          | List     | Alarm device list collection |

### Pull the alarm message list

```java
void getAlarmMessageListWithHomeId(ITuyaResultCallback<ArrayList<AlarmMessageBean>> callback)
```

##### Parameter Description

no

##### Sample code

```java
mTuyaSecurityBaseSdk.newAlarmInstance(mHomeId).getAlarmMessageListWithHomeId(new ITuyaResultCallback<ArrayList<AlarmMessageBean>>() {
            @Override
            public void onSuccess(ArrayList<AlarmMessageBean> result) {
                // do something
            }

            @Override
            public void onError(String errorCode, String errorMessage) {
                // do something
            }
        });
```

### Get the registration type of the home monitoring center

```java
void getHomeMonitorStateWithHomeId(ITuyaResultCallback<MonitorServiceStateBean> callback)
```

##### Parameter Description

no

##### Sample code

```java
mTuyaSecurityBaseSdk.newAlarmInstance(mHomeId).getHomeMonitorStateWithHomeId(new ITuyaResultCallback<MonitorServiceStateBean>() {
            @Override
            public void onSuccess(MonitorServiceStateBean result) {
                // do something
            }

            @Override
            public void onError(String errorCode, String errorMessage) {
                // do something
            }
        });
```

### Verify whether the family service includes MC services

```java
void checkLocationServiceContainMCWithHomeId(ITuyaResultCallback<ContainsMcBean> callback)
```

##### Parameter Description

no

##### Sample code

```java
mTuyaSecurityBaseSdk.newAlarmInstance(mHomeId).checkLocationServiceContainMCWithHomeId(new ITuyaResultCallback<ContainsMcBean>() {
            @Override
            public void onSuccess(ContainsMcBean result) {
                // do something
            }

            @Override
            public void onError(String errorCode, String errorMessage) {
                // do something
            }
        });
```

### Call emergency contact to report (when the user dials the emergency contact number, report mark)

```java
void makeCallEmergencyPhoneMarkWithHomeId(String phone, ITuyaResultCallback<Boolean> callback)
```

##### Parameter Description

| parameter | Description         |
| --------- | ------------------- |
| phone     | mobile phone number |

##### Sample code

```java
mTuyaSecurityBaseSdk.newAlarmInstance(mHomeId).makeCallEmergencyPhoneMarkWithHomeId(phone, new ITuyaResultCallback<Boolean>() {
            @Override
            public void onSuccess(Boolean result) {
                // do something
            }

            @Override
            public void onError(String errorCode, String errorMessage) {
                // do something
            }
        });
```

### Get alarm operation copy

```java
void getAlarmOperationTitleWithHomeId(ITuyaResultCallback<ArrayList<AlarmActionBean>> callback)
```

##### Parameter Description

no

##### Sample code

```java
mTuyaSecurityBaseSdk.newAlarmInstance(mHomeId).getAlarmOperationTitleWithHomeId(new ITuyaResultCallback<ArrayList<AlarmActionBean>>() {
            @Override
            public void onSuccess(ArrayList<AlarmActionBean> result) {
                // do something
            }

            @Override
            public void onError(String errorCode, String errorMessage) {
                // do something
            }
        });
```

### Alarm emergency contact list

```java
void getAlarmEmergencyConnectWithHomeId(ITuyaResultCallback<ArrayList<EmergencyContactBean>> callback)
```

##### Parameter Description

no

##### Sample code

```java
mTuyaSecurityBaseSdk.newAlarmInstance(mHomeId).getAlarmEmergencyConnectWithHomeId(new ITuyaResultCallback<ArrayList<EmergencyContactBean>>() {
            @Override
            public void onSuccess(ArrayList<EmergencyContactBean> result) {
                // do something
            }

            @Override
            public void onError(String errorCode, String errorMessage) {
                // do something
            }
        });
```

### Get the alarm automatically sent to the MC countdown

```java
void getAlarmAutoSendMCCountDownTimeWithHomeId(ITuyaResultCallback<CountDownBean> callback)
```

##### Parameter Description

no

##### Sample code

```java
mTuyaSecurityBaseSdk.newAlarmInstance(mHomeId).getAlarmAutoSendMCCountDownTimeWithHomeId(new ITuyaResultCallback<CountDownBean>() {
            @Override
            public void onSuccess(CountDownBean result) {
                // do something
            }

            @Override
            public void onError(String errorCode, String errorMessage) {
                // do something
            }
        });
```

### Report the alarm to the monitoring center

```java
void sendAlarmToMonitorCenterWithHomeId(String alarmId, ITuyaResultCallback<Boolean> callback)
```

##### Parameter Description

| parameter | Description |
| --------- | ----------- |
| alarmId   | Alarm ID    |

##### Sample code

```java
mTuyaSecurityBaseSdknewAlarmInstance(mHomeId).sendAlarmToMonitorCenterWithHomeId(alarmId, new ITuyaResultCallback<Boolean>() {
            @Override
            public void onSuccess(Boolean result) {
                // do something
            }

            @Override
            public void onError(String errorCode, String errorMessage) {
                // do something
            }
        });
```

### Alarm page operation events (sound switch, cancel alarm, disarm and cancel alarm)

```java
void updateLocationAlarmStatusWithHomeId(Integer state, ITuyaResultCallback<Boolean> callback)
```

##### Parameter Description

| parameter | Description                                                  |
| --------- | ------------------------------------------------------------ |
| state     | Status (0: cancel the alarm; 1: disarm; 10: turn on the sound; 11: turn off the sound) |

##### Sample code

```java
mTuyaSecurityBaseSdk.newAlarmInstance(mHomeId).updateLocationAlarmStatusWithHomeId(state, new ITuyaResultCallback<Boolean>() {
            @Override
            public void onSuccess(Boolean result) {
                // do something
            }

            @Override
            public void onError(String errorCode, String errorMessage) {
                // do something
            }
        });
```

### Get the sound status of the alarm page

```java
void getLocationAlarmVoiceStateWithHomeId(ITuyaResultCallback<HomeInfoBean> callback)
```

##### Parameter Description

no

##### Sample code

```java
mTuyaSecurityBaseSdk.newAlarmInstance(mHomeId).getLocationAlarmVoiceStateWithHomeId(new ITuyaResultCallback<HomeInfoBean>() {
            @Override
            public void onSuccess(HomeInfoBean result) {
                // do something
            }

            @Override
            public void onError(String errorCode, String errorMessage) {
                // do something
            }
        });
```