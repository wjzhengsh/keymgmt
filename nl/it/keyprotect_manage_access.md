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

# Gestione dell'accesso utente con la gestione dell'accesso e dell'identità
{: #managing-access-iam}

{{site.data.keyword.keymanagementservicefull}} supporta un sistema di controllo dell'accesso centralizzato, controllato dalla gestione dell'accesso e dell'identità
{{site.data.keyword.Bluemix_notm}}, per aiutarti a gestire gli utenti e l'accesso alle tue chiavi crittografate.
{: shortdesc}

Ti raccomandiamo di concedere le autorizzazioni di accesso quando inviti nuovi utenti nel tuo servizio o account. Ad esempio, considera le seguenti linee guida:

- **Abilita l'accesso utente alle risorse nel tuo account assegnando i ruoli IAM.**
    Anziché condividere le tue credenziali ammin, crea nuove politiche per gli utenti che devono accedere alle chiavi crittografate nel tuo account. Se sei l'amministratore del tuo account, ti viene automaticamente assegnata una politica di gestione con l'accesso a tutte le risorse nell'account.
- **Concedi i ruoli e le autorizzazioni solo per gli scopi necessari.**
    Ad esempio, se un utente deve solo accedere a una vista di alto livello delle chiavi in uno spazio specifico, concedi il ruolo _Visualizzatore_ all'utente per tale spazio.
- **Controlla regolarmente chi dispone della capacità di gestire il controllo dell'accesso ed eliminare le risorse chiave.**
    Ricorda che concedendo un ruolo _Amministratore_ a un utente lo rendi capace di modificare le politiche del servizio per altri utenti, in aggiunta a distruggere le risorse.

## Ruoli e autorizzazioni
{: #roles}

Con IAM (Identity and Access Management) {{site.data.keyword.Bluemix_notm}}, puoi configurare le politiche che definiscono l'ambito di accesso a membri del tuo team.

Per semplificare l'accesso, {{site.data.keyword.keymanagementserviceshort}} allinea i ruoli IAM in modo che ogni utente disponga di una vista differente del servizio, in base al ruolo assegnato. Se sei un amministratore della sicurezza del tuo servizio, puoi assegnare i ruoli IAM che corrispondono alle autorizzazioni {{site.data.keyword.keymanagementserviceshort}} specifiche che vuoi concedere ai membri del tuo team.

La seguente tabella mostra come i ruoli di identità e accesso vengono associati alle autorizzazioni {{site.data.keyword.keymanagementserviceshort}}:
<table>
  <tr>
    <th>Ruolo</th>
    <th>Descrizione</th>
    <th>Azioni</th>
  </tr>
  <tr>
    <td>Visualizzatore</td>
    <td>Un visualizzatore può accedere alla vista di alto livello delle chiavi. I visualizzatori non possono accedere o modificare i dettagli della chiave.</td>
    <td>
      <ul>
        <li>Visualizza le chiavi</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Editor</td>
    <td>Un editor può creare, modificare le chiavi e visualizzare i dettagli della chiave.</td>
    <td>
      <ul>
        <li>Crea le chiavi</li>
        <li>Visualizza le chiavi</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Amministratore</td>
    <td>Un amministratore può eseguire tutte le azioni di un visualizzatore e di un editor, inclusa la possibilità di eliminare le chiavi, invitare nuovi utenti e gestire il controllo dell'accesso. </td>
    <td>
      <ul>
        <li>Crea le chiavi</li>
        <li>Visualizza le chiavi</li>
        <li>Elimina le chiavi</li>
        <li>Gestisce il controllo dell'accesso</li>
      </ul>
    </td>
  </tr>
  <caption style="caption-side:bottom;">Tabella 1. Associazione dei ruoli di identità e accesso alle autorizzazioni {{site.data.keyword.keymanagementserviceshort}}.</caption>
</table>

**Nota**: i ruoli utente IAM forniscono l'accesso al livello dell'istanza del servizio o del servizio. [Ruoli Cloud Foundry](/docs/iam/users_roles.html#cfroles) sono separati e definiscono l'accesso al livello dello spazio o dell'organizzazione.

Per ulteriori informazioni sulla gestione dell'accesso e dell'identità {{site.data.keyword.Bluemix_notm}}, consulta
[Ruoli utente e autorizzazioni](/docs/iam/users_roles.html#iamusermanpol).

### Operazioni successive

Gli amministratori e i proprietari dell'account possono invitare gli utenti e configurare le politiche del servizio che corrispondono alle azioni {{site.data.keyword.keymanagementserviceshort}} che possono eseguire gli utenti.

- Per informazioni sull'assegnazione dei ruoli utente nella IU {{site.data.keyword.Bluemix_notm}}, consulta [Politiche di accesso al servizio abilitate per l'accesso e l'identità](/docs/iam/iamusermanage.html#iammanidaccser).
- Per ulteriori informazioni su come concedere le autorizzazioni avanzate per accedere a chiavi crittografate specifiche, consulta [Gestione dell'accesso alle chiavi con l'API](/docs/services/keymgmt/keyprotect_manage_access_api.html).
