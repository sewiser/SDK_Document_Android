# Shared Devices
When a device needs to be provided for other users to operate, the device can be shared with other users, and the user who receives the shared device can simply operate the device.

| Class Name           | Description                                       |
| -------------------- | ------------------------------------------------- |
| IWiserHomeDeviceShare | Share device, get share info, manage share device |

## Add Device Share
### Add Multiple Device Sharing (coverage)

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



### Add Shares (new, not overwriting old Shares)

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
WiserHomeSdk.getDeviceShareInstance().addShareWithMemberId(userId, devIdList, new IResultCallback() {
            @Override
            public void onError(String errorCode, String errorMsg) {
            }
            @Override
            public void onSuccess() {
            }
});
```


### Device Add Sharing

Sharing single or multiple devices to users will add the devices to all user shareing

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
WiserHomeSdk.getDeviceShareInstance().addShareWithHomeId(homeId, countryCode,
        userAccount, devsIdList, new IWiserResultCallback<SharedUserInfoBean>() {
            @Override
            public void onSuccess(SharedUserInfoBean sharedUserInfoBean) {
            }
    
            @Override
            public void onError(String errorCode, String errorMsg) {                       
            }
});
```



## Getting Shared Relationships

### Get List of All Active Shared Users in the Home

**Declaration**

```java
void queryUserShareList(long homeId, final IWiserResultCallback<List<SharedUserInfoBean>> callback);
```

**Parameters**

| Parameter | Description                                            |
| --------- | ------------------------------------------------------ |
| homeId    | home id                                                |
| callback  | callback, including success or failure, cannot be null |

**Example**

```java
WiserHomeSdk.getDeviceShareInstance().queryUserShareList(homeId, new IWiserResultCallback<List<SharedUserInfoBean>>() {
            @Override
            public void onSuccess(List<SharedUserInfoBean> sharedUserInfoBeans) {}
            @Override
            public void onError(String errorCode, String errorMsg) {}
        });
```



### Get List of All Shared Uers Received

**Declaration**

```java
void queryShareReceivedUserList(final IWiserResultCallback<List<SharedUserInfoBean>> callback);
```

**Parameters**

| Parameter | Description                                            |
| --------- | ------------------------------------------------------ |
| callback  | callback, including success or failure, cannot be null |

**Example**

```java
WiserHomeSdk.getDeviceShareInstance().queryShareReceivedUserList(new IWiserResultCallback<List<SharedUserInfoBean>>() {
    @Override
    public void onSuccess(List<SharedUserInfoBean> sharedUserInfoBeans) {
    }
    @Override
    public void onError(String errorCode, String errorMsg) {
    }
});
```



### Obtaining User-shared Data that is Actively Shared by a Single User

**Declaration**

```java
void getUserShareInfo(long memberId, final IWiserResultCallback<ShareSentUserDetailBean> callback);
```

**Parameters**

| Parameter | Description                                            |
| --------- | ------------------------------------------------------ |
| memberId  | share member id                                        |
| callback  | callback, including success or failure, cannot be null |

**Example**

```java
WiserHomeSdk.getDeviceShareInstance().getUserShareInfo(mRelationId, new IWiserResultCallback<ShareSentUserDetailBean>() {
                @Override
                public void onSuccess(ShareSentUserDetailBean shareSentUserDetailBean) {}
                @Override
                public void onError(String errorCode, String errorMsg) {}
            });
```



### Getting Shared Data from a Single Recipient

**Declaration**

```java
void getReceivedShareInfo(long memberId, final IWiserResultCallback<ShareReceivedUserDetailBean> callback);
```

**Parameters**

| Parameter | Description                                            |
| --------- | ------------------------------------------------------ |
| memberId  | member id                                              |
| callback  | callback, including success or failure, cannot be null |

**Example**

```java
 WiserHomeSdk.getDeviceShareInstance().getReceivedShareInfo(mRelationId, new IWiserResultCallback<ShareReceivedUserDetailBean>() {
                @Override
                public void onSuccess(ShareReceivedUserDetailBean shareReceivedUserDetailBean) {}
                @Override
                public void onError(String errorCode, String errorMsg) {}
            });
```



### Get a Single Device Shared User List

**Declaration**

```java
void queryDevShareUserList(String devId, final IWiserResultCallback<List<SharedUserInfoBean>> callback);
```

**Parameters**

| Parameter | Description                                            |
| --------- | ------------------------------------------------------ |
| devId     | device id                                              |
| callback  | callback, including success or failure, cannot be null |

**Example**

```java
WiserHomeSdk.getDeviceShareInstance().queryDevShareUserList(mDevId, new IWiserResultCallback<List<SharedUserInfoBean>>() {
        @Override
        public void onError(String errorCode, String errorMsg) {}
        @Override
        public void onSuccess(List<SharedUserInfoBean> shareUserBeen) {}
    });
```



### Who Shares Access Devices

**Declaration**

```java
void queryShareDevFromInfo(String devId, final IWiserResultCallback<SharedUserInfoBean> callback);
```

**Parameters**

| Parameter | Description                                            |
| --------- | ------------------------------------------------------ |
| devId     | receive share device id                                |
| callback  | callback, including success or failure, cannot be null |

**Example**

```java
WiserHomeSdk.getDeviceShareInstance().queryShareDevFromInfo(devId, new IWiserResultCallback<SharedUserInfoBean>() {
            @Override
            public void onSuccess(SharedUserInfoBean result) {
            }
            @Override
            public void onError(String errorCode, String errorMessage) {
            }
        });
```



## Remove Sharing

### Delete Active Sharers

The sharer deletes all shared relationships with this user through memberId (user dimension delete)

**Declaration**

```java
void removeUserShare(long memberId, IResultCallback callback);
```

**Parameters**

| Parameter | Description                                                  |
| --------- | ------------------------------------------------------------ |
| memberId  | share memer id                                               |
| callback  | callback, including delete success or failure, cannot be null |

**Example**

```java
WiserHomeSdk.getDeviceShareInstance().removeUserShare(memberId, new IResultCallback() {
    @Override
    public void onError(String code, String error) {
    }
    @Override
    public void onSuccess() {
    }
})
```



### Delete Receiving Sharer

The shared party obtains the information of all shared devices of this user through memberId

**Declaration**

```java
void removeReceivedUserShare(long memberId, IResultCallback callback);
```

**Parameters**

| Parameter | Description                                                  |
| --------- | ------------------------------------------------------------ |
| memberId  | revice share member id                                       |
| callback  | callback, including delete success or failure, cannot be null |

**Example**

```java
WiserHomeSdk.getDeviceShareInstance().removeReceivedUserShare(memberId, new IResultCallback() {
    @Override
    public void onError(String code, String error) {
    }
    @Override
    public void onSuccess() {
    }
})
```



### Single Device Remove Sharing

**Declaration**

```java
void disableDevShare(String devId, long memberId, IResultCallback callback);
```

**Parameters**

| Parameter | Description                                                  |
| --------- | ------------------------------------------------------------ |
| memberId  | share member id                                              |
| devId     | share device id                                              |
| callback  | callback, including delete success or failure, cannot be null |

**Example**

```java
WiserHomeSdk.getDeviceShareInstance().disableDevShare (devId, memberId, new IResultCallback() {
    @Override
    public void onError(String code, String error) {
    }
    @Override
    public void onSuccess() {
    }
});
```



### Remove Shared Devices Received

**Declaration**

```java
void removeReceivedDevShare(String devId, IResultCallback callback);
```

**Parameters**

| Parameter | Description                                                  |
| --------- | ------------------------------------------------------------ |
| devId     | reviced device id                                            |
| callback  | callback, including delete success or failure, cannot be null |

**Example**

```java
WiserHomeSdk.getDeviceShareInstance().removeReceivedDevShare(devId,new IResultCallback() {
    @Override
    public void onError(String code, String error) {}
    @Override
    public void onSuccess() {}
})
```



## Modify Note Name

### Modify the nickname of the active sharer

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



### Modify the Nickname of the Recipient Sharer

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
WiserHomeSdk.getDeviceShareInstance().renameReceivedShareNickname(mRelationId, inputText, new IResultCallback() {
                @Override
                public void onError(String s, String s1) {}
                @Override
                public void onSuccess() {}
            });
```
