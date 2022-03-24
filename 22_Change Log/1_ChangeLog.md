# Change Log
This topic provides changelog and release notes for the App SDK for Android. The SDK is updated consistently, and Wiser claims all the rights of each version with **&copy;  2014 - 2021 Wiser Inc. All Rights Reserved** terms.

## V3.25.0

Release date: 2021.03.26

### New updates

- Registration Optimization
- Bluetooth Device connection optimization
- Dual-module Pairing Optimization 

## V3.24.0

Release date: 2021.02.05

### New updates

- Provided low-code generic panel for controlling smart devices.
- Supported fast switching to Bluetooth when dual-mode devices disconnect from Wi-Fi.

## V3.22.0

Release date: 2020.12.25

### New features

- Added the feature to link an email address.
- Enriched network error codes.
- Supported the infrared radio frequency devices.
- Added entries to the big data channel.

### Fixed issues

- Fixed a display issue when the shared device is switched to the home where the shared device is located.
- Fixed an issue where pairing failed after the maximum transmission unit (MTU) was changed in a Redmi M2004J7BC smartphone.
- Modified error code format and 205200 of the big data channel.
- Fixed the DP reporting and sending verification logic that was inaccurate in some cases.
- Fixed an issue where a crash occurred in case of the type error of Bluetooth mesh group control localId.
- Fixed an issue where a crash occurred in case of group control localId error.

## v3.20.0

Release date: 2020.11.11

### Highlights

- New guest user login mode
- Bug fixed

## v3.19.2

Release date: 2020.10.31

### Highlights

- `IWiserMessage` add method `deleteMessageWithType`
- Native bug fixed

## v3.19.0

Release date: 2020.10.15

### Highlights

- Upgrade to AndroidX
- New timing interface function
- The room supports changing custom pictures
- Added device DPs time for device attributes, which can record the time corresponding to the nearest change of DP.
- Internal optimization and bugfix

## v3.17.13

Release date: 2020.10.31

### Highlights

- `IWiserMessage` add method `deleteMessageWithType`
- Native bug fixed

## v3.17.10

Release date: 2020.10.05

### Highlights

- Certificate update abnormal problem fix
- Other improvements and bug fix

## v3.17.9

Release date: 2020.09.10

### Highlights

- Add standard product information interface
- Other improvements and bug fix

## v3.17.8

Release date: 2020.08.19

### Highlights

- Fix some NPE
- Other improvements and bug fix

## v3.17.6

Release date: 2020.07.18

### Highlights

- Support Dual-mode Device
- Add scene information change synchronization interface
- Add the function of synchronizing user information
- Add shortcut control SDK
- Add scan code login function
- Added the function of deleting certain types of messages in batches
- Added check for new messages
- Added function to get family weather
- Repair ZigBee sub-device distribution network HTTPS compensation scheme
- Other improvements and bug fix

## v3.17.0

Release date: 2020.06.08

### Highlights

- Firmware upgrade status prompt
- Mesh support fast active
- Support Wi-Fi sub-device group
- Other improvements and bug fix

## v3.15.2

Release date: 2020.05.13

### Highlights

- Fix socket create a bug

## v3.15.0

Release date: 2020.05.06

### Highlights

- Internal optimization and bugfix

## v3.14.5

Release date: 2020.04.10

### Highlights

- Update the dependency of the MQTT library
- Improve the stability of communication within the LAN
- Data encryption for network request and response
- Internal optimization and bugfix

## v3.13.0

Release date: 2020.01.08

### Highlights

- Bugs fixed
- Support BLE devices
- Support BLE+WIFI Dual-mode devices

## v3.12.4

Release date: 2019.11.09

### Highlights

- Recommended upgrade
- Bug fixed

## v3.12.1

Release date: 2019.09.29

### Highlights

- Support sub-device OTA
- AP Distribution Network Optimization
- Timing support annotation and push function
- Support SigMesh Devices
- RegisterDevice
- RegisterDevice deprecated the "gcm" parameter. Use "fcm"
- Bug fixed

## v3.11.2

Release date: 2019.08.13

### Highlights

- Change the integration of the so library, SDK provides the so library of armeabi-v7a, arm64-v8a, armeabi developers use as needed
- Added Bluetooth mesh function
- New message center features
- Bugs fixed

## v3.9.6

Release date: 2019.05.17

### Interface changed

- The attribute of Device 、ProductBean int becomes long
- Message Center List Gets Increased Pagination and Type Acquisition

### Bugfix

- Repair model ZigBee gateway distribution network problem
- After repairing some Huawei mobile phone upgrade systems, the AP distribution network will choose 4g NIC to issue the package problem.
- Fix unsuccessful creation of timing type
- Fixed sub-device data synchronization problem under gateway LAN
- Local cache (device list) is not updated after repairing the distribution network
- Fix multi-threaded command control issues
- Fix 433 gateway LAN connection problem

## v3.0.0

### Highlights

- Encryption upgrade: Appkey, AppSecret, and security images

## v2.9.+

### Highlights

- LAN stability upgrade, remove Netty dependency
- Remove Rxjava
- Sweeper flow channel is open

## v2.7.+

### Highlights

- Support infrared equipment
- SDK component upgrade
- Support Bluetooth mesh

## v2.4.+

### Highlights

- The device is based on the family dimension SDK. Unlike the 1 series, the user account needs to create a family to control the device. The 1 series account needs to be upgraded before it can be used.

- Added ZigBee distribution network, control

## v1.+.+

### Highlights

- The device is based on the user dimension
- Only WiFi devices are supported

## Beta version

### v3.20.0-beta1

Release date: 2020.10.31

- New guest user login mode
- Bugs fixed

### v3.17.6-beta2

Release date: 2020.06.24

### v3.17.6-beta1

Release date: 2020.06.12

### v3.17.0-beta1

Release date: 2020.05.06

### v3.15.0-beta3

Release date: 2020.04.28

### v3.15.0-beta2

Release date: 2020.04.22

### v3.15.0-beta1

Release date: 2020.04.11

### v3.14.5-beta2

Release date: 2020.02.28

### v3.14.5-beta1

Release date: 2020.01.13

### v3.13.0-beta4

Release date: 2019.12.20