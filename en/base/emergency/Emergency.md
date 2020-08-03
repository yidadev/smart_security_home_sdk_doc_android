### emergency contact

#### Obtain the arm and disarm SDK

```java
ITuyaSecurityBaseSdk mTuyaSecurityBaseSdk = TuyaOptimusSdk.getManager(ITuyaSecurityBaseSdk.class)
```

##### ContactBean field information

| Field     | Types of | description         |
| --------- | -------- | ------------------- |
| areaCode  | String   | Area code           |
| phone     | String   | mobile phone number |
| homeId    | String   | Family ID           |
| firstName | String   | name                |
| lastName  | String   | name                |
| id        | Integer  | Contact ID          |
| gmtCreate | String   | Creation time       |
| sequence  | Integer  | Contact sort        |

### Add emergency contact

##### Interface Description

```java
void addNewConnectWithHomeId(String phone, String firstName, String lastName, String areaCode, Integer order, ITuyaResultCallback<ContactBean> callback)
```

##### Parameter Description

| parameter | Description         |
| --------- | ------------------- |
| phone     | mobile phone number |
| firstName | name                |
| lastName  | name                |
| areaCode  | Area code           |
| order     | Sort level          |

##### Sample code

```java
mTuyaSecurityBaseSdk.newEmergencyInstance(mHomeId).addNewConnectWithHomeId(phone, firstName, lastName, areaCode, order, new ITuyaResultCallback<ContactBean>() {
        @Override
        public void onSuccess(ContactBean result) {
            // do something
        }

        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
    });
```

### Edit emergency contacts (edit, sort

##### Interface Description

```java
void editConnectWithHomeId(ArrayList<ContactBean> contactBeans, ITuyaResultCallback<Boolean> callback)
```

##### Parameter Description

| parameter    | Description        |
| ------------ | ------------------ |
| contactBeans | Contact array list |

##### Sample code

```java
mTuyaSecurityBaseSdk.newEmergencyInstance(mHomeId).editConnectWithHomeId(contactBeans, new ITuyaResultCallback<Boolean>() {
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

### Delete emergency contact

##### Interface Description

```java
void deleteConnectWithHomeId(ArrayList<Integer> ids, ITuyaResultCallback<Boolean> callback)
```

##### Parameter Description

| parameter | Description           |
| --------- | --------------------- |
| ids       | Contact ID array list |

##### Sample code

```java
mTuyaSecurityBaseSdk.newEmergencyInstance(mHomeId).deleteConnectWithHomeId(ids, new ITuyaResultCallback<Boolean>() {
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

### Get emergency contact list

##### Interface Description

```java
void getLocationEmergencyConnectWithHomeId(ITuyaResultCallback<ArrayList<ContactBean>> callback)
```

##### Parameter Description

no

##### Sample code

```java
mTuyaSecurityBaseSdk.newEmergencyInstance(mHomeId).getLocationEmergencyConnectWithHomeId(new ITuyaResultCallback<ArrayList<ContactBean>>() {
            @Override
            public void onSuccess(ArrayList<ContactBean> result) {
                // do something
            }

            @Override
            public void onError(String errorCode, String errorMessage) {
                // do something
            }
        });
```