# Account Binding
There are two interfaces for account mailbox association. First, get the verification code, and then use the verification code to bind the mailbox.

## Get the verification code

**Declaration**

Get the verification code of the bound email

``` java
void sendBindVerifyCodeWithEmail(@NonNull String countryCode, @NonNull String email, @NonNull IResultCallback callback);
```

**Parameters**

| Param | Description   |
| ----------- | ----------------- |
| countryCode | Country code, for example: 86 |
| email | email |
| callback | Callback |

## Associate with the Email address

**Declaration**

Bind Email

``` java
void bindEmail(@NonNull String countryCode, @NonNull String email, @NonNull String code, @NonNull String sId, @NonNull IResultCallback callback);
```

**Parameters**

| Param | Description  |
| ----------- | ----------------- |
| countryCode | Country code, for example: 86 |
| email | email |
| code  | Verification Code   |
| sId   | User sessionId |
| callback | Callback  |

**Example**

``` java
        WiserHomeSdk.getUserInstance().sendBindVerifyCodeWithEmail("86","123456@123.com", new IResultCallback(){

            @Override
            public void onError(String code, String error) {

            }

            @Override
            public void onSuccess() {
                Toast.makeText(mContext, "sendBindVerifyCodeWithEmail success", Toast.LENGTH_SHORT).show();
            }
        });

        WiserHomeSdk.getUserInstance().bindEmail("86", "123456@123.com","123456", WiserHomeSdk.getUserInstance().getUser().getSid(), new IResultCallback() {
            @Override
            public void onError(String code, String error) {
                Toast.makeText(mContext, "bind fail", Toast.LENGTH_SHORT).show();
            }

            @Override
            public void onSuccess() {
                Toast.makeText(mContext, "bind success", Toast.LENGTH_SHORT).show();
            }
        });
```