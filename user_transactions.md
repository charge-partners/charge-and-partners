# Retrieve a users transactions

If you want to retrieve the transactions a user has done, you can use the following endpoint

## Retrieve transaction list of user

| Method           | URL                                                   | Environment                          
|------------------|-------------------------------------------------------|--------------|
| GET              | https://api.and-charge.com/public/v1/partners/{partnerId}/accounts/{userId}/transactions | Production
| GET              | https://api-pp.and-charge.com/public/v1/partners/{partnerId}/accounts/{userId}/transactions | Pre Production

### Request parameters are as follows:

| Attribute     | Request part  | Type                               | Cardinality | max. Length | Description 
|---------------|---------------|------------------------------------|-------------|-------------|---------------------------------------------------------------------------------------------------|
| Authorization |Request header | String                             |1            |100          | The accessToken authorizing you to do the request. The header value must be in form of: Bearer <accessToken>
| partnerId     |Path param     | String                             |1            |100          | Your partner ID with which you registered yourself as a partner
| userId        |Path param     | String                             |1            |100          | The user for which you request the summary
| page          |Query param    | Integer                            |?            |-/-          | The number of the page that shall be retrieved; default: 0
| limit         |Query param    | Integer                            |?            |-/-          | The number of transactions that shall be retrieved; default: 20

### Response payload is as follows:

| Attribute      | Type                                     | Cardinality | max. Length | Description 
|----------------|------------------------------------------|-------------|-------------|---------------------------------------------------------------------------------------------------|
| -/-            |[Transaction](types.md#transaction-class) |*            | -/-         | A list of transactions

### Sample request & response

#### Request

   GET https://api.and-charge.com/public/v1/partners/PCS-001/accounts/pcsUserId001/transactions

   Request headers:
```
Accept: application/json
Content-Type: application/json
Authorization: Bearer <your JWT access token received during login>
```

#### Response

Response body:
```json
[{"transactionId":"5322","partner":"","kilometer":20,"status":"CONFIRMED","created":"2019-04-23T06:08:52.045+0000","type":"ACCOUNT_REGISTRATION","address":null}]
```
