# Wi-Fi Network Configuration
The network configuration modes supported by Wiser SDK including:

- Pairing through Wi-Fi easy connect
- Pairing through hotspot
- Camera scan code network configuration
- Wired network configuration
- Sub-device configuration
- Scan the QR code of the device configuration
- Lightning search or activate
- NB device activate
- Bluetooth configuration

## Terms

| Terms | Description |
| ---- | ---- |
| Wi-Fi device | The device that use a Wi-Fi module to connect the router, and interact with the app and cloud. |
| Pairing through Wi-Fi easy connect | Also known as the quick connection mode, the app packs the network data packets into the designated area of the 802.11 data packets and sends them to the surrounding environment. The Wi-Fi module of the smart device is in mingled status and monitors and captures all the packets in the network. According to the agreed protocol data format, it can parse out the network information packet sent by the app.|
| Pairing through hotspot | Also known as hotspot mode, the mobile phone connects the smart device's hotspot. The two parties establish a Socket connection to exchange data through the agreed port. |
| Camera scan code configuration network | The camera device obtains the configuration data information by scanning the QR code on the app. |
| Wired devices |Devices connected to the router via a wired network, such as Zigbee wired gateway, wired camera, etc.|
| sub-device |Devices that interact with app and cloud data through gateways, such as Zigbee sub-devices|
| Zigbee | Zigbee technology is a short-range, low-complexity, low-power, low-speed, low-cost two-way wireless communication technology. It is mainly used for data transmission between various electronic devices with short distances, low power consumption, and low transmission rates, as well as typical applications with periodic data, intermittent data, and low response time data transmission.|
| Zigbee gateway | The device that integrates the coordinator and Wi-Fi functions in the Zigbee network is responsible for the establishment of the Zigbee network and the storage of data information.|
| Zigbee sub-device | Routing or terminal equipment in Zigbee network, responsible for data forwarding or terminal control response.|

## Instructions

Before developing a Wi-Fi device network config, you need to understand the basic logic of WiserHomeSDK, and have used WiserHomeSdk to complete the basic operations such as logging in and creating a home.

## Implementation

### Quick connection mode

![](https://airtake-public-data-1254153901.cos.ap-shanghai.myqcloud.com/goat/20201225/1b18bb5b2bb44ac094dcef538de53ef5.png)

#### Initialize parameters

```java
ActivatorBuilder builder = new ActivatorBuilder()
		.setSsid(ssid)
		.setContext(context)
		.setPassword(password)
		.setActivatorModel(ActivatorModelEnum.TY_EZ)
		.setTimeOut(timeout)
		.setToken(token)
		.setListener(new IWiserSmartActivatorListener() {

				@Override
				public void onError(String errorCode, String errorMsg) {

				}

				@Override
				public void onActiveSuccess(DeviceBean devResp) {
					//If multiple devices are activated at the same time, they will be called back multiple times
				}

				@Override
				public void onStep(String step, Object data) {

				}
			}
		));
```

**Parameters**

| Parameters | Description |
| ---- | ---- |
| token | Activation key required for Configuration |
| context | context |
| ssid | WiFi ssid|
| password | WiFi password|
| activatorModel | Configuration Mode, EZ Mode: ActivatorModelEnum.TY_EZ |
| timeout | Configuration timeout, default setting is 100s, unit is second|

**Get Network Configuration Token**

Before the Wi-Fi network configuration, the SDK needs to obtain the network configuration Token from the Wiser IoT.

The term of validity of Token is 10 minutes, and the Token becomes invalid once the network configuration succeeds.

A new Token has to be obtained if you have to reconfigure the network.

```java
WiserHomeSdk.getActivatorInstance().getActivatorToken(homeId,
		new IWiserActivatorGetToken() {

			@Override
			public void onSuccess(String token) {

			}

			@Override
			public void onFailure(String s, String s1) {

			}
		});
```

**Parameters**

| Parameters | Description |
| ---- | ---- |
| homeId | Family ID, please refer to the family management section for details |

#### Configuration method invocation

```java
IWiserActivator mWiserActivator = WiserHomeSdk.getActivatorInstance().newMultiActivator(builder);
//Start configuration
mWiserActivator.start();
//Stop configuration
mWiserActivator.stop();
//Exit the page to destroy some cache data and monitoring data.
mWiserActivator.onDestroy();
```

### Hotspot mode

![](https://airtake-public-data-1254153901.cos.ap-shanghai.myqcloud.com/goat/20201225/a3f7c3a55f404e64adb13737b657dd7f.png)

#### Initialize parameters

```java
ActivatorBuilder builder = new ActivatorBuilder()
		.setContext(context)
		.setSsid(ssid)
		.setPassword(password)
		.setActivatorModel(ActivatorModelEnum.TY_AP)
		.setTimeOut(timeout)
		.setToken(token)
		.setListener(new IWiserSmartActivatorListener() {

				@Override
				public void onError(String errorCode, String errorMsg) {

				}

				@Override
				public void onActiveSuccess(DeviceBean devResp) {

				}

				@Override
				public void onStep(String step, Object data) {

				}
			}
		));
```

**Parameters**

| Parameters | Description |
| ---- | ---- |
| token | Activation key required for Configuration |
| context | context |
| ssid | Wi-Fi ssid|
| password | Wi-Fi password|
| activatorModel | Configuration Mode, AP Mode: ActivatorModelEnum.TY_AP |
| timeout | Configuration timeout, default setting is 100s, unit is second|

**Get Network Configuration Token**

Before the Wi-Fi network configuration, the SDK needs to obtain the network configuration Token from the Wiser IoT.

The term of validity of Token is 10 minutes, and the Token becomes invalid once the network configuration succeeds.

A new Token has to be obtained if you have to reconfigure the network.

```java
WiserHomeSdk.getActivatorInstance().getActivatorToken(homeId,
	new IWiserActivatorGetToken() {

		@Override
		public void onSuccess(String token) {

		}

		@Override
		public void onFailure(String s, String s1) {

		}
	});
```
**Parameters**

| Parameters | Description |
| ---- | ---- |
| homeId | Family ID, please refer to the family management section for details |

#### Configuration method invocation

```java
IWiserActivator mWiserActivator = WiserHomeSdk.getActivatorInstance().newActivator(builder);
//Start configuration
mWiserActivator.start();
//Stop configuration
mWiserActivator.stop();
//Exit the page to destroy some cache data and monitoring data.
mWiserActivator.onDestroy();
```

### Camera scan code network configuration

#### Description

Use the camera device to scan the QR code of the app to transfer the Configuration information to active and bind the camera device.

![image.png](https://airtake-public-data-1254153901.cos.ap-shanghai.myqcloud.com/goat/20201228/1c089f2df8cc4749afc34c46dd4d29bd.png)

#### Initialize parameters

```java
WiserCameraActivatorBuilder builder = new WiserCameraActivatorBuilder()
		.setContext(context)
		.setSsid(ssid)
		.setPassword(password)
		.setToken(token)
		.setTimeOut(timeout)
		.setListener(new IWiserSmartCameraActivatorListener() {
			@Override
			public void onQRCodeSuccess(String qrcodeUrl) {
				//Return URL link to generate QR code
			}

			@Override
			public void onError(String errorCode, String errorMsg) {
				//Network configuration failed
			}

			@Override
			public void onActiveSuccess(DeviceBean devResp) {
			//Network configuration succeed
			}
		}));
```
**Parameters**

| Parameters | Description |
| ---- | ---- |
| token | Activation key required for Configuration |
| context | context |
| ssid | WiFi ssid|
| password | WiFi password|
| timeout | Configuration timeout, default setting is 100s, unit is second|

**Get Network Configuration Token**

Before the Wi-Fi network configuration, the SDK needs to obtain the network configuration Token from the Wiser IoT.

The term of validity of Token is 10 minutes, and the Token becomes invalid once the network configuration succeeds.

A new Token has to be obtained if you have to reconfigure the network.

```java
WiserHomeSdk.getActivatorInstance().getActivatorToken(homeId,
		new IWiserActivatorGetToken() {

			@Override
			public void onSuccess(String token) {

			}

			@Override
			public void onFailure(String s, String s1) {

			}
		});
```
**Parameters**

| Parameters | Description |
| ---- | ---- |
| homeId | Family ID, please refer to the family management section for details |

#### Configuration Method Invocation

* Instance class

	```java
	IWiserCameraDevActivator mWiserActivator = WiserHomeSdk.getActivatorInstance().newCameraDevActivator(builder);
	```

* Get QR code URL link

	```java
	mWiserActivator.createQRCode(); //Return via onQRCodeSuccess callback
	```

* Generate QR code based on URL

	Examples: Need to implement zxing (implementation `com.google.zxing:core:3.2.1`)

	```java
	public static Bitmap createQRCode(String url, int widthAndHeight)
				throws WriterException {
			Hashtable hints = new Hashtable();
			hints.put(EncodeHintType.CHARACTER_SET, "utf-8");
			hints.put(EncodeHintType.MARGIN,0);
			BitMatrix matrix = new MultiFormatWriter().encode(url,
					BarcodeFormat.QR_CODE, widthAndHeight, widthAndHeight, hints);

			int width = matrix.getWidth();
			int height = matrix.getHeight();
			int[] pixels = new int[width * height];

			for (int y = 0; y < height; y++) {
				for (int x = 0; x < width; x++) {
					if (matrix.get(x, y)) {
						pixels[y * width + x] = BLACK;
					}
				}
			}
			Bitmap bitmap = Bitmap.createBitmap(width, height,
					Bitmap.Config.ARGB_8888);
			bitmap.setPixels(pixels, 0, width, 0, 0, width, height);
			return bitmap;
		}
	```

* Start configuration

	```java
	mWiserActivator.start();
	```

* Stop configuration

	```java
	mWiserActivator.stop();
	```

* Exit the page to destroy some cache data and monitoring data

	```java
	mWiserActivator.onDestory();
	```

### Wired network configuration

#### Description

A wired device refers to the connection of the router through a wired network, without entering the hotspot name and password of the router during the network configuration. The Zigbee cable gateway is used to introduce the cable configuration network business process.

![image.png](https://airtake-public-data-1254153901.cos.ap-shanghai.myqcloud.com/goat/20201228/48362e2a3c8f448cac09f9a90209f2a8.png)

#### Discovery device

Wiser SDK provides the function of discovering wired devices. You should register the notification of the wired device to get device information. Before obtaining the device, the phone must be connected to the same network as the device.

```java
IWiserGwSearcher mWiserGwSearcher = WiserHomeSdk.getActivatorInstance().newWiserGwActivator().newSearcher();
		mWiserGwSearcher.registerGwSearchListener(new IGwSearchListener() {
			@Override
			public void onDevFind(HgwBean hgwBean) {

			}
		});
```
**Parameters**

| Parameters | Description |
| ---- | ---- |
| hgwBean | gateway data entity discovered |

#### Initialize parameters

* Used device discovery function

```java
IWiserActivator mIWiserActivator = WiserHomeSdk.getActivatorInstance().newGwActivator(
		new WiserGwActivatorBuilder()
			.setToken(token)
			.setTimeOut(timeout)
			.setContext(context)
			.setHgwBean(hgwBean)
			.setListener(new IWiserSmartActivatorListener() {

					@Override
					public void onError(String errorCode, String errorMsg) {

					}

					@Override
					public void onActiveSuccess(DeviceBean devResp) {

					}

					@Override
					public void onStep(String step, Object data) {

					}
			}
		));
```
**Parameters**

| Parameters | Description |
| ---- | ---- |
| token | Activation key required for Configuration |
| timeout | Configuration timeout, the default setting is 100s, the unit is second|
| context | context |
| hgwBean | the discovered gateway data entity |

* Unused device discovery function

```java
IWiserActivator mIWiserActivator = WiserHomeSdk.getActivatorInstance().newGwActivator(
		new WiserGwActivatorBuilder()
			.setToken(token)
			.setTimeOut(timeout)
			.setContext(context)
			.setListener(new IWiserSmartActivatorListener() {

					@Override
					public void onError(String errorCode, String errorMsg) {

					}

					@Override
					public void onActiveSuccess(DeviceBean devResp) {

					}

					@Override
					public void onStep(String step, Object data) {

					}
			}
		));
```

**Parameters**

| Parameters | Description |
| ---- | ---- |
| token | Activation key required for Configuration |
| timeout | Configuration timeout, the default setting is 100s, the unit is second|
| context | context |

**Get network configuration token**

Before the Wi-Fi network configuration, the SDK needs to obtain the network configuration Token from the Wiser IoT.

The term of validity of Token is 10 minutes, and the Token becomes invalid once the network configuration succeeds.
A new Token has to be obtained if you have to reconfigure the network.

```java
WiserHomeSdk.getActivatorInstance().getActivatorToken(homeId,
		new IWiserActivatorGetToken() {

			@Override
			public void onSuccess(String token) {

			}

			@Override
			public void onFailure(String s, String s1) {

			}
		});
```
**Parameters**

| Parameters | Description |
| ---- | ---- |
| homeId | Family ID, please refer to the family management section for details |

#### Configuration method invocation

```java
IWiserActivator mIWiserActivator = WiserHomeSdk.getActivatorInstance().newGwActivator(builder);
//Start the network pairing
mIWiserActivator.start()
//Stop the network pairing
mIWiserActivator.stop()
//What to do if the user leaves the page.
mIWiserActivator.onDestroy()
```

### Sub-device configuration

#### Description

The sub-device configuration network can only be initiated when the gateway device cloud is online, and the sub-device is in the network configuration state. The following uses the Zigbee gateway sub-device as an example to introduce the configuration network business process

![image.png](https://airtake-public-data-1254153901.cos.ap-shanghai.myqcloud.com/goat/20201228/f93b7264564b48d4a745f38d5e43f72d.png)

#### Initialize parameters

```java
WiserGwSubDevActivatorBuilder builder = new WiserGwSubDevActivatorBuilder()
		.setDevId(mDevId)
		.setTimeOut(timeout)
		.setListener(new IWiserSmartActivatorListener() {

				@Override
				public void onError(String errorCode, String errorMsg) {

				}

				@Override
				public void onActiveSuccess(DeviceBean devResp) {

				}

				@Override
				public void onStep(String step, Object data) {

				}
			}
		));
```

**Parameters**

| Parameters | Description |
| ---- | ---- |
| mDevId | Setting the gateway ID |
| timeout | Setting the time-out period for network configuration |

#### Configuration method invocation

```java
IWiserActivator mWiserGWActivator = WiserHomeSdk.getActivatorInstance(). newGwSubDevActivator(builder);
// Start network configuration
mWiserGWActivator.start();
// Stop network configuration
mWiserGWActivator.stop();
// Destroy
mWiserGWActivator.onDestory();
```

### Scan the QR code of the device configuration

#### Description

This feature is only available for devices connected to the Internet

![image.png](https://airtake-public-data-1254153901.cos.ap-shanghai.myqcloud.com/goat/20201228/e71c74e25f204ff29701913925e86af4.png)

#### Get device uuid

```java
Map<String, Object> postData = new HashMap<>();
//get url by scanning the QR code
postData.put("code", url);

WiserHomeSdk.getRequestInstance().requestWithApiNameWithoutSession("wiser.m.qrcode.parse", "4.0", postData, String.class, new IWiserDataCallback<String>() {
    @Override
    public void onSuccess(String result) {
      //get uuid from result
      Log.i("TAG" , result);
    }

    @Override
    public void onError(String errorCode, String errorMessage) {
        Log.i("TAG" , errorCode);
    }
});
```

#### Initialize parameters

```java
WiserQRCodeActivatorBuilder builder = new WiserQRCodeActivatorBuilder()
        .setUuid(uuid)
        .setHomeId(homeId)
        .setContext(mActivity)
        .setTimeOut(timeout)
        .setListener(new IWiserSmartActivatorListener() {

                @Override
                public void onError(String errorCode, String errorMsg) {

                }

                @Override
                public void onActiveSuccess(DeviceBean devResp) {

                }

                @Override
                public void onStep(String step, Object data) {

                }
            }
        ));
```

**Parameters**

| Parameters | Description |
| ---- | ---- |
| uuid | Device Uuid |
| homeId | Family ID, please refer to the family management section for details |
| timeout | Setting the time-out period for network configuration, The default is 100s |

#### Configuration method invocation

```java
IWiserActivator mWiserActivator = WiserHomeSdk.getActivatorInstance().newQRCodeDevActivator(builder);
// Start network configuration
mWiserActivator.start();
// Stop network configuration
mWiserActivator.stop();
// Destroy
mWiserActivator.onDestory();
```

### Lightning search or activate

#### Process schematic

![LightningDeviceSearchActivate.png](https://airtake-public-data-1254153901.cos.ap-shanghai.myqcloud.com/goat/20210128/94a1e178e5a042a2b838357e7f0bc849.png)

**Parameter Description**

| Parameter | Type | Description |
| --- | --- | --- |
| devIds | List<String> | The devId set of configured network devices |
| serverTimeout | long | second |
| clientTimeout | long | second |
| IWiserLightningSearchListener | Callback | Lightning Search callback |

#### Code example

```java
WiserHomeSdk.getActivatorInstance().newLightningActivator().startSearch(devList, serverTimeout, clientTimeout, new IWiserLightningSearchListener() {
            @Override
            public void onSearchResponse(LightningSearchBean bean) {
                //search result callback
            }
        });
```

#### Lightning activate

**Parameter Description**

| Parameter | Type | Description |
| --- | --- | --- |
| lightningSearchBeanList | List<LightningSearchBean> | Lightning devices that have been searched |
| token | String | Activation key required for network distribution |
| timeout | Int | Network timeout period, unit ms, 120s recommended |
| IWiserDevActivatorListener | Callback | Network distribution result callback |

**Obtain token**

Before starting the network configuration, the SDK needs to obtain the network distribution Token from Wiser IoT in the online state. The validity period of the Token is 10 minutes, and it will become invalid after the configuration is successful (the network needs to be re-obtained again).

**Parameter Description**

| Parameter | Type | Description |
| --- | --- | --- |
| homeId | String | Family id, refer to the chapter on family management for details |

#### Code example

```java
WiserHomeSdk.getActivatorInstance().getActivatorToken(homeId, new IWiserActivatorGetToken() {
    @Override
    public void onSuccess(String token) {

    }

    @Override
    public void onFailure(String errorCode, String errorMsg) {

    }
});
```

#### Code example

```java
WiserHomeSdk.getActivatorInstance()
        .newLightningActivator()
        .startActive(new WiserLightningDevActivatorBuilder()
                .setLightningSearchBeanList(lightningSearchBeans)
                .setTimeOut(60 * 1000)
                .setToken(token)
                .setListener(new IWiserDevActivatorListener() {
                    @Override
                    public void onError(String errorCode, String errorMsg) {

                    }

                    @Override
                    public void onActiveSuccess(DeviceBean devResp) {

                    }
                }));
```

### NB device activate

#### Function description

Scan the QR code of the NB device to activate.

**Scanning the QR code of NB device**

1. **get device id using common interface**.

	Scan the QR code of the device to get the URL, and then get the id through the general interface

	**Common interface call documentation and code examples**

	

	**Parameter Description**

	| **Key**  | **Value**  |
	| --- | --- |
	| apiName | wiser.m.qrcode.parse |
	| version | 4.0 |
	| postData | {"code":url} |

2. **NB device activate**

	**Parameter Description**

	| **Key**  | **Value** |
	| --- | --- |
	| apiName | wiser.m.nb.device.user.bind |
	| version | 1.0 |
	| postData | {"hid":id,"timeZone":String} |
	| gid | homeId |


### Bluetooth configuration

For Bluetooth device configuration, you can refer to the document Bluetooth.