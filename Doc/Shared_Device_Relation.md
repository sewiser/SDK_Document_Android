# Getting Shared Relationships

## Get List of All Active Shared Users in the Home

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



## Get List of All Shared Uers Received

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
            public void onSuccess(List<SharedUserInfoBean> sharedUserInfoBeans) {}
            @Override
            public void onError(String errorCode, String errorMsg) {}
        });
```



## Obtaining User-shared Data that is Actively Shared by a Single User

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



## Getting Shared Data from a Single Recipient

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



## Get a Single Device Shared User List

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



## Who Shares Access Devices

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
WiserHomeSdk.getDeviceShareInstance().queryDevShareUserList(devId, new IWiserResultCallback<List<SharedUserInfoBean>>() {
            @Override
            public void onError(String s, String s1) {}
            @Override
            public void onSuccess(List<SharedUserInfoBean> list) {
            }
        });
```
