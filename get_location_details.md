# Get location details

Retrieves detail information of a list of charging locations. This is meant as a service to support partner side caching. Update your cache by using this paged API. Retrieve a list of pictures of your locations on a daily basis.

## Get location details

| Method           | URL                                                   | Environment                          
|------------------|-------------------------------------------------------|--------------|
| GET              | https://api.and-charge.com/v1/partners/{partnerId}/locations | Production
| GET              | https://api-pp.and-charge.com/v1/partners/{partnerId}/locations | Pre Production

### Request parameters are as follows:

| Attribute     | Request part  | Type    | Cardinality | max. Length | Description 
|---------------|---------------|---------|-------------|-------------|---------------------------------------------------------------------------------------------------|
| Authorization |Request header | String  |1            |100          | The accessToken authorizing you to do the request. The header value must be in form of: Bearer <accessToken>
| partnerId     |Path param     | String  |1            |100          | Your partner ID with which you registered yourself as a partner
| page          |Query param    | Integer |?            |-/-          | The page you want to retrieve; default 0
| limit         |Query param    | Integer |?            |-/-          | The amount of location details you want to retrieve per page; default 20

### Response payload:

| Attribute     | Type                                              | Cardinality | max. Length | Description 
|---------------|---------------------------------------------------|-------------|-------------|---------------------------------------------------------------------------------------------------|
| -/-           | [LocationDetails](types.md#locationdetails-class) | *           | -/-         | A list of location details

### Sample request

#### Request

   GET https://api.and-charge.com/v1/partners/PCS-001/locations?page=1&limit=4

   Request headers:
```
Accept: application/json
Content-Type: application/json
Authorization: Bearer <your JWT access token received during login>
```


### Sample response
```json
[
    {
		"locationId": "602",
		"pictures": []
	}, {
		"locationId": "603",
		"pictures": []
	}, {
		"locationId": "604",
		"pictures": []
	}, {
		"locationId": "605",
		"pictures": [{
				"uri": "https://pictures.and-charge.com/img/x6NOEAjbh7JPH5d2nDagDoRMsdHEuKze.jpg",
				"thumbnailUri": "https://pictures.and-charge.com/thumb/x6NOEAjbh7JPH5d2nDagDoRMsdHEuKze.jpg",
				"perspective": "LOCATION_SURROUNDINGS"
			}, {
				"uri": "https://pictures.and-charge.com/img/qJZZSxd13jvU9hDPs7JC9mAee5cmDZdp.jpg",
				"thumbnailUri": "https://pictures.and-charge.com/thumb/qJZZSxd13jvU9hDPs7JC9mAee5cmDZdp.jpg",
				"perspective": "CHARGING_STATION"
			}, {
				"uri": "https://pictures.and-charge.com/img/Qv1Q9SLEc15gamxxXczFw2CsUlCGstIJ.jpg",
				"thumbnailUri": "https://pictures.and-charge.com/thumb/Qv1Q9SLEc15gamxxXczFw2CsUlCGstIJ.jpg",
				"perspective": "CHARGING_STATION"
			}, {
				"uri": "https://pictures.and-charge.com/img/CQSBxXp14dyNIeDdYA9mfS8J4pH5DVDY.jpg",
				"thumbnailUri": "https://pictures.and-charge.com/thumb/CQSBxXp14dyNIeDdYA9mfS8J4pH5DVDY.jpg",
				"perspective": "LOCATION_FULL"
			}, {
				"uri": "https://pictures.and-charge.com/img/gts4bN34Y93v4aLK1wGk8ZzJh5ryu99x.jpg",
				"thumbnailUri": "https://pictures.and-charge.com/thumb/gts4bN34Y93v4aLK1wGk8ZzJh5ryu99x.jpg",
				"perspective": "LOCATION_ENTRANCE"
			}
		]
	}
]
```