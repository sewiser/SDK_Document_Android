# Push Notification

## Get Push Notification Status 

The message push switch is the master switch. In the off state, no messages such as device alarms, home messages, and notification messages can be received.

**Declaration**

```java
void getPushStatus(IWiserResultCallback<PushStatusBean> callback);
```

**Parameters**

| Parameters     | Description                    |
| -------- | ----------------------- |
| callback | callbacks, including success and failure to get total switch status |

**Example**

```java
 WiserHomeSdk.getPushInstance().getPushStatus(new IWiserResultCallback<PushStatusBean>() {
       @Override
       public void onSuccess(PushStatusBean result) {}
       @Override
       public void onError(String errorCode, String errorMessage) {}
 });
```



## Set Push Notification Status

The message push switch is the master switch, and no messages such as device alarms, home messages, notification messages, etc. can be received in the off state.

**Declaration**

```java
void setPushStatus(boolean isOpen, IWiserDataCallback<Boolean> callback);
```

**Parameters**

| Parameters     | Description                       |
| -------- | --------------------------- |
| isOpen   | Whether to open                    |
| callback | Callbacks, including setting success and failure             |

**Example**

```java
WiserHomeSdk.getPushInstance().setPushStatus(open, new IWiserDataCallback<Boolean>() {
      @Override
      public void onSuccess(Boolean result) {}
      @Override
      public void onError(String errorCode, String errorMessage) {}
});
```



## Get the switch status of the message according to the message type

Get the switch status of the current type of message according to the message type

**Declaration**

```java
void getPushStatusByType(PushType type, IWiserDataCallback<Boolean> callback);
```

**Parameters**

| Parameters     | Description                     |
| -------- | ------------------------ |
| type     | Message type                |
| callback | Callbacks, including success and failure |

**Example**

```java
WiserHomeSdk.getPushInstance().getPushStatusByType(type, new IWiserDataCallback<Boolean>() {
      @Override
      public void onSuccess(Boolean result) {}
      @Override
      public void onError(String errorCode, String errorMessage) {}
});
```



## Set the switch status of the message according to the message type

Set the switch status of the current type of message according to the message type.

**Declaration**

```java
void setPushStatusByType(PushType type, isOpen, IWiserDataCallback<Boolean> callback);
```

**Parameter**

| Parameter     | Description                     |
| -------- | ------------------------ |
| type     | Message type                 |
| isOpen     | Whether to open                 |
| callback | Callbacks, including success and failure |

**Example**

```java
WiserHomeSdk.getPushInstance().setPushStatusByType(pushType, checked, new IWiserDataCallback<Boolean>() {
      @Override
      public void onSuccess(Boolean result) {
      }

      @Override
      public void onError(String errorCode, String errorMessage) {
      }
});
```

