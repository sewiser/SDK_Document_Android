# Home Relationship Management

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

## Get Family List

**Declaration**

```java
void queryHomeList(IWiserGetHomeListCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| callback | Result callback |

**Example**

```java
WiserHomeSdk.getHomeManagerInstance().queryHomeList(new IWiserGetHomeListCallback() {
        @Override
        public void onError(String errorCode, String error) {
            // do something
        }
        @Override
        public void onSuccess(List<HomeBean> homeBeans) {
            // do something
        }
    });
```

## Create family

**Declaration**

```java
void createHome(String name, double lon, double lat, String geoName, List rooms, IWiserHomeResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| name | Family name |
| lon | longitude |
| lat | latitude |
| geoName | Home location name |
| rooms | Room list |
| callback | Result callback |

**Example**

```java
WiserHomeSdk.getHomeManagerInstance().createHome(name, lon, lat, geoName, rooms, new IWiserHomeResultCallback() {
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
## Change of home information
### register or unRegister Listener
Change of registered home information includes:
adding and removing homes, information change, change of shared lists and monitoring of successfully server connection.

**Declaration**
```java
void registerWiserHomeChangeListener(IWiserHomeChangeListener listener);
```
**Parameters**

| Parameters | Description |
| :--- | :--- |
| listener | Monitor |

**Example**
```java
IWiserHomeChangeListener listener = new IWiserHomeChangeListener() {
        @Override
        public void onHomeInvite(long homeId, String homeName) {
            // do something
        }
        @Override
        public void onHomeRemoved(long homeId) {
            // do something
        }
        @Override
        public void onHomeInfoChanged(long homeId) {
            // do something
        }
        @Override
        public void onSharedDeviceList(List<DeviceBean> sharedDeviceList) {
            // do something
        }
        @Override
        public void onSharedGroupList(List<GroupBean> sharedGroupList) {
            // do something
        }
        @Override
        public void onServerConnectSuccess() {
            // do something
        }
        @Override
        public void onHomeAdded(long homeId) {
            // do something
        }
    };
WiserHomeSdk.getHomeManagerInstance().registerWiserHomeChangeListener(listener);
```
### Deregistered the information Change of a home.
**Declaration**
```java
void unRegisterWiserHomeChangeListener(IWiserHomeChangeListener listener)
```
**Parameters**

| Parameters | Description |
| :--- | :--- |
| listener | Monitor |

**Example**
```java
IWiserHomeChangeListener listener = new IWiserHomeChangeListener() {
        @Override
        public void onHomeInvite(long homeId, String homeName) {
            // do something
        }
        @Override
        public void onHomeRemoved(long homeId) {
            // do something
        }
        @Override
        public void onHomeInfoChanged(long homeId) {
            // do something
        }
        @Override
        public void onSharedDeviceList(List<DeviceBean> sharedDeviceList) {
            // do something
        }
        @Override
        public void onSharedGroupList(List<GroupBean> sharedGroupList) {
            // do something
        }
        @Override
        public void onServerConnectSuccess() {
            // do something
        }
        @Override
        public void onHomeAdded(long homeId) {
            // do something
        }
    };
WiserHomeSdk.getHomeManagerInstance().registerWiserHomeChangeListener(listener);
// ...
WiserHomeSdk.getHomeManagerInstance().unRegisterWiserHomeChangeListener(listener);
```
### Callback of MQTT Service Connection Success
**Declaration**

```java
void onServerConnectSuccess()
```
**Example**

```java
IWiserHomeChangeListener listener = new IWiserHomeChangeListener() {
        @Override
        public void onHomeInvite(long homeId, String homeName) {
            // do something
        }
        @Override
        public void onHomeRemoved(long homeId) {
            // do something
        }
        @Override
        public void onHomeInfoChanged(long homeId) {
            // do something
        }
        @Override
        public void onSharedDeviceList(List<DeviceBean> sharedDeviceList) {
            // do something
        }
        @Override
        public void onSharedGroupList(List<GroupBean> sharedGroupList) {
            // do something
        }
        @Override
        public void onServerConnectSuccess() {
            // do something
        }
        @Override
        public void onHomeAdded(long homeId) {
            // do something
        }
    };

WiserHomeSdk.getHomeManagerInstance().registerWiserHomeChangeListener(listener);
// ...
WiserHomeSdk.getHomeManagerInstance().unRegisterWiserHomeChangeListener(listener);
```

# Family Management
## Get Family Details

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

## Update Family Information

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

## Disband Family

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

## Add Room

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

## Remove Room

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
## Sorting Rooms

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
# Family Member Management
## Add Home Member

**Declaration**

The field autoAccept in `MemberWrapperBean` was used to control if the member added should accept the invaitation. If the value was false, the added member shuold call `processInvitation()` and then he/she can join the family.

```java
void addMember(MemberWrapperBean memberWrapperBean, IWiserDataCallback<MemberBean> callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| memberWrapperBean | Member information |

**Example**

```java
WiserHomeSdk.getMemberInstance().addMember(memberWrapperBean, new IWiserDataCallback<MemberBean>() {
        @Override
        public void onError(String errorCode, String errorMessage) {
            // do something
        }
        @Override
        public void onSuccess(MemberBean result) {
            // do something
        }
    });
```

## Delete Home Member

**Declaration**

```java
void removeMember(long memberId, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| memberId | Member ID |

**Example**

```java
WiserHomeSdk.getMemberInstance().removeMember(memberId, new IResultCallback() {
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
## Query the Member List Under Home

**Declaration**

```java
void queryMemberList(long mHomeId, IWiserGetMemberListCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| mHomeId | Family ID |

**Example**

```java
WiserHomeSdk.getMemberInstance().queryMemberList(mHomeId, new IWiserGetMemberListCallback() {
        @Override
        public void onError(String errorCode, String error) {
            // do something
        }
        @Override
        public void onSuccess(List<MemberBean> memberBeans) {
            // do something
        }
    });
```
## Update Member Information

**Declaration**

```java
void updateMember(MemberWrapperBean memberWrapperBean, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| memberWrapperBean | Member information |

**Example**

```java
WiserHomeSdk.getMemberInstance().updateMember(memberWrapperBean, new IResultCallback() {
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
## Accept or Refuse To Join the Family

**Declaration**

```java
void processInvitation(long homeId, boolean action, IResultCallback callBack)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| homeId | Family ID |
| action | Accept \/ reject |

**Example**

```java
WiserHomeSdk.getMemberInstance().processInvitation(homeId, action, new IResultCallback() {
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
## Sort Groups or Devices in Your Home

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
## Log Off Monitoring of Information Changes Below Home

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

# Room Information Management  

**RoomBean**

| Parameters | Type | Description |
| :--- | :--- | :--- |
| roomId | long  | Room id|
| name | String   | Room name|
| deviceList | List &lt;DeviceBean&gt;   | Devices of room |
| groupList | List &lt;GroupBean&gt;  | Groups of room |
| displayOrder | int | Room display order |

## Update Room Name

**Declaration**

```java
void updateRoom(String name, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| name | New room name |

**Example**

```java
WiserHomeSdk.newRoomInstance(10000).updateRoom(name, new IResultCallback() {
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

## Update Room Icon

Room support custom background image,  you can get the room background image url as below after upload successed.

```java
RoomBean roomBean = homeBean.rooms.get(index);
String roomBgImageurl = roomBean.iconUrl;
```

**Declaration**

```java
void updateIcon(File file, IResultCallback callback);
```

**Parameters**

| Parameters | Description |
| ---------- | ----------- |
| file       | Room image  |
| callback   | callback    |

**Example**

```java
WiserHomeSdk.newRoomInstance(10000).updateIcon(file, new IResultCallback() {
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

#### 

## Add Device to a Room

**Declaration**

```java
void addDevice(String devId, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| devId | Device ID |

**Example**

```java
WiserHomeSdk.newRoomInstance(10000).addDevice(devId, new IResultCallback() {
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

## Remove Device from a Room

**Declaration**

```java
void removeDevice(String devId, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| devId | Device ID |

**Example**

```java
WiserHomeSdk.newRoomInstance(10000).removeDevice(devId, new IResultCallback() {
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
## Add Group in a Room

**Declaration**

```java
void addGroup(long groupId, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| groupId | Group ID |

**Example**

```java
WiserHomeSdk.newRoomInstance(10000).addGroup(groupId, new IResultCallback() {
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

## Remove Group in a Room

**Declaration**

```java
void removeGroup(Long groupId, IResultCallback resultCallback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| groupId | Group ID |

**Example**

```java
WiserHomeSdk.newRoomInstance(10000).removeGroup(groupId, new IResultCallback() {
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

## Remove Group or Device From Room

**Declaration**

```java
void moveDevGroupListFromRoom(List list, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| list | Group or device |

**Example**

```java
WiserHomeSdk.newRoomInstance(10000).moveDevGroupListFromRoom(list, new IResultCallback() {
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

## Sort Groups or Devices in a Room

**Declaration**

```java
void sortDevInRoom(List<DeviceAndGroupInRoomBean> list, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| list | Group or device |

**Example**

```java
WiserHomeSdk.newRoomInstance(10000).sortDevInRoom(list, new IResultCallback() {
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

# Home Weather

## Get Home's Weather Simple Summary Parameters

Sush as state of weather(clear, cloudy, rainy, and so on),weather icon.

**Declaration**

```java
void getHomeWeatherSketch(double lon,double lat,IIGetHomeWetherSketchCallBack callback);
```

**Parameters**

| **Parameters** | **Description** |
| -------------- | --------------- |
| lon            | longitude       |
| lat            | latitude        |
| callback       | callback        |

WeatherBean Description

| **Parameters** | **Description**     |
| -------------- | ------------------- |
| condition      | weather description |
| temp           | temperature         |
| iconUrl        | weather icon        |
| inIconUrl      | weather icon        |

**Example**

```java
WiserHomeSdk.newHomeInstance(mHomeId).getHomeWeatherSketch(120.075652,30.306265
  new IIGetHomeWetherSketchCallBack() {
    @Override
    public void onSuccess(WeatherBean result) {
    }
    @Override
    public void onFailure(String errorCode, String errorMsg) {
    }
  });
```

## Get Home's Weather Summary Parameters with More Detail

Such as tempature, humidity, ultraviolet index, air quality.

**Declaration**

```java
void getHomeWeatherDetail(int limit, Map<String,Object> unit, IGetHomeWetherCallBack callback);
```

**Parameters**

| **Parameters** | **Description** |
| :------------- | :-------------- |
| limit          | list count      |
| unit           | parameter unit  |
| callback       | callback        |

More explanations about the unit:

| key      | value                       |
| -------- | --------------------------- |
| tempUnit | Celsius：1<br>Fahrenheit：2 |

For example, when the unit of the data you want to obtain is Celsius unit:

```java
Map<String,Object> units = new HashMap<>();
units.put("tempUnit",1);
```

**Example**

```java
Map<String,Object> units = new HashMap<>();
units.put("tempUnit",1);

WiserHomeSdk.newHomeInstance(mHomeId).getHomeWeatherDetail(10, units, new IGetHomeWetherCallBack() {
    @Override
    public void onSuccess(ArrayList<DashBoardBean> result) {

    }

    @Override
    public void onFailure(String errorCode, String errorMsg) {

    }
});
```
