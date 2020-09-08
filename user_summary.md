# Retrieve a users account summary

If you want to retrieve summary information about a linked user, you can use the following endpoint

## Retrieve summary of user account

| Method           | URL                                                   | Environment                          
|------------------|-------------------------------------------------------|--------------|
| GET              | https://api.and-charge.com/v1/partners/{partnerId}/accounts/{userId} | Production
| GET              | https://api-pp.and-charge.com/v1/partners/{partnerId}/accounts/{userId} | Pre Production

### Request parameters are as follows:

| Attribute     | Request part  | Type                               | Cardinality | max. Length | Description 
|---------------|---------------|------------------------------------|-------------|-------------|---------------------------------------------------------------------------------------------------|
| Authorization |Request header | String                             |1            |100          | The accessToken authorizing you to do the request. The header value must be in form of: Bearer <accessToken>
| partnerId     |Path param     | String                             |1            |100          | Your partner ID with which you registered yourself as a partner
| userId        |Path param     | String                             |1            |100          | The user for which you request the summary

### Response payload is as follows:

| Attribute      | Type                               | Cardinality | max. Length | Description 
|----------------|------------------------------------|-------------|-------------|---------------------------------------------------------------------------------------------------|
| kmAvailable     |int                                 |1            | -/-         | The &Charge KM available to the user
| kmPending       |int                                 |1            | -/-         | The &Charge KM that are currently pending (e.g. open online shopping transactions)
| picturesPending |int                                 |1            | -/-         | TODO
| picturesAccepted|int                                 |1            | -/-         | TODO
| challengesSolved|int                                 |1            | -/-         | TODO
| role            |String                              |1            | -/-         | TODO

### Sample request & response

#### Request

   GET https://api.and-charge.com/v1/partners/PCS-001/accounts/pcsUserId001

   Request headers:
```
Accept: application/json
Content-Type: application/json
Authorization: Bearer <your JWT access token received during login>
```

#### Response

Response body:
```json
{
    "kmAvailable": 42,
    "kmPending": 0,
    "picturesPending": 0,
    "picturesAccepted": 0,
    "challengesSolved": 0,
    "role": "USER"
}
```
