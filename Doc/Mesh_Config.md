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

SearchBuilder searchBuilder = new SearchBuilder()
				.setMeshName("out_of_mesh")        //To scan the name of the device (the default will be out_of_mesh, the name of the device in the unconfigured state)
                .setTimeOut(100)        //Scan duration in seconds
                .setWiserBlueMeshSearchListener(iWiserBlueMeshSearchListener).build();

IWiserBlueMeshSearch mMeshSearch = WiserHomeSdk.getWiserBlueMeshConfig().newWiserBlueMeshSearch(searchBuilder);

//start search
mMeshSearch.startSearch();

//stop search
mMeshSearch.stopSearch();
```

### Sub-device Configuration
##### 【Description】
There are two types of sub-device configuration, one is common device access, and the other is mesh gateway access.

##### 【Initial parameter configuration】
```java
//common sub-device configuration parameter
WiserBlueMeshActivatorBuilder wiserBlueMeshActivatorBuilder = new WiserBlueMeshActivatorBuilder()
            .setSearchDeviceBeans(mSearchDeviceBeanList)
            //default version number
            .setVersion("1.0")
            .setBlueMeshBean(mMeshBean)
            .setTimeOut(CONFIG_TIME_OUT)  //scan duration in seconds
            .setWiserBlueMeshActivatorListener();
            
//Mesh gateway configuration parameter    
WiserBlueMeshActivatorBuilder wiserBlueMeshActivatorBuilder = new WiserBlueMeshActivatorBuilder()
            .setWifiSsid(mSsid)
            .setWifiPassword(mPassword)     
            .setSearchDeviceBeans(mSearchDeviceBeanList)
            .setVersion("2.2")
            .setBlueMeshBean(mMeshBean)
            .setHomeId("homeId")
        	  .setTimeOut(CONFIG_TIME_OUT)
            .setWiserBlueMeshActivatorListener();
```

##### 【参数说明】
###### 【入参】
```java
* @param mSearchDeviceBeans     list of device to be configured
* @param timeout   Timeout setting for network configuration, default is 100s
* @param ssid        Name of the Wifi used by devices in working after the network isconfigured.  (Home network)
* @param password   Password of the Wifi used by devices in working after the network is configured.  (Home network)
* @param mMeshBean  MeshBean 
* @param homeId     join homeId
* @param version    Common device is 1.0 , gateway is 2.2
```

###### 【出参】
IWiserBlueMeshActivatorListener listener configuration callback

```java
//single device configuration failed callback
void onError(String errorCode, String errorMsg);

@param errorCode:
13007       login failed
13004       reset device address failed
13005       device address allocation is full
13007       ssid is empty 
13011       configuration time out

//single device configuration success callback
void onSuccess(DeviceBean deviceBean);

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
//common sub-device configuration
WiserBlueMeshActivatorBuilder wiserBlueMeshActivatorBuilder = new WiserBlueMeshActivatorBuilder()
                .setSearchDeviceBeans(foundDevices)
                .setVersion("1.0")
                .setBlueMeshBean(mMeshBean)
                .setTimeOut(timeOut)
                .setWiserBlueMeshActivatorListener(new IWiserBlueMeshActivatorListener() {
                    @Override
                    public void onSuccess(DeviceBean deviceBean) {
                        L.d(TAG, "subDevBean onSuccess: " + deviceBean.getName());
                    }

                    @Override
                    public void onError(String errorCode, String errorMsg) {
                        L.d(TAG, "config mesh error" + errorCode + " " + errorMsg);
                    }

                    @Override
                    public void onFinish() {
                        L.d(TAG, "config mesh onFinish： ");
                    }
                });
IWiserBlueMeshActivator iWiserBlueMeshActivator = WiserHomeSdk.getWiserBlueMeshConfig().newActivator(wiserBlueMeshActivatorBuilder);

iWiserBlueMeshActivator.startActivator();


//gateway sub-device configuration
WiserBlueMeshActivatorBuilder wiserBlueMeshActivatorBuilder = new WiserBlueMeshActivatorBuilder()
                .setWifiSsid(mSsid)
                .setWifiPassword(mPassword)
                .setSearchDeviceBeans(foundDevices)
                .setVersion("2.2")
                .setBlueMeshBean(mMeshBean)
                .setHomeId("homeId")
                .setWiserBlueMeshActivatorListener(new IWiserBlueMeshActivatorListener() {

                    @Override
                    public void onSuccess(DeviceBean devBean) {
                        L.d(TAG, "startConfig  success");
                    }

                    @Override
                    public void onError(String errorCode, String errorMsg) {
                        L.d(TAG, "errorCode: " + errorCode + " errorMsg: " + errorMsg);
                    }

                    @Override
                    public void onFinish() {
                        L.d(TAG, "subDevBean onFinish: ");             
                    }
                });
IWiserBlueMeshActivator iWiserBlueMeshActivator = WiserHomeSdk.getWiserBlueMeshConfig().newWifiActivator(wiserBlueMeshActivatorBuilder);
iWiserBlueMeshActivator.startActivator();

```
