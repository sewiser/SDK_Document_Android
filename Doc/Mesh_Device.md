## Device

### Mesh Device Judgment Method
##### 【Example Codes】

```java
DeviceBean deviceBean=WiserHomeSdk.getDataInstance().getDeviceBean(mDevId);
// Determine whether it is a bluemesh device (child device + gateway)
if(deviceBean.isBlueMesh()){
    L.d(TAG, "This device is blue mesh device");
 }

// Determine if it is a bluemesh gateway device
if(deviceBean.isBlueMeshWifi()){
    L.d(TAG, "This device is blue mesh wifi device");
 }
```
###  Sub-device Rename
##### 【Method Invocation】
```java
* @param devId    	 device id
* @param name		     new name
* @param callback	
public void renameMeshSubDev(String devId, String name, IResultCallback callback);

```

##### 【Example Codes】
```java
mWiserBlueMesh.renameMeshSubDev(devBean.getDevId(),"new name", new IResultCallback() {
            @Override
            public void onError(String code, String errorMsg) {
            		Toast.makeText(mContext, "rename failed "+ errorMsg, Toast.LENGTH_LONG).show();
            }

            @Override
            public void onSuccess() {
            		Toast.makeText(mContext, "rename success", Toast.LENGTH_LONG).show();
            }
        });
```

###  Sub-device Remove
#####  【Method Invocation】
```java
* @param devId    	 device id
* @param pcc  		   device category
* @param callback	
public void removeMeshSubDev(String devId, IResultCallback callback) ;

```
#####  【Example Codes】
```java
mWiserBlueMesh.removeMeshSubDev(devBean.getDevId(),devBean.getCategory(), new IResultCallback() {
            @Override
            public void onError(String code, String errorMsg) {
            		Toast.makeText(mContext, "remove fail "+ errorMsg, Toast.LENGTH_LONG).show();
    
            }

            @Override
            public void onSuccess() {
            		Toast.makeText(mContext, "remove success", Toast.LENGTH_LONG).show();
            }
        });
```

### Query of a Single Sub-device Information
##### 【Description】
The dp point data obtained in the cloud may not be the real-time data of the current device. You can use this command to query the current data value of the device. The result is returned by the onDpUpdate method of IMeshDevListener.

#####  【Method Invocation】
```java
* @param pcc  		   device categoty
* @param nodeId    	 device nodeId
* @param callback
public void querySubDevStatusByLocal(String pcc, final String nodeId, final IResultCallback callback);

```

#####  【Example Codes】
```java
 mWiserBlueMeshDevice.querySubDevStatusByLocal(devBean.getCategory(), devBean.getNodeId(), new IResultCallback() {
            @Override
            public void onError(String code, String errorMsg) {
            		Toast.makeText(mContext, "query failed "+ errorMsg, Toast.LENGTH_LONG).show();
            }

            @Override
            public void onSuccess() {
            		Toast.makeText(mContext, "query success ", Toast.LENGTH_LONG).show();
            }
        });
```
