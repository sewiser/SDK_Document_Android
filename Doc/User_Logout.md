## Logout Interface

When the user account is switched, it is necessary to call the logout interface

**Example**

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
## Disable Account

**Declaration**

After calling the logout account interface, the account will be permanently deactivated after one week and all information under your account will be deleted. Log back in before that, and your deactivation request will be cancelled.

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
