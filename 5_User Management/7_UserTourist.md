# Anonymous Registration

**Declaration**

SDK provides anonymous registration to log in, passing parameters: nickName, anonymous login nickname; countryCode, country code.

 ```java
void touristRegisterAndLogin(String countryCode, String nickName, final IRegisterCallback callback)
 ```

 **Parameters**

| Params | Type     | Description       |
| ---- | ---- | ---- |
| countryCode | String    | Country code, 86: China, 1: USA |
| nickName | String    | Nickname of anonymous login  (for example: device name) |
| callback | IRegisterCallback | Callback |


 **Example**

 ```java
WiserHomeSdk.getUserInstance().touristRegisterAndLogin(countryCode, nickName, new IRegisterCallback() {
    @Override
    public void onSuccess(User user) {
        
    }
    @Override
    public void onError(String code, String error) {

    }
});
 ```

 ## Anonymous User Logout

 **Declaration**

 Users who log in anonymously can log out through this interface. Anonymous accounts will be logged out immediately.

 ```java
void touristLogOut(final ILogoutCallback callback)
 ```

 **Parameters**

| Params | Type        | Description |
| ---- | ---- | ---- |
| success | ILogoutCallback | Callback    |

 **Example**

```java
WiserHomeSdk.getUserInstance().touristLogOut(new ILogoutCallback() {
    @Override
    public void onSuccess() {
        
    }
    @Override
    public void onError(String code, String error) {

    }
});
```



 ## Anonymous User Bind Account

 **Declaration**

 Users who log in anonymously can further improve their mobile phone or email information and transform them into normal users.
There are usually two steps to perfecting information:

* Verify email or mobile phone

* Set account password

  

 ```java
void touristBindWithUserName(String countryCode, String userName, String verifyCode, String password, final IBooleanCallback callback)
 ```

 **Parameters**

| Params  | Type         | Description                                |
| ---- | ---- | ---- |
| countryCode | String       | Country code（For example: 1, USA; 86, China） |
| userName | String       | User's phone number or email               |
| vefifyCode | String       | Verification code                          |
| password | String       | Password                                   |
| callback | IBooleanCallback | Callback                                   |

 **实例代码**

```java
WiserHomeSdk.getUserInstance().touristBindWithUserName(countryCode, userName, code, password, new IBooleanCallback() {
    @Override
    public void onSuccess() {
        
    }
    @Override
    public void onError(String code, String error) {

    }
});
```

