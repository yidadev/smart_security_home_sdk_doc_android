### Security scene

#### Get the security scene SDK

```java
ITuyaSecuritySceneSdk mTuyaSecuritySceneSdk = TuyaOptimusSdk.getManager(ITuyaSecuritySceneSdk.class)
```

#### Create a security scene

###### Interface Description

```java
void createScene(String name, boolean stickyOnTop, String background, String displayColor, String coverIcon, List<SceneCondition> conditions, List<SceneTask> tasks, int matchType, final ITuyaResultCallback<SceneBean> callback);
```

###### Parameter Description

| parameter    | Description                                                  |
| ------------ | ------------------------------------------------------------ |
| name         | Scene name                                                   |
| stickyOnTop  | Whether it appears at the head of the room page              |
| background   | Scene home background url                                    |
| displayColor | Scene icon color                                             |
| coverIcon    | Scene foreground icon                                        |
| conditions   | Scene condition list                                         |
| tasks        | Scene action list                                            |
| matchType    | The type that satisfies the condition, satisfies any condition as 1, and satisfies all conditions as 2 |
| callback     | Get result callback                                          |

###### Example description

```java
mTuyaSecuritySceneSdk.newSceneInstance(家庭id).createScene("scene name", "appear in home page",
                "background image url", "icon color", "icon url", "condition list", "action list", "run condition",
                new ITuyaResultCallback<SceneBean>() {
                    @Override
                    public void onSuccess(SceneBean sceneBean) {

                    }

                    @Override
                    public void onError(String s, String s1) {

                    }
                });
```

#### Get a list of scenes

###### Interface Description

```java
void getSceneList(ITuyaResultCallback<List<SceneBean>> callback);
```

###### Parameter Description

| parameter | Description         |
| --------- | ------------------- |
| callback  | Get result callback |

###### Example description

```java
mTuyaSecuritySceneSdk.newSceneInstance(家庭id).getSceneList(new ITuyaResultCallback<List<SceneBean>>() {
            @Override
            public void onSuccess(List<SceneBean> sceneBeans) {

            }

            @Override
            public void onError(String s, String s1) {

            }
        });
```

#### Delete scene

###### Interface Description

```java
void deleteScene(String scenceId, ITuyaResultCallback<Boolean> callback);
```

###### Parameter Description

| parameter | Description         |
| --------- | ------------------- |
| scenceId  | Scene id            |
| callback  | Get result callback |

###### Example description

```java
mTuyaSecuritySceneSdk.newSceneInstance(家庭id).deleteScene("scene id", new ITuyaResultCallback<Boolean>() {
            @Override
            public void onSuccess(Boolean result) {

            }

            @Override
            public void onError(String errorCode, String errorMessage) {

            }
        });
```

#### Modify the scene

###### Interface Description

```java
void modifyScene(SceneBean sceneBean, ITuyaResultCallback<SceneBean> callback);
```

###### Parameter Description

| parameter | Description               |
| --------- | ------------------------- |
| sceneBean | Modified scene parameters |
| callback  | Get result callback       |

###### Example description

```java
mTuyaSecuritySceneSdk.newSceneInstance(家庭id).modifyScene("", new ITuyaResultCallback<SceneBean>() {
            @Override
            public void onSuccess(SceneBean sceneBean) {

            }

            @Override
            public void onError(String errorCode, String errorMessage) {

            }
        });
```