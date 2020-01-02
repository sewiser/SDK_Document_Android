## Control
IWiserBlueMeshDevice provides operations on Mesh devices

###  Control Command Publish
#####  【command format】
```java
// Example for boolean type function point with dpId set to 101. Function: turn on switch. 

dps = {"101": true};

// Example of string type function point with dpId set to 102. Function: set RGB to ff5500.

dps = {"102": "ff5500"};

// Example of enumeration type function point with dpId set to 103. Function: set gear to position 2.

dps = {"103": "2"};

// Example of value type function point with dpId set to 104. Function: set temperature to 20 centigrade degree.

dps = {"104": 20};

// Example of transparent (byte array) function point with dpId set to 105. Function: transparently transfer infrared data (i.e., 1122).

dps = {"105": "1122"};

// Send multiple dp data in one time.

dps = {"101": true, "102": "ff5500"};
```



##### 【Method Invocation】
```java
//control device
* @param nodeId   sub-device local number
* @param pcc		  device product category
* @param dps		  command
* @param callback
void publishDps(String nodeId, String pcc, String dps, IResultCallback callback);


//control group
* @param localId   group local number
* @param pcc		   product category
* @param dps		   command
* @param callback  
void multicastDps(String localId, String pcc, String dps, IResultCallback callback)
```

##### 【Example Codes】
```java
//control device
String dps = {"1":false};
IWiserBlueMeshDevice mWiserSigMeshDevice=WiserHomeSdk.newSigMeshDeviceInstance("meshId");
mWiserSigMeshDevice.publishDps(devBean.getNodeId(), devBean.getCategory(), dps, new IResultCallback() {
            @Override
            public void onError(String s, String s1) {
            		Toast.makeText(mContext, "send fail "+ errorMsg, Toast.LENGTH_LONG).show();
            }

            @Override
            public void onSuccess() {
            		Toast.makeText(mContext, "send success", Toast.LENGTH_LONG).show();
            }
        });
        
        
//control group       
String dps = {"1":false};
IWiserBlueMeshDevice mWiserSigMeshDevice= WiserHomeSdk.newSigMeshDeviceInstance("meshId");
mWiserSigMeshDevice.multicastDps(groupBean.getLocalId(), devBean.getCategory(), dps, new IResultCallback() {
            @Override
            public void onError(String errorCode, String errorMsg) {
            		Toast.makeText(mContext, "send fail "+ errorMsg, Toast.LENGTH_LONG).show();
            }

            @Override
            public void onSuccess() {
            		Toast.makeText(mContext, "send success", Toast.LENGTH_LONG).show();
            }
        });

```
###  Data Callback
##### 【Description】
Relevant information (dp data, status change, device name, device removal) in the mesh network will be synchronized to IMeshDevListener in real time

##### 【Example Codes】
```java
mWiserSigMeshDevice.registerMeshDevListener(new IMeshDevListener() {

		/**
         * dp update
         * @param nodeId    update the nodeId of the device
         * @param dps       dp data
         * @param isFromLocal   data source true means from local Bluetooth and false means from cloud
         */
            @Override
            public void onDpUpdate(String nodeId, String dps,boolean isFromLocal) {
                //You can find the DeviceBean by nodeId
                DeviceBean deviceBean = mWiserBlueMeshDevice.getMeshSubDevBeanByNodeId(nodeId);
            }

		 /**
         * 设备状态的上报
         * @param online    onlins
         * @param offline   offlines
         * @param gwId      The source of the status gwId is not empty means it is from the cloud (gwId is the gateway ID for reporting data). It is empty means it is from the local Bluetooth
         */
            @Override
            public void onStatusChanged(List<String> online, List<String> offline,String gwId) {

            }
            
        /**
         * network status change
         * @param devId
         * @param status
         */
            @Override
            public void onNetworkStatusChanged(String devId, boolean status) {

            }
            

        /**
         * report raw data
         * @param bytes
         */
            @Override
            public void onRawDataUpdate(byte[] bytes) {

            }
            

        /**
         * change of device information (name, etc.)
         * @param bytes
         */            
            @Override
            public void onDevInfoUpdate(String devId) {

            }
            
        /**
         * Device removal
         * @param devId
         */
            @Override
            public void onRemoved(String devId) {

            }
        });
```



