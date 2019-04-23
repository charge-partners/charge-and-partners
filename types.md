# Data types

## Description *class*

| Attribute | Type  | Cardinality  | max. Length | Description 
|-----------|-------|--------------|-------------|---------------------------------------------------------------------------------------------------|
| lang      |String | 1            |2            | The alpha-2 language code of the language according to ISO 639-1
| text      |String | 1            |2000         | The description text in the corresponding language

## Transaction *class*

| Attribute      | Type       | Cardinality  | max. Length   | Description 
|----------------|------------|--------------|---------------|---------------------------------------------------------------------------------------------------|
| transactionId  |String      | 1            |100            | The ID of the transaction.
| partner        |String      | 1            |100            | The name of the partner with which the user did this transaction
| kilometer      |Integer     | 1            |-/-            | The kilometer added or removed from the account for this transaction
| status         |Enumeration | 1            |-/-            | An enumeration defining the status of the transaction. Possible values are: OPEN, CONFIRMED, CANCELLED
| created        |String      | 1            |-/-            | The date and time when the transaction was created
| type           |String      | 1            |-/-            | The transaction type (an enumeration). Possible values are: ACCOUNT_REGISTRATION, ONLINE_SHOPPING, CHARGING_SESSION, CO2_OFFSET_CHARGING_SESSION, CO2_DONATION
| address        |String      | ?            |-/-            | The address where the transaction happened. This attribute is unavailable for many transaction types.

## TransactionRequest *class*

| Attribute            | Type       | Cardinality  | max. Length   | Description 
|----------------------|------------|--------------|---------------|---------------------------------------------------------------------------------------------------|
| transactionId        |String      | 1            |100            | The ID of the transaction.
| transactionReference |String      | ?            |100            | A transaction reference, if you need it
| service              |Enumeration | 1            |-/-            | The service you want to create a transaction for. Possible values are: PAY_FOR_CHARGING_SESSION, CO2_OFFSET_CHARGING_SESSION, DONATE_FOR_CO2_OFFSET
| kilometer            |Integer     | 1            |-/-            | The value of the transaction in Charge& kilometers
| serviceSpecificData  |Map of [ServiceAttribute](types.md#serviceattribute-enumeration) | 1            |-/-            | All service specific attributes

## ServiceAttribute *enumeration*

| Possible values          | Type        | Format                      | Required for services                                 | Description 
|--------------------------|-------------|-----------------------------|-------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| EVSE_ID                  | String      | -/-                         | PAY_FOR_CHARGING_SESSION, CO2_OFFSET_CHARGING_SESSION | The evse ID which was used for the charging session
| COUNTRY                  | String      | ISO 3166 alpha-2 or alpha-3 | PAY_FOR_CHARGING_SESSION, CO2_OFFSET_CHARGING_SESSION | The country in which the charging session was done
| CITY                     | String      | -/-                         | PAY_FOR_CHARGING_SESSION, CO2_OFFSET_CHARGING_SESSION | The city in which the charging session was done
| STREET                   | String      | -/-                         | PAY_FOR_CHARGING_SESSION, CO2_OFFSET_CHARGING_SESSION | The street in which the charging session was done
| HOUSE_NUMBER             | String      | -/-                         | PAY_FOR_CHARGING_SESSION, CO2_OFFSET_CHARGING_SESSION | The house-number of the charging location
| CONSUMED_ENERGY_KWH      | Decimal     | #.##                        | PAY_FOR_CHARGING_SESSION, CO2_OFFSET_CHARGING_SESSION | The amount of energy charged during the session
| SESSION_START            | String      | yyyy-MM-dd'T'HH:mm:ss.SSSZ  | PAY_FOR_CHARGING_SESSION, CO2_OFFSET_CHARGING_SESSION | The date & time when the session was started
| SESSION_END              | String      | yyyy-MM-dd'T'HH:mm:ss.SSSZ  | PAY_FOR_CHARGING_SESSION, CO2_OFFSET_CHARGING_SESSION | The date & time when the session ended
| GEO_POSITION_USER        | String      | [-]#.######,[-]#.######     | PAY_FOR_CHARGING_SESSION, CO2_OFFSET_CHARGING_SESSION | The geo position of the user when the session was authorized
| GEO_POSITION_CHARGEPOINT | String      | [-]#.######,[-]#.######     | PAY_FOR_CHARGING_SESSION, CO2_OFFSET_CHARGING_SESSION | The geo position of the charging station
