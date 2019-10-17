# API Endpoint - accounts

If you want to link your users with &Charge users, a set of APIs is available to you.

## Setting up an account link

| Method           | URL                                                   | Environment                          
|------------------|-------------------------------------------------------|--------------|
| POST             | https://api.and-charge.com/v1/partners/{partnerId}/accounts?userId={userId} | Production
| POST             | https://api-pp.and-charge.com/v1/partners/{partnerId}/accounts?userId={userId} | Pre Production

### Request parameters are as follows:

| Attribute     | Request part  | Type                               | Cardinality | max. Length | Description 
|---------------|---------------|------------------------------------|-------------|-------------|---------------------------------------------------------------------------------------------------|
| Authorization |Request header | String                             |1            |100          | The accessToken authorizing you to do the request. The header value must be in form of: Bearer <accessToken>
| partnerId     |Path param     | String                             |1            |100          | Your partner ID with which you registered yourself as a partner
| userId        |Query param    | String                             |1            |100          | The user for which you request the account link

### Response payload is as follows:

| Attribute      | Type                               | Cardinality | max. Length | Description 
|----------------|------------------------------------|-------------|-------------|---------------------------------------------------------------------------------------------------|
| status         |String                              |1            | -/-         | An enumeration reporting on the status of the operation. Possible values are: INITIAL, LINKED
| activationCode |String                              |1            |100          | The activation code that needs to be passed to the &Charge webpage or iOS app to complete the link
| userId         |String                              |1            |100          | The user ID for which you requested the account link

### Sample request & response

#### Request

   POST https://api.and-charge.com/v1/partners/PCS-001/accounts?userId=pcsUserId001

   Request headers:
```
Accept: application/json
Content-Type: application/json
Authorization: Bearer <your JWT access token received during login>
```

#### Response

Response body:
```json
{"status":"INITIAL","activationCode":"yx3Uwa233GO0MD/u2XlTLayaeHh6j3LpHFkx9lRmI/M=","userId":"newLink1"}
```


## Removing an account link

| Method           | URL                                                   | Environment                          
|------------------|-------------------------------------------------------|--------------|
| DELETE           | https://api.and-charge.com/v1/partners/{partnerId}/accounts?userId={userId} | Production
| DELETE           | https://api-pp.and-charge.com/v1/partners/{partnerId}/accounts?userId={userId} | Pre Production

### Request parameters are as follows:

| Attribute     | Request part  | Type                               | Cardinality | max. Length | Description 
|---------------|---------------|------------------------------------|-------------|-------------|---------------------------------------------------------------------------------------------------|
| Authorization |Request header | String                             |1            |100          | The accessToken authorizing you to do the request. The header value must be in form of: Bearer <accessToken>
| partnerId     |Path param     | String                             |1            |100          | Your partner ID with which you registered yourself as a partner
| userId        |Query param    | String                             |1            |100          | The user for which you want to remove account links

### Response payload
The request does not offer a response load as such. Success or failure of the request can be determined by the HTTP status code of the response.

### Sample request

   DELETE https://api.and-charge.com/v1/partners/PCS-001/accounts?userId=pcsUserId001

   Request headers:
```
Accept: application/json
Content-Type: application/json
Authorization: Bearer <your JWT access token received during login>
```
