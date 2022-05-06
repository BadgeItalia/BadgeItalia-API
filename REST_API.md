![logo_transparent_background](https://user-images.githubusercontent.com/15046219/167154553-9da0758f-c419-496c-a6e5-5c3c46169232.png)

# Documentazione API per l'integrazione della piattaforma app.badgeitalia.it
![image](https://user-images.githubusercontent.com/15046219/166956263-a189f454-bd60-4de8-b947-5265875ad8ba.png)

Questa documentazione è in riferimento alle api offerte dalla piattaforma per lo svolgimento delle seguenti attività:
- [Creazione di un badge](#creazione-di-una-nuova-tipologia-di-badge)
- [Rilascio di un badge](#rilascio-di-un-badge-ad-un-utente)
- [Annullamento di un badge](#annullamento-di-un-badge-rilasciato-ad-un-utente)
- [Elenco badge rilasciabili](#ottenimento-lista-badge-rilasciabili)
- [Dettaglio singolo badge rilasciabile](#ottenimento-singolo-badge-rilasciabile)
- [Elenco badge rilasciati](#ottenimento-lista-badge-rilasciati)
- [Dettaglio singolo badge rilasciato](#ottenimento-dettaglio-singolo-badge-rilasciato)
- Creazione curatori [coming soon]
- Modifica curatori [coming soon]

### Procedura di autenticazione:
Per utilizzare queste api è necessario avere un token di autenticazione. Le api utilizzato un [token](#procedura-di-autenticazione) di tipo *jwt* che va incluso all'interno dell'header di ogni singola chiamata mediante il valore `x-access-token`. In alterativa a questo token può essere usata una chiave API reperibile e revocabile all'interno del proprio pannello di controllo. Nel caso di utilizzo della chiave API invece del valore `x-access-token` all'interno dell'header sarà necessario specificare il valore `api-token`.

### Parole chiave:
- Badge (rappresenta il badge rilasciabile agli utenti)
- Assertion (rappresenta il rilascio di un badge ad un utente)

### HOST di chiamata:
 `https://app.badgeitalia.it`

## Come ottenere il token di autenticazione:

**URL** : `/apiv1/token/`

**Method** : `POST`

**Esempio richiesta curl**
```bash
curl --location --request POST '/apiv1/token' \
--form 'email="valid@email.com"' \
--form 'password="user_password"'
```

### Risposta per chiamata corretta:

**Code** : `200 OK`

**Content example**

```json
{
    "x-access-token":"valore-token",
    "expires":"data-scadenza-token"
}
```

### Eventuale risposta di errore:

**Condition** : Se non vengono specificate credenziali valide

**Code** : `400 Bad Request`

**Content** :

```json
{
    "status": false,
    "message": "Messaggio di errore:"
}
```

## Creazione di una nuova tipologia di badge:

**URL** : `/apiv1/badge/`

**Method** : `POST`


**Esempio richiesta curl**
```bash
curl --location --request POST '/apiv1/badge' \
--header 'x-access-token: valoretoken' \
--form 'nome="nome del badge"' \
--form 'descrizione="descrizione della tipologia di achivement rappresentata da questo badge"' \
--form 'url="url descrizione criteri"' \
--form 'tags="[tag1,tag2]"' \
--form 'immagine=@"/path/to/file"'
```

### Risposta per chiamata corretta:

**Code** : `200 OK`

**Content example**

```json
{
    "id-badge":"id_univoco_badge_creato"
}
```

### Eventuale risposta di errore:

**Condition** : Token non valido, errore dati

**Code** : `400 Bad Request`

**Content** :

```json
{
    "status": false,
    "message": "Messaggio di errore:"
}
```
## Rilascio di un badge ad un utente:

**URL** : `/apiv1/assertion/`

**Method** : `POST`


**Esempio richiesta curl**
```bash
curl --location --request POST '/apiv1/assertion' \
--header 'x-access-token: valoretoken' \
--form 'id-badge="id_univoco_badge_creato"' \
--form 'nominativo="nominativo_destinatario"' \
--form 'email="email_destinatario"' \
--form 'scadenza="GG/MM/AAAA"' \
--form 'allegato=@"/path/to/file"'
```
`scadenza` e `allegato` sono campi opzionali

### Risposta per chiamata corretta:

**Code** : `200 OK`

**Content example**

```json
{
    "id-assertion":"id_univoco_assertion_generata"
}
```

### Eventuale risposta di errore:

**Condition** : Token non valido, errore dati

**Code** : `400 Bad Request`

**Content** :

```json
{
    "status": false,
    "message": "Messaggio di errore:"
}
```
## Annullamento di un badge rilasciato ad un utente:

**URL** : `/apiv1/assertion/`

**Method** : `DELETE`


**Esempio richiesta curl**
```bash
curl --location --request DELETE '/apiv1/assertion' \
--header 'x-access-token: valoretoken' \
--form 'id-assertion="id_univoco_assertion_generata"'
```

### Risposta per chiamata corretta:

**Code** : `200 OK`

**Content example**

```json
{
    "id-assertion":"id_univoco_assertion_generata"
}
```

### Eventuale risposta di errore:

**Condition** : Token non valido, errore dati

**Code** : `400 Bad Request`

**Content** :

```json
{
    "status": false,
    "message": "Messaggio di errore:"
}
```
## Ottenimento lista badge rilasciabili:

**URL** : `/apiv1/badge/`

**Method** : `GET`


**Esempio richiesta curl**
```bash
curl --location --request GET '/apiv1/badge' \
--header 'x-access-token: valoretoken'
```

### Risposta per chiamata corretta:

**Code** : `200 OK`

**Content example**

```json
[
    {
    "id-badge":"id-badge1",
    "nome":"nome del badge",
    "descrizione":"descrizione del badge",
    "url":"url",
    "tags":["tag1","tag2"],
    "immagine":"https://urlimmagine.png"
    },
    {
    "id-badge":"id-badge2",
    "nome":"nome del badge",
    "descrizione":"descrizione del badge",
    "url":"url",
    "tags":["tag1","tag2"],
    "immagine":"https://urlimmagine.png"
    }
]
```

### Eventuale risposta di errore:

**Condition** : Token non valido

**Code** : `400 Bad Request`

**Content** :

```json
{
    "status": false,
    "message": "Messaggio di errore:"
}
```
## Ottenimento singolo badge rilasciabile:

**URL** : `/apiv1/badge/:idbadge`

**Method** : `GET`


**Esempio richiesta curl**
```bash
curl --location --request GET '/apiv1/badge/id-badge1' \
--header 'x-access-token: valoretoken'
```

### Risposta per chiamata corretta:

**Code** : `200 OK`

**Content example**

```json
{
    "id-badge":"id-badge1",
    "nome":"nome del badge",
    "descrizione":"descrizione del badge",
    "url":"url",
    "tags":["tag1","tag2"],
    "immagine":"https://urlimmagine.png"
}
```

### Eventuale risposta di errore:

**Condition** : Token non valido, id badge non valido

**Code** : `400 Bad Request`

**Content** :

```json
{
    "status": false,
    "message": "Messaggio di errore:"
}
```
## Ottenimento lista badge rilasciati:

**URL** : `/apiv1/assertion`

**Method** : `GET`


**Esempio richiesta curl**
```bash
curl --location --request GET '/apiv1/assertion' \
--header 'x-access-token: valoretoken'
```

### Risposta per chiamata corretta:

**Code** : `200 OK`

**Content example**

```json
[
    {
       "id-badge":"id-badge-1",
       "id-assertion":"id-assertion-1",
       "nominativo":"nominativo",
       "email":"email",
       "scadenza":"GG/MM/AAAA",
       "allegato":"https://urlallegato.pdf" 
    },
    {
       "id-badge":"id-badge-1",
       "id-assertion":"id-assertion-2",
       "nominativo":"nominativo",
       "email":"email",
       "scadenza":"GG/MM/AAAA",
       "allegato":"https://urlallegato.pdf" 
    }
]
```
`scadenza` e `allegato` disponibili solo se creati durante il rilascio del badge

### Eventuale risposta di errore:

**Condition** : Token non valido

**Code** : `400 Bad Request`

**Content** :

```json
{
    "status": false,
    "message": "Messaggio di errore:"
}
```
## Ottenimento dettaglio singolo badge rilasciato:

**URL** : `/apiv1/assertion/:id-assertion`

**Method** : `GET`


**Esempio richiesta curl**
```bash
curl --location --request GET '/apiv1/assertion/id-assertion1' \
--header 'x-access-token: valoretoken'
```

### Risposta per chiamata corretta:

**Code** : `200 OK`

**Content example**

```json
{
       "id-badge":"id-badge-1",
       "id-assertion":"id-assertion-1",
       "nominativo":"nominativo",
       "email":"email",
       "scadenza":"GG/MM/AAAA",
       "allegato":"https://urlallegato.pdf" 
}
```
`scadenza` e `allegato` disponibili solo se creati durante il rilascio del badge

### Eventuale risposta di errore:

**Condition** : Token non valido, id-assertion errata

**Code** : `400 Bad Request`

**Content** :

```json
{
    "status": false,
    "message": "Messaggio di errore:"
}
```
