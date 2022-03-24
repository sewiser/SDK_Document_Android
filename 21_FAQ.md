# FAQ
## Permission verification failed

 Please check the `appKey`, `appSecret`, `Security img`(t_s.bmp), any one of the mismatches will fail the verification. Please refer to [Preparation for integration](./3_Integrated.md) and [Integrate SDK](./3_Integrated.md) section.

## After upgrading the SDK, the following problems occur

```
java.lang.IllegalAccessError: Class okhttp3.EventListener extended by class com.wiser.smart.android.network.http.HttpEventListener is inaccessible (declaration of 'com.wiser.smart.android.network.http.HttpEventListener' ***)
```

Please upgrade the OkHttp version by using the following command.
	 
`implementation 'com.squareup.okhttp3: okhttp-urlconnection: 3.12.3'`

<!--
## Configuration Network FAQ

1. [Summary of Problems for Wi-Fi Configuration](Activator_wifi_faq.md)
-->