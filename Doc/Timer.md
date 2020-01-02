# Timer task

Wiser Smart provides basic timing capabilities, and supports devices (including WiFi devices, Bluetooth mesh sub-devices and zigbee sub-devices) and groups. It is also provided with the interface for addition, deletion, change and querying of timer information for dp points of the device. After the APP sets the timer information through the timing interface, the hardware module automatically performs the scheduled operation according to the timing requirements. Multiple timers can be included in each timer task, as shown in the figure below:

![](./images/android-sdk-timer.jpg)

All methods related to timing are included in WiserHomeSdk.getTimerManagerInstance().

The taskName is used by multiple interfaces, which can be described as a group, and a group may include multiple timers. Each timer task belongs to or does not belong to a group, and the group is currently only used for presentation.

## Adding Timer

**[Description]**

Add one timer.

**[Method Invocation]**

```java
/**
*  Add a single dp point of timer (default: true); the sub-device is supported.
*  @param taskName     name of timer task
*  @param loops        number of loops: "0000000”; 0 denotes off, and 1 denotes on. Each 0 from the left to the right denotes: Sunday, Monday, Tuesday, Wednesday, Thursday, Friday and Saturday, respectively.
*  @param devId        device Id or group Id
*  @param dpId  			id of dp point
*  @param time         time clock in a timer task
*  @param callback     callback
*/
void addTimerWithTask(String taskName, String loops, String devId, String dpId, String time, final IResultStatusCallback callback);


/**
 * Add a timer          the new interface of a device is supported.
 * Meanings of other parameter values are the same as above.
 * @param dps    key-value pair of dp point; key: dpId; value: dpValue (only a single dp point is supported)
 * @param callback
 */
void addTimerWithTask(String taskName, String devId, String loops, Map<String, Object> dps, String time, final IResultStatusCallback callback);
```
**[Example Codes]**

```java
WiserHomeSdk.getTimerManagerInstance().addTimerWithTask("task01", "1111111",mDevId,  "1", "14:29", new IResultStatusCallback() {
    @Override
    public void onSuccess() {
        Toast.makeText(mContext, “adding timer tasks succeeded", Toast.LENGTH_LONG).show();
    }
    @Override
    public void onError(String errorCode, String errorMsg) {
        Toast.makeText(mContext, "adding timer tasks failed" + errorMsg, Toast.LENGTH_LONG).show();
    }

});
```
### Obtaining States of All Timer Tasks of a Certain Device

**[Description]**

Obtain states of all timer tasks of a certain device.

**[Method Invocation]**

```java
/**
* Obtain states of all timer tasks of a certain device.
*
* @param devId    device Id
* @param 	 callback
*/
void getTimerTaskStatusWithDeviceId(String devId, final IGetDeviceTimerStatusCallback callback);
```
**[Example Codes]**

```java
WiserHomeSdk.getTimerManagerInstance().getTimerTaskStatusWithDeviceId(mDevId, new IGetDeviceTimerStatusCallback() {
    @Override
    public void onSuccess(ArrayList<TimerTaskStatus> list) {
        Toast.makeText(mContext, “obtaining states of timer tasks of a device succeeded", Toast.LENGTH_LONG).show();
    }
    @Override
    public void onError(String errorCode, String errorMsg) {
        Toast.makeText(mContext, "obtaining states of timer tasks of a device failed" + errorMsg, Toast.LENGTH_LONG).show();
    }

});
```
### Controlling Switch Status of all Timers in a Timer Task

**[Description]**

Control switch status of all timers in a timer task.

**[Method Invocation]**

```java
/**
* Control switch status of all timers in a timer task.
* @param taskName	name of timer task
* @param devId    device Id or group I
* @param status   status value 1: on; 0: off
* @param 	 callback
*/
void updateTimerTaskStatusWithTask(String taskName, String devId, int status, final IResultStatusCallback callback);
```
**[Example Codes]**

```java
WiserHomeSdk.getTimerManagerInstance().updateTimerTaskStatusWithTask(taskName, mDevId, 1, new IResultStatusCallback() {
    @Override
    public void onSuccess() {
        Toast.makeText(mContext, “controlling switch status of all timers in a timer task succeeded", Toast.LENGTH_LONG).show();
    }
    @Override
    public void onError(String errorCode, String errorMsg) {
        Toast.makeText(mContext, "controlling switch status of all timers in a timer task failed" + errorMsg, Toast.LENGTH_LONG).show();
    }

});
```
### Controlling Switch Status of a Timer

**[Description]**

Control switch status of a timer.

**[Method Invocation]**

```java
/**
* Control switch status of a timer.
* @param taskName	name of timer task

* @param devId    device Id or group Id
* @param timerId  time clock Id
* @param isOpen   switch
* @param 	 callback
**/
void updateTimerStatusWithTask(String taskName, String devId, String timerId, boolean isOpen, IResultStatusCallback callback);
```
**[Example Codes]**

```java
WiserHomeSdk.getTimerManagerInstance().updateTimerStatusWithTask(taskName, mDevId, timeId, false, new IResultStatusCallback() {
        @Override
        public void onSuccess() {
            Toast.makeText(mContext, “controlling switch status of a timer succeeded", Toast.LENGTH_LONG).show();
        }

        @Override
        public void onError(String errorCode, String errorMsg) {
            Toast.makeText(mContext, "controlling switch status of a timer failed" + errorMsg, Toast.LENGTH_LONG).show();
        }
    });
```
## Removing Timer

**[Description]**

Removing timer

**[Method Invocation]**

```java
/**
* Remove timer
* @param taskName	name of timer task
* @param devId    device Id or group Id
* @param timerId  time clock Id
* @param 	 callback
*/
void removeTimerWithTask(String taskName, String devId, String timerId, IResultStatusCallback callback);
```
**[Example Codes]**

```java
WiserHomeSdk.getTimerManagerInstance().removeTimerWithTask(taskName, mDevId, timeId, new IResultStatusCallback() {
    @Override
    public void onSuccess() {

       Toast.makeText(mContext, “removing timer succeeded", Toast.LENGTH_LONG).show();
    }

    @Override
    public void onError(String errorCode, String errorMsg) {
        Toast.makeText(mContext, "removing timer failed" + errorMsg, Toast.LENGTH_LONG).show();
    }

});
```
### Updating Timer Status

**[Description]**

Updating timer status (this interface can modify all attributes of a timer)

**[Method Invocation]**

```java
/**
* Update timer status.
* @param taskName	name of timer task
* @param loops    number of loops (daily and weekly transmission: ”1111111”)
* @param devId    device Id or group Id
* @param timerId  time clock Id
* @param dpId     id of dp point
* @param time     timing time
* @param isOpen	  switching on or off 
* @param 	 callback
*/
void updateTimerWithTask(String taskName, String loops, String devId, String timerId, String dpId, String time, boolean isOpen, final IResultStatusCallback callback);



/**

 * Updating timer status

 * @param taskName	name of timer task

 * @param devId    device id or group Id

 * @param timerId  time clock Id

 * @param loops    number of loops

 * @param instruct	dp point data for timing; only a single dp point is supported (json format); for example:   [{

 *                 "time": "20:00",

 *                 "dps": {

 *                 "1": true

 *                 }]

 * @param callback

 */

void updateTimerWithTask(String taskName, String loops, String devId, String timerId, String instruct, final IResultStatusCallback callback);
```
**[Example Codes]**

```java
WiserHomeSdk.getTimerManagerInstance().updateTimerWithTask(taskName,"0011001", mDevId, timeId,  "[{"time": "20:00", "dps": { "1": true},{"time": "22:00","dps": {"2": true}]",  new IResultStatusCallback() {
    @Override
    public void onSuccess() {
        Toast.makeText(mContext, “updating timer attribute succeeded", Toast.LENGTH_LONG).show();
    }
    @Override
    public void onError(String errorCode, String errorMsg) {
        Toast.makeText(mContext, "updating timer attribute failed" + errorMsg, Toast.LENGTH_LONG).show();
    }
});
```
### Obtain All Timers of Timer Task

**[Description]**

Obtain all timers of timer task.

**[Method Invocation]**

```java
/**
* Obtaining all timers of timer task.
* @param taskName	name of timer task
* @param devId    device Id or group Id
* @param 	 callback
*/
void getTimerWithTask(String taskName, String devId, final IGetTimerWithTaskCallback callback);
```
**[Example Codes]**

```java
WiserHomeSdk.getTimerManagerInstance().getTimerWithTask(taskName, mDevId, new IGetTimerWithTaskCallback() {
    @Override
    public void onSuccess(TimerTask timerTask) {
        Toast.makeText(mContext, “obtaining timers of timer tasks succeeded", Toast.LENGTH_LONG).show();
    }
    @Override
    public void onError(String errorCode, String errorMsg) {
        Toast.makeText(mContext, "obtaining timers of timer tasks failed" + errorMsg, Toast.LENGTH_LONG).show();
    }
});
```
### Obtaining All Timers of All Timer Tasks for a Device

**[Description]**

Obtain all timers of all timer tasks for a device.

**[Method Invocation]**

```java
/**
* Obtaining all timers of all timer tasks for a device.
* @param devId    device Id or group Id
* @param 	 callback
*/
void getAllTimerWithDeviceId(String devId, final IGetAllTimerWithDevIdCallback callback);
```
**[Example Codes]**

```java
WiserHomeSdk.getTimerManagerInstance().getAllTimerWithDeviceId(mDevId, new IGetAllTimerWithDevIdCallback() {
    @Override
    public void onSuccess(ArrayList<TimerTask> taskArrayList) {
        Toast.makeText(mContext, “obtaining timers for a device succeeded", Toast.LENGTH_LONG).show();
    }
    @Override
    public void onError(String errorCode, String errorMsg) {
        Toast.makeText(mContext, "obtaining timers for a device failed" + errorMsg, Toast.LENGTH_LONG).show();
    }
});
```
