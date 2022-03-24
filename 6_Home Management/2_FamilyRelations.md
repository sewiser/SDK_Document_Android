# Home Relationship Management
Get the family list, family management, room and equipment management under the family and information monitoring, and so forth.

**HomeBean description**

| Parameters | Type | Description |
| :--- | :--- | :--- |
| name | String | The home name|
| lon | double | The home lon |
| lat | double | The home lat |
| geoName | String | The home location name |
| homeId | long | The home Id |
| admin | boolean | Administrator status |
| rooms | List&lt;RoomBean&gt; | All the rooms|
| deviceList | List&lt;DeviceBean&gt; | All the devices |
| groupList | List&lt;GroupBean&gt; | All the groups |
| meshList | List&lt;BlueMeshBean&gt; |All of the mesh devices |
| sharedDeviceList | List&lt;DeviceBean&gt;|Shared devices received |
| sharedGroupList | List&lt;GroupBean&gt; |Shared groups received |
| homeStatus | int| The home status (1:to be accepted 2:accepted 3:reject) |

## Get the family list

**Description**

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

## Create a family

**Description**

```java
void createHome(String name, double lon, double lat, String geoName, List rooms, IWiserHomeResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| name | Family name (Support up to **25** characters) |
| lon | longitude (Pass **`0`** if you don't set family location information) |
| lat | latitude (Pass **`0`** if you don't set family location information) |
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

## Change the home information

Change of registered home information includes:

inviting home, adding home and removing home, change of home information, change of shared lists, and monitoring of successfully server connection.

**Description**

```java
public interface IWiserHomeChangeListener {
	/**
	* Family added successfully.
	* Used for multi-device data synchronization
	*
	* @param homeId Family ID
	*/
	void onHomeAdded(long homeId);

	/**
	* Family invitation.
	* @param homeId    Family ID
	* @param homeName  Family name
	*/
	void onHomeInvite(long homeId,String homeName);

	/**
	* Family deleted successfully.
	* Used for multi-device data synchronization
	*
	* @param homeId  Family ID
	*/
	void onHomeRemoved(long homeId);

	/**
	* Family information changed.
	* Used for multi-device data synchronization
	*
	* @param homeId  Family ID
	*/
	void onHomeInfoChanged(long homeId);

	/**
	* Shared device list change.
	* Used for multi-device data synchronization
	*
	* @param sharedDeviceList shared device list
	*/
	void onSharedDeviceList(List<DeviceBean> sharedDeviceList);

	/**
	* The mobile phone successfully connects to the Wiser Cloud server and receives this notification.
	* Local data and server data may be inconsistent or the device cannot be controlled,
	* You can call the getHomeDetail interface under Home to reinitialize the data.
	*/
	void onServerConnectSuccess();
}
```

### Register the information change of a home

**Description**

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

### Cancel the information registration of home

**Description**

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

### Callback of MQTT service connection success

**Description**

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

## Get family details

Obtain all data under the family, including equipment, groups, rooms, etc

**Description**

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

### Get family offline details

Obtain all offline data under the family, including equipment, groups, rooms, and more.

**Description**

```java
void getHomeLocalCache(IWiserHomeResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :---- | :---- |
| callback | Callback to get results |

**Example**

```java
WiserHomeSdk.newHomeInstance(10000).getHomeLocalCache(new IWiserHomeResultCallback() {
		@Override
		public void onSuccess(HomeBean bean) {
			// do something
		}
		@Override
		public void onError(String errorCode, String errorMsg) {
			//sdk cache error do not deal
		}
	});
```

### Operate family cached data

`IWiserHomeDataManager` provides the ability to access cached data, the interface entry is `WiserHomeSdk.getDataInstance()`.

**Note**: Before obtaining this data, you should call the family's initialization interface `WiserHomeSdk.newHomeInstance("homeId").getHomeDetail()` or `WiserHomeSdk.newHomeInstance("homeId").getHomeLocalCache()`, then you can get it.

### Update family information

**Description**

```java
void updateHome(String name, double lon, double lat, String geoName, List<String> rooms, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| name | Family name (Support up to **25** characters) |
| lon | Longitude of current family |
| lat | Latitude of the current family |
| geoName | Address of geographical location |
| rooms | Room information |
| callback | Result callback |

**Example**

```java
WiserHomeSdk.newHomeInstance(10000).updateHome(name, lon, lat, geoName, rooms, new IResultCallback() {
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

### Delete home

**Description**

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

### Add room

**Description**

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

### Remove room

**Description**

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

### Sorting rooms

**Description**

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

### Get room information based on devId

**Description**

```java
void getDeviceRoomBean(String devId)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| devId | device ID |

**Example**

```java
WiserHomeSdk.getDataInstance().getDeviceRoomBean(devId);
```
## Family member management

### Add home member

**Description**

The field autoAccept in `MemberWrapperBean` was used to control if the member added should accept the invitation. If the value was false, the added member should call `processInvitation()`, and then he/she can join the family.

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

### Delete home member

**Description**

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

### Query the member list under home

**Description**

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

### Update member information

**Description**

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

### Get the invitation code to add a family member

**Description**

```java
void getInvitationMessage(long homeId, IWiserDataCallback callback)
```

**Parameters**

| Parameters | Description |
| ---- | ---- |
| homeId | Family ID |

**Example**

```java
WiserHomeSdk.getMemberInstance().getInvitationMessage(homeId, new IWiserDataCallback<InviteMessageBean>() {
			@Override
			public void onSuccess(InviteMessageBean result) {
				// onSuc
			}

			@Override
			public void onError(String errorCode, String errorMessage) {
				// onErr
			}
		});
```

### Withdraw family invitation

**Description**

```java
void cancelMemberInvitationCode(long invitationId, IResultCallback callBack)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| invitationId | Invitation ID |

**Example**

```java
WiserHomeSdk.getMemberInstance().cancelMemberInvitationCode(invitationId, new IResultCallback() {
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

### Accept or refuse to join the family

**Description**

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

### Get the record of invited members

**Description**

```java
void getInvitationList(long homeId, IWiserDataCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| homeId | Family ID |

**Example**

```java
WiserHomeSdk.getMemberInstance().getInvitationList(homeId, new IWiserDataCallback() {
		@Override
		public void onSuccess(List<InvitedMemberBean> memberBeans) {
			// do something
		}
		@Override
		public void onError(String errorCode, String error) {
			// do something
		}
	});
```

### Update information of invited member

**Description**

```java
void updateInvitedMember(long invitationId, String memberName, int memberRole, IResultCallback callBack)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| invitationId | Invitation ID |
| memberName | Remark name of invited member |
| memberRole | Role of invited member |

**Example**

```java
WiserHomeSdk.getMemberInstance().updateInvitedMember(invitationId, memberName, membeRole, new IResultCallback() {
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

### Sort groups or devices in the home

**Description**

```java
void sortDevInHome(String homeId, List<DeviceAndGroupInHomeBean> list, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| homeId | Home ID |
| list | Room or group list. The list element DeviceAndGroupInHomeBean here contains two fields. The one is `bizType`, which is the target type to sort. You can refer to BizParentTypeEnum for details. Another is `bizId`, which is the ID of the target, for example, group id or device id. |
| callback | result callback |

Meanings of the enum BizParentTypeEnum:

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
for (DeviceBean bean: deviceList) {
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

### Log off monitoring of information changes below the home

**Description**

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

## Room information management

**RoomBean**

| Parameters | Type | Description |
| :--- | :--- | :--- |
| roomId | long | Room id|
| name | String | Room name|
| deviceList | List &lt;DeviceBean&gt; | Devices of room |
| groupList | List &lt;GroupBean&gt; | Groups of room |
| displayOrder | int | Room display order |

### Update room name

**Description**

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

### Update room icon

Room support custom background image,  you can get the room background image URL as below after upload succeeded. (This method is new in version 3.19)

```java
RoomBean roomBean = homeBean.rooms.get(index);
String roomBgImageurl = roomBean.iconUrl;
```

**Description**

```java
void updateIcon(File file, IResultCallback callback);
```

**Parameters**

| Parameters | Description |
| ---- | ---- |
| file | Room image |
| callback | callback |

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

### Add device to a room

**Description**

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

### Remove a device from a room

**Description**

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

### Add group in a room

**Description**

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

### Remove group in a room

**Description**

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

### Remove group or device from room

**Description**

This method can be used to move devices and groups into or out of the room in batches.

```java
void moveDevGroupListFromRoom(List list, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| list | Group or device |

The data format of **DeviceAndGroupInRoomBean** is as follows:

| Parameters | Type | Description |
| ---- | ---- | ---- |
| id | String | Device or group ID |
| type | int | Type ( device type returns **6**, group type returns **5** ) |

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

### Sort groups or devices in a room

**Description**

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

### Query room info by devId

**Description**

```java
RoomBean getDeviceRoomBean(String devId);
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| devId | device Id|

**Example**

```java
WiserHomeSdk.getDataInstance().getDeviceRoomBean(String devId);
```

### Query room info by groupId

**Description**

```java
RoomBean getGroupRoomBean(String devId);
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| groupId | groupd Id|

**Example**

```java
WiserHomeSdk.getDataInstance().getGroupRoomBean(long groupId);
```

## Home weather

### Get home's weather simple summary parameters

Such as the state of weather(clear, cloudy, rainy, and so on), weather icon.

**Description**

```java
void getHomeWeatherSketch(double lon,double lat,IIGetHomeWetherSketchCallBack callback);
```

**Parameters**

| **Parameters** | **Description** |
| ---- | ---- |
| lon | longitude |
| lat | latitude |
| callback | callback |

WeatherBean Description

| **Parameters** | **Description** |
| ---- | ---- |
| condition | weather description |
| temp | temperature |
| iconUrl | weather icon |
| inIconUrl | weather icon |

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

### Get home's weather summary parameters with more detail

Such as temperature, humidity, ultraviolet index, air quality.

**Description**

```java
void getHomeWeatherDetail(int limit, Map<String,Object> unit, IGetHomeWetherCallBack callback);
```

**Parameters**

| **Parameters** | **Description** |
| :---- | :---- |
| limit | list count |
| unit | parameter unit |
| callback | callback |

More explanations about the unit:

| key | value |
| ---- | ---- |
| tempUnit | Celsius: 1<br>Fahrenheit: 2 |

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