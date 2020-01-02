# Device data stream channel

It is mainly used for a large number of real-time reporting scenarios such as sweeper map data.

```java
IWiserSingleTransfer singleTransfer = WiserHomeSdk.getTransferInstance();
```

```java
public interface IWiserSingleTransfer {
    /**
     * 开始连接
     */
    void startConnect();

    /**
     * 是否在线
     */
    boolean isOnline();

    /**
     * 订阅设备数据，订阅设备之后，设备如果有数据上报上来，便可以通过 registerTransferDataListener 回调上来。需要注意的是，每次通道连接成功都需要重新订阅设备数据
     */
    void subscribeDevice(String devId);

    /**
     * 取消订阅设备信息，则设备数据不在收到
     *
     */
    void unSubscribeDevice(String devId);

    /**
     * 注册设备数据流，SDK不做数据解析，具体格式需要和硬件上报方协商一致，然后解析。
     */
    void registerTransferDataListener(IWiserDataCallback<TransferDataBean> callback);
    /**
     * 取消订阅设备数据流
     */
    void unRegisterTransferDataListener(IWiserDataCallback<TransferDataBean> callback);

    /**
     * 注册通道状态变化，在网络波动的情况下会导致通道断开重连的情况 
     */
    void registerTransferCallback(IWiserTransferCallback callback);

    /** 取消注册
    */
    void unRegisterTransferCallback(IWiserTransferCallback callback);

    /**
        断开数据流通道
    */
    void stopConnect();
}
```

##  Data Model

### DeviceBean

- iconUrl: address of device icon link
- devId: unique id of device
- isOnline: is the device online? (via LAN or cloud)
- name: device name
- schema: attribute of dp point of device
- productId: unique id of product
- pv: version of gateway communication protocol (expressed as x.x).
- bv: version of common firmware for gateway (expressed as x.x).
- time: time of adding the device
- isShare: is the device shared?
- schemaMap: type of Map; key: dpId; value: Schema data.
- dps: current data information of the device. key: dpId; value: value.
- Lon and lat: longitude and latitude (before using sdk, the user shall invoke WiserSdk.setLatAndLong to set the information about the longitude and latitude).
- isZigBeeWifi: is it a ZigBee gateway device?
- HasZigBee: does it have ZigBee capabilities? (gateway device or sub-device)
