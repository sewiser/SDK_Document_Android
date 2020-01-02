### 3.13.0-beta4
- Support BLE Devices
- Support BLE+WIFI Dual-mode Devices

### 3.12.4

bugfix

### 3.12.1

- Support sub device OTA
- AP Distribution Network Optimization
- Timing support annotation and push function
- Support SigMesh Devices
- registerDevice 
- registerDevice deprecated the "gcm" parameter. Use "fcm"
- bug fixed

###  3.11.2

- Change the integration of the so library, sdk provides the so library of armeabi-v7a, arm64-v8a, armeabi developers use as needed
- Added Bluetooth mesh function
- New message center features
- bugfix

### 3.9.6

Interface change

* the attribute  of Device 、ProductBean int becomes long
* Message Center List Gets Increased Pagination and Type Acquisition


Bug Fix

* Repair model ZigBee gateway distribution network problem
* After repairing some Huawei mobile phone upgrade systems, the AP distribution network will choose 4g NIC to issue the package problem.
* Fix unsuccessful creation of timing type
* Fixed sub-device data synchronization problem under gateway LAN
* Local cache (device list) is not updated after repairing the distribution network
* Fix multi-threaded command control issues
* Fix 433 gateway LAN connection problem



### 3.0.0
* Encryption upgrade: Appkey, AppSecret and security images

### 2.9.+
* LAN stability upgrade, remove Netty dependency
* Remove Rxjava
* Sweeper flow channel is open

### 2.7.+
* Support infrared equipment
* SDK component upgrade
* Support Bluetooth mesh

### 2.4.+
* The device is based on the family dimension SDK. Unlike the 1 series, the user account needs to create a family to control the device. The 1 series account needs to be upgraded before it can be used.
* Added ZigBee distribution network, control

### 1.+.+

* The device is based on the user dimension
* Only WiFi devices are supported
