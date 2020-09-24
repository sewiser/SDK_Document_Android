## Using Platform of a Third Party for Login

The third-party login needs to configure the corresponding third-party configuration information on the wiser iot platform, otherwise, calling the following interface will fail.

![image-20200608154257066](images/user_third_config.png)

![image-20200608154314932](images/user_third.png)



## Login on Facebook

**Declaration**

```java
WiserHomeSdk.getUserInstance().loginByFacebook(String phoneCode, String token, ILoginCallback callback);
```

**Parameters**

|  Parameters        | Description                        |
| ----------- | --------------------------- |
| phoneCode | phone code,such as：86           |
| token       |The Token that authorizes login on Facebook. |
