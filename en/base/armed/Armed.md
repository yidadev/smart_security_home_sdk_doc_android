### Alarm

#### Obtain the arm and disarm SDK

```java
ITuyaSecurityBaseSdk mTuyaSecurityBaseSdk = TuyaOptimusSdk.getManager(ITuyaSecurityBaseSdk.class)
```

##### GatewayModeBean field information

| Field   | Types of | description                                                  |
| ------- | -------- | ------------------------------------------------------------ |
| state   | int      | Arming and disarming execution state (0: initial state; 1: start task; 2: continue task; 3: terminate task; 4: all success; 5: all failure; 6: part of abnormal state) |
| mode    | int      | Armed and disarmed state (0: disarmed; 1: at home; 2: away from home) |
| majorId | String   | Home main gateway ID                                         |
| detail  | List     | Gateway list details                                         |

##### GatewayDetailBean field information

| Field | Types of | description                             |
| ----- | -------- | --------------------------------------- |
| gwId  | String   | Gateway ID                              |
| state | int      | Gateway status (0: abnormal; 1: normal) |

##### BypassDetailBean field information

| Field  | Types of | description                             |
| ------ | -------- | --------------------------------------- |
| gwId   | String   | Gateway ID                              |
| state  | int      | Gateway status (0: abnormal; 1: normal) |
| bypass | List     | Bypass device nodeID list               |

##### BypassDetailBean field information

| Field  | Types of | description                             |
| ------ | -------- | --------------------------------------- |
| gwId   | String   | Gateway ID                              |
| state  | int      | Gateway status (0: abnormal; 1: normal) |
| ignore | List     | Ignore the device nodeID list           |

##### HomeInfoBean field information

| Field          | Types of | description                                 |
| -------------- | -------- | ------------------------------------------- |
| homeId         | String   | Family ID                                   |
| mode           | int      | Home Armed and Disarmed State               |
| alarmState     | int      | Family alarm status (0: normal; 1: alarm)   |
| alarmVoice     | int      | Home alarm sound status (0: mute; 1: alarm) |
| alarmCountdown | long     | Alarm countdown                             |

##### TYSecurityModeErrorType field information

| Field                    | Types of | description                       |
| ------------------------ | -------- | --------------------------------- |
| QueryModeError           | Enum     | Failed to query the arming status |
| SwitchModeError          | Enum     | Failed to switch arming state     |
| QueryIgnoreDeviceError   | Enum     | Ignore device query failure       |
| QueryBypassDeviceError   | Enum     | Bypass device query failed        |
| QueryAbnormalDeviceError | Enum     | Failed to query abnormal device   |

##### Mqtt 52 protocol callback monitoring

Register Mqtt52 protocol listener

```java
mTuyaSecurityBaseSdk.newGatewayInstance(mHomeId).registerProtocolListener(mTuyaProtocolListener)
```

Destroy the Mqtt52 protocol listener

```java
mTuyaSecurityBaseSdk.newGatewayInstance(mHomeId).unRegisterProtocolListener(mTuyaProtocolListener)
```

Reference interface **ITuyaProtocolListener**

| Method name                   | Method description                                   |
| ----------------------------- | ---------------------------------------------------- |
| onProcessBypassNotice         | Handling Bypass device notifications                 |
| onProcessArmResultNotice      | Handle the notification of successful arm and disarm |
| onProcessArmCountDownNotice   | Handle the countdown notification                    |
| onProcessAlarmCountDownNotice | Handle alarm countdown notification                  |
| onProcessTamperAlarmNotice    | Handling anti-tamper alarm notifications             |
| onProcessAddGatewayNotice     | Processing the notification of adding a gateway      |
| onProcessNewAlarmNotice       | Processing new alarm notification                    |
| onProcessUpdateAlarmNotice    | Processing alarm update notification                 |
| onProcessAlarmStateNotice     | Processing alarm status notification                 |
| onProcessAlarmVoiceNotice     | Processing alarm sound notification                  |

```java
public interface ITuyaProtocolListener {
    void onProcessBypassNotice(NormalResult result);
  
    void onProcessArmResultNotice(NormalResult result);

    void onProcessArmCountDownNotice(CountDownResult result);

    void onProcessAlarmCountDownNotice(CountDownResult result);


    void onProcessTamperAlarmNotice();

    void onProcessAddGatewayNotice();
  
    void onProcessNewAlarmNotice(AlarmResult result);

    void onProcessUpdateAlarmNotice();

    void onProcessAlarmStateNotice(AlarmResult result);

    void onProcessAlarmVoiceNotice(AlarmResult result);
}
```

##### Security gateway monitoring callback

Register Security Gateway Listener

```java
mTuyaSecurityBaseSdk.newGatewayInstance(mHomeId).registerGatewayListener(mTuyaGatewayListener)
```

Destroy the security gateway listener

```java
mTuyaSecurityBaseSdk.newGatewayInstance(mHomeId).unRegisterGatewayListener(mTuyaGatewayListener)
```

Reference interface **ITuyaGatewayListener**

| Method name                        | Method description                                           |
| ---------------------------------- | ------------------------------------------------------------ |
| onSecurityModeWillSwitchAfterDelay | Get the countdown after arming and disarming switch from the gateway |
| didReceiveUnusualDevice            | Get a list of ignored devices from the cloud                 |
| onIgnoreDeviceFromGateway          | Get the list of ignored devices from the gateway             |

```java
public interface ITuyaGatewayListener {

    void onSecurityModeWillSwitchAfterDelay(int countDownTime);
    void didReceiveUnusualDevice(ArrayList<String> deviceIds);

    void onIgnoreDeviceFromGateway(JSONArray devices);

}
```

### Get a list of gateways

##### Interface Description

```java
void getLocationGateWayDeviceWithHomeId(ITuyaResultCallback<ArrayList<String>> callback)
```

##### Parameter Description

no

##### Sample code

```java
mTuyaSecurityBaseSdk.newGatewayInstance(mHomeId).getLocationGateWayDeviceWithHomeId(new ITuyaResultCallback<ArrayList<String>>() {
            @Override
            public void onSuccess(ArrayList<String> result) {
                // do something
            }

            @Override
            public void onError(String errorCode, String errorMessage) {
                // do something
            }
        });
```

### Switch arm and disarm mode

##### Interface Description

```java
void switchHomeModeWithHomeId(String mode, ITuyaResultCallback<String> callback)
```

##### Parameter Description

| parameter | Description                                                  |
| --------- | ------------------------------------------------------------ |
| mode      | Armed and disarmed state (0: disarmed; 1: at home; 2: away from home) |

##### Sample code

```java
mTuyaSecurityBaseSdk.newArmedInstance(mHomeId).switchHomeModeWithHomeId(mode,object :ITuyaResultCallback<String>{
        override fun onSuccess(result: String?) {
            // do something
        }

        override fun onError(errorCode: String?, errorMessage: String?) {
            // do something
        }

    })
```

##### Trigger interface callback

In the process of switching arming and disarming, if there is an ignored device, and the gateway needs to be queried locally, it will trigger the ArmedGatewayListener.onIgnoreDeviceFromGateway() method interface callback, and return the ignored device list collection

```java
mArmedGatewayListener.onIgnoreDeviceFromGateway(deviceIds);
```

Otherwise, the arming and disarming will be carried out directly, and the ITuyaProtocolListener.onProcessPreModeSwitchNotice() method interface callback will be triggered before the arming and disarming is executed, and the preconditioning state of the family's arming and disarming will be returned.

```java
mTuyaProtocolListener.onProcessPreModeSwitchNotice(result);
```

When the countdown of arming and disarming is completed, the arming and disarming is executed successfully, and the ITuyaProtocolListener.onProcessRealModeSwitchNotice() method interface callback will be triggered

```java
mTuyaProtocolListener.onProcessRealModeSwitchNotice(result);
```

### Query current arm and disarm status

##### Interface Description

```java
void getHomeModeWithHomeId(ITuyaResultCallback<HomeModeGetBean> callback)
```

##### Parameter Description

no

##### Sample code

```java
mTuyaSecurityBaseSdk.newArmedInstance(mHomeId).getHomeModeWithHomeId(object :ITuyaResultCallback<HomeModeGetBean>{
    override fun onSuccess(result: HomeModeGetBean?) {
        // do something
    }

    override fun onError(errorCode: String?, errorMessage: String?) {
        // do something
    }
})
```

### Initiate SOS alarm

##### Interface Description

```java
void startSOSAlarmWithHomeId(SosAlarmType type,ITuyaResultCallback<Boolean> callback)
```

| parameter | Description    |
| --------- | -------------- |
| type      | SOS alarm type |

##### Sample code

```java
mTuyaSecurityBaseSdk.newArmedInstance(mHomeId).startSOSAlarmWithHomeId(SosAlarmType.SOS_FIRE,object :ITuyaResultCallback<Boolean>{
    override fun onSuccess(result: Boolean?) {
        // do something
    }

    override fun onError(errorCode: String?, errorMessage: String?) {
        // do something
    }
})
```

### Query bypass device

##### Interface Description

```java
void queryLocationBypssDevicesWithHomeId(ITuyaResultCallback<ArrayList<BypassDetailBean>> callback)
```

##### Parameter Description

no

##### Sample code

```java
mTuyaSecurityBaseSdk.newArmedInstance(mHomeId).queryLocationBypssDevicesWithHomeId(object :ITuyaResultCallback<ArrayList<BypassDetailBean>>{
    override fun onSuccess(result: ArrayList<BypassDetailBean>?) {
        // do something
    }

    override fun onError(errorCode: String?, errorMessage: String?) {
        // do something
    }
})
```

### Get device exception information (home page interface)

##### Interface Description

```java
 void queryLocationAbnormalDevicesWithHomeId(ITuyaResultCallback<ArrayList<DpAbnormalBean>> callback)
```

##### Parameter Description

no

##### Sample code

```java
mTuyaSecurityBaseSdk.newArmedInstance(mHomeId).queryLocationAbnormalDevicesWithHomeId(object :ITuyaResultCallback<ArrayList<DpAbnormalBean>>{
    override fun onSuccess(result: ArrayList<DpAbnormalBean>?) {
        // do something
    }

    override fun onError(errorCode: String?, errorMessage: String?) {
        // do something
    }
})
```

### Query ignore devices (each gateway)

##### Interface Description

```java
void queryIgnoreDeviceFromGateway(String deviceId, ArmModeStatus mode, ITuyaResultCallback<Boolean> callback)
```

##### Parameter Description

| parameter | Description            |
| --------- | ---------------------- |
| deviceId  | Gateway device ID      |
| mode      | Current gateway status |

##### Sample code

```java
mTuyaSecurityBaseSdk.newGatewayInstance(mHomeId).queryIgnoreDeviceFromGateway(deviceId, ArmModeStatus.LEAVING,object :ITuyaResultCallback<Boolean>{
        override fun onSuccess(result: Boolean?) {
            // do something
        }

        override fun onError(errorCode: String?, errorMessage: String?) {
            // do something
        }
    })
```

##### Trigger interface callback

When getting ignored devices from the gateway, it will trigger the ITuyaGatewayListener.onIgnoreDeviceFromGateway() callback to get the JSON array ID set of the devices ignored by the current gateway

```java
mTuyaGatewayListener.onIgnoreDeviceFromGateway(jsonArray)
```

### Get home alarm status (called at startup, including alarm countdown information)

##### Interface Description

```java
void getHomeAlarmStateWithHomeId(ITuyaResultCallback<HomeInfoBean> callback)
```

##### Parameter Description

no

##### Sample code

```java
mTuyaSecurityBaseSdk.newArmedInstance(mHomeId).getHomeAlarmStateWithHomeId(object : ITuyaResultCallback<HomeInfoBean?> {
        override fun onSuccess(result: HomeInfoBean?) {
            // do something
        }

        override fun onError(errorCode: String, errorMessage: String) {
            // do something
        }
    })
```

### Error callback

##### Interface Description

```java
public interface ITuyaErrorListener {

    void handlerError(TYSecurityModeErrorType errorType, String errorMsg);
}
```

##### Register to listen

```java
mTuyaSecurityBaseSdk.newGatewayInstance(mHomeId).registerHandleErrorListener(mHandleErrorListener);
```

### Set gateway voice password

##### Interface Description

```java
void setGatewayVoicePasswordWithHomeId(Integer type, String password, ITuyaResultCallback<Boolean> callback)
```

| parameter | Description                                              |
| --------- | -------------------------------------------------------- |
| type      | Setting type (1: family dimension; 2: gateway dimension) |
| password  | Voice password                                           |

##### Sample code

```java
mTuyaSecurityBaseSdk.newArmedInstance(mHomeId).setGatewayVoicePasswordWithHomeId(type, password, object : ITuyaResultCallback<Boolean?> {
        override fun onSuccess(result: Boolean?) {
            // do something
        }

        override fun onError(errorCode: String, errorMessage: String) {
            // do something
        }
    })
```

### Get the home gateway voice password is set

##### Interface Description

```java
void getGatewayVoicePasswordStateWithHomeId(Integer type, ITuyaResultCallback<String> callback)
```

| parameter | Description                                              |
| --------- | -------------------------------------------------------- |
| type      | Setting type (1: family dimension; 2: gateway dimension) |

##### Sample code

```java
mTuyaSecurityBaseSdk.newArmedInstance(mHomeId).getGatewayVoicePasswordStateWithHomeId(type, object : ITuyaResultCallback<String?> {
            override fun onSuccess(result: String?) {
                // do something
            }

            override fun onError(errorCode: String, errorMessage: String) {
                // do something
            }
        })
```