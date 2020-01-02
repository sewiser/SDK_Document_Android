## Using Platform of a Third Party for Login

## Login on Twitter

**[Method Invocation]**

```java
/**
* @param countryCode Country code
* @param token       token that authorizes login on twitter.
* @param secret      secret that authorizes login on twitter.
*/

WiserHomeSdk.getUserInstance().loginByTwitter(String countryCode, String token, String secret, ILoginCallback callback);
```

## Login on QQ

**[Method Invocation]**
```java
/**
* @param countryCode Country code
* @param userId         The userId that authorizes login on QQ.
* @param accessToken    The accessToken that authorizes login on QQ. 
*/
WiserHomeSdk.getUserInstance().loginByQQ(String countryCode, String userId, String accessToken, ILoginCallback callback);
```
## Login on Wechat

**[Method Invocation]**
```java
/**
 * @param countryCode Country code
 *  @param code The code that authorizes login on Wechat. 
*/
WiserHomeSdk.getUserInstance().loginByWechat(String countryCode, String code, ILoginCallback callback);
```
## Login on Facebook
```java
/**
 * @param countryCode Country code
 *  @param token The Token that authorizes login on Facebook.
*/

WiserHomeSdk.getUserInstance().loginByFacebook(String countryCode, String token, ILoginCallback callback);
```
