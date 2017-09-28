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

# Eliminazione delle chiavi

Puoi utilizzare {{site.data.keyword.keymanagementservicefull}} per eliminare una chiave crittografata e il suo contenuto, se sei un amministratore del tuo spazio {{site.data.keyword.Bluemix_notm}} o dell'istanza del servizio {{site.data.keyword.keymanagementserviceshort}}.
{: shortdesc}

**Importante**: quando elimini una chiave, distrugge permanentemente il suo contenuto e i dati associati. L'azione è irreversibile. Distruggere le risorse non è consigliato negli ambienti di produzione, ma può essere utile negli ambienti temporanei come test o QA.

## Eliminazione delle chiavi con la GUI
{: #gui}

Se preferisci eliminare le tue risorse chiave con un'interfaccia grafica, puoi utilizzare la GUI {{site.data.keyword.keymanagementserviceshort}}.

[Dopo aver creato o importato le tue chiavi esistenti nel servizio](/docs/services/keymgmt/keyprotect_create_keys.html), completa la seguente procedura per eliminare una chiave:

1. [Accedi alla console {{site.data.keyword.Bluemix_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.bluemix.net/).
2. Dal tuo dashboard {{site.data.keyword.Bluemix_notm}}, seleziona l'istanza di cui è stato eseguito il provisioning di {{site.data.keyword.keymanagementserviceshort}}.
3. Passa al pannello **Manage** per sfogliare le chiavi nel tuo servizio.
4. Fai clic sull'icona per aprire un elenco di opzioni per la chiave che desideri eliminare.
5. Dal menu di opzioni, fai clic su **Delete key** e conferma l'eliminazione della chiave nella schermata successiva.

## Eliminazione delle chiavi con l'API
{: #api}

Per eliminare una chiave e i suoi contenuti, effettua una chiamata `DELETE` al seguente endpoint:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID>
```

1. [Richiama il tuo token di autorizzazione, il GUID organizzazione e il GUID spazio per utilizzare le chiavi nel sevizio.](/docs/services/keymgmt/keyprotect_authentication.html)

2. Richiama l'ID della chiave che desideri eliminare.

    Puoi richiamare l'ID di una chiave specifica effettuando una richiesta `GET /v2/keys` o visualizzando le tue chiavi nel dashboard {{site.data.keyword.keymanagementserviceshort}}.

3. Esegui il seguente comando cURL per eliminare permanentemente la chiave e il suo contenuto.

    ```cURL
    curl -X DELETE \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID> \
      -H 'authorization: Bearer <OAuth_token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
      -H 'prefer: <return_preference>'
    ```
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
        <td>L'identificativo univoco che viene assegnato al tuo spazio {{site.data.keyword.Bluemix_notm}}. </td>
      </tr>
      <tr>
        <td><em>organization_GUID</em></td>
        <td>L'identificativo univoco che viene assegnato alla tua organizzazione {{site.data.keyword.Bluemix_notm}}. </td>
      </tr>
      <tr>
        <td><em>key_ID</em></td>
        <td>L'identificativo univoco della chiave che desideri eliminare.</td>
      </tr>
      <tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p>Un'intestazione che modifica il comportamento del server per le operazioni <code>POST</code> e <code>DELETE</code>.</p><p>Se impostata su <code>return=minimal</code>, il servizio restituisce solo i metadati della chiave, come il valore <code>id</code> e nome, nel corpo-entità della risposta. Se impostata su <code>return=representation</code>, il servizio restituisce i metadati e il materiale della chiave.</p></td>
      </tr>
      <caption style="caption-side:bottom;">Tabella 1. Descrive le variabili necessarie per eliminare le chiavi tramite l'API {{site.data.keyword.keymanagementserviceshort}}.</caption>
    </table>

    I dettagli della richiesta `DELETE` vengono restituiti nel corpo-entità della risposta.
