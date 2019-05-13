# Charge&Pay

Pay for a users charging session with Charge& kilometers.
Send us a users CDR, and the amount of kilometers you expect the user to pay for this CDR and we will check with the users account balance and do the transaction.

To use this service, you can use the following endpoint

## Create transaction

| Method           | URL                                                   | Environment                          
|------------------|-------------------------------------------------------|--------------|
| POST              | https://api.charge-and.com/v1/partners/{partnerId}/accounts/{userId}/transactions | Production
| POST              | https://api-pp.charge-and.com/v1/partners/{partnerId}/accounts/{userId}/transactions | Pre Production

### Request parameters are as follows:

| Attribute     | Request part  | Type                               | Cardinality | max. Length | Description 
|---------------|---------------|------------------------------------|-------------|-------------|---------------------------------------------------------------------------------------------------|
| Authorization |Request header | String                             |1            |100          | The accessToken authorizing you to do the request. The header value must be in form of: Bearer <accessToken>
| partnerId     |Path param     | String                             |1            |100          | Your partner ID with which you registered yourself as a partner
| userId        |Path param     | String                             |1            |100          | The user for which you want to create the transaction
| request       |Request body   | [TransactionRequest](types.md#transactionrequest-class) |1            |-/-          | The transaction request

### Response payload is as follows:

| Attribute      | Type                                     | Cardinality | max. Length | Description 
|----------------|------------------------------------------|-------------|-------------|---------------------------------------------------------------------------------------------------|
| -/-            |[Transaction](types.md#transaction-class) |1            | -/-         | The newly created transaction

### Sample request & response

#### Request

   POST https://api.charge-and.com/v1/partners/PCS-001/accounts/pcsUserId001/transactions

   Request headers:
```
Accept: application/json
Content-Type: application/json
Authorization: Bearer <your JWT access token received during partner registration>
```

   POST data:
```json
{
	"transactionId": "348328463873",
	"transactionReference": "partner-20190423-0011",
	"service": "PAY_FOR_CHARGING_SESSION",
	"kilometer": 38,
	"serviceSpecificData": {
		"EVSE_ID": "DE*911E12345",
		"CONSUMED_ENERGY_KWH": "12.234",
		"SESSION_START": "2019-02-28T12:12:12.123Z",
		"SESSION_END": "2019-02-28T15:48:12.888Z",
		"GEO_POSITION_USER": "20.12366,21.23425",
		"GEO_POSITION_CHARGEPOINT": "20.12345,21.23445",
		"COUNTRY": "DE",
		"CITY": "Eschborn",
		"STREET": "Kölner Straße",
		"HOUSE_NUMBER": ""
	}
}

```


#### Response

Response body:
```json
{"transactionId":"348328463872","partner":"MSP Partner","kilometer":-38,"status":"CONFIRMED","created":"2019-04-23T08:07:48.788+0000","type":"PAY_FOR_CHARGING_SESSION","address":"Kölner Straße, Eschborn"}
```
