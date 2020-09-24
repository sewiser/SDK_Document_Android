# Wi-Fi Network Configuration

## Functional Overview

The network configuration modes supported by Wiser SDK including:

- Quick Connection (EZ) Mode 
- Hotspot (AP) Mode
- Camera Scan Code Network Configuration
- Wired Network Configuration
- Sub-device Configuration 
- Bluetooth Configuration

| Attributes | Description |
| -------- | -------------------------------------------------------  |
| Wi-Fi Device | The device that use Wi-Fi module to connect the router, and interact with APP and cloud. |
| EZ mode   | Also known as the quick connection mode, the APP packs the network data packets into the designated area of the 802.11 data packets and sends them to the surrounding environment. The Wi-Fi module of the smart device is in the promiscuous model and monitors and captures all the packets in the network. According to the agreed protocol data format, it can parse out the network information packet sent by the APP.|
| AP mode   | Also known as hotspot mode, the mobile phone connects the smart device's hotspot. The two parties establish a Socket connection to exchange data through the agreed port. |
| Camera scan code configuration network | The camera device obtains the configuration data information by scanning the QR code on the APP. |
| Wired Devices |Devices connected to the router via a wired network, such as ZigBee wired gateway, wired camera, etc.|
| sub-device |Devices that interact with APP and cloud data through gateways, such as ZigBee sub-devices|
| ZigBee | ZigBee technology is a short-range, low-complexity, low-power, low-speed, low-cost two-way wireless communication technology. It is mainly used for data transmission between various electronic devices with short distances, low power consumption and low transmission rates, as well as typical applications with periodic data, intermittent data and low response time data transmission.|
| ZigBee Gateway | The device that integrates the coordinator and WiFi functions in the ZigBee network is responsible for the establishment of the ZigBee network and the storage of data information.|
| ZigBee sub-device | Routing or terminal equipment in ZigBee network, responsible for data forwarding or terminal control response.|

## Instructions
Before developing Wi-Fi device network config, you need to understand the basic logic of WiserHomeSDK, and have used WiserHomeSdk to complete the basic operations such as logging in and creating a home.

## Implementation

### Quick Connection Mode

```sequence
Title: EZ Mode

participant APP
participant Device
participant Service

Note over APP: Connect to the WiFi of router
Note over Device: Switch to the EZ mode

APP-->Service: Get Token
Service-->APP: Response Token

Note over APP: Start network configuration (send configuration data), broadcast configuration data
Device->Device: Get configuration data

APP-->Server: Use the token to poll the list of network activation devices every 2 seconds (the total duration is 100s by default)

Device->Service: Activate the device
Service-->Device: Network configuration succeeds

Server-->APP: Network configuration succeeds
```

#### Initialize Parameters

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
                    
                }
                
                @Override
                public void onStep(String step, Object data) {
                    
                }
            }
        ));
```
**Parameters**

| Parameters         | Description |
| ------------ | -------------------------- |
| token           | Activation key required for Configuration |
| context         | context |
| ssid            | WiFi ssid|
| password        | WiFi password|
| activatorModel  | Configuration Mode，EZ Mode：ActivatorModelEnum.TY_EZ |
| timeout         | Configuration timeout, default setting is 100s, unit is second|

**Get Network Configuration Token**

Before the Wi-Fi network configuration, the SDK needs to obtain the network configuration Token from the Wiser Cloud.
The term of validity of Token is 10 minutes, and the Token become invalid once the network configuration succeeds.
A new Token has to be obtained if you have to reconfigure network.

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

| Parameters         | Description |
| ------------ | -------------------------- |
| homeId          | Family ID, please refer to the family management section for details |

#### Configuration Method Invocation

```java
IWiserActivator mWiserActivator = WiserHomeSdk.getActivatorInstance().newMultiActivator(builder);
//Start configuration
mWiserActivator.start();
//Stop configuration
mWiserActivator.stop(); 
//Exit the page to destroy some cache data and monitoring data.
mWiserActivator.onDestroy(); 
```

### Hotspot Mode

```sequence
Title: AP Mode

participant APP
participant Device
participant Service

Note over Device: Switch to the AP mode

APP-->Service: Get Token
Service-->APP: Response Token

Note over APP: Connect the hotspot device

APP->Device: Start network configuration (send configuration data), send configuration data

APP-->Server: Use the token to poll the list of network activation devices every 2 seconds (the total duration is 100s by default)

Note over Device: Device turns off hotspot automatically
Note over Device: The device is connected to the Wi-Fi of router

Device->Service: Activate the device
Service-->Device: Network configuration succeeds

Server-->APP: Network configuration succeeds

```

#### Initialize Parameters

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

| Parameters         | Description |
| ------------ | -------------------------- |
| token           | Activation key required for Configuration |
| context         | context |
| ssid            | Wi-Fi ssid|
| password        | Wi-Fi password|
| activatorModel  | Configuration Mode，AP Mode：ActivatorModelEnum.TY_AP |
| timeout         | Configuration timeout, default setting is 100s, unit is second|

**Get Network Configuration Token**

Before the Wi-Fi network configuration, the SDK needs to obtain the network configuration Token from the Wiser Cloud.
The term of validity of Token is 10 minutes, and the Token become invalid once the network configuration succeeds.
A new Token has to be obtained if you have to reconfigure network.

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

| Parameters         | Description |
| ------------ | -------------------------- |
| homeId          | Family ID, please refer to the family management section for details |

#### Configuration Method Invocation

```java
IWiserActivator mWiserActivator = WiserHomeSdk.getActivatorInstance().newActivator(builder);
//Start configuration
mWiserActivator.start(); 
//Stop configuration
mWiserActivator.stop(); 
//Exit the page to destroy some cache data and monitoring data.
mWiserActivator.onDestroy(); 
```

### Camera Scan Code Network Configuration

#### Description

Use the camera device to scan the QR code of the APP to transfer the Configuration information to active and bind the camera device.


```sequence

Title: Camera scan code Network Configuration

participant APP
participant Camera
participant Server

Note over APP: Connect to the router 
Note over Camera: resetting the device status
APP-->Server: Get Token
Server-->APP: Response Token

Note over APP: Generate QR code through ssid / password / token

Camera-->APP: Get the ssid / password / token by scanning the QR code on the APP
APP-->Server: Use the token to poll the list of network activation devices every 2 seconds (the total duration is 100s by default)
Camera-->Server: Activate the device
Server-->Camera: Network configuration succeeds

Server-->APP: Network configuration succeeds

```

#### Initialize Parameters

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

| Parameters         | Description |
| ------------ | -------------------------- |
| token           | Activation key required for Configuration |
| context         | context |
| ssid            | WiFi ssid|
| password        | WiFi password|
| timeout         | Configuration timeout, default setting is 100s, unit is second|

**Get Network Configuration Token**

Before the Wi-Fi network configuration, the SDK needs to obtain the network configuration Token from the Wiser Cloud.
The term of validity of Token is 10 minutes, and the Token become invalid once the network configuration succeeds.
A new Token has to be obtained if you have to reconfigure network.

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

| Parameters         | Description |
| ------------ | -------------------------- |
| homeId          | Family ID, please refer to the family management section for details |

#### Configuration Method Invocation

* Instance class

```java
IWiserCameraDevActivator mWiserActivator = WiserHomeSdk.getActivatorInstance().newCameraDevActivator(builder);
```

* Get QR code URL link

```java
mWiserActivator.createQRCode(); //Return via onQRCodeSuccess callback
```

* Generate QR code based on url

Examples：Need to implement zxing（ implementation 'com.google.zxing:core:3.2.1' ）

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

### Wired Network Configuration

#### Description

Wired device refers to the connection of the router through a wired network, without entering the hotspot name and password of the router during the network configuration. The ZigBee cable gateway is used to introduce the cable configuration network business process.

```sequence
Title: Zigbee Gateway Configuration

participant APP
participant ZigBee Gateway
participant Service

Note over ZigBee Gateway: Reset ZigBee Gateway

APP-->Service: Get Token
Service-->APP: Response Token

APP -> APP: connect mobile phone to the same hotspot of the Gateway

Device-->APP: broadcast configuration data
APP-->APP: Receive Gateway information and active status

APP-->ZigBee Gateway: sends the activation instruction
APP-->Server: Use the token to poll the list of network activation devices every 2 seconds (the total duration is 100s by default)

Note over ZigBee Gateway: device receives the activation data

ZigBee Gateway->Service: activate the device
Service-->ZigBee Gateway: network configuration succeeds

Server-->APP: Network configuration succeeds
```

#### Discovery Device

Wiser SDK provides the function of discovering the wired devices. You should register the notification of the wired device to get device infomation. Before obtaining the device, the phone must be connected to the same network as the device.

```java
IWiserGwSearcher mWiserGwSearcher = WiserHomeSdk.getActivatorInstance().newTuyaGwActivator().newSearcher();
        mWiserGwSearcher.registerGwSearchListener(new IGwSearchListener() {
            @Override
            public void onDevFind(HgwBean hgwBean) {
                
            }
        });
```
**Parameters**

| Parameters         | Description |
| ------------ | -------------------------- |
| hgwBean         | gateway data entity discovered |

#### Initialize Parameters

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

| Parameters         | Description |
| ------------ | -------------------------- |
| token           | Activation key required for Configuration |
| timeout         | Configuration timeout, default setting is 100s, unit is second|
| context         | context |
| hgwBean         | the discovered gateway data entity |

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

| Parameters         | Description |
| ------------ | -------------------------- |
| token           | Activation key required for Configuration |
| timeout         | Configuration timeout, default setting is 100s, unit is second|
| context         | context |

**Get Network Configuration Token**

Before the Wi-Fi network configuration, the SDK needs to obtain the network configuration Token from the Wiser Cloud.
The term of validity of Token is 10 minutes, and the Token become invalid once the network configuration succeeds.
A new Token has to be obtained if you have to reconfigure network.

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

| Parameters         | Description |
| ------------ | -------------------------- |
| homeId          | Family ID, please refer to the family management section for details |

#### Configuration Method Invocation

```java
IWiserActivator mIWiserActivator = WiserHomeSdk.getActivatorInstance().newGwActivator(builder);
//开始配网
mIWiserActivator.start()
//停止配网
mIWiserActivator.stop()
//退出页面清理
mIWiserActivator.onDestroy()
```

### Sub-device Configuration

#### Description

The sub-device configuration network can only be initiated when the gateway device cloud is online, and the sub-device is in the network configuration state. The following uses the ZigBee gateway sub-device as an example to introduce the configuration network business process

```sequence
Title: Zigbee sub-device configuration

participant APP
participant SDK
participant Zigbee Gateway
participant Service

Note over Zigbee Gateway: Reset zigbee sub device
APP->SDK: sends the subdevice activation instruction
SDK->Zigbee Gateway: sends the activation instruction

Note over Zigbee Gateway: zigbee gateway receives the activation data

Zigbee Gateway->Service: activate the sub device
Service-->Zigbee Gateway: network configuration succeeds

Zigbee Gateway-->SDK: network configuration succeeds
SDK-->APP: network configuration succeeds

```

#### Initialize Parameters

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

| Parameters         | Description |
| ------------ | -------------------------- |
| mDevId           | Setting the gateway ID |
| timeout         | Setting the time-out period for network configuration |

#### Configuration Method Invocation

```java
IWiserActivator mWiserGWActivator = WiserHomeSdk.getActivatorInstance(). newGwSubDevActivator(builder);
// Start network configuration
mWiserGWActivator.start();
// Stop network configuration
mWiserGWActivator.stop();
// Destroy
mWiserGWActivator.onDestory();
```

### Bluetooth Configuration

For Bluetooth device configuration, you can refer to [the document BLE](./BLE.md).




