### Summary of Problems for Wi-Fi Configuration

**1. Timeout in network configuration. The device cannot be connected to the network. The causes may be:**

- The obtained Wi-Fi Ssid is incorrect. The ssid obtained in the Android system usually has “” in the front or back of it.  It is recommended to use the WiFiUtil.getCurrentSSID() in the Wiser Sdk to obtain the Wi-Fi Ssid. 
- The Wi-Fi password has space. User may accidentally enter the space because of the predictive typing function. It is recommended that users enable the displaying password option when entering password. Or prop-up windows shall be displayed if the password entered includes spaces. 
- Users have not entered the Wi-Fi password. User may forget to enter the password when they use the smart device for the first time. It is recommended that prop-up windows be displayed if no password is entered and the Wi-Fi encryption type is not set to NONE.
- Users select the hotspot name of device in the AP mode network configuration. This problem is prevalent when users use the smart device for the first time. It is recommended that prop-up windows be displayed if users selected the hotspot name of devices in the AP mode network configuration. 
- The Ssid of the obtained Wi-Fi is “0x” and <unknown ssid>. Currently, this problem may occur in Chinese mobile phones, and this problem is not caused by Wi-Fi but the permission to locate. It is recommended that user enter the Ssid of Wi-Fi manually or the prop-up windows be displayed to ask users to authorize permissions.

**2. Timeout in network configuration, but the device has been successfully activated. The possible cause is:**

- The App is not using a normal network, and the status of device cannot be obtained. 

