# Timer Task

Wiser Smart provides basic timing capabilities and supports devices (including WiFi devices, Bluetooth mesh sub-devices, and Zigbee sub-devices) and groups. It is also provided with the interface for addition, deletion, change, and querying of timer information for DP of the device. After the APP sets the timer information through the timing interface, the hardware module automatically performs the scheduled operation according to the timing requirements. Multiple timers can be included in each timer task, as shown in the figure below:

![](./img/a8ba7dda-7928-4180-99fc-34a41de20226.jpg)

| Class           | Description     |
| ---- | ---- |
| IWiserCommonTimer | Timer package class |

All methods related to timing are included in WiserHomeSdk.getTimerManagerInstance().

The taskName is used by multiple interfaces, which can be described as a group, and a group may include multiple timers. Each timer task belongs to or does not belong to a group, and the group is currently only used for presentation.

## Version Imprint


A new set of timing interfaces has been added from version 3.18.0 to solve the problems of the old interface, 

The new timer apis are all in `WiserHomeSdk.getTimerInstance()`,

The old timer apis are in `WiserHomeSdk.getTimerManagerInstance()`

Compared with the old version of the interface, the new version of the interface has the following updates:

- Add or update the timer interface to set the timer switch state

- Provide an interface for batch modification of timer status
- Fix the problem of the failure of the old version to close the timer categories
- Provide category timers delete function

**Upgrade suggestion**

The old interface is no longer maintained, and it is recommended to upgrade to the new interface. The upgrade needs to replace the entire set of timing interfaces. Using the old version of the interface to set the timing can still be obtained through the new version of the timer list.

## Add Timer Task

Up to 30 timers per device or group

Add a timer to the required task specified by a device or group.

**Declaration**

```java
void addTimer(WiserTimerBuilder builder, final IResultCallback callback);
```


**Parameters**

WiserTimerBuilder and IResultCallback description

| Parameters    | Description                                        |
| ---- | ---- |
| taskName | Name of timer task                         |
| devId | Device Id or group Id|
| loops | Execute the timer times of a week. a number of loops: "0000000”; 0 denotes off, and 1 denotes on. Each 0 from the left to the right denotes Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, and Saturday, respectively."0000000" means execute once."1111111" means execute everyday                           |
| actions		 |dps task, json format: {/"dps/":{},/"time/":””}, the dp of the raw type needs format conversion：`new String(Base64.encodeBase64(HexUtil.hexStringToBytes(dps)))` |
| status		 | Initialize the timer switch state 0: off, 1: on|
| appPush | Is support push message after the timer executed (The app must be supported FCM)|
| aliasName | The timer remark name |
| timerDeviceTypeEnum | Enumeration, timing type: device timing or group timing|
| callback | callback not null|


**Example**

```java
WiserTimerBuilder builder = new WiserTimerBuilder.Builder()
        .taskName(mTaskName)
        .devId(id)
        .deviceType(TimerDeviceTypeEnum.DEVICE)
        .actions(dps)
        .loops("1100011")
        .aliasName("Test")
        .status(1)
        .appPush(true)
        .build();
WiserHomeSdk.getTimerInstance().addTimer(builder, new IResultCallback() {
    @Override
    public void onSuccess() {
            }

    @Override
    public void onError(String errorCode, String errorMsg) {
        
    }
});
```



## Batch Modify Common Timers Status or Delete Dimer

**Declaration**

```java
void updateTimerStatus(String devId, TimerDeviceTypeEnum deviceTimerTypeEnum, List<String> ids, TimerUpdateEnum timerUpdateEnum, final IResultCallback callback);
```

**Parameters**

| Parameters    | Description |
| ---- | ---- |
| devId | Device Id or group Id|
| TimerDeviceTypeEnum | Enumeration, timing type: device timing or group timing |
| ids 	 | Timer id list |
| TimerUpdateEnum |  Enumeration, operation type: turn on timer, turn off timer, delete timer |
| callback | callback not null|

**Example**

```java
WiserHomeSdk.getTimerInstance().updateTimerStatus(mDevId, TimerDeviceTypeEnum.DEVICE, list, TimerUpdateEnum.DELETE, new IResultCallback() {
    @Override
    public void onError(String code, String error) {
        
    }

    @Override
    public void onSuccess() {
        
    }
});
```

## Update Timer 

Update the timer of a task specified by a device.


**Declaration**

Updating timer status (this interface can modify all attributes of a timer).

```java
void updateTimer(WiserTimerBuilder builder, final IResultCallback callback);

```

**Parameters**

| Parameters    | Description                                        |
| ---- | ---- |
| taskName | Name of timer task                         |
| loops | Execute the timer times of a week.number of loops: "0000000”; 0 denotes off, and 1 denotes on. Each 0 from the left to the right denotes: Sunday, Monday, Tuesday, Wednesday, Thursday, Friday and Saturday, respectively."0000000" means execute once."1111111" means execute everyday                           |
| devId | Device Id or group Id|
| actions | time clock Id |
| actions		 |dps task, json format: {/"dps/":{},/"time/":""}, the dp of the raw type needs format conversion：`new String(Base64.encodeBase64(HexUtil.hexStringToBytes(dps)))` |
| status		 | Initialize the timer switch state 0: off, 1: on|
| callback | callback not null|
| appPush | Whether to support regular execution result push|
| aliasName | Set timer note name |
| TimerDeviceTypeEnum | Enumeration, timing type: device timer or group timer |


**Example**

```java
WiserTimerBuilder builder = new WiserTimerBuilder.Builder()
    .timerId(Long.parseLong(alarmTimerBean.getGroupId()))
    .devId(id)
    .deviceType(TimerDeviceTypeEnum.DEVICE)
    .actions(dps)
    .loops("1111111")
    .aliasName("test")
    .status(1)
    .appPush(true)
    .build();
WiserHomeSdk.getTimerInstance().updateTimer(builder, new IResultCallback() {
    @Override
    public void onSuccess() {
        
    }

    @Override
    public void onError(String errorCode, String errorMsg) {
        
    }
});
```

## Obtain All Timers of Timer Task

**Declaration**

Obtain all-timer modules of the task required by a device.

```java
void getTimerList(String taskName, String devId, TimerDeviceTypeEnum deviceTimerTypeEnum, final IWiserDataCallback<TimerTask> callback);
```
**Parameters**

| Parameters    | Description                                        |
| ---- | ---- |
| taskName | Name of timer task, optional, empty means to get a list of common timers |
| devId | Device Id or group Id|
| TimerDeviceTypeEnum | Enumeration, timing type: device timing or group timing|
| callback | callback not null|
| TimerTaskStatus| Timer switch status and name|
| ArrayList<Timer> | Single timer list |


**Example**

```java
WiserHomeSdk.getTimerInstance().getTimerList(null, mGwId, TimerDeviceTypeEnum.DEVICE, new IWiserDataCallback<TimerTask>() {
    @Override
    public void onSuccess(TimerTask timerTask) 			{

    }

    @Override
    public void onError(String errorCode, String errorMessage) {
        
    }
});

```
## Modify the Status of All Scheduled Tasks Under the Category or Delete the Timer

**Declaration**

```java
void updateCategoryTimerStatus(String taskName, String devId, TimerDeviceTypeEnum deviceTimerTypeEnum, TimerUpdateEnum timerUpdateEnum, IResultCallback callback);
```
**Parameters**

| Parameters    | Description                                        |
| ---- | ---- |
| taskName | Name of timer task|
| devId | Device Id or group Id|
| TimerDeviceTypeEnum | Enumeration, timing type: device timing or group timing|
| TimerUpdateEnum |Enumeration, operation type: turn on timer, turn off timer, delete timer|
| callback | callback not null|

**Example**

```java
WiserHomeSdk.getTimerInstance().updateCategoryTimerStatus(taskname ,mDevId, TimerDeviceTypeEnum.DEVICE, TimerUpdateEnum.CLOSE,new IResultCallback() {
    @Override
    public void onSuccess() {
        
    }

    @Override
    public void onError(String errorCode, String errorMsg) {
        
    }
});

```