### Family Management

Create and query family information change monitor

#### Destruction

**Declaration**

```java
void onDestroy()
```

**Example**

```java
WiserHomeSdk.getHomeManagerInstance().onDestroy();
```

#### Create family

**Declaration**

```java
void createHome(String name, double lon, double lat, String geoName, List rooms, IWiserHomeResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| name | Family name |
| lon | longitude |
| lat | latitude |
| geoName | Home location name |
| rooms | Room list |
| callback | Result callback |

**Example**

```java
WiserHomeSdk.getHomeManagerInstance().createHome(name, lon, lat, geoName, rooms, new IWiserHomeResultCallback() {
        @Override
        public void onError(String errorCode, String errorMsg) {
            // do something
        }
        @Override
        public void onSuccess(HomeBean bean) {
            // do something
        }
    });
```

#### Get Family List

**Declaration**

```java
void queryHomeList(IWiserGetHomeListCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| callback | Result callback |

**Example**

```java
WiserHomeSdk.getHomeManagerInstance().queryHomeList(new IWiserGetHomeListCallback() {
        @Override
        public void onError(String errorCode, String error) {
            // do something
        }
        @Override
        public void onSuccess(List<HomeBean> homeBeans) {
            // do something
        }
    });
```

#### Change of Registered Family Information

There are: addition and deletion of family, information change, change of sharing list and successful monitoring of server connection

**Declaration**

```java
void registerWiserHomeChangeListener(IWiserHomeChangeListener listener)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| listener | Monitor |

**Example**

```java
// define a listener
IWiserHomeChangeListener listener = new IWiserHomeChangeListener() {
        @Override
        public void onHomeInvite(long homeId, String homeName) {
            // do something
        }
        @Override
        public void onHomeRemoved(long homeId) {
            // do something
        }
        @Override
        public void onHomeInfoChanged(long homeId) {
            // do something
        }
        @Override
        public void onSharedDeviceList(List<DeviceBean> sharedDeviceList) {
            // do something
        }
        @Override
        public void onSharedGroupList(List<GroupBean> sharedGroupList) {
            // do something
        }
        @Override
        public void onServerConnectSuccess() {
            // do something
        }
        @Override
        public void onHomeAdded(long homeId) {
            // do something
        }
    };
// register a listener
WiserHomeSdk.getHomeManagerInstance().registerWiserHomeChangeListener(listener);
```

#### Change of Cancellation Family Information

**Declaration**

```java
void unRegisterWiserHomeChangeListener(IWiserHomeChangeListener listener)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| listener | Monitor |

**Example**

```java
// define a listener
IWiserHomeChangeListener listener = new IWiserHomeChangeListener() {
        @Override
        public void onHomeInvite(long homeId, String homeName) {
            // do something
        }
        @Override
        public void onHomeRemoved(long homeId) {
            // do something
        }
        @Override
        public void onHomeInfoChanged(long homeId) {
            // do something
        }
        @Override
        public void onSharedDeviceList(List<DeviceBean> sharedDeviceList) {
            // do something
        }
        @Override
        public void onSharedGroupList(List<GroupBean> sharedGroupList) {
            // do something
        }
        @Override
        public void onServerConnectSuccess() {
            // do something
        }
        @Override
        public void onHomeAdded(long homeId) {
            // do something
        }
    };
// register a listener
WiserHomeSdk.getHomeManagerInstance().registerWiserHomeChangeListener(listener);
// ...
// unregister a listener
WiserHomeSdk.getHomeManagerInstance().unRegisterWiserHomeChangeListener(listener);
```


