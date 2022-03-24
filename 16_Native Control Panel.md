# Native Control Panel
The native control panel supports most Wiser Smart products and functions. You can quickly integrate product capabilities powered by Wiser into devices with simple access and let users easily experience different smart devices.

## Advantages

* Native lite solution, without React Native frameworks.
* Quick plan for testing products, which is also applicable to the model room building environment.
* Easy to debug and understand in the development stage, DP (data points) updated dynamically.

	<p> <img src="https://airtake-public-data-1254153901.cos.ap-shanghai.myqcloud.com/goat/20210218/55df2d386223476ea4ea1a1cb646820e.jpg" width = "250" / style='vertical-align:middle; display:inline;border:1px solid black'>	<img src="https://airtake-public-data-1254153901.cos.ap-shanghai.myqcloud.com/goat/20210218/1c25a3bc99d14d99b9c98bb4a9cc3138.jpg" width = "250" / style='vertical-align:middle; display:inline;border:1px solid black'> </p>

### Enable native control panel

**Interface description**

```java
void openDefaultPanel(Context context, String devId, MenuBean menuBean);
```

**Parameter description**

| Parameters | Description |
| ---- | ---- |
| context | Context for opening the Activity |
| devId | Device Id |
| menuBean | Used to create and display custom menus and events |

> **Note:** `menuBean` is used to create and display custom menus and events, you can set it null if you don't need it.

**MenuBean data model**

| Filed | Type | Description |
| ---- | ---- | ---- |
| menuRes | Int | Custom menu resource id |
| menuItemId | Int | Item id in custom menu |
| bundle | Bundle | Custom bundle can be obtained in custom Activity by IDefaultPanelController.BUNDLE_KEY |
| activityClassName | String | Custom activity ClassName，like TestActivity.class.getName() |

**Sample code**

```java
MenuBean menuBean = new MenuBean();
menuBean.setMenuRes(R.menu.common_menu);
menuBean.setMenuItemId(R.id.check);
Bundle bundle = new Bundle();
bundle.putString("DEV_ID_KEY", devId);
menuBean.setBundle(bundle);
menuBean.setActivityClassName(TestActivity.class.getName());
IDefaultPanelController defaultPanelController = PluginManager.service(IDefaultPanelController.class);
defaultPanelController.openDefaultPanel(context, devId, menuBean);
```

> **Note:** The native control panel uses `startActivityForResult(Intent, IDefaultPanelController.REQUEST_CODE_DEFAULT_PANEL)` to enable the custom activity. If the `onActivityResult` shows that the `(requestCode == IDefaultPanelController.REQUEST_CODE_DEFAULT_PANEL && resultCode == RESULT_OK)` is `true`, the default panel will be closed.