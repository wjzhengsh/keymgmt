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

# Creazione di chiavi

Puoi gestire il ciclo di vita delle tue chiavi utilizzando {{site.data.keyword.keymanagementservicefull}}.
{: shortdesc}

Ti si consiglia di gestire le tue chiavi in modo sicuro mentre sviluppi il tuo codice. Ad esempio, valuta
le seguenti linee guida, con le altre prassi di codifica sicura. 

- Considera le implicazioni per la sicurezza quando integri le chiavi nel tuo codice.
- Crea le chiavi solo per l'accesso programmatico alle tue applicazioni e risorse. Non creare chiavi quando puoi concedere delle [autorizzazioni utente più semplici ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")](https://console.bluemix.net/docs/admin/patterns.html#userroles){: new_window}.
- Esegui una rotazione delle chiavi e rimuovi le chiavi non utilizzate.
- Utilizza l'autenticazione a più fattori per le operazioni sensibili.
- Isola le applicazioni disponendo di chiavi separate per ciascuna applicazione.
- Considera di utilizzare l'API programmatica quando trasferisci un elevato numero di informazioni sensibili.

Se vuoi provare il servizio prima di aggiungere le tue chiavi, controlla l'[applicazione di esempio ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}

## Creazione delle chiavi con la GUI
{: #gui}

Per aggiungere le chiavi al tuo servizio con la GUI {{site.data.keyword.keymanagementserviceshort}}, consulta
[Introduzione a {{site.data.keyword.keymanagementserviceshort}}](/docs/services/keymgmt/index.html#addkey).

## Creazione delle chiavi con l'API
{: #api}

Puoi utilizzare l'API {{site.data.keyword.keymanagementserviceshort}} per proteggere le chiavi esistenti
o per generare nuove chiavi in modo programmatico. 

Crea nuove chiavi o importane di esistenti effettuando una chiamata `POST` al seguente
endpoint: 

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys
```
{: codeblock}

1. [Richiama il tuo token di autorizzazione, il GUID organizzazione e il GUID spazio per utilizzare le chiavi nel sevizio](/docs/services/keymgmt/keyprotect_authentication.html).

2. Chiama l'[{{site.data.keyword.keymanagementserviceshort}}API](https://console.ng.bluemix.net/apidocs/639) con il seguente comando cURL.

    ```cURL
    curl -X POST \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
      -H 'authorization: Bearer <OAuth_token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
      -H 'content-type: application/vnd.ibm.kms.key+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
     "metadata": {
       "collectionType": "application/vnd.ibm.kms.key+json",
       "collectionTotal": 1
     },
    "resources": [
      {
       "type": "application/vnd.ibm.kms.key+json",
       "name": "<key_alias>",
       "description": "<key_description>",
       "expirationDate": "<YYYY-MM-DDTHH:MM:SS.SSZ>",
       "payload": "<key_material>"
       }
     ]
    }'
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
        <td>L'identificativo univoco che viene assegnato alla tua organizzazione {{site.data.keyword.Bluemix_notm}}. </td>
      </tr>
      <tr>
        <td><em>space_GUID</em></td>
        <td>L'identificativo univoco che viene assegnato al tuo spazio {{site.data.keyword.Bluemix_notm}}. </td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>L'identificativo univoco utilizzato per tracciare e correlare le transazioni. </td>
      </tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p>Un'intestazione che modifica il comportamento del server per le operazioni <code>POST</code> e <code>DELETE</code>.</p><p>Se impostata su <code>return=minimal</code>, il servizio restituisce solo i metadati della chiave, come il valore <code>id</code> e nome, nel corpo-entità della risposta. Se impostata su <code>return=representation</code>, il servizio restituisce i metadati e il materiale della chiave.</p></td>
      </tr>
      <tr>
        <td><em>key_alias</em></td>
        <td>Un nome leggibile dall'utente per una facile identificazione della tua chiave.</td>
      </tr>
      <tr>
        <td><em>key_description</em></td>
        <td>Una descrizione estesa della tua chiave.</td>
      </tr>
      <tr>
        <td><em>YYYY-MM-DD</em><br><em>HH:MM:SS.SS</em></td>
        <td>Facoltativo: la data e l'ora di scadenza della chiave nel sistema, nel formato RFC 3339. Se l'attributo
<code>expirationDate</code> viene omesso, la chiave non avrà scadenza. </td>
      </tr>
      <tr>
        <td><em>key_material</em></td>
        <td>Il materiale della chiave, come ad esempio la chiave RSA, che desideri archiviare in {{site.data.keyword.keymanagementserviceshort}}. Per generare una nuova chiave, ometti l'attributo
<code>payload</code> e la variabile <em>key_material</em>.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabella 1. Variabili necessarie per aggiungere le chiavi tramite l'API {{site.data.keyword.keymanagementserviceshort}}</caption>
    </table>

    Una risposta positiva restituisce il valore `id` per la tua chiave, insieme ad altri metadati. L'`id` è un identificativo univoco che viene assegnato alla tua chiave e utilizzato per le seguenti chiamate.

3. **Facoltativo:** verifica che la chiave sia stata creata eseguendo la seguente chiamata per ottenere le chiavi nel tuo spazio {{site.data.keyword.Bluemix_notm}}.

    ```cURL
    curl -X GET \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <OAuth-token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
    ```
    {: codeblock}

### Operazioni successive

Ora puoi utilizzare le chiavi per crittografare i tuoi servizi e le tue applicazioni. 

- Per i dettagli completi di ogni richiesta e risposta REST, consulta
{{site.data.keyword.keymanagementserviceshort}} [REST API reference doc
![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
