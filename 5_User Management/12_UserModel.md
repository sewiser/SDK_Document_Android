# User Data Model

**User**

| Parameters | Description                              |
| ---- | ---- |
| nickName  | Nickname                                 |
| phoneCode | Country code                             |
| mobile | Mobile phone number                      |
| username  | User name                                |
| email  | Email                                    |
| uid    | Unique user identifier                   |
| sid    | Login generates the unique identification id |

| Parameters    | Description                                              |
| ---- | ---- |
| headPic       | Url of the User Account Picture                          |
| nickName      | Nickname                                                 |
| username      | User name<br>If the main account is a mobile phone number, username is the mobile phone number<br>If the primary account is a mailbox, username is the mailbox |
| mobile        | Phone number                                             |
| email         | email                                                    |
| phoneCode     | Country code<br/>For example:<br/>86: China<br/>1: United States |
| Domain.regionCode | The country area where the current account is located. AY: China, AZ: United States, EU: Europe |
| timezoneId    | User time zone information, for example: Asia/Shanghai   |
| tempUnit      | Temperature unit. 1: °C, 2: °F                           |
| snsNickname   | Nickname of the third-party account                      |
| regFrom       | Types of account registration<br/>0: email<br/>1: phone<br/>2: other<br/>3: qq<br/>4: weibo<br/>5: facebook<br/>6: twitter<br/>7: weixin<br>9: uid<br/>10: google |

