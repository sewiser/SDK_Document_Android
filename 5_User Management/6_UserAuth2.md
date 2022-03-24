# Login by Auth2

**Declaration**

Auth2 is a general login interface. You can use some Auth2 login type by passed type parameters.

```java
void thirdLogin(String countryCode, String accessToken, String type, String extraInfo, ILoginCallback callback) 
```

**Parameters**

| Param   | Description                                              |
| ---- | ---- |
| countryCode | Country code, for example: 86                            |
| accessToken | AccessToken                                              |
| type    | Type of Auth2 interface call, for example: "gg" for Google login |
| extraInfo  | Extra info                                               |
| callback | Callback                                                 |

**Example**

```java
WiserHomeSdk.getUserInstance().thirdLogin("your_country_code","auth2_token","auth2_type","{"info_key":"info_value"}", new ILoginCallback() {
    @Override
    public void onSuccess(User user) {
       
    }
    @Override
    public void onError(String code, String error) {
      
    }
});
```



## Login with Google

**Declaration**

The Auth2 interface supports three-party login. After the authorization is successful, insert the token (here, Google id Token) and extraInfo and other information through the Auth2 connection to achieve Google login. (Recommended for foreign users)

**Parameters**

| Param   | Description               |
| ---- | ---- |
| type    | "gg"                      |
| countryCode | Country code, for example: 86 |
| accessToken | Google authorized id token |
| extraInfo  | {\"pubVersion\": 1}       |
| callback | Callback                  |

**示例代码**

```java
WiserHomeSdk.getUserInstance().thirdLogin(countryNumberCode,token,"gg","{\"pubVersion\":1}", new ILoginCallback() {
    @Override
    public void onSuccess(User user) {
       
    }
    @Override
    public void onError(String code, String error) {
      
    }
});
```