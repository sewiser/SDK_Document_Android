## Release Version

## Beta Version

### 3.19.0-beta2(2020.09.21)

* Upgrade to AndroidX
* New timing interface function
* The room supports changing custom pictures
* Added device dps time for device attributes, which can record the time corresponding to the nearest change of dp
* Internal optimization and bugfix

[3.19.0 Upgrade Guide](./Update_3_19_0.md)

### 3.17.8 (2020.0819)

* Fix some NPE
* Other improvements and bug fix

### 3.17.6 (2020.07.18)

* Support Dual-mode Device
* Add scene information change synchronization interface
* Add the function of synchronizing user information
* Add shortcut control SDK
* Add scan code login function

* Added the function of deleting certain types of messages in batches
* Added check for new messages
* Added function to get family weather
* Repair ZigBee sub-device distribution network https compensation scheme

* Other improvements and bug fix

### 3.17.0 (2020.06.08)

- Smart scene support for geofence condition trigger
- Firmware upgrade status prompt
- Mesh support fast active
- Support Wi-Fi sub-device group
- Other improvements and bug fix

### 3.15.2 (2020.05.13)

* fix socket create bug

### 3.15.0 (2020.05.06)

* Internal optimization and bugfix

### 3.14.5 (2020.04.10)

[Upgrade guide before 3.13.0 to version after 3.14.x](./Update_3_14_0.md)

* Update the dependency of mqtt library
* Improve the stability of communication within the LAN
* Data encryption for network request response
* Internal optimization and bugfix

### 3.13.0(2020.01.08)

* bugfix

- Support BLE Devices
- Support BLE+WIFI Dual-mode Devices

### 3.12.4 (2019.11.09)

* bugfix

* Recommended upgrade

### 3.12.1 (2019.09.29)

- Support sub device OTA
- AP Distribution Network Optimization
- Timing support annotation and push function
- Support SigMesh Devices
- registerDevice 
- registerDevice deprecated the "gcm" parameter. Use "fcm"
- bug fixed

###  3.11.2 (2019.08.13)

- Change the integration of the so library, sdk provides the so library of armeabi-v7a, arm64-v8a, armeabi developers use as needed
- Added Bluetooth mesh function
- New message center features
- bugfix

### 3.9.6 (2019.05.17)

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



## History Beta Versions

### 3.17.6-beta2 (2020.06.24)

### 3.17.6-beta1 (2020.06.12)

### 3.17.0-beta1 (2020.05.06)

### 3.15.0-beta3 (2020.04.28)

### 3.15.0-beta2 (2020.04.22)

### 3.15.0-beta1 (2020.04.11)

### 3.14.5-beta2 (2020.02.28）

### 3.14.5-beta1 (2020.01.13）

### 3.13.0-beta4 (2019.12.20)
