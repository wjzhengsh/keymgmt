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

# Generazione delle credenziali di autenticazione 
{: #authentication}

{{site.data.keyword.keymanagementservicefull}} fornisce un'API REST
che può essere utilizzata con qualsiasi linguaggio di programmazione per archiviare, richiamare e generare le chiavi.
{: shortdesc}

Per utilizzare l'API, devi generare le tue credenziali del servizio e di autenticazione. 

## Richiamo dei tuoi GUID spazio e organizzazione
{: #retrieve_GUIDs}

Puoi richiamare le informazioni di identificazione per i tuoi spazio e organizzazione {{site.data.keyword.Bluemix_notm}} con la CLI [{{site.data.keyword.Bluemix_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.bluemix.net/docs/cli/reference/bluemix_cli/index.html#getting-started).

1. Accedi a {{site.data.keyword.Bluemix_notm}} con la CLI {{site.data.keyword.Bluemix_notm}}.

    ```
    bx login [--sso]
    ```
    {: codeblock}

    Il parametro `--sso` è obbligatorio quando
accedi con un ID federato. Se viene utilizzata questa opzione, vai al link elencato nell'output della CLI
per generare una passcode monouso. 

2. Seleziona l'organizzazione o lo spazio {{site.data.keyword.Bluemix_notm}}
che contiene la tua istanza del servizio {{site.data.keyword.keymanagementserviceshort}}.

    Prendi nota dei nomi dei tuoi spazio e organizzazione nell'output della CLI. Puoi anche eseguire `bx
target` per visualizzare queste informazioni.

3. Richiama i tuoi GUID dell'organizzazione e dello spazio {{site.data.keyword.Bluemix_notm}}.

    ```
    bx iam org [organization_name] --guid
    bx iam space [space_name] --guid
    ```
    {: codeblock}
    Sostituisci _organization_name_ e _space_name_ con l'alias univoco che hai assegnato ai tuoi organizzazione e spazio.

## Richiamo del tuo token di autorizzazione
{: #retrieve_token}

Puoi utilizzare un token di autorizzazione per gestire in modo programmatico le tue chiavi utilizzando l'API {{site.data.keyword.keymanagementserviceshort}}.

**Nota**: per abilitare il controllo dell'accesso granulare controllato dalla gestione dell'accesso e dell'identità {{site.data.keyword.Bluemix_notm}}, utilizza un token IAM quando effettui le chiamate al servizio.

1. Nella CLI {{site.data.keyword.Bluemix_notm}}, seleziona l'organizzazione o lo spazio che contiene il tuo servizio {{site.data.keyword.keymanagementserviceshort}}.

2. Richiama e visualizza i tuoi token di autorizzazione.

    ```
    bx iam oauth-tokens
    ```
    {: codeblock}

    Il seguente esempio troncato mostra l'output del token {{site.data.keyword.Bluemix_notm}}. La variabile _Bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7_ è un esempio di token di accesso.


    ```
    IAM token: Bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7...
    UAA token: Bearer mjEyJhbGciOiJIUzI1Ni.chWyW1faWQiOiJJQkWs1...
    ```
    {: screen}

    Utilizza il valore di connessione `IAM` o `UAA` per gestire in modo programmatico le chiavi nel tuo servizio utilizzando l'API {{site.data.keyword.keymanagementserviceshort}}.

### Operazioni successive

Consulta il [{{site.data.keyword.keymanagementserviceshort}}documento di riferimento della API REST ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")](https://console.ng.bluemix.net/apidocs/639){: new_window} per iniziare a gestire le chiavi nel tuo spazio.
