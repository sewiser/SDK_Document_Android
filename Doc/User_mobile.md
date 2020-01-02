## Use Mobile Phone Verification Code for Login

Wiser Smart provides the mobile phone verification code login system. 

### (1) Use Mobile Phone Verification Code for Login

**[Description]**

The mobile phone verification code login function needs to first call the verification code sending interface and send the verification code. Then call the phone verification code verification interface. Fill in the received verification code into the corresponding parameters.

**[Code Invocation]**

```java

/** Obtain mobile phone verification code.
* @param countryCode   Country code
* @param phoneNumber   Mobile phone number.
*/
WiserHomeSdk.getUserInstance().getValidateCode(String countryCode, String phoneNumber, final IValidateCallback callback);

/** Use mobile phone verification code for login
* @param countryCode Country code
* @param phone       Mobile phone number
* @param code        Verification code
* @param callback    Login callback interface. 
*/
WiserHomeSdk.getUserInstance().loginWithPhone(String countryCode, String phone, String code, final ILoginCallback callback)
```

**[Example Codes]**

```java

// Obtain mobile phone verification code.

WiserHomeSdk.getUserInstance().getValidateCode("86","13666666666", new IValidateCallback(){
    @Override
    public void onSuccess() {
       Toast.makeText(mContext, "Obtaining verification code succeeds.", Toast.LENGTH_SHORT).show();
    }
    @Override
    public void onError(String code, String error) {
        Toast.makeText(mContext, "code: " + code + "error:" + error, Toast.LENGTH_SHORT).show();
    }
});

// Use mobile phone verification code for login
WiserHomeSdk.getUserInstance().loginWithPhone("86", "13355555555", "123456", new ILoginCallback() {
    @Override
    public void onSuccess(User user) {
        Toast.makeText(mContext, "Login succeeds, username:" +WiserHomeSdk.getUserInstance().getUser().getUsername(), Toast.LENGTH_SHORT).show();
    }
    @Override
    public void onError(String code, String error) {
        Toast.makeText(mContext, error, Toast.LENGTH_SHORT).show();
    }
});
```
## Use Mobile Phone Password for Login

Wiser Smart provides the mobile phone password login system.

**(1) Register Password on the Mobile Phone.** 

**[Description]**

Register password on the mobile phone.

**[Method Invocation]**

```java


/** Obtain mobile phone verification code.
* @param countryCode   Country code
* @param phoneNumber   Mobile phone number.
*/

WiserHomeSdk.getUserInstance().getValidateCode(String countryCode, String phoneNumber, final IValidateCallback callback);



/** Use your mobile phone to register account and password.
* @param countryCode Country code
* @param phone       Mobile phone 
* @param passwd      Password
* @param code        Verification code
* @param callback    Login callback interface. 
*/

WiserHomeSdk.getUserInstance().registerAccountWithPhone(final String countryCode, final String phone, final String passwd, final String code, final IRegisterCallback callback);
```

**[Example Codes]**
```java

// Obtain mobile phone verification code.

WiserHomeSdk.getUserInstance().getValidateCode("86","13666666666", new IValidateCallback(){
    @Override
    public void onSuccess() {
        Toast.makeText(mContext, "Obtaining verification code succeeds.", Toast.LENGTH_SHORT).show();
    }
    @Override
    public void onError(String code, String error) {
        Toast.makeText(mContext, "code: " + code + "error:" + error, Toast.LENGTH_SHORT).show();
    }
});

// Use your mobile phone to register account and password.

WiserHomeSdk.getUserInstance().registerAccountWithPhone("86","13666666666","123456","124332", new IRegisterCallback() {
    @Override
    public void onSuccess(User user) {
        Toast.makeText(mContext, "The registration succeeds.", Toast.LENGTH_SHORT).show();
    }
    @Override
    public void onError(String code, String error) {
        Toast.makeText(mContext, "code: " + code + "error:" + error, Toast.LENGTH_SHORT).show();
    }
});

```

### (2) Mobile Phone Password Login

**[Description]**

Use mobile phone password for login.

**[Method Invocation]**
```java
/** Use mobile phone password for login.
* @param countryCode Country code
* @param phone       Mobile phone password
* @param passwd      Password
* @param callback    Login callback interface. 
*/
WiserHomeSdk.getUserInstance().loginWithPhonePassword(String countryCode, String phone, String passwd, final ILoginCallback callback);

```
**[Example Codes]**

```java

// Use mobile phone password for login.
WiserHomeSdk.getUserInstance().loginWithPhonePassword("86", "13666666666", "123456", new ILoginCallback() {
    @Override
    public void onSuccess(User user) {
        Toast.makeText(mContext, "Login succeeds, username:" +WiserHomeSdk.getUserInstance().getUser().getUsername(), Toast.LENGTH_SHORT).show();
    }

    @Override
    public void onError(String code, String error) {
        Toast.makeText(mContext, "code: " + code + "error:" + error, Toast.LENGTH_SHORT).show();
    }
});

```
### (3) Reset App Password on the Mobile Phone

**[Description]**

Reset App password on the mobile phone.

**[Method Invocation]**

```java
/** Obtain mobile phone verification code.
* @param countryCode   Country code
* @param phoneNumber   Mobile phone number.
*/
WiserHomeSdk.getUserInstance().getValidateCode(String countryCode, String phoneNumber, final IValidateCallback callback);



/** Reset password
* @param countryCode Country code
* @param phone       Mobile phone number
* @param code        Mobile phone verification code
* @param newPasswd   New password
* @param callback    Reset the mobile phone password callback interface. 
*/
WiserHomeSdk.getUserInstance().resetPhonePassword(final String countryCode, final String phone, final String code, final String newPasswd, final IResetPasswordCallback callback);

```
**[Example Codes]**

```java
// Obtain the verification code received on your mobile phone.
WiserHomeSdk.getUserInstance().getValidateCode("86", "13555555555", new IValidateCallback() {
    @Override
    public void onSuccess() {
        Toast.makeText(mContext, "Obtaining verification code succeeds.", Toast.LENGTH_SHORT).show();
    }
    @Override
    public void onError(String code, String error) {
        Toast.makeText(mContext, "code: " + code + "error:" + error, Toast.LENGTH_SHORT).show();
    }
});
// Reset the App password on your mobile phone.
WiserHomeSdk.getUserInstance().resetPhonePassword("86", "13555555555", "123456", "123123", new IResetPasswordCallback(){
    @Override
    public void onSuccess() {
        Toast.makeText(mContext, "Retrieve password succeeds.", Toast.LENGTH_SHORT).show();
    }
    @Override
    public void onError(String code, String error) {
        Toast.makeText(mContext, "code: " + code + "error:" + error, Toast.LENGTH_SHORT).show();
    }
});
```
