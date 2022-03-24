# Use Mobile Phone for Login
Wiser Smart provides the mobile phone verification code login system.

> **Note**: For the privacy and security of user information, we have optimized the mobile phone number registration mechanism. If you want to use the mobile phone number registration service, you can contact the relevant docking business.

## Phone password registration

Mobile phone password registration, including obtaining a verification code interface and a registration interface.

**Description**

Get a phone verification code.

>**Important**: 
>- This interface has differences in SDKs prior to version 3.25.0, if you are using an older version of the SDK, please refer to Migrating to 3.25.0.
>- Please pay attention to the [white list](#WhiteList) API.

```java
WiserHomeSdk.getUserInstance().sendVerifyCodeWithUserName(String userName, String region, String countryCode, int type, IResultCallback callback);
```

**Parameters**

| Parameters | Description |
| ---- | ---- |
| userName | Mobile phone number |
| region | Field, the default to fill in: "" |
| countryCode | country code, for example: 86 |
| type | 1: mobile phone verification code register |
| callback | callback |

**Description**

Phone password registration

```java
WiserHomeSdk.getUserInstance().registerAccountWithPhone(final String phoneCode, final String phoneNumber, final String passwd, final String code, final IRegisterCallback callback);
```

**Parameters**

| Parameters | Description |
| ---- | ---- |
| phoneCode | Mobile Area Code: Such as "86" |
| phoneNumber | phone number |
| passwd | password |
| code | Verification Code |
| callback | callback |

**Example**

```java
// Get phone verification code
WiserHomeSdk.getUserInstance().sendVerifyCodeWithUserName("13666666666", "", "86", 1, new IResultCallback() {
			@Override
			public void onError(String code, String error) {
				Toast.makeText(mContext, "code: " + code + "error:" + error, Toast.LENGTH_SHORT).show();
			}

			@Override
			public void onSuccess() {
				Toast.makeText(mContext, "Success in obtaining verification code", Toast.LENGTH_SHORT).show();
			}
		});
// Register mobile password account
WiserHomeSdk.getUserInstance().registerAccountWithPhone("86", "13666666666", "123456", "124332", new IRegisterCallback () {
    @Override
    public void onSuccess (User user) {
        Toast.makeText (mContext, "Registration succeeded", Toast.LENGTH_SHORT) .show ();
    }
    @Override
    public void onError (String code, String error) {
        Toast.makeText (mContext, "code:" + code + "error:" + error, Toast.LENGTH_SHORT) .show ();
    }
});
```

## Phone password login

**Description**

Sign in with your mobile number and password.

```java
WiserHomeSdk.getUserInstance().loginWithPhonePassword(String phoneCode, String phone, String passwd, final ILoginCallback callback);
```

**Parameters**

| Parameters | Description |
| ---- | ---- |
| phoneCode | Mobile Area Code: Such as "86" |
| phone | mobile number |
| passwd | Login password |
callback | Login callback interface |

**Example**

```java
// Mobile password login
WiserHomeSdk.getUserInstance().loginWithPhonePassword ("86", "13666666666", "123456", new ILoginCallback () {
    @Override
    public void onSuccess (User user) {
        Toast.makeText (mContext, "Successfully logged in, username:" + WiserHomeSdk.getUserInstance (). GetUser (). GetUsername (), Toast.LENGTH_SHORT) .show ();
    }

    @Override
    public void onError (String code, String error) {
        Toast.makeText (mContext, "code:" + code + "error:" + error, Toast.LENGTH_SHORT) .show ();
    }
});
```

Wiser Smart provides a mobile phone verification code login system.

## Mobile verification code login

The verification code login function of the mobile phone needs to call the verification code sending interface first to send the verification code. Then call the mobile phone verification code verification interface. Fill the received verification code into the corresponding parameters.

**Description**

Get phone verification code.

>**Important**: 
>- This interface has differences in SDKs prior to version 3.25.0, if you are using an older version of the SDK, please refer to Migrating to 3.25.0.
>- Please pay attention to the [white list](#WhiteList) API.

```java
WiserHomeSdk.getUserInstance().sendVerifyCodeWithUserName(String userName, String region, String countryCode, int type, IResultCallback callback);
```

**Parameters**

| Parameters | Description |
| ---- | ---- |
| userName | Mobile phone number |
| region | Field, the default to fill in: "" |
| countryCode | country code, for example: 86 |
| type | 2: Verification code login |
| callback | callback |


**Description**

Phone verification code login


```java
WiserHomeSdk.getUserInstance().loginWithPhone(String phoneCode, String phone, String code, final ILoginCallback callback)
```

**Parameters**

| Parameters | Description |
| ---- | ---- |
| phoneCode | Mobile Area Code: Such as "86" |
| phone | phone number |
| code | Verification Code |
| callback | Login callback interface |

**Example**

```java
// Get phone verification code
WiserHomeSdk.getUserInstance().sendVerifyCodeWithUserName("13666666666", "", "86", 2, new IResultCallback() {
			@Override
			public void onError(String code, String error) {
				Toast.makeText(mContext, "code: " + code + "error:" + error, Toast.LENGTH_SHORT).show();
			}

			@Override
			public void onSuccess() {
				Toast.makeText(mContext, "Success in obtaining verification code", Toast.LENGTH_SHORT).show();
			}
		});
// Mobile verification code login
WiserHomeSdk.getUserInstance().loginWithPhone("86", "13355555555", "123456", new ILoginCallback () {
    @Override
    public void onSuccess (User user) {
        Toast.makeText (mContext, "Successfully logged in, username:" + WiserHomeSdk.getUserInstance (). GetUser (). GetUsername (), Toast.LENGTH_SHORT) .show ();
    }
    @Override
    public void onError (String code, String error) {
        Toast.makeText (mContext, error, Toast.LENGTH_SHORT) .show ();
    }
});
```

## Phone reset password

Phone reset password function, including two interfaces: send verification code interface and reset password interface

**Description**

Get phone verification code.

>**Important**: 
>- This interface has differences in SDKs prior to version 3.25.0, if you are using an older version of the SDK, please refer to Migrating to 3.25.0.
>- Please pay attention to the [white list](#WhiteList) API.

```java
WiserHomeSdk.getUserInstance().sendVerifyCodeWithUserName(String userName, String region, String countryCode, int type, IResultCallback callback);
```

**Parameters**

| Parameters | Description |
| ---- | ---- |
| userName | Mobile phone number |
| region | Field, the default to fill in: "" |
| countryCode | country code, for example: 86 |
| type | 3: mobile phone password reset. |
| callback | callback |

**Description**

reset Password

```java
WiserHomeSdk.getUserInstance().resetPhonePassword (final String phoneCode, final String phone, final String code, final String newPasswd, final IResetPasswordCallback callback);
```

**Parameters**

| Parameters | Description |
| ---- | ---- |
| phoneCode | Mobile Area Code: Such as "86" |
| phone | mobile number |
| code | Verification Code |
| newPasswd | new password |
| callback |


>**Note**:
>- After the password is reset, if multiple devices log in to the same account at the same time, other devices will trigger a callback for session failure. Please implement the actions after the callback, such as jumping to the login page.**
>- For more information, please refer to the chapter "Handling of Expired Session".

## Verification code verification

**Description**

Verification verification code, used for verification verification during registration, login, and password reset

```java
WiserHomeSdk.getUserInstance().checkCodeWithUserName(String userName, String region, String countryCode, String code, int type, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| ---- | ---- |
| userName | User name |
| region | region，Fill in the default: "" |
| countryCode | Country code |
| code | Verification code |
| type | Type: <br/>1: For verification code verification during registration <br/>2: Use the verification code to log in <br/>3: Used when resetting the password |

<a id="WhiteList"></a>

## User get whitelist list

**Description**

The user gets the whitelist, and only in the whitelisted area can the mobile phone number verification code be sent to register an account

```java
WiserHomeSdk.getUserInstance().getWhiteListWhoCanSendMobileCodeSuccess(IWhiteListCallback callback);
```

**Parameters**

| Parameters | Description |
| ---- | ---- |
| callback | callback interface |

**Example**

```java
WiserHomeSdk.getUserInstance().getWhiteListWhoCanSendMobileCodeSuccess(new IWhiteListCallback() {
		@Override
		public void onSuccess(WhiteList whiteList) {
			Toast.makeText(mContext, "Whitelist obtained successfully:" + whiteList.getCountryCodes(), Toast.LENGTH_SHORT).show();
		}

		@Override
		public void onError(String code, String error) {
			Toast.makeText(mContext, "code: " + code + "error:" + error, Toast.LENGTH_SHORT).show();
		}
	});
```