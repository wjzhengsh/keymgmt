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

# Schlüssel anzeigen

Sie können den Inhalt Ihrer Verschlüsselungsschlüssel mit {{site.data.keyword.keymanagementservicefull}} anzeigen.
{: shortdesc}

## Schlüssel mit GUI anzeigen
{: #gui}

Informationen zum Durchsuchen von Schlüsseln in Ihrem Service mit der {{site.data.keyword.keymanagementserviceshort}}-GUI finden Sie im Abschnitt mit der [Einführung zu {{site.data.keyword.keymanagementserviceshort}}](/docs/services/keymgmt/index.html#managekey).

## Schlüssel mit API anzeigen
{: #api}

Sie können den Inhalt Ihrer Schlüssel abrufen, indem Sie die {{site.data.keyword.keymanagementserviceshort}}-API verwenden.

### Schritt 1: Gruppe von Schlüsseln abrufen
{: #retrieve_keys_api}

Für eine übergeordnete Ansicht können Sie die Schlüssel durchsuchen, die in Ihrem Bereich verwaltet werden, indem Sie einen `GET`-Aufruf an den folgenden Endpunkt durchführen:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys
```
{: codeblock}

1. [Rufen Sie das Berechtigungstoken, die Organisations-GUID und die Bereichs-GUID ab, um im Service mit Schlüsseln arbeiten zu können.](/docs/services/keymgmt/keyprotect_authentication.html)
2. Führen Sie den folgenden cURL-Befehl aus, um allgemeine Merkmale Ihres Schlüssels anzuzeigen.

    ```cURL
    curl -X GET \
    https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <OAuth_token>' \
    -H 'bluemix-org: <organization_GUID>' \
    -H 'bluemix-space: <space_GUID>' \
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
        <td><em>space_GUID</em></td>
        <td>Die eindeutige ID, die Ihrem {{site.data.keyword.cloud_notm}}-Bereich zugewiesen ist.</td>
      </tr>
      <tr>
        <td><em>organization_GUID</em></td>
        <td>Die eindeutige ID, die Ihrer {{site.data.keyword.cloud_notm}}-Organisation zugewiesen ist.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabelle 1. Beschreibt die Variablen, die zum Anzeigen von Schlüsseln über die {{site.data.keyword.keymanagementserviceshort}}-API erforderlich sind.</caption>
    </table>

    Eine erfolgreiche Anforderung gibt eine Gruppe von Schlüsseln zurück, die in Ihrem {{site.data.keyword.cloud_notm}}-Bereich vorhanden sind.

    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.kms.key+json",
        "collectionTotal": 2
      },
    "resources": [
      {
          "id": "Key ID 1",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Key alias",
          "description": "Key description",
          "state": 1,
          "algorithmType": "AES",
          "createdBy": "v4 UUID of the user who creates the key",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "Key length",
            "mode": "GCM"
          }
        },
        {
          "id": "Key ID 2",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Key alias",
          "description": "Key description",
          "state": 1,
          "algorithmType": "AES",
          "createdBy": "v4 UUID of the user who creates the key",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "Key length",
            "mode": "GCM"
          }
        }
      ]
    }
    ```
    {:screen}

### Schritt 2: Schlüssel nach ID abrufen
{: #retrieve_key_api}

Um detaillierte Informationen zu einem bestimmten Schlüssel anzuzeigen, können Sie einen weiteren `GET`-Aufruf für den folgenden Endpunkt durchführen:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID>
```
{: codeblock}

1. [Rufen Sie das Berechtigungstoken, die Organisations-GUID und die Bereichs-GUID ab, um im Service mit Schlüsseln arbeiten zu können.](/docs/services/keymgmt/keyprotect_authentication.html)
2. Rufen Sie die ID des Schlüssels ab, auf den Sie zugreifen möchten.

    Der ID-Wert wird für den Zugriff auf ausführliche Informationen zu dem Schlüssel (z. B. auf die Schlüsselinformationen selbst) verwendet. Sie können die ID für einen angegebenen Schlüssel abrufen, indem Sie die Anforderung `GET v2/keys` absetzen oder indem Sie auf die {{site.data.keyword.keymanagementserviceshort}}-GUI zugreifen.

3. Führen Sie den folgenden cURL-Befehl aus, um Details zu Ihrem Schlüssel und die Schlüsselinformationen abzurufen.

    ```cURL
    curl -X GET \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID> \
      -H 'accept: application/vnd.ibm.kms.secret+json' \
      -H 'authorization: Bearer <OAuth_token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
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
        <td><em>OAuth_token</em></td>
        <td>Ihr Berechtigungstoken. Nehmen Sie den vollständigen Inhalt des Tokens einschließlich des Werts für Bearer in die cURL-Anforderung auf.</td>
      </tr>
      <tr>
        <td><em>organization_GUID</em></td>
        <td>Die eindeutige ID, die Ihrer {{site.data.keyword.cloud_notm}}-Organisation zugewiesen ist.</td>
      </tr>
      <tr>
        <td><em>space_GUID</em></td>
        <td>Die eindeutige ID, die Ihrem {{site.data.keyword.cloud_notm}}-Bereich zugewiesen ist.</td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>Optional: Die eindeutige ID, die zum Überwachen und Korrelieren von Transaktionen verwendet wird.</td>
      </tr>
      <tr>
        <td><em>key_ID</em></td>
        <td>Die ID für den Schlüssel, der in [Schritt 1](#retrieve_keys_api) abgerufen wurde.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabelle 2. Beschreibt die Variablen, die zum Anzeigen eines angegebenen Schlüssels über die {{site.data.keyword.keymanagementserviceshort}}-API erforderlich sind.</caption>
    </table>

    Eine erfolgreiche Antwort gibt Details zu Ihrem Schlüssel und zu den Schlüsselinformationen zurück. Das folgende JSON-Objekt zeigt ein Beispiel für einen zurückgegebenen Wert.

    ```
    {
        "metadata": {
            "collectionTotal": 1,
            "collectionType": "application/vnd.ibm.kms.key+json"
        },
    "resources": [
      {
                "createdBy": "...",
                "creationDate": "...",
                "id": "...",
                "name": "...",
                "payload": "...",
                "state": 1,
                "type": "application/vnd.ibm.kms.key+json"
            }
        ]
    }
    ```
    {:screen}

    Die [REST-API-Referenzdokumentation![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/apidocs/639){: new_window} zu {{site.data.keyword.keymanagementserviceshort}} enthält eine detaillierte Beschreibung zu den verfügbaren Parametern.
