### Network Configuration for ZigBee Sub-device

#### Description

The network configuration for ZigBee sub-device can be initiated only when the cloud for ZigBee gateway device is online, and the sub-device has been configured.

```sequence
Title: Zigbee sub-device configuration

participant APP
participant SDK
participant Zigbee Gateway
participant Service

Note over Zigbee Gateway: Reset zigbee sub device
APP->SDK: sends the subdevice activation instruction
SDK->Zigbee Gateway: sends the activation instruction

Note over Zigbee Gateway: zigbee gateway receives the activation data

Zigbee Gateway->Service: activate the sub device
Service-->Zigbee Gateway: network configuration succeeds

Zigbee Gateway-->SDK: network configuration succeeds
SDK-->APP: network configuration succeeds

```

#### Configuration Method Invocation

```java
WiserGwSubDevActivatorBuilder builder = new WiserGwSubDevActivatorBuilder()
// Setting the gateway ID
.setDevId(mDevId)
// Setting the time-out period for network configuration
.setTimeOut(100)
.setListener(new IWiserSmartActivatorListener() {
@Override
public void onError(String s, String s1) {
}

@Override
public void onActiveSuccess(DeviceBean deviceBean) {
}

@Override
public void onStep(String s, Object o) {
}
});

IWiserActivator mWiserGWActivator = WiserHomeSdk.getActivatorInstance(). newGwSubDevActivator(builder);
// Start network configuration
mWiserGWActivator.start();
// Stop network configuration
mWiserGWActivator.stop();
// Destroy
mWiserGWActivator.onDestory();
```
