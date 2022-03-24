# Email Account
Wiser Smart provides a login system for email registration.

## Account registration

There are two interfaces for email registration. First, get the verification code, and then use the verification code and password to register.

### Get verification code

>**Important**: 
>
>- This interface has differences in SDKs prior to version 3.26.5, if you are using an older version of the SDK, please refer to [Migrating to 3.26.5]().

```java
WiserHomeSdk.getUserInstance().sendVerifyCodeWithUserName(String userName, String region, String countryCode, int type, IResultCallback callback);
```

**Parameters**

| Parameter   | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| userName    | email address                                                |
| region      | Region, fill in by default: "" is fine                       |
| countryCode | Country code: such as "86"                                   |
| type        | Type of verification code sent: 1: Register verification code |
| callback    | callback                                                     |

### Registration

```java
void registerAccountWithEmail (final String countryCode, final String email, final String passwd, final String code, final IRegisterCallback callback);
```

**Parameters**

| Parameters | Description |
| ---- | ---- |
| countryCode | country code, for example: 86 |
| email | email |
| passwd | password |
| code | Verification Code |
| callback | callback |

**Example**

```java
// Sign up for email verification code
WiserHomeSdk.getUserInstance().sendVerifyCodeWithUserName("123456@123.com", "", "86", 1, new IResultCallback() {
            @Override
            public void onError(String code, String error) {
                Toast.makeText(mContext, "code: " + code + "error:" + error, Toast.LENGTH_SHORT).show();
            }

            @Override
            public void onSuccess() {
                Toast.makeText(mContext, "Get the verification code successfully", Toast.LENGTH_SHORT).show();
            }
        });

// Email password registration
WiserHomeSdk.getUserInstance(). registerAccountWithEmail ("86", "123456@123.com", "123456", "5723", new IRegisterCallback () {
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

> **Note**:
>
> Once the account is registered in one country, data cannot currently be migrated to other countries.

## Login with Email

### User email password login

```java
WiserHomeSdk.getUserInstance().loginWithEmail(String countryCode, String email, String passwd, final ILoginCallback callback);
```

**Parameters**

|Parameters | Description |
| ---- | ---- |
| countryCode | country code, for example: 86 |
| email | email |
| passwd | Login password |
| callback | callback |

**Example**

```java
// mail password login
WiserHomeSdk.getUserInstance().loginWithEmail("86", "123456@123.com", "123123", new ILoginCallback () {
    @Override
    public void onSuccess (User user) {
        Toast.makeText (mContext, "Login succeeded, username:"). Show ();
    }

    @Override
    public void onError (String code, String error) {
        Toast.makeText (mContext, "code:" + code + "error:" + error, Toast.LENGTH_SHORT) .show ();
    }
});
```

## User email reset password

The user mailbox reset password function is divided into two interfaces, a verification code interface, and a password reset interface.

### Get verification code

>**Important**: 
>
>- This interface has differences in SDKs prior to version 3.26.5, if you are using an older version of the SDK, please refer to [Migrating to 3.26.5]().

```java
WiserHomeSdk.getUserInstance().sendVerifyCodeWithUserName(String userName, String region, String countryCode, int type, IResultCallback callback);
```

**Parameters**

| Parameter   | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| userName    | email address                                                |
| region      | Region, fill in by default: "" is fine                       |
| countryCode | Country code: such as "86"                                   |
| type        | Type of verification code sent:  3: Reset password verification code |
| callback    | callback                                                     |

### Email reset password

```java
WiserHomeSdk.getUserInstance().resetEmailPassword (String countryCode, final String email, final String emailCode, final String passwd, final IResetPasswordCallback callback);
```

**Parameters**

| Parameters | Description |
| ---- | ---- |
| countryCode | country code, for example: 86 |
| email | email |
| emailCode | verification code |
| passwd | New password |
| callback | callback |

**Example**

```java
// Get email verification code
WiserHomeSdk.getUserInstance().sendVerifyCodeWithUserName("123456@123.com", "", "86", 3, new IResultCallback() {
            @Override
            public void onError(String code, String error) {
                Toast.makeText(mContext, "code: " + code + "error:" + error, Toast.LENGTH_SHORT).show();
            }

            @Override
            public void onSuccess() {
                Toast.makeText(mContext, "Get the verification code successfully", Toast.LENGTH_SHORT).show();
            }
        });
//reset Password
WiserHomeSdk.getUserInstance().resetEmailPassword("86", "123456@123.com", "123123", "a12345", new IResetPasswordCallback () {
    @Override
    public void onSuccess () {
        Toast.makeText (mContext, "Successfully retrieved password", Toast.LENGTH_SHORT) .show ();
    }
    @Override
    public void onError (String code, String error) {
        Toast.makeText (mContext, "code:" + code + "error:" + error, Toast.LENGTH_SHORT) .show ();
    }
});
```

>**Note**:
>- After the password is reset, if multiple devices log in to the same account at the same time, other devices will trigger a callback for session failure. Please implement the actions after the callback, such as jumping to the login page.
>- For more information, please refer to the chapter "Handling of Expired Session".