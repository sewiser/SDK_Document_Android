# Migration of One Series of SDK Accounts

Upgrade after the login

```java
/**
* Check to determine whether the user data needs to be upgraded
*
* @return
*/
boolean checkVersionUpgrade();

/**
* Upgrade the account.
/
void upgradeVersion(IResultCallback callback);

/**
*	Check upgrade
*/
WiserHomeSdk.getUserInstance().checkVersionUpgrade()

/**
*	Upgrade the user account.
*/
WiserHomeSdk.getUserInstance().upgradeVersion()
```
