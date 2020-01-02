## Group
IWiserGroup class provides operations on Mesh groups
### Mesh Group Judgment Method

IWiserGroup class provides operations on Mesh groups
#####  【Example Codes】

```java
GroupBean groupBean=WiserHomeSdk.getDataInstance().getGroupBean("groupId");
if(!TextUtils.isEmpty(groupBean.getMeshId())){    
	L.d(TAG, "This group is mesh group");
}else{

}

```

### Add Sub-devices To Group

##### 【Method Invocation】
```java
* @param devId		device Id
* @param callback	
public void addDevice(String devId,IResultCallback callback);
```
##### 【Example Codes】

```java
IWiserGroup mGroup = WiserHomeSdk.newBlueMeshGroupInstance(groupId);
mGroup.addDevice("devId", new IResultCallback() {
            @Override
            public void onError(String code, String errorMsg) {
            		Toast.makeText(mContext, "Adding device to group failed "+ errorMsg, Toast.LENGTH_LONG).show();
            }

            @Override
            public void onSuccess() {
            		Toast.makeText(mContext, "Adding device to group success", Toast.LENGTH_LONG).show();
            }
        });
```


### Remove Sub-devices from Group
##### 【Method Invocation】
```java
* @param devId		device id
* @param callback	
public void removeDevice(String devId,IResultCallback callback);

```

##### 【Example Codes】
```java
IWiserGroup mGroup = WiserHomeSdk.newBlueMeshGroupInstance(groupId);
mGroup.removeDevice("devId", new IResultCallback() {
            @Override
            public void onError(String code, String errorMsg) {
            		Toast.makeText(mContext, "Remove device from group failed "+ errorMsg, Toast.LENGTH_LONG).show();
            }

            @Override
            public void onSuccess() {
            		Toast.makeText(mContext, "Remove device from group success ", Toast.LENGTH_LONG).show();
            }
        });

```

### Dismiss Group
##### 【Method Invocation】
```java
* @param callback	
public void dismissGroup(IResultCallback callback);
```
##### 【Example Codes】
```java
IWiserGroup mGroup = WiserHomeSdk.newBlueMeshGroupInstance(groupId);
mGroup.dismissGroup(new IResultCallback() {
            @Override
            public void onError(String code, String errorMsg) {
            		Toast.makeText(mContext, "dismiss group failed "+ errorMsg, Toast.LENGTH_LONG).show();
            }

            @Override
            public void onSuccess() {
            		Toast.makeText(mContext, "dismiss group success", Toast.LENGTH_LONG).show();
            }
        });

```


### Rename Group
##### 【Method Invocation】
```java
* @param groupName	rename name
* @param callback	
public void renameGroup(String groupName,IResultCallback callback);
```
##### 【Example Codes】
```java
IWiserGroup mGroup = WiserHomeSdk.newBlueMeshGroupInstance(groupId);
mGroup.renameGroup("new group name",new IResultCallback() {
            @Override
            public void onError(String code, String errorMsg) {
            		Toast.makeText(mContext, "rename group failed "+ errorMsg, Toast.LENGTH_LONG).show();
            }

            @Override
            public void onSuccess() {
            		Toast.makeText(mContext, "rename group success", Toast.LENGTH_LONG).show();
            }
        });

```
