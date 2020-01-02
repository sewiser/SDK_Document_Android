# Firmware Upgrade

**[Description]**

The firmware upgrade is mainly used to fix device bugs and add new device functions. There are two main types of firmware upgrades, i.e., device upgrade and MCU upgrade. The interface for upgrade is located in IWiserOta.Zigbee sub-device OTA is available on 2.9.1 and the follow-up version.

## Querying Firmware Upgrade Information**

**[Method Invocation]**

```java
/**
 *	the init OTA method of wifi、zigbee gateway、camera ect.  Attention:This two constructor methods are not Singleton Pattern
 * @param devId  device id
 * @return
 */
IWiserOta newOTAInstance(String devId)

/**
 * the init OTA method of zigbee sub-device
 * @param meshId zigbee gateway id
 * @param devId zigbee sub-device id
 * @param nodeId zigbee sub-device mac address（get from the DeviceBean of zigbee sub-device）
 * @return
 */
IWiserOta newOTAInstance(String meshId, String devId, String nodeId);

```

```java

// Obtain firmware upgrade information

WiserHomeSdk.newOTAInstance(mDevId).getOtaInfo(new IGetOtaInfoCallback({
	@Override
	void onSuccess(List<UpgradeInfoBean> list){
	
	}
	@Override
	void onFailure(String code, String error);	

});

WiserHomeSdk.newOTAInstance("xxxmeshId","xxxdevId","xxxmac address").getOtaInfo(new IGetOtaInfoCallback({
	@Override
	void onSuccess(List<UpgradeInfoBean> list){
	
	}
	@Override
	void onFailure(String code, String error);
	
});


UpgradeInfoBean returns information about the firmware upgrade, including:
	private int upgradeStatus;// upgrade status (0: no new version 1: new version available 2: upgrading)
    private String version;// latest version
    private String currentVersion;//current version
    private int timeout;// time-out period (unit: s)
    private int upgradeType;//0: app reminding upgrade; 2-app carrying out forced upgrade; 3-detecting upgrade
    private int type;//0: wifi device; 1: bluetooth device; 2: GPRS device; 3: zigbee device (currently only zigbee gateway available); 9: MCU
    private String typeDesc;//module description
    private long lastUpgradeTime;// last upgrade time (unit: ms)
```
**[Example Codes]**

```java

iWiserOta.getOtaInfo(new IGetOtaInfoCallback() {
    @Override
    public void onSuccess(List<UpgradeInfoBean> list) {
        
        }
    }
    @Override
    public void onFailure(String code, String error) {

        L.e(TAG, "check error " + code + "----error=" + error);
    }
        });
```
## Setting Upgrade Status Callback

**[Description]**

Before ota, registration of listener is required to obtain the upgrade status in real time.

**[Method Invocation]**

```java

// otaType: type of device to be upgraded (identical to the type field of ‘UpgradeInfoBean’)

iWiserOta.setOtaListener(new IOtaListener() {
    @Override
    public void onSuccess(int otaType) {
        
	}
    @Override
    public void onFailure(int otaType, String code, String error) {
    }

    @Override
    public void onProgress(int otaType, int progress) {
    }

});
```
**Start Upgrading**

**[Description]**

Invoke to start the upgrade, and the registered ota listener after the invoking will return the upgrade status to facilitate the developer building UI.

**[Method Invocation]**

```java
iWiserOta.startOta();
```

**Destroy**

**[Description]**

After exiting the upgrade page, destroying is required to release the memory.

**[Method Invocation]**
```java
iWiserOta.onDestroy();
```
