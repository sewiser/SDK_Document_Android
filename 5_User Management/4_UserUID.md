# Use UID for Login

## User Uid Registration and Login

**Declaration**

If had registered, then automatically logged in. If had not registered, then automatically registered and logged in.

```java
WiserHomeSdk.getUserInstance().loginOrRegisterWithUid(String countryCode, String uid, String passwd, ILoginCallback callback);

//support to create a default family
WiserHomeSdk.getUserInstance().loginOrRegisterWithUid(String countryCode, String uid, String passwd, boolean isCreateHome, IUidLoginCallback callback);
```
**Parameters**

|Parameters | Description |
| ---- | ---- |
|countryCode | country code, for example: 86 |
| uid | uid |
| passwd | User Password |
| isCreateHome | Whether to create default family |
| callback | callback |

**Example**

```java
// uid login
WiserHomeSdk.getUserInstance().loginOrRegisterWithUid("86", "1234", "123456", new ILoginCallback () {
    @Override
    public void onSuccess (User user) {
        Toast.makeText (mContext, "Successfully logged in, username:", Toast.LENGTH_SHORT) .show ();
    }

    @Override
    public void onError (String code, String error) {
        Toast.makeText (mContext, "code:" + code + "error:" + error, Toast.LENGTH_SHORT) .show ();
    }
});
```