# Email Account
Wiser Smart provides a login system for email passwords.
## Email Registration
There are two interfaces for email registration. First, get the verification code, and then use the verification code and password to register.

**Declaration**

Email registration to get verification code

```java
void getRegisterEmailValidateCode (String countryCode, String email, IResultCallback callback);
```

**Parameters**

| Parameters | Description |
| ----------- | ----------------- |
| countryCode | country code, for example: 86 |
| email | email |
| callback | callback |

**Declaration**

Email registration to get verification code

```java
void registerAccountWithEmail (final String countryCode, final String email, final String passwd, final String code, final IRegisterCallback callback);

```

**Parameters**

| Parameters | Description |
| ----------- | ----------------- |
| countryCode | country code, for example: 86 |
| email | email |
| passwd | password |
| code | Verification Code |
| callback | callback |

**Example**

```java
// Sign up for email verification code
WiserHomeSdk.getUserInstance().getRegisterEmailValidateCode ("86", "123456@123.com", new IResultCallback () {
    @Override
    public void onError (String code, String error) {
    }

    @Override
    public void onSuccess () {
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
> Note:
>
> Once the account is registered in one country, data cannot currently be migrated to other countries.

## Login with Email 
**Declaration**

User email password login

```java
WiserHomeSdk.getUserInstance().loginWithEmail(String countryCode, String email, String passwd, final ILoginCallback callback);
```
**Parameters**

|Parameters | Description |
| ----------- | ----------------- |
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
## User Email Reset Password
The user mailbox reset password function is divided into two interfaces, a verification code interface and a password reset interface.

**Declaration**

Email recovery password, get verification code

```java
WiserHomeSdk.getUserInstance().getEmailValidateCode (String countryCode, final String email, final IValidateCallback callback);
```
**Parameters**

|Parameters | Description |
| ----------- | ----------------- |
|countryCode | country code, for example: 86 |
| email | email |
| callback | callback |

**Declaration**

Email reset password

```java
WiserHomeSdk.getUserInstance().resetEmailPassword (String countryCode, final String email, final String emailCode, final String passwd, final IResetPasswordCallback callback);
```

**Parameters**

| Parameters | Description |
| ----------- | ----------------- |
| countryCode | country code, for example: 86 |
| email | email |
| emailCode | verification code |
| passwd | New password |
| callback | callback |

**Example**

```java
// Get email verification code
WiserHomeSdk.getUserInstance().getEmailValidateCode("86", "123456@123.com", new IValidateCallback () {
    @Override
    public void onSuccess () {
        Toast.makeText (mContext, "Success in obtaining verification code", Toast.LENGTH_SHORT) .show ();
    }
    @Override
    public void onError (String code, String error) {
        Toast.makeText (mContext, "code:" + code + "error:" + error, Toast.LENGTH_SHORT) .show ();
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

>[!TIP]
>
>After the password is reset, if multiple devices log in to the same account at the same time, other devices will trigger a callback for session failure. Please implement the actions after the callback, such as jumping to the login page.
>
>For more information, please refer to the chapter "Handling of Expired Session"
