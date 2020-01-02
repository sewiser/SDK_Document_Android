##  Common interface

The server api calls the common function interface in the interface` IWiserSmartRequest`

There are the following interfaces available for calling

```java
  /**
 * Applicable to api interface request with session
 * @param apiName: api name
 * @param version: api version
 * @param postData: Post sent data
 * @param object: Data object returned by the server
 * @param callback: callback
 * @param <T>
 */
<T> void requestWithApiName(String apiName, String version, Map<String, Object> postData, Class<T> object, final IWiserDataCallback<T> callback);

/**
 * Applies to api interface requests without session
 * @param apiName: api name
 * @param version: api version
 * @param postData: Post sent data
 * @param object: Data object returned by the server
 * @param callback: callback
 * @param <T>
 */
<T> void requestWithApiNameWithoutSession(String apiName, String version, Map<String, Object> postData, Class<T> object, final IWiserDataCallback<T> callback);

```

The calling method is as follows:`WiserHomeSdk.getRequestInstance()`

