# Charge&Carbon offset

Make your charging session is CO2 neutral. 
Send us a users CDR. We will take the delivered amount of energy (or estimate the amount of energy charged) and make that session CO2 neutral by offsetting the carbon footprint incurred by this session.
We take the country and, if possible, the CPO into consideration.

To use this service, you can use the following endpoint

## Create transaction

| Method           | URL                                                                                   | Environment                          
|------------------|---------------------------------------------------------------------------------------|--------------|
| POST              | https://api.and-charge.com/v1/partners/{partnerId}/accounts/{userId}/transactions    | Production
| POST              | https://api-pp.and-charge.com/v1/partners/{partnerId}/accounts/{userId}/transactions | Pre Production

### Carbon offset charging sessions directly

If you do not want your users to pay for carbon offsetting charging sessions, you can cover the costs of offsetting those sessions directly. 
We will include those transactions in your billing and reports. For this use case you can use the following endpoint. Payload and error handling are identical:

| Method           | URL                                                                 | Environment                          
|------------------|---------------------------------------------------------------------|--------------|
| POST              | https://api.and-charge.com/v1/partners/{partnerId}/transactions    | Production
| POST              | https://api-pp.and-charge.com/v1/partners/{partnerId}/transactions | Pre Production


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

   POST https://api.and-charge.com/v1/partners/PCS-001/accounts/pcsUserId001/transactions

   Request headers:
```
Accept: application/json
Content-Type: application/json
Authorization: Bearer <your JWT access token received during login>
```

   POST data:
```json
{
	"transactionId": "348324563873",
	"transactionReference": "partner-20190423-0011",
	"service": "CO2_OFFSET_CHARGING_SESSION",
	"serviceSpecificData": {
		"EVSE_ID": "DE*911E12345",
		"CPO_ID": "DE*911",
		"MAX_CHARGING_POWER": "22",
		"CONSUMED_ENERGY_KWH": "",
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
{"transactionId":"348324563873","partner":"MSP Partner","kilometer":-3,"status":"CONFIRMED","created":"2019-04-23T08:07:48.788+0000","type":"CO2_OFFSET_CHARGING_SESSION","address":"Kölner Straße, Eschborn"}
```
