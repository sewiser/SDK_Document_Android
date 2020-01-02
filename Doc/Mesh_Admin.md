# Management
### Create Mesh

##### 【Method Invocation】
```java
* @param meshName   mesh name（no more than 16 bytes）
* @param callback   
void createBlueMesh(String meshName, IWiserResultCallback<BlueMeshBean> callback);
```

##### 【Example Codes】
``` java
WiserHomeSdk.newHomeInstance("homeId").createBlueMesh("meshName", new IWiserResultCallback<BlueMeshBean>() {
    @Override
    public void onError(String errorCode, String errorMsg) {
        Toast.makeText(mContext, "create mesh fail "+ errorMsg, Toast.LENGTH_LONG).show();
    }

    @Override	
    public void onSuccess(BlueMeshBean blueMeshBean) {
        Toast.makeText(mContext, "creat mesh success", Toast.LENGTH_LONG).show();
    }
});
```

### Remove Mesh

##### 【Example Codes】
```java
WiserHomeSdk.newBlueMeshDeviceInstance(meshId).removeMesh(new IResultCallback() {
    @Override
    public void onError(String errorCode, String errorMsg) {
	    Toast.makeText(mContext, "remove mesh fail "+ errorMsg, Toast.LENGTH_LONG).show();
    }
	
    @Override
    public void onSuccess() {
	    Toast.makeText(mContext, "remove mesh success ", Toast.LENGTH_LONG).show();
    }
});

```

### Get Mesh Data From Cache
##### 【Method Invocation】
```java
WiserHomeSdk.newHomeInstance("homeId").getHomeBean().getMeshList()
```
##### 【Example Codes】
```java
IWiserHome mWiserHome = WiserHomeSdk.newHomeInstance("homeId");
if (mWiserHome.getHomeBean() != null){
	List<BlueMeshBean> meshList = mWiserHome.getHomeBean().getMeshList();
	BlueMeshBean meshBean= meshList.get(0);
}            
```

###  Get Mesh Sub-device Data From Cache 
##### 【Example Codes】
```java
List<DeviceBean> meshSubDevList = WiserHomeSdk.newBlueMeshDeviceInstance("meshId").getMeshSubDevList();
    
```


### Mesh Initialization And Destruction
建议在家庭切换的时候 销毁当前mesh  然后重新初始化家庭中的mesh

##### 【Method Invocation】
```java
//初始化mesh
WiserHomeSdk.getWiserBlueMeshClient().initMesh(String meshId);       

//销毁当前mesh
WiserHomeSdk.getWiserBlueMeshClient().destroyMesh();       
```


### Mesh Sub-device Connect And Disconnect
##### 【Description】
IWiserBlueMeshClientProvides start connection, disconnect, start scan, stop scan

##### 【Method Invocation】

```java
// start connection
WiserHomeSdk.getWiserBlueMeshClient().startClient(mBlueMeshBean);

//disconnect
WiserHomeSdk.getWiserBlueMeshClient().stopClient();

//start scan
WiserHomeSdk.getWiserBlueMeshClient().startSearch()

//stop scan
WiserHomeSdk.getWiserBlueMeshClient().stopSearch();

```

##### 【Precautions】 
###### startClient(mSigMeshBean) After opening the connection, it will continuously scan the surrounding connectable devices in the background until the connection is successful.

###### startClient(mSigMeshBean,searchTime) After the connection is opened, the device will not be scanned within the search time.

###### Scanning in the background always consumes resources. You can control scanning in the background by startSearch and stopSearch.

###### When startClient () is not started, calling startSearch () and stopSearch () has no effect.

###### When connected to the mesh network, calling startSearch and stopSearch has no effect.
