### Wifi Network Configuration

#### Description

The Wifi network configuration mainly includes two network configuration modes, namely, EZ mode and AP mode.

#### Get Network Configuration Token

Before the wifi network configuration, the SDK needs to obtain the network configuration Token from the Wiser Cloud.
The term of validity of Token is 5 minutes, and the Token become invalid once the network configuration succeeds.
A new Token has to be obtained if you have to reconfigure network.

```java
/**
* @param homeId(Reference family management section)
* @param callback
*/
WiserHomeSdk.getActivatorInstance().getActivatorToken(homeId, new IWiserActivatorGetToken() {
@Override
public void onSuccess(String token) {

}

@Override
public void onFailure(String s, String s1) {

}
});
```

#### Initialize The Network Configuration Parameter

```java
protected IWiserActivator mWiserActivator; // the interface for configuration business class implements
```

```java
/**
* @param token: The activation key required for network configuration.
* @param ssid: Name of the Wifi used by devices in working after the network isconfigured.  (Home network)
* @param password: Password of the Wifi used by devices in working after the network is configured.  (Home network)
* @param activatorModel: Currently, the following two methods are used for network configuration of devices.
ActivatorModelEnum.TY_EZ: The EZ mode network configuration is enabled is this parameter is transfered.
ActivatorModelEnum.TY_AP: The AP mode network configuration is enabled is this parameter is transfered.
* @param timeout: The timeout for the network configuration is set to 100s by default.
* @param context: The context that is needed to be transferred to the activity.
*/
```

#### EZ Mode Configuration

```sequence
Title: EZ Mode

participant APP
participant Device
participant Service

Note over APP: Connect to the Wifi of router
Note over Device: Switch to the EZ mode

APP-->Service: Get Token
Service-->APP: Response Token

Note over APP: Start network configuration (send configuration data), broadcast configuration data
Device->Device: Get configuration data

APP-->Server: Use the token to poll the list of network activation devices every 2 seconds (the total duration is 100s by default)

Device->Service: Activate the device
Service-->Device: Network configuration succeeds

Server-->APP: Network configuration succeeds


```

```java
mWiserActivator = WiserHomeSdk.getActivatorInstance().newMultiActivator(new ActivatorBuilder()
.setSsid(ssid)
.setContext(context)
.setPassword(password)
.setActivatorModel(ActivatorModelEnum.TY_EZ)
.setTimeOut(CONFIG_TIME_OUT)
.setToken(token)
.setListener(this));
```

#### AP Mode Configuration

```sequence
Title: AP Mode

participant APP
participant Device
participant Service

Note over Device: Switch to the AP mode

APP-->Service: Get Token
Service-->APP: Response Token

Note over APP: Connect the hotspot device

APP->Device: Start network configuration (send configuration data), send configuration data

APP-->Server: Use the token to poll the list of network activation devices every 2 seconds (the total duration is 100s by default)

Note over Device: Device turns off hotspot automatically
Note over Device: The device is connected to the Wifi of router

Device->Service: Activate the device
Service-->Device: Network configuration succeeds

Server-->APP: Network configuration succeeds

```

```java
mWiserActivator = WiserHomeSdk.getActivatorInstance().newActivator(new ActivatorBuilder()
.setSsid(ssid)
.setContext(context)
.setPassword(password)
.setActivatorModel(ActivatorModelEnum.TY_AP)
.setTimeOut(CONFIG_TIME_OUT)
.setToken(token)
.setListener(this));
```

#### Configuration Method Invocation

```java
mWiserActivator.start(); // Start configuration

mWiserActivator.stop(); // Stop configuration

mWiserActivator.onDestroy(); // Exit the page to destroy some cache data and monitoring data.
```

#### Configuration Result Callback

```
IWiserSmartActivatorListener listener // network configuration callback interface
```

```java
/**
* @method onError(String errorCode,String errorMsg);
@param errorCode:
1001        Network error
1002        The invocation of device network configuration interface fails.
1003        The activation of network configuration device fails, and device is not detected.
1004        Obtaining token fails.
1005        The device is offline.
1006        Timeout in network configuration
@param errorMsg:
Temporarily, no data is available, please refer to the errorCode.

* @method onActiveSuccess(DeviceBean deviceBean);
The network configuration of device succeeds, and the device goes online (Mobile phone can control device directly).

* @method onStep(String step, Object o);
|@param step         |@param o
|device_find         |devId (String)
|device_bind_success |dev (DeviceBean)
[Note]
Device_find Find device.
Device_bind_success Binding device succeeds, but the device is not online yet and cannot be controlled with your mobile phone.
**/
```

#### Summary of Problems for Network Configuration

Timeout in network configuration. The device cannot be connected to the network. The causes may be:

- The obtained WiFi Ssid is incorrect. The ssid obtained in the Android system usually has “” in the front or back of it.  It is recommended to use the WiFiUtil.getCurrentSSID() in the Wiser Sdk to obtain the Wifi Ssid. 
- The Wifi password has space. User may accidentally enter the space because of the predictive typing function. It is recommended that users enable the displaying password option when entering password. Or prop-up windows shall be displayed if the password entered includes spaces. 
- Users have not entered the Wifi password. User may forget to enter the password when they use the smart device for the first time. It is recommended that prop-up windows be displayed if no password is entered and the Wifi encryption type is not set to NONE.
- Users select the hotspot name of device in the AP mode network configuration. This problem is prevalent when users use the smart device for the first time. It is recommended that prop-up windows be displayed if users selected the hotspot name of devices in the AP mode network configuration. 
- The Ssid of the obtained Wifi is “0x” and <unknown ssid>. Currently, this problem may occur in Chinese mobile phones, and this problem is not caused by Wifi but the permission to locate. It is recommended that user enter the Ssid of Wifi manually or the prop-up windows be displayed to ask users to authorize permissions.

Timeout in network configuration, but the device has been successfully activated. The possible cause is:

- The App is not using a normal network, and the status of device cannot be obtained. 
