## Change NickName

[Method Prototype]

```java
/**
* change nickname
*
* @param name   nickname
* @param callback
*/
void reRickName(String name, final IReNickNameCallback callback);
```
**[Example Codes]**

```java
WiserHomeSdk.getUserInstance().reRickName(
    nickName, 
    new IReNickNameCallback() {
        @Override
        public void onSuccess() {
        }

        @Override
        public void onError(String code, String error) {

        }
});
```

## Update user's time zone

[Method Prototype]

```java
/**
* Update user's time zone
*
* @param timezoneId   time zone id
* @param callback
*/
 void updateTimeZone(String timezoneId, IResultCallback callback);
```
**代码范例**

```java
WiserHomeSdk.getUserInstance().updateTimeZone(
    timezoneId, 
    new IResultCallback() {
        @Override
        public void onSuccess() {
        }

        @Override
        public void onError(String code, String error) {

        }
});
```

## Upload the User Account Picture

**[Description]**

It is for user to upload his/her self-defined account image. 

**[Method Prototype]**

```java
/**
 * Upload user account picture
 * @param file     user account picture file
 * @param callback
 */
void uploadUserAvatar(File file, IBooleanCallback callback)
```

**[Example Codes]**

```java
WiserHomeSdk.getUserInstance().uploadUserAvatar(
    file, 
    new IBooleanCallback() {
        @Override
        public void onSuccess() {
        }
        @Override
        public void onError(String code, String error) {

        }
});
```
## Set the Unit of Temperature

Select the centigrade or Fahrenheit.
```java
/**
 * TempUnitEnum.Celsius and TempUnitEnum.Fahrenheit *
 * @param unit
 * @param callback
 */
void setTempUnit(TempUnitEnum unit, IResultCallback callback);
```

## Update user location information

If necessary, the positioning information can be reported through the following interfaces:

```java
WiserSdk.setLatAndLong(lat,lon);
```
## Log Out of the Login Interface

The logout interface has to be invoked for account switching. 
```java
WiserHomeSdk.getUserInstance().logout(new ILogoutCallback() {
    @Override
    public void onSuccess() {
        // Logout succeeds
    }
    @Override
    public void onError(String errorCode, String errorMsg) {

    }
});
```


## Disable account (deregister user)

After one week, the account will be permanently disabled, and all information in the account will be deleted. If you log in to the account again before it is permanently disabled, your deregistration will be canceled.
```java
/**
* Deregister account
* Account cancellation
* @param callback
*/

void cancelAccount(IResultCallback callback);
```
**[Example Codes]**
```java
WiserHomeSdk.getUserInstance().cancelAccount(new IResultCallback() {
    @Override
    public void onError(String code, String error) {
    }
    @Override
    public void onSuccess() {
    }
});
```
