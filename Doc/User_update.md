# Modify User Infomation

## Change Nickname

**Declaration**

Change nickname

```java
void reRickName (String name, final IReNickNameCallback callback);
```
**Parameters**

| Parameters | Description |
| -------- | ---- |
| name | Nickname |
| callback | callback |

**Example**

```java
WiserHomeSdk.getUserInstance().reRickName (nickName,
    new IReNickNameCallback () {
        @Override
        public void onSuccess () {
        }
        @Override
        public void onError (String code, String error) {

        }
});
```
## Update User Time Zone

**Declaration**

Used to update the user time zone.

```java
void updateTimeZone(String timezoneId, IResultCallback callback);
```
**Parameters**

| Parameters | Description |
| ---------- | ------ |
| timezoneId | timezone id |
| callback | callback |

**Example**

```java
WiserHomeSdk.getUserInstance().updateTimeZone (
    timezoneId,
    new IResultCallback () {
        @Override
        public void onSuccess () {
        }

        @Override
        public void onError (String code, String error) {

        }
});
```
## Upload User Avatar
**Declaration**

Used to upload user-defined avatars.

```java
void uploadUserAvatar(File file, IBooleanCallback callback)
```
**Parameters**

| Parameters | Description |
| -------- | ---------------- |
| file | User avatar image file |
| callback | callback |

** Code Example **

```java
WiserHomeSdk.getUserInstance().uploadUserAvatar (
    file,
    new IBooleanCallback () {
        @Override
        public void onSuccess () {
        }

        @Override
        public void onError (String code, String error) {

        }
});
```
## Set the Temperature Unit
**Declaration**

Set whether the temperature unit is Celsius or Fahrenheit

* TempUnitEnum.Celsius: Celsius
* TempUnitEnum.Fahrenheit: Hua degree

```java
void setTempUnit (TempUnitEnum unit, IResultCallback callback);
```

| Parameters | Description |
| -------- | ---- |
| unit | unit |
| callback | callback |

## Update User Targeting

If necessary, the positioning information can be reported through the following interfaces:

```java
WiserSdk.setLatAndLong (lat, lon);
```

## Synchronize User information

When the user information changes, such as modifying the user's avatar, nickname, etc., you need to call the synchronous user information interface to keep the user information up to date. If multiple devices log in at the same time, one device modifies the user information. Another device also needs to synchronize user information. You can call the synchronization interface when viewing user information to synchronize the latest user information.

**Description**

Used to synchronize user information

```java
void updateUserInfo(IResultCallback callback);
```

**Parameters**

| **Parameters** | **Description** |
| -------------- | --------------- |
| callback       | callback        |

**Example**

```java
WiserHomeSdk.getUserInstance().updateUserInfo(new IResultCallback() {
    @Override
    public void onError(String code, String error) {

    }

    @Override
    public void onSuccess() {
        User user = WiserHomeSdk.getUserInstance().getUser();
    }
});
```

