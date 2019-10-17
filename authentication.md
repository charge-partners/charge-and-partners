# Authentication

For most &Charge APIs you need to authenticate your system for accessing the API.

- 1st you exchange your Api key and secret (which you received during partner registration) for an access and refresh token.
- 2nd you use this access token to request our API.
- In case you receive an error with http status code 401 during the API call, you can safely assume that your access token is not valid anymore. In that case you can exchange your refresh token for a new pair of access and refresh tokens or perform a fresh login again.
- If you receive an error with http status code 401 during token refresh, you should throw away both, your access and refresh tokens and start with a login procedure again.

You'll find a comprehensive documentation of those API endpoints subsequently:

# Login endpoint:

| Method           | URL                                                         | Environment                          
|------------------|-------------------------------------------------------------|--------------|
| POST             | https://api.and-charge.com/public/v1/login/partner/token    | Production
| POST             | https://api-pp.and-charge.com/public/v1/login/partner/token | Pre Production

## Request payload is as follows:

| Attribute    | Type                               | [Cardinality](syntax.md#cardinality) | max. Length | Description 
|--------------|------------------------------------|-------------|-------------|---------------------------------------------------------------------------------------------------|
| Authorization |Request header                     |1            |100          | Basic auth. Please use the following content: <pre>Basic base64(\<accessKeyId\>:\<secretAccessKey\>)</pre>Please take accessKeyId and secretAccessKey from the registration request response.

## Response payload is as follows:

| Attribute    | Type                               | Cardinality | max. Length | Description 
|--------------|------------------------------------|-------------|-------------|---------------------------------------------------------------------------------------------------|
| accessToken  |String                              |1            |100          | The access token with which you can access the API. Please do not share this token with any third party.
| refreshToken |String                              |1            |100          | The refresh token which you can trade in for a new access token / refresh token pair.
| idToken      |String                              |1            |100          | The id token which contains basic information about your partner; please do not expose this token to any API.

## Sample request & response

### Request

   POST https://api.and-charge.com/public/v1/login/partner/token
   
	Accept: application/json
	Content-Type: application/json
	Authorization: Basic LTEwMDBhYmNkZWY6cGFzc3dvcmQ=
	Content-Length: 0

### Response

```json
{
	"accessToken": "<a valid JWT to access our API>",
	"refreshToken": "<a valid JWT to refresh tokens>",
	"idToken": "<a valid JWT to give details about your system with us>"
}
```

### Error handling

The following errors are specific to this service:

| Error                      | Http status code                   | Description 
|----------------------------|------------------------------------|---------------------------------------------------------------------------------------------------------------|
| AUTHORIZATION_INVALID      | 401                                | The authorization parameters are invalid.

Please refer to [error handling](error_handling.md) for the general concept and usage of errors within the API

# Token refresh

If you receive http status code 401 on any API call, you can assume that your access token has expired. To continue using our API you need to refresh you access token by using your refresh token. For this you can call an endpoint on our system:

| Method           | URL                                           | Environment                          
|------------------|-----------------------------------------------|--------------|
| GET             | https://api.and-charge.com/public/v1/tokens    | Production
| GET             | https://api-pp.and-charge.com/public/v1/tokens | Pre Production

## Request payload is as follows:

| Attribute    | Type                               | [Cardinality](syntax.md#cardinality) | max. Length | Description 
|--------------|------------------------------------|-------------|-------------|---------------------------------------------------------------------------------------------------|
| Authorization |Request header                     |1            |100          | Bearer auth. Please use the following content: <pre>Bearer \<refresh-token\></pre>

## Response payload is as follows:

| Attribute    | Type                               | Cardinality | max. Length | Description 
|--------------|------------------------------------|-------------|-------------|---------------------------------------------------------------------------------------------------|
| accessToken  |String                              |1            |100          | The access token with which you can access the API. Please do not share this token with any third party.
| refreshToken |String                              |1            |100          | The refresh token which you can trade in for a new access token / refresh token pair.
| idToken      |String                              |1            |100          | The id token which contains basic information about your partner; please do not expose this token to any API.

## Sample request & response

### Request

   GET https://api.and-charge.com/public/v1/tokens
   
	Accept: application/json
	Content-Type: application/json
	Authorization: Bearer eyJpc3MiOiJDaGFyZ2UmTW9yZSIsInR5cCI6IkpXVCIsImFsZyI6IkVTMjU2Iiwia2lkIjoiMjYxNzYzZTUtNTU1Yy00ZDFiLThlM2MtNmI2ZDk1NGM3NmI1In0.eyJzdWIiOiItMTAwMCIsImF1ZCI6IiZDaGFyZ2UgdG9rZW4gcmVmcmVzaCIsImlzcyI6IkNoYXJnZSZNb3JlIiwiZXhwIjoxNTczOTA5ODQyLCJpYXQiOjE1NzEzMTc4NDIsInN1YmplY3QgdHlwZSI6IlBBUlRORVIifQ.cmVIsImlzcyI6IkNoYXJnZSZNoxNTcsdkj32DiOjE1NzEzMTc4mcmVzaCb3JlIiwiZXhwIjQyLCJpYXQ
	Content-Length: 0

### Response

```json
{
	"accessToken": "<a valid JWT to access our API>",
	"refreshToken": "<a valid JWT to refresh tokens>",
	"idToken": "<a valid JWT to give details about your system with us>"
}
```

### Error handling

The following errors are specific to this service:

| Error                      | Http status code                   | Description 
|----------------------------|------------------------------------|---------------------------------------------------------------------------------------------------------------|
| AUTHORIZATION_INVALID      | 401                                | The authorization parameters are invalid. Please login again


# Reset API credentials


If you want to replace your api key or secret (e.g. out of routine or because you have reason to believe that your secret has been compromised), you can use the following API.
This API will return a new api key and secret to you.

| Method           | URL                                                          | Environment                          
|------------------|--------------------------------------------------------------|--------------|
| PUT             | https://api.and-charge.com//v1/partners/{partnerId}/apikey    | Production
| PUT             | https://api-pp.and-charge.com//v1/partners/{partnerId}/apikey | Pre Production

## Request payload is as follows:

| Attribute    | Type                               | [Cardinality](syntax.md#cardinality) | max. Length | Description 
|--------------|------------------------------------|-------------|-------------|---------------------------------------------------------------------------------------------------|
| Authorization |Request header                     |1            |100          | Bearer auth. Please use the following content: <pre>Bearer \<access-token\></pre>

## Response payload is as follows:

| Attribute    | Type                               | Cardinality | max. Length | Description 
|--------------|------------------------------------|-------------|-------------|---------------------------------------------------------------------------------------------------|
| accessKeyId  |String                              |1            |100          | The ID of your API access key. This is your system's user at our [login endpoint](authentication.md#login-endpoint)
| secretAccessKey |String                           |1            |100          | The secret value with which your system authenticates itself at our [login endpoint](authentication.md#login-endpoint)
| name         |String                              |1            |100          | The name of the partner. Will be visible on our website and on transactions done with this partner
| partnerId    |String                              |1            |100          | A system wide unique identifier of this partner. Pick any ID you see fit. Will not be visible to users
| type         |Enumeration                         |1            |-/-          | The partner type. Possible values are: MSP, ONLINE_SHOP, OFFLINE_SHOP
| logo         |URL                                 |1            |2000         | A url to a logo of this partner. Ideally sized 320x240px; will be visible to users to identify the partner
| web          |URL                                 |1            |2000         | A link to the partners web site
| android      |URL                                 |?            |2000         | A link to an android app of the partner
| iOS          |URL                                 |?            |2000         | A link to an iOS app of the partner
| descriptions |[Description](types.md#description-class) |+            |-/-          | A list of descriptions for that partner (one text per language) explaining the partner within the context of Charge&. Will be visible to users. Please provide translations for at least `de` and `en`

## Sample request & response

### Request

   PUT https://api.and-charge.com/public/v1/tokens
   
	Accept: application/json
	Content-Type: application/json
	Authorization: Bearer eyJpc3MiOiJDaGFyZ2UmTW9yZSIsInR5cCI6IkpXVCIsImFsZyI6IkVTMjU2Iiwia2lkIjoiMjYxNzYzZTUtNTU1Yy00ZDFiLThlM2MtNmI2ZDk1NGM3NmI1In0.eyJzdWIiOiItMTAwMCIsImF1ZCI6IiZDaGFyZ2UgdG9rZW4gcmVmcmVzaCIsImlzcyI6IkNoYXJnZSZNb3JlIiwiZXhwIjoxNTczOTA5ODQyLCJpYXQiOjE1NzEzMTc4NDIsInN1YmplY3QgdHlwZSI6IlBBUlRORVIifQ.cmVIsImlzcyI6IkNoYXJnZSZNoxNTcsdkj32DiOjE1NzEzMTc4mcmVzaCb3JlIiwiZXhwIjQyLCJpYXQ
	Content-Length: 0

### Response

```json
{
	"id": 4,
   	"name": "Porsche Charging Service",
   	"partnerId": "PCS-001",
   	"logo": "https://connect-store-static01.porsche.com/_ui/images/porsche-logo@3x.png",
   	"web": " https://connect-store.porsche.com/de/de/porsche-charging-service/p/PorscheChargingService",
   	"android": "https://play.google.com/store/apps/details?id=com.porsche.mobilityapp&gl=de&hl=de",
   	"iOS": "https://itunes.apple.com/de/app/mobility-by-porsche/id1286754490?mt=8",
	"descriptions": [{
			"key": "DESCRIPTION",
			"lang": "de",
			"text": "Der Porsche Charging Service integriert Elektromobilität problemlos in deinen Alltag – digital und vielfältig. Er vereint alle Lademöglichkeiten für Plug-in-Hybride und Elektrofahrzeuge und eröffnet dir Zugang zu Ladesäulen unterschiedlicher Anbieter. Nach einer einfachen Anmeldung über My Porsche und dem Kauf im Porsche Connect Store erhältst du die Porsche ID Card und Zugang zur App. Der Porsche Charging Service bietet aktuell ca. 49.000 Ladepunkte in Deutschland, Österreich, Schweiz, Belgien, Niederlande, Spanien, Frankreich, Dänemark, Finnland und Norwegen."
		}, {
			"key": "DESCRIPTION",
			"lang": "en",
			"text": "The Porsche Charging Service integrates e-mobility seamlessly into your daily life - digital and versatile. It combine all charging opportunities for plug-in hybrid and electric cars and opens up access to charging stations of various operators. After an easy registration at My Porsche and buying the service within the Porsche Connect store you will receive the Porsche ID Card and access to the Charging App. The Porsche Charging Service offers access to about 49,000 charging stations in Germany, Austria, Switzerland, Belgium, Netherlands, Spain, France, Denmark, Finland and Norway."
		}
	],
	"status": "INITIAL",
	"accessKeyId": "alkj21FHJqhq",
	"secretAccessKey": "<treat this value as a secret, don't share it with anybody else>"
}
```

### Error handling

The following errors are specific to this service:

| Error                      | Http status code                   | Description 
|----------------------------|------------------------------------|---------------------------------------------------------------------------------------------------------------|
| AUTHORIZATION_INVALID      | 401                                | The authorization parameters are invalid. Please login again

