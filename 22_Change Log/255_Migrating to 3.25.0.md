# Migrating to 3.25.0
In consideration of the privacy and security of user information, Wiser App SDK has optimized the mobile phone number registration feature. Starting from version 3.25.0, the previous version SMS verification code sending interface will be removed from the SDK. You need to use the new SMS verification code sending interface to replace the previous version interface to prevent compilation errors.

>**Note**: If you want to use the mobile phone number registration service, you can contact the relevant Wiser account manager.

## SMS sending interface after 3.25.0

**Description**



```java
WiserHomeSdk.getUserInstance().sendVerifyCodeWithUserName(String userName, String region, String countryCode, int type, IResultCallback callback);
```

 **Parameter**
 
 | Parameters | Description |
 | ---- | ---- |
 | userName | Mobile number |
 | region | Region, fill in by default: "" is fine |
 | countryCode | Phone area code: such as "86" |
 | type | Type of verification code sent: 1: Register verification code 2: Login verification code 3: Reset password verification code|
 | callback | callback |

**Sample**

```java
WiserHomeSdk.getUserInstance().sendVerifyCodeWithUserName("13666666666", "", "86", 1, new IResultCallback() {
            @Override
            public void onError(String code, String error) {
                Toast.makeText(mContext, "code: "+ code + "error:" + error, Toast.LENGTH_SHORT).show();
            }

            @Override
            public void onSuccess() {
                Toast.makeText(mContext, "Get the verification code successfully", Toast.LENGTH_SHORT).show();
            }
        });
```

## SMS sending interface before 3.25.0

**Description**



```java
WiserHomeSdk.getUserInstance().getValidateCode(String countryCode, String phoneNumber, final IValidateCallback callback);
```

 **Parameter**
 
 | Parameters | Description |
 | ---- | ---- |
 | countryCode | Phone area code: such as "86" |
 | phoneNumber | Phone Number |
 | callback | callback |

**Sample**

```java
WiserHomeSdk.getUserInstance().getValidateCode("86","13666666666", new IValidateCallback(){
    @Override
    public void onSuccess() {
        Toast.makeText(mContext, "Get the verification code successfully", Toast.LENGTH_SHORT).show();
    }

    @Override
    public void onError(String code, String error) {
        Toast.makeText(mContext, "code: "+ code + "error:" + error, Toast.LENGTH_SHORT).show();
    }
 });
```

## Related topics

