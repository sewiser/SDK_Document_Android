## Room Management Class

The IWiserRoom provides the room management class, and adding devices, removing devices or groups are handled in this class. The `WiserHomeSdk.newRoomInstance("roomId") `can be used to build the room management class. 

#### RoomBean Field Information:
| field | type | describe |
| --- | --- | --- |
| roomId | long  | The id of the room|
| name | String   | The name of the room|
| deviceList | List &lt;DeviceBean&gt;  |The devices in the room|
| groupList | List &lt;GroupBean&gt;  | The groups in the room|
| displayOrder | int | Room order|

#### Interface Manifest:
```java
/**
* Update room name 
*
* @param name     New name of room
* @param callback
*/
void updateRoom(String name, IResultCallback callback);
/**
* Add device
*
* @param devId
* @param callback
*/
void addDevice(String devId, IResultCallback callback);

/**
* Add group
*
* @param groupId
* @param callback
*/
void addGroup(long groupId, IResultCallback callback);
/**
* Remove device
*
* @param devId
* @param callback
*/
void removeDevice(String devId, IResultCallback callback);
/**
* Remove group
*
* @param groupId
* @param resultCallback
*/
void removeGroup(Long groupId, IResultCallback resultCallback);

/**
* Remove groups or devices from a room.
* @param list
* @param callback
*/
void moveDevGroupListFromRoom(List<DeviceAndGroupInRoomBean> list, IResultCallback callback);

/**
* Sort groups or devices in a room.
* @param list
* @param callback
*/
void sortDevInRoom(List<DeviceAndGroupInRoomBean> list, IResultCallback callback);
```
