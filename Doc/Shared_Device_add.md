# Add Device Share

## Add Multiple Device Sharing (coverage)

Sharing multiple devices to users will override all previous user sharing

**Declaration**

```java
void addShare(long homeId, String countryCode, final String userAccount, ShareIdBean bean, boolean autoSharing, final IWiserResultCallback<SharedUserInfoBean> callback);
```

**Parameters**

| Parameter   | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| homeId      | device home id                                               |
| countryCode | share member country code                                    |
| userAccount | share member user account                                    |
| bean        | share device id list                                         |
| autoSharing | auto sharing                                                 |
| callback    | callback, including sharing success or failure, cannot be null |

**Example**

```java
WiserHomeSdk.getDeviceShareInstance().addShare(homeId, countryCode, userAccount,
                shareIdBean, autoSharing, new IWiserResultCallback<SharedUserInfoBean>() {
                    @Override
                    public void onSuccess(SharedUserInfoBean sharedUserInfoBean) {}
                    @Override
                    public void onError(String errorCode, String errorMsg) {}
                });
```



## Add Shares (new, not overwriting old Shares)

### Add shares (Called when the target user's id is known)

Sharing multiple devices to users will add the devices to all user shareing

**Declaration**

```java
void addShareWithMemberId(long memberId,List<String> devIds,IResultCallback callback);
```

**Parameters**

| Parameter | Description                                                  |
| --------- | ------------------------------------------------------------ |
| memberId  | share user member id                                         |
| devIds    | share device id list                                         |
| callback  | Callback, including sharing success or failure, cannot be null |

**Example**

```java
void addShareWithMemberId (memberId, devIds, new IResultCallback() {
    @Override
    public void onError(String code, String error) {}
    @Override
    public void onSuccess() {}
});
```



### Add shares (Called when the target user's account is known)

Sharing multiple devices to users will add the devices to all user shareing

**Declaration**

```java

void addShareWithHomeId(long homeId, String countryCode, String userAccount, List<String> devIds, IWiserResultCallback<SharedUserInfoBean> callback);
```

**Parameters**

| Parameters        | Description                                  |
| ----------- | ------------------------------------- |
| homeId      | device home id |
| countryCode | share member country code |
| userAccount | share member user account                                    |
| devIds      | share device id list                                         |
| callback    | Callback, including sharing success or failure, cannot be null |

**Example**

```java
void addShareWithHomeId(homeId, countryCode, userAccount, devIds, new IWiserResultCallback<SharedUserInfoBean>() {
    @Override
    public void onSuccess(SharedUserInfoBean bean) {}
    @Override
    public void onError(String errorMsg, String errorCode) {}
});
```
