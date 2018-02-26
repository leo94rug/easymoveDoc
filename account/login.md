# Login


Allows the user to log in, also returns the token needed to make other calls

**URL** : `/rest/login/`

**Method** : `POST`

**Auth required** : NO

**Data constraints** :

```json
{
    "email": "[String]",
    "password": "[String]"
}
```

**Data example** All fields must be sent.

```json
{
    "email": "prova@prova.it",
    "password": "secret"
}
```
## Success Responses

**Condition** : Correct information.

**Code** : `200 OK`

**Content** : 
```json
{
    "token": "eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1c2Vycy9Uek1Vb2NNRjRwIiwiZXhwIjoxNTIyMDQ5MTYyLCJpZCI6IjYyMDRhY2FhLTE4NTQtNDBjNC04Njg4LWIyMWQ1NjFkNWYwOCJ9.g7TLotkdP9irww7XBIIbZBX6QWzFfDOGHB1ViQXQZj0",
    "eta": 24,
    "email": "leo94rug@gmail.com",
    "nome": "Leonardo",
    "cognome": "Secondo",
    "anno_nascita": "1994-01-25 00:00:00",
    "professione": "Studente",
    "telefono1": "3246905278",
    "telefono2": "3246905278",
    "biografia": "L'utente non ha ancora inserito una biografia",
    "foto_utente": "https://www.dropbox.com/s/ht1ik2uygkjea3u/profile?raw=1",
    "image_path": "/immagine-profilo/profile",
    "sesso": "male",
    "fumare": 0,
    "animali": 0,
    "tipo": 1,
    "media_feedback": 0
}
```
## Error Responses

**Condition** : If account don't exists.

**Code** : `404 NOT FOUND`

**Content** : `{}`

### Or

**Condition** : If the account has not been confirmed

**Code** : `499`

**Content** : `{}`
### Or

**Condition** : Server error

**Code** : `500 SERVER ERROR`

**Content** : `{}`