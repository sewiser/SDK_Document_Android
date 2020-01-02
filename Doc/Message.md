# Message center

## Obtain message list

**[Description]**

It is used to obtain lists of all messages.

**[Method Prototype]**
```java
/**
 * Obtain message list
 *
 * @param callback
 */
void getMessageList(IWiserDataCallback<List<MessageBean>> callback);

Among,  MessageBeanprovides the following interfaces:

/**
 * Obtain date and time  Format: 2017-09-08 17:12:45
 *
 * @return date and time
 */
public String getDateTime() {
     return dateTime;
}
/**
 * Obtain message icon URL
 *
 * @return Message icon URL
 */
public String getIcon() {
     return icon;
}
/**
 * Obtain the message type name (if it is alarm type message, then dp points name are available.)
 *
 * @return message class name 
 */
public String getMsgTypeContent() {
     return msgTypeContent;
}

/**
 * Obtain the message content for interface display.
 *
 * @return Message content 
 */
public String getMsgContent() {

     return msgContent;

}

/**
 * obtain message type
 * 0: System Messages
 * 1: With new device
 * 2: With new friends
 * 4: Device alarm
 *
 * @return message class 
 */

public int getMsgType() {
     return msgType;
}

/**
 *  Obtain id of device
 Note: This field is only available for alarm type messages.
 *
 * @return device ID
 */
public String getMsgSrcId() {
     return msgSrcId;
}

/**
 * obtain message id
 *
 * @return message id
 */
public String getId() {
     return id;
}
```
**[Example Codes]**
```java
WiserHomeSdk.getMessageInstance().getMessageList(new IWiserDataCallback<List<MessageBean>>() {
     @Override
     public void onSuccess(List<MessageBean> result) {
     }
     @Override
     public void onError(String errorCode, String errorMessage) {
     }
});
```
## Delete messages

**[Description]**

It is used to delete messages in bulk.

**[Method Prototype]**
```java
/**
 *  Delete messages
 *
 * @param mIds to be deleted message id list
 * @param callback
 */
void deleteMessage(List<String> mIds, IBooleanCallback callback);
```
**[Example Codes]**
```java
List<String> deleteList = new ArrayList<>();  
deleteList.add(messageBean.getId());  //add the id of the targeted message into the list

WiserMessage.getInstance().deleteMessages(
     deleteList, 
     new IBooleanCallback() {
         @Override
         public void onSuccess() {       
         }
         @Override
         public void onError(String errorCode, String errorMessage) {

         }
});
```

### Get the latest message

**[Description]**

Gets the timestamp of the latest message

**[Method Prototype]**

```java

    /**
     *  Gets the timestamp of the latest message
     * @param callback
     */
    void getMessageMaxTime(IWiserDataCallback<Integer> callback);

```

**[Example Codes]**

```java

        WiserHomeSdk.getMessageInstance().getMessageMaxTime(new IWiserDataCallback<Integer>() {
            @Override
            public void onSuccess(Integer integer) {
                
            }

            @Override
            public void onError(String s, String s1) {

            }
        });
        
```


### Get the latest message based on the message type

**[Description]**

Get the latest message based on the message type, there are currently three types of messages (MSG_REPORT alert) (MSG_FAMILY family) (MSG_NOTIFY notification)

**[Method Prototype]**

```java

    /**
     * Get the latest message based on the message type
     * @param offset  The offset is obtained from the n th data
     * @param limit Number of messages per page
     * @param msgType  Message type (MSG_REPORT alert) (MSG_FAMILY family) (MSG_NOTIFY notification)
     * @param callback
     */
    void getMessageListByMsgType(int offset, int limit, MessageType msgType, IWiserDataCallback<MessageListBean> callback);

```

**[Example Codes]**


```java
        WiserHomeSdk.getMessageInstance().getMessageListByMsgType(offset, limit, MessageType.MSG_REPORT, new IWiserDataCallback<MessageListBean>() {
            @Override
            public void onSuccess(MessageListBean result) {
            
            }

            @Override
            public void onError(String errorCode, String errorMessage) {
            
            }
        });
        
```


### Gets the list of messages according to the message SrcId

**[Description]**

Gets the list of messages according to message SrcId, currently only messages of type (MSG_REPORT alert) are supported

**[Method Prototype]**

```java

    /**
     * Gets the list of messages according to the message SrcId
     * @param offset  The offset is obtained from the n th data
     * @param limit Number of messages per page
     * @param msgType  Message type (MSG_REPORT alert)
     * @param msgSrcId  Message SrcId
     * @param callback
     */
    void getMessageListByMsgSrcId(int offset, int limit, MessageType msgType, String msgSrcId, IWiserDataCallback<MessageListBean> callback);

```

**[Example Codes]**

```java
WiserHomeSdk.getMessageInstance().getMessageListByMsgSrcId(offset, limit, MessageType.MSG_REPORT, msgSrcId, true , new IWiserDataCallback<MessageListBean>() {
            @Override
            public void onSuccess(MessageListBean result) {
            }

            @Override
            public void onError(String errorCode, String errorMessage) {
            }
        });
        
```
