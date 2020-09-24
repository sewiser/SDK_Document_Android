### Family Management

Get the family list, family management, room and equipment management under the family and information monitoring, etc.

**HomeBean description**

| Parameters | Type | Description |
| :--- | :--- | :--- |
| name | String  | The home name|
| lon | double   | The home lon |
| lat | double | The home lat |
| geoName | String | The home location name |
| homeId | long | The home Id |
| admin | boolean  | Administrator status |
| rooms | List&lt;RoomBean&gt; | All the rooms|
| deviceList | List&lt;DeviceBean&gt;  | All the devices |
| groupList | List&lt;GroupBean&gt; | All the groups |
| meshList | List&lt;BlueMeshBean&gt; |All of the mesh devices |
| sharedDeviceList | List&lt;DeviceBean&gt;|Shared devices received |
| sharedGroupList | List&lt;GroupBean&gt; |Shared groups received |
| homeStatus | int| The home status （1:to be accepted 2:accepted 3:reject）|

#### Get Data Information in Local Cache

**Declaration**

Get home data from local cache. If you hasn't request for home info before, it will return a empty HomeBean object.

```java
void getHomeLocalCache(IWiserHomeResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| callback | Callback to get results |

**Example**

```java
WiserHomeSdk.newHomeInstance(10000).getHomeLocalCache(new IWiserHomeResultCallback() {
        @Override
        public void onError(String errorCode, String errorMsg) {
            // do something
        }
        @Override
        public void onSuccess(HomeBean bean) {
            // do something
        }
    });
```

#### Update Family Information

**Declaration**

```java
void updateHome(String name, double lon, double lat, String geoName, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| name | Family name |
| lon | Longitude of current family |
| lat | Latitude of the current family |
| geoName | Address of geographical location |
| callback | Result callback |

**Example**

```java
WiserHomeSdk.newHomeInstance(10000).updateHome(name, lon, lat, geoName, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### Family Sort

**Declaration**

```java
void sortHome(List idList, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| idList | Family ID list |
| callback | Result callback |

**Example**

```java
WiserHomeSdk.newHomeInstance(10000).sortHome(idList, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### Get Family Details

Obtain all data under the family, including equipment, groups, rooms, etc

**Declaration**

```java
void getHomeDetail(IWiserHomeResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| callback | Callback to get results |

**Example**

```java
WiserHomeSdk.newHomeInstance(10000).getHomeDetail(new IWiserHomeResultCallback() {
        @Override
        public void onError(String errorCode, String errorMsg) {
            // do something
        }
        @Override
        public void onSuccess(HomeBean bean) {
            // do something
        }
    });
```

#### Disband Family

**Declaration**

```java
void dismissHome(IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| callback | Result callback |

**Example**

```java
WiserHomeSdk.newHomeInstance(10000).dismissHome(new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### Add Room

**Declaration**

```java
void addRoom(String name, IWiserRoomResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| name | Room name |
| callback | Result callback |

**Example**

```java
WiserHomeSdk.newHomeInstance(10000).addRoom(name, new IWiserRoomResultCallback() {
        @Override
        public void onError(String errorCode, String errorMsg) {
            // do something
        }
        @Override
        public void onSuccess(RoomBean bean) {
            // do something
        }
    });
```

#### Remove Room

**Declaration**

```java
void removeRoom(long roomId, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| roomId | Room ID |
| callback | Result callback |

**Example**

```java
WiserHomeSdk.newHomeInstance(10000).removeRoom(roomId, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### Sorting Rooms

**Declaration**

```java
void sortRoom(List<Long> idList, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| idList | Room ID list |
| callback | Result callback |

**Example**

```java
WiserHomeSdk.newHomeInstance(10000).sortRoom(idList, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### Query Room List

**Declaration**

```java
void queryRoomList(IWiserGetRoomListCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| callback | Result callback |

**Example**

```java
WiserHomeSdk.newHomeInstance(10000).queryRoomList(new IWiserGetRoomListCallback() {
        @Override
        public void onError(String errorCode, String error) {
            // do something
        }
        @Override
        public void onSuccess(List<RoomBean> romeBeans) {
            // do something
        }
    });
```

#### Get Home Instance Information

**Declaration**

```java
HomeBean getHomeBean()
```

**Example**

```java
WiserHomeSdk.newHomeInstance(10000).getHomeBean();
```

#### Create Group

**Declaration**

```java
void createGroup(String productId, String name, List<String> devIdList, IWiserResultCallback<Long> callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| productId | Product ID |
| name | group name |
| devIdList | Device ID list |
| callback | Result callback |

**Example**

```java
WiserHomeSdk.newHomeInstance(10000).createGroup(productId, name, devIdList, new IWiserResultCallback() {
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
        @Override
        public void onSuccess(Object result) {
            // do something
        }
    });
```

#### Query Room Information According To Equipment

**Declaration**

```java
List<RoomBean> queryRoomInfoByDevice(List<DeviceBean> deviceList)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| deviceList | Device list |

**Example**

```java
WiserHomeSdk.newHomeInstance(10000).queryRoomInfoByDevice(deviceList);
```

#### Monitor the Change of Information in the Home

**Declaration**

```java
void registerHomeStatusListener(IWiserHomeStatusListener listener)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| listener | Monitor |

**Example**

```java
// define a listener
IWiserHomeStatusListener listener = new IWiserHomeStatusListener() {
        @Override
        public void onDeviceAdded(String devId) {
            // do something
        }
        @Override
        public void onDeviceRemoved(String devId) {
            // do something
        }
        @Override
        public void onGroupAdded(long groupId) {
            // do something
        }
        @Override
        public void onGroupRemoved(long groupId) {
            // do something
        }
        @Override
        public void onMeshAdded(String meshId) {
            // do something
        }
    };
// register a listener somewhere
WiserHomeSdk.newHomeInstance(10000).registerHomeStatusListener(listener);
```

#### Log Off Monitoring of Information Changes Below Home

**Declaration**

```java
void unRegisterHomeStatusListener(IWiserHomeStatusListener listener)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| listener | Monitor |

**Example**

```java
// define a listener
IWiserHomeStatusListener listener = new IWiserHomeStatusListener() {
        @Override
        public void onDeviceAdded(String devId) {
            // do something
        }
        @Override
        public void onDeviceRemoved(String devId) {
            // do something
        }
        @Override
        public void onGroupAdded(long groupId) {
            // do something
        }
        @Override
        public void onGroupRemoved(long groupId) {
            // do something
        }
        @Override
        public void onMeshAdded(String meshId) {
            // do something
        }
    };
// register a listener somewhere
WiserHomeSdk.newHomeInstance(10000).registerHomeStatusListener(listener);
// ...
// unregister a listener
WiserHomeSdk.newHomeInstance(10000).unRegisterHomeStatusListener(listener);
```

#### Monitor the Change of Device Information Under the Home

**Declaration**

```java
void registerHomeDeviceStatusListener(IWiserHomeDeviceStatusListener listener)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| listener | Monitor |

**Example**

```java
// define a listener
IWiserHomeDeviceStatusListener listener = new IWiserHomeDeviceStatusListener() {
        @Override
        public void onDeviceDpUpdate(String devId, String dpStr) {
            // do something
        }
        @Override
        public void onDeviceStatusChanged(String devId, boolean online) {
            // do something
        }
        @Override
        public void onDeviceInfoUpdate(String devId) {
            // do something
        }
    };
// register a listener somewhere
WiserHomeSdk.newHomeInstance(10000).registerHomeDeviceStatusListener(listener);
```

#### Log Off Monitoring of Device Information Changes Under Home

**Declaration**

```java
void unRegisterHomeDeviceStatusListener(IWiserHomeDeviceStatusListener listener)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| listener | Monitor |

**Example**

```java
// define a listener
IWiserHomeDeviceStatusListener listener = new IWiserHomeDeviceStatusListener() {
        @Override
        public void onDeviceDpUpdate(String devId, String dpStr) {
            // do something
        }
        @Override
        public void onDeviceStatusChanged(String devId, boolean online) {
            // do something
        }
        @Override
        public void onDeviceInfoUpdate(String devId) {
            // do something
        }
    };
// register a listener somewhere
WiserHomeSdk.newHomeInstance(10000).registerHomeDeviceStatusListener(listener);
// ...
// unregister a listener
WiserHomeSdk.newHomeInstance(10000).unRegisterHomeDeviceStatusListener(listener);
```

#### Create Bluetooth Mesh

**Declaration**

```java
void createBlueMesh(String meshName, IWiserResultCallback<BlueMeshBean> callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| meshName | Mesh name |
| callback | Result callback |

**Example**

```java
WiserHomeSdk.newHomeInstance(10000).createBlueMesh(meshName, new IWiserResultCallback() {
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
        @Override
        public void onSuccess(BlueMeshBean result) {
            // do something
        }
    });
```

#### Create Bluetooth SIG Mesh

**Declaration**

```java
void createSigMesh(IWiserResultCallback<SigMeshBean> callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| callback | Result callback |

**Example**

```java
WiserHomeSdk.newHomeInstance(10000).createSigMesh(new IWiserResultCallback() {
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
        @Override
        public void onSuccess(SigMeshBean result) {
            // do something
        }
    });
```

#### Query the List of Devices Added To the Group

**Declaration**

```java
void queryDeviceListToAddGroup(long groupId, String productId, IWiserResultCallback<List<GroupDeviceBean>> callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| groupId | Group ID |
| productId | Product ID |
| callback | Result callback |

**Example**

```java
WiserHomeSdk.newHomeInstance(10000).queryDeviceListToAddGroup(groupId, productId, new IWiserResultCallback<List<GroupDeviceBean>>() {
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
        @Override
        public void onSuccess(List<GroupDeviceBean> result) {
            // do something
        }
    });
```

#### Query ZigBee Device List Added To Group

**Declaration**

```java
void queryZigbeeDeviceListToAddGroup(long groupId, String productId, String parentId, IWiserResultCallback<List<GroupDeviceBean>> callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| groupId | Group ID |
| productId | Product ID |
| parentId | mesh id |
| callback | Result callback |

**Example**

```java
WiserHomeSdk.newHomeInstance(10000).queryZigbeeDeviceListToAddGroup(groupId, productId, parentId, new IWiserResultCallback<List<GroupDeviceBean>>() {
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
        @Override
        public void onSuccess(<List<GroupDeviceBean>> result) {
            // do something
        }
    });
```

#### Destruction

**Declaration**

```java
void onDestroy()
```

**Example**

```java
WiserHomeSdk.newHomeInstance(10000).onDestroy();
```

#### Create ZigBee Group

**Declaration**

```java
void createZigbeeGroup(String productId, String parentId, int parentType, String name, IWiserResultCallback<CloudZigbeeGroupCreateBean> callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| productId | Product Id |
| parentId | Parent node ID |
| parentType | Parent node type |
| name | group name |
| callback | Result callback |

**Example**

```java
WiserHomeSdk.newHomeInstance(10000).createZigbeeGroup(productId, parentId, parentType, name, new IWiserResultCallback<CloudZigbeeGroupCreateBean>() {
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
        @Override
        public void onSuccess(CloudZigbeeGroupCreateBean result) {
            // do something
        }
    });
```

#### Use Groups To Query Room Information

**Declaration**

```java
List<RoomBean> queryRoomInfoByGroup(List<GroupBean> groupList)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| groupList | Group list |

**Example**

```java
WiserHomeSdk.newHomeInstance(10000).queryRoomInfoByGroup(groupList);
```

#### Bind New Device

**Declaration**

```java
void bindNewConfigDevs(List<String> devIds, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| devIds | Device ID list |
| callback | Result callback |

**Example**

```java
WiserHomeSdk.newHomeInstance(10000).bindNewConfigDevs(devIds, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### Registered Product Alarm Monitoring

**Declaration**

```java
void registerProductWarnListener(IWarningMsgListener listener)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| listener | Monitor |

**Example**

```java
// define a listener
IWarningMsgListener listener = new IWarningMsgListener() {
        @Override
        public void onWarnMessageArrived(WarnMessageBean warnMessageBean) {
            // do something
        }
    };
// register a listener somewhere
WiserHomeSdk.newHomeInstance(10000).registerProductWarnListener(listener);
```

#### Unregister Product Alarm Monitoring

**Declaration**

```java
void unRegisterProductWarnListener(IWarningMsgListener listener)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| listener | Monitor |

**Example**

```java
// define a listener
IWarningMsgListener listener = new IWarningMsgListener() {
        @Override
        public void onWarnMessageArrived(WarnMessageBean warnMessageBean) {
            // do something
        }
    };
// register a listener somewhere
WiserHomeSdk.newHomeInstance(10000).registerProductWarnListener(listener);
// ...
// unregister a listener
WiserHomeSdk.newHomeInstance(10000).unRegisterProductWarnListener(listener);
```

#### Sort Groups or Devices in Your Home

**Declaration**

```java
void sortDevInHome(String homeId, List<DeviceAndGroupInHomeBean> list, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| homeId | Room ID |
| list | Room or group liist. The list element DeviceAndGroupInHomeBean here contains two fields. The one is `bizType`, which is the target type to sort. You can refer to BizParentTypeEnum for details. Another is `bizId`, which is the id of target, for example, group id or device id. |
| callback | result callback |

Meanings of the enum BizParentTypeEnum：

- LOCATION
- MESH
- ROOM
- GROUP
- DEVICE

**Example**

```java
List<DeviceAndGroupInHomeBean> list = new ArrayList<>();
List<DeviceBean> deviceList = homeBean.getDeviceList();
List<GroupBean> groupList = homeBean.getGroupList();
for (GroupBean bean : groupList) {
    DeviceAndGroupInHomeBean deviceInRoomBean = new DeviceAndGroupInHomeBean();
    deviceInRoomBean.setBizId(bean.getDevId());
    deviceInRoomBean.setBizType(BizParentTypeEnum.GROUP.getType());
    list.add(deviceInRoomBean);
}
for (DeviceBean bean : deviceList) {
    DeviceAndGroupInHomeBean deviceInRoomBean = new DeviceAndGroupInHomeBean();
    deviceInRoomBean.setBizId(bean.getDevId());
    deviceInRoomBean.setBizType(BizParentTypeEnum.DEVICE.getType());
    list.add();
}
WiserHomeSdk.newHomeInstance(10000).sortDevInHome(homeId, list, new IResultCallback() {
        @Override
        public void onSuccess() {
            // do something
        }
        @Override
        public void onError(String code, String error) {
            // do something
        }
    });
```

#### Update Family Information

**Declaration**

```java
void updateHome(String name, double lon, double lat, String geoName, List rooms, boolean overWriteRoom, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| name | Family name |
| lon | Longitude of current family |
| lat | Latitude of the current family |
| geoName | Address of geographical location |
| rooms | Room information |
| overWriteRoom | Whether to overwrite the existing room |
| callback | Result callback |

**Example**

```java
WiserHomeSdk.newHomeInstance(10000).updateHome(name, lon, lat, geoName, rooms, overWriteRoom, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### Create ZigBee Group

**Declaration**

```java
void createZigbeeGroup(String productId, String parentId, String name, IWiserResultCallback<CloudZigbeeGroupCreateBean> callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| productId | Product Id |
| parentId | Parent node ID |
| name | group name |
| callback | Result callback |

**Example**

```java
WiserHomeSdk.newHomeInstance(10000).createZigbeeGroup(productId, parentId, name, new IWiserResultCallback<CloudZigbeeGroupCreateBean>() {
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
        @Override
        public void onSuccess(CloudZigbeeGroupCreateBean result) {
            // do something
        }
    });
```

#### Register Upgrade Status Listener

**Declaration**

```java
void registerUpgradeStatusListener(IWiserDeviceUpgradeStatusCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| callback | Result callback |

**Example**

```java
WiserHomeSdk.newHomeInstance(10000).registerUpgradeStatusListener(new IWiserDeviceUpgradeStatusCallback() {
        @Override
        public void onStatusUpgrade(String devId, UpgradeStatusEnum upgradeStatusEnum) {
            // do something
        }
    });
```



