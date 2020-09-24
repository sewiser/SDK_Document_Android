# Firmware upgrade

Firmware upgrades are mainly used to repair device bugs and add new device features. There are two main types of firmware upgrades. The first is device upgrade and the second is MCU upgrade. The upgraded interface is located in IwiserOta.
Zigbe sub-device upgrades are supported from SDK version 2.9.1.

## Query firmware upgrade information

**Declaration**

wifi, zigbee gateway, camera and other equipment initialization interface

```java
IWiserOta newOTAInstance (String devId)
```

**Parameters**

| Parameters | Description |
| ----- | ------ |
| devId | device id |

**Declaration**

Child device initialization interface

```java
IWiserOta newOTAInstance (String meshId, String devId, String nodeId);
```

**Parameters**

|Parameters | Description |
| ------ | ---------------------------------------------- |
|meshId | zigbee gateway id |
|devId | zigbee child device id |
|nodeId | igbee sub-device mac address (obtained from the DeviceBean of the sub-device) |

**Example**

Obtaining Firmware Upgrade Information

```java
WiserHomeSdk.newOTAInstance (mDevId) .getOtaInfo (new IGetOtaInfoCallback ({
@Override
void onSuccess (List <UpgradeInfoBean> list) {
Ranch
}
@Override
void onFailure (String code, String error);
Ranch
});

WiserHomeSdk.newOTAInstance ("xxxmeshId", "xxxdevId", "xxxmac address"). GetOtaInfo (new IGetOtaInfoCallback ({
@Override
void onSuccess (List <UpgradeInfoBean> list) {
Ranch
}
@Override
void onFailure (String code, String error);
Ranch
});

```

`UpgradeInfoBean` returns firmware upgrade information, providing the following information

|Field | Type | Description |
| --------------- | ------ | ------------------------------------------ |
|upgradeStatus | int | upgrade status, 0: no new version 1: new version available 2: in upgrade |
| version | String | Latest version |
| currentVersion | String | Current version |
timeout | int | timeout, unit: second |
upgradeType | int | 0: app reminder upgrade 2-app forced upgrade 3-detect upgrade
| type | int | 0: wifi device 1: Bluetooth device 2: GPRS device 3: zigbee device 9: MCU |
| typeDesc | String | module description |
| lastUpgradeTime | long | last upgrade time in milliseconds |

**Example**

```java
iWiserOta.getOtaInfo (new IGetOtaInfoCallback () {
    @Override
    public void onSuccess (List <UpgradeInfoBean> list) {
        
        }
    }

    @Override
    public void onFailure (String code, String error) {
        L.e (TAG, "check error" + code + "---- error =" + error);
    }
        });
```

## Set upgrade status callback

Before ota, you need to register for monitoring to get the upgrade status in real time

**Example**

```java
// otaType The device type to be upgraded, the same as the type field of `UpgradeInfoBean`
iWiserOta.setOtaListener (new IOtaListener () {
    @Override
    public void onSuccess (int otaType) {
        
    }

    @Override
    public void onFailure (int otaType, String code, String error) {

    }

    @Override
    public void onProgress (int otaType, int progress) {

    }
});
```

## Start the upgrade

 Call this method to start the upgrade. The ota listener registered after the call will return the upgrade status so that the developer can build the UI.

**Example**

```java
iWiserOta.startOta ();
```

## Destroy

Destroy after leaving the upgrade page and reclaim memory.

**Example**

```java
iWiserOta.onDestroy ();
```

####
