---

copyright:
  years: 2017
lastupdated: "2017-11-08"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Schlüssel erstellen

Sie können den Lebenszyklus Ihrer Schlüssel mithilfe von {{site.data.keyword.keymanagementservicefull}} verwalten.
{: shortdesc}

Bewährt hat sich die sichere Verwaltung Ihrer Schlüssel während der Entwicklung des Codes. Beachten Sie neben einigen anderen sicheren Codierungsverfahren zum Beispiel auch die folgenden Leitlinien.

- Berücksichtigen Sie Auswirkungen auf die Sicherheit, wenn Sie Schlüssel in Ihren Code einbetten.
- Erstellen Sie Schlüssel nur für den programmgestützten Zugriff auf Ihre Apps und Ressourcen. Erstellen Sie keine Schlüssel, wenn Sie einfachere [Benutzerberechtigungen![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.bluemix.net/docs/admin/patterns.html#userroles){: new_window} erstellen können.
- Wechseln Sie Schlüssel regelmäßig (Schlüsselrotation) und entfernen Sie nicht genutzte Schlüssel.
- Verwenden Sie eine Mehrfaktorauthentifizierung für kritische Operationen.
- Isolieren Sie Apps, indem Sie separate Schlüssel für jede App benutzen.
- Ziehen Sie die Verwendung der programmgesteuerten API in Betracht, wenn Sie besonders sensible Informationen übertragen.

Wenn Sie den Service zuerst testen möchten, bevor Sie eigene Schlüssel hinzufügen, können Sie die [Beispiel-App![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window} verwenden.

## Schlüssel mit GUI erstellen
{: #gui}

Informationen zum Hinzufügen von Schlüsseln zu Ihrem Service mit der {{site.data.keyword.keymanagementserviceshort}}-GUI finden Sie im Abschnitt mit der [Einführung zu {{site.data.keyword.keymanagementserviceshort}}](/docs/services/keymgmt/index.html#addkey).

## Schlüssel mit der API erstellen
{: #api}

Mit der {{site.data.keyword.keymanagementserviceshort}}-API können Sie vorhandene Schlüssel programmgesteuert schützen oder neue Schlüssel generieren.

Um Schlüssel zu erstellen oder vorhandene Schlüssel zu importieren, senden Sie einen `POST`-Aufruf an den folgenden Endpunkt:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys
```
{: codeblock}

1. [Rufen Sie das Berechtigungstoken, die Organisations-GUID und die Bereichs-GUID ab, um im Service mit Schlüsseln arbeiten zu können.](/docs/services/keymgmt/keyprotect_authentication.html)

2. Rufen Sie die [{{site.data.keyword.keymanagementserviceshort}}-API](https://console.ng.bluemix.net/apidocs/639) mit dem folgenden cURL-Befehl auf.

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

    Ersetzen Sie die Variablen in der Beispielanforderung mithilfe der Angaben in der folgenden Tabelle.
    <table>
      <tr>
        <th>Variable</th>
        <th>Beschreibung</th>
      </tr>
      <tr>
        <td><em>OAuth_token</em></td>
        <td>Ihr Berechtigungstoken. Nehmen Sie den vollständigen Inhalt des Tokens einschließlich des Werts für Bearer in die cURL-Anforderung auf.</td>
      </tr>
      <tr>
        <td><em>organization_GUID</em></td>
        <td>Die eindeutige ID, die Ihrer {{site.data.keyword.cloud_notm}}-Organisation zugewiesen ist. </td>
      </tr>
      <tr>
        <td><em>space_GUID</em></td>
        <td>Die eindeutige ID, die Ihrem {{site.data.keyword.cloud_notm}}-Bereich zugewiesen ist.</td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>Die eindeutige ID, die zum Überwachen und Korrelieren von Transaktionen verwendet wird.</td>
      </tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p>Ein Header, der das Serververhalten für <code>POST</code>- und <code>DELETE</code>-Operationen ändert.</p><p>Bei Verwendung der Einstellung <code>return=minimal</code> gibt der Service im Entitätshauptteil der Antwort nur die Schlüsselmetadaten zurück, z. B. den Schlüsselnamen und den Wert für <code>id</code>. Wird <code>return=representation</code> verwendet, dann gibt der Service sowohl die Schlüsselinformationen als auch die Schlüsselmetadaten zurück.</p></td>
      </tr>
      <tr>
        <td><em>key_alias</em></td>
        <td>Ein lesbarer Name zur einfachen Identifikation Ihres Schlüssels.</td>
      </tr>
      <tr>
        <td><em>key_description</em></td>
        <td>Eine erweiterte Beschreibung Ihres Schlüssels.</td>
      </tr>
      <tr>
        <td><em>YYYY-MM-DD</em><br><em>HH:MM:SS.SS</em></td>
        <td>Optional: Der Zeitpunkt (Datum und Uhrzeit), zu dem der Schlüssel im System abläuft, im RFC-3339-Format. Wenn das Attribut <code>expirationDate</code> fehlt, bleibt der Schlüssel unbegrenzt gültig. </td>
      </tr>
      <tr>
        <td><em>key_material</em></td>
        <td>Die Schlüsselinformationen (z. B. ein RSA-Schlüssel), die Sie in {{site.data.keyword.keymanagementserviceshort}} speichern möchten. Lassen Sie für die Generierung eines neuen Schlüssels das Attribut <code>payload</code> und die Variable <em>key_material</em> weg.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabelle 1. Für das Hinzufügen von Schlüsseln über die {{site.data.keyword.keymanagementserviceshort}}-API erforderliche Variablen</caption>
    </table>

    In einer erfolgreichen Antwort werden der Wert für `id` Ihres Schlüssel sowie weitere Metadaten zurückgegeben. In `id` wird eine eindeutige Kennung angegeben, die Ihrem Schlüssel zugewiesen wurde und die für nachfolgende Aufrufe verwendet wird.

3. **Optional:** Stellen Sie sicher, dass der Schlüssel durch Ausführen des folgenden Aufrufs zum Abrufen der Schlüssel in Ihrem {{site.data.keyword.cloud_notm}}-Bereich erstellt wurde.

    ```cURL
    curl -X GET \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <OAuth-token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
    ```
    {: codeblock}

### Weitere Schritte

Sie können Ihre Schlüssel nun verwenden, um Ihre Apps und Services zu codieren.

- Die [REST-API-Referenzdokumentation![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/apidocs/639){: new_window} zu {{site.data.keyword.keymanagementserviceshort}} enthält detaillierte Informationen zu allen REST-Anforderungen und -Antworten.
