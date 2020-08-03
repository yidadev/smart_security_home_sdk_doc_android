## 1 User registration, login

### 1.1 Mobile phone account system

Use TuyaHomeSdk directly, refer to section 1.1 of Tuya's basic SDK [mobile phone account system](<https://tuyainc.github.io/tuyasmart_home_android_sdk_doc/en/resource/User_mobile.html>)

### 1.2 Email account login system

Use TuyaHomeSdk directly, refer to section 1.2 of Tuya's basic SDK [email account system](<https://tuyainc.github.io/tuyasmart_home_android_sdk_doc/en/resource/User_email.html>)

### 1.3 User uid registration and login (already have an account system)

Use TuyaHomeSdk directly, refer to section 1.3 of Tuya Basic SDK [user uid login system](<https://tuyainc.github.io/tuyasmart_home_android_sdk_doc/en/resource/User_uid.html>)

### 1.4 Modify user information

Use TuyaHomeSdk directly, refer to Tuya Basic SDK to [modify user information](<https://tuyainc.github.io/tuyasmart_home_android_sdk_doc/en/resource/User_update.html>) section 1.6

### 1.5 Logout, disable account

Use TuyaHomeSdk directly, refer to Tuya Basic SDK [Logout, disable account](<https://tuyainc.github.io/tuyasmart_home_android_sdk_doc/en/resource/User_logout.html>) Chapter 1.7

### 1.6 User Data Model

Use TuyaHomeSdk directly, refer to Chapter 1.8 of Tuya Basic SDK [User Data Model](<https://tuyainc.github.io/tuyasmart_home_android_sdk_doc/en/resource/User_model.html>)

## 2 User Service

### 2.1 User service synchronization

After successful registration or login through the **1.1.x** interface, the user's service status needs to be verified. Call **getServiceInfoWithHandler** immediately to check the status of service binding;

#### Two situations related to user service:

\1. Use security SaaS default binding: Security SaaS configures a service provider for customers by default in the background, and all user information will be collected on this SaaS platform without distinction;

\2. No security SaaS default binding: You need to log in to the security SaaS backend to create an activation code, and verify whether it is bound through the data model returned by **getServiceInfoWithHandler** . If it is not bound, then use **bindServiceWithCode** ; in this way, you can use the activation code To distinguish the channels of users.

#### Interface Description

Obtain and synchronize user service information

Obtain the service provider ID, channel ID, and activation code bound to the user, and determine whether the customer is bound to the activation code

If you don’t need the activation code, you can directly contact Tuya Development to enable the default activation code to ensure that the value obtained every time is bound.

```java
void getServiceInfoWithHandler(ITuyaResultCallback<ServiceDealerBean> callback);
```

#### Parameter Description:

| **parameter** | **Description**  |
| ------------- | ---------------- |
| callback      | Success callback |

Return value description:

| return value | Types of | Description                                                  |
| ------------ | -------- | ------------------------------------------------------------ |
| isBind       | boolean  | Whether to bind activation code                              |
| code         | String   | Activation code                                              |
| channelId    | String   | Channel ID corresponding to the bound activation code        |
| dealerId     | String   | Service provider ID corresponding to the bound activation code |

#### Code example:

```java
ITuyaSecurityServiceSdk mTuyaSecurityService = TuyaOptimusSdk.getManager(ITuyaSecurityServiceSdk.class);
final ITuyaSecurityService iTuyaSecurityService = mTuyaSecurityService.newServiceInstance();
            iTuyaSecurityService.getServiceInfoWithHandler(new ITuyaResultCallback<ServiceDealerBean>() {
                @Override
                public void onSuccess(ServiceDealerBean result) {
                    
                }

                @Override
                public void onError(String errorCode, String errorMessage) {
                    
                }
            });
```

### 2.2 Bind activation code

#### Interface Description:

Customers can distinguish users by channel based on the activation code created by themselves

```java
void bindServiceWithCode(String code, ITuyaResultCallback<Boolean> callback);
```

#### Parameter Description:

| **parameter** | Description     |
| ------------- | --------------- |
| code          | Activation code |
| callback      | Callback        |

#### Code example:

```java
ITuyaSecurityServiceSdk mTuyaSecurityService = TuyaOptimusSdk.getManager(ITuyaSecurityServiceSdk.class);
final ITuyaSecurityService iTuyaSecurityService = mTuyaSecurityService.newServiceInstance();
iTuyaSecurityService.bindServiceWithCode("your code", new ITuyaResultCallback<Boolean>() {
                @Override
                public void onSuccess(Boolean result) {
                    
                }

                @Override
                public void onError(String errorCode, String errorMessage) {

                }
            });
```