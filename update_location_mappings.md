# Update location mappings

Send us your location data so we can use it to map pictures and other data to it.

## Update location mappings

| Method           | URL                                                   | Environment                          
|------------------|-------------------------------------------------------|--------------|
| POST             | https://api.charge-and.com/public/v1/partners/{partnerId}/locations | Production
| POST             | https://api-pp.charge-and.com/public/v1/partners/{partnerId}/locations | Pre Production

### Request parameters are as follows:

| Attribute     | Request part  | Type                               | Cardinality | max. Length | Description 
|---------------|---------------|------------------------------------|-------------|-------------|---------------------------------------------------------------------------------------------------|
| Authorization |Request header | String                             |1            |100          | The accessToken authorizing you to do the request. The header value must be in form of: Bearer <accessToken>
| partnerId     |Path param     | String                             |1            |100          | Your partner ID with which you registered yourself as a partner
| mappings      |Request body   | [LocationMappingsInput](types.md#locationmappingsinput-class) |1            |-/-          | Your location data

### Response payload:

The request does not deliver any data as a response. Verify the http status to ensure the request was successful, everything in the range of HTTP status 2XX indicates a successful operation.

### Sample request

#### Request

   POST https://api.charge-and.com/public/v1/partners/PCS-001/locations

   Request headers:
```
Content-Type: application/json
Authorization: Bearer <your JWT access token received during partner registration>
```

   POST data:
```json
{
	"mappings": [
	  {
	     "latitude":"51.582837",
	     "longitude": "7.212042",
	     "locationId": "7981",
	     "cpoId": "DE*ISE"
	  },
	  {
	     "latitude":"49.296461",
	     "longitude": "10.578064",
	     "locationId": "9028",
	     "cpoId": "DE*BDO"
	  },
	  {
	     "latitude":"51.670907",
	     "longitude": "5.023878",
	     "locationId": "24158",
	     "cpoId": "NL*LMS"
	  }
     ]
}   
```