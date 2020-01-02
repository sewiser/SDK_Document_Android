# Modifying Remark Name

## (1) Modifying the remark name of the person issuing the sharing information

**[Description]**

The sharer modifies the remark name of the person issuing the sharing information (i.e., if you receive the device shared by other users, you can modify their remark names. (sharing information issued)

**[Code Invocation]**
```java
* @param memberId     user member Id (obtained from SharedUserInfoBean)
* @param name   			  remark name to be modified
void renameShareNickname(long memberId, String name, IResultCallback callback);
```
**[Example Codes]**
```java
WiserHomeSdk.getDeviceShareInstance().renameShareNickname(memberId, name, new IResultCallback() {
    @Override
    public void onError(String code, String error) {        
    }
    @Override
    public void onSuccess() {
    }
})
```
## (2) Modifying the remark name of the person receiving the sharing information**

**[Description]**

The sharer modifies the remark name of the person receiving the sharing information (i.e., if you share a device to others, you can modify their remark names. (sharing information received)

**[Method Invocation]**
```java
* @param memberId     user member Id (obtained from SharedUserInfoBean)
* @param name    		 remark name to be modified 
void renameReceivedShareNickname(long memberId, String name, IResultCallback callback);
```
**[Example Codes]**
```java
WiserHomeSdk.getDeviceShareInstance().renameReceivedShareNickname(memberId, name, new IResultCallback() {
    @OverrideWiserHomeSdk.getDeviceShareInstance
    public void onError(String code, String error) {
        
	}
    @Override
    public void onSuccess() {
    }

})
```
