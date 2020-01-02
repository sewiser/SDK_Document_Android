## Home Management Class

The IWiserHomeManager provides changes related to creating home, obtaining the home list and monitoring home, and it can be obtained by invoking the `WiserHomeSdk.getHomeManagerInstance()`.

## HomeBean Field Information
| field | type | describe |
| --- | --- | --- |
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

## Create Home

```java
    /**
    *
    * @param name     Name of home
    * @param lon      Longitude
    * @param lat      Latitude
    * @param geoName  Name of geographic position
    * @param rooms    Room list
    * @param callback
    */
    
    void createHome(String name, double lon, double lat, String geoName, List<String> rooms, IWiserHomeResultCallback callback);
```

## Obtain Home List
```java
    /**
    *
    * @param callback
    */
    
    void queryHomeList(IWiserGetHomeListCallback callback);
```

## Change of home information
1.register or unRegister Listener
```java
    /**
    * Change of registered home information includes:
    * adding and removing homes, information change, change of shared lists and monitoring of successfully server connection.
    *
    * @param listener
    */
    
    void registerWiserHomeChangeListener(IWiserHomeChangeListener listener);
    
    /**
    * Deregistered the information Change of a home.
    *
    * @param listener
    */
    void unRegisterWiserHomeChangeListener(IWiserHomeChangeListener listener);
```


2.list of events
```java
public interface IWiserHomeChangeListener {
    /**
    * Adding home succeeds Used for data synchronization of multiple devices
    *
    * @param homeId
    */
    void onHomeAdded(long homeId);
   
    /**
     * Receive the family invitation 
     * @param homeId    
     * @param homeName  
     */
    void onHomeInvite(long homeId,String homeName);

    /**
    * Removing home succeeds Used for data decarbonization of multiple devices
    *
    * @param homeId
    */
    void onHomeRemoved(long homeId);
    /**
    * Change of home information
    Used for data decarbonization of multiple devices
    *
    * @param homeId
    */
    void onHomeInfoChanged(long homeId);
    /**
    * Release the change of device list Used for data decarbonization of multiple devices
    *
    * @param sharedDeviceList
    */
    void onSharedDeviceList(List<DeviceBean> sharedDeviceList);
    /**
    *
    * The mobile phone has been connected successfully to the Wiser Cloud Server. Special attention shall be paid to this message. In some cases, the local data may be inconsistent with the data of servers, the getHomeDetail interface of Home can be invoked to update data. 
    *
    */
    void onServerConnectSuccess();
    }
```

## Operate Cache Data of a Home
**Attention**: Before obtaining the cache data, the initiation interface of home, WiserHomeSdk.newHomeInstance("homeId").getHomeDetail() or WiserHomeSdk.newHomeInstance("homeId").getHomeLocalCache shall be invoked first.
Interface entry:`WiserHomeSdk.getDataInstance()`


```java

    /**
     * Devices, groups and room list of a home
     *
     * @param homeId 
     * @return List<RoomBean>
     */
    List<RoomBean> getHomeRoomList(long homeId);

    /**
     * Obtain the device list of a home.
     *
     * @param homeId 
     * @return List<DeviceBean>
     */
    List<DeviceBean> getHomeDeviceList(long homeId);

    /**
     * Obtain the group list of a home.
     *
     * @param homeId 
     * @return List<DeviceBean>
     */
    List<GroupBean> getHomeGroupList(long homeId);

    /**
     * Obtain group
     *
     * @param groupId 
     * @return GroupBean
     */
    GroupBean getGroupBean(long groupId);

    /**
     * Obtain device
     *
     * @param devId 
     * @return DeviceBean
     */
    DeviceBean getDeviceBean(String devId);

    /**
     * Obtain room according to the group ID
     *
     * @param groupId 
     * @return RoomBean
     */
    RoomBean getGroupRoomBean(long groupId);

    /**
     * Obtain room
     *
     * @param roomId 
     * @return RoomBean
     */
    RoomBean getRoomBean(long roomId);

    /**
     * Obtain room information based on devices
     *
     * @param devId 
     * @return RoomBean
     */
    RoomBean getDeviceRoomBean(String devId);

    /**
     * Obtain device list of a group
     *
     * @param groupId 
     * @return List<DeviceBean>
     */
    List<DeviceBean> getGroupDeviceList(long groupId);

    /**
     * Obtain the group list of a mesh
     *
     * @param meshId meshId
     * @return List<GroupBean>
     */
    List<GroupBean> getMeshGroupList(String meshId);

    /**
     * Obtain the device list of a mesh
     * @param meshId 
     * @return List<DeviceBean>
     */
    List<DeviceBean> getMeshDeviceList(String meshId);

    /**
     * Obtain the following device list of a room according to the room ID.
     *
     * @param roomId 
     * @return List<DeviceBean>
     */
    List<DeviceBean> getRoomDeviceList(long roomId);

    /**
     * Obtain the following group list of a room according to the room ID.
     *
     * @param roomId room id
     * @return List<GroupBean>
     */
    List<GroupBean> getRoomGroupList(long roomId);

    /**
     * Obtain the data of home.
     *
     * @param homeId homeId
     * @return HomeBean
     */
    HomeBean getHomeBean(long homeId);

```
