# Migrating to 3.26.5

Starting from version 3.26.5, a new email verification code sending interface will be opened, and the method of use is the same as the mobile verification code interface.

>**Note**: The old email verification code sending interface is still available and may be removed from the SDK in the future. It is recommended to migrate to the new interface.

## Mailbox verification code sending interface after 3.26.5

**Description**



```java
WiserHomeSdk.getUserInstance().sendVerifyCodeWithUserName(String userName, String region, String countryCode, int type, IResultCallback callback);

```

 **Parameter**

| Parameter   | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| userName    | email address                                                |
| region      | Region, fill in by default: "" is fine                       |
| countryCode | Country code: such as "86"                                   |
| type        | Type of verification code sent: 1: Register verification code  3: Reset password verification code |
| callback    | callback                                                     |

**Sample**

```java
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
```

## Mailbox verification code sending interface before 3.26.5

## Email registration to get verification code

**Description**

Email registration to get verification code

```java
void getRegisterEmailValidateCode(String countryCode, String email, IResultCallback callback);
```

 **Parameter**

| Parameter   | **Description**               |
| ----------- | ----------------------------- |
| countryCode | country code, for example: 86 |
| email       | email                         |
| callback    | callback                      |

**Sample**

```java
//Email registration to get verification code
WiserHomeSdk.getUserInstance().getRegisterEmailValidateCode("86","123456@123.com",new IResultCallback() {
    @Override
    public void onError(String code, String error) {
    }

    @Override
    public void onSuccess() {
    }
} );
```

## Retrieve password by email to get verification code

**Description**

Retrieve password by email to get verification code

```java
WiserHomeSdk.getUserInstance().getEmailValidateCode(String countryCode, final String email, final IValidateCallback callback);
```

**Parameter**

| Parameter   | **Description**               |
| :---------- | :---------------------------- |
| countryCode | country code, for example: 86 |
| email       | email                         |
| callback    | callback                      |

**Sample**

```java
//Get email verification code
WiserHomeSdk.getUserInstance().getEmailValidateCode("86", "123456@123.com", new IValidateCallback() {
    @Override
    public void onSuccess() {
        Toast.makeText(mContext, "Get the verification code successfully", Toast.LENGTH_SHORT).show();
    }
    @Override
    public void onError(String code, String error) {
        Toast.makeText(mContext, "code: " + code + "error:" + error, Toast.LENGTH_SHORT).show();
    }
});
```

## Related topics



