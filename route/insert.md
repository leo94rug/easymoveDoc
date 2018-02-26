# Insert travel

Insert travel

**URL** : `/rest/route/insert/`

**Method** : `POST`

**Auth required** : YES

**Data constraints** : 
```json
{
    "andata":[
        {
            "orario_partenza":[String],
            "enumerazione":[Int],
            "prezzo":[Double],
            "distanza":[Int],
            "posti":[String],
            "lat_partenza":[Double],
            "lng_partenza":[Double],
            "lat_arrivo":[Double],
            "lng_arrivo":[Double],
            "denominazione_partenza":[String],
            "denominazione_arrivo":[String],
            "durata":[Int]
        }
    ],
    "ritorno":[

    ],
    "viaggio":{
        "utente_fk":[String],
        "tipologia":[Int],
        "disponibilita_deviazioni":[String],
        "bagaglio_max":[String],
        "ritardo_max":[String],
        "auto":[String],
        "tipo":[Int]
    }
}
```

**Data example** 
```json
{
    "andata":[
        {
            "orario_partenza":"2018-05-02 00:00:00",
            "enumerazione":1,
            "prezzo":8.16400221585973,
            "distanza":152857,
            "posti":"3",
            "lat_partenza":43.3048492,
            "lng_partenza":13.721835100000021,
            "lat_arrivo":42.3498479,
            "lng_arrivo":13.399509099999932,
            "denominazione_partenza":"Civitanova Marche",
            "denominazione_arrivo":"L'Aquila",
            "durata":443820000
        }
    ],
    "ritorno":[

    ],
    "viaggio":{
        "utente_fk":"a87c3400-14ef-48b0-b198-1782d2ee2eb9",
        "tipologia":0,
        "disponibilita_deviazioni":"Faccio piccole deviazioni",
        "bagaglio_max":"Piccolo",
        "ritardo_max":"+/- 30 minuti",
        "auto":"aaa",
        "tipo":1
    }
}
```
## Success Responses

**Condition** : Correct information.

**Code** : `200 OK`

**Content** : `
{}
`

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
