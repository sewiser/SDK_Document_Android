## Firmware Upgrade
There are two types of sub-device upgrades, one is the ordinary sub-device upgrade, and the other is the mesh gateway upgrade.

### Get Sub-device Upgrade Information
```java
WiserHomeSdk.getMeshInstance().requestUpgradeInfo(mDevID, new IRequestUpgradeInfoCallback() {
    @Override
    public void onSuccess(ArrayList<BLEUpgradeBean> bleUpgradeBeans) {
    	for (BLEUpgradeBean bean : bleUpgradeBeans) {
       if (bean.getUpgradeStatus()==1) {
          if (bean.getType() == 0) {
            // wifi module needs to be upgraded
          }else if(bean.getType == 1){
            // Bluetooth module needs to be upgraded
            // Need to download ota firmware manually
            url=bean.getUrl()
					}
       }else{
         // No update required
       }
		 }
    }

    @Override
    public void onError(String errorCode, String errorMsg) {
    }
});
```

### Sub-device Upgrade
##### 【Initial parameter configuration】
```java
WiserBlueMeshOtaBuilder build = new WiserBlueMeshOtaBuilder()
            .setData(byte[] data)
            .setMeshId(String meshId)
            .setProductKey(String productKey)
            .setNodeId(String nodeId)      
            .setDevId(String devId)
            .setVersion(String version)
            .setWiserBlueMeshActivatorListener(MeshUpgradeListener mListener)
            .bulid();

```
##### 【Parameter Description】
###### 【Entry parameters】
```java
* @param data     				byte stream of the firmware to be upgraded
* @param meshId   				meshId
* @param productKey    		product Id
* @param mNodeId  				nodeId
* @param devId 					  device Id 
* @param version     			the version number of the firmware to be upgraded
```

###### 【Back parameters】
MeshUpgradeListener listener 

##### 【Example Codes】
```java
private MeshUpgradeListener mListener = new MeshUpgradeListener() {
        @Override
        public void onUpgrade(int percent) {
        	// upgrade progress
        }

        @Override
        public void onSendSuccess() {
        	// firmware data sent successfully

        }

        @Override
        public void onUpgradeSuccess() {
        	// update successed
        	 mMeshOta.onDestroy();
        }

        @Override
        public void onFail(String errorCode, String errorMsg) {
        	// update failed
        	 mMeshOta.onDestroy();
        }
    };
//Get the byte stream of the specified file
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

// Start upgrading
mMeshOta.startOta();
```

### Gateway Device Upgrade
The gateway device upgrade is divided into 2 steps.

1. Upgrade the Bluetooth module (the operation is the same as that of ordinary sub-device upgrades) 
2. Upgrade the wifi module

##### 【Example Codes】
```java
private IOtaListener iOtaListener = new IOtaListener() {
        @Override
        public void onSuccess(int otaType) {
            // update successed
  		
  		}

        @Override
        public void onFailure(int otaType, String code, String error) {
         	// update failed

        }

        @Override
        public void onProgress(int otaType, final int progress) {
           // update progress
                      
        }
    };

IWiserOta iWiserOta = WiserHomeSdk.newOTAInstance(mDevID);
iWiserOta.setOtaListener(mOtaListener);
// start upgrading
iWiserOta.startOta();

// destroy upgrading
iWiserOta.onDestroy();

```
