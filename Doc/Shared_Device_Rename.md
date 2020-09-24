# Modify Note Name

## Modify the nickname of the active sharer

The sharer modifies the remark name of the person being shared. If you share the device with other people, you can modify the remark name of the person.

**Declaration**

```java
void renameShareNickname(long memberId, String name, IResultCallback callback);
```

**Parameters**

| Parameters        | Description                                  |
| ----------- | ------------------------------------- |
| memberId | share member id   |
| name       | new name                                                     |
| callback | callback, including modification success and failure, cannot be null |

**Example**

```java
WiserHomeSdk.getDeviceShareInstance().renameShareNickname(mRelationId, inputText, new IResultCallback() {
                @Override
                public void onError(String s, String s1) {}
                @Override
                public void onSuccess() {}
            });
```



## Modify the Nickname of the Recipient Sharer

**Declaration**

```java
void renameReceivedShareNickname(long memberId, String name, IResultCallback callback);
```

**Parameters**

| Parameters     | Description |
| -------- | -------------------------------------- |
| memberId   | revice share member id                                       |
| name | new name                                                     |
| callback | callback, including modification success and failure, cannot be null |

**Example**

```java
void addShareWithHomeId(homeId, countryCode, userAccount, devIds, new IWiserResultCallback<SharedUserInfoBean>() {
    @Override
    public void onSuccess(SharedUserInfoBean bean) {}
    @Override
    public void onError(String errorMsg, String errorCode) {}
});
```
