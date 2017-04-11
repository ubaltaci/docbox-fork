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

## Digital User (GET)

Get digital user data from KNS

* Email parameter should be encoded just in case.

* **HTTP 200** Digital-user exist

* **HTTP 204** Digital-user is not exist

* **HTTP 400** Email param is invalid or KNS system has a problem

```endpoint
GET /v1/ext/thekom/digital-user/{email} digital-user:GET
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
  "name": "Ugur",
  "surname": "Baltaci",
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
#### Example No Content Response (Digital-user is not exist) 

> HTTP 204

#### Example Error Response

> HTTP 400

```json
{
  "error": "Digital user not found for given e-mail: me@ugurbaltaci.com",
}
```


## Digital User (PUT)

Update digital user data with TheKom data

* Email parameter should be encoded just in case.

* **HTTP 200** Digital-user exist

* **HTTP 204** Digital-user is not exist

* **HTTP 400** Email param or request body is invalid or KNS system has a problem

* **To detach a card from a user card field should constructed as empty object ie: `card: {}`**

```
{
	"name": "String", // required
	"surname": "String", // required
	"gender": "String", // required, valid values: "M","F"
	"newsletterAllowed": Boolean // required
	
	"birthdate": "String", // optional, format: YYYY-MM-DD or empty string 
	"phone": "String", // optional
	
	"address": { // optional
		"country": "String", 
		"province": "String",
		"city": "String", 
		"cap": "String", // validate: should contain 4 or 5 digits or empty string
		"address_detail": "String"
	},
	
	"card": { // optional
		"id: "String",
		"outletCode": "String",
		"type": Number,
		"insertDate": "String", // format: YYYY-MM-DD or empty string,
		"activationDate": "String", // format: YYYY-MM-DD or empty string,
		"expiringDate": "String", // format: YYYY-MM-DD or empty string,
	}
}
```

```endpoint
PUT /v1/ext/thekom/digital-user/{email} digital-user:PUT
```

#### Example request

```curl
$ curl -H "Authentication:TOKEN_VAL" -H "Content-Type:application/json" -X PUT https://api.mallframe.com/v1/ext/thekom/digital-user/me%40ugurbaltaci.com -d @data.json
```

```json
{
	"name": "Ugur2",
	"surname": "Baltaci2",
	"gender": "M",
	"newsletterAllowed": false,
	"birthdate": "1988/06/07",
	"phone": "05416258925"
}

```

#### Example Success Response

> HTTP 200

```json
{
  "mail": "me@ugurbaltaci.com",
  "name": "Ugur",
  "surname": "Baltaci",
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
#### Example No Content Response (Digital-user is not exist) 

> HTTP 204

#### Example Error Response

> HTTP 400

```json
{
	"error":"Birthdate is not valid: NOT_VALID_BIRTHDATE_DATA"
}
```

## Card Issued (DELETE)

Delete Card from Digital User

* Email parameter should be encoded just in case.

* **HTTP 200** Digital-user exist and card removed

* **HTTP 204** Digital-user is not exist.

* **HTTP 400** Email param or request body is invalid or KNS system has a problem

```endpoint
DELETE /v1/ext/thekom/card-issued/{email} card-issued:DELETE
```

#### Example request

```curl
$ curl -H "Authentication:TOKEN_VAL" -H "Content-Type:application/json" -X DELETE https://api.mallframe.com/v1/ext/thekom/card-issued/me%40ugurbaltaci.com
```


#### Example Success Response

> HTTP 200

```json
{
  "mail": "me@ugurbaltaci.com",
  "name": "Ugur",
  "surname": "Baltaci",
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
#### Example No Content Response (Digital-user is not exist) 

> HTTP 204

#### Example Error Response

> HTTP 400

```json
{
	"error":"Birthdate is not valid: NOT_VALID_BIRTHDATE_DATA"
}
```

## Card Issued (POST)

New loyalty card issued or e-mail added to existing card. If existing card has already e-mail,  /card-issued [PUT] should be called.

* Email parameter should be encoded just in case.

* **HTTP 200** Digital-user exist and card associated.

* **HTTP 204** Digital-user is not exist.

* **HTTP 400** Email param or request body is invalid or KNS system has a problem

```endpoint
POST /v1/ext/thekom/card-issued/{email} card-issued:POST
```

#### Example request

```curl
$ curl -H "Authentication:TOKEN_VAL" -H "Content-Type:application/json" -X POST https://api.mallframe.com/v1/ext/thekom/card-issued/me%40ugurbaltaci.com -d @data.json
```

```json
{
   "name": "Ugur",
	"surname": "Baltaci",
	"gender": "M",
	"newsletterAllowed": false,
	"birthdate": "1988/06/07",
	"phone": "05416258925",
	"address": { 
		"country": "Turkey", 
		"province": "Marmara",
		"city": "Istanbul", 
		"cap": "03589", 
		"address_detail": "Akar Cd: No:3/59"
	},
	"card": {
		"id: "11223434455",
		"outletCode": "FRA",
		"type": 1,
		"insertDate": "2017-01-01", 
		"activationDate": "2017-01-01",
		"expiringDate": "2022-01-01"
	},
}

```

#### Example Success Response

> HTTP 200

```json
{
	"mail": "me@ugurbaltaci.com",
	"name": "Ugur",
	"surname": "Baltaci",
	"card": {},
	"birthdate": "1987-06-07",
	"gender": "M",
	"phone": "+905416258925",
	"address": { 
		"country": "Turkey", 
		"province": "Marmara",
		"city": "Istanbul", 
		"cap": "03589", 
		"address_detail": "Akar Cd: No:3/59"
	},
	"card": {
		"id: "11223434455",
		"outletCode": "FRA",
		"type": 1,
		"insertDate": "2017-01-01", 
		"activationDate": "2017-01-01",
		"expiringDate": "2022-01-01"
	},
	"newsletterAllowed": true
}


#### Example No Content Response (Digital-user is not exist) 

> HTTP 204

#### Example Error Response

> HTTP 400

```json
{
	"error":"Birthdate is not valid: NOT_VALID_BIRTHDATE_DATA"
}
```

## Card Issued (PUT)

Only used when e-mail address of existing card changed.

If existing card has not an e-mail previously, /card-issued [POST] should be called.

* Email parameter should be encoded just in case.

* **HTTP 200** Card associated.

* **HTTP 202** Card associated. **TheKom displays a message to the assistant at the info point: "Remind to the person that has to perform logout from the mobile app (if installed) and login again in the web site using old mail and password in order to set new password"**

* **HTTP 204** No-content, card is not associated.

* **HTTP 400** Email param or request body is invalid or KNS system has a problem

```endpoint
PUT /v1/ext/thekom/card-issued/{old-email}/{new-email} card-issued:PUT
```

#### Example request

```curl
$ curl -H "Authentication:TOKEN_VAL" -H "Content-Type:application/json" -X PUT https://api.mallframe.com/v1/ext/thekom/card-issued/me%40ugurbaltaci.com/ugur.baltaci%40mallframe.com -d @data.json
```

```json
{
	"name": "Ugur",
	"surname": "Baltaci",
	"gender": "M",
	"birthdate": "1988/06/07",
	"phone": "05416258925",
	"address": { 
		"country": "Turkey", 
		"province": "Marmara",
		"city": "Istanbul", 
		"cap": "03589", 
		"address_detail": "Akar Cd: No:3/59"
	},
	"card": {
		"id: "11223434455",
		"outletCode": "FRA",
		"type": 1,
		"insertDate": "2017-01-01", 
		"activationDate": "2017-01-01",
		"expiringDate": "2022-01-01"
	},
	"newsletterAllowed": false
}

```

#### Example Success Response

> HTTP 200 or HTTP 202

```json
{
  "mail": "me@ugurbaltaci.com",
  "name": "Ugur",
  "surname": "Baltaci",
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
  "card": {
		"id: "11223434455",
		"outletCode": "FRA",
		"type": 1,
		"insertDate": "2017-01-01", 
		"activationDate": "2017-01-01",
		"expiringDate": "2022-01-01"
  },
  "newsletterAllowed": true 
}


#### Example No Content Response (Digital-user is not exist) 

> HTTP 204

#### Example Error Response

> HTTP 400

```json
{
	"error":"Birthdate is not valid: NOT_VALID_BIRTHDATE_DATA"
}
```