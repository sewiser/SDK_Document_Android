# Bluetooth Mesh (SIG)
Wiser Bluetooth has 3 technology lines.

- **SingleBLE**: Bluetooth single point device, one-to-one connection between Bluetooth device and phone;
- **WiserMesh**: Mesh released by Wiser.
- **SigMesh**: Mesh released by SIG (Bluetooth Special Interest Group).
In addition to the above three, there are some multi-protocol devices, such as **Dual-mode Device** with Wi-Fi and BLE capabilities. You can use both BLE and Wi-Fi capabilities.

|Category | Product Examples |
| ----------- | -----------------  |
| SingleBLE     | Body fat scale, bracelet, electric toothbrush, door lock, etc. |
| SigMesh     | Light bulb, socket, sensor,etc.|
| WiserMesh    | Light bulb, socket, sensor,etc.|
| Dual-mode Device | Sigmesh gateways, IPC devices, and new multi-protocol Wi-Fi devices are all possible |
> Dual-mode's Bluetooth distribution network part, Use SingleBLE technology to network the device, Will be explained in the SingleBLE chapter.

#### Tips

Please familiar with WiserHomeSdk first and develop Bluetooth Mesh. All operations of Mesh are based on the initialization of family data.
A family can has multiple Meshs (recommend one family create one).

## Prepare

**Mobile System Requirements**

WiserHomesdk has been supported since Android 4.4.   API>=19

**Manifest Permissions**

```java
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
```

**Permissions  Check**

  *  Before the APP uses the Bluetooth connection or scanning operation, it needs to check whether the APP positioning permission is allowed.
  *  Check if the Bluetooth status is on.

## Basic Notion
|Basic Notion|Description|
|--|--|
|pcc|Each mesh device corresponds to a product, and each product has its own size class label. The SDK uses pcc andtype as the size class label.|
|mesh node Id |	The node id is used to distinguish the "unique identifier" of each mesh device in the mesh network. For example, if you want to control a device, you can send the nodeId command corresponding to this device to the mesh network|
|mesh group local Id|	The local Id is used to distinguish the `unique identifier` of each mesh group in the mesh network.For example, if you want to control the devices in a group, you can send the localId command corresponding to this group to the mesh network.|
|Local Connection |	The networked device is connected via Bluetooth to control mesh and command operations|
|Gateway Connection|	The networked devices are connected through the gateway (the gateway needs to be with the device, and the distance cannot be too far) to control the mesh and command operations.|


## Management
Contains MeshId creation, destruction

### Create SIG Mesh

MeshId is created by the cloud. Only one Mesh can be created in a family.

**Declaration**
```java
void createSigMesh(IWiserResultCallback<SigMeshBean> callback);
```

**Example**

```java
WiserHomeSdk.newHomeInstance("homeIdxxxx").createSigMesh(new IWiserResultCallback<SigMeshBean>() {
    @Override
    public void onError(String errorCode, String errorMsg) {
    }

    @Override
    public void onSuccess(SigMeshBean sigMeshBean) {
    }
});
```

### Delete SIG Mesh
Delete SigMesh MeshId

**Declaration**
```java
void removeMesh(IResultCallback callback);
```

**Example**
```java
WiserHomeSdk.newSigMeshDeviceInstance(meshId).removeMesh(new IResultCallback() {
    @Override
    public void onError(String errorCode, String errorMsg) {
    }

    @Override
    public void onSuccess() {
    }
});

```

### Get the List of SIG Mesh in the Family

**Declaration**

```java
List<SigMeshBean> getSigMeshList();
```
**Example**
```java
IWiserHome mWiserHome = WiserHomeSdk.newHomeInstance("homeIdxxxx");
if (mWiserHome.getHomeBean() != null){
	List<SigMeshBean> meshList = WiserHomeSdk.getSigMeshInstance().getSigMeshList()
}
```

### Get Sub-device Data

**Declaration**

```java
 List<DeviceBean> getMeshSubDevList();
```
**Example**
```java
List<DeviceBean> meshSubDevList = WiserHomeSdk.newSigMeshDeviceInstance("meshIdxxxxx").getMeshSubDevList();
```

### SIG Mesh Instance 
It is recommended to destroy the current mesh and re-initialize the mesh when the family switches.

**Declaration**

```java
//init mesh
void initMesh(String meshId);
```
**Example**

```java
//init mesh
WiserHomeSdk.getWiserSigMeshClient().initMesh("meshIdxxxxx");
```

### SIG Mesh Destory

**Declaration**

```java
void destroyMesh();
```

**Example**

```java
WiserHomeSdk.getWiserSigMeshClient().destroyMesh();
```

### SIG Mesh Sub-device Connect and disconnect

`IWiserBlueMeshClient` provides connect, disconnect, scan, stop scan.

**Example**
```java
// start connect
WiserHomeSdk.getWiserSigMeshClient().startClient(mSigMeshBean);
// start connect with timeout
WiserHomeSdk.getWiserSigMeshClient().startClient(mSigMeshBean,searchTime);

//disconnect
WiserHomeSdk.getWiserSigMeshClient().stopClient();

//start scan
WiserHomeSdk.getWiserSigMeshClient().startSearch()

//stop scan
WiserHomeSdk.getWiserSigMeshClient().stopSearch();

```

**Precautions**

 - `startClient(mSigMeshBean)` After calling, it will continuously scan the surrounding connectable devices in the background until the connection is successful.
 - Scanning in the background always consumes resources. You can control background scanning by starting and stopping
 - if not call  `startClient()` , `startSearch()` and  `stopSearch()` is not working
 - When connected to the Mesh network, calling startSearch and stopSearch is not working.

## Activation

### Scaning SIG Mesh Devices
 Keep bluetooth ON and check location permissions before scanning.

**Declaration**

```java
//start scanning
void startSearch();
//stop scanning
void stopSearch();

```

**Example**

```java
IWiserBlueMeshSearchListener iWiserBlueMeshSearchListener=new IWiserBlueMeshSearchListener() {
    @Override
    public void onSearched(SearchDeviceBean deviceBean) {

    }

    @Override
    public void onSearchFinish() {

    }
};
// SigMesh's UUID
UUID[] MESH_PROVISIONING_UUID = {UUID.fromString("00001827-0000-1000-8000-00805f9b34fb")};
SearchBuilder searchBuilder = new SearchBuilder()
								.setServiceUUIDs(MESH_PROVISIONING_UUID)
                .setTimeOut(100)      
                .setWiserBlueMeshSearchListener(iWiserBlueMeshSearchListener).build();

IWiserBlueMeshSearch mMeshSearch = WiserHomeSdk.getWiserBlueMeshConfig().newWiserBlueMeshSearch(searchBuilder);

//start
mMeshSearch.startSearch();

//stop
mMeshSearch.stopSearch();
```

### Active SIG Mesh Device by Bluetooth

Two types of sub-devices Activation, App activation and Mesh gateway activation.

**Declaration**

```java

void startActivator();

void stopActivator();
```
**Example**

```java
WiserSigMeshActivatorBuilder wiserSigMeshActivatorBuilder = new WiserSigMeshActivatorBuilder()
            .setSearchDeviceBeans(mSearchDeviceBeanList)
            .setSigMeshBean(sigMeshBean) 
            .setTimeOut(timeout) 
            .setWiserBlueMeshActivatorListener(new IWiserBlueMeshActivatorListener() {
     @Override
     public void onSuccess(String mac, DeviceBean deviceBean) {
     }
     @Override
     public void onError(String mac, String errorCode, String errorMsg) {
     }
     @Override
     public void onFinish() {
     });

IWiserBlueMeshActivator iWiserBlueMeshActivator = WiserHomeSdk.getWiserBlueMeshConfig().newSigActivator(wiserSigMeshActivatorBuilder);

//start
iWiserBlueMeshActivator.startActivator();
//stop
iWiserBlueMeshActivator.stopActivator();
```

**Parameters**

|field|describe|
|--|--|
|mSearchDeviceBeanList|List of devices to be activated|
|timeout|Activation timeout，default 100s.|
|sigMeshBean|SigMeshBean|

**Data Model**

`DeviceBean` See [DeviceBean Data Model](./Device.md#Device Information Acquisition)

`errorCode` See Error Code

### Active SIG Mesh Gateway Device

See  [ZigBee Sub-devices Activation](./Activator_zigbee_subdevice.md)

### Active SIG Mesh Device by Gateway

SigMesh gateway essentially dual-mode device
1. Activation as a Wi-Fi device. See [Wifi EZ Activation](./Activator_wifi_ez.md)
2. Activation as a BLE device. See [Dual-mode Activation](./BLE_Activator.md#Dual-mode-Device-Activation)

### Error Code

| Code   | MSG                               |
| ------ | --------------------------------- |
| 21002  | invite failed                     |
| 21004  | provision failed                  |
| 21006  | send public key failed            |
| 21008  | conform failed                    |
| 210010 | random conform failed             |
| 210014 | send data failed                  |
| 210016 | composition data failed           |
| 210018 | add appkey failed                 |
| 210020 | bind model failed                 |
| 210022 | publication model failed          |
| 210024 | network transmit failed           |
| 210026 | Cloud registration failed         |
| 210027 | Device address allocation is full |
| 210034 | notify failed                     |
| 20021  | timeout                           |

## Device

`IWiserBlueMeshDevice` provides all operations for Mesh devices.

```java
IWiserBlueMeshDevice  mWiserBlueMeshDevice = WiserHomeSdk.newSigMeshDeviceInstance(meshId);
```

###  Get Device Instance

**Example**

```java
DeviceBean deviceBean=WiserHomeSdk.getDataInstance().getDeviceBean(mDevId);

if(deviceBean.isSigMesh()){
    L.d(TAG, "This device is sigmesh device");
 }

if(deviceBean.isSigMeshWifi()){
    L.d(TAG, "This device is sigmesh wifi device");
 }
```
### Local Connection and Gateway Connection

**Example**

```java
DeviceBean deviceBean=WiserHomeSdk.getDataInstance().getDeviceBean(mDevId);

//online status (Including local online and gateway online)
boolean online=deviceBean.getIsOnline()
//local online
boolean localOnline=deviceBean.getIsLocalOnline()
//gateway online
boolean wifiOnline=deviceBean.isCloudOnline() && gwBean.getIsOnline() 
```

### SIG Mesh Device And Gateway Judgment Method

**Example**

```java
DeviceBean deviceBean=WiserHomeSdk.getDataInstance().getDeviceBean(mDevId);

if(deviceBean.isSigMesh()){
    L.d(TAG, "This device is sigmesh device");
}

if(deviceBean.isSigMeshWifi()){
    L.d(TAG, "This device is sigmesh wifi device");
}
```

###  SIG Mesh Sub-devices Rename

**Declaration**

```java
void renameMeshSubDev(String devId, String name, IResultCallback callback);
```
**Parameters**

|param|describe|
|--|--|
|devId|Device Id|
|name|New name|
|callback|Callback|

**Example**

```java
mWiserBlueMesh.renameMeshSubDev(devBean.getDevId(),"new name", new IResultCallback() {
     @Override
     public void onError(String code, String errorMsg) {
     }

     @Override
     public void onSuccess() {
   }});
```

### Get Device Status

Get dp data from cloud maybe not real-time data, can use it search real-time data and `IMeshDevListener`'s `onDpUpdate` will be callback.

**Declaration**

```java
void querySubDevStatusByLocal(String pcc, final String nodeId, final IResultCallback callback);
```

**Parameters**

|param|describe|
|--|--|
|pcc|Device type|
|nodeId|Device nodeId|
|callback|Callback|

**Example**

```java
mWiserBlueMeshDevice.querySubDevStatusByLocal(devBean.getCategory(), devBean.getNodeId(), new IResultCallback() {
            @Override
            public void onError(String code, String errorMsg) {
            }
            @Override
            public void onSuccess() {
            }
        });
```

###  Remove Device

**Declaration**

```java
void removeMeshSubDev(String devId, IResultCallback callback);
```

**Parameters**

| param    | 说明        |
| -------- | ----------- |
| devId    | Device Id   |
| pcc      | Device type |
| callback | Callback    |

**Example**

```java
mWiserBlueMesh.removeMeshSubDev(devBean.getDevId(),devBean.getCategory(), new IResultCallback() {
            @Override
            public void onError(String code, String errorMsg) {
            }
            @Override
            public void onSuccess() {
            }
        });
```

## Group

`IWiserGroup` provides operations for Mesh group.

### Find Mesh Group

A Mesh group or a WiFi group can be distinguished by whether it has a MeshId.

**Example**

```java
GroupBean groupBean=WiserHomeSdk.getDataInstance().getGroupBean("groupId");
if(!TextUtils.isEmpty(groupBean.getMeshId())){    
	L.d(TAG, "This group is mesh group");
}
```

### Add Group

16128 groups can be created in a mesh network. The id range when returning is 0xC000-0xFEFF . It is maintained locally.

Declaration

```java
void addGroup(String name, String pcc, String localId,IAddGroupCallback callback);
```
Parameters

|param|describe|
|--|--|
|name|group name|
|pcc|device type|
|localId|LocalId (0xC000 - 0xFFFF)|
|callback|Callback|

Example

```java
IWiserBlueMeshDevice mWiserSigMeshDevice= WiserHomeSdk.newSigMeshDeviceInstance("meshId");

mWiserSigMeshDevice.addGroup("group name","pcc", "8001", new IAddGroupCallback() {
			@Override
     public void onError(String errorCode, String errorMsg) {
     }

     @Override
     public void onSuccess(long groupId) {
     }
     });
```



### Add Device to Group

**Declaration**

```java
void addDevice(String devId,IResultCallback callback);
```
**Parameters**

|param|describe|
|--|--|
|devId|device Id|
|callback|callback|

**Example**

```java
IWiserGroup mGroup = WiserHomeSdk.newSigMeshGroupInstance(groupId);
mGroup.addDevice("devId", new IResultCallback() {
            @Override
            public void onError(String code, String errorMsg) {
            }

            @Override
            public void onSuccess() {
            }
        });
```


### Remove Device From Group

**Declaration**

```java
void removeDevice(String devId,IResultCallback callback);
```
**Parameters**

|param|describe|
|--|--|
|devId|Device Id|
|callback|Callback|

**Example**
```java
IWiserGroup mGroup = WiserHomeSdk.newSigMeshGroupInstance(groupId);
mGroup.removeDevice("devId", new IResultCallback() {
            @Override
            public void onError(String code, String errorMsg) {
            }
            @Override
            public void onSuccess() {
            }
        });

```

### Disband Group

**Declaration**

```java
void dismissGroup(IResultCallback callback);
```
**Parameters**

|param|describe|
|--|--|
|callback|Callback|

**Example**
```java
IWiserGroup mGroup = WiserHomeSdk.newSigMeshGroupInstance(groupId);
mGroup.dismissGroup(new IResultCallback() {
            @Override
            public void onError(String code, String errorMsg) {
            }

            @Override
            public void onSuccess() {
            }
        });

```


### Group Rename

**Declaration**

```java
void renameGroup(String groupName,IResultCallback callback);
```

**Parameters**

|param|describe|
|--|--|
|groupName|new name|
|callback|Callback|

**Example**

```java
IWiserGroup mGroup = WiserHomeSdk.newSigMeshGroupInstance(groupId);
mGroup.renameGroup("group name",new IResultCallback() {
            @Override
            public void onError(String code, String errorMsg) {
            }

            @Override
            public void onSuccess() {
            }
        });

```

## Control
`IWiserBlueMeshDevice` provides operations for Mesh devices.

###  Control Command - Control Devices

Format： 
```java
{"(dpId)":"(dpValue)"}  
```

**Declaration**

```java
void publishDps(String nodeId, String pcc, String dps, IResultCallback callback);
```

**Parameters**

|param|describe|
|--|--|
|nodeId|Sub-devices No.|
|pcc|Devices type|
|dps|dps|
|callback|Callback|

**Example**

```java
String dps = {"1":false};
IWiserBlueMeshDevice mWiserSigMeshDevice=WiserHomeSdk.newSigMeshDeviceInstance("meshId");
mWiserSigMeshDevice.publishDps(devBean.getNodeId(), devBean.getCategory(), dps, new IResultCallback() {
            @Override
            public void onError(String s, String s1) {
            }

            @Override
            public void onSuccess() {
            }
        });
```

###  Control Command - Control Group

**Declaration**

```java
void multicastDps(String localId, String pcc, String dps, IResultCallback callback)
```

**Parameters**

|param|describe|
|--|--|
|localId|Group No.|
|pcc|Device type|
|dps|dps|
|callback|Callback|

**Example**

```java      
String dps = {"1":false};
IWiserBlueMeshDevice mWiserSigMeshDevice= WiserHomeSdk.newSigMeshDeviceInstance("meshId");
mWiserSigMeshDevice.multicastDps(groupBean.getLocalId(), devBean.getCategory(), dps, new IResultCallback() {
            @Override
            public void onError(String errorCode, String errorMsg) {
            }

            @Override
            public void onSuccess() {
            }
        });

```
###  Data Monitor

Mesh info（ dp data、status change、device name、device remove）will real-time sync to `IMeshDevListener` 

**Example**

```java
mWiserSigMeshDevice.registerMeshDevListener(new IMeshDevListener() {

@Override
public void onDpUpdate(String nodeId, String dps,boolean isFromLocal) {
    DeviceBean deviceBean = mWiserBlueMeshDevice.getMeshSubDevBeanByNodeId(nodeId);
}
  
@Override
public void onStatusChanged(List<String> online, List<String> offline,String gwId) {
}
 
@Override
public void onNetworkStatusChanged(String devId, boolean status) {
      
}        

@Override
public void onRawDataUpdate(byte[] bytes) {

}
         
@Override
public void onDevInfoUpdate(String devId) {
}  

@Override
public void onRemoved(String devId) {
}
});
```

## Firmware Upgrade

There are two types of sub-device upgrades, one is ordinary sub-device upgrade, and the other is mesh gateway upgrade.

### Query Firmware Info

**Declaration**

```java
void requestUpgradeInfo(String devId, IRequestUpgradeInfoCallback callback);
```

**Parameters**

|param|type|description|
|--|--|--|
|devId|String|devId|
|callback|IRequestUpgradeInfoCallback|callback|

**Example**

```java
WiserHomeSdk.getMeshInstance().requestUpgradeInfo(mDevID, new IRequestUpgradeInfoCallback() {
    @Override
    public void onSuccess(ArrayList<BLEUpgradeBean> bleUpgradeBeans) {
       
    }

    @Override
    public void onError(String errorCode, String errorMsg) {
    }
});
```

`BLEUpgradeBean`  data model

|param|type|description|
|------|------|-------|
|upgradeStatus|int|0: No new version 1: New version available 2: In upgrade|
|version| String|Latest version|
|currentVersion| String |Current version|
|timeout| int| timeout, Unit s|
|upgradeType|int|0:Reminds to upgrade 2: Forced upgrade 3: Detect upgrade|
|type|int|0: Wi-Fi 1: BLE  2: GPRS 3: Zigbee 9: MCU|
|typeDesc| String |Upgrade description|
|lastUpgradeTime|long|Last upgrade time|
|**url**|String|New firmware download url, `type` =` 1` or `9` has value|
|fileSize|long|New firmware size|
|md5|String|New firmware MD5 value|


### Sub-device Upgrade

**Declaration**

```java
void startOta();
```

**Example**

```java
private MeshUpgradeListener mListener = new MeshUpgradeListener() {
        @Override
        public void onUpgrade(int percent) {
        }

        @Override
        public void onSendSuccess() {
        }

        @Override
        public void onUpgradeSuccess() {
        	 mMeshOta.onDestroy();
        }

        @Override
        public void onFail(String errorCode, String errorMsg) {
        	 mMeshOta.onDestroy();
        }
    };
byte data[] = getFromFile(path);

WiserBlueMeshOtaBuilder build = new WiserBlueMeshOtaBuilder()
        .setData(data)
        .setMeshId(mDevBean.getMeshId())
        .setProductKey(mDevBean.getProductId())
        .setNodeId(mDevBean.getNodeId())
        .setDevId(mDevID)
        .setVersion("version")
        .setWiserBlueMeshActivatorListener(mListener)
        .bulid();
IWiserBlueMeshOta  = WiserHomeSdk.newMeshOtaManagerInstance(build);

//start
mMeshOta.startOta();
```

**Parameter**

`WiserBlueMeshOtaBuilder`

|param|type|description|
|--|--|--|
|data|byte[]|Byte stream of the firmware to be upgraded|
|meshId|String|Device MeshId|
|productKey|String|Product Id|
|mNodeId|String|Device NodeId|
|devId|String|Device Id|
|version|String|Version|


### Mesh Gateway Upgrade

Refer to the gateway upgrade, the following is the sample code

**Example**

```java
private IOtaListener iOtaListener = new IOtaListener() {
        @Override
        public void onSuccess(int otaType) {
  		}

        @Override
        public void onFailure(int otaType, String code, String error) {
        }

        @Override
        public void onProgress(int otaType, final int progress) {     
        }
    };

IWiserOta iWiserOta = WiserHomeSdk.newOTAInstance(mDevID);
iWiserOta.setOtaListener(mOtaListener);
//start
iWiserOta.startOta();

//destroy
iWiserOta.onDestroy();

```
