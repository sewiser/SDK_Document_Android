# Group Management

## Functional Overview

The Wiser Cloud supports the group management system. User can create group, change group name, manage devices of group, manage multiple devices via the group and dismiss group.
Wiser Smart provides some interfaces for device group control.

## Create Group

### Create Wi-Fi Group

#### Group List Acquisition

Obtain the device list of product

```java
WiserHomeSdk.newHomeInstance(homeId).queryDeviceListToAddGroup(groupId, productId, 
        new IWiserResultCallback<List<GroupDeviceBean>>() {
               @Override
               public void onSuccess(List<GroupDeviceBean> arrayList) {
               }
        
               @Override
               public void onError(String errorCode, String errorMsg) {
               }
        });
```

**Parameters**


| Parameters | Description |
| ---- | ---- |
| homeId   | Family ID, please refer to the family management section for details |
| groupId  | the group is not created, parameter groupId must be an integer -1 |
| productId  | Select the pid of the device that created the group |

#### Creating a Group

```java
WiserHomeSdk.newHomeInstance(mHomeId).createGroup(productId, name, selectedDeviceIds, 
        new IWiserResultCallback<Long>() {
            @Override
            public void onSuccess(Long groupId) {
                    //return groupId
            }
        
            @Override
            public void onError(String errorCode, String errorMsg) {
            }
        });
```
**Parameters**

| Parameters | Description |
| ---- | ---- |
| homeId   | Family ID, please refer to the family management section for details |
| productId       | the pid of the device what is using to create group|
| name            | a name of the group to be created |
| selectedDeviceIds  | the deviceList choosed |

#### Update and Save Group

```java
WiserHomeSdk.newGroupInstance(groupId).updateDeviceList(deviceIds, 
        new IResultCallback() {
        
            @Override
            public void onError(String s, String s1) {
            
            }
            
            @Override
            public void onSuccess() {
            
            }
        });
```
**Parameters**

| Parameters | Description |
| ---- | ---- |
| groupId         | group id |
| deviceIds       | Add or delete the selected device id list |

### Create ZigBee Group

Support ZigBee sub-devices, smart gateway pro sub-devices, Sub-G sub-devices and other devices that reuse the ZigBee network protocol to form groups

#### Group List Acquisition

```java
WiserHomeSdk.newHomeInstance(homeId).queryZigbeeDeviceListToAddGroup(groupId, productId, meshId, 
          new IWiserResultCallback<List<GroupDeviceBean>>() {
                @Override
                public void onSuccess(List<GroupDeviceBean> arrayList) {
                }
    
                @Override
                public void onError(String errorCode, String errorMsg) {
                }
          });
```

**Parameters**

| Parameters | Description |
| ---- | ---- |
| homeId   | Family ID, please refer to the family management section for details |
| groupId  | the group is not created, parameter groupId must be an integer -1 |
| productId | Select the pid of the device that created the group |
| meshId | Select the meshId of the device that created the group, deviceBean.getMeshId() |

#### Creating a Group

```java
WiserHomeSdk.newHomeInstance(homeId).createZigbeeGroup(productId, meshId, name, 
        new IWiserResultCallback<CloudZigbeeGroupCreateBean>() {
        
            @Override
            public void onSuccess(CloudZigbeeGroupCreateBean cloudZigbeeGroupCreateBean) {
                long mGroupId = cloudZigbeeGroupCreateBean.getGroupId();
                String mGId = cloudZigbeeGroupCreateBean.getLocalId();
            }
        
            @Override
            public void onError(String errorCode, String errorMsg) {
                
            }
        });
});
```
**Parameters**

| Parameters | Description |
| ---- | ---- |
| homeId          | Family ID, please refer to the family management section for details |
| productId       | the pid of the device what is using to create group|
| name            | a name of the group to be created |
| meshId          | deviceBean.getMeshId() |

#### Add Devices to Group

Add new devices to the group, mainly interact with the firmware, write group devices to the gateway

```java
mIWiserZigbeeGroup.addDeviceToGroup(meshId, selectedDeviceIds, gid, 
        new IWiserResultCallback<ZigbeeGroupCreateResultBean>() {
       
            @Override
            public void onSuccess(ZigbeeGroupCreateResultBean zigbeeGroupCreateResultBean) {
                if (zigbeeGroupCreateResultBean != null) {
                    if (zigbeeGroupCreateResultBean.getSuccess() != null && zigbeeGroupCreateResultBean.getSuccess().size() > 0) {
                        List<String> mAddSuccessDeviceIds = new ArrayList<>();
                        mAddSuccessDeviceIds.addAll(zigbeeGroupCreateResultBean.getSuccess());
                    }
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

**Parameters**

| Parameters | Description |
| ---- | ---- |
| meshId             | Select the gateway id of the device that created the group, (deviceBean.getMeshId())|
| selectedDeviceIds  | the idList of the selected devices |
| gid                | the localId of group（groupBean.getLocalId() or cloudZigbeeGroupCreateBean.getLocalId()) |

#### Delete Devices of Group

Delete existing devices in the group stored in the gateway

```java
mIWiserZigbeeGroup.delDeviceToGroup(meshId, selectedDeviceIds, gid, 
        new IWiserResultCallback<ZigbeeGroupCreateResultBean>() {
        
            @Override
            public void onSuccess(ZigbeeGroupCreateResultBean zigbeeGroupCreateResultBean) {
                if (zigbeeGroupCreateResultBean != null) {
                    if (zigbeeGroupCreateResultBean.getSuccess() != null && zigbeeGroupCreateResultBean.getSuccess().size() > 0) {
                        List<String> mDelSuccessDeviceIds = new ArrayList<>();
                        mDelSuccessDeviceIds.addAll(zigbeeGroupCreateResultBean.getSuccess());
                    }
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
**Parameters**

| Parameters | Description |
| ---- | ---- |
| meshId             | Select the gateway id of the device that created the group, (deviceBean.getMeshId())|
| selectedDeviceIds  | the idList of the selected devices |
| gid                | the localId of group（groupBean.getLocalId() or cloudZigbeeGroupCreateBean.getLocalId()) |

#### Update and Save Group

Save and update the results of the addition and deletion of the gateway firmware group device to the cloud

```java
WiserHomeSdk.newZigbeeGroupInstance(groupId).updateGroupDeviceList(homeId, selectedDeviceIds, 
        new IResultCallback() {
        
            @Override
            public void onError(String s, String s1) {
                
            }
            
            @Override
            public void onSuccess() {
                
            }
        });
```
**Parameters**

| Parameters | Description |
| ---- | ---- |
| groupId            | group id |
| homeId             | Family ID, please refer to the family management section for details |
| selectedDeviceIds  | the ids of the choosed device that to add or del successfully |

## Group Operation

### Instantiation

```java
IWiserGroup mIWiserGroup= WiserHomeSdk.newGroupInstance(groupId);
```

**Parameters**

| Parameters     | Description |
| ---- | ---- |
| groupId         | group id |

### Modifying group name

```java
WiserHomeSdk.newGroupInstance(groupId).renameGroup(titleName, 
            new IResultCallback() {
            
            @Override
            public void onError(String s, String s1) {
            
            }
            
            @Override
            public void onSuccess() {
                
            }
        });
```
**Parameters**

| Parameters | Description |
| ---- | ---- |
| groupId  | group id |
| titleName | group name |

### Dismiss Group

```java
WiserHomeSdk.newGroupInstance(groupId).dismissGroup(new IResultCallback() {
    
            @Override
            public void onError(String s, String s1) {
            
            }
            
            @Override
            public void onSuccess() {
            
            }
        });
```

**Parameters**

| Parameters | Description |
| ---- | ---- |
| groupId  | the id of Group to be disbanded |


### Sending group control command

```java
mWiserGroup.publishDps(String command, IResultCallback listener);
```

**Parameters**

| Parameters | Description |
| ---- | ---- |
| command  | control commands |

**Example**

```java
//Code segment for switching on the light in a group
LampBean bean = new LampBean();
bean.setOpen(true);
HashMap<String, Object> hashMap = new HashMap<>();
hashMap.put(STHEME_LAMP_DPID_1, bean.isOpen());
mWiserGroup.publishDps(JSONObject.toJSONString(hashMap),callback)；
```
**Notes**

The returned result of a command sent from a group means that the command is sent to the cloud successfully, and it does not mean that the device has been actually controlled.

### Group callback event

```java
//Registering group callback event
mIWiserGroup.registerGroupListener(new IGroupListener() {
        
            @Override
            public void onDpUpdate(long l, String s) {
            
            }
            
            @Override
            public void onGroupInfoUpdate(long l) {
            
            }
            
            @Override
            public void onGroupRemoved(long l) {
            
            }
        });

//Cancel group callback event
mIWiserGroup.unRegisterGroupListener();
```

### Group data acquisition

For obtaining the group data, the data cannot be obtained before the initialization of Home (invoking getHomeDetail() or getHomeLocalCache).

```java
//Get customized group data
WiserHomeDataManager.getInstance().getGroupBean(long groupId);

//Get device list under group
WiserHomeDataManager.getInstance().getGroupDeviceList(long groupId);
```

### Group data destruction

```java
//It is recommended to invoke the group data destruction function when exiting the group control page.
mIWiserGroup.onDestroy();
```



