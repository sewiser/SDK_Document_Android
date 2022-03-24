# Device Management

Wiser Smart provides a lot of interfaces for developers to realize the acquisition of device information and management capabilities (removal, and so on). Receivers shall be informed of the device-related return data by means of asynchronous messages.The IWiserDevice class provides the device status notification capability. By registering callback functions, developers can easily obtain notifications on device data reception, device removal, online/offline status of device, and mobile network changes. In addition, it also provides an interface for controlling command issuing and device firmware upgrade. 


**DeviceBean Data Model**


|     Field |  Type  |                         Description                      |
| ---- | ----| ----|
|    iconUrl | String |                         device icon                      |
|   getIsOnline | Boolean |      Whether the device is online (LAN or Cloud Online)  |
|     name  | String |                        device's name                     |
|    schema | String |          Device Control Data Point Type Information      |
|   productId  | String | Product ID, the same product ID, Schema information consistent |
| supportGroup | Boolean | whether the device support groups? If not, you can go to the open platform to turn on this feature |
|     Time  |  Long  |                    Device Activation Time                |
|      pv   | String |                   Gateway Protocol Version               |
|      bv   | String |              Gateway Universal Firmware Version          |
|   schemaMap  |   Map  |                      Schema Cached Data                  |
|      dps  |   Map  |                         Device Data                      |
|    isShare | Boolean |                       a shared device                    |
|    virtual | Boolean |                    is it a virtual device                |
|   lon, lat | String |              Longitude and Latitude Information          |
| IsLocalOnline | Boolean |                   Device LAN Online Status               |
|    nodeId | String | Device for gateway and subdevice type, which is an attribute of the subdevice and identifies its short address ID which one gateway have a unique nodeId for each subdevice |
|  timezoneId  | String |                       Device time zone                   |
|   category | String |                         Device Type                      |
|    MeshId | String | Device for gateway and subdevice type, which is an attribute of subdevice and identifies its gateway ID |
|     devId | String |                 Device unique identifier id              |
| isZigBeeWifi | boolean |                Is it a ZigBee gateway device?            |
|   hasZigBee  | boolean |                          hasZigBee                       |

**Notes**

 If device control need to use the latitude and longitude, you need to call the method to set the latitude and longitude:

```java
WiserSdk.setLatAndLong(String latitude, String longitude)
```

## Initialize Device

###  Initial Device Data

The device control must first initialize the data, and call the following method to get the device information in the home：

```java
WiserHomeSdk.newHomeInstance(homeId).getHomeDetail(new IWiserHomeResultCallback() {
    @Override
    public void onSuccess(HomeBean homeBean) {
    	
    }

    @Override
    public void onError(String errorCode, String errorMsg) {

    }
});
```

The `onSuccess` method of this interface will return `HomeBean`, and then call `getDeviceList` of `HomeBean` to get the device list:

```java
List<DeviceBean> deviceList = homeBean.getDeviceList();
```

### Initial Device Object

**Declaration**

Initialize the device control class based on the device id

```java
WiserHomeSdk.newDeviceInstance(String devId);
```

**Parameters**

| Parameters | Description|
| ---- | --- |
| devId |device id|

**Example**

```java
IWiserDevice mDevice = WiserHomeSdk.newDeviceInstance(deviceBean.getDevId());
```

## Device Data Listener

### Register 

**Declaration**

WiserHomeDevice provide monitoring of device related information (dp data, device name, device online status and device removal), which will be synchronized here in real time.

```java
IWiserDevice.registerDevListener(IDevListener listener)
```

**Parameters**

| Parameters |Description|
| ---- | --- |
| listener| device status listener|

`IDevListener` interface is as follows：

```java
public interface IDevListener {

    /**
     * dp data update
     *
     * @param devId device id
     * @param dpStr the function point of the device change. It is a json string with the data format: {"101": true}
     */
    void onDpUpdate(String devId, String dpStr);

    /**
     * Device removal callback
     *
     * @param devId device id
     */
    void onRemoved(String devId);

    /**
     * On device online/offline. If the device is powered off or disconnected from the network,
     * the server will call back to this method after 3 minutes.
     *
     * @param devId  Device id
     * @param online Is the device online
     */
    void onStatusChanged(String devId, boolean online);

    /**
     * network status changes
     *
     * @param devId  device id
     *  @param status Whether the network status is available, true is available
     */
    void onNetworkStatusChanged(String devId, boolean status);

    /**
     * Device information update callback
     *
     * @param devId  device id
     */
    void onDevInfoUpdate(String devId);

}
```

Among them, the description of the device function point is described in the "[Function Points of Device](#function-points-of-device)" in the next section of the document.

**Example**


```java
mDevice.registerDevListener(new IDevListener() {
    @Override
    public void onDpUpdate(String devId, String dpStr) {

    }
    @Override
    public void onRemoved(String devId) {

    }
    @Override
    public void onStatusChanged(String devId, boolean online) {

    }
    @Override
    public void onNetworkStatusChanged(String devId, boolean status) {

    }
    @Override
    public void onDevInfoUpdate(String devId) {

    }
});
```

Note: Do not use the `void registerDeviceListener(IDeviceListener listener)` method. This method needs to be used with standard device api. The api is not yet release.

### Unregister

When you do not need to listen to the device, you can unregister the device listener.

**Declaration**

```java
IWiserDevice.unRegisterDevListener()
```

**Example**


```java
mDevice.unRegisterDevListener();
```

## Device Control

The device control interface function is to send function points to the device to change the device status or function.

**Declaration**

Device control supports three kinds of channel control, LAN control, cloud control, and automatic mode (if LAN is online, first go LAN control, LAN is not online, go cloud control)

* control by local area network

  ```java
  IWiserDevice.publishDps(dps, TYDevicePublishModeEnum.TYDevicePublishModeLocal, callback);
  ```

* control by internet

  ```java
  IWiserDevice.publishDps(dps, TYDevicePublishModeEnum.TYDevicePublishModeInternet, callback);
  ```

* automatic control mode selection

  ```java
  IWiserDevice.publishDps(dps, TYDevicePublishModeEnum.TYDevicePublishModeAuto, callback);
  ```

  or

  ```java
  IWiserDevice.publishDps(dps, callback);
  ```

Recommended use `IWiserDevice.publishDps(dps, callback)`

**Parameters**

| Parameters | Description |
| ---- | --- |
| dps | data points, device function point, format is json string |
| publishModeEnum | device control mode |
| callback |Callback to send control instruction success|

**Example**

Assuming that the function point of the device that turns on the light is 101, the control code for turning on the light is as follows:

```java
mDevice.publishDps("{\"101\": true}", new IResultCallback() {
  @Override
  public void onError(String code, String error) {
  	Toast.makeText(mContext, "turn on the light failure", Toast.LENGTH_SHORT).show();
  }
  @Override
  public void onSuccess() {
  	Toast.makeText(mContext, "turn on the light success", Toast.LENGTH_SHORT).show();
  }
});
```

**[Notes]**

> * The successful issuing of a command does not mean that the device is successfully operated, but only means that the command has been successfully sent. If the operation succeeds, the dp data information will be reported, and returned through the IDevListener onDpUpdate interface.
>* The command string is converted to JsonString in the format of Map<String dpId,Object dpValue>.
> * The command can send multiple dp data at a time.

## Functions of Device

The dps attribute of the DeviceBean class defines the state of the device, and is called the data point (DP) or the function point. Each key in the dps dictionary refers to a dpId of a function point, and the dpValue is the value of the function point. Refer to the functions of product on the Wiser developer platformfor definition of function points of products. For details of function points, please refer to the Functional Point Related Concepts

**Command Format**

The control commands shall be sent in the format given below. {"(dpId)":"(dpValue)"}

**Example of Function Point**

A product interface on the development platform is as follows:![功能点](./img/2f5f50a3-59ff-4aaa-8f57-5348b6ef3789.png) 

According to the definition of function points of the product in the back end, the example codes is as follows.
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

mDevice.publishDps(dps, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
				        //Error code 11001
        //In the following cases:
        //1. Type error send to, for example, string type format, being        sent to boolean type data
        //2. Read-only type DP data can not be sent. Reference to SchemaBean getMode "ro" is read-only type.
        //3, raw format send data format is not a hexadecimal string.
        }
        @Override
        public void onSuccess() {
        }
});
```
**Notes**

- Special attention shall be paid to the type of data in sending the control commands. 
	 For example, the data type of function points shall be value, and {"104": 25} shall be sent as the control command, instead of {"104": "25"}.
- For the transparent transmission, the byte array shall be the string format, and the string must have even bits. 
	 The correct format shall be: {"105": "0110"}, instead of {"105": "110"}.

## Querying Device Information

**Declaration**

Query single dp data.

Query the latest data of the dp from the device; those data will be called back via the IDevicePanelCallback onDpUpdate interface.

```java
mDevice.getDp(String dpId, IResultCallback callback);
```

**Example**

```java
mDevice.getDp(dpId, new IResultCallback() {
    @Override
    public void onError(String code, String error) {

    }

    @Override
    public void onSuccess() {

    }
});
```

**Notes**

- This interface is mainly for the dp points where the data will not be reported automatically. The dp data values for regular query can be obtained through getDps() in DeviceBean.

## Modify the Device Name

**Declaration**

Device renaming can be conducted in multiple devices synchronously.

```java
// Rename
mDevice.renameDevice(String name,IResultCallback callback);
```

**Example**

```java
mDevice.renameDevice("device name", new IResultCallback() {
    @Override
    public void onError(String code, String error) {
        // Renaming failed
    }
    @Override
    public void onSuccess() {
        // Renaming succeeded
    }
});
```
After renaming succeeded, IDevListener.onDevInfoUpdate() will be notified.

Invoke the following method to get the latest data, and then refresh the device information.
```java
WiserHomeDataManager.getInstance().getDeviceBean(String devId);
```

## Remove Device

**Declaration**

It is used to remove a device from the list of user devices.

```java
/**
* Remove device
*
* @param callback
*/

void removeDevice(IResultCallback callback);
```
**Example**

```java
mDevice.removeDevice(new IResultCallback() {
    @Override
    public void onError(String errorCode, String errorMsg) {
    }
    @Override
    public void onSuccess() {
    }

});
```

## Restore Factory Settings

**Declaration**

Used to reset the device and restore the factory settings, After the device is restored to the factory settings, it will re-enter the network to be distributed state (smart config mode), and the relevant data of the device will be cleared.[]()

```java
void resetFactory(IResultCallback callback)；
```

**Example**

```java
mDevice.resetFactory(new IResultCallback() {
    @Override
    public void onError(String errorCode, String errorMsg) {
    }

    @Override
    public void onSuccess() {
    }
});
```


## Obtain Wi-Fi Signal Strength

**Declaration**

Query the signal strength of the current device's Wi-Fi

```java
void requestWifiSignal(WifiSignalListener listener);
```

**Example**

```java
mDevice.requestWifiSignal(new WifiSignalListener() {
     
     @Override
     public void onSignalValueFind(String signal) {
      
     }
     
     @Override
     public void onError(String errorCode, String errorMsg) {

     }
});
```

## Recycling Device Resources
**Declaration**

When the application or Activity is closed, this interface can be called to recycle the resources occupied by the device.

```java
void onDestroy()
```

**Example**

```java
mDevice.onDestroy();
```
