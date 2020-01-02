### Wifi Group

#### Group List Acquisition

```java
/**
* Obtain the device list of product
* @param homeId home id
* @param groupId the group is not created, parameter groupId must be an integer -1
* @param productId the pid of the device what is using to create group
*/
WiserHomeSdk.newHomeInstance(homeId).queryDeviceListToAddGroup(groupId, productId, new IGetDevsFromGroupByPidCallback() {
    @Override
    public void onSuccess(List<GroupDeviceBean> bizResult) {

    }

    @Override
    public void onError(String errorCode, String errorMsg) {

    }
});
```

#### Creating a Group

```java
/**
* create a empty group
* @param homeId home id
* @param productId the pid of the device what is using to create group
* @param name a name of the group to be created
* @param selectedDeviceIds the deviceList choosed
*/
WiserHomeSdk.newHomeInstance(homeId).createNewGroup(productId, name, selectedDeviceIds, new ICreateGroupCallback() {
    @Override
    public void onSuccess(long groupId) {
			//return groupId
    }

    @Override
    public void onError(String errorCode, String errorMsg) {

    }
});
```

#### Update and Save Group

```java
/**
* update and save the group
* @param groupId group id
* @param deviceIds the choosed ids
*/
WiserHomeSdk.newGroupInstance(groupId).updateDeviceList(deviceIds, new IResultCallback() {
                @Override
                public void onError(String s, String s1) {

                }

                @Override
                public void onSuccess() {

                }
            });
```
