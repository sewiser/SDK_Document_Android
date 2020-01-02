### Zigbee Group

#### Group List Acquisition

```java
/**
* Obtain the device list of product
* @param homeId home id
* @param groupId the group is not created, parameter groupId must be an integer -1
* @param productId the pid of the device what is using to create group
*/
WiserHomeSdk.newHomeInstance(homeId).queryZigbeeDeviceListToAddGroup(groupId, productId, 
        new IWiserResultCallback<List<GroupDeviceBean>>() {
            @Override
            public void onSuccess(List<GroupDeviceBean> arrayList) {
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
* @param meshId deviceBean.getMeshId()
* @param name a name of the group to be created
*/
WiserHomeSdk.newHomeInstance(homeId).createZigbeeGroup(productId, meshId, name, new IWiserResultCallback<CloudZigbeeGroupCreateBean>() {
    @Override
    public void onSuccess(CloudZigbeeGroupCreateBean cloudZigbeeGroupCreateBean) {
        //out
        long mGroupId = cloudZigbeeGroupCreateBean.getGroupId();
        String mGId = cloudZigbeeGroupCreateBean.getLocalId();
    }

    @Override
    public void onError(String errorCode, String errorMsg) {
    }
});
```

#### Add Devices to Group

```java
/**
* add devices to group
* @param meshId deviceBean.getMeshId()
* @param selectedDeviceIds the idList of the selected devices
* @param gid the localId of group（groupBean.getLocalId() or cloudZigbeeGroupCreateBean.getLocalId()）
*/
mIWiserZigbeeGroup.addDeviceToGroup(meshId, selectedDeviceIds, gid, new IWiserResultCallback<ZigbeeGroupCreateResultBean>() {
            @Override
            public void onSuccess(ZigbeeGroupCreateResultBean zigbeeGroupCreateResultBean) {
                if (zigbeeGroupCreateResultBean != null) {
                    //add successfully idlist
                    if (zigbeeGroupCreateResultBean.getSuccess() != null && zigbeeGroupCreateResultBean.getSuccess().size() > 0) {
                        List<String> mAddSuccessDeviceIds = new ArrayList<>();
                        mAddSuccessDeviceIds.addAll(zigbeeGroupCreateResultBean.getSuccess());
                    }
                    //add failure idlist
                    if (zigbeeGroupCreateResultBean.getFailure() != null && zigbeeGroupCreateResultBean.getFailure().size() > 0) {
                        List<String>mAddFailDeviceIds = new ArrayList<>();
                        mAddFailDeviceIds.addAll(zigbeeGroupCreateResultBean.getFailure());
                    }
                }
            }

            @Override
            public void onError(String errorCode, String errorMsg) {
            }
        });
```

#### Delete Devices of Group

```java
/**
* delete devices of group
* @param meshId deviceBean.getMeshId()
* @param selectedDeviceIds the idList of the selected devices
* @param gid the localId of group（groupBean.getLocalId() or cloudZigbeeGroupCreateBean.getLocalId()）
*/
mIWiserZigbeeGroup.delDeviceToGroup(meshId, selectedDeviceIds, gid, new IWiserResultCallback<ZigbeeGroupCreateResultBean>() {
            @Override
            public void onSuccess(ZigbeeGroupCreateResultBean zigbeeGroupCreateResultBean) {
                if (zigbeeGroupCreateResultBean != null) {
                    //delete successfully idlist
                    if (zigbeeGroupCreateResultBean.getSuccess() != null && zigbeeGroupCreateResultBean.getSuccess().size() > 0) {
                        List<String> mDelSuccessDeviceIds = new ArrayList<>();
                        mDelSuccessDeviceIds.addAll(zigbeeGroupCreateResultBean.getSuccess());
                    }
                    //delete failure idlist
                    if (zigbeeGroupCreateResultBean.getFailure() != null && zigbeeGroupCreateResultBean.getFailure().size() > 0) {
                        List<String> mDelFailDeviceIds = new ArrayList<>();
                        mDelFailDeviceIds.addAll(zigbeeGroupCreateResultBean.getFailure());
                    }
                }
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
* @param selectedDeviceIds the ids of the choosed device that to add or del successfully
*/
WiserHomeSdk.newZigbeeGroupInstance(groupId).updateGroupDeviceList(homeId, selectedDeviceIds, new IResultCallback() {
        @Override
        public void onError(String s, String s1) {
        }

        @Override
        public void onSuccess() {
        }
    });
```
