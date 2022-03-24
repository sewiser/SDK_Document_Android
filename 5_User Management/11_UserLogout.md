# Account Logout
When the user account is switched, it is necessary to call the logout API.

## Java sample

```java
WiserHomeSdk.getUserInstance().logout (new ILogoutCallback () {
  @Override
  public void onSuccess () {
    // Sign out successfully
  }

  @Override
  public void onError (String errorCode, String errorMsg) {
  }
});
```

## Disable account

After calling the logout account interface, the account will be permanently deactivated after one week and all information under your account will be deleted. Log back in before that, and your deactivation request will be canceled.

```java
void cancelAccount (IResultCallback callback);
```
**Example**

```java
WiserHomeSdk.getUserInstance().cancelAccount (new IResultCallback () {
    @Override
    public void onError (String code, String error) {

    }
    @Override
    public void onSuccess () {

    }
});

```