# Search travel

Search travel

**URL** : `/rest/route/cercaauto/`

**Method** : `POST`

**Auth required** : YES

**Data constraints** : 
```json
{
    "lat_p":[Double],
    "lat_a":[Double],
    "lng_p":[Double],
    "lng_a":[Double],
    "tipo":[Int],
    "date_search":[String],
    "cambio":[Int],
    "distanza":[Int],
    "utente_fk":[String],
    "distanza_tra":[Int]
}
```

**Data example** 
```json
{
    "lat_p":43.3048492,
    "lat_a":43.2563334,
    "lng_p":13.721835100000021,
    "lng_a":13.759297500000002,
    "tipo":0,
    "date_search":"2018-02-26 11:28:02",
    "cambio":0,
    "distanza":1,
    "utente_fk":"a87c3400-14ef-48b0-b198-1782d2ee2eb9",
    "distanza_tra":10069
}
```
## Success Responses

**Condition** : Correct information.

**Code** : `200 OK`

**Content** : 
```json
[
    {
        "tratta_auto":{
            "id":"3c30103f-427c-45a2-a2e9-e25776b9bebc",
            "orario_partenza":"2018-05-09 00:00:00",
            "enumerazione":1,
            "data":"2018-02-26 11:03:45",
            "viaggio_fk":"a8c434b2-dc8b-4bd3-9f2f-b5a1fe1a55ef",
            "prezzo":4,
            "distanza":89188,
            "posti":2,
            "lat_partenza":43.3040597,
            "lng_partenza":13.734304000000066,
            "lat_arrivo":43.5296138,
            "lng_arrivo":13.054238400000031,
            "denominazione_partenza":"Viale Vittorio Veneto, Civitanova Marche",
            "denominazione_arrivo":"Passetto"
        },
        "utente":{
            "eta":24,
            "id":"a87c3400-14ef-48b0-b198-1782d2ee2eb9",
            "email":"master_94@virgilio.it",
            "nome":"Leonardo",
            "cognome":"Ruggeri",
            "anno_nascita":"1994-01-25 00:00:00",
            "professione":"asdf",
            "telefono1":"3332057204",
            "telefono2":"3332057204",
            "password":"D73AzyBnRpR5b2VClNCr8w\u003d\u003d",
            "biografia":"L\u0027utente non ha ancora inserito una biografia",
            "foto_utente":"https://www.dropbox.com/s/ht1ik2uygkjea3u/profile?raw\u003d1",
            "image_path":"/immagine-profilo/profile",
            "sesso":"male",
            "fumare":0,
            "animali":0,
            "tipo":1,
            "media_feedback":0
        },
        "id_partenza":"3c30103f-427c-45a2-a2e9-e25776b9bebc",
        "id_arrivo":"3c30103f-427c-45a2-a2e9-e25776b9bebc",
        "id":"a8c434b2-dc8b-4bd3-9f2f-b5a1fe1a55ef",
        "ritardo_max":"+/- 15 minuti",
        "bagaglio_max":"Medio",
        "disponibilita_deviazioni":"Non faccio deviazioni",
        "utente_fk":"a87c3400-14ef-48b0-b198-1782d2ee2eb9",
        "auto":"A8",
        "data":"2018-02-26 11:03:45",
        "tipologia":1
    }
]
```

## Error Responses

**Condition** : Server error

**Code** : `500 SERVER ERROR`

**Content** : `{}`





Provide name of Account to be created.
Provide name of Account to be created.

```json
{
    "name": "[unicode 64 chars max]"
}
```

**Data example** All fields must be sent.

```json
{
    "name": "Build something project dot com"
}
```

## Success Response

**Condition** : If everything is OK and an Account didn't exist for this User.

**Code** : `201 CREATED`

**Content example**

```json
{
    "id": 123,
    "name": "Build something project dot com",
    "url": "http://testserver/api/accounts/123/"
}
```

## Error Responses

**Condition** : If Account already exists for User.

**Code** : `303 SEE OTHER`

**Headers** : `Location: http://testserver/api/accounts/123/`

**Content** : `{}`

### Or

**Condition** : If fields are missed.

**Code** : `400 BAD REQUEST`

**Content example**

```json
{
    "name": [
        "This field is required."
    ]
}
```

# Update Current User

Allow the Authenticated User to update their details.

**URL** : `/api/user/`

**Method** : `PUT`

**Auth required** : YES

**Permissions required** : None

**Data constraints**

```json
{
    "first_name": "[1 to 30 chars]",
    "last_name": "[1 to 30 chars]"
}
```

Note that `id` and `email` are currently read only fields.

**Header constraints**

The application used to update the User's information can be sent in the
header. Values passed in the `UAPP` header only pass basic checks for validity:

- If 0 characters, or not provided, ignore.
- If 1 to 8 characters, save.
- If longer than 8 characters, ignore.

```
UAPP: [1 to 8 chars]
```

**Data examples**

Partial data is allowed.

```json
{
    "first_name": "John"
}
```

Empty data can be PUT to erase the name, in this case from the iOS application
version 1.2:

```
UAPP: ios1_2
```

```json
{
    "last_name": ""
}
```

## Success Responses

**Condition** : Data provided is valid and User is Authenticated.

**Code** : `200 OK`

**Content example** : Response will reflect back the updated information. A
User with `id` of '1234' sets their name, passing `UAPP` header of 'ios1_2':

```json
{
    "id": 1234,
    "first_name": "Joe",
    "last_name": "Bloggs",
    "email": "joe25@example.com",
    "uapp": "ios1_2"
}
```

## Error Response

**Condition** : If provided data is invalid, e.g. a name field is too long.

**Code** : `400 BAD REQUEST`

**Content example** :

```json
{
    "first_name": [
        "Please provide maximum 30 character or empty string",
    ]
}
```

## Notes

* Endpoint will ignore irrelevant and read-only data such as parameters that
  don't exist, or fields that are not editable like `id` or `email`.
* Similar to the `GET` endpoint for the User, if the User does not have a
  UserInfo instance, then one will be created for them.

  Login
Used to collect a Token for a registered User.

URL : /api/login/

Method : POST

Auth required : NO

Data constraints

{
    "username": "[valid email address]",
    "password": "[password in plain text]"
}
Data example

{
    "username": "iloveauth@example.com",
    "password": "abcd1234"
}
Success Response
Code : 200 OK
