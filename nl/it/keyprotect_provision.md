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

#  Provisioning del servizio {{site.data.keyword.keymanagementserviceshort}}
{: #provision}

Puoi creare un'istanza sicura di {{site.data.keyword.keymanagementservicefull}} utilizzando la console
{{site.data.keyword.Bluemix_notm}} o la CLI {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

## Provisioning dalla console {{site.data.keyword.Bluemix_notm}} 
{: #gui}

Per eseguire il provisioning di un'istanza di {{site.data.keyword.keymanagementserviceshort}} dalla console
{{site.data.keyword.Bluemix_notm}}, completa la seguente procedura.

1. [Accedi al tuo account {{site.data.keyword.Bluemix_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.bluemix.net/){: new_window}.
2. Fai clic su **Catalogo** per visualizzare l'elenco dei sevizi disponibili in {{site.data.keyword.Bluemix_notm}}.
3. Seleziona la categoria **Servizi** e fai clic sul tile **{{site.data.keyword.keymanagementserviceshort}}**.
5. Selezione un piano dei sevizi e fai clic su **Crea** per eseguire il provisioning di un'istanza del servizio
{{site.data.keyword.keymanagementserviceshort}} nello spazio e nell'organizzazione {{site.data.keyword.Bluemix_notm}} in cui hai eseguito l'accesso.

## Provisioning dalla CLI {{site.data.keyword.Bluemix_notm}} 
{: #cli}

Puoi eseguire il provisioning di un'istanza di {{site.data.keyword.keymanagementserviceshort}} utilizzando la CLI {{site.data.keyword.Bluemix_notm}}. [Scarica e installa lo strumento riga di comando nel tuo sistema](https://clis.ng.bluemix.net/ui/home.html){: new_window} per completare le seguenti istruzioni.

1. Accedi alla CLI {{site.data.keyword.Bluemix_notm}}.

    ```sh
    bx login [--sso]
    ```
    {: codeblock}
    **Nota**: il parametro `--sso` è obbligatorio quando
accedi con un ID federato. Se viene utilizzata questa opzione, vai al link elencato nell'output della CLI
per generare una passcode monouso.

2. Seleziona l'organizzazione e lo spazio {{site.data.keyword.Bluemix_notm}} in cui vuoi creare un'istanza del servizio {{site.data.keyword.keymanagementserviceshort}}.

    Puoi anche utilizzare il seguente comando per impostare l'organizzazione e lo spazio di destinazione. 

    ```sh
    bx target [-o organization_name] [-s space_name]
    ```
    {: codeblock}

3. Esegui il provisioning di un'istanza di {{site.data.keyword.keymanagementserviceshort}} in tali regione, organizzazione e spazio.

    ```sh
    bx service create ibm_key_management TieredPricing [instance_name]
    ```
    {: codeblock}

    Sostituisci _instance_name_ con un alias univoco per la tua istanza del servizio.

4. Verifica che tale istanza del servizio sia stata creata correttamente.

    ```sh
    bx service list
    ```
    {: codeblock}


### Operazioni successive

Ora puoi utilizzare le chiavi per crittografare i tuoi servizi e le tue applicazioni.

- Per visualizzare un esempio di come è possibile utilizzare le chiavi archiviate in {{site.data.keyword.keymanagementserviceshort}} per crittografare e decrittografare i dati, [controlla l'applicazione di esempio in GitHub ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.
- Per ulteriori informazioni sulla gestione a livello programmatico delle tue chiavi, [consulta la documentazione di riferimento API {{site.data.keyword.keymanagementserviceshort}} per esempi di codice ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
