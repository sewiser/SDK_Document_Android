# Message Center
The message management module contains message center and push functions. Its messages have three categories: alarm, home, and notification, and each category supports turn on or turn off respectively.

| Class name | Description |
| ---- | ---- |
| IWiserMessage | Get Message List, Batch Delete Message, Check New Message |
| IWiserPush | Get Or Set Push Notification Status |

## Message

### Get message list

**Declaration**

```java
void getMessageList(IWiserDataCallback<List<MessageBean>> callback);
```

**Parameters**

| Parameter | Description |
| ---- | ---- |
| callback | Callbacks, including success and failure of getting message list |

**MessageBean data model**

| Field | Type | Description |
| ---- | ---- | ---- |
| dateTime | String | Date and time |
| Icon | String | Message icon URL |
| msgTypeContent | String | Message type name |
| msgContent | String | Message content |
| msgType | Integer | Message type |
| msgSrcId | String | Device Id (this field is only available in alarm messages) |
| id | String | Message id |

**Example**

```java
WiserHomeSdk.getMessageInstance().getMessageList(new IWiserDataCallback<List<MessageBean>>() {
    @Override
    public void onSuccess(List<MessageBean> result) {}
    @Override
    public void onError(String errorCode, String errorMessage) {}
});
```

### Get a list of paged messages

**Declaration**

```java
void getMessageList(int offset, int limit, IWiserDataCallback<MessageListBean> callback);
```

**Parameters**

| parameter | description |
| ---- | ---- |
| offset | Offset is obtained from the nth data |
| limit | Number of messages per page |
| callback | Callbacks, including success and failure |

**Example**

```java
WiserHomeSdk.getMessageInstance().getMessageList(offset, limit, new IWiserDataCallback<MessageListBean>() {
            @Override
            public void onSuccess(MessageListBean result) {}
            @Override
            public void onError(String errorCode, String errorMessage) {}
});
```

### Gets a list of messages by paging by message type

**Declaration**

```java
void getMessageListByMsgType(int offset, int limit, MessageType msgType, IWiserDataCallback<MessageListBean> callback);
```

**Parameters**

| parameter | description |
| ---- | ---- |
| offset | Offset is obtained from the nth data |
| limit | Number of messages per page |
| msgType | Message type (MSG\_REPORT alert) (MSG\_FAMILY family) (MSG\_NOTIFY notification) |
| callback | Callbacks, including success and failure |

**Example**

```java
WiserHomeSdk.getMessageInstance().getMessageListByMsgType(offset, limit, type, new IWiserDataCallback<MessageListBean>() {
      @Override
      public void onSuccess(MessageListBean result) {}
      @Override
      public void onError(String errorCode, String errorMessage) {}
});
```

### Get a list of detail messages by paging by MsgSrcId

The message list is obtained according to the message SrcId. Currently, only messages of the type (MSG_REPORT alarm) are supported.

**Declaration**

```java
void getMessageListByMsgSrcId(int offset, int limit, MessageType msgType, String msgSrcId, IWiserDataCallback<MessageListBean> callback);
```

**Parameters**

| parameter | description |
| ---- | ---- |
| offset | Offset is obtained from the nth data |
| limit | Number of messages per page |
| msgType | Message type (MSG_REPORT alert) |
| msgSrcId | Interest group id |
| callback | Callbacks, including success and failure |

>**Note**:
>1. If you need alarm information to support switching between different languages, you need to do language internationalization
>2. The alarm information that has been received will not change with the change of the phone system language

**Example**

```java
WiserHomeSdk.getMessageInstance().getMessageListByMsgSrcId(offset, limit, MessageType.MSG_REPORT, msgSrcId, true, new IWiserDataCallback<MessageListBean>() {
    @Override
    public void onSuccess(final MessageListBean result) {              
    }
    @Override
    public void onError(String errorCode, String errorMessage) {               
    }
});
```

### Delete message

#### Delete one or more message

**Declaration**

```java
void deleteMessages(List<String> mIds, IBooleanCallback callback);
```

**Parameters**

| parameter | description |
| ---- | ---- |
| mIds | Device ids |
| contact | Callbacks, including delete success and failure |

**Example**

```java
WiserHomeSdk.getMessageInstance().deleteMessages(mIds, new IBooleanCallback() {
    @Override
    public void onSuccess() {
    }
    @Override
    public void onError(String code, String error) {
    }
});
```

#### Delete one or more specific types of message

**Declaration**

```java
void deleteMessageWithType(int msgType, List<String> mIds, List<String> mSrcIds, final IBooleanCallback callback);
```

**Parameters**

| Parameter | Description |
| ---- | ---- |
| msgType | Message type（1 - alarm，2 - family，3 - notifiction） |
| mIds | Delete messageId list |
| mSrcIds | Delete alarm messageId list，null or empty mean don't delete alarm message |
| callback | Callbacks, including delete success and failure |

**Example**

```java
WiserHomeSdk.getMessageInstance().deleteMessageWithType(msgType, mIds, mSrcIds, new IBooleanCallback() {
    @Override
    public void onSuccess() {
    }
    @Override
    public void onError(String code, String error) {
    }
});
```

### Check new message

**Declaration**

```java
void requestMessageNew(final IWiserDataCallback<MessageHasNew> callback);
```

**Parameters**

| Parameter | Description |
| ---- | ---- |
| callback | Get the latest news type |

**MessageHasNew data model**

| field | type | description |
| ---- | ---- | ---- |
| alarm | boolean | Is there an alarm message |
| family | boolean | Is there an family message |
| notification | boolean | Is there an notification message |

**Example**

```java
WiserHomeSdk.getMessageInstance().requestMessageNew(new IWiserDataCallback<MessageHasNew>() {
    @Override
    public void onSuccess(MessageHasNew result) {     
    }
    @Override
    public void onError(String errorCode, String errorMessage) {
    }
});
```

## Push notification

### Get push notification status 

The message push switch is the master switch. In the off state, no messages such as device alarms, home messages, and notification messages can be received.

**Declaration**

```java
void getPushStatus(IWiserResultCallback<PushStatusBean> callback);
```

**Parameters**

| Parameters | Description |
| ---- | ---- |
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

### Set push notification status

The message push switch is the master switch, and no messages such as device alarms, home messages, notification messages, etc. can be received in the off state.

**Declaration**

```java
void setPushStatus(boolean isOpen, IWiserDataCallback<Boolean> callback);
```

**Parameters**

| Parameters | Description |
| ---- | ---- |
| isOpen | Whether to open |
| callback | Callbacks, including setting success and failure |

**Example**

```java
WiserHomeSdk.getPushInstance().setPushStatus(open, new IWiserDataCallback<Boolean>() {
      @Override
      public void onSuccess(Boolean result) {}
      @Override
      public void onError(String errorCode, String errorMessage) {}
});
```

### Get the switch status of the message according to the message type

Get the switch status of the current type of message according to the message type

**Declaration**

```java
void getPushStatusByType(PushType type, IWiserDataCallback<Boolean> callback);
```

**Parameters**

| Parameters | Description |
| ---- | ---- |
| type | Message type(0-alarm message, 1-family message, 2-notification message, 4-marketing message) |
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

### Set the switch status of the message according to the message type

Set the switch status of the current type of message according to the message type.

**Declaration**

```java
void setPushStatusByType(PushType type, isOpen, IWiserDataCallback<Boolean> callback);
```

**Parameter**

| Parameter | Description |
| ---- | ---- |
| type | Message type(0-alarm message, 1-family message, 2-notification message, 4-marketing message) |
| isOpen | Whether to open |
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