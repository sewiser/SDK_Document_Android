# Handling of Expired Session
If you have not logged in to your account for a long time, the session expiration error will be returned when you access the server interface. You have to monitor the notification of the`setOnNeedLoginListener` and log in to the account again after the login page is displayed.

**Declaration**

```java
WiserHomeSdk.setOnNeedLoginListener(INeedLoginListener needLoginListener);
```
**Example**

```java
WiserHomeSdk.setOnNeedLoginListener(new INeedLoginListener() {
  @Override
  public void onNeedLogin(Context context) {

  }
});
```

>**Notes**:
>* Once such a callback occurs, please go to the login page and let the user log in again.
>* Recommended for use in Application