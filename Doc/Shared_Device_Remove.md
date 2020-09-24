# Remove Sharing

## Delete Active Sharers

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
void removeUserShare(memberId, new IResultCallback() {
    @Override
    public void onError(String code, String error) {}
    @Override
    public void onSuccess() {}
})
```



## Delete Receiving Sharer

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
void removeReceivedUserShare(memberId, new IResultCallback() {
    @Override
    public void onError(String code, String error) {}
    @Override
    public void onSuccess() {}
})
```



## Single Device Remove Sharing

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
void disableDevShare(devId, memberId, new IResultCallback() {
    @Override
    public void onError(String code, String error) {}
    @Override
    public void onSuccess() {}
})
```



## Remove Shared Devices Received

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
