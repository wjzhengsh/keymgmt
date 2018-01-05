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

# Schlüssel anzeigen
{: #viewing-keys}

{{site.data.keyword.keymanagementservicefull}} stellt ein zentrales System zum Anzeigen, Verwalten und Prüfen Ihrer Verschlüsselungsschlüssel bereit. Prüfen Sie Ihre Schlüssel und Zugriffsbeschränkungen für Schlüssel, um die Sicherheit Ihrer Ressourcen sicherzustellen.
{: shortdesc}

Prüfen Sie Ihre Schlüsselkonfiguration regelmäßig:

- Untersuchen Sie, wann die Schlüssel erstellt wurden und stellen Sie fest, ob es an der Zeit ist, den Schlüssel zu wechseln.
- [Überwachen Sie API-Aufrufe für {{site.data.keyword.keymanagementserviceshort}} mit {{site.data.keyword.cloudaccesstrailshort}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/cloud-activity-tracker/svcs/kp_at.html#kp_at){: new_window}.
- Untersuchen Sie, welche Benutzer auf Schlüssel zugreifen können, und ob entsprechende Zugriffsberechtigungen
erteilt wurden.

Weitere Informationen zum Prüfen des Zugriffs auf Ihre Ressourcen finden Sie in [Benutzerzugriff mit Cloud IAM verwalten](/docs/services/keymgmt/keyprotect_manage_access.html).

## Schlüssel mit GUI anzeigen
{: #gui}

Wenn Sie die Überprüfung von Verschlüsselungsschlüssel über eine grafische Oberfläche bevorzugen, dann können Sie hierzu das {{site.data.keyword.keymanagementserviceshort}}-Dashboard verwenden.

[Nach dem Erstellen oder Importieren der vorhandenen Schlüssel in den Service](/docs/services/keymgmt/keyprotect_create_keys.html) müssen Sie die folgenden Schritte ausführen, um Ihre Schlüssel anzuzeigen.

1. [Melden Sie sich bei der {{site.data.keyword.cloud_notm}}-Konsole ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.bluemix.net/) an.
2. Wählen Sie im {{site.data.keyword.cloud_notm}}-Dashboard die bereitgestellte Instanz von {{site.data.keyword.keymanagementserviceshort}} aus.
3. Durchsuchen Sie die allgemeinen Merkmale Ihrer Schlüssel mithilfe des {{site.data.keyword.keymanagementserviceshort}}-Dashboards:

    <table>
      <tr>
        <th>Spalte</th>
        <th>Beschreibung</th>
      </tr>
      <tr>
        <td>Name</td>
        <td>Der eindeutige, lesbare Alias, der Ihrem Schlüssel zugewiesen wurde.</td>
      </tr>
      <tr>
        <td>ID</td>
        <td>Eine eindeutige Schlüssel-ID, die Ihrem Schlüssel vom {{site.data.keyword.keymanagementserviceshort}}-Service zugewiesen wurde. Mit dem ID-Wert können Sie den Service mit der [{{site.data.keyword.keymanagementserviceshort}}-API](https://console.ng.bluemix.net/apidocs/639) aufrufen.</td>
      </tr>
      <tr>
        <td>Status</td>
        <td>Der [Schlüsselzustand](/docs/services/keymgmt/keyprotect_states.html) basiert auf der Dokumentation ['NIST Special Publication 800-57, Recommendation for Key Management' ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf). Diese Zustände sind <i>Pre-active</i> (Bereits aktiv), <i>Active</i> (Aktiv), <i>Deactivated</i> (Inaktiviert) und <i>Destroyed</i> (Gelöscht).</td>
      </tr>
      <tr>
        <td>Typ</td>
        <td>Der [Schlüsseltyp](/docs/services/keymgmt/keyprotect_envelope.html#key_types), der den Zweck des Schlüssels im Service beschreibt.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabelle 1. Beschreibung der Tabelle <b>Schlüssel</b></caption>
    </table>

## Schlüssel mit API anzeigen
{: #api}

Sie können den Inhalt Ihrer Schlüssel abrufen, indem Sie die {{site.data.keyword.keymanagementserviceshort}}-API verwenden.

### Schritt 1: Gruppe von Schlüsseln abrufen
{: #retrieve_keys_api}

Für eine übergeordnete Ansicht können Sie die Schlüssel durchsuchen, die in Ihrer bereitgestellten Instanz von {{site.data.keyword.keymanagementserviceshort}} verwaltet werden, indem Sie einen `GET`-Aufruf zum folgenden Endpunkt absetzen:

```
https://key-protect.us-south.bluemix.net/api/v2/keys
```
{: codeblock}

1. [Rufen Sie Ihren Service- und Authentifizierungsnachweis ab, um mit den Schlüsseln im Service zu arbeiten.](/docs/services/keymgmt/keyprotect_authentication.html)
2. Führen Sie den folgenden cURL-Befehl aus, um allgemeine Merkmale Ihres Schlüssels anzuzeigen.

    ```cURL
    curl -X GET \
    https://key-protect.us-south.bluemix.net/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <IAM_token>' \
    -H 'bluemix-instance: <instance_ID>' \
    -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

    Um mit Schlüsseln in bestimmten Cloud Foundry-Organisationen und -Bereichen zu arbeiten, ersetzen Sie `Bluemix-Instance` durch die entsprechenden Header `Bluemix-org` und `Bluemix-space`. [Siehe auch die Codebeispiele in der {{site.data.keyword.keymanagementserviceshort}}-API-Referenzdokumentation ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
    {: tip}

    Ersetzen Sie die Variablen in der Beispielanforderung mithilfe der Angaben in der folgenden Tabelle.
    <table>
      <tr>
        <th>Variable</th>
        <th>Beschreibung</th>
      </tr>
      <tr>
        <td><em>IAM_token</em></td>
        <td>Ihr Berechtigungstoken. Nehmen Sie den vollständigen Inhalt des <code>IAM</code>-Tokens einschließlich des Werts für Bearer in die cURL-Anforderung auf.</td>
      </tr>
      <tr>
        <td><em>instance_ID</em></td>
        <td>Die eindeutige ID, die Ihrer {{site.data.keyword.keymanagementserviceshort}}-Serviceinstanz zugewiesen ist.</td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>Optional: Die eindeutige ID, die zum Überwachen und Korrelieren von Transaktionen verwendet wird.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabelle 2. Beschreibt die Variablen, die zum Anzeigen von Schlüsseln über die {{site.data.keyword.keymanagementserviceshort}}-API erforderlich sind.</caption>
    </table>

    Die erfolgreiche Anforderung `POST /v2/keys/` gibt eine Gruppe von Schlüsseln zurück, die in Ihrer {{site.data.keyword.keymanagementserviceshort}}-Serviceinstanz vorhanden ist.

    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.collection+json",
        "collectionTotal": 2
      },
    "resources": [
      {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Standard key",
          "description": "...",
          "state": 1,
          "crn": "...",
          "algorithmType": "AES",
          "createdBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "256",
            "mode": "GCM"
          },
          "extractable": true
        },
        {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Root key",
          "description": "...",
          "state": 1,
          "crn": "...",
          "algorithmType": "AES",
          "createdBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "256",
            "mode": "GCM"
          },
          "extractable": false
        }
      ]
    }
    ```
    {:screen}

### Schritt 2: Schlüssel nach ID abrufen
{: #retrieve_key_api}

Um detaillierte Informationen zu einem bestimmten Schlüssel anzuzeigen, können Sie einen weiteren `GET`-Aufruf zum folgenden Endpunkt absetzen:

```
https://key-protect.us-south.bluemix.net/api/v2/keys<key_ID>
```
{: codeblock}

1. [Rufen Sie Ihren Service- und Authentifizierungsnachweis ab, um mit den Schlüsseln im Service zu arbeiten.](/docs/services/keymgmt/keyprotect_authentication.html)
2. Rufen Sie die ID des Schlüssels ab, auf den Sie zugreifen möchten.

    Der ID-Wert wird für den Zugriff auf ausführliche Informationen zu dem Schlüssel (z. B. auf die Schlüsselinformationen selbst) verwendet. Sie können die ID für einen angegebenen Schlüssel abrufen, indem Sie die Anforderung `GET v2/keys` absetzen oder indem Sie auf die {{site.data.keyword.keymanagementserviceshort}}-GUI zugreifen.

3. Führen Sie den folgenden cURL-Befehl aus, um Details zu Ihrem Schlüssel und die Schlüsselinformationen abzurufen.

    ```cURL
    curl -X GET \
      https://key-protect.us-south.bluemix.net/api/v2/keys<key_ID> \
      -H 'accept: application/vnd.ibm.kms.key+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

    Ersetzen Sie die Variablen in der Beispielanforderung mithilfe der Angaben in der folgenden Tabelle.

    <table>
      <tr>
        <th>Variable</th>
        <th>Beschreibung</th>
      </tr>
      <tr>
        <td><em>IAM_token</em></td>
        <td>Ihr Berechtigungstoken. Nehmen Sie den vollständigen Inhalt des `IAM`-Tokens einschließlich des Werts für Bearer in die cURL-Anforderung auf.</td>
      </tr>
      <tr>
        <td><em>instance_ID</em></td>
        <td>Die eindeutige ID, die Ihrer {{site.data.keyword.keymanagementserviceshort}}-Serviceinstanz zugewiesen ist.</td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>Optional: Die eindeutige ID, die zum Überwachen und Korrelieren von Transaktionen verwendet wird.</td>
      </tr>
      <tr>
        <td><em>key_ID</em></td>
        <td>Die ID für den Schlüssel, der in [Schritt 1](#retrieve_keys_api) abgerufen wurde.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabelle 3. Beschreibt die Variablen, die zum Anzeigen eines angegebenen Schlüssels über die {{site.data.keyword.keymanagementserviceshort}}-API erforderlich sind.</caption>
    </table>

    Die erfolgreiche Antwort `GET v2/keys/<key_ID>` gibt Details zu Ihrem Schlüssel und zu den Schlüsselinformationen zurück. Das folgende JSON-Objekt zeigt ein Beispiel für einen zurückgegebenen Wert für einen Standardschlüssel.

    ```
    {
        "metadata": {
            "collectionTotal": 1,
            "collectionType": "application/vnd.ibm.kms.key+json"
        },
    "resources": [
      {
            "id": "...",
            "type": "application/vnd.ibm.kms.key+json",
            "name": "Standard key",
            "description": "...",
            "state": 1,
            "crn": "...",
            "algorithmType": "AES",
            "payload": "...",
            "createdBy": "...",
            "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
            "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
            "algorithmMetadata": {
                "bitLength": "256",
                "mode": "GCM"
            },
            "extractable": true
        }
      ]
    }
    ```
    {:screen}

    Die [REST-API-Referenzdokumentation![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/apidocs/639){: new_window} zu {{site.data.keyword.keymanagementserviceshort}} enthält eine detaillierte Beschreibung zu den verfügbaren Parametern.
