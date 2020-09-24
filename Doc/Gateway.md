# Zigbee Gateway Control

The gateway itself is also a device. If you want to control the gateway itself, you can refer to the previous chapter.

This section describes the sub-devices under the control gateway.

|  ClassName   | Description                                                  |
| :----------: | :----------------------------------------------------------- |
| IWiserGateway | The gateway class encapsulates the related operations of the Zigbee gateway, including controlling, querying sub-devices, and monitoring the status of the sub-devices. |

## Initialize the Gateway

**Declaration**

Create a gateway instance to control sub-devices.

```java
WiserHomeSdk.newGatewayInstance(String devId)
```

**Parameters**

| Parameters | Description              |
| ---------- | ------------------------ |
| devId      | Device id of the gateway |

## Get Sub-devices

**Declaration**

Request the server interface to get the list of child devices of the current gateway device.

```java
void getSubDevList(IWiserDataCallback<List<DeviceBean>> callback)
```

**Parameters**

The parameter of this interface is the callback of asynchronous callback. The content of callback is as follows:

```java
public interface IWiserDataCallback<List<DeviceBean>> {
  
    void onSuccess(List<DeviceBean> result);

    void onError(String errorCode, String errorMessage);
  
}
```

A list of device information will be returned upon success.

**Example**

```java
WiserHomeSdk.newGatewayInstance(devId).getSubDevList(new IWiserDataCallback<List<DeviceBean>>() {
    @Override
    public void onSuccess(List<DeviceBean> list) {
    }

    @Override
    public void onError(String errorCode, String errorMessage) {

    }
});
```

## Register Sub-device Listener

**Declaration**

Register the sub-device status listener, and the change of the sub-device status will be callback to the asynchronous listener.

```java
void registerSubDevListener(ISubDevListener listener);
```

**Parameters**

The contents of the listener interface as follows:

```java
public interface ISubDevListener {

    /**
     * Called when device dp point status changes
     *
     * @param nodeId sub-device nodeId, nodeId field in sub-device's DeviceBean
     * @param dpStr 子设备变更的功能点数据
     */
    void onSubDevDpUpdate(String nodeId, String dpStr);

    /**
     * Called when device is removed
     */
    void onSubDevRemoved(String devId);

    /**
     * Called when adding a device
     */
    void onSubDevAdded(String devId);

    /**
     * Called when child device is renamed
     */
    void onSubDevInfoUpdate(String devId);
    
    /**
     * Called when sub-device online or offline status change
     */
    void onSubDevStatusChanged(List<String> onlineNodeIds, List<String> offlineNodeIds);
}
```

**Example**

```java
WiserHomeSdk.newGatewayInstance(devId).registerSubDevListener(new ISubDevListener() {
    @Override
    public void onSubDevDpUpdate(String nodeId, String dpStr) {
        
    }

    @Override
    public void onSubDevRemoved(String devId) {

    }

    @Override
    public void onSubDevAdded(String devId) {

    }

    @Override
    public void onSubDevInfoUpdate(String devId) {

    }

    @Override
    public void onSubDevStatusChanged(List<String> onlines, List<String> offlines) {

    }
});
```

## Unregister Sub-device Listener

**Declaration**

When you do not need to listen to the sub-device, unregister sub-device listener.

```java
void unRegisterSubDevListener();
```

**Example**

```java
WiserHomeSdk.newGatewayInstance(devId).unRegisterSubDevListener();
```

## Single Sub-device Control

**Declaration**

Send control instructions to a single sub-device.

```java
void publishDps(String nodeId, String dps, IResultCallback callback)
```

**Parameters**

| Parameters | Description                                                  |
| ---------- | ------------------------------------------------------------ |
| nodeId     | sub-device nodeId, nodeId field in sub-device's DeviceBean   |
| dps        | List of function points to be controlled, formatted as json string |
| callback   | Send success or failure callback                             |

**Example**

```java
WiserHomeSdk.newGatewayInstance(devId).publishDps(subDeviceBean.getNodeId(), "{\"101\": true}", new IResultCallback() {
    @Override
    public void onError(String code, String error) {

    }

    @Override
    public void onSuccess() {

    }
});
```

## Sub-device Group Control

**Declaration**

Control all devices in the same group as this sub-device.

```java
void multicastDps(String nodeId, String dps, IResultCallback callback)
```

**Parameters**

| Parameters | Description                                                  |
| ---------- | ------------------------------------------------------------ |
| nodeId     | sub-device nodeId, nodeId field in sub-device's DeviceBean   |
| dps        | List of function points to be controlled, formatted as json string |
| callback   | Send success or failure callback                             |

**Example**

```java
WiserHomeSdk.newGatewayInstance(devId).multicastDps(subDeviceBean.getNodeId(), "{\"101\": true}", new IResultCallback() {
    @Override
    public void onError(String code, String error) {

    }
    
    @Override
    public void onSuccess() {
    
    }

});
```

## Sub-device Broadcast Control

**Declaration**

Controls all sub-devices under the gateway.

```
void broadcastDps(String dps, IResultCallback callback)
```

**Parameters**

| Parameters | Description                                                  |
| ---------- | ------------------------------------------------------------ |
| dps        | List of function points to be controlled, formatted as json string |
| callback   | Send success or failure callback                             |

**Example**

```java
WiserHomeSdk.newGatewayInstance(devId).broadcastDps("{\"101\": true}", new IResultCallback() {
    @Override
    public void onError(String code, String error) {

    }
    
    @Override
    public void onSuccess() {
    
    }

});
```

