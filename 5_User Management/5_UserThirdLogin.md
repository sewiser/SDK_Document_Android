# Using Platform of a Third Party for Login

The third-party login needs to configure the corresponding third-party configuration information on the wiser iot platform, otherwise, calling the following interface will fail.

![third-party-login](./img/f21febcb-f631-4ff8-926b-72e02c744679.png)

## Login on Facebook

**Declaration**

```java
WiserHomeSdk.getUserInstance().loginByFacebook(String phoneCode, String token, ILoginCallback callback);
```

**Parameters**

|  Parameters    | Description                    |
| ---- | ---- |
| phoneCode | phone code,such as：86       |
| token   |The Token that authorizes login on Facebook. |
