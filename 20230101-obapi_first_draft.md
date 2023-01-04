# OpenBusinessAPI - First draft

## endpoint

**`/obapi/v1`**

## errors

Conventional HTTP response codes to indicate the success or failure of an API request.
* **2xx** range indicate success
* **4xx** range indicate an error that failed given the information provided
* **5xx** range indicate an error with server

### errors attributes

* **type** string
* **code** string
* **message** string


## authentication

Authentification may be done with API keys but normal humans don't care about that ... so first auth could be done with only login/passwd + one more thing (secret code send by email for example), then the API key will be generated and provide for next requests.

Auth URI will be **`/obapi/v1/auth`**

### auth process

First you have to request for a new temporary crypt key


* **login** string
* **action: preauth**
* **method** POST : (POST /obapi/v1/auth)

Example:
```json
{
  login: "eric@obapi.org";
  action: "preauth";
}
```


Then the server will give you a response like


```json
{
  message: "welcome eric@obapi.org !";
  apiversion: "1.0";
  key: "XXXXXXXX";
}
```


### auth parameters

* **login** string
* **password** string (password crypted with key)
* **action: auth**
* **method** POST : (POST /obapi/v1/auth)


Example:

```json
{
  login: "eric@obapi.org";
  password: "xxxxxxxxxxxxxxxxxxxxxxxxxx";
  action: "auth";
}
```


Then the server will give you a response like


```json
{
  message: "welcome onboard eric@obapi.org !";
  apikey: "YOUR_AUTH_KEY";
}
```

Save that apikey, you have to use if for all other requests

### auth with api key

Now you have your api key, so please use it for all other requests with classic Beacon: requests

Authenticate requests to this API's endpoints by sending an Authorization header with the value "Bearer {YOUR_AUTH_KEY}".


## listing invoices

* **method** GET : (GET /obapi/v1/invoices)
* **headers**

Result will be a list of available invoices

```json
{
    message: "here is your invoices";
    "invoices":   
    {
        "ref": "20220424-124588",
        "date": "2022-04-24",
        "amount": "9.99",
        "label": "april 2022",
        "status": "payed",
    },
    {
        "ref": "20220522-184521",
        "date": "2022-05-22",
        "amount": "9.99",
        "label": "may 2022",
        "status": "unpayed",
    }
}
```


## downloading resources

* **method** GET : (GET /obapi/v1/download/ref), example GET /obapi/v1/download/20220424-124588
* **object** : string keyword of type of object to download (invoices)
* **headers**

Result will be a binary file (PDF)

