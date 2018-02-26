# Conferma email


Allows the user to confirm email

**URL** : `/rest/confermaemail/`

**Method** : `PUT`

**Auth required** : NO

**Data constraints** : 

```json
{
    "email": "[String]",
    "hash": "[String]"
}
```

**Data example** All fields must be sent.

```json
{
    "email": "prova@prova.it",
    "hash": "dsvlafnvnuirnvrenvrevern"
}
```
## Success Responses

**Condition** : Correct information.

**Code** : `200 OK`

**Content** : `{}`
## Error Responses

**Condition** : If account don't exists.

**Code** : `404 NOT FOUND`

**Content** : `{}`

### Or

**Condition** : If the account has alredy been confirmed

**Code** : `498`

**Content** : `{}`
### Or

**Condition** : Server error

**Code** : `500 SERVER ERROR`

**Content** : `{}`
Provide name of Account to be created.
### Or

**Condition** : Validation error

**Code** : `400 SERVER ERROR`

**Content** : `{}`