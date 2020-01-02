## Gateway

The gateway class encapsulates the operations of the ZigBee gateway, including control, querying sub-devices and monitoring sub-device status. The gateway can be initialized via WiserHomeSdk.newGatewayInstance().

```java
public interface IWiserGateway {
     /**
      * Send command
      * 
      * @param dps
      * @param callback
      */
     void publishDps(String nodeId, String dps, IResultCallback callback);
    /**
      * Broadcast control device
      *
      * @param dps
      * @param callback
      */
     void broadcastDps(String dps, IResultCallback callback);
     /**
      * Multicast control device
      *
      * @param localId
      * @param dps
      * @param callback
      */
     void multicastDps(String localId, String dps, IResultCallback callback);
     /**
      * Obtain the sub-device of a gateway from cloud
      *
      * @param callback
      */
     void getSubDevList(IWiserDataCallback<List<DeviceBean>> callback);
     /**
      * Change of registered sub-device information 
      *
      * @param listener
      */
     void registerSubDevListener(ISubDevListener listener);
     /**
     * Change of logout sub-device information
      */
     void unRegisterSubDevListener();
}
```

### ISubDevListener

#### Description

```java

public interface ISubDevListener {

    /**
     * Device dps change
     *
     * @param nodeId
     * @param dpStr
     */
    void onSubDevDpUpdate(String nodeId, String dpStr);

    /**
     * Device removed
     */
    void onSubDevRemoved(String devId);

    /**
     * Device added
     *
     * @param devId
     */
    void onSubDevAdded(String devId);

    /**
     * Device information updates such as name
     */
    void onSubDevInfoUpdate(String devId);
    
    /**
     * Subdevices  online and offline status
     */
     
    void onSubDevStatusChanged(List<String> onlineNodeIds, List<String> offlineNodeIds);
}


```
