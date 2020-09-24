# Error Code

| Error code | Description                                              |
| ---------- | -------------------------------------------------------- |
| 101        | Network anomaly                                          |
| 102        | json escape failed                                       |
| 103        | Network anomaly, unable to access to network             |
| 104        | Wrong cellphone clock, HTTPS certificate expired         |
| 105        | Login information which requires session                 |
| 106        | Wrong synchronize io                                     |
| 1001       | Network of configuration wrong                           |
| 1002       | The network binding gateway failed                       |
| 1004       | Network access token failed                              |
| 1005       | The online status of the network detection device failed |
| 1006       | Network configuration failed                             |
| 1007       | List of failed configuration devices                     |
| 1100       | The phone number is incorrect                            |
| 1101       | The verification code is incorrect                       |
| 1102       | Upgrade error                                            |
| 10201      | The device LAN is not online                             |
| 10202      | The device is not online in the cloud                    |
| 10203      | Device out of line                                       |
| 11001      | The command was sent in the wrong format                 |
| 11002      | Device is removed                                        |
| 11004      | Wrong signature                                          |
| 11005      | Fail to issue                                            |
| 11009      | The issued data is empty                                 |
| 12001      | Data parsing failed                                      |
| 12002      | Inconsistent signature                                   |
| 12003      | Data expired                                             |
| 12004      | The protocol number does not exist                       |

## Network error codes

| Error Code | Error Information | Error Cause Analysis |
| ------ | ----------------------------------- | ----------------------------------- |
| 50500 | Other errors | Unknown error |
| 50502 | javax.net.ssl.sslhandshakeexception | (1) The time of the client's mobile phone is inaccurate and the certificate is beyond the valid range. This problem will occur. <br> (2) The client's mobile phone network has certificate verification turned on. All applications cannot access the Internet <br> (3) There is a problem with the load balancing of cloud certificates, which will cause some users' phones to be inoperable.<br>  (4) Cloud certificates will expire, and 50502 problems will occur in large areas. <br> (5) The client's mobile phone does not have our certificate. The CA's root certificate  <br>(6) There is a problem with the intermediate certificate configured on the server certificate chain |
| 50501 | The network is unavailable | The system recognizes that the network is unavailable, the WiFi or mobile phone network is not turned on |
| 50408 | timeout | Network Request Timeout |
| 50504 | unable to resolve host |
| 50503 | read timed out | Network request read timeout |
| 50505 | failed to connect to .. |
| 50506 | no route to host | |
| 50507 | connect timed out | |
| 50508 | ssl handshake timed out | |
| 50509 | connection closed by peer | Request rejected by the cloud |
| 50510 | stream was reset: protocol_error | |
| 50511 | canceled | Network request has been canceled (canceled locally by APP) |
| 50512 | 502 | Invalid Gateway Cloud Issue |
| 50513 | 503 | A server-side error status code for the HTTP protocol, which indicates that the server is not yet ready to accept requests |
| 50514 | json error | JSON parsing error |
| 50515 | Hostname ... not verified ||
| 50516 | certificate pinning failure ||
