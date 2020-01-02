## Message Center

### Message Push Setting

#### Gets the current state of the message master switch

##### 【Description】

The message push switch is the main switch, and when it is off, it cannot receive any message such as device Alarm, Family, Notify message.

##### 【Method】

```java
   /**
     * Gets the message master switch state
     * @param callback
     */
    void getPushStatus(IWiserResultCallback<PushStatusBean> callback);
```

##### 【Example Codes】

```java
 WiserHomeSdk.getPushInstance().getPushStatus(new IWiserResultCallback<PushStatusBean>() {
            @Override
            public void onSuccess(PushStatusBean result) {
            }

            @Override
            public void onError(String errorCode, String errorMessage) {
            }
        });
```

#### Set the message master switch

##### 【Description】

The message push switch is the main switch, and when it is off, it cannot receive any message such as device Alarm, Family, Notify message.

##### 【Method】

```java
    /**
     * Set the message master switch
     * @param isOpen Message is Open
     * @param callback
     */
    void setPushStatus(boolean isOpen, IWiserDataCallback<Boolean> callback);
```

##### 【Example Codes】

```java
WiserHomeSdk.getPushInstance().setPushStatus(open, new IWiserDataCallback<Boolean>() {
            @Override
            public void onSuccess(Boolean result) {
            }

            @Override
            public void onError(String errorCode, String errorMessage) {
            }
        });
```


#### Gets the on-off state of a message based on its type

##### 【Description】

Gets the on-off state of a message based on its type

##### 【Method】

```java
  /**
     *  Gets the on-off state of a message based on its type
     *  PushType.PUSH_ALARM  Alarm Message
     *  PushType.PUSH_FAMILY Family Message
     *  PushType.PUSH_NOTIFY Notify Message
     * @param type Message type
     * @param callback
     */
    void getPushStatusByType(PushType type, IWiserDataCallback<Boolean> callback);
```

##### 【Example Codes】

```java
    WiserHomeSdk.getPushInstance().getPushStatusByType(type, new IWiserDataCallback<Boolean>() {
            @Override
            public void onSuccess(Boolean result) {
            }

            @Override
            public void onError(String errorCode, String errorMessage) {
            }
        });
```

#### Sets the on-off state of a message based on its type

##### 【Description】

Sets the on-off state of a message based on its type

##### 【Method】

```java
  /**
     *  Sets the on-off state of a message based on its type
     *  PushType.PUSH_ALARM  Alarm Message
     *  PushType.PUSH_FAMILY Family Message
     *  PushType.PUSH_NOTIFY Notify Message
     * @param type Message Type
     * @param isOpen Message is Open
     * @param callback
     */
    void setPushStatusByType(PushType type, isOpen, IWiserDataCallback<Boolean> callback);
```

##### 【Example Codes】

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
