---

copyright:
  years: 2017
lastupdated: "2017-09-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Visualizzazione delle chiavi

Puoi visualizzare i contenuti delle tue chiavi di crittografia con {{site.data.keyword.keymanagementservicefull}}.
{: shortdesc}

## Visualizzazione delle chiavi con la GUI 
{: #gui}

Per sfogliare le chiavi nel tuo servizio con la GUI {{site.data.keyword.keymanagementserviceshort}}, consulta
[Introduzione a {{site.data.keyword.keymanagementserviceshort}}](/docs/services/keymgmt/index.html#managekey). 

## Visualizzazione delle chiavi con l'API
{: #api}

Puoi richiamare i contenuti delle tue chiavi utilizzando l'API {{site.data.keyword.keymanagementserviceshort}}.

### Passo 1: Richiama una raccolta di chiavi
{: #retrieve_keys_api}

Per le viste avanzate, puoi scorrere le chiavi gestite nel tuo spazio effettuando una chiamata `GET` a seguente endpoint:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys
```
{: codeblock}

1. [Richiama il tuo token di autorizzazione, il GUID organizzazione e il GUID spazio per utilizzare le chiavi nel sevizio.](/docs/services/keymgmt/keyprotect_authentication.html)
2. Esegui il seguente comando cURL per visualizzare le caratteristiche generali delle chiavi. 

    ```cURL
    curl -X GET \
    https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <OAuth_token>' \
    -H 'bluemix-org: <organization_GUID>' \
    -H 'bluemix-space: <space_GUID>' \
    ```
    {: codeblock}

    Sostituisci le variabili nella richiesta di esempio in base alla seguente tabella.
    <table>
      <tr>
        <th>Variabile</th>
        <th>Descrizione</th>
      </tr>
      <tr>
        <td><em>OAuth_token</em></td>
        <td>Il tuo token di autorizzazione. Includi il contenuto completo del token, compreso il valore Bearer, nella richiesta cURL.</td>
      </tr>
      <tr>
        <td><em>space_GUID</em></td>
        <td>L'identificativo univoco che viene assegnato al tuo spazio {{site.data.keyword.Bluemix_notm}}.</td>
      </tr>
      <tr>
        <td><em>organization_GUID</em></td>
        <td>L'identificativo univoco che viene assegnato alla tua organizzazione {{site.data.keyword.Bluemix_notm}}.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabella 1. Descrive le variabili necessarie per visualizzare le chiavi tramite l'API {{site.data.keyword.keymanagementserviceshort}}.</caption>
    </table>

    Una richiesta con esito positivo restituisce una raccolta di chiavi disponibili nel tuo spazio {{site.data.keyword.Bluemix_notm}}.

    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.kms.key+json",
        "collectionTotal": 2
      },
    "resources": [
      {
          "id": "Key ID 1",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Key alias",
          "description": "Key description",
          "state": 1,
          "algorithmType": "AES",
          "createdBy": "v4 UUID of the user who creates the key",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "Key length",
            "mode": "GCM"
          }
        },
        {
          "id": "Key ID 2",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Key alias",
          "description": "Key description",
          "state": 1,
          "algorithmType": "AES",
          "createdBy": "v4 UUID of the user who creates the key",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "Key length",
            "mode": "GCM"
          }
        }
      ]
    }
    ```
    {:screen}

### Passo 2: Richiamo di una chiave per ID
{: #retrieve_key_api}

Per visualizzare le informazioni dettagliate su una chiave specifica, puoi effettuare una successiva chiamata `GET` al seguente endpoint:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID>
```
{: codeblock}

1. [Richiama il tuo token di autorizzazione, il GUID organizzazione e il GUID spazio per utilizzare le chiavi nel sevizio.](/docs/services/keymgmt/keyprotect_authentication.html)
2. Richiama l'ID della chiave che desideri gestire o a cui vuoi accedere. 

    Il valore ID viene utilizzato per accedere a informazioni dettagliate sulla chiave, come
il materiale della chiave stesso. Puoi richiamare l'ID di una chiave specifica effettuando una richiesta
`GET v2/keys` o accedendo alla GUI {{site.data.keyword.keymanagementserviceshort}}.

3. Esegui il seguente comando cURL per ottenere i dettagli sulla tua chiave e il materiale relativo.

    ```cURL
    curl -X GET \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID> \
      -H 'accept: application/vnd.ibm.kms.secret+json' \
      -H 'authorization: Bearer <OAuth_token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

    Sostituisci le variabili nella richiesta di esempio in base alla seguente tabella.

    <table>
      <tr>
        <th>Variabile</th>
        <th>Descrizione</th>
      </tr>
      <tr>
        <td><em>OAuth_token</em></td>
        <td>Il tuo token di autorizzazione. Includi il contenuto completo del token, compreso il valore Bearer, nella richiesta cURL.</td>
      </tr>
      <tr>
        <td><em>organization_GUID</em></td>
        <td>L'identificativo univoco che viene assegnato alla tua organizzazione {{site.data.keyword.Bluemix_notm}}.</td>
      </tr>
      <tr>
        <td><em>space_GUID</em></td>
        <td>L'identificativo univoco che viene assegnato al tuo spazio {{site.data.keyword.Bluemix_notm}}.</td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>Facoltativo: l'identificativo univoco utilizzato per tracciare e correlare le transazioni.</td>
      </tr>
      <tr>
        <td><em>key_ID</em></td>
        <td>L'identificativo della chiave che hai richiamato nel [passo 1](#retrieve_keys_api).</td>
      </tr>
      <caption style="caption-side:bottom;">Tabella 2. Descrive le variabili necessarie per visualizzare una chiave specificata tramite l'API {{site.data.keyword.keymanagementserviceshort}}.</caption>
    </table>

    Una risposta con esito positivo restituisce i dettagli sulla tua chiave e il materiale della chiave.  Il seguente oggetto JSON mostra un valore restituito di esempio.

    ```
    {
        "metadata": {
            "collectionTotal": 1,
            "collectionType": "application/vnd.ibm.kms.key+json"
        },
    "resources": [
      {
                "createdBy": "...",
                "creationDate": "...",
                "id": "...",
                "name": "...",
                "payload": "...",
                "state": 1,
                "type": "application/vnd.ibm.kms.key+json"
            }
        ]
    }
    ```
    {:screen}

    Per una descrizione dettagliata dei parametri disponibili, consulta
{{site.data.keyword.keymanagementserviceshort}} [REST API reference doc ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
