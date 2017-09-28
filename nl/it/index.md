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

# Introduzione a {{site.data.keyword.keymanagementserviceshort}}

I seguenti sono i passi necessari per generare, immettere e gestire le chiavi in {{site.data.keyword.keymanagementservicelong}}.
{: shortdesc}

## Prerequisiti
{: #prereqs }

{{site.data.keyword.keymanagementserviceshort}} è disponibile per i servizi e le applicazioni che possono, con la corretta autorizzazione, effettuare una chiamata API a {{site.data.keyword.keymanagementserviceshort}}. Avrai bisogno di quanto segue prima di aggiungere una chiave.
- [Un ID IBM e una password](https://console.bluemix.net/docs/admin/adminpublic.html#signing-up-for-bluemix){: new_window}
- [Un'istanza del servizio](https://console.ng.bluemix.net/catalog/services/key-protect/?taxonomyNavigation=apps){: new_window}

## Aggiunta di una chiave
{: #addkey }

Utilizza i seguenti passi per creare una nuova chiave o caricarne una esistente.

1. [Accedi alla console Bluemix.](https://console.bluemix.net/catalog){: new_window}
2. Passa con il mouse sul link **All Categories** per far comparire la barra di scorrimento. Scorri fino a **Services > Security**. Sarà visualizzato un elenco dei tuoi servizi e applicazioni.
3. Fai doppio clic sulla tua istanza del servizio **Key Protect**. Tieni presente che in **Actions** puoi ridenominare o eliminare il servizio.

Sarai automaticamente reindirizzato alla pagina **Add a new key** se stai immettendo o generando una chiave per la prima volta. **Generate New Key** viene utilizzato per generare una nuova chiave in {{site.data.keyword.keymanagementserviceshort}} e **Enter Existing Key** viene utilizzato per immettere una chiave esistente nel servizio.

### Generazione di una chiave
{: #genkey }

Utilizza i seguenti passi per generare una nuova chiave con Key Protect.

1. Immetti le seguenti informazioni in **Generate new key** per creare una nuova chiave con Key Protect.
    <table>
      <tr>
        <th>Campo</th>
        <th>Descrizione</th>
      </tr>
      <tr>
        <td>Nome</td>
        <td>Un alias leggibile dall'utente da assegnare alla tua chiave. Il nome può essere qualsiasi cosa ti aiuti a identificare la chiave,
come ad esempio come viene utilizzata la chiave o chi è associata ad essa.</td>
      </tr>
      <tr>
        <td>Tipo di chiave</td>
        <td>L'impostazione predefinita è chiave standard. Una chiave standard viene utilizzata come una chiave di crittografia dei dati per codificare i tuoi dati di testo non crittografato in testo cifrato.</td>
      </tr>
        <caption style="caption-side:bottom;">Tabella 1. Descrizione delle impostazioni di generazione nuova chiave</caption>
    </table>

2. Fai clic sul pulsante **Generate key**. Le chiavi sono disponibili immediatamente. Le nuove chiavi vengono generate dagli HSM (Hardware Security Module) ubicati nei data center {{site.data.keyword.IBM}} sicuri.
3. Copia l'identificativo di riferimento nella riga della chiave. Il valore **ID** è l'identificativo che utilizzi nell'API {{site.data.keyword.keymanagementserviceshort}}.

### Immissione di una chiave esistente
{: #existkey }

Utilizza i seguenti passi per immettere una chiave esistente in Key Protect.

1. Immetti le seguenti informazioni in **Enter existing key**.
    <table>
      <tr>
        <th>Campo</th>
        <th>Descrizione</th>
      </tr>
      <tr>
        <td>Nome</td>
        <td>Un alias leggibile dall'utente da assegnare alla tua chiave. Il nome può essere qualsiasi cosa ti aiuti a identificare la chiave,
come ad esempio come viene utilizzata la chiave o chi è associata ad essa.</td>
      </tr>
      <tr>
        <td>Tipo di chiave</td>
        <td>L'impostazione predefinita è chiave standard. Una chiave standard viene utilizzata come una chiave di crittografia dei dati per codificare i tuoi dati di testo non crittografato in testo cifrato.</td>
      </tr>
      <tr>
        <td>Materiale della chiave</td>
        <td>Il materiale della chiave può essere qualsiasi tipo di dati desideri archiviare nel servizio {{site.data.keyword.keymanagementserviceshort}}, come un certificato o una chiave RSA.</td>
      </tr>
        <caption style="caption-side:bottom;">Tabella 2. Descrizione delle impostazioni di immissione di una chiave esistente</caption>
    </table>

2. Fai clic sul pulsante **Add a new key**. Le chiavi sono disponibili immediatamente.
3. Copia l'identificativo di riferimento nella riga della chiave. Il valore **ID** è l'identificativo che utilizzi nell'API {{site.data.keyword.keymanagementserviceshort}}.

## Gestione delle tue chiavi
{: #managekey }

Per visualizzare le tue chiavi dopo averle generate e immesse, segui le istruzioni in [Adding a key](index.html#addkey). Sarai reindirizzato alla finestra **Keys**. Le tue chiavi saranno visualizzate in ordine di data di creazione con la chiave più recente all'inizio dell'elenco.
<table>
      <tr>
        <th>Colonna</th>
        <th>Descrizione</th>
      </tr>
      <tr>
        <td>Nome</td>
        <td>Un alias leggibile dall'utente assegnato alla tua chiave. </td>
      </tr>
      <tr>
        <td>ID</td>
        <td>Un ID della chiave univoco per la tua chiave da Key Protect.</td>
      </tr>
      <tr>
        <td>Stato</td>
        <td>Uno degli stati della chiave dal NIST (National Institute of Standards and Technology) - Pre-attivato, Attivato, Disattivato e Distrutto.<td>
      </tr>
      <tr>
        <td>Creato</td>
        <td>Data e ora in cui è stata creata la chiave.</td>
      </tr>
      <tr>
        <td>Tipo</td>
        <td>L'impostazione predefinita è chiave standard. </td>
      </tr>
      <caption style="caption-side:bottom;">Tabella 3. Descrizione della finestra delle chiavi</caption>
    </table>

### Operazioni successive

Ora, puoi utilizzare le chiavi per crittografare i tuoi servizi e le tue applicazioni.

- Per visualizzare un esempio di come è possibile utilizzare le chiavi archiviate in {{site.data.keyword.keymanagementserviceshort}} per crittografare e decrittografare i dati, [controlla l'applicazione di esempio in Github ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.
- Per ulteriori informazioni sulla gestione a livello programmatico delle tue chiavi, controlla il [{{site.data.keyword.keymanagementserviceshort}}documento di riferimento dell'API](https://console.ng.bluemix.net/apidocs/639) per degli esempi di codice.

### Link correlati

- [API REST {{site.data.keyword.keymanagementserviceshort}} ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")](https://console.ng.bluemix.net/apidocs/639){: new_window}
- [API REST di gestione {{site.data.keyword.keymanagementserviceshort}} ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")](https://docs-admin-keyprotect.ng.bluemix.net/){: new_window}
- [Offerta HSM cloud ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")](http://www.softlayer.com/ibm-cloud-hsm){: new_window}
- [{{site.data.keyword.keymanagementservicelong_notm}} Service Level Agreement ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www-03.ibm.com/software/sla/sladb.nsf/sla/bm-7603-01){: new_window}
