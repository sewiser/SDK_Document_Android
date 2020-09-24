# Migration from 1.x SDK

If you are using 1.x SDK, you need to migrate user accounts. If not, please ignore this section.

## Check User Upgrade

Check if you need to upgrade user.

**Declaration**

```java
boolean checkVersionUpgrade();
```

**Example**

```java
WiserHomeSdk.getUserInstance().checkVersionUpgrade();
```

## Upgrade Account
**Declaration**

```java
void upgradeVersion(IResultCallback callback);
```
**Example**

```java
WiserHomeSdk.getUserInstance().upgradeVersion ()
```
