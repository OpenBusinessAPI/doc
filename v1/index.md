---
Title: Draft v1
---

# OpenBusinessAPI - draft version 1

Sources : https://inligit.fr/obapi/doc


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
