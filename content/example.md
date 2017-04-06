## Test

Test for api endpoint

```endpoint
POST /v1/ext/thekom/test/saymyname/{name} test:read
```

#### Example request

```curl
$ curl -H "Authentication:TOKEN_VAL" -H "Content-Type:application/json" -X POST https://api.mallframe.com/v1/ext/thekom/test/saymyname/ugur
```

#### Example response

> HTTP 200

```json
{
	"success": "Hi, ugur!"  
}
```

## Get Digital User

Get digital user data from KNS

* Email parameter should be encoded just in case.

* **HTTP 200** Digital-user exist

* **HTTP 404** Digital-user is not exist

* **HTTP 400** Email param is invalid or KNS system has a problem

```endpoint
GET /v1/ext/thekom/digital-user/{email} digitaluser:read
```

#### Example request

```curl
$ curl -H "Authentication:TOKEN_VAL" -H "Content-Type:application/json" https://api.mallframe.com/v1/ext/thekom/digital-user/me%40ugurbaltaci.com
```

#### Example Success Response

> HTTP 200

```json
{
  "mail": "me@ugurbaltaci.com",
  "name": "Uğur",
  "surname": "Baltacı",
  "card": {},
  "birthdate": "1987-06-07",
  "gender": "M",
  "phone": "+905416258925",
  "address": {
    "country": "Italy",
    "province": "BARI",
    "city": "İstanbul",
    "cap": "34511",
    "address_detail": "Sasasasasa"
  },
  "newsletterAllowed": true
}

```

#### Example Error Response

> HTTP 404 or HTTP 400

```json
{
  "error": "Digital user not found for given e-mail: me@ugurbaltaci.com",
}
```


## Update Digital User

Update digital user data with TheKom data

* Email parameter should be encoded just in case.

* **HTTP 200** Digital-user exist

* **HTTP 404** Digital-user is not exist

* **HTTP 400** Email param or request body is invalid or KNS system has a problem

* Body, if any field is empty or does not exist, KNS does not update that field. (If it is possible TheKom should send only updated data)

```
{
	"name": "String",
	"surname": "String",
	"birthdate": "String", // Format: YYYY-MM-DD
	"gender": "String|Enum", // Valid values: "M","F"
	"phone": "String",
	"address": {
		"country": "String",
		"province": "String",
		"city": "String",
		"cap": "String", // Validate: should contain 4 or 5 digits
		"address_detail": "String"
	},
	"newsletterAllowed": Boolean
}
```

```endpoint
PUT /v1/ext/thekom/digital-user/{email} digitaluser:put
```

#### Example request

```curl
$ curl -H "Authentication:TOKEN_VAL" -H "Content-Type:application/json" -X PUT https://api.mallframe.com/v1/ext/thekom/digital-user/me%40ugurbaltaci.com -d @data.json
```

```json
{
	"birthdate": "1988/06/07",
	"phone": "05416258925"
}

```

#### Example Success Response

> HTTP 200

```json
{
  "mail": "me@ugurbaltaci.com",
  "name": "Uğur",
  "surname": "Baltacı",
  "card": {},
  "birthdate": "1987-06-07",
  "gender": "M",
  "phone": "+905416258925",
  "address": {
    "country": "Italy",
    "province": "BARI",
    "city": "İstanbul",
    "cap": "34511",
    "address_detail": "Sasasasasa"
  },
  "newsletterAllowed": true
}

```

#### Example Error Response

> HTTP 404 or HTTP 400

```json
{
	"error":"Birthdate is not valid: NOT_VALID_BIRTHDATE_DATA"
}
```
