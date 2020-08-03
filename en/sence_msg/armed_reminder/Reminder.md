### Arming reminder

#### Get the scene arming reminder SDK

```
ITuyaSecuritySceneSdk mTuyaSecuritySceneSdk = TuyaOptimusSdk.getManager(ITuyaSecuritySceneSdk.class)
```

#### Get arm and disarm reminder status

```java
void getArmReminderStatus(ITuyaResultCallback<ArrayList<ArmReminderBean>> callback);
```

###### Parameter Description

| parameter | Description         |
| --------- | ------------------- |
| callback  | Get result callback |

###### Back to the ArmReminderBean description

??

| parameter | Types of | Description                                                  |
| --------- | -------- | ------------------------------------------------------------ |
| homeId    | String   | Family id                                                    |
| type      | int      | Disarming reminder to distinguish fields 1. Disarming reminder 2. Arming reminder |
| enable    | int      | Whether to open 1 open 0 close                               |

###### Example description

```java
  mTuyaSecuritySceneSdk.newGeofenceInstance(location id).getArmReminderStatus(new ITuyaResultCallback<ArrayList<ArmReminderBean>>() {
            @Override
            public void onSuccess(ArrayList<ArmReminderBean> result) {

            }

            @Override
            public void onError(String errorCode, String errorMessage) {

            }
        });
```

#### Update arm and disarm status

```java
void updateArmReminderStatus(Integer enable, Integer type, String checkTime, String timeZone, ITuyaResultCallback<Boolean> callback);
```

###### Parameter Description

| parameter | Description                                                  |
| --------- | ------------------------------------------------------------ |
| enable    | Whether to open 1 open 0 close                               |
| type      | Disarming reminder to distinguish fields 1. Disarming reminder 2. Arming reminder |
| checkTime | Unified transmission "00:00"                                 |
| timeZone  | Current user's time zone                                     |
| callback  | Get result callback                                          |

###### Example description

```java
mTuyaSecuritySceneSdk.newGeofenceInstance(gid).updateArmReminderStatus(isOpen, security mode type, "00:00", "time zone", new ITuyaResultCallback<Boolean>() {
            @Override
            public void onSuccess(Boolean result) {

            }

            @Override
            public void onError(String errorCode, String errorMessage) {

            }
        });
```