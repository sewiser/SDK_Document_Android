# Feedback

If user intends to submit feedback, he has to select the type of feedback first and fill the feedback content. After submission, a feedback talk will be generated based on the selected type of feedback. User may continue to fill feedback in the session, and the feedback will be displayed in the feedback list of the session.

All functions related to the feedback will be realized by using the IWiserFeedbackManager Or IWiserFeedbackMsg class. Obtaining feedback talk list, feedback content list in the session and feedback type list and adding feedback are supported.

|Class Name |         Description |
|----|----|
| IWiserFeedbackManager | Feedback management class|
| IWiserFeedbackMsg | A feedback management class for some conversation |

## Obtain Feedback Talk List

Obtain the feedback talk list submitted by user

**Declaration**

```java
void getFeedbackList(final IWiserDataCallback<List<FeedbackBean>> callback);
```

**Parameters**

| Parameters | Description                                              |
| ---- | ---- |
| callback  | Callback, including obtain feedback list success or failure, cannot be null |

**FeedbackBean data model**

| field | type  | description                                              |
| ---- | ---- | ---- |
| dateTime | String | Date and time                                            |
| content | String | Feedback content                                         |
| hdId | String | Feedback id                                              |
| hdType  | String | Feedback Type                                            |
| title | String | Title (if it is equipment failure feedback, that is, equipment name) |

**Example**

```java
WiserHomeSdk.getWiserFeekback().getFeedbackManager().getFeedbackList(new IWiserDataCallback<List<FeedbackBean>>() {
     @Override
     public void onSuccess(List<FeedbackBean> feedbackTalkBeans) {
     }
     @Override
     public void onError(String errorCode, String errorMessage) {
     }
}); 
```
## Obtain Feedback List

Obtain the feedback content list from the feedback talk. 

**Declaration**

```java
IWiserFeedbackMag getFeedbackMsg(String hdId, int hdType);
void getMsgList(IWiserDataCallback<List<FeedbackMsgBean>> callback);
```

**Parameters**

| Parameters    | Description                                              |
| ---- | ---- |
| hdId          | Feedback Id                                              |
| hdType        | Feedback type                                            |
| IWiserDataCallback | callback, including obtain feedback list success or failure, cannot be null |

**Example**

```java
WiserHomeSdk.getWiserFeekback().getFeedbackMsg(hdId, hdType).getMsgList(new IWiserDataCallback<List<FeedbackMsgBean>>() {
    @Override
    public void onSuccess(List<FeedbackMsgBean> result) {}
    @Override
    public void onError(String errorCode, String errorMessage) {}
});
```

## Obtain Feedback Type List

The feedback type can be selected first when adding feedback.

**Declaration**

```java
void getFeedbackType(final IWiserDataCallback<List<FeedbackTypeRespBean>> callback);
```

**Parameters**

| Parameters | Description                                              |
| ---- | ---- |
| callback  | callback, including obtain feedback list success or failure, cannot be null |

**FeedbackTypeRespBean data model**

| field | type               | description                                     |
| ---- | ---- | ---- |
| list | List<FeedbackTypeBean> | Feedback type list                              |
| type | String             | List categories (currently only devices and others) |

**FeedbackTypeBean data model**

| field | type  | description                                              |
| ---- | ---- | ---- |
| hdId  | String | Feedback id                                              |
| hdType | String | feedback type                                            |
| title | String | Title (if it is equipment failure feedback, that is, equipment name) |

**Example**

```java
WiserHomeSdk.getWiserFeekback().getFeedbackManager().getFeedbackType(new IWiserDataCallback<List<FeedbackTypeRespBean>>() {
    @Override
    public void onSuccess(List<FeedbackTypeRespBean> feedbackTypeRespBeans) {}
    @Override
    public void onError(String errorCode, String errorMsg) {}
});
```

## Add Feedback

Add and submit feedback.

**Declaration**

```java
void addFeedback(final String message,String contact, String hdId, int hdType, final IWiserDataCallback<FeedbackMsgBean> callback);
```

**Parameters**

| Parameters | Description                                            |
| ---- | ---- |
| message | Feedback content                                       |
| contact | Contact information (phone or email)                   |
| hdId   | Feedback Id                                            |
| hdType | Feedback type                                          |
| callback  | Callback, including add success or failure, cannot be null |

**Example**

```java
WiserHomeSdk.getWiserFeekback().getFeedbackManager().addFeedback(
     “Thedevice fails ", //feedback
     "abc@qq.com",
     feebackTypeBean.getHdId(), 
     feebackTypeBean.getHdType(), 
     new IWiserDataCallback<FeedbackMsgBean>() {
         @Override
         public void onSuccess(FeedbackMsgBean feedbackMsgBean) {
         }
         @Override
         public void onError(String errorCode, String errorMsg) {
         }
});
```