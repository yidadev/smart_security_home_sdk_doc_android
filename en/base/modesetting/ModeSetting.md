### Mode setting

#### Obtain the arm and disarm SDK

```java
ITuyaSecurityBaseSdk mTuyaSecurityBaseSdk = TuyaOptimusSdk.getManager(ITuyaSecurityBaseSdk.class)
```

##### DelayDateBean field information

| Field           | Types of | description                                 |
| --------------- | -------- | ------------------------------------------- |
| mode            | String   | Armed state (1: at home; 2: away from home) |
| enableDelayTime | int      | Countdown to Arming                         |
| alarmDelayTime  | int      | Alarm countdown                             |

##### DelayTimeBean field information

| Field           | Types of | description         |
| --------------- | -------- | ------------------- |
| enableDelayTime | int      | Countdown to Arming |
| alarmDelayTime  | int      | Alarm countdown     |

##### SaveModeSettingBean field information

| Field     | Types of | description                     |
| --------- | -------- | ------------------------------- |
| gatewayId | String   | Gateway ID                      |
| deviceIds | List     | Child device ID list collection |

### Get a list of delay rules for all modes

##### Interface Description

```java
void getAllModeDelayRuleWithHomeId(ITuyaResultCallback<ArrayList<DelayDateBean>> callback)
```

##### Parameter Description

no

##### Sample code

```java
mTuyaSecurityBaseSdk.newModeSettingInstance(mHomeId).getAllModeDelayRuleWithHomeId(new ITuyaResultCallback<ArrayList<DelayDateBean>>() {
            @Override
            public void onSuccess(ArrayList<DelayDateBean> result) {
                // do something
            }

            @Override
            public void onError(String errorCode, String errorMessage) {
                // do something
            }
        });
```

### Get the delay rule in the specified mode

##### Interface Description

```java
void getDelayTimeWithMode(String mode, ITuyaResultCallback<DelayTimeBean> callback)
```

##### Parameter Description

| parameter | Description                                 |
| --------- | ------------------------------------------- |
| mode      | Armed state (1: at home; 2: away from home) |

##### Sample code

```java
mTuyaSecurityBaseSdk.newModeSettingInstance(mHomeId).getDelayTimeWithMode(mode, new ITuyaResultCallback<DelayTimeBean>() {
            @Override
            public void onSuccess(DelayTimeBean result) {
                // do something
            }

            @Override
            public void onError(String errorCode, String errorMessage) {
                // do something
            }
        });
```

### Save the delay rule in the specified mode

##### Interface Description

```java
void saveDelayTimeWithDelayRule(String mode, int enableDelayTime, int alarmDelayTime, ITuyaResultCallback<Boolean> callback)
```

##### Parameter Description

| parameter       | Description                                 |
| --------------- | ------------------------------------------- |
| mode            | Armed state (1: at home; 2: away from home) |
| enableDelayTime | Countdown to Arming                         |
| alarmDelayTime  | Alarm countdown                             |

##### Sample code

```java
mTuyaSecurityBaseSdk.newModeSettingInstance(mHomeId).saveDelayTimeWithDelayRule(mode, enableDelayTime, alarmDelayTime, new ITuyaResultCallback<Boolean>() {
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

### Save the list of device rules in the specified mode

##### Interface Description

```java
void saveDeviceListWithMode(String mode, ArrayList<SaveModeSettingBean> data, ITuyaResultCallback<Boolean> callback)
```

##### Parameter Description

| parameter | Description                                 |
| --------- | ------------------------------------------- |
| mode      | Armed state (1: at home; 2: away from home) |
| data      | Armed device rule data                      |

##### Sample code

```java
mTuyaSecurityBaseSdk.newModeSettingInstance(mHomeId).saveDeviceListWithMode(mode, data, new ITuyaResultCallback<Boolean>() {
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

### Get the list of device rules in the specified mode

##### Interface Description

```java
void getDeviceListWithMode(String mode, ITuyaResultCallback<ArrayList<ModeSettingDeviceBean>> callback)
```

##### Parameter Description

| parameter | Description                                 |
| --------- | ------------------------------------------- |
| mode      | Armed state (1: at home; 2: away from home) |

##### Sample code

```java
mTuyaSecurityBaseSdk.newModeSettingInstance(mHomeId).getDeviceListWithMode(mode, new ITuyaResultCallback<ArrayList<ModeSettingDeviceBean>>() {
            @Override
            public void onSuccess(ArrayList<ModeSettingDeviceBean> result) {
                // do something
            }

            @Override
            public void onError(String errorCode, String errorMessage) {
                // do something
            }
        });
```