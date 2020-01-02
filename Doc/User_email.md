# Use email Box Password for Login

Wiser Smart provides the email password login system.

## (1) User Email Box Password Registration

**[Description]**

User email password registration. 

**[Method Invocation]**
```java

/**Register your email and obtain the verification code received in the email. 
* Register your email and obtain the verification code received in the email.
* @param email
* @param callback
*/

void getRegisterEmailValidateCode(String countryCode, String email, IResultCallback callback);

/** Select a password for your email.
* @param countryCode Country code
* @param email       Email account
* @param passwd      Password
* @param code        verification code
* @param callback    Email registration callback interface. 
*/
WiserHomeSdk.getUserInstance().registerAccountWithEmail(final String countryCode, final String email, final String passwd, final String code, final IRegisterCallback callback);

```
**[Example Codes]**

```java
// Register your email and obtain the verification code received in the email.

WiserHomeSdk.getUserInstance().getRegisterEmailValidateCode("86","123456@123.com",new IResultCallback() {
    @Override
    public void onError(String code, String error) {
    }

    @Override
    public void onSuccess() {
    }
} );

// Select a password for your email.

WiserHomeSdk.getUserInstance().registerAccountWithEmail("86", "123456@123.com","123456","5723", new IRegisterCallback() {
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
**[Note]**

- Currently, the data of an account register in one country cannot be migrated to other countries. 

## (2) Use email Box Password for Login

**[Description]**

Use email box password for login

**[Method Invocation]**
```java

/** Use email box password for login
* @param email  Email account
* @param passwd      Password
*/
WiserHomeSdk.getUserInstance().loginWithEmail(String countryCode, String email, String passwd, final ILoginCallback callback);
```
**[Example Codes]**

```java
// Use email box password for login

WiserHomeSdk.getUserInstance().loginWithEmail("86", "123456@123.com", "123123", new ILoginCallback() {
    @Override
    public void onSuccess(User user) {
        Toast.makeText(mContext, "Login succeeds, username:").show();
   }

    @Override
    public void onError(String code, String error) {

        Toast.makeText(mContext, "code: " + code + "error:" + error, Toast.LENGTH_SHORT).show();
    }

});

```
## **(3) Reset the Password of User Email Box** 

**[Description]**

Reset the password of user email box 

**[Method Invocation]**
```java

// Use your email box to obtain the password to retrieve your password.
/**
* @param countryCode Country code
* @param email       Email account
* @param callback    Obtain the verification code callback interface. 
*/
WiserHomeSdk.getUserInstance().getEmailValidateCode(String countryCode, final String email, final IValidateCallback callback);



/** Reset email box password
* @param email     User account
* @param emailCode Verification code received in the email box.
* @param passwd    New password
* @param callback  Reset the password callback interface. 
**/
WiserHomeSdk.getUserInstance().resetEmailPassword(final String email, final String emailCode, final String passwd, final IResetPasswordCallback callback);

**[Example Codes]**

// Use the email box to obtain the verification code.

WiserHomeSdk.getUserInstance().getEmailValidateCode("86", "123456@123.com", new IValidateCallback() {
    @Override
    public void onSuccess() {
        Toast.makeText(mContext, "Obtaining verification code succeeds.", Toast.LENGTH_SHORT).show();
    }
    @Override
    public void onError(String code, String error) {
        Toast.makeText(mContext, "code: " + code + "error:" + error, Toast.LENGTH_SHORT).show();
    }
});

// Reset password

WiserHomeSdk.getUserInstance().resetEmailPassword("86", "123456@123.com", "123123", new IResetPasswordCallback() {
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
