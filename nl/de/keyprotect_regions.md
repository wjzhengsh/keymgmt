---

copyright:
  years: 2017
lastupdated: "2017-12-15"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Regionen und Standorte
{: #regions-and-locations}

Sie können Ihre Anwendungen mit dem {{site.data.keyword.keymanagementservicelong_notm}}-Service verbinden, indem Sie einen regionalen Serviceendpunkt angeben.
{: shortdesc}

## Verfügbare Regionen
{: #regions}

{{site.data.keyword.keymanagementserviceshort}} ist in den folgenden Regionen verfügbar:

- Vereinigte Staaten (Süden)
- Vereinigtes Königreich  

## Serviceendpunkte
{: #endpoints}

Wenn Sie Ihre {{site.data.keyword.keymanagementserviceshort}}-Ressourcen programmgesteuert verwalten, können Sie mithilfe der folgenden Tabelle die API-Endpunkte bestimmen, die für die Verbindung zur [{{site.data.keyword.keymanagementserviceshort}}-API](https://console.ng.bluemix.net/apidocs/639) verwendet werden: 

<table>
    <tr>
        <th>Region</th>
        <th>API-Endpunkt</th>
    </tr>
    <tr>
        <td>Vereinigte Staaten (Süden)</td>
        <td>
            <code>https://keyprotect.us-south.bluemix.net</code>
        </td>
    </tr>
    <tr>
        <td>Vereinigtes Königreich</td>
        <td>
            <code>https://keyprotect.eu-gb.bluemix.net</code>
        </td>
    </tr>
    <caption style="caption-side:bottom;">Tabelle 2. Verfügbare Endpunkte für die {{site.data.keyword.keymanagementserviceshort}}-API</caption>
</table>

**Hinweis:** Verwenden Sie für {{site.data.keyword.keymanagementserviceshort}}-Serviceinstanzen, die in Cloud Foundry-Organisationen oder -Bereichen vorhanden sind, den alten Endpunkt `https://ibm-key-protect.edge.bluemix.net`, um mit der {{site.data.keyword.keymanagementserviceshort}}-API zu interagieren.

Informationen zur Authentifizierung mit {{site.data.keyword.keymanagementserviceshort}} finden Sie in [Auf die API zugreifen](/docs/services/keymgmt/keyprotect_authentication.html).
