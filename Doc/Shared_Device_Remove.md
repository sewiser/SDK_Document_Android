# Removing Sharing

## (1) Deleting the shared relationship

**[Description]**

The sharer deletes all shared relationships with the relationship user via memberId (deleting user dimension).

**[Method Invocation]**
```java
@param memberId 	user member Id (obtained from SharedUserInfoBean)

void removeUserShare(long memberId, IResultCallback callback);
```
**[Example Codes]**
```java
WiserHomeSdk.getDeviceShareInstance().removeUserShare(memberId, new IResultCallback() {
    @Override
    public void onError(String code, String error) {
    }

    @Override
    public void onSuccess() {
    }

})
```
## (2) Deleting the received relationship for sharing

**[Description]**

The receiver deletes all shared relationships with the relationship user via memberId (deleting user dimension).
`
**[Method Invocation]**
```java
@param memberId 	user member Id (obtained from SharedUserInfoBean)
void removeReceivedUserShare(long memberId, IResultCallback callback);
```
**[Example Codes]**
```java
WiserHomeSdk.getDeviceShareInstance().removeReceivedUserShare(memberId, new IResultCallback() {
    @Override
    public void onError(String code, String error) {
    }


    @Override
    public void onSuccess() {
    }

})
```
## (3) Deleting sharing of a device

**[Description]**

The sharer deletes a shared device of a specified relationship user.

**[Method Invocation]**
```java
@param devId	device Id

@param memberId 	user member Id (obtained from SharedUserInfoBean)

void removeDevShare(String devId, long memberId, IResultCallback callback);
```
**[Example Codes]**
```java
WiserHomeSdk.getDeviceShareInstance().removeDevShare(devId, memberId, new IResultCallback() {
    @Override
    public void onError(String code, String error) {

    }

    @Override
    public void onSuccess() {

    }

})
```
## (4) Removing the received device for sharing

**[Description]**

The receiver deletes a shared device.

**[Method Invocation]**
```java
@param devId	device Id

void removeReceivedDevShare(String devId, IResultCallback callback);
```
**[Example Codes]**
```java
WiserHomeSdk.getDeviceShareInstance().removeReceivedDevShare(devId,new IResultCallback() {
    @Override
    public void onError(String code, String error) {

    }

    @Override
    public void onSuccess() {

    }

})
```
