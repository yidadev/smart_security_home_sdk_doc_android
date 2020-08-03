### Security news

#### Get the security message SDK

```java
ITuyaSecurityMessageSdk mTuyaSecurityMessageSdk = TuyaOptimusSdk.getManager(ITuyaSecurityMessageSdk.class)
```

##### CenterMessageBean field information

| Field            | Types of | description            |
| ---------------- | -------- | ---------------------- |
| attachPics       | String   | The map's address      |
| deviceIds        | List     | Device ID collection   |
| gmtCreate        | long     | Timestamp              |
| id               | long     | id identification      |
| homeId           | String   | Family ID              |
| msgId            | String   | Message ID             |
| msgContent       | String   | Message content        |
| msgTitle         | String   | Message title          |
| productType      | String   | Category               |
| productId        | String   | Category ID            |
| icon             | String   | Device icon address    |
| readStatus       | int      | Message read status    |
| msgSrcId         | String   | Message resource ID    |
| actionURL        | String   | Device panel routing   |
| msgTypeContent   | String   | Message content        |
| deviceName       | String   | Equipment name         |
| deviceCustomName | String   | Device custom name     |
| favorite         | int      | Collection status      |
| msgCategory      | int      | Message classification |
| attachType       | int      | Message type category  |
| msgType          | int      | Message type           |

##### Condition field information

| Field     | Types of | description          |
| --------- | -------- | -------------------- |
| startTime | Long     | Start query time     |
| endTime   | Long     | End query time       |
| favorite  | Integer  | Whether to collect   |
| deviceIds | List     | Device ID collection |

##### PushCategoryBean field information

| Field     | Types of | description        |
| --------- | -------- | ------------------ |
| sms       | int      | Message Push SMS   |
| voicecall | int      | Message push voice |
| push      | int      | Push message push  |
| email     | int      | Push message       |

##### PushConfigBean field information

| Field      | Types of | description                     |
| ---------- | -------- | ------------------------------- |
| isDefault  | boolean  | Is enough to show by default    |
| bizKey     | String   | Push settings business subclass |
| name       | String   | name                            |
| switchList | List     | Push switch list collection     |

##### PushSwitchBean field information

| Field       | Types of | description                    |
| ----------- | -------- | ------------------------------ |
| sortOrder   | int      | Sort number                    |
| type        | int      | Push setting type              |
| value       | int      | Push switch display            |
| name        | String   | name                           |
| disturbList | List     | Push Do Not Disturb Collection |

##### PushSwitchBean field information

| Field       | Types of | description                    |
| ----------- | -------- | ------------------------------ |
| sortOrder   | int      | Sort number                    |
| type        | int      | Push setting type              |
| value       | int      | Push switch display            |
| name        | String   | name                           |
| disturbList | List     | Push Do Not Disturb Collection |

##### DisturbBean field information

| Field       | Types of | description               |
| ----------- | -------- | ------------------------- |
| gmtModified | long     | Change the time           |
| timeZoneId  | String   | Time zone                 |
| bizId       | String   | Push business categories  |
| startTime   | String   | Do not disturb start time |
| endTime     | String   | Do not disturb end time   |
| gmtCreate   | long     | Creation time             |
| id          | long     | Push Do Not Disturb ID    |

### Get message list

##### Interface Description

```
void getCenterMessages(Integer msgType, int limit, int offset, Condition condition)
```

##### Parameter Description

| parameter | Description                                           |
| --------- | ----------------------------------------------------- |
| msgType   | Message category (1: CAMERA, 2: SECURITY, 3: GENERAL) |
| limit     | Limit the number of                                   |
| offset    | Offset                                                |
| condition | Query filter conditions                               |

##### Sample code

```
  mTuyaSecurityMessageSdk.newMessageInstance(mHomeId).getCenterMessages(msgType, limit, offset, condition, new ITuyaResultCallback<ArrayList<CenterMessageBean>>() {
            @Override
            public void onSuccess(ArrayList<CenterMessageBean> result) {
                // do something
            }

            @Override
            public void onError(String errorCode, String errorMessage) {
                // do something
            }
        });
```

### Delete messages in bulk

##### Interface Description

```
void removeCenterMessages(ArrayList<String> mids, int type)
```

##### Parameter Description

| parameter | Description                                           |
| --------- | ----------------------------------------------------- |
| type      | Message category (1: CAMERA, 2: SECURITY, 3: GENERAL) |
| mids      | Message ID collection                                 |

##### Sample code

```
 mTuyaSecurityMessageSdk.newMessageInstance(mHomeId).removeCenterMessages(mids, type, new ITuyaResultCallback<Boolean>() {
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

### Update message read status

##### Interface Description

```
void updateMessageState(String mid, int type)
```

##### Parameter Description

| parameter | Description                                           |
| --------- | ----------------------------------------------------- |
| mid       | Message ID                                            |
| type      | Message category (1: CAMERA, 2: SECURITY, 3: GENERAL) |

##### Sample code

```
 mTuyaSecurityMessageSdk.newMessageInstance(mHomeId).updateMessageState(mid, type, new ITuyaResultCallback<Boolean>() {
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

### Message bulk collection/unfavorite

##### Interface Description

```
void updateFavoriteMessageState(List<String> mids, Integer favorite)
```

##### Parameter Description

| parameter | Description                                    |
| --------- | ---------------------------------------------- |
| mids      | Message ID collection                          |
| favorite  | Favorite mark (0-cancel favorite, 1- favorite) |

##### Sample code

```
 mTuyaSecurityMessageSdk.newMessageInstance(mHomeId).updateFavoriteMessageState(mids, favorite, new ITuyaResultCallback<Boolean>() {
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

### Get notification setting list information

##### Interface Description

```
void getNotificationConfigList(String bizId, String bizKey)
```

##### Parameter Description

| parameter | Description                                                  |
| --------- | ------------------------------------------------------------ |
| bizId     | Business categories (push, email, sms, voicecall)            |
| bizKey    | Subcategories (alarmAlerts, cameraAlerts, homeAutomationAlerts, bulletins) |

##### Sample code

```
mTuyaSecurityMessageSdk.newMessageInstance(mHomeId).getNotificationConfigList(bizId, bizKey, new ITuyaResultCallback<ArrayList<PushConfigBean>>() {
            @Override
            public void onSuccess(ArrayList<PushConfigBean> result) {
                // do something
            }

            @Override
            public void onError(String errorCode, String errorMessage) {
                // do something
            }
        });
```

### Update notification setting switch information

##### Interface Description

```
void updateNotificationConfig(String bizId, Integer messageType, Integer bizValue)
```

##### Parameter Description

| parameter   | Description                                       |
| ----------- | ------------------------------------------------- |
| bizId       | Business categories (push, email, sms, voicecall) |
| messageType | Message type                                      |
| bizValue    | Subclass pass by value                            |

##### Sample code

```
 mTuyaSecurityMessageSdk.newMessageInstance(mHomeId).updateNotificationConfig(bizId, messageType, bizValue, new ITuyaResultCallback<Boolean>() {
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

### Reset notification settings defaults

##### Interface Description

```
void restNotificationConfigDefault(String bizId, String bizKey)
```

##### Parameter Description

| parameter | Description                                                  |
| --------- | ------------------------------------------------------------ |
| bizId     | Business categories (push, email, sms, voicecall)            |
| bizKey    | Subcategories (alarmAlerts, cameraAlerts, homeAutomationAlerts, bulletins) |

##### Sample code

```
mTuyaSecurityMessageSdk.newMessageInstance(mHomeId).restNotificationConfigDefault(bizId, bizKey, new ITuyaResultCallback<Boolean>() {
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

### Set notification settings category switch

##### Interface Description

```
void updateNotificationCategory(String bizId, Integer bizValue)
```

##### Parameter Description

| parameter | Description                                       |
| --------- | ------------------------------------------------- |
| bizId     | Business categories (push, email, sms, voicecall) |
| bizValue  | Subclass pass by value                            |

##### Sample code

```
mTuyaSecurityMessageSdk.newMessageInstance(mHomeId).updateNotificationCategory(bizId, bizValue, new ITuyaResultCallback<Boolean>() {
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

### Get notification settings category settings

##### Interface Description

```
void getNotificationCategoryList()
```

##### Parameter Description

no

##### Sample code

```
 mTuyaSecurityMessageSdk.newMessageInstance(mHomeId).getNotificationCategoryList(new ITuyaResultCallback<PushCategoryBean>() {
            @Override
            public void onSuccess(PushCategoryBean result) {
                // do something
            }

            @Override
            public void onError(String errorCode, String errorMessage) {
                // do something
            }
        });
```

### Update Do Not Disturb Time

##### Interface Description

```
void updateNotDisturbTime(Long id, String startTime, String endTime, String bizId, ITuyaResultCallback<Boolean> callback)
```

##### Parameter Description

| parameter | Description                                       |
| --------- | ------------------------------------------------- |
| bizId     | Business categories (push, email, sms, voicecall) |
| id        | Configuration ID                                  |
| startTime | Starting time                                     |
| endTime   | End Time                                          |

##### Sample code

```
 mTuyaSecurityMessageSdk.newMessageInstance(mHomeId).updateNotDisturbTime(id, startTime, endTime, bizId, new ITuyaResultCallback<Boolean>() {
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

### Get the DND time configuration

##### Interface Description

```
void getNotDisturbConfigList(String bizId, String bizKey, ITuyaResultCallback<ArrayList<PushConfigBean>> callback)
```

##### Parameter Description

| parameter | Description                                       |
| --------- | ------------------------------------------------- |
| bizId     | Business categories (push, email, sms, voicecall) |
| bizValue  | Subclass pass by value                            |

##### Sample code

```
mTuyaSecurityMessageSdk.newMessageInstance(mHomeId).getNotDisturbConfigList(bizId, bizKey, new ITuyaResultCallback<ArrayList<PushConfigBean>>() {
            @Override
            public void onSuccess(ArrayList<PushConfigBean> result) {
                // do something
            }

            @Override
            public void onError(String errorCode, String errorMessage) {
                // do something
            }
        });
```