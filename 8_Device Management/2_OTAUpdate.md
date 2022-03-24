# Firmware upgrade

Firmware upgrades are mainly used to add new device features and repair device bugs;

There are two main types of firmware upgrades. The first is device upgrade and the second is MCU upgrade. 

## Initialize the firmware information

**Declaration**

wifi, zigbee gateway, camera and other equipment:

```java
IWiserOta newOTAInstance(String devId);
```

**Parameters**

| Parameters | Description |
| ---- | ---- |
| devId | device id |

**Example**

```java
IWiserOta iWiserOta = WiserHomeSdk.newOTAInstance("devId");
```

## Initialize sub-device firmware information

NOTE：Zigbe sub-device upgrades are supported from SDK version 2.9.1.

**Declaration**

sub-device：

```java
IWiserOta newOTAInstance(String meshId, String devId, String nodeId);
```

**Parameters**

| Parameters  | Description                                  |
| ---- | ---- |
| meshId | Zigbee gateway id                 |
| devId | Zigbee child device id                  |
| nodeId | Zigbee sub-device mac address (obtained from the DeviceBean of the sub-device) |

**Example**

```java
IWiserOta iWiserOta = WiserHomeSdk.newOTAInstance("meshId", "devId", "nodeId");
```

## Obtaining Firmware Upgrade Information

**Declaration**

```java
iWiserOta.getOtaInfo(new IGetOtaInfoCallback({
	@Override
	void onSuccess(List<UpgradeInfoBean> list) {
	
	}
	@Override
	void onFailure(String code, String error) {
	
	}
});
```

**Parameters**

| Parameters        | Type | Description                                       |
| ---- | ---- | ---- |
| upgradeStatus  | int | upgrade status, 0: no new version 1: new version available 2: in upgrade |
| version     | String | Latest version |
| currentVersion | String | Current version |
| timeout     | int | timeout, unit: second |
| upgradeType | int | 0: app reminder upgrade 2-app forced upgrade 3-detect upgrade |
| type        | int | 0: wifi device 1: Bluetooth device 2: GPRS device 3: zigbee device 9: MCU |
| typeDesc    | String | module description |
| lastUpgradeTime | long  | last upgrade time in milliseconds |

## Set upgrade status callback

**Declaration**

```java
iWiserOta.setOtaListener(new IOtaListener() {
        @Override
        public void onSuccess(int otaType) {

        }

        @Override
        public void onFailure(int otaType, String code, String error) {

        }

        @Override
        public void onFailureWithText(int otaType, String code,
                                      OTAErrorMessageBean messageBean) {

        }

        @Override
        public void onProgress(int otaType, int progress) {

        }

        @Override
        public void onTimeout(int otaType) {

        }
});
```

**Parameters**

| Parameters | Description |
| ---- | ---- |
| otaType | The device type to be upgraded, the same as the type field of `UpgradeInfoBean` |

## Start upgrade

**Declaration**

Call this method to start the upgrade. The ota listener registered after the call will return the upgrade status so that the developer can build the UI.

```java
iWiserOta.startOta();
```

## Destroy

**Declaration**

Destroy after leaving the upgrade page and reclaim memory.

```java
iWiserOta.onDestory();
```

## Full example

```java
public void start() {
    String devId = "your_devId";
    final IWiserOta iWiserOta = WiserHomeSdk.newOTAInstance(devId);
    iWiserOta.getOtaInfo(new IGetOtaInfoCallback() {
        @Override
        public void onSuccess(List<UpgradeInfoBean> upgradeInfoBeans) {
            int type = getUpgradeType(upgradeInfoBeans);
            if (type > 0) {
                startUpgrade(iWiserOta, type);
            }
        }

        @Override
        public void onFailure(String code, String error) {
            Log.i(TAG, "Get OTA info failed,errorCode=" + code
                    + ",errorMessage=" + error);
        }
    });
}

private int getUpgradeType(List<UpgradeInfoBean> upgradeInfoBeans) {
    int type = -1;
    for (UpgradeInfoBean bean : upgradeInfoBeans) {
        if (bean.upgradeType == 2) {
            return -1;
        } else if (bean.upgradeType == 1 && type == -1) {
            type = bean.getType();
        }
    }
    return type;
}

private void startUpgrade(final IWiserOta iWiserOta, int type) {
    final int messageWhat = 10001;
    final Handler handler = new Handler(Looper.getMainLooper()) {
        @Override
        public void handleMessage(@NonNull Message msg) {
            super.handleMessage(msg);
            Log.i(TAG, "upgrade timeout");
        }
    };
    iWiserOta.setOtaListener(new IOtaListener() {
        @Override
        public void onSuccess(int otaType) {
            handler.removeMessages(messageWhat);
            iWiserOta.onDestroy();
            Log.i(TAG, "upgrade success");
        }

        @Override
        public void onFailure(int otaType, String code, String error) {
            handler.removeMessages(messageWhat);
            iWiserOta.onDestroy();
            Log.i(TAG, "upgrade failure, errorCode = " + code
                    + ",errorMessage = " + error);
        }

        @Override
        public void onFailureWithText(int otaType, String code,
                                      OTAErrorMessageBean messageBean) {
            handler.removeMessages(messageWhat);
            iWiserOta.onDestroy();
            Log.i(TAG, "upgrade failure, errorCode = " + code
                    + ",errorMessage = " + messageBean.text);
        }

        @Override
        public void onProgress(int otaType, int progress) {
            Log.i(TAG, "upgrade progress = " + progress);
          	handler.removeMessages(messageWhat);
            handler.sendEmptyMessageDelayed(messageWhat, 120 * 1000);
        }

        @Override
        public void onTimeout(int otaType) {
            handler.removeMessages(messageWhat);
            iWiserOta.onDestroy();
            Log.i(TAG, "upgrade timeout");
        }
    });
    handler.sendEmptyMessageDelayed(messageWhat, 120 * 1000);
    iWiserOta.startOta();
}
```