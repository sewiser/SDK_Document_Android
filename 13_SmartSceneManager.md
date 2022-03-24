# Smart Scene
Smart scenes are divided into **one-click execution scene** and **automated scene**, hereinafter referred to as **scene** and **automation**, respectively.

- The scene is user-added actions that are triggered manually.
- Automation is that the user sets conditions and automatically executes the set actions when the conditions trigger.

## Overview

Wiser IoT supports users to set weather or equipment conditions according to the actual life scene, and when the conditions are met, let one or more devices perform the corresponding tasks.

| Scene Management | Description |
| ---- | ---- |
|  WiserHomeSdk.newSceneInstance(String sceneId) |   Provides editing, deletion, and execution of a single scene, which needs to be initialized with the scene id. The scene id refers to the id field of SceneBean, which can be obtained from the return result of the [Get Scene List interface](#GetSceneList). |
|WiserHomeSdk.getSceneManagerInstance()| It mainly provides all the data related to the conditions, tasks, equipment, and cities in the scene, and the scene list data acquisition.|

Before using intelligent scene-related interfaces, you need to understand the two concepts of scene conditions and scene tasks.

## Scene condition

Scene conditions correspond to the SceneCondition class. Wiser IoT supports the following condition types:

- Meteorological conditions: including temperature, humidity, weather, PM2.5, air quality, sunset, and sunrise. When the user selects meteorological conditions, he can select the current city.
- Equipment condition: It means that the user can select the functional status of a device in advance. When the device reaches this state, the task in the current scene will be triggered, but the same device cannot be used as a condition and task at the same time to avoid operation conflicts.
- Timing condition: It means that the scheduled task can be performed according to the specified time.

## Scene task

A scenario task refers to having one or more devices perform certain operations when the scenario meets the set weather or equipment conditions, corresponding to the `SceneTask` class. Or turn off and on automation.

The main properties of SceneTask are defined as follows:

|Field|Type|Description|
| ---- | ---- | ---- |
| id | Sting | task id
| actionExecutor | String | Task type, enum as follows: <br>ruleTrigger: Trigger scene<br>ruleEnable: Enable scene<br>ruleDisable: Disable scene<br>appPushTrigger: Trigger app push<br>mobileVoiceSend: Mobile service<br>smsSend: SMS service<br>deviceGroupDpIssue: Trigger group device<br>irIssue: Trigger first generation IR device<br>dpIssue: Trigger device<br>delay: Delay<br>irIssueVii: Trigger second generation IR device<br>toggle: Trigger toggle task<br>dpStep: Trigger dpStep task
| entityId | String | Device id
| entityName | String | Device name
| actionDisplayNew | Map&lt;String, List&lt;String&gt;&gt; | Task display information
| executorProperty | Map&lt;String, Object&gt; | Task executor property
| extraProperty | Map&lt;String, Object&gt; | Task extra property

## Smart scene management

### <span id="GetSceneList">Scene list function</span>

**Description**

Get scene list data. Scenarios are returned with automation, and scenarios and automation are distinguished by whether the conditions field is empty.

```java
void getSceneList(long homeId,IWiserDataCallback<List<SceneBean>> callback)
```
**Parameters**

| Parameter | Description |
| ---- | ---- |
| homeId | Home id | |
| callback | Callback |

Among them, the main attributes of `SceneBean` are defined as follows

|Field|Type| Description |
| ---- | ---- | ---- |
| id |Sting| Scene  id
| name |String| Scene name
| conditions | List&lt;SceneCondition&gt; | Scene condition list
| actions | List&lt;SceneTask&gt; | Scene task list
| matchType | int | The type that satisfies the condition. Any condition is 1 and all conditions are 2
| enable | boolean | Whether automation is enabled

**Example**

```java
WiserHomeSdk.getSceneManagerInstance().getSceneList(long homeId, new IWiserResultCallback<List<SceneBean>>() {
	@Override
	public void onSuccess(List<SceneBean> result) {
	}

	@Override
	public void onError(String errorCode, String errorMessage) {
	}
});
```

### <span id="GetSceneList">Scene list function</span>

**Description**

Get scene list data. Scenarios are returned with automation, and scenarios and automation are distinguished by whether the conditions field is empty.

```java
void getSceneList(long homeId,IWiserDataCallback<List<SceneBean>> callback)
```
**Parameters**

| Parameter | Description |
| ---- | ---- |
| homeId | Home id | |
| callback | Callback |

Among them, the main attributes of `SceneBean` are defined as follows

|Field|Type| Description |
| ---- | ---- | ---- |
| id |Sting| Scene  id
| name |String| Scene name
| conditions | List&lt;SceneCondition&gt; | Scene condition list
| actions | List&lt;SceneTask&gt; | Scene task list
| matchType | int | The type that satisfies the condition. Any condition is 1 and all conditions are 2
| enable | boolean | Whether automation is enabled

**Example**

```java
WiserHomeSdk.getSceneManagerInstance().getSceneList(long homeId, new IWiserResultCallback<List<SceneBean>>() {
	@Override
	public void onSuccess(List<SceneBean> result) {
	}

	@Override
	public void onError(String errorCode, String errorMessage) {
	}
});
```

### Scene simple list function

**Description**

Get scene list data. Scenarios are returned with automation, and scenarios and automation are distinguished by whether the conditions field is empty.
This interface is lighter than the scene list interface, but some data such as the actionDisplayNew of SceneTask may return null.

```java
void getSimpleSceneList(long homeId, IWiserResultCallback<List<SceneBean>> callback)
```
**Parameters**

| Parameter | Description |
| ---- | ---- |
| homeId | Home id | |
| callback | Callback |

Among them, the main attributes of `SceneBean` are defined as follows

|Field|Type| Description |
| ---- | ---- | ---- |
| id |Sting| Scene  id
| name |String| Scene name
| conditions | List&lt;SceneCondition&gt; | Scene condition list
| actions | List&lt;SceneTask&gt; | Scene task list
| matchType | int | The type that satisfies the condition. Any condition is 1 and all conditions are 2
| enable | boolean | Whether automation is enabled

**Example**

```java
	WiserHomeSdk.getSceneManagerInstance().getSimpleSceneList(SceneUtil.getHomeId(), new IWiserResultCallback<List<SceneBean>>() {
			@Override
			public void onSuccess(List<SceneBean> result) {
			}

			@Override
			public void onError(String errorCode, String errorMessage) {
			}
		});
```

### Get condition list

**Description**

Get a list of conditions, such as temperature, humidity, weather, PM2.5, sunset, and sunrise, etc. Note: the device can also be used as a condition.

The temperature in the conditions is divided into degrees Celsius and Fahrenheit, and the required data is passed in as required.

```java
void getConditionList(boolean showFahrenheit,IWiserResultCallback<List<ConditionListBean>> callback);
```
**Parameters**

| Parameter | Description |
| ---- | ---- |
| showFahrenheit |True:Fahrenheit units. False:Celsius units|
| callback |Callback |

**Example**

```java
WiserHomeSdk.getSceneManagerInstance().getConditionList(new IWiserDataCallback<List<ConditionListBean>>() {
	@Override
	public void onSuccess(List<ConditionListBean> conditionActionBeans) {
	}

	@Override
	public void onError(String errorCode, String errorMessage) {
	}
});

```

Among them, the main attributes of ConditionListBean are defined as follows

|Field|Type| Description |
| ---- | ---- | ---- |
| name |Sting| Condition name
| type |String| Condition category
| Property | IProperty | Condition attribute

Currently supported weather condition categories with their names and Property types

| name | Type | Property Type |
| ---- | ---- | ---- |
| Temperature | temp | ValueProperty |
| Humidity | humidity | EnumProperty |
| Weather | condition | EnumProperty |
| PM2.5 | pm25 | EnumProperty |
| Air Quality | aqi | EnumProperty |
| Sunset/Sunrise | sunsetrise | EnumProperty |
| Timer | timer | TimerProperty |

Property is a commonly used data structure in Wiser Smart, which can be used to control equipment and other functions. There are currently five types of Property: Numeric, Enumerated, Boolean, and Types for Timing (corresponding to Numeric, Enumerated, and Boolean in conditions). Each Property provides different access interfaces. See [Rules Introduction](#rules) for details.

### Create weather conditions

**Description**

Weather conditions include temperature, humidity, weather, PM2.5, air quality, sunrise and sunset, and the city can be selected freely. The weather conditions that can be selected vary depending on the device in the user account.

```java
SceneCondition createWeatherCondition(PlaceFacadeBean place, String type, Rule rule)
```
**Parameters**

| Parameter | Required | Description |
| ----| ---- | ----|
| place | yes | Corresponding city weather. PlaceFacadeBean objects can be obtained from [Get City List](#GetCityList), [Get cities based on latitude and longitude](#GetCityInfoByLATLNG), [Get cities based on city id](#GetCityByCityId) interface. Currently, access to the city interface is only supported China. |
| type | yes | Condition type. |
| rule | yes | Conditional rules, see [rule introduction](#rules)|

**Example**

```java
ValueRule tempRule = ValueRule.newInstance(
	"temp",
	">",
	20
);
SceneCondition tempCondition = SceneCondition.createWeatherCondition(
	placeFacadeBean,
	"temp",
	tempRule
);
```

### Create before or after sunrise and sunset conditions

**Description**

The sunrise and sunset conditions value the conditions of a few minutes before or after sunrise and sunset, and the conditions at sunrise and sunset are still weather-type conditions.

```java
SceneCondition createSunRiseSetCondition(PlaceFacadeBean city, Rule rule)
```
**Parameters**

| Parameter | Required | Description |
| ----| ---- | ----|
| place | yes |  PlaceFacadeBean objects can be obtained from [Get City List](#GetCityList), [Get cities based on latitude and longitude](#GetCityInfoByLATLNG), [Get cities based on city id](#GetCityByCityId) interface. Currently, access to the city interface is only supported China. | |
| rule | yes | Conditional rules, see [rule introduction](#rules)|

**Example**

```java
SunSetRiseRule tempRule = SunSetRiseRule.newInstance(
	placeFacadeBean,  // PlaceFacadeBean object
	type,          //SunType.SUNRISE or SunType.SUNSET
	minutes       //Minutes before or after sunrise and sunset. Range: -300 to 300.
);
SceneCondition tempCondition = SceneCondition.createWeatherCondition(
	placeFacadeBean,   //PlaceFacadeBean object
	tempRule           // Rule of sunraiseset
);
```

### Create a device-type condition

**Description**

A device condition is when one device is in a certain state that triggers a scheduled task for another device or multiple devices. <strong> To avoid loop control, the same device cannot be used as a condition and task at the same time. </strong>

```java
SceneCondition createDevCondition(DeviceBean devBean, String dpId, Rule rule)
```
**Parameters**

| Parameter | Description |
| ---- | ---- |
| devBean | Conditional equipment. DeviceBean is obtained from the [Get Condition Device List](#GetConditionDeviceList) interface
| dpId | Condition dpId. |
| rule | Condition rule |

**Example**

```java
BoolRule boolRule = BoolRule.newInstance(
	"dp1",    //"dp" + dpId
	true    //value
);
SceneCondition devCondition = SceneCondition.createDevCondition(
	devBean,
	"1",        //dpId
	boolRule    //rule
);
SceneCondition createDevCondition(DeviceBean devBean, String dpId, Rule rule)

```

### Create timing type conditions

**Description**

Timing conditions refer to the execution of a scheduled task at a specified time

```java
SceneCondition createTimerCondition(String display,String name,String type,Rule rule)
```

**Parameters**

| Parameter | Description
| ---- | ---- |
| display | User-selected time condition for display
| name | Name of timing condition
| type | Condition type|
| rule | Conditional rules|

**Example**

```java
TimerRule timerRule = TimerRule.newInstance("Asia/Shanghai","0111110","16:00","20180310")
SceneCondition.createTimerCondition(
	"Monday, Tuesday, Wednesday, Thursday, Friday",
	"Working day timing",
	"timer",
	timerRule
	)
```

### <span id="rules">Five types of rules</span>

- Numerical type

	Taking temperature as an example, the final expression of the numerical condition is formatted as "temp > 20". You can get the currently supported temperature maximum, minimum, and granularity (stepping) from the Obtain Condition List interface; you can get the supported temperature from the Obtain Condition List, etc. After the configuration is completed on the user interface, the `ValueRule.newInstance` method is invoked to build the rules, and the rules are used to form the conditions.

	**Example**

	```java

	ValueProperty tempProperty = (ValueProperty) conditionListBean.getProperty();

	int max = tempProperty.getMax();       //Maximum value
	int min = tempProperty.getMin();       //Minimum value
	int step = tempProperty.getStep();     //Granularity
	String unit = tempProperty.getUnit();  //Unit

	//The temperature is greater than 20 ℃
	ValueRule tempRule = ValueRule.newInstance(
		"temp",  //Category
		">",     //operational rule (">", "==", "<")
		20       //Critical value
	);
	SceneCondition tempCondition = SceneCondition.createWeatherCondition(
		placeFacadeBean,   //City
		"temp",            //Category
		tempRule           //Rule
	);
	```

- Enumerated type

	Taking the weather condition as an example, the final expression of the enumerated condition is formatted as "condition == rainy". You can get the currently supported weather conditions from the Obtain Condition List interface, including the code and name of each weather condition. After the configuration is completed on the user interface, the  `EnumRule.newInstance` method is invoked to build the rules, and the rules are used to form the conditions.

	**Example**

	```java
	EnumProperty weatherProperty = (EnumProperty) conditionListBean.getProperty();  //Enumeration type Property
	/**
	*{
	*  {"sunny", " fine day"},
	*  {"rainy", "rainy day"}
	*}
	*/
	HashMap<Object, String> enums = weatherProperty.getEnums();
	//It's rainy.
	EnumRule enumRule = EnumRule.newInstance(
				"condition",  //Category
				"rainy"        // Enumerated value selected
	);
	SceneCondition weatherCondition = SceneCondition.createWeatherCondition(
				placeFacadeBean,    //City
				"condition",        //Category
				enumRule            //Rule
	);
	```

- Boolean type

	Boolean types are common in device type conditions, and the final expression is formatted as "dp1 == true". You need to invoke the [Obtain the conditioning device list](#GetConditionDeviceList) interface to obtain devices that support the configuration of the smart scene, and then query the operations that the device can support based on the device id. See the Obtain Operations Supported by Device for details. After the configuration is completed on the user interface, the `BoolRule.newInstance` method is invoked to build the rules, and the rules are used to form the conditions.

	**Example**

	```java

	BoolProperty devProperty = (BoolProperty) conditionListBean.getProperty();  // Boolean

	/**
	{
	{true, "on"},
	{false, "off"}
	}
	*/
	HashMap<Boolean, String> boolMap = devProperty.getBoolMap();

	//When the device is turned on.
	BoolRule boolRule = BoolRule.newInstance(
		"dp1",    //"dp" + dpId
		true    //bool of triggering conditions
	);
	SceneCondition devCondition = SceneCondition.createDevCondition(
		devBean,    //Device
		"1",        //dpId
		boolRule    //Rule
	);
	```

- Sunrise and sunset type

	The expression of sunrise and sunset is of Map type, namely Key: Value. After the user completes the sunrise and sunset configuration, call `SunSetRiseRule.newInstance` to complete the Map data assembly by the SDK to form the rule conditions.

	**Example**

	```java
	public static TimerRule newInstance(String timeZoneId,String loops,String time,String date);

	//Build sunrise and sunset rule
	SunSetRiseRule sunRule = SunSetRiseRule.newInstance(city,sunType,10)

	/**
	* @param city PlaceFacadeBean object
	* @param sunType  SunType.SUNRISE or SunType.SUNSET
	* @param minutes Time before or after sunrise and sunset  range -300 to 300 minutes
	* @return
	*/
	public static SunSetRiseRule newInstance(PlaceFacadeBean city, SunType type, Integer minutes)

	/**
	* Create sunrise and sunset conditions
	* @param city PlaceFacadeBean object
	* @param rule  Rule of sunraiseset
	* @return
	*/
	public static SceneCondition createSunRiseSetCondition(PlaceFacadeBean city, Rule rule);

	SceneCondition createSunRiseSetCondition(city,rule)

	```

- Timer type

	The timer is expressed as a Map type, that is Key: Value. After the user completes the timer configuration, the `TimerRule.newInstance` is invoked to complete the Map data assembly by the SDK to form the rule condition.

	**Example**

	```java

	TimerProperty timerProperty = (TimerProperty)conditionListBean.
	getProperty();	//Timer-type property

	//TimerRule.newInstance provides two construction methods, the difference is whether it will pass the time zone.
	//If it does not pass the time zone, read the default time zone.
	/**
	*
	* @param timeZoneId time zone, the format like "Asia/Shanghai"
	* @param loops 7-digit character string; each digit represents what day of the week; the first digit represents Sunday, and the second digit represents Monday.
	* By analogy, the character indicates on which days the timer is enabled. 0 indicates not selected; 1 indicates selected, with a format like only Monday Selected.
	* Tuesday: "0110000". If they are not selected, it means that the timer is only executed once, with the format: "0000000"
	* @param time 24-hour system with a format like "08:00",
	* If the user uses the 12-hour system, the developer needs to convert it to a 24-hour system and upload it.
	* @param date, format like "20180310"
	* @return
	*/
	public static TimerRule newInstance(String timeZoneId,String loops,String time,String date);

	//Create timer rule
	TimerRule timerRule = TimerRule.newInstance("Asia/Shanghai","0111110","16:00","20180310")

	/**
	* The required parameters have the same meaning as the parameters of the above method, and the default time zone is read.
	* @param loops
	* @param time
	* @param date
	* @return
	*/
	public static TimerRule newInstance(String loops,String time,String date);

	/**
	* Create timer conditions
	* @param display  is used to display the user-selected time conditions.
	* @param name  Name of Timer condition
	* @param type condition type
	* @param rule  condition regulations
	* @return
	*/
	public static SceneCondition createTimerCondition(String display,String name,String type,Rule rule);

	//Create timer conditions, taking the Timer rule constructed above as an example.
	SceneCondition.createTimerCondition(
	"Monday, Tuesday, Wednesday, Thursday & Friday",
	"Timer in workday",
	"timer",
	timerRule
	)
	```

### <span id="GetConditionDeviceList">Obtain the condition device list</span>

**Description**

When selecting a scene condition, a device is selected, and a device dp list needs to be obtained according to the deviceId of the selected device, and then a certain dp function point is selected, that is, the device is designated to execute the dp function as the execution condition of the scene.

```java
void getConditionDevList(long homeId, IWiserResultCallback<List<DeviceBean>> callback);
```

**Parameters**

| Parameter | Description |
| ---- | ---- |
| homeId | home id
| callback | callback |

**Example**

```java
WiserHomeSdk.getSceneManagerInstance().getConditionDevList(homeId ,new IWiserResultCallback<List<DeviceBean>>() {
	@Override
	public void onSuccess(List<DeviceBean> deviceBeans) {
	}

	@Override
	public void onError(String errorCode, String errorMessage) {
	}
});
```

### Get device task-based on device ID

**Description**

It is used to obtain tasks that can be selected when selecting specific trigger conditions of the device.

```java
void getDeviceConditionOperationList(String devId,IWiserResultCallback<List<TaskListBean>> callback);
```
**Parameters**

| Parameter | Description
| ---- | ---- |
| devId | device id
| callback | callback |

**Example**

```java
WiserHomeSdk.getSceneManagerInstance().getDeviceConditionOperationList(
	devId, //device id
	new IWiserDataCallback<List<TaskListBean>>() {
		@Override
		public void onSuccess(List<TaskListBean> conditionActionBeans) {
		}

		@Override
		public void onError(String errorCode, String errorMessage) {
		}
});
}
```

Among them, `TaskListBean` main attribute definition:

|Field|Type| Description |
| ---- | ---- | ---- |
| name |Sting| dp point name for interface display
| dpId |long| deivce dpId
| tasks | HashMap&lt;Object, String&gt; | dp point configurable operation, format: {true, "opened"}, {false, "closed"}
| type | String | Condition type bool, value, enum, etc.

### <span id="GetCityList">Get city list</span>

**Description**

Used to select cities when creating weather conditions.
Note: Currently the city list only supports China.

```java
void getCityListByCountryCode(String countryCode, IWiserResultCallback<List<PlaceFacadeBean>> callback);
```

**Parameters**

| Parameter | Description
| ---- | ---- |
| countryCode | Country code , China = "cn"
| callback | callback |

**Example**

```java

WiserHomeSdk.getSceneManagerInstance().getCityListByCountryCode(
	"cn",  //China
	new IWiserResultCallback<List<PlaceFacadeBean>>() {
		@Override
		public void onSuccess(List<PlaceFacadeBean> placeFacadeBeans) {
		}

		@Override
		public void onError(String errorCode, String errorMessage) {
		}
});

```

Among them, the main properties of the `PlaceFacadeBean` class are defined as follows:

|Field|Type| Description |
| ---- | ---- | ---- |
| area |Sting| area name
| province | String | province name
| city | String | city name
| cityId | long | cityId

### <span id="GetCityInfoByLATLNG">Get cities based on latitude and longitude</span>

**Description**

The city information is obtained according to latitude and longitude and is used to display the existing weather conditions.

```java
void getCityByLatLng(String lon, String lat, IWiserResultCallback<PlaceFacadeBean> callback);
```
**Parameters**

| Parameter | Description
| ---- | ---- |
| lon | Longitude |
| lat |Latitude|
| callback | callback|

**Example**

```java
WiserHomeSdk.getSceneManagerInstance().getCityByLatLng(
	String.valueOf(longitude), //Longitude
	String.valueOf(latitude),   //Latitude
	new IWiserResultCallback<PlaceFacadeBean>() {
		@Override
		public void onSuccess(PlaceFacadeBean placeFacadeBean) {
		}

		@Override
		public void onError(String errorCode, String errorMessage) {
		}
});
```

### <span id="GetCityByCityId">Get cities based on city ID</span>

**Description**

The city information is obtained according to the city ID and is used to display the existing weather conditions. The city id can be obtained in the get city list interface.

```java
void getCityByCityIndex(long cityId, IWiserResultCallback<PlaceFacadeBean> callback);
```

**Parameters**

| Parameter | Description
| ---- | ---- |
| cityId |City Id|
| callback | callback |

**Example**

```java
WiserHomeSdk.getSceneManagerInstance().getCityByCityIndex(
	cityId, //city id
	new IWiserResultCallback<PlaceFacadeBean>() {
		@Override
		public void onSuccess(PlaceFacadeBean placeFacadeBean) {
		}

		@Override
		public void onError(String errorCode, String errorMessage) {
		}
});
```

### Scene task

Scene task refer to control actions performed when conditions trigger. Tasks executable in manual scenarios include [smart device type](#Device_Type), [group device type](#Group_Type), [automation scenario type](#Scene_Type) and [delay type](#Delay_Type). The executable actions of automation scenario include [smart device type](#Device_Type), [group device type](#Group_Type), [manual scene type](#Scene_Type), [automation scene type](#Scene_Type), [delay type](#Delay_Type) and [message type](#Message_Type). The tasks that users can set vary depending on the device of users. Please note that not every product supports the scene.

### <span id="Device_Type">Create device type action</span>

**Description**

It is used to create device type actions.

```java
SceneTask createDpTask(@NonNull String devId, HashMap<String, Object> tasks)

```

**Parameters**

| Parameter | Description
| ---- | ---- |
| devId |device id|
| tasks |tasks to be implemented task format: { dpId: dp point value}|

**Example**

```java
HashMap<String, Object> taskMap = new HashMap<>();
taskMap.put("1", true); //Turn on the device
SceneTask task = WiserHomeSceneManager.getInstance().createDpTask(
	devId,      //Device id
	taskMap     //Device action
);
```

### <span id="GetActionDevList">A list of devices supported by obtaining execution action</span>

**Description**

Obtain a list of devices supporting scene actions for selecting to add to the action to be executed.

```java
void getTaskDevList(long homeId, IWiserResultCallback<List<DeviceBean>> callback);
```

**Parameters**

| Parameter | Description
| ---- | ---- |
| homeId |home id|
| callback | callback |

Among them, the main properties of `DeviceBean` are defined as follows:

|Field|Type| Description |
| ---- | ---- | ---- |
| name | String | device name
| productId | String | product id
| devId | String | device id
| iconUrl | String | icon URL
| isOnline | Boolean | Device online status, note: use this method to get device online status getIsOnline ()

**Example**

```java
WiserHomeSdk.getSceneManagerInstance().getTaskDevList(homeId,new IWiserResultCallback<List<DeviceBean>>() {
	@Override
	public void onSuccess(List<DeviceBean> deviceBeans) {
	}

	@Override
	public void onError(String errorCode, String errorMessage) {
	}
});
```

### Obtain executable actions based on device ID

**Description**

It is used to obtain the tasks executed by the device when creating an action. The device id can be obtained from the [a list of devices supported by obtaining execution action](#GetActionDevList)

```java
void getDeviceTaskOperationList(String devId, IWiserResultCallback<List<TaskListBean>> callback);
```

**Parameters**

| Parameter | Description
| ---- | ---- |
| devId | device id|
| callback |callback |

Among them, the main properties of `TaskListBean` are defined as follows:

|Field|Type| Description |
| ---- | ---- | ---- |
| name |Sting| dp point name for interface display
| dpId |long| Device dpId
| tasks | HashMap&lt;Object, String&gt; | Obtain the operation configured by the dp point,Format::{true, "on"},{false, "off"}
| type | String |  Type of condition: bool, value, enum, etc.

**Example**

```java
WiserHomeSdk.getSceneManagerInstance().getDeviceTaskOperationList(
	devId, //device id
	new IWiserResultCallback<List<TaskListBean>>() {
		@Override
		public void onSuccess(List<TaskListBean> conditionActionBeans) {
		}

		@Override
		public void onError(String errorCode, String errorMessage) {
		}
});
```

### <span id="Group_Type">Create group device type action</span>

**Description**

It is used to create group device type actions.

```java
SceneTask createDpGroupTask(@NonNull long groupId, HashMap<String, Object> tasks);
```

**Parameters**

| Parameter | Description
| ---- | ---- |
| groupId | group id|
| tasks |tasks to be implemented task format: { dpId: dp point value}|

**Example**

```java
HashMap<String, Object> taskMap = new HashMap<>();
taskMap.put("1", true); //Turn on the device
WiserHomeSceneManager.getInstance().createDpGroupTask(
	groupId, 	//group id
	taskMap 	//Device action
);
```

### <span id="GetGroupActionDevList">A list of group devices to get execution action support</span>

**Description**

Obtain a list of devices that support scenario actions, including common devices and group devices, for selecting the actions to be added to.

```java
getTaskDevAndGoupList(long homeId, IWiserResultCallback<SceneTaskGroupDevice> callback)
```
**Parameters**

| Parameter | Description
| ---- | ---- |
| homeId | home id|
| callback | callback |

Among them, the main properties of `SceneTaskGroupDevice` are defined as follows:

|Field|Type| Description |
| ---- | ---- | ---- |
| devices |List&lt;DeviceBean&gt; |List of common devices
| goups |List&lt; GroupBean&gt;| Group device list

**Example**

```java
WiserHomeSdk.getSceneManagerInstance().getTaskDevAndGoupList(homeId, new IWiserResultCallback<SceneTaskGroupDevice>() {
				@Override
				public void onSuccess(SceneTaskGroupDevice sceneTaskGroupDevice) {
					List<DeviceBean> deviceBeans = sceneTaskGroupDevice.getDevices();
					List<GroupBean> groupBeans = sceneTaskGroupDevice.getGoups();
					...
				}

				@Override
				public void onError(String errorCode, String errorMessage) {
					...
				}
			});
```

### Obtain executable actions based on group ID

**Description**

It is used to obtain the tasks executed by the group device when creating an action. The group id can be obtained from the [a list of group devices to get execution action support](#GetGroupActionDevList)

```java
void getDeviceTaskOperationListByGroup(String goupId, IWiserResultCallback<List<TaskListBean>> callback)
```

**Parameters**

| Parameter | Description
| ---- | ---- |
| groupId | group id|
| callback | callback |

**Example**

```java
WiserHomeSdk.getSceneManagerInstance().getDeviceTaskOperationListByGroup(groupId, new IWiserResultCallback<List<TaskListBean>>() {
				@Override
				public void onSuccess(List<TaskListBean> result) {

				}

				@Override
				public void onError(String errorCode, String errorMessage) {

				}
			});
```

### <span id="Scene_Type">Create scenario type action</span>

**Description**

Scenario-type actions are used to create scene type actions, including manual and automated scenarios. Parameters can be obtained through the [scenario list interface](#GetSceneList)

```java
SceneTask createSceneTask(SceneBean sceneBean);

```
**Parameters**

| Parameter | Description
| ---- | ---- |
| sceneBean | scene object|

**Example**

```java
WiserHomeSceneManager.getInstance().createSceneTask(scnenBean);
```

### <span id="Delay_Type">Create delay type action</span>

**Description**

Used to create a delay-type action. SDK version supports a maximum delay time of 300 minutes after 3.13.3, and only supports 59 minutes and 59s before 3.13.3. If the time with hours is used in business, it needs to be converted to minutes as a parameter.

```java
SceneTask createDelayTask(int minute, int second);

```
**Parameters**

| Parameter | Description
| ---- | ---- |
| minute | minutes|
| second | seconds|

**Example**

```java
WiserHomeSceneManager.getInstance().createDelayTask(
	2,  //minutes
	2	//seconds
);
```

### <span id="Message_Type">Create message type action</span>

**Description**

Used to create a message type action.

```java
SceneTask createPushMessage();
```

**Example**

```java
WiserHomeSceneManager.getInstance().createPushMessage();
```

### Sort scene

**Description**

Manual scene or automation scene sorting. Note: Manual or automation scenes can only be sorted separately and cannot be shuffled.

```java
void sortSceneList(long homeId, List<String> sceneIds, IResultCallback callback)
```

**Parameters**

| Parameter | Description
| ---- | ---- |
| homeId |home Id|
| sceneIds |Scene id list|
| callback |callback|

**Example**

```java
WiserHomeSdk.getSceneManagerInstance().sortSceneList(
	homeId, //home id
	sceneIds,//Scene id list
	new IResultCallback() {
		@Override
		public void onSuccess() {
		}

		@Override
		public void onError(String errorCode, String errorMessage) {
		}
});
```
###  <span id="GET_BGS">Scene background images</span>

**Description**

Get scene background images

```java
void getSceneBgs(IWiserResultCallback<ArrayList<String>> callback);
```

**Parameters**

| Parameter | Description
| ---- | ---- |
| callback | callback |

**Example**

```java
WiserHomeSdk.getSceneManagerInstance().getSceneBgs(new IWiserResultCallback<ArrayList<String>>() {
		@Override
		public void onSuccess(ArrayList<String> strings) {

		}

		@Override
		public void onError(String s, String s1) {

		}
	});
```

## Scene operation

WiserHomeSdk provides five operations for creating, modifying, executing, and deleting a single scene. In addition to creating other operations, the scene ID needs to be initialized. The scene ID can be obtained from the interface of [obtaining the scene list interface.](#GetSceneList)

### Create scene

**Description**

To add a scene, you need to pass in the Id of the family, the name of the scene, whether it is displayed on the homepage, the URL of the background image, the condition list, the task list (at least one task), and the precondition list (valid time period, can not pass, the default is effective all day), Executed when either or all of the conditions are met. You can also set only the name and task, background image, and no conditions, but you need to perform it manually.

**Parameters**

| Parameter | Description
| ---- | ---- |
| homeId | Home Id |
| name | Scene name |
| stickyOnTop |  whether it is displayed on the homepage |
| background | the URL of the background image. You can only use the background image provided in the [Get Scene Background Picture List] (#GET_BGS) interface|
| preConditions | Effective time period, which is passed in as a set of pre-condition objects, which may not be passed. |
| conditions | Scene trigger conditions |
| tasks | Scene execution tasks |
| matchType |Condition match type, "AND" or "OR", default value: SceneBean.MATCH\_TYPE\_OR means that any condition is fulfilled, SceneBean.MATCH\_TYPE\_AND means that all conditions are met|
| callback |callback|

The `PreCondition` property is defined as follows

|Field|Type| Description |
| ---- | ---- | ---- |
| id |Sting| The effective time period id. After the scene is created, it is automatically generated in the cloud, without a manual setting.
| condType |String| Please set PreCondition.TYPE\_TIME\_CHECK at present, which means the preset condition is the effective time period type
| expr | PreConditionExpr | Precondition rule object

The `PreConditionExpr` property is defined as follows

|Field|Type| Description |
| ---- | ---- | ---- |
| loops | String | A 7-character string, each of which indicates the day of the week, the first of which indicates Sunday, the second of which indicates Monday, and so on, and which days the automation takes effect. 0 means not selected, 1 means selected. For example, only Monday and Tuesday are selected: "0110000". If neither of them is selected, it means it only takes effect once. Format: "0000000"|
| start |String| Start time (only the `TIMEINTERVAL_CUSTOM` custom type setting will take effect)
| end | String | End time (only the `TIMEINTERVAL_CUSTOM` custom type setting will take effect)
| timeInterval | String | Effective time period type, `PreCondition.TIMEINTERVAL_ALLDAY` all day,` TIMEINTERVAL_NIGHT` night, `TIMEINTERVAL_DAYTIME` daytime,` TIMEINTERVAL_CUSTOM` custom |
| cityId | String | City Id, which can be obtained through [Get City List] (#GetCityList)
| timeZoneId | String | Effective time zone
| cityName | String | City name

**Example**

```java
//Data creation in effective period, can be empty
PreCondition preCondition = new PreCondition();
PreConditionExpr expr = new PreConditionExpr();
expr.setCityName("hangzhou");
expr.setCityId("xxxxx");//cityId Available via city list interface
expr.setStart("00:00");
expr.setEnd("23:59");
expr.setLoops("1111111");
expr.setTimeInterval(PreCondition.TIMEINTERVAL_ALLDAY);
preCondition.setCondType(PreCondition.TYPE_TIME_CHECK);
expr.setTimeZoneId(TimeZone.getDefault().getID());
preCondition.setExpr(expr);
List<PreCondition> preConditions = new ArrayList<>();
preConditions.add(preCondition);

WiserHomeSdk.getSceneManagerInstance().createScene(
	100001,
	"Morning", //scene name
	"https://images.png"
	true,  //Whether to display on the homepage
	preConditions, //Effective period, may not be transmitted
	conditions, //condition
	tasks,     //task
	SceneBean.MATCH_TYPE_AND, //Execution condition type
	new IWiserResultCallback<SceneBean>() {
		@Override
		public void onSuccess(SceneBean sceneBean) {
			Log.d(TAG, "createScene Success");
		}

		@Override
		public void onError(String errorCode, String errorMessage) {
		}
});
```

###  Modify the scene

**Description**

It is used to modify the scene. After it succeeded, it will return to new scene data.

```java
void modifyScene(SceneBean sceneReqBean, IWiserResultCallback<SceneBean> callback);
```

**Parameters**

| Parameter | Description
| ---- | ---- |
| sceneReqBean | Modified scene object |

**Example**

```java
sceneBean.setName("New name");  //Change Scene name
sceneBean.setConditions(Collections.singletonList(condition)); //Change scene conditions
sceneBean.setActions(tasks); //Change scene action

String sceneId = sceneBean.getId();  //Get the Scene id to initialize
WiserHomeSdk.newSceneInstance(sceneId).modifyScene(
	sceneBean,  //Modified Scene data class
	new IWiserResultCallback<SceneBean>() {
		@Override
		public void onSuccess(SceneBean sceneBean) {
			Log.d(TAG, "Modify Scene Success");
		}

		@Override
		public void onError(String errorCode, String errorMessage) {
		}
});
```

###  Delete scene

**Description**

For deleting scene

```java
void deleteScene(IResultCallback callback);
```

**Parameters**

| Parameter | Description
| ---- | ---- |
| callback | callback |

**Example**

```java
String sceneId = sceneBean.getId();

WiserHomeSdk.newSceneInstance(sceneId).deleteScene(new
IResultCallback() {
	@Override
	public void onSuccess() {
		Log.d(TAG, "Delete Scene Success");
	}

	@Override
	public void onError(String errorCode, String errorMessage) {
	}
});
```

### Run scene

**Description**

It is used to execute manual scenes.

Note: This method only sends commands to the cloud execution scenario. If the specific device is executed successfully, you need to monitor the device's DP change through WiserHomeSdk.newDeviceInstance(devId).registerDevListener().

```java
void executeScene(IResultCallback callback);
```

**Parameters**

| Parameter | Description
| ---- | ---- |
| callback | callback |

**Example**

```java
String sceneId = sceneBean.getId();
WiserHomeSdk.newSceneInstance(sceneId).executeScene(new IResultCallback() {
	@Override
	public void onSuccess() {
		Log.d(TAG, "Excute Scene Success");
	}

	@Override
	public void onError(String errorCode, String errorMessage) {
	}
});
```

### Turn on and turn off the automation scene

**Description**

It is used to turn on or off the automatic scene.

```java
void enableScene(String sceneId, final IResultCallback callback);

void disableScene(String sceneId, final IResultCallback callback);
```

**Parameters**

| Parameter | Description
| ---- | ---- |
| sceneId |sceneId |
| callback | callback |

**Example**

```java
String sceneId = sceneBean.getId();

WiserHomeSdk.newSceneInstance(sceneId).enableScene(sceneId,new
IResultCallback() {
	@Override
	public void onSuccess() {
		Log.d(TAG, "enable Scene Success");
	}

	@Override
	public void onError(String errorCode, String errorMessage) {
	}
});

WiserHomeSdk.newSceneInstance(sceneId).disableScene(sceneId,new
IResultCallback() {
	@Override
	public void onSuccess() {
		Log.d(TAG, "disable Scene Success");
	}

	@Override
	public void onError(String errorCode, String errorMessage) {
	}
});
```

### Erase

**Description**

If the user exits the activity of the scene, the scene destruction method should be invoked to reclaim the memory and enhance the experience.

**Example**

```java
WiserHomeSdk.getSceneManagerInstance().onDestroy();

WiserHomeSdk.newSceneInstance(sceneId).onDestroy();
```

### Register

**Description**

The monitoring of scene addition, editing, deletion, execution, opening and closing operations

```java
void registerSmartUpdateListener(ISmartUpdateListener listener);
```

**Parameters**

| Parameter | Description |
| ---- | ---- |
| listener |scene status listener |

`ISmartUpdateListener` interface is as follows:

```java
public interface ISmartUpdateListener {
	/**
	* Automatic scene update
	*/
	void onSmartUpdateListener();

	/**
	* Recommended
	*/
	void onCollectionsUpdateListener();
}
```

**Example**

```java
WiserHomeSdk.getSceneManagerInstance().registerSmartUpdateListener(new ISmartUpdateListener() {
			@Override
			public void onSmartUpdateListener() {

			}

			@Override
			public void onCollectionsUpdateListener() {

			}
		});
```

### Unregister

When you do not need to listen to the scene, you can unregister the listener

**Example**

```java
WiserHomeSdk.getSceneManagerInstance().unRegisterSmartUpdateListener(mSmartUpdateListener);
```

### Registration scene information change listener

**Description**

Scene addition, editing, deletion, execution, monitoring of opening and closing operations

```java
void registerSmartUpdateListener(ISmartUpdateListener listener);
```

**Parameters**

| Parameter | Description |
| ---- | ---- |
| listener | listener |

The `ISmartUpdateListener` method:

```java
public interface ISmartUpdateListener {
	/**
	* Automatic scene update
	*/
	void onSmartUpdateListener();

	/**
	* Recommended scenes to add to the collection update
	*/
	void onCollectionsUpdateListener();
}
```

**Example**

```java
WiserHomeSdk.getSceneManagerInstance().registerSmartUpdateListener(new ISmartUpdateListener() {
			@Override
			public void onSmartUpdateListener() {

			}

			@Override
			public void onCollectionsUpdateListener() {

			}
		});
```

### Unregister scene information change listener

**Description**

When the scene information change listener is not required, unregister the listener.

**Example**

```java
WiserHomeSdk.getSceneManagerInstance().unRegisterSmartUpdateListener(mSmartUpdateListener);
```
