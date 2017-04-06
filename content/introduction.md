## TheKom - KNS Integration

**Authentication**

Authentication token should be added in the request headers.

```curl
$ curl -H "Authentication:PREDEFINED_TOKEN_VAL" https://api.mallframe.com/v1/ext/thekom/ 
```

**Content-Type**

Requests contain json body should add content-type header with application/json 

```curl
$ curl -H "Content-Type:application/json" https://api.mallframe.com/v1/ext/thekom/ 
```

