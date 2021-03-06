# Users

## Create a customer

```shell
curl -X POST "https://127.0.0.1.xip.io/api/v1/users"
  -H "Authorization: Token token=YOURTOKEN"
  -H "Content-Type: application/json"
  -d '{"first_name":"CHERYL","last_name":"SERFONTEIN","email_address":"cheryl@imogo.co.za","mobile_number":"08012345679","store_id":"12345678901","till_id":"1"}'
```

> The above command returns JSON structured like this:

```json
{
  "status":"ok",
  "details":{
    "uuid":"2b1c1f24-c5ff-11e5-99c3-5a8f9bcf73ec",
    "account_number":"53224172946"
  }
}
```

This endpoint creates a new customer on the BongoTel Platform.  During the
registration process a wallet is issued to the customer.

### HTTP Request

`POST https://127.0.0.1.xip.io/api/v1/users`

### JSON Payload Parameters

Parameter | Type | Required | Description
--------- | ---- | -------- | -----------
first_name | string (64) | true | First names of the user
last_name | string (64) | true | Surname of the user
id_type | string | false | Identification Document Type (ZAID == South African ID / PASSPORT = Passport / ZAASYLUM = South African Asylum Document)
id_document_number | string (32) | false | The document number for the given identification type
mobile_number | integer | true | MSISDN for the user in E.164 format (minus the leading +)
email_address | string(64) | true | Email address of the user
key_field | varchar(32) | false | Your key field for the user (i.e. user id on your system)
store_id | integer | true | Store ID
till_id | integer | true | Till Id (i.e. Lane 1 == Till 1)

### Response Result Set

Parameter | Type | Description
--------- | ---- | -----------
uuid | string (36) | UUID of the user that was created
account_number | interger | BongoTel Wallet Account Number

## Lookup a customer

```shell
curl -X POST "https://127.0.0.1.xip.io/api/v1/users/search"
  -H "Authorization: Token token=YOURTOKEN"
  -H "Content-Type: application/json"
  -d '{"email_address":"cheryl@imogo.co.za","mobile_number":"08012345679"}'
```

> The above command returns JSON structured like this:

```json
{
  "status": "ok",
  "details": [
    {
       "first_name": "CHERYL",
       "last_name": "SERFONTEIN",
       "email_address": "cheryl@imogo.co.za",
       "mobile_number": "08012345679"
    }
  ]
}
```

### HTTP Request

`POST https://127.0.0.1.xip.io/api/v1/users/search`

### JSON Payload Parameters

Parameter | Type | Description
--------- | ---- | -----------
id_type | string | Identification Document Type (ZAID == South African ID / PASSPORT = Passport / ZAASYLUM = South African Asylum Document)
id_document_number | string (32) | The document number for the given identification type
mobile_number | integer | MSISDN for the user in E.164 format (minus the leading +)
email_address | string(64) | Email address of the user
key_field | string (32) | Your key field for the user (i.e. user id on your system)
store_id | integer | Store ID
till_id | integer | Till Id (i.e. Lane 1 == Till 1)

### Response Result Set

Parameter | Type | Description
--------- | ---- | -----------
uuid | string (36) | UUID of the user that was created
first_name | string (64) | true | First names of the user
last_name | string (64) | true | Surname of the user
id_type | string | Identification Document Type (ZAID == South African ID / PASSPORT = Passport / ZAASYLUM = South African Asylum Document)
id_document_number | string (32) | The document number for the given identification type
mobile_number | integer | MSISDN for the user in E.164 format (minus the leading +)
email_address | string(64) | Email address of the user
fica_status | integer | 0 == Not FICA'd / Exemption 17 | 1 == (POID on File) | 2 == Full FICA (POID and POA on File)
key_field | string (32) | Your key field for the user (i.e. user id on your system)

## Update a customer

```shell
curl -X POST "https://127.0.0.1.xip.io/api/v1/users/<USER>"
  -H "Authorization: Token token=YOURTOKEN"
  -H "Content-Type: application/json"
  -d '{"first_name":"CHERYL","last_name":"SERFONTEIN","email_address":"cheryl@imogo.co.za","mobile_number":"08012345679","store_id":"12345678901","till_id":"1"}'
```

> The above command returns JSON structured like this:

```json
{
  "status": "ok",
  "message": "Customer updated successfully."
}
```

### HTTP Request

`POST https://127.0.0.1.xip.io/api/v1/users/<USER>`

### URL Parameters

Parameter | Description
--------- | -----------
USER | The UUID of the user to update

### JSON Payload Parameters

Parameter | Type | Description
--------- | ---- | -----------
first_name | string (64) | First names of the user
last_name | string (64) | Surname of the user
id_type | string | Identification Document Type (ZAID == South African ID / PASSPORT = Passport / ZAASYLUM = South African Asylum Document)
id_document_number | string (32) | The document number for the given identification type
mobile_number | integer | MSISDN for the user in E.164 format (minus the leading +)
email_address | string(64) | Email address of the user
key_field | varchar(32) | Your key field for the user (i.e. user id on your system)
store_id | integer | Store ID
till_id | integer | Till Id (i.e. Lane 1 == Till 1)
