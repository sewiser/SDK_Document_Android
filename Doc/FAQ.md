# FAQ

**1. Permission Verification Failed**
 Please check the `appKey`、`appSecret`、`Security img`(t_s.bmp), any one of the mismatches will fail the verification. Please refer to [Preparation for integration](https://tuyainc.github.io/tuyasmart_home_android_sdk_doc/en/resource/Preparation.html) and [Integrate SDK](https://tuyainc.github.io/tuyasmart_home_android_sdk_doc/en/resource/Integrated.html) section.

**2. After upgrading the SDK, the following problems occur**

	     java.lang.IllegalAccessError: Class okhttp3.EventListener extended by class com.wiser.smart.android.network.http.HttpEventListener is inaccessible (declaration of 'com.wiser.smart.android.network.http.HttpEventListener' ***)
	
	Please upgrade the okhttp version 
	
	```groovy
	implementation 'com.squareup.okhttp3: okhttp-urlconnection: 3.12.3'
	```


## Configuration Network FAQ

1. [Summary of Problems for Wi-Fi Configuration](Activator_wifi_faq.md)

