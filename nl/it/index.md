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

# Introduzione a {{site.data.keyword.keymanagementserviceshort}}

{{site.data.keyword.keymanagementservicelong}} ti aiuta
ad eseguire il provisioning di chiavi crittografate per le applicazioni in {{site.data.keyword.Bluemix_short}}. Mentre gestisci il ciclo di vita delle tue chiavi,
puoi ottenere dei benefici sapendo che le tue chiavi sono protette
dagli HSM (Hardware Security Module) basati sul cloud che proteggono dal furto di informazioni.
{: shortdesc}

{{site.data.keyword.keymanagementserviceshort}} è
disponibile automaticamente per tutte le applicazioni all'interno dello spazio in cui è stato creato. [Dopo aver creato un'istanza del servizio](https://console.ng.bluemix.net/catalog/services/key-protect/?taxonomyNavigation=apps){: new_window},
completa la seguente procedura per essere operativo:

1. Per creare o caricare una chiave esistente, fai clic su **Aggiungi chiave**.
    Specifica i dettagli della chiave:
    <table>
      <tr>
        <th>Configurazione</th>
        <th>Descrizione</th>
      </tr>
      <tr>
        <td>Nome</td>
        <td>Un alias leggibile dall'utente da assegnare alla tua chiave. Il nome può essere qualsiasi cosa ti aiuti a identificare la chiave,
come ad esempio come viene utilizzata la chiave o chi è associata ad essa.</td>
      </tr>
      <tr>
        <td>Algoritmo</td>
        <td>La crittografia della chiave simmetrica è supportata dall'algoritmo AES-GCM.</td>
      </tr>
      <tr>
        <td>Chiave</td>
        <td>Obbligatoria solo se stai aggiungendo una chiave esistente. Il materiale della chiave può essere uno qualsiasi dei dati
che desideri archiviare nel servizio {{site.data.keyword.keymanagementserviceshort}}, come
un certificato o una chiave RSA.</td>
      </tr>
        <caption style="caption-side:bottom;">Tabella 1. Descrizione delle impostazioni delle chiavi</caption>
    </table>

2. Una volta che hai finito di compilare i dettagli della chiave, fai clic su **Aggiungi chiave** per confermare. Le chiavi sono disponibili immediatamente. Le nuove chiavi vengono generate dagli HSM (Hardware Security Module) ubicati nei data center {{site.data.keyword.IBM}} sicuri.
3. Copia l'identificativo di riferimento nella riga della chiave. Il valore **ID** è l'identificativo che utilizzi nell'API {{site.data.keyword.keymanagementserviceshort}}.
4. **Facoltativo**: se desideri eliminare una chiave, tieni presente che il materiale della chiave non è ripristinabile. I metadati
associati alla chiave vengono conservati nel database {{site.data.keyword.keymanagementserviceshort}}. Per eliminare una chiave,
fai clic sull'icona **Azioni** nella riga della chiave e conferma l'eliminazione nella schermata successiva.

Operazioni successive:

Ora, puoi utilizzare le chiavi per crittografare i tuoi servizi e le tue applicazioni.

- Per visualizzare un esempio di come è possibile utilizzare le chiavi archiviate in {{site.data.keyword.keymanagementserviceshort}} per crittografare e decrittografare i dati, [controlla l'applicazione di esempio in Github ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")](https://github.com/IBM-Bluemix/key-protect-helloworld-python "Icona di link esterno"){: new_window}.
- Per ulteriori informazioni sulla gestione a livello programmatico delle tue chiavi, controlla il [{{site.data.keyword.keymanagementserviceshort}}documento di riferimento dell'API](https://console.ng.bluemix.net/apidocs/639) per degli esempi di codice.

## Link correlati

- [API REST {{site.data.keyword.keymanagementserviceshort}} ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")](https://console.ng.bluemix.net/apidocs/639 "Icona di link esterno"){: new_window}
- [API REST di gestione {{site.data.keyword.keymanagementserviceshort}} ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")](https://docs-admin-keyprotect.ng.bluemix.net/ "Icona di link esterno"){: new_window}
- [Offerta HSM cloud ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")](http://www.softlayer.com/ibm-cloud-hsm "Icona di link esterno"){: new_window}
