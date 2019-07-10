# Error handling

For every API call, there is a small chance that things might go wrong. This section explains on how we handle and communicate errors.
To determine the status of an API call, the http status code of the response will give a general indication:

| Status code      | Meaning                                                                   | How to fix
|------------------|---------------------------------------------------------------------------|--------------|
| 200 till 299     | Success. The request was successfully handled           .                 | -/-
| 400 till 499     | Client error. Bad request. Something with the request was wrong.          | Check the request and fix the issue. Usually something like a missing attribute; an invalid reference to a resource or an invalid value
| 500 till 599     | Server error. Something went wrong within Charge& or a system we rely on. | Your request was legit. Please notify us if the issue pertains. Usually we scan our logs for those errors and are working on a fix

As the http status is only a number, you might get confused on why a specific error occurs. To help you debug or analyze an issue, we try to give you a more detailed error object that explains and possible parameterizes an issue.
E.g. you might get the information that a mandatory parameter was missing within the request. For this error you can expect us to deliver the name of the attribute within the error object.

Whenever possible we will include an error object with each response that has a status code between 400 and 599. However as there is a lot of network infrastructure between your host and our application and this infrastructure can fail as well, we cannot guarantuee an error object with every error request.

## Structure of an error object:

| Attribute    | Type                               | Cardinality | max. Length | Description 
|--------------|------------------------------------|-------------|-------------|---------------------------------------------------------------------------------------------------|
| error        |Enumeration                         |1            |-/-          | The type of error that occurred
| args         |String                              |*            |100          | An argument detailing the source or kind of error. You can use this to e.g. determine which part of the request was invalid

## Sample error messages:

Here is a list of some very common error objects:

If the request is missing the parameter **name** which we declared to be mandatory:
```json
{"error":"MANDATORY_PARAMETER_NOT_SET","args":["name"]}
```

If the value of an attribute **name** is too long. Allowed length is **100** characters:
```json
{"error":"PARAMETER_MAX_LENGTH","args":["name",100]}
```

If the input of the request cannot be parsed as valid JSON:
```json
{"error":"INVALID_FORMAT","args":["An input parameter did not have the expected format. Please check interface specification."]}
```

If the authorization header provided is not valid (wrong token, expired token, token could not be verified):
```json
{"error":"AUTHORIZATION_INVALID","args":[]}
```

If an attribute of the request exceeds the defined range (in this case an invalid **latitude** of **90.01**:
```json
{"error":"INVALID_PARAMETER","args":["mappings[2]..latitude (must be between -90 and +90)","90.01"]}
```
