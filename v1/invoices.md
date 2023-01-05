---
Title: Invoices
---

## listing invoices

* **method** GET : (GET /obapi/v1/invoices)
* **headers**

### listing parameters

* **datestart** (option), string YYYY-mm-dd to specify a date from wich you want to get the list
* **datestop**  (option), string YYYY-mm-dd for the end period to request

### result


Result will be a list of available invoices

```json
{
    "message": "here is your invoices",
    "invoices":   
    {
        "ref": "20220424-124588",
        "uuid": "0000-1111-2222-3333",
        "date": "2022-04-24",
        "amount": "9.99",
        "label": "april 2022",
        "status": "payed",
    },
    {
        "ref": "20220522-184521",
        "uuid": "0000-1111-2222-3334",
        "date": "2022-05-22",
        "amount": "9.99",
        "label": "may 2022",
        "status": "unpayed",
    }
}
```

