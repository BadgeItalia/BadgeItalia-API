# Documentazione API per app.badgeitalia.it

Questa documentazione è in riferimento alle api offerte per la visualizzazione generale dei dati, da utilizzarsi esclusivamente nelle pagine di front-end. Non hanno nulla a che vedere con le api di servizio esposte per i singoli issuer e non permettono di operare direttamente con la piattaforma.

### Operazioni possibili tramite queste api
 - Ottenimento id di tutti gli gli issuer (sconsigliata)
 - Ottenimento dei dati completi di tutti gli issuer (consigliata)
 - Lista badge per singolo issuer
 - Dettagli singolo badge
 - Lista di tutti i badge rilasciati dalla piattaforma

## Ottenimento id di tutti issuer
Da utilizzarsi nel caso si voglia ottenere un array contenente tutti gli issuer id (ossia gli id di tutti gli enti registrati alla piattaforma)

**URL** : `/api/issuerlist/`

**Method** : `GET`

**Auth required** : YES (token in header)


**Esempio richiesta**

```bash
curl --location --request GET 'app.badgeitalia.it/api/issuerlist' \
--header 'token: VALORE_TOKEN_SEGRETO'
```

### Esempio di risposta per chiamata corretta

**Code** : `200 OK`

**Content example**

```json
[
    "614dde8efbf7b7a8551a3bfd",
    "615332714ab7e64a24d1940d"
]
```

### Esempio errore risposta

**Condition** : Se non viene specificato un token valido

**Code** : `400 Bad Request`

**Content** :

```json
{
    "status": false,
    "message": "Non sei autorizzato"
}
```

## Ottenimento dei dati completi di tutti gli issuer
Da utilizzarsi nel caso si voglia ottenere un array contenente tutti gli issuer compresi dei loro specifici dati (ossia i dati di tutti gli enti registrati alla piattaforma)

**URL** : `/api/issuers/`

**Method** : `GET`

**Auth required** : YES (token in header)


**Esempio richiesta**

```bash
curl --location --request GET 'app.badgeitalia.it/api/issuers' \
--header 'token: VALORE_TOKEN_SEGRETO'
```

### Esempio di risposta per chiamata corretta

**Code** : `200 OK`

**Content example**

```json
[
    {
        "@context": "https://w3id.org/openbadges/v2",
        "type": "Issuer",
        "id": "https://app.badgeitalia.it/open/issuer/614dde8efbf7b7a8551a3bfd.json",
        "name": "Scuola Innovativa srl",
        "image": "https://scuolainnovativa.com/wp-content/uploads/2021/09/cropped-cropped-logo-scuol-ainnovativa.png",
        "url": "https://scuolainnovativa.com",
        "email": "info@scuolainnovativa.com",
        "description": "Testo descrittivo ente"
    },
    {
        "@context": "https://w3id.org/openbadges/v2",
        "type": "Issuer",
        "id": "https://app.badgeitalia.it/open/issuer/615332714ab7e64a24d1940d.json",
        "name": "A-Sapiens",
        "image": "https://asapiens.eu/wp-content/uploads/2019/05/Risorsa-1-3.png",
        "url": "https://asapiens.eu",
        "email": "info@asapiens.eu",
        "description": "Testo descrittivo ente"
    }
]
```

### Esempio errore risposta

**Condition** : Se non viene specificato un token valido

**Code** : `400 Bad Request`

**Content** :

```json
{
    "status": false,
    "message": "Non sei autorizzato"
}
```
## Lista badge per singolo issuer
Da utilizzarsi nel caso si voglia ottenere un array contenente tutti i badge di un singolo issuer

**URL** : `/api/badgelist/ID_ISSUER`

**Method** : `GET`

**Auth required** : YES (token in header)


**Esempio richiesta**

```bash
curl --location --request GET 'app.badgeitalia.it/api/badgelist/614dde8efbf7b7a8551a3bfd' \
--header 'token: VALORE_TOKEN_SEGRETO'
```

### Esempio di risposta per chiamata corretta

**Code** : `200 OK`

**Content example**

```json
[
    {
        "idBadge": "614de0732ff6240012dc8d36",
        "rilasciati": 5,
        "annullati": 4,
        "badgeClass": {
            "@context": "https://w3id.org/openbadges/v2",
            "type": "BadgeClass",
            "id": "https://app.badgeitalia.it/open/badge/614de0732ff6240012dc8d36.json",
            "name": "Badge di test",
            "description": "Questo badge serve a controllare la corretta emissione e verifica",
            "image": "https://scopenbadges-file.fra1.digitaloceanspaces.com/image-1632493683123-773620146.png",
            "criteria": {
                "id": "https://badgeitalia.it",
                "narrative": "Nulla di particolare, è unicamente una questione di testing"
            },
            "tags": [
                "test"
            ],
            "issuer": "https://app.badgeitalia.it/open/issuer/614dde8efbf7b7a8551a3bfd.json"
        }
    }
]
```

### Esempio errore risposta

**Condition** : Se non viene specificato un token valido

**Code** : `400 Bad Request`

**Content** :

```json
{
    "status": false,
    "message": "Non sei autorizzato"
}
```

## Dettagli singolo badge
Da utilizzarsi nel caso si vogliano ottenere i dettagli di un singolo badge

**URL** : `/api/singolobadge/ID_BADGE`

**Method** : `GET`

**Auth required** : YES (token in header)


**Esempio richiesta**

```bash
curl --location --request GET 'app.badgeitalia.it/api/singolobadge/614de0732ff6240012dc8d36' \
--header 'token: VALORE_TOKEN_SEGRETO'
```

### Esempio di risposta per chiamata corretta

**Code** : `200 OK`

**Content example**

```json
{
    "idBadge": "614de0732ff6240012dc8d36",
    "rilasciati": 5,
    "annullati": 4,
    "badgeClass": {
        "@context": "https://w3id.org/openbadges/v2",
        "type": "BadgeClass",
        "id": "https://app.badgeitalia.it/open/badge/614de0732ff6240012dc8d36.json",
        "name": "Badge di test",
        "description": "Questo badge serve a controllare la corretta emissione e verifica",
        "image": "https://scopenbadges-file.fra1.digitaloceanspaces.com/image-1632493683123-773620146.png",
        "criteria": {
            "id": "https://badgeitalia.it",
            "narrative": "Nulla di particolare, è unicamente una questione di testing"
        },
        "tags": [
            "test"
        ],
        "issuer": "https://app.badgeitalia.it/open/issuer/614dde8efbf7b7a8551a3bfd.json"
    }
}
```

### Esempio errore risposta

**Condition** : Se non viene specificato un token valido

**Code** : `400 Bad Request`

**Content** :

```json
{
    "status": false,
    "message": "Non sei autorizzato"
}
```
## Lista di tutti i badge rilasciati dalla piattaforma
Da utilizzarsi nel caso si voglia ottenere un array contenente una lista di tutti i badge, per tutti gli issuer

**URL** : `/api/badgelist`

**Method** : `GET`

**Auth required** : YES (token in header)


**Esempio richiesta**

```bash
curl --location --request GET 'app.badgeitalia.it/api/badgelist' \
--header 'token: VALORE_TOKEN_SEGRETO'
```

### Esempio di risposta per chiamata corretta

**Code** : `200 OK`

**Content example**

```json
[
    {
        "idBadge": "614de0732ff6240012dc8d36",
        "rilasciati": 5,
        "annullati": 4,
        "badgeClass": {
            "@context": "https://w3id.org/openbadges/v2",
            "type": "BadgeClass",
            "id": "https://app.badgeitalia.it/open/badge/614de0732ff6240012dc8d36.json",
            "name": "Badge di test",
            "description": "Questo badge serve a controllare la corretta emissione e verifica",
            "image": "https://scopenbadges-file.fra1.digitaloceanspaces.com/image-1632493683123-773620146.png",
            "criteria": {
                "id": "https://badgeitalia.it",
                "narrative": "Nulla di particolare, è unicamente una questione di testing"
            },
            "tags": [
                "test"
            ],
            "issuer": "https://app.badgeitalia.it/open/issuer/614dde8efbf7b7a8551a3bfd.json"
        }
    },
    {
        "idBadge": "615c1a5d324b6f0011dca9f7",
        "rilasciati": 0,
        "annullati": 0,
        "badgeClass": {
            "@context": "https://w3id.org/openbadges/v2",
            "type": "BadgeClass",
            "id": "https://app.badgeitalia.it/open/badge/615c1a5d324b6f0011dca9f7.json",
            "name": "Modulo A RSPP",
            "description": "Corso di formazione RSPP Modulo A. Corso in e-learning della durata di 28 ore.\r\nLa fruizione dell’intero corso avviene per via telematica mediante qualsiasi dispositivo dotato di web browser e con un accesso alla rete internet. Il partecipante trova disponibili in streaming indiretto tutte le lezioni con commento audio e può accedere ad attività di varia natura che ne formano l’apprendimento e ne consolidano i concetti. Prima di poter passare ad un’attività successiva è necessario aver svolto quella precedente: aver quindi visionato una lezione o superato con almeno la sufficienza uno dei quiz di consolidamento delle conoscenze.",
            "image": "https://scopenbadges-file.fra1.digitaloceanspaces.com/image-1633426013110-264477921.png",
            "criteria": {
                "id": "https://asapiens.eu/projects/rspp-modulo-a-elearning/",
                "narrative": "Il badge viene assegnato al completamento del corso. Per completare il corso è necessario aver visionato per intero il materiale didattico avendo raggiunto il monte ore previsto dalla normativa, è inoltre necessario superare tutte le verifiche intermedie e una verifica finale al fine di ottenere il badge."
            },
            "tags": [
                "elearning",
                "sicurezza",
                "81/08",
                "rspp",
                "modulo a",
                "dlgs 81/08"
            ],
            "issuer": "https://app.badgeitalia.it/open/issuer/615332714ab7e64a24d1940d.json"
        }
    },
    {
        "idBadge": "615c1c42324b6f0011dca9f8",
        "rilasciati": 0,
        "annullati": 0,
        "badgeClass": {
            "@context": "https://w3id.org/openbadges/v2",
            "type": "BadgeClass",
            "id": "https://app.badgeitalia.it/open/badge/615c1c42324b6f0011dca9f8.json",
            "name": "Modulo B RSPP",
            "description": "Corso in videoconferenza da 48H.  Il modulo B è comune per il corso di ASPP e RSPP e contiene i seguenti obbiettivi generali: acquisire conoscenze relative ai fattori di rischio e alle misure di prevenzione e protezione presenti negli specifici comparti,; acquisire capacità di analisi per individuare i pericoli e quantificare i rischi presenti negli ambienti di lavoro del comparto; contribuire alla individuazione de adeguate soluzioni tecniche organizzative e procedurali di sicurezza per ogni tipologia di rischio,; contribuire ad individuare per le diverse lavorazioni del comparto, gli idonei dispositivi di protezione individuali-DPI; contribuire ad individuare i fattori di rischio per i quali è prevista la sorveglianza sanitaria.",
            "image": "https://scopenbadges-file.fra1.digitaloceanspaces.com/image-1633426498864-825844697.png",
            "criteria": {
                "id": "https://asapiens.eu/projects/rspp-modulo-b-videoconferenza/",
                "narrative": "Il badge viene assegnato se il partecipante partecipa almeno al 90% delle lezioni e se supera con successo una verifica scritta."
            },
            "tags": [
                "videoconferenza",
                "sicurezza",
                "81/08",
                "rspp",
                "modulo b",
                "dlgs 81/08"
            ],
            "issuer": "https://app.badgeitalia.it/open/issuer/615332714ab7e64a24d1940d.json"
        }
    }
]
```

### Esempio errore risposta

**Condition** : Se non viene specificato un token valido

**Code** : `400 Bad Request`

**Content** :

```json
{
    "status": false,
    "message": "Non sei autorizzato"
}
```
