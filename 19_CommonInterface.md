#  Common interface

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

## Example

Take the following interface as an example:

| Interface Description | apiName         | version | postData |
| ----| ---- | ---- | ---- |
|Get a list of countries| wiser.m.country.list | 1.0 | - |

```java
Map<String, Object> postData = null;

WiserHomeSdk.getRequestInstance().requestWithApiNameWithoutSession("wiser.m.country.list", "1.0", postData, String.class, new IWiserDataCallback<String>() {
    @Override
    public void onSuccess(String result) {
        Log.i("TAG" , result);
    }

    @Override
    public void onError(String errorCode, String errorMessage) {
        Log.i("TAG" , errorCode);
    }
});
```

