### Device QRCode Configuration

#### Description

This function is only applicable to the device that has self-entered internet after powered on the device. 
And after resetting the device status, it will connect to the Wiser Cloud Server.

```sequence

Title: Device QRCode Configuration

participant Device
participant httpdns
participant mqtt
participant APP
participant cloud

Note over Device: power on the device, and device will connect the internet
Note over Device: resetting the device status

Device -> httpdns: select httpdns to get the mqttsUrl domain name.
httpdns -> Device: return the mqttsUrl domain name
Device -> mqtt: use uuid to connect mqtt

APP -> Device: scan device QR code
APP -> cloud: APP gets the device uuid and creates a token from the cloud.
APP -> cloud: Use the token to poll the list of network activation devices every 2 seconds (the total duration is 100s by default)

cloud -> mqtt: push token and region
mqtt -> Device: push token and region to device

Device->cloud: Activate the device
cloud-->Device: Network configuration succeeds
cloud-->APP: Network configuration succeeds

```

#### Configuration Method Invocation

```java
/**
* @param uuid 设备UUID
* @param homeId 家庭ID
* @param CONFIG_TIME_OUT 超时时间，建议设置为120s（单位是秒）
*/
WiserQRCodeActivatorBuilder builder = new WiserQRCodeActivatorBuilder()
.setUuid(uuid)
.setHomeId(homeId)
.setContext(mActivity)
.setTimeOut(CONFIG_TIME_OUT)
.setListener(new IWiserSmartActivatorListener() {
    @Override
    public void onError(String errorCode, String errorMsg) {
    }

    @Override
    public void onActiveSuccess(DeviceBean devResp) {
    }

    @Override
    public void onStep(String step, Object data) {
    }
}));

IWiserActivator mWiserActivator = WiserHomeSdk.getActivatorInstance().newQRCodeDevActivator(builder);
// Start network configuration
mWiserActivator.start();
// Stop network configuration
mWiserActivator.stop();
// Destroy
mWiserActivator.onDestory();
```
