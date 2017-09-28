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

# Gestione dell'accesso alle chiavi con l'API
{: #managing-access-api}

Con la gestione dell'identità e dell'accesso {{site.data.keyword.Bluemix}}, puoi abilitare il controllo dell'accesso granulare per le tue risorse chiave creando e modificando le politiche di accesso.
{: shortdesc}

Questa pagina ti guida attraverso diversi scenari per gestire l'accesso alle tue risorse chiave con [Access Management API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://iampap.ng.bluemix.net/v1/docs/#!/Access_Policies/){: new_window}.


Prima di iniziare:
- [Richiama il tuo token IAM e il GUID spazio](/docs/services/keymgmt/keyprotect_authentication.html)
- [Richiama l'ID della chiave per specificare la risorsa](/docs/services/keymgmt/keyprotect_view_keys.html)
- [Richiama l'ID dell'account per specificare il motivo dell'accesso](keyprotect_manage_access_api.html#retrieve_account_ID)
- [Richiama l'ID utente per cui desideri modificare l'accesso](keyprotect_manage_access_api.html#retrieve_user_ID)

## Creazione di una nuova politica di accesso
{: #create_policy}

Per abilitare il controllo dell'accesso per una chiave specifica, puoi inviare una richiesta alla gestione dell'identità e dell'accesso {{site.data.keyword.Bluemix_notm}} immettendo il seguente comando. Ripeti il comando per ogni politica di accesso.

```cURL
curl -X POST \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
  "roles": [
    {
      "id": "crn:v1:bluemix:public:iam::::role:<IAM_role>"
    }
  ],
  "resources": [
    {
      "serviceName": "IBM Key Protect",
      "region": "us-south",
      "resourceType": "key",
      "resource": "<key_ID>",
      "accountId": "<account_ID>",
      "spaceId": "<space_GUID>"
    }
  ]
}'
```
{: codeblock}

Sostituisci `<account_ID>`, `<user_ID>`, `<Admin_IAM_token>`, `<IAM_role>`, `<space_GUID>` e `<key_ID>` con i valori appropriati.

**Facoltativo:** verifica che la politica sia stata correttamente creata.

```cURL
curl -X GET \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}


## Aggiornamento di una politica di accesso
{: #update_policy}

Puoi utilizzare un ID della politica richiamato per modificare una politica esistente di un utente. Invia una richiesta alla gestione dell'identità e dell'accesso {{site.data.keyword.Bluemix_notm}} immettendo il seguente comando:

```cURL
curl -X PUT \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies/<policy_ID> \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'If-Match': <ETag_ID> \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
  "roles": [
    {
      "id": "crn:v1:bluemix:public:iam::::role:<IAM_role>"
    }
  ],
  "resources": [
    {
      "serviceName": "IBM Key Protect",
      "region": "us-south",
      "resourceType": "key",
      "resource": "<key_ID>",
      "accountId": "<account_ID>",
      "spaceId": "<space_GUID>"
    }
  ]
}'
```
{: codeblock}

Sostituisci `<account_ID>`, `<user_ID>`, `<policy_ID>`, `<Admin_IAM_token>`, `<ETag_ID>`, `<IAM_role>`, `<space_GUID>` e `<key_ID>` con i valori appropriati.

**Facoltativo:** verifica che la politica sia stata correttamente aggiornata.

```cURL
curl -X GET \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

## Eliminazione di una politica di accesso  
{: #delete_policy}

Puoi utilizzare un ID della politica richiamato per eliminare una politica esistente di un utente. Invia una richiesta alla gestione dell'identità e dell'accesso {{site.data.keyword.Bluemix_notm}} immettendo il seguente comando:

```cURL
curl -X DELETE \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies/<policy_ID> \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

Sostituisci `<account_ID>`, `<user_ID>`, `<policy_ID>` e  `<Admin_IAM_token>` con i valori appropriati.

**Facoltativo:** verifica che la politica sia stata correttamente eliminata. 

```cURL
curl -X GET \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

## Richiamo di un ID dell'account
{: #retrieve_account_id}

1. Accedi alla CLI {{site.data.keyword.Bluemix_notm}}.
    ```sh
    bx login [--sso]
    ```
    {: codeblock}

    **Nota**: il parametro `--sso` è obbligatorio quando
accedi con un ID federato. Se viene utilizzata questa opzione, vai al link elencato nell'output della CLI
per generare una passcode monouso.

    Il risultato visualizza le informazioni di identificazione del tuo account.

    ```sh
    Authenticating...
    OK

    Select an account (or press enter to skip):

    1. sample-account (b6hnh3560ehqjkf89s4ba06i367801e)
    Enter a number> 1
    Targeted account sample-acount (b6hnh3560ehqjkf89s4ba06i367801e)

    API endpoint:   https://api.ng.bluemix.net (API version: 2.75.0)
    Region:         us-south
    User:           admin
    Account:        sample-account (b6hnh3560ehqjkf89s4ba06i367801e)
    ```
    {: screen}
2. Copia il valore per il tuo ID dell'account.

## Richiamo di un ID utente 
{: #retrieve_user_id}

1. [Chiedi all'utente di fornire il proprio token IAM](/docs/services/keymgmt/keyprotect_authentication.html#retrieve_token).
    La struttura del token IAM è la seguente:

    ```sh
    IAM token: Bearer <value>.<value>.<value>
    ```
    {: screen}

2. Copia il valore intermedio ed esegui il seguente comando:
    ```sh
    echo -n "<value>" | base64 --decode
    ```
    {: codeblock}

    Il risultato mostra un oggetto JSON simile al seguente:
   ```json
   {
        "iam_id":"...",
        "id":"...",
        "realmid":"...",
        "identifier":"...",
        "given_name":"...",
        "family_name":"...",
        "name":"...",
        "email":"...",
        "sub":"...",
        "account":{
            "bss":"..."},
            "iat":...,
            "exp":...,
            "iss":"...",
            "grant_type":"...",
            "scope":"...",
            "client_id":"..."
        }
   }
   ```
   {: screen}

4. Copia il valore della proprietà `id`.
