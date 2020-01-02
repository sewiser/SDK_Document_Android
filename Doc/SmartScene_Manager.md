# <span id ="Smart">Smart</span>

## Brief Introduction

Smart divides into scene or automation actions. Scene is a condition that users add actions and it is triggered manually; automation action is a condition set by users, and the set action is automatically executed when the condition is triggered.

In the Wiser smart Android SDK, smart includes the unified management interface of scene and automation actions, 

`WiserHomeSdk.WiserHomeSdk.getSceneManagerInstance() `

and the independent operation interface

` WiserHomeSdk.newSceneInstance(String sceneId)`, The independent operation interface needs to be initialized with the scene id. The scene id can be obtained in the result of [obtaining the scene list interface.](#ObtainSceneList)

**In the following documents, manual scene and automated scene are simply referred to as scene.**

## <span id="ObtainSceneList">Obtain scene list</span>

**[Description]**

Get the scene list, which can be used when the scene home page is initialized. Determine the manual scene and automation actions through SceneBean's getConditions(); the value is empty when it is a manual scene.

**[Method Prototype]**

```java
/**
 * Obtain scene list
 * @param callback
 */
public void getSceneList(IWiserDataCallback<List<SceneBean>> callback)
```

Among, the interface of `SceneBean` is defined as follows

```java
/**
  * Obtain scene id
  * @returnScene id
 */
public String getId()

/**
  * Obtain scene name
  * @returnScene name
 */
public String getName()

/**
  *  Obtain scene conditions 
  * @returnScene condition
 */
public List<SceneCondition> getConditions()

/**
  *  Obtain scene task
  * @returnScene task
 */
public List<SceneTask> getActions()

/**
  * Obtain scene id
  * @return Scene id
 */
public String getId()


```

**[Example Codes]**

```java
WiserHomeSdk.getSceneManagerInstance().getSceneList(new IWiserResultCallback<List<SceneBean>>() {
      @Override
      public void onSuccess(List<SceneBean> result) {
      }

      @Override
      public void onError(String errorCode, String errorMessage) {
      }
});
```
**Automation condition**

User's configurable conditions include weather conditions, device status and timer.

- Weather type

Weather conditions include temperature, humidity, weather, PM2.5, air quality, sunrise and sunset, and cities can be freely selected. The weather conditions that can be selected differently depending on the device in the user account.

```java
/**
  * Create weather conditions
  *
  * @param place weather city 
  * @param type condition type
  * @param rule  condition regulations
  * @return
 */
 public static SceneCondition createWeatherCondition(
      PlaceFacadeBean place, 
      String type,
      Rule rule)
```
Note: The PlaceFacadeBean class object is obtained from the [Obtain City List](#citylist),[Obtain City By Altitude And Longitude](#ObtainCityAltitudeLongitude) and [Obtain City By City ID](#ObtainCityById) interface. Currently, the acquired urban interface only supports domestic cities.

- Device type

A device condition is a scheduled task for another device or devices triggered by a device which is in a certain state. **The same device cannot be used as both a condition and a task to avoid cycle control.**

```java
/**
  * Create device type conditions
  *
  * @param devBean  condition device
  * @param dpId    condition dpId
  * @param rule    condition regulations
  * @return
 */
public static SceneCondition createDevCondition(
      SceneDevBean devBean,
      String dpId,
      Rule rule) 
```
Note: SceneDevBean class object can be obtained from the interface of [Obtain the condition device list](#ObtainConditionDeviceList).

- Timer

Timer refers that the scheduled task can be executed when the specified time is reached.

```java
/**
   * Create timer conditions
   * @param display is used to display the user-selected time conditions.
   * @param name  Name of Timer condition
   * @param type condition type
   * @param rule  condition regulations
   * @return
  */
  public static SceneCondition createTimerCondition(String display,String name,String type,Rule rule)
```
#### <span id="rules">There are four rules for rule-condition rules:</span>

- Numerical type

Taking temperature as an example, the final expression of the numerical condition is formatted as "temp > 20". You can get the currently supported temperature maximum, minimum and granularity (stepping) from the Obtain Condition List interface; you can get the supported temperature from the Obtain Condition List, etc. After the configuration is completed on the user interface, the `ValueRule.newInstance` method is invoked to build the rules, and the rules are used to form the conditions.

For example:

```java
 ValueProperty tempProperty = (ValueProperty) conditionListBean.getProperty();       //Numeric Property


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
       “temp",            //Category
       tempRule           //Rule
 );
```
- Enumerated type

Taking the weather condition as an example, the final expression of the enumerated condition is formatted as "condition == rainy". You can get the currently supported weather conditions from the Obtain Condition List interface, including the code and name of each weather condition. After the configuration is completed on the user interface, the EnumRule.newInstancemethod is invoked to build the rules, and the rules are used to form the conditions.

For example:

 ```java
 EnumProperty weatherProperty = (EnumProperty) conditionListBean.getProperty();  //Enumeration type Property

/** 
 {
      {"sunny", " fine day"},
      {"rainy", "rainy day"}
 } 
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

Boolean types are common in device type conditions, and the final expression is formatted as "dp1 == true". You need to invoke the [Obtain the condition device list](#ObtainConditionDeviceList) interface to obtain devices that support the configuration of the smart scene, and then query the operations that the device can support based on the device id. See the Obtain Operations Supported by Device for details. After the configuration is completed on the user interface, the BoolRule.newInstancemethod is invoked to build the rules, and the rules are used to form the conditions.

For example:
```java
BoolProperty devProperty = (BoolProperty) conditionListBean.getProperty();  //Boolean type Property
/**
{
  {true, “on"},
  {false, "off"}
}
*/
HashMap<Boolean, String> boolMap = devProperty.getBoolMap(); 

//When the device starts.
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
- Timer type

Timer is expressed as a Map type, that is Key: Value. After the user completes the timer configuration, the `TimerRule.newInstance` is invoked to complete the Map data assembly by the SDK to form the rule condition.

For example:

```java

TimerProperty timerProperty = (TimerProperty)conditionListBean.
 getProperty();	//Timer-type property


 //TimerRule.newInstance provides two construction methods, the difference is whether it will pass the time zone.
 //If it does not pass the time zone, read default time zone.
 /**
   * 
   * @param timeZoneId time zone, the format like "Asia/Shanghai”
   * @param loops 7-digit character string; each digit represents what day of the week; the first digit represents Sunday, and the second digit represents Monday.
   * By analogy, the character indicates on which days the timer is enabled. 0 indicates not selected; 1 indicates selected, with format like only Monday Selected.
   * Tuesday: "0110000"。 If they are not selected, it means that the timer is only executed once, with the format: "0000000"
   * @param time 24-hour system With format like "08:00", 
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

 “Timer in work day",

 "timer",

 timerRule

 )


```

### Obtain condition list

**[Interface Description]**

It can be used to get a list of conditions that are currently supported by the user, as a first step in adding or modifying conditions usually.

**[Method Prototype]**

```java
/**
  * Obtain condition list
  * @param showFahrenheit shows Fahrenheit degree or not
  * @param callback
 */
void getConditionList(boolean showFahrenheit,IWiserResultCallback<List<ConditionListBean>> callback);
Among,  the interface provided by ConditionListBean is
/**
  * Obtain condition category
  *
  * @return category [1]
 */
public String getType() {
      return type;
}·

/**
  * Obtain condition name
  *
  * @return name 
 */
public String getName() {
      return name;
}
/**
  * Obtain Property [2]
  *
  * @return Property 
 */
public IProperty getProperty() {
      return property;
} 
```
**Note:**

1.Currently supported weather condition categories, names and Property types

| **Description**  | **Type**   | **Property Type** |
| ---------------- | ---------- | ----------------- |
| Temperature      | Temp       | ValueProperty     |
| Humidity         | humidity   | EnumProperty      |
| Weather          | condition  | EnumProperty      |
| PM2.5            | pm25       | EnumProperty      |
| Air quality      | aqi        | EnumProperty      |
| Sunrise & sunset | sunsetrise | EnumProperty      |
| Timer            | timer      | TimerProperty     |
	
2.Property is a commonly used data structure in Wiser smart to control devices and other functions. Currently, four properties are available: Numerical Type, Enumerated Type, Boolean Type, and Timer Type (corresponding to Value, Enum and Boolean in the condition), each property is provided with a different access interface. See the [rules introduction section](#rules) above for details.

**[Example Codes]**

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
### <span id="ObtainConditionDeviceList">Obtain the condition device list</span>

**[Description]**

Obtain a list of devices that can be used for conditional settings.

**[Method Prototype]**

```java
/**
  * Obtain a list of optional devices in the condition
  * @param homeId Home id
  * @param callback
 */

void getConditionDevList(long homeId, IWiserResultCallback<List<DeviceBean>> callback);

```
**[Example Codes]**  

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
### Obtain device tasks based on device id 

**[Description]**

It is used to obtain the tasks that can be selected when selecting the specific trigger conditions of the device.


**[Method Prototype]**

```java
  /**
     * Obtain a list of task conditions supported by the device
     *
     * @param devId    device id
     * @param callback
     */
      void getDeviceConditionOperationList(String devId, IWiserResultCallback<List<TaskListBean>> callback);
```

Among, `TaskListBean` provides the following interfaces:

```java
/**
 *  obtain the name of dp points for display interface.
 *
 * @return name of dp points
 */
public String getName() {
      return name;
}

/**
 *  Obtain dpId
 *
 * @return dpId
 */
public long getDpId() {
      return dpId;
}

/**
 * Obtain the operation configured by the dp point
 *
 *   Format:
 *     {
 *       {true, “on"},
 *       {false, "off"}
 *     {
 *
 * @return 

 */
public HashMap<Object, String> getTasks() {
      return tasks;
}
/**
 * Obtain the type bool, value, enum, etc. of the condition. 
 */
public String getType() {
      return type;
}
```
**[Example Codes]**
```java
WiserHomeSdk.getSceneManagerInstance().getDeviceConditionOperationList(
      devId, //Device id
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
### <span id="citylist">Obtain the city list</span>

**[Description]**

It is used to select a city when creating weather conditions. Note: Only Chinese cities are supported in the current city list for the time being.

**[Method Prototype]**

```java

/**
 Obtain the city list according to the country code.
 *
 * @param countryCode Country code
 * @param callback    callback
 */
void getCityListByCountryCode(String countryCode, IWiserResultCallback<List<PlaceFacadeBean>> callback);

```

Among, PlaceFacadeBean category provides interfaces as follows:

```java
/**
 * Obtain area name
 *
 * @return Area name
 */
public String getArea() {
      return area;
}

/**
 * Obtain name of province
 *
 * @return province name 
 */
public String getProvince() {
      return province;
}
/**
 * Obtain the city name
 *
 * @return city name 
 */
public String getCity() {
      return city;
}

/**
 * Obtain the city id
 *
 * @return city id
 */
public long getCityId() {
      return cityId;
}
```
**[Example Codes]**
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
### <span id="ObtainCityById">Obtain the city information according to the city id.</span>

**[Description]**

Obtain the city information according to the city id to display existing weather conditions. City id can be obtained from the [Obtain City List](#citylist) interface.

**[Method Prototype]**
```java
/**
 * Obtain the city information according to the city id.
 *
 * @param cityId   cityid{@link PlaceFacadeBean}
 * @param callback
 */
void getCityByCityIndex(long cityId, IWiserResultCallback<PlaceFacadeBean> callback);
```
**[Example Codes]**
```java
WiserHomeSdk.getSceneManagerInstance().getCityByCityIndex(
  	cityId, //City id
  	new IWiserResultCallback<PlaceFacadeBean>() {
  		@Override
  		public void onSuccess(PlaceFacadeBean placeFacadeBean) {

  		}

  		@Override
  		public void onError(String errorCode, String errorMessage) {

  		}

});
```
### <span id="ObtainCityAltitudeLongitude">Obtain the city information according to the altitude and longitude of city </span>

**[Description]**

Obtain the city information according to the longitude and latitude to display existing weather conditions.

**[Method Prototype]**
```java
/**
 * Obtain the city information according to the altitude and longitude of city
 *
 * @param lon      Longitude
 * @param lat      Latitude
 * @param callback
 */
void getCityByLatLng(String lon, String lat, IWiserResultCallback<PlaceFacadeBean> callback);
```
**[Example Codes]**
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
### Scene action

Scene actions refer to control actions performed when conditions trigger. Actions executable in manual scenarios include [smart device type](#Device_Type), [group device type](#Group_Type), [automation scenario type](#Scene_Type) and [delay type](#Delay_Type). The executable actions of automation scenario include [smart device type](#Device_Type), [group device type](#Group_Type), [manual scene type](#Scene_Type), [automation scene type](#Scene_Type), [delay type](#Delay_Type) and [message type](#Message_Type). The tasks that users can set vary depending on the user’s device. Please note that not every product supports the scene.

#### <span id="Device_Type">1.Create device type action</span>

**[Description]**

It is used to create device type actions.

**[Method Prototype]**

```java

/**
 * It is used to create device type actions.
 *
 * @param devId device id
 * @param tasks to be implemented task format: { dpId: dp point value}
 *   For example:
 *   {
 *     "1": true,
 *   }
 * @returnScene action
 */
SceneTask createDpTask(@NonNull String devId, HashMap<String, Object> tasks)

```
**[Example Codes]**

```java
HashMap<String, Object> taskMap = new HashMap<>();
taskMap.put("1", true); //Turn on the device
SceneTask task = WiserHomeSceneManager.getInstance().createDpTask(
      devId,      //Device id
      taskMap     //Device action
);
```


### <span id="ObtainExecutionAction">A list of devices supported by obtaining execution action</span>

**[Description]**

Obtain a list of devices supporting scene actions for selecting to add to the action to be executed.

**[Method Prototype]**

```java
/**
 * Obtain a list of optional devices in the action
 * @param homeId Home id
 * @param callback
 */
void getTaskDevList(long homeId, IWiserResultCallback<List<DeviceBean>> callback);
```

Among, **DeviceBean****provides interfaces as follows:**

```java
/**
 *  Obtain name of Device
 * 
 * @return Device name 
 */
public String getName() {
      return name;
}

/**
 *  Product ID
 * 
 * @return product id
 */

public String getProductId() {

      return productId;

}



/**
 *  Obtain id of device
 * 
 * @return device id
 */

public String getDevId() {

      return devId;

}



/**
 *  Obtain icon of device
 * 
 * @return icon address
 */

public String getIconUrl() {

       return iconUrl;

 }

/**
 * device is online
 * @return device is online
 */
 
public Boolean getIsOnline()

```
**[Example Codes]**

```java
WiserHomeSdk.getSceneManagerInstance().getTaskDevList(new IWiserResultCallback<List<DeviceBean>>() {
      @Override
      public void onSuccess(List<DeviceBean> deviceBeans) {
      }
      @Override
      public void onError(String errorCode, String errorMessage) {
      }

});
```
### Obtain executable actions based on device id

**[Description]**

It is used to obtain the tasks executed by the device when creating an action. The device id can be obtained from the [a list of devices supported by obtaining execution action](#ObtainExecutionAction)

**[Method Prototype]**

```java
/**
* Obtain what the device can execute
* @param devId    device id
* @param callback
*/
void getDeviceTaskOperationList(String devId, IWiserResultCallback<List<TaskListBean>> callback);
Among, TaskListBean provides interfaces as follows:
/**
 *  obtain the name of dp points for display interface.
 *
 * @return name of dp points
 */
public String getName() {
    return name;
}



/**
 *
 *  Obtain dpId
 * @return dpId
 */

public long getDpId() {

    return dpId;

}



/**
 * Obtain the operation configured by the dp point
 *
 *   Format:
 *     {
 *       {true, “on"},
 *       {false, "off"}
 *     }
 *
 * @return 
 */

public HashMap<Object, String> getTasks() {
    return tasks;
}
/**
 * Obtain the type bool, value, enum, etc. of the condition.
*/
public String getType() {
    return type;

}
```
**[Example Codes]**

```java
WiserHomeSdk.getSceneManagerInstance().getDeviceTaskOperationList(
    devId,      //Device id
    new IWiserResultCallback<List<TaskListBean>>() {
        @Override
        public void onSuccess(List<TaskListBean> conditionActionBeans) {
        }
       @Override
        public void onError(String errorCode, String errorMessage) {
       }

});
```
#### <span id="Group_Type">2.Create group device type action</span>

**[Description]**

It is used to create group device type actions.

**[Method Prototype]**

```java

/**
 * It is used to create group device type actions.
 *
 * @param group id
 * @param tasks to be implemented task format: { dpId: dp point value}
 *   For example:
 *   {
 *     "1": true,
 *   }
 * @returnScene action
 */
SceneTask createDpTask(@NonNull long groupId, HashMap<String, Object> tasks)

```

**[Example Codes]**

```java
HashMap<String, Object> taskMap = new HashMap<>();
taskMap.put("1", true); //Turn on the device
WiserHomeSceneManager.getInstance().createDpGroupTask(
	groupId, 	//group id
	taskMap 	//Device action
);
```

#### <span id="GetGroupActionDevList">A List of Group Devices to Get Execution Action Support</span>

**[Description]**

Obtain a list of devices that support scenario actions, including common devices and group devices, for selecting the actions to be added to.

**[Method Prototype]**

```java
/**
* Obtain a list of devices that support scenario actions, including groups and common devices
* @param homeId
* @param callback 
*/
getTaskDevAndGoupList(long homeId, IWiserResultCallback<SceneTaskGroupDevice> callback)
```
Among, `SceneTaskGroupDevice` provides interfaces as follows:


```java

/**
*  obtain a list of common devices
*/
public List<DeviceBean> getDevices() {
    return devices;
}
/**
*  obtain a list of group devices
*/
public List<GroupBean> getGoups() {
    return goups;
}

```


#### Obtain executable actions based on group id

**[Description]**

It is used to obtain the tasks executed by the group device when creating an action. The group id can be obtained from the [a list of group devices to get execution action support](#GetGroupActionDevList)

**[Method Prototype]**

```java
/**
* Obtain executable actions based on group id
*
* @param goupId   
* @param callback
*/
void getDeviceTaskOperationListByGroup(String goupId, IWiserResultCallback<List<TaskListBean>> callback)
```

#### <span id="Scene_Type">3.Create scenario type action</span>

**[Description]**

Scenario type actions are used to create scene type actions, including manual and automated scenarios. Parameters can be obtained through the [scenario list interface](#ObtainSceneList)

**[Method Prototype]**

```java
/**
 * create scene type action
 * @sceneBean scene object
 * @return sceneTask
 */
SceneTask createSceneTask(SceneBean sceneBean);

```

**[Example Codes]**

```java
WiserHomeSceneManager.getInstance().createSceneTask(scnenBean);
```

#### <span id="Delay_Type">4.Create delay type action</span>

**[Description]**

It is used to create delay type actions.

**[Method Prototype]**

```java

/**
 * Create delay type action
 * Maximum support for 59m59s
 * @param minute minutes
 * @param second seconds
 * @return sceneTask
 */
SceneTask createDelayTask(int minute, int second);

```

**[Example Codes]**

```java
WiserHomeSceneManager.getInstance().createDelayTask(
	2,  //minutes
	2	//seconds
);
```


#### <span id="Message_Type">5.Create message type action</span>

**[Description]**

It is used to create message type actions.

**[Method Prototype]**

```java
/**
 * create message type action
 * @return
 */
SceneTask createPushMessage();

```

**[Example Codes]**

```java
WiserHomeSceneManager.getInstance().createPushMessage();
```

## <span id="Scene_operation">Scene Operation</span>
WiserHomeSdk provides four operations for creating, modifying, executing, and deleting a single scene. In addition to creating other operations, the scene ID needs to be initialized. The scene ID can be obtained from the interface of [obtaining the scene list interface.](#ObtainSceneList)

### Create Scene

**[Description]**

It is used to assemble conditions and actions into a scene and create a new scene, and then returns the scene data after success. There are two creation methods, and the only difference is whether there are stickyOnTop parameters.

**[Method Prototype]**

```java
/**
 * Create Scene
 *
 * @param homeId	  Home id
 * @param name      Scene name 
 * @param stickyOnTop shows in the home page or not
 * @param conditions Scene triggering conditions {@link SceneCondition}
 * @param tasks     Scene task {@link SceneTask}
 * @param matchType Scene condition and/or relationship  SceneBean.MATCH_TYPE_OR represents that it satisfies any conditions, default value; SceneBean.MATCH_TYPE_AND represents that it satisfies all conditions
 * @param callback   callback

 */

public void createScene(long homeId, String name, boolean stickyOnTop, String background, List<SceneCondition> conditions, List<SceneTask> tasks,int matchType, final IWiserResultCallback<SceneBean> callback) ;

/**
 * Create Scene
 *
 * @param homeId	  Home id
 * @param name      Scene name 
 * @param conditions Scene triggering conditions {@link SceneCondition}
 * @param tasks     Scene task {@link SceneTask}
 * @param matchType Scene condition and/or relationship  SceneBean.MATCH_TYPE_OR represents that it satisfies any conditions, default value; SceneBean.MATCH_TYPE_AND represents that it satisfies all conditions
 * @param callback   callback
 */

public void createScene(long homeId, String name, String background, List<SceneCondition> conditions, List<SceneTask> tasks,int matchType, final IWiserResultCallback<SceneBean> callback) ;
```
**[Example Codes]**

```java
WiserHomeSdk.getSceneManagerInstance().createScene(
	 "100001"
    “Morning", // Scene name
    true,  //Show it in the home page or not
    conditions, //condition
    tasks,     //task
    SceneBean.MATCH_TYPE_AND, //Implement condition type
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
### Modify the scene

**[Description]**

It is used to modify the scene. After it succeeded, it will return to new scene data.

**[Method Prototype]**

```java

/**
 * Modify the scene
 * 
 * @param sceneReqBean Scene data class
 * @param callback
 */

void modifyScene(SceneBean sceneReqBean, IWiserResultCallback<SceneBean> callback);
```
Note: The interface can only be used to modify the scene. Do not transmit into the newly created SceneBean object.

**[Example Codes]**

```java
sceneBean.setName("New name");  //Change Scene name 
sceneBean.setConditions(Collections.singletonList(condition)); //Change Scene condition
sceneBean.setActions(tasks); //Change Scene action
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
### Execute scene

**[Description]**

It is used to execute manual scene.


Note: This method only sends commands to the cloud execution scenario. If the specific device is executed successfully, you need to monitor the device's dp point change through WiserHomeSdk.newDeviceInstance(devId).registerDevListener().

**[Method Prototype]**

```java
/**
 * Perform scene actions
 *
 * @param callback
 */
void executeScene(IResultCallback callback);
```
**[Example Codes]**

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
###  Delete scene

**[Description]**

For deleting scene

**[Method Prototype]**

```java
/**
 * Delete Scene
 *
 * @param callback
 */
void deleteScene(IResultCallback callback);
```
**[Example Codes]**

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
### Turn on and turn off the automation scene

**[Description]**

It is used to turn on or off the automatic scene.

**[Method Prototype]**

```java
/**
 * Turn on automation scene
 * @param sceneId  
 * @param callback
 */
void enableScene(String sceneId, final IResultCallback callback);

/**
 * Turn off the automation scene
 * @param sceneId  
 * @param callback
 */
void disableScene(String sceneId, final IResultCallback callback);
```
**[Example Codes]**

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
### Sort scene

**[Description]**

Manual scene or automation scene sorting. Note: Manual or automation scenes can only be sorted separately and cannot be shuffled.

**[Method Prototype]**

```java
/**
 * Scene sorting
 * @param homeId family id
 * @param sceneIds  Sorted id list for manual or automation scenes 
 * @param callback    callback
 */
void sortSceneList(long homeId, List<String> sceneIds, IResultCallback callback)
```
**[Example Codes]**

```java
WiserHomeSdk.getSceneManagerInstance().sortSceneList(
    homeId, //Home list
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
### Scene Background Images

**[Description]**

Get scene background images


**[Method Prototype]**

```java
/**
* 
* @param callback callback
*/
 void getSceneBgs(IWiserResultCallback<ArrayList<String>> callback);
```

**[Example Codes]**

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

### Erase

**[Description]**

If the user exits the activity of the scene, the scene destruction method should be invoked to reclaim the memory and enhance the experience.

**[Example Codes]**

```java
WiserHomeSdk.getSceneManagerInstance().onDestroy();
WiserHomeSdk.newSceneInstance(sceneId).onDestroy();
```
