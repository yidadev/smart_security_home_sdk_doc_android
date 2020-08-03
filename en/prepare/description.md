- ### Introduction:

  Demo App mainly introduces the SDK development process and some simple business logic. Before developing the App, it is recommended to complete the Demo App operation according to this document.

  In **preparation for** acquisition section inside `iOS`of `AppKey`, `AppSecret`, safety picture. Make sure that when the SDK integration `BundleId`, , `AppKey`, `AppSecret`safety picture is consistent with the information on the platform, a mismatch will cause any SDK can not be used.

  The security-related business entry in the security demo is in SecurityFragment, and the security-related business is in the class beginning with Security.

  ### Functional Overview:

  Demo App mainly includes

  - User module: registration and login of account (mobile phone or email)
  - Family management and equipment management modules: including the creation of a family and the switching of the current family. The display of the device list in the family, the control of the device function points. Device renaming and device removal.
  - Device network configuration module: including EZ mode, AP mode, wired gateway network configuration, and gateway sub-device network configuration
  - Scene module: scene creation and execution
  - User information module: user information
  - Security module: security arming and disarming, security setting, geofencing

  ### common problem:

  **API interface request prompts signature error**

  ```objc
  {
    "success" : false,
    "errorCode" : "SING_VALIDATE_FALED",
    "status" : "error",
    "errorMsg" : "Permission Verification Failed",
    "t" : 1583208740059
  }
  ```

  - Confirm whether the BundleId, AppKey, AppSecret, and security image are consistent with the information on the IoT platform. If any one of them does not match, the verification will fail. For details, please check in accordance with the **preparatory work** chapter.