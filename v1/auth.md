---
Title: Authentication
Order: 1001
---

## Authentication

Authentification may be done with API keys but normal humans don't care about that ... so first auth could be done with only login/passwd + one more thing (secret code send by email for example), then the API key will be generated and will be required for next requests.

Auth URI will be **`/obapi/v1/auth`**

### auth process

To avoid sending plain password (even if ssl transport layer is required) you have to request for a new temporary crypt key.


* **login** string, example eric@obapi.org
* **action: preauth**
* **method** POST : (POST /obapi/v1/auth)

Example:
```json
{
  "login": "eric@obapi.org",
  "action": "preauth"
}
```


Then the server will give you a response like


```json
{
  "message": "welcome eric@obapi.org !",
  "apiversion": "1.0",
  "tmpkey": "XXXXXXXX",
  "validuntil": "30"
}
```

* **`publickey`**: string, please use that temporary key for the next auth request
* **`validuntil`** : peremption delay in seconds for the temporary key, then you have to ask for a new one

Note: during that step the server will build a couple of private&public key, it store the public one and returns the private in "tmpkey" json field, then the client will use that key to crypt the password


### auth parameters

* **login** string, example eric@obapi.org
* **password** string (password crypted with the key from the previous step)
* **action: auth**
* **method** POST : (POST /obapi/v1/auth)


Example:

```json
{
  "login": "eric@obapi.org",
  "password": "xxxxxxxxxxxxxxxxxxxxxxxxxx",
  "action": "auth"
}
```


Then the server will give you a response like


```json
{
  "message": "welcome onboard eric@obapi.org !",
  "apikey": "YOUR_AUTH_KEY"
}
```

Save that apikey, you have to use if for all other requests

### auth with api key

Now you have your api key, so please use it for all other requests with classic `Bearer: requests`

Authenticate requests to this API's endpoints by sending an Authorization header with the value "Bearer {YOUR_AUTH_KEY}".
