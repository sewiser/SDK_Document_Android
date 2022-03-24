# Login with QR Code Authorization
## Flow description

> **Note**: Before using the app of central control devices shown in the following process, your account must be granted whitelist privilege. Otherwise, the response will receive an error.
>
> For example, if you use the **Wiser Smart** app to scan the QR code of your SDK created by the IoT platform, an error will be reported and the session will be invalid.

The QR code authorization login function is suitable for APP scanning code to authorize another device to log in to the same account. The device can be a central control device, TV, Pad, etc. The complete authorization process is as follows:

![image.png](https://airtake-public-data-1254153901.cos.ap-shanghai.myqcloud.com/goat/20201228/a5bb7a453bb845dc99d8595d473fcb6a.png)

<!--
```
sequenceDiagram
participant APP
participant Device with QR code
participant Serve
A device with QR code->>Serve: Get token ①
Serve->>Device with QR code: Return token
A device with QR code->>Device with QR code: Generate QR code ②
loop Auth status
	A device with QR code->>Serve: Get login status ③
	Serve->>Device with QR code: Return to login status
end
APP->>Device with QR code: Scan QR code: get token ④
A device with QR code->>APP: Get token
APP->>Serve: Authorization: use token ⑤
Serve->>APP: Authorization success/failure

alt Auth success
Device with QR code->>Device with QR code: Go to the homepage
else
end
```
-->

Explanation of the general steps marked in the preceding figure:

### Get token

The device requests the API to obtain the token used in the authorization process, the API is `getQRCodeToken`.

### Generate QR code

1. Use the obtained token to generate a QR code in a specific format:

	* The format is: `wiser.m.rt--qrLogin?token=xxxxxxx`

	* Example: `wiser.m.rt--qrLogin?token=AZc72de000-ec00-4000-9e51-b610fc300000`

	* Generated QR code:

		![image](./img/2804daa7-bb75-409c-902e-44b511763825.png)

2. Display the QR code generated from the above string on the screen of the device.

### Get login status

Obtain whether the authorization is successful from the server. If the authorization is successful, the user information will be returned, navigate to the application home page, and enter the subsequent operation.

The API is: `QRCodeLogin`.

### Scan QR code

The app scans the QR code on the device, resolves the token in the QR code, and performs the authorization operation.

### Authorization

Send the parsed QR code to the Server to complete the authorization action.

The authorization method is `QRcodeAuth`.

## APIs

### Get token

**Description**

```java
void getQRCodeToken(String countryCode, IGetQRCodeTokenCallback callback);
```

**Parameters**

| **Parameters** | **Description** |
| ---- | ---- |
| countryCode | Country code, for example: 86 |
| callback | callback |

**Java sample**

```java
WiserHomeSdk.getUserInstance().getQRCodeToken("86", new IGetQRCodeTokenCallback() {
	@Override
	public void onSuccess(String token) {

	}

	@Override
	public void onError(String code, String error) {

	}
});
```

### Get login status

**Description**

```Java
void QRCodeLogin(String countryCode, String token, ILoginCallback callback);
```

**Parameters**

| **Parameters** | **Description** |
| ---- | ---- |
| countryCode | country code, for example: 86 |
| token | token |
| callback | callback |

**Java sample**

```java
WiserHomeSdk.getUserInstance().QRCodeLogin("86", "xxxx", new ILoginCallback() {
	@Override
	public void onSuccess(User user) {
		if (user != null && !TextUtils.isEmpty(user.getSid())){
			WiserHomeSdk.getUserInstance().loginSuccess(user);
			//get homeId
			Object homeId = user.getExtras().get("homeId");

			gotoHomePage();
		}
	}

	@Override
	public void onError(String code, String error) {

	}
});
```

### Authorization

```java
void QRcodeAuth(String countryCode, long homeId, String token, IBooleanCallback callback);
```

**Parameters**

| **Parameters** | **Description** |
| ---- | ---- |
| countryCode | country code, for example: 86 |
| homeId | home id. Please refer to the Home Management chapters |
| token | token |
| callback | callback |

**Java sample**

```java
WiserHomeSdk.getUserInstance().QRcodeAuth("86", mHomeId, getActivityToken(), new IBooleanCallback() {
	@Override
	public void onSuccess() {

	}

	@Override
	public void onError(String code, String error) {

	}
});
```