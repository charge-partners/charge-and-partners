# Get pictures by location

Retrieve pictures of one charging location. The location is identified by the locationId you send us with the [update location mappings](update_location_mappings.md) API.

## Get pictures by location

| Method           | URL                                                   | Environment                          
|------------------|-------------------------------------------------------|--------------|
| GET              | https://api.charge-and.com/public/v1/partners/{partnerId}/locations/{locationId} | Production
| GET              | https://api-pp.charge-and.com/public/v1/partners/{partnerId}/locations/{locationId} | Pre Production

### Request parameters are as follows:

| Attribute     | Request part  | Type   | Cardinality | max. Length | Description 
|---------------|---------------|--------|-------------|-------------|---------------------------------------------------------------------------------------------------|
| Authorization |Request header | String |1            |100          | The accessToken authorizing you to do the request. The header value must be in form of: Bearer <accessToken>
| partnerId     |Path param     | String |1            |100          | Your partner ID with which you registered yourself as a partner
| locationId    |Path param     | String |1            |100          | Your location ID

### Response payload:

| Attribute     | Type                                      | Cardinality | max. Length | Description 
|---------------|-------------------------------------------|-------------|-------------|---------------------------------------------------------------------------------------------------|
| locationId    | String                                    | 1           |100          | The location ID for which you requested data
| pictures      | [PictureLink](types.md#picturelink-class) | *           |-/-          | A list of pictures available for this location

### Sample request

#### Request

   GET https://api.charge-and.com/public/v1/partners/PCS-001/locations/4553

   Request headers:
```
Accept: application/json
Content-Type: application/json
Authorization: Bearer <your JWT access token received during partner registration>
```


### Sample response
```json
{
	"locationId": "4553",
	"pictures": [{
			"uri": "https://pictures.charge-and.com/img/o758HZt8fl6hJy0K2CNGX836xJehDgaT.jpg",
			"thumbnailUri": "https://pictures.charge-and.com/thumb/o758HZt8fl6hJy0K2CNGX836xJehDgaT.jpg",
			"perspective": "LOCATION_SURROUNDINGS"
		}, {
			"uri": "https://pictures.charge-and.com/img/fkDngJU0r34BN20F7ymJ4Kx27BQ2B7Gq.jpg",
			"thumbnailUri": "https://pictures.charge-and.com/thumb/fkDngJU0r34BN20F7ymJ4Kx27BQ2B7Gq.jpg",
			"perspective": "CHARGING_STATION"
		}, {
			"uri": "https://pictures.charge-and.com/img/UQ7FiyjZrGWNfzol3T6L2ZaQtPElKoKw.jpg",
			"thumbnailUri": "https://pictures.charge-and.com/thumb/UQ7FiyjZrGWNfzol3T6L2ZaQtPElKoKw.jpg",
			"perspective": "LOCATION_FULL"
		}, {
			"uri": "https://pictures.charge-and.com/img/9zD0vmluH2oa1y0uiFTIBUjkqM0Synqt.jpg",
			"thumbnailUri": "https://pictures.charge-and.com/thumb/9zD0vmluH2oa1y0uiFTIBUjkqM0Synqt.jpg",
			"perspective": "LOCATION_ENTRANCE"
		}
	]
}
```