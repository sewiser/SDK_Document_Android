# Demo App
The demo app mainly demonstrates the SDK development process. Before developing the app, it is recommended to complete the operation of the Demo app according to this document.

## Overview

After completing the [Preparation for Integration](./3_Integrated.md) section, you will get the AppKey, AppSecret, and security picture information used by the SDK. When integrating the SDK, please confirm that the AppKey, AppSecret, and security pictures are consistent with the information on the platform. Any mismatch will cause the SDK to be unusable.



Demo app includes:

- User module: Account (mobile phone or email) registration and login
- Home management and device management module: including home creation and current home switching. Display of device list and control of device function point in the home. Device rename and device removal.
- Device activator module: including smartConfig mode, AP mode, wired gateway distribution network, gateway sub-device activator, Bluetooth low energy, and dual-mode.

	<img src="https://airtake-public-data-1254153901.cos.ap-shanghai.myqcloud.com/goat/20210326/71ec28807c2d45e2b9d5edf364262b06.jpeg" style="zoom: 25%;" />

## Run the demo

1. Replace the `applicationId` in the `build.gradle` file in the app directory with the package name of your application.

	![image-20191101112723293](./img/e4a39c6a-35f2-4a66-a82d-c5aace2889f4.png)

2. Name your security picture: "t_s.bmp" and put it in the "src"-"main"-"assets" folder under the app directory.

	<img src="./img/8f8ca63c-7a41-4d7d-8301-6f4843dbf614.png" alt="image-20191101112851418" style="zoom:40%;" />

3. Fill your AppKey and AppSecret into the corresponding `<meta-data>` tags in `AndroidManifest.xml`.

	![image-20191101113051694](./img/28872d1c-4a6b-44b7-9b3b-2c70e44b20ad.png)

4. Then click run to run your demo.

## Troubleshooting

**API interface request prompt signature error**

```json
{
  "success": false,
  "errorCode" : "SING_VALIDATE_FALED",
  "status" : "error",
  "errorMsg" : "Permission Verification Failed",
  "t" : 1583208740059
}
```

* Please check whether your AppKey, AppSecret, and Security Picture are configured correctly and are consistent with those obtained in the  [Preparation for Integration](./3_Integrated.md) section.
* Please check whether the security picture in the correct directory and the file name is`t_s.bmp`.