# Use Mobile Phone for Login

> [!DANGER]
>
> For the privacy and security of user information, we have optimized the mobile phone number registration mechanism. If you want to use the mobile phone number registration service, you can contact the relevant docking business

Wiser Smart provides the mobile phone verification code login system.

### Phone Password Registration
Mobile phone password registration, including obtaining a verification code interface and a registration interface

**Declaration**

Get phone verification code

```java
WiserHomeSdk.getUserInstance().getValidateCode(String phoneCode, String phoneNumber, final IValidateCallback callback);
```

**Parameters**

| Parameters | Description |
| ----------- | ----------------- |
| phoneCode | Mobile Area Code: Such as "86" |
| phoneNumber | phone number |
| callback | callback |

**Declaration**

Phone password registration

```java
WiserHomeSdk.getUserInstance().registerAccountWithPhone(final String phoneCode, final String phoneNumber, final String passwd, final String code, final IRegisterCallback callback);
```

**Parameters**

| Parameters | Description |
| ----------- | ----------------- |
| phoneCode | Mobile Area Code: Such as "86" |
| phoneNumber | phone number |
| passwd | password |
| code | Verification Code |
| callback | callback |

**Example**

```java
// Get phone verification code
WiserHomeSdk.getUserInstance().getValidateCode("86", "13666666666", new IValidateCallback () {
    @Override
    public void onSuccess () {
        Toast.makeText (mContext, "Success in obtaining verification code", Toast.LENGTH_SHORT) .show ();
    }

    @Override
    public void onError (String code, String error) {
        Toast.makeText (mContext, "code:" + code + "error:" + error, Toast.LENGTH_SHORT) .show ();
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
### Phone Password Login
**Declaration**

Sign in with your mobile number and password.

```java
WiserHomeSdk.getUserInstance().loginWithPhonePassword(String phoneCode, String phone, String passwd, final ILoginCallback callback);
```

**Parameters**

| Parameters | Description |
| ----------- | ----------------- |
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

### Mobile Verification Code Login

The verification code login function of the mobile phone needs to call the verification code sending interface first to send the verification code. Then call the mobile phone verification code verification interface. Fill the received verification code into the corresponding parameters.

**Declaration**

Get phone verification code

```java
WiserHomeSdk.getUserInstance().getValidateCode(String phoneCode, String phoneNumber, final IValidateCallback callback);
```

**Parameters**

| Parameters  | Description                    |
| ----------- | ------------------------------ |
| phoneCode   | Mobile Area Code: Such as "86" |
| phoneNumber | mobile number                  |
| callback    | callback                       |

**Declaration** 

Phone verification code login


```java
WiserHomeSdk.getUserInstance().loginWithPhone(String phoneCode, String phone, String code, final ILoginCallback callback)
```

**Parameters**

| Parameters | Description                    |
| ---------- | ------------------------------ |
| phoneCode  | Mobile Area Code: Such as "86" |
| phone      | phone number                   |
| code       | Verification Code              |
| callback   | Login callback interface       |

**Example**

```java
// Get phone verification code
WiserHomeSdk.getUserInstance().getValidateCode("86", "13666666666", new IValidateCallback () {
    @Override
    public void onSuccess () {
        Toast.makeText (mContext, "Success in obtaining verification code", Toast.LENGTH_SHORT) .show ();
    }

    @Override
    public void onError (String code, String error) {
        Toast.makeText (mContext, "code:" + code + "error:" + error, Toast.LENGTH_SHORT) .show ();
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

### Phone Reset Password

Phone reset password function, including two interfaces: send verification code interface and reset password interface

**Declaration**

Get phone verification code

```java
WiserHomeSdk.getUserInstance().getValidateCode (String phoneCode, String phoneNumber, final IValidateCallback callback);
```

**Parameters**

| Parameters | Description |
| ----------- | ----------------- |
|phoneCode | Mobile Area Code: Such as "86" |
| phoneNumber | mobile number |

**Declaration**

reset Password

```java
WiserHomeSdk.getUserInstance().resetPhonePassword (final String phoneCode, final String phone, final String code, final String newPasswd, final IResetPasswordCallback callback);
```

**Parameters**

| Parameters | Description |
| ----------- | ----------------- |
| phoneCode | Mobile Area Code: Such as "86" |
| phone | mobile number |
| code | Verification Code |
| newPasswd | new password |
| callback |

>[!TIP]
>
>After the password is reset, if multiple devices log in to the same account at the same time, other devices will trigger a callback for session failure. Please implement the actions after the callback, such as jumping to the login page.
>
>For more information, please refer to the chapter "Handling of Expired Session"

### Verification code verification

**Declaration**

Verification verification code, used for verification verification during registration, login, and password reset

```java
WiserHomeSdk.getUserInstance().checkCodeWithUserName(String userName, String region, String countryCode, String code, int type, IResultCallback callback)
```

**Parameters**

| Parameters  | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| userName    | User name                                                    |
| region      | region，Fill in the default: ""                              |
| countryCode | Country code                                                 |
| code        | Verification code                                            |
| type        | Type: <br/>1: For verification code verification during registration <br/>2: Use the verification code to log in <br/>3: Used when resetting the password |
