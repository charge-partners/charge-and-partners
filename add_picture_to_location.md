# Add picture to location

Submits a picture for a charging location. The location is identified by the locationId you send us with the [update location mappings](update_location_mappings.md) API. The userId is the user ID you were using on linking your account with Charge&.
After the picture is submitted, it will be reviewed and eventually either published or rejected. In case the picture is being published and the picture was needed at the location, the user will receive a reward from Charge&

## Add picture to location

| Method           | URL                                                   | Environment                          
|------------------|-------------------------------------------------------|--------------|
| POST              | https://api.charge-and.com/public/v1/partners/{partnerId}/locations/{locationId}/pictures?userId={userId} | Production
| POST              | https://api-pp.charge-and.com/public/v1/partners/{partnerId}/locations/{locationId}/pictures?userId={userId} | Pre Production

### Request parameters are as follows:

| Attribute     | Request part  | Type   | Cardinality | max. Length | Description 
|---------------|---------------|--------|-------------|-------------|---------------------------------------------------------------------------------------------------|
| Authorization |Request header | String |1            |100          | The accessToken authorizing you to do the request. The header value must be in form of: Bearer <accessToken>
| partnerId     |Path param     | String |1            |100          | Your partner ID with which you registered yourself as a partner
| locationId    |Path param     | String |1            |100          | Your location ID
| userId        |Query param    | String |?            |100          | The user ID of the user posting the picture. Is optional. If not sent, this picture is originating from the partner (or a backend system of the partner). No user will be rewarded in this case.
| body          |Request body   | [AddPicture](types.md#addpicture-class) |1            |-/-          | The request body containing the picture and meta data

### Response payload:

The request does not deliver any data as a response. Verify the http status to ensure the request was successful, everything in the range of HTTP status 2XX indicates a successful operation.

### Sample request

#### Request

   POST https://api.charge-and.com/public/v1/partners/PCS-001/locations/4553/pictures?userId=pcsUserId001

   Request headers:
```
Accept: application/json
Content-Type: application/json
Authorization: Bearer <your JWT access token received during partner registration>
```

   POST body:
```json
{
	"latitude": "50.435276",
	"longitude": "8.684159",
	"imageData": "<base 64 encoded picture data>",
	"perspective": "CHARGING_STATION"
}
```
