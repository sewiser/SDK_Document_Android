### Room Management

**RoomBean**

| Parameters | Type | Description |
| :--- | :--- | :--- |
| roomId | long  | Room id|
| name | String   | Room name|
| deviceList | List &lt;DeviceBean&gt;   | Devices of room |
| groupList | List &lt;GroupBean&gt;  | Groups of room |
| displayOrder | int | Room display order |

#### Update Room Name

**Declaration**

```java
void updateRoom(String name, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| name | New room name |

**Example**

```java
WiserHomeSdk.newRoomInstance(10000).updateRoom(name, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### Update Room Icon

The room can support upload custom image, after success, you can get the room icon URL through `RoomBean.iconUrl`

**Declaration**

```java
void updateIcon(File file, IResultCallback callback);
```

**Parameters**

| Parameters | Description |
| ---------- | ----------- |
| file       | Room image  |
| callback   | callback    |

**Example**

```java
WiserHomeSdk.newRoomInstance(10000).updateIcon(file, new IResultCallback() {
        @Override
        public void onSuccess() {
            // do something
        }
        @Override
        public void onError(String code, String error) {
            // do something
        }
    });
```

#### Add Device

**Declaration**

```java
void addDevice(String devId, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| devId | Device ID |

**Example**

```java
WiserHomeSdk.newRoomInstance(10000).addDevice(devId, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### Delete Device

**Declaration**

```java
void removeDevice(String devId, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| devId | Device ID |

**Example**

```java
WiserHomeSdk.newRoomInstance(10000).removeDevice(devId, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```
#### Add Group

**Declaration**

```java
void addGroup(long groupId, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--------- | :---------- |
| groupId    | Group ID    |

**Example**

```java
WiserHomeSdk.newRoomInstance(10000).addGroup(groupId, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### 

#### Delete Group

**Declaration**

```java
void removeGroup(Long groupId, IResultCallback resultCallback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| groupId | Group ID |

**Example**

```java
WiserHomeSdk.newRoomInstance(10000).removeGroup(groupId, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### Remove Group or Device From Room

**Declaration**

```java
void moveDevGroupListFromRoom(List list, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| list | Group or device |

**Example**

```java
WiserHomeSdk.newRoomInstance(10000).moveDevGroupListFromRoom(list, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

#### Sort Groups or Devices in a Room

**Declaration**

```java
void sortDevInRoom(List<DeviceAndGroupInRoomBean> list, IResultCallback callback)
```

**Parameters**

| Parameters | Description |
| :--- | :--- |
| list | Group or device |

**Example**

```java
WiserHomeSdk.newRoomInstance(10000).sortDevInRoom(list, new IResultCallback() {
        @Override
        public void onError(String code, String error) {
            // do something
        }
        @Override
        public void onSuccess() {
            // do something
        }
    });
```

## Home Weather

### Get Home's Weather Simple Summary Parameters

Sush as state of weather(clear, cloudy, rainy, and so on),weather icon.

**Declaration**

```java
void getHomeWeatherSketch(double lon,double lat,IIGetHomeWetherSketchCallBack callback);
```

**Parameters**

| **Parameters** | **Description** |
| -------------- | --------------- |
| lon            | longitude       |
| lat            | latitude        |
| callback       | callback        |

WeatherBean Description

| **Parameters** | **Description**     |
| -------------- | ------------------- |
| condition      | weather description |
| temp           | temperature         |
| iconUrl        | weather icon        |
| inIconUrl      | weather icon        |

**Example**

```java
WiserHomeSdk.newHomeInstance(mHomeId).getHomeWeatherSketch(120.075652,30.306265
  new IIGetHomeWetherSketchCallBack() {
    @Override
    public void onSuccess(WeatherBean result) {
    }
    @Override
    public void onFailure(String errorCode, String errorMsg) {
    }
  });
```

### Get Home's Weather Summary Parameters with More Detail

Such as tempature, humidity, ultraviolet index, air quality.

**Declaration**

```java
void getHomeWeatherDetail(int limit, Map<String,Object> unit, IGetHomeWetherCallBack callback);
```

**Parameters**

| **Parameters** | **Description** |
| :------------- | :-------------- |
| limit          | list count      |
| unit           | parameter unit  |
| callback       | callback        |

More explanations about the unit:

| key      | value                       |
| -------- | --------------------------- |
| tempUnit | Celsius：1<br>Fahrenheit：2 |

For example, when the unit of the data you want to obtain is Celsius unit:

```java
Map<String,Object> units = new HashMap<>();
units.put("tempUnit",1);
```

**Example**

```java
Map<String,Object> units = new HashMap<>();
units.put("tempUnit",1);

WiserHomeSdk.newHomeInstance(mHomeId).getHomeWeatherDetail(10, units, new IGetHomeWetherCallBack() {
    @Override
    public void onSuccess(ArrayList<DashBoardBean> result) {

    }

    @Override
    public void onFailure(String errorCode, String errorMsg) {

    }
});
```
