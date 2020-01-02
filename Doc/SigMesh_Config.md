## Configuration

### Scan nearby sub-devices to be configured
##### 【Description】
Need to check Bluetooth and location permissions before scanning

##### 【Method Invocation】
```java
//start search
mMeshSearch.startSearch();
//stop search
mMeshSearch.stopSearch();

```
##### 【Example Codes】
```java
IWiserBlueMeshSearchListener iWiserBlueMeshSearchListener=new IWiserBlueMeshSearchListener() {
    @Override
    public void onSearched(SearchDeviceBean deviceBean) {

    }

    @Override
    public void onSearchFinish() {

    }
};
// The UUID of the SigMesh device to be deployed is fixed
UUID[] MESH_PROVISIONING_UUID = {UUID.fromString("00001827-0000-1000-8000-00805f9b34fb")};
SearchBuilder searchBuilder = new SearchBuilder()
								.setServiceUUIDs(MESH_PROVISIONING_UUID)
                .setTimeOut(100)        //scan duration in seconds
                .setWiserBlueMeshSearchListener(iWiserBlueMeshSearchListener).build();

IWiserBlueMeshSearch mMeshSearch = WiserHomeSdk.getWiserBlueMeshConfig().newWiserBlueMeshSearch(searchBuilder);

//start search
mMeshSearch.startSearch();

//stop search
mMeshSearch.stopSearch();
```

### Sub-device Configuration

#### By mobile phone's Bluetooth channel

##### 【Initial parameter configuration】
```java
WiserSigMeshActivatorBuilder wiserSigMeshActivatorBuilder = new WiserSigMeshActivatorBuilder()
            .setSearchDeviceBeans(mSearchDeviceBeanList)
            .setSigMeshBean(sigMeshBean)
            .setTimeOut(CONFIG_TIME_OUT)  // time out
            .setWiserBlueMeshActivatorListener();
```

##### 【Parameter Description】
###### 【Entry parameters】
```java
* @param mSearchDeviceBeans     list of device to be configured,get by startSearch
* @param timeout    Timeout setting for network configuration, default is 100s (when there are too many devices for one-time network configuration, you need to increase the time)
* @param sigMeshBean  SigMeshBean   
```

###### 【Back parameters】
IWiserBlueMeshActivatorListener listener configuration callback

```java
//single device configuration failed callback
void onError(String mac, String errorCode, String errorMsg);

@param errorCode:
21002       invite failed
21004       provision failed
21006       send public key failed
21008       conform failed
210010      random conform failed
210014      send data failed
210016      composition data failed
210018      add appkey failed
210020      bind model failed
210022      publication model failed
210024      network transmit failed
210026      cloud registration failed
210027      device address allocation is full
210034      notify failed
20021       configuration time out

//single device configuration success callback
void onSuccess(String mac, DeviceBean deviceBean);

//configuration finish callback
void onFinish();

```

##### 【Method Invocation】

```java
//start activator
iWiserBlueMeshActivator.startActivator();

//stop activator
iWiserBlueMeshActivator.stopActivator();
```

##### 【Example Codes】
```java
//sub-device configuration
WiserSigMeshActivatorBuilder wiserSigMeshActivatorBuilder = new WiserSigMeshActivatorBuilder()
            .setSearchDeviceBeans(mSearchDeviceBeanList)
            .setSigMeshBean(sigMeshBean)
            .setTimeOut(CONFIG_TIME_OUT)
            .setWiserBlueMeshActivatorListener(new IWiserBlueMeshActivatorListener() {
                    @Override
                    public void onSuccess(String mac, DeviceBean deviceBean) {
                        L.d(TAG, "subDevBean onSuccess: " + deviceBean.getName());
                    }

                    @Override
                    public void onError(String mac, String errorCode, String errorMsg) {
                        L.d(TAG, "config mesh error" + errorCode + " " + errorMsg);
                    }

                    @Override
                    public void onFinish() {
                        L.d(TAG, "config mesh onFinish： ");
                    }
                });
IWiserBlueMeshActivator iWiserBlueMeshActivator = WiserHomeSdk.getWiserBlueMeshConfig().newActivator(wiserBlueMeshActivatorBuilder);

iWiserBlueMeshActivator.startActivator();

```

#### By Gateway Channel
same as  [ZigBee Sub-device Configuration](./Activator_ZigbeeSub.md)

### Gateway Configuration
same as  [AP Mode Configuration](./Activator_wifi.md#EZ Mode Configuration)
