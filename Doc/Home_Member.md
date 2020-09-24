## Home Member Management Class

The IWiserHomeMember provides the family member management interfaces including adding member, removing member, update the control permission of member and obtaining home member list ,etc. The invocation method is `WiserHomeSdk.getMemberInstance()`.  

## MemberBean Field Information
| Field | Type | Describe |
| --- | --- | --- |
| homeId | long  | Unique id of Home |
| nickName | String |The member nickName  |
| admin | boolean | Administrator or not |
| memberId | long | Member id |
| headPic | String | Directory of account picture|
| account | String  | AccountName of member |
| uid | String | Unique id of member |
| memberStatus | int| The member status （1:to be accepted 2:accepted 3:reject）|

## Add Members in a Home
```java
/**
* Add members in home
*
* @param countryCode Country code
* @param userAccount User name
* @param name     Nickname
* @param admin       Have the administrator permission or not.
* @param callback
*/
void addMember(long homeId ,int countryCode, String userAccount, String name, boolean admin, IWiserMemberResultCallback callback);
```
## Remove Member of a Home
```java
/**
* Remove member of a home
*
* @param id
* @param callback
*/
void removeMember(long memberId, IResultCallback callback);
```
## Change Name and Permission of Members
```java
/**Change name and permission of members
* @param memberId of member. 
* @param name of member. 
* @param admin administrator or not.
* @param callback
*/

void updateMember(long memberId,String name, boolean admin, IResultCallback callback);
```
## Query the Member List of a Home
```java
/**
* Query the member list of a home
*
* @param callback
*/
void queryMemberList(long homeId,IWiserGetMemberListCallback callback);
```

## To accept or reject family invitation

```java
 /**
 * To accept or reject family invitation
 * @param homeId    
 * @param action    true:accept,false:reject
 * @param callBack
*/
void processInvitation(long homeId, boolean action, final IResultCallback callBack);
```
