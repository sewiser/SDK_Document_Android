# Bluetooth Mesh (WISER)

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
###  Create Mesh

**Declaration**

```java
void createBlueMesh(String meshName, IWiserResultCallback<BlueMeshBean> callback);
```
**Parameters**

|Field|Type|Describe|
|--|--|--|
|meshName|String|mesh's name（limit 16）|
|callback|IWiserResultCallback|callback|

**Example**

``` java
WiserHomeSdk.newHomeInstance("homeId").createBlueMesh("meshName", new IWiserResultCallback<BlueMeshBean>() {
    @Override
    public void onError(String errorCode, String errorMsg) {
    }

    @Override	
    public void onSuccess(BlueMeshBean blueMeshBean) {
    }
});
```

### Delete Mesh

**Declaration**

```java
void removeMesh(IResultCallback callback);
```
**Parameters**

|Field|Type|Describe|
|--|--|--|
|callback|IResultCallback|callback|

**Example**

```java
WiserHomeSdk.newBlueMeshDeviceInstance(meshId).removeMesh(new IResultCallback() {
    @Override
    public void onError(String errorCode, String errorMsg) {
    }
	
    @Override
    public void onSuccess() {
    }
});

```

### Get The List Of Mesh In The Family

**Declaration**

```java
List<BlueMeshBean> getMeshList();
```
**Example**

```java
IWiserHome mWiserHome = WiserHomeSdk.newHomeInstance("homeId");
if (mWiserHome.getHomeBean() != null){
	List<BlueMeshBean> meshList = mWiserHome.getHomeBean().getMeshList();
	BlueMeshBean meshBean= meshList.get(0);
}            
```

### Get Data of Mesh's Sub-devices
**Declaration**

```java
List<DeviceBean> getMeshSubDevList();
```
**Example**

```java
List<DeviceBean> meshSubDevList = WiserHomeSdk.newBlueMeshDeviceInstance("meshId").getMeshSubDevList();
    
```


### Mesh Instance and Destroy
recommend to destroy the Mesh and re-initialize the Mesh in the family when the family switches.

**Example**

```java
//init
WiserHomeSdk.getWiserBlueMeshClient().initMesh(String meshId);       

//destroy
WiserHomeSdk.getWiserBlueMeshClient().destroyMesh();       
```


### Mesh Sub-devices's Connect and Disconnect
IWiserBlueMeshClient has start connecting, disconnect, start scanning, stop scanning.

**Example**

```java
//start connecting
WiserHomeSdk.getWiserBlueMeshClient().startClient(mBlueMeshBean);

//disconnect
WiserHomeSdk.getWiserBlueMeshClient().stopClient();

//start scanning
WiserHomeSdk.getWiserBlueMeshClient().startSearch()

//stop scanning
WiserHomeSdk.getWiserBlueMeshClient().stopSearch();

```

**Precautions** 

 -  Start connecting and will be scanning the connectable devices in the background until the connection is successful.
 -  Scanning always consumes resources, can control scanning by turning on scanning and stopping scanning.
 -  Use `startSearch()` or `stopSearch()` must be after calling `startClient()`.
 -   `startSearch()` or `stopSearch()` will be not working when connected to the Mesh.

## Activation

### Device Reset

| Product Type      | Reset Operate                    | Phenomenon                                                   |
| ----------------- | -------------------------------- | ------------------------------------------------------------ |
| Light             | Switch three times in a row      | Flashing lights                                              |
| Socket            | Press and hold the switch for 3s | The socket indicator flashes quickly                         |
| Gateway           | Press and hold the switch for 3s | Red and blue lights flash fast                               |
| Low-power devices | Press and hold the switch for 3s | Press again to display a long light to configure the network, and the network configuration must be completed during the light is on |
| Alarm             | Press and hold the switch for 3s | Flashing lights                                              |

The device in reset state has a default name is `out_of_mesh` and a default password is `123456`.

### Scaning Mesh Device

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

SearchBuilder searchBuilder = new SearchBuilder()
		 .setMeshName("out_of_mesh")        
     .setTimeOut(100)        
     .setWiserBlueMeshSearchListener(iWiserBlueMeshSearchListener).build();

IWiserBlueMeshSearch mMeshSearch = WiserHomeSdk.getWiserBlueMeshConfig().newWiserBlueMeshSearch(searchBuilder);

//start
mMeshSearch.startSearch();
//stop
mMeshSearch.stopSearch();
```

### Active Mesh Device By Bluetooth

Two types of sub-devices Activation, App activation and Mesh gateway activation.

**Declaration**

```java
void startActivator();

void stopActivator();
```

**Parameters**

|field|type|describe|
|--|--|--|
|mSearchDeviceBeans     |List|List of devices to be activated|
|timeout                |Int|Activation timeout，default 100s.|
|ssid                   |String|After activation, Wi-Fi's ssid.|
|password               |String|After activation, Wi-Fi's password.|
|mMeshBean              |MeshBean|MeshBean |
|homeId                 |Long|HomeId|
|version                |String|Devices activation is 1.0, gateway activation is 2.2.|



**Example**

```java
WiserBlueMeshActivatorBuilder wiserBlueMeshActivatorBuilder = new WiserBlueMeshActivatorBuilder()
                .setSearchDeviceBeans(foundDevices)
                .setVersion("1.0")
                .setBlueMeshBean(mMeshBean)
                .setTimeOut(timeOut)
                .setWiserBlueMeshActivatorListener(new IWiserBlueMeshActivatorListener() {
     @Override
     public void onSuccess(DeviceBean deviceBean) {
     }

     @Override
     public void onError(String errorCode, String errorMsg) {
     }

     @Override
     public void onFinish() {
     }});
      
IWiserBlueMeshActivator iWiserBlueMeshActivator = WiserHomeSdk.getWiserBlueMeshConfig().newActivator(wiserBlueMeshActivatorBuilder);

iWiserBlueMeshActivator.startActivator();

iWiserBlueMeshActivator.stopActivator();

```

### Active Mesh Gateway Device

**Declaration**

```java
void startActivator();

void stopActivator();
```
**Parameters**

|field|type|describe|
|--|--|--|
|mSearchDeviceBeans     |List|List of devices to be configured|
|timeout                |Int|Activation timeout，default 100s.|
|ssid                   |String|After activation, Wi-Fi's ssid.|
|password               |String|After activation, Wi-Fi's password.|
|mMeshBean              |MeshBean|MeshBean |
|homeId                 |Long|HomeId|
|version                |String|Devices activation is 1.0, gateway activation is 2.2.|

**Example**

```java
WiserBlueMeshActivatorBuilder wiserBlueMeshActivatorBuilder = new WiserBlueMeshActivatorBuilder()
                .setWifiSsid(mSsid)
                .setWifiPassword(mPassword)
                .setSearchDeviceBeans(foundDevices)
                .setVersion("2.2")
                .setBlueMeshBean(mMeshBean)
                .setHomeId("homeId")
                .setWiserBlueMeshActivatorListener(new IWiserBlueMeshActivatorListener() {

   @Override
   public void onSuccess(DeviceBean devBean) {
    }

   @Override
   public void onError(String errorCode, String errorMsg) {
  }

   @Override
   public void onFinish() {  
 
   }});
IWiserBlueMeshActivator iWiserBlueMeshActivator = WiserHomeSdk.getWiserBlueMeshConfig().newWifiActivator(wiserBlueMeshActivatorBuilder);

iWiserBlueMeshActivator.startActivator();

iWiserBlueMeshActivator.stopActivator();

```


### Error Code

|Code|describe|
|--|--|
|13007|Device login failed|
|13004|Failed to reset device address|
|13005|Device address is full|
|13007|Ssid is empty|
|13011|Activation timeout|

## Device

### Found Mesh Devices

**Example**

```java
DeviceBean deviceBean=WiserHomeSdk.getDataInstance().getDeviceBean(mDevId);

if(deviceBean.isBlueMesh()){
    L.d(TAG, "This device is blue mesh device");
 }

if(deviceBean.isBlueMeshWifi()){
    L.d(TAG, "This device is blue mesh wifi device");
 }
```
###  Rename Device

**Declaration**

```java
void renameMeshSubDev(String devId, String name, IResultCallback callback);
```

**Parameters**

|param|type|describe|
|--|--|--|
|devId  |String| Device Id |
|name		|String|New name|
|callback|IResultCallback|Callback|

**Example**

```java
mWiserBlueMesh.renameMeshSubDev(devBean.getDevId(),"device name", new IResultCallback() {
            @Override
            public void onError(String code, String errorMsg) {
            }

            @Override
            public void onSuccess() {
            }
        });
```

### Local Connection And Gateway Connection

**Example**

```java
DeviceBean deviceBean=WiserHomeSdk.getDataInstance().getDeviceBean(mDevId);

boolean online=deviceBean.getIsOnline()

boolean localOnline=deviceBean.getIsLocalOnline()

boolean wifiOnline=deviceBean.isCloudOnline() && gwBean.getIsOnline() 
```

### Remove Device

**Declaration**

```java
void removeMeshSubDev(String devId, IResultCallback callback);
```
**Parameters**

|param|type|describe|
|--|--|--|
|devId  |String| Device Id |
|pcc		|String|Device type|
|callback|IResultCallback|Callback|

**Example**

```java
mWiserBlueMesh.removeMeshSubDev(devBean.getDevId(), new IResultCallback(){
  @Override
  public void onError(String code, String errorMsg) {
 }

 @Override
 public void onSuccess() {
  Toast.makeText(mContext, "sub-deivces remove success", Toast.LENGTH_LONG).show();
  }});
```

### Query Mesh Device Status

Get dp data from cloud maybe not real-time data, can use it search real-time data and `IMeshDevListener`'s `onDpUpdate` will be callback.

**Declaration**

```java
void querySubDevStatusByLocal(String pcc, String nodeId, IResultCallback callback);
```

**Parameters**

|param|type|describe|
|--|--|--|
|pcc  |String| Device type |
|nodeId		|String|Device nodeId|
|callback|IResultCallback|Callback|

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

### Create Group

Currently, each mesh supports a maximum of 28672 groups  id in 8000 ~ EFFF  (0x).

**Declaration**

```java
void addGroup(String name, String pcc, String localId,IAddGroupCallback callback);
```

**Parameters**

| field    | describe      |
| -------- | ------------- |
| name     | group name    |
| pcc      | pcc           |
| localId  | group address |
| callback | callback      |

**Example**

```java
mIWiserBlueMesh.addGroup("groupName","pcc", "8001", new IAddGroupCallback() {
   @Override
   public void onError(String errorCode, String errorMsg) {
   }   

   @Override
   public void onSuccess(long groupId) {
   }
});
```

### Add Deivce to Group

**Declaration**

```java
void addDevice(String devId,IResultCallback callback);
```
**Parameters**

|field|type|describe|
|--|--|--|
|devId|String|Device Id|
|callback|IResultCallback|Callback|

**Example**

```java
IWiserGroup mGroup = WiserHomeSdk.newBlueMeshGroupInstance(groupId);
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

|field|type|describe|
|--|--|--|
|devId|String|Device Id|
|callback|IResultCallback|Callback|



**Example**

```java
IWiserGroup mGroup = WiserHomeSdk.newBlueMeshGroupInstance(groupId);
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

|field|type|describe|
|--|--|--|
|callback|IResultCallback|Callback|

**Example**

```java
IWiserGroup mGroup = WiserHomeSdk.newBlueMeshGroupInstance(groupId);
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

|field|type|describe|
|--|--|--|
|groupName|String|Rename|
|callback|IResultCallback|Callback|

**Example**

```java
IWiserGroup mGroup = WiserHomeSdk.newBlueMeshGroupInstance(groupId);
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
|:-|--|
|nodeId|Sub-devices No.|
|pcc|Devices type|
|dps|Control command|
|callback|Callback|

**Example**

```java
String dps = {"1":false};
IWiserBlueMeshDevice mWiserBlueMeshDevice=WiserHomeSdk.newBlueMeshDeviceInstance("meshId");
mWiserBlueMeshDevice.publishDps(devBean.getNodeId(), devBean.getCategory(), dps, new IResultCallback() {
            @Override
            public void onError(String s, String s1) {
            }

            @Override
            public void onSuccess() {
            }
        });
```
###  Control Command - Control Group

Format： 

```java
{"(dpId)":"(dpValue)"}  
```

**Declaration**

```java
void multicastDps(String localId, String pcc, String dps, IResultCallback callback)
```

**Parameters**

|field|describe|
|--|--|
|localId|Group No.|
|pcc|Device type|
|dps|Control command|
|callback|Callback|

**Example**

```java     
String dps = {"1":false};
IWiserBlueMeshDevice mWiserBlueMeshDevice= WiserHomeSdk.newBlueMeshDeviceInstance("meshId");
mWiserBlueMeshDevice.multicastDps(groupBean.getLocalId(), devBean.getCategory(), dps, new IResultCallback() {
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
mWiserBlueMeshDevice.registerMeshDevListener(new IMeshDevListener() {

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
}});
```


### Create Group
Mesh can create 28672 groups, id in [8000 ~ EFFF]  (Hexadecimal)  and locally maintained.

**Declaration**

```java
void addGroup(String name, String pcc, String localId,IAddGroupCallback callback);
```

**Parameters**

|field|describe|
|--|--|
|name|Group name|
|pcc|Device size|
|localId|Group's localId|
|callback|Callback|

**Example**

```java
mIWiserBlueMesh.addGroup("group name","device size", "8001", new IAddGroupCallback() {
			@Override
            public void onError(String errorCode, String errorMsg) {
            }   
            	
            @Override
            public void onSuccess(long groupId) {
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


### Sub-device Gateway Upgrade

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





