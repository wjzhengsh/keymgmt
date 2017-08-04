---

copyright:
  years: 2017
lastupdated: "2017-08-03"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Gestione delle chiavi

Puoi gestire il ciclo di vita delle tue chiavi utilizzando
{{site.data.keyword.keymanagementservicelong}} per {{site.data.keyword.Bluemix_short}}.
{: shortdesc}

Ti si consiglia di gestire le tue chiavi in modo sicuro mentre sviluppi il tuo codice. Ad esempio, valuta
i seguenti tipi di linee guida, con le altre prassi di codifica sicura.

- Considera le implicazioni per la sicurezza quando integri le chiavi nel tuo codice.
- Crea le chiavi solo per l'accesso programmatico alle tue applicazioni e risorse. Non creare chiavi quando puoi concedere delle [autorizzazioni utente più semplici ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")](https://console.bluemix.net/docs/admin/patterns.html#userroles "Icona di link esterno"){: new_window}.
- Esegui una rotazione delle chiavi e rimuovi le chiavi non utilizzate.
- Utilizza l'autenticazione a più fattori per le operazioni sensibili.
- Isola le applicazioni disponendo di chiavi separate per ciascuna applicazione.
- Considera di utilizzare l'API programmatica quando trasferisci un elevato numero di informazioni sensibili.

## Generazione delle credenziali di autenticazione per l'API {{site.data.keyword.keymanagementserviceshort}}
{: #authentication_api}

{{site.data.keyword.keymanagementservicelong_notm}} fornisce un'API REST
che può essere utilizzata con qualsiasi linguaggio di programmazione per archiviare, richiamare e generare le chiavi.

Per utilizzare l'API, devi generare le tue credenziali del servizio e di autenticazione.

1. Accedi a {{site.data.keyword.Bluemix_notm}} con la CLI Cloud
Foundry.

    ```
    cf login [a api.DomainName] [-sso]
    ```
    {: codeblock}

2. Seleziona l'organizzazione e lo spazio {{site.data.keyword.Bluemix_notm}} che contengono la tua istanza del servizio Key Protect.
    Prendi nota dei nomi dei tuoi spazio e organizzazione nell'output della CLI. Puoi anche eseguire `cf
target` per visualizzare queste informazioni.
3. Richiama i tuoi GUID dell'organizzazione e dello spazio {{site.data.keyword.Bluemix_notm}}.

    ```
    cf org organization_name --guid
    cf space space_name --guid
    ```
    {: codeblock}

4. Richiesta di un token di accesso {{site.data.keyword.Bluemix_notm}}.

    ```
    cf oauth-token
    ```
    {: codeblock}

    Il seguente esempio troncato mostra l'output del token {{site.data.keyword.Bluemix_notm}}. La variabile _bearer
mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7_ è un esempio di token di accesso.

    ```
    bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7...
    ```
    {: screen}

Operazioni successive:

Consulta il {{site.data.keyword.keymanagementserviceshort}} [documento di riferimento dell'API REST ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")](https://console.ng.bluemix.net/apidocs/639 "Icona di link esterno"){: new_window} per iniziare a gestire le chiavi nel tuo spazio.


## Creazione delle chiavi con l'API {{site.data.keyword.keymanagementserviceshort}}
{: #codingapps}

Puoi utilizzare l'API {{site.data.keyword.keymanagementservicelong_notm}} per proteggere le chiavi esistenti
o per generare nuove chiavi.

Crea nuove chiavi o aggiungine di esistenti effettuando una chiamata **POST** al seguente
endpoint:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/secrets
```
{: codeblock}

Se vuoi provare il servizio prima di aggiungere le tue chiavi, controlla l'[applicazione di esempio ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")](https://github.com/IBM-Bluemix/key-protect-helloworld-python "Icona di link esterno"){: new_window}.

1. [Richiama il tuo token di accesso {{site.data.keyword.Bluemix_notm}}, il GUID organizzazione e il GUID spazio per utilizzare le chiavi nel servizio](#authentication_api).

2. Chiama l'[{{site.data.keyword.keymanagementserviceshort}}API](https://console.ng.bluemix.net/apidocs/639) con il seguente comando cURL.

  ```cURL
  curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: bluemix_access_token' --header 'Bluemix-Space: space_GUID' --header 'Bluemix-Org: organization_GUID' -d '{
    "metadata": {
      "collectionType": "application/vnd.ibm.kms.secret+json",
      "collectionTotal": 1
    },
    "resources": [
      {
      "type": "application/vnd.ibm.kms.secret+json",
      "name": "key_alias",
      "description": "key_description",
      "expirationDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
      "payload": "key_contents"
      }
    ]
  }' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets'
  ```
  {: codeblock}

  Sostituisci le variabili nella richiesta di esempio in base alla seguente tabella.
  <table>
    <tr>
      <th>Variabile</th>
      <th>Descrizione</th>
    </tr>
    <tr>
      <td><em>bluemix_access_token</em></td>
      <td>Il tuo token di autorizzazione. Includi il contenuto completo del token, compreso il valore Bearer, nella richiesta cURL.</td>
    </tr>
    <tr>
      <td><em>space_GUID</em></td>
      <td>L'identificativo per il tuo spazio {{site.data.keyword.Bluemix_notm}}.</td>
    </tr>
    <tr>
      <td><em>organization_GUID</em></td>
      <td>L'identificativo per la tua organizzazione {{site.data.keyword.Bluemix_notm}}. </td>
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
      <td>Facoltativo: la data e l'ora di scadenza della chiave nel sistema, nel formato RFC3339. Se l'attributo
<code>expirationDate</code> viene omesso, la chiave non avrà scadenza. </td>
    </tr>
    <tr>
      <td><em>key_contents</em></td>
      <td>Il materiale della chiave, come ad esempio la chiave RSA, che desideri archiviare in {{site.data.keyword.keymanagementserviceshort}}. Per generare una nuova chiave, ometti l'attributo payload e la variabile key_contents.</td>
    </tr>
      <caption style="caption-side:bottom;">Tabella 1. Variabili necessarie per aggiungere le chiavi tramite l'API {{site.data.keyword.keymanagementserviceshort}}</caption>
  </table>

3. Verifica che la chiave sia stata creata eseguendo la seguente chiamata per ottenere le chiavi nel tuo spazio {{site.data.keyword.Bluemix_notm}}.

  ```cURL
  curl -X GET --header 'Accept: application/json' --header 'Authorization: bluemix_access_token' --header 'Bluemix-Space: space_GUID' --header 'Bluemix-Org: organization_GUID' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets'
  ```
  {: codeblock}

## Visualizzazione delle chiavi con l'API {{site.data.keyword.keymanagementserviceshort}}
{: #viewingkeys_api}

Puoi visualizzare
i contenuti delle tue chiavi tramite l'API {{site.data.keyword.keymanagementservicelong_notm}},
se sei uno sviluppatore o un gestore dello spazio {{site.data.keyword.Bluemix_notm}}.

Per le viste avanzate, puoi scorrere le chiavi gestite nel tuo spazio tramite la IU
{{site.data.keyword.keymanagementserviceshort}}.

Visualizza le informazioni dettagliate sulle tue chiavi effettuando una chiamata GET al seguente endpoint:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/secrets/key_ID
```
{: codeblock}

1. Dall'IU {{site.data.keyword.keymanagementserviceshort}}, nei servizi di sicurezza, puoi visualizzare le caratteristiche generali delle tue chiavi. Puoi esplorare le chiavi facendo clic sulle intestazioni di colonna ordinabili.
2. Copiare l'**ID** nella riga della chiave. Il valore ID viene utilizzato per accedere ad ulteriori informazioni dettagliate sulla chiave nell'API, come
il materiale della chiave stesso.
3. [Richiama il tuo token di accesso {{site.data.keyword.Bluemix_notm}},
il GUID organizzazione e il GUID spazio per utilizzare le chiavi nel servizio. ](#authentication_api)
4. Esegui il seguente comando cURL per ottenere i dettagli sulla tua chiave e il materiale relativo.

  ```cURL
  curl -X GET --header 'Accept: application/json' --header 'Authorization: bluemix_access_token' --header 'Bluemix-Space: space_GUID' --header 'Bluemix-Org: organization_GUID' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets/key_ID'
  ```
  {: codeblock}

  Sostituisci le variabili nella richiesta di esempio in base alla seguente tabella.
  <table>
    <tr>
      <th>Variabile</th>
      <th>Descrizione</th>
    </tr>
    <tr>
      <td><em>bluemix_access_token</em></td>
      <td>Il tuo token di autorizzazione. Includi il contenuto completo del token, compreso il valore Bearer, nella richiesta cURL.</td>
    </tr>
    <tr>
      <td><em>space_GUID</em></td>
      <td>L'identificativo generato casualmente che viene assegnato al tuo spazio {{site.data.keyword.Bluemix_notm}}.</td>
    </tr>
    <tr>
      <td><em>organization_GUID</em></td>
      <td>L'identificativo generato casualmente che viene assegnato alla tua organizzazione {{site.data.keyword.Bluemix_notm}}.</td>
    </tr>
    <tr>
      <td><em>key_ID</em></td>
      <td>L'identificativo per la tua chiave che hai ottenuto nel passo [2](https://console.bluemix.net/docs/services/keymgmt/managing.html#viewingkeys_api__keyid).</td>
    </tr>
    <caption style="caption-side:bottom;">Tabella 2. Descrive le variabili necessarie per visualizzare le chiavi tramite l'API {{site.data.keyword.keymanagementserviceshort}}.</caption>
  </table>

  Il materiale della chiave viene restituita nel corpo-entità della risposta. Le chiavi generate automaticamente dagli HSM (Hardware
Security Module) sono codificate in base-64.

## Controllo delle chiavi e dell'accesso
{: #viewkeyassignments}

{{site.data.keyword.keymanagementservicelong_notm}}
fornisce un sistema centralizzato per visualizzare, gestire e controllare le tue chiavi di crittografia. Controlla le tue chiavi e le restrizioni di accesso
alle chiavi per assicurare la protezione alle tue risorse.

Controlla regolarmente la configurazione delle tue chiavi:

- Esamina quando vengono create le chiavi e determina se è il momento di ruotare la chiave.
- [Monitorare le chiamate API a{{site.data.keyword.keymanagementserviceshort}} con {{site.data.keyword.cloudaccesstrailshort}} ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")](https://console.bluemix.net/docs/services/AccessTrail/at_integration.html#at_integration_key_protect "Icona di link esterno"){: new_window}.
- Ispeziona quali utenti dispongono dell'accesso alle chiavi e se il livello di accesso è appropriato.

Per controllare gli utenti con l'accesso:

1. Come responsabile dello spazio, vai alle tue configurazioni dell'account e seleziona **Gestisci organizzazioni**.
2. Apri lo spazio che contiene l'istanza del servizio {{site.data.keyword.keymanagementserviceshort}}
per controllare quali utenti hanno accesso.
3. Se devi aggiungere degli utenti, vai a **Invita membri del team** e seleziona i ruoli {{site.data.keyword.Bluemix_notm}} che corrispondono alle autorizzazioni
{{site.data.keyword.keymanagementserviceshort}} che desideri concedere
all'utente:

  <table>
    <tr>
      <th>Ruoli {{site.data.keyword.Bluemix_notm}}</th>
      <th>Autorizzazioni {{site.data.keyword.keymanagementserviceshort}}</th>
    </tr>
    <tr>
      <td>Responsabile dello spazio</td>
      <td>Un responsabile dello spazio può creare, visualizzare ed eliminare le chiavi.</td>
    </tr>
    <tr>
      <td>Sviluppatore</td>
      <td>Uno sviluppatore può creare le chiavi e visualizzare i dettagli della chiave</td>
    </tr>
    <tr>
      <td>Revisore</td>
      <td>Un revisore può accedere alla vista di alto livello delle chiavi. </td>
    </tr>
    <caption style="caption-side:bottom;">Tabella 3. Associazione dei ruoli {{site.data.keyword.Bluemix_notm}} alle autorizzazioni {{site.data.keyword.keymanagementserviceshort}}.</caption>
  </table>
