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

# Schlüssel löschen
{: #deleting-keys}

Sie können {{site.data.keyword.keymanagementservicefull}} verwenden, um einen Verschlüsselungsschlüssel und seinen Inhalt zu löschen, wenn Sie der Administrator Ihres {{site.data.keyword.cloud_notm}}-Bereichs oder der {{site.data.keyword.keymanagementserviceshort}}-Serviceinstanz sind.
{: shortdesc}

**Wichtig:** Wenn Sie einen Schlüssel löschen, dann werden sein Inhalt und die zugehörigen Daten permanent vernichtet. Die Aktion kann nicht rückgängig gemacht werden. Das Löschen von Ressourcen wird in Produktionsumgebungen nicht empfohlen. Diese Vorgehensweise kann jedoch in temporären Umgebungen (z. B. in Testumgebungen oder QA-Umgebungen) von Nutzen sein.

## Schlüssel mit GUI löschen
{: #gui}

Wenn Sie die Löschung von Verschlüsselungsschlüssel über eine grafische Oberfläche bevorzugen, dann können Sie hierzu die {{site.data.keyword.keymanagementserviceshort}}-GUI verwenden.

[Nach dem Erstellen oder Importieren der vorhandenen Schlüssel in den Service](/docs/services/keymgmt/keyprotect_create_keys.html) müssen Sie die folgenden Schritte ausführen, um einen Schlüssel zu löschen:

1. [Melden Sie sich bei der {{site.data.keyword.cloud_notm}}-Konsole ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.bluemix.net/) an.
2. Wählen Sie im {{site.data.keyword.cloud_notm}}-Dashboard die bereitgestellte Instanz von {{site.data.keyword.keymanagementserviceshort}} aus.
3. Navigieren Sie zur Tabelle **Schlüssel**, um die Schlüssel in Ihrem Service zu suchen.
4. Klicken Sie auf das Symbol, um eine Liste mit Optionen für den Schlüssel zu öffnen, den Sie löschen möchten.
5. Klicken Sie im Auswahlmenü auf **Schlüssel löschen** und bestätigen Sie die Schlüssellöschung in der nächsten Anzeige.

Sobald der Schlüssel gelöscht wurde, nimmt der Schlüssel den Zustand _Gelöscht_ an. Schlüssel, die sich in diesem Zustand befinden, sind nicht wiederherstellbar. Die zugehörigen Metadaten für den Schlüssel (z. B. das Löschdatum des Schlüssels) werden in der {{site.data.keyword.keymanagementserviceshort}}-Datenbank aufbewahrt.

## Schlüssel mit API löschen
{: #api}

Um einen Schlüssel und seinen Inhalt zu löschen, müssen Sie einen `DELETE`-Aufruf zum folgenden Endpunkt absetzen:

```
https://keyprotect.us-south.bluemix.net/api/v2/keys<key_ID>
```

1. [Rufen Sie Ihren Service- und Authentifizierungsnachweis ab, um mit den Schlüsseln im Service zu arbeiten.](/docs/services/keymgmt/keyprotect_authentication.html)

2. Rufen Sie die ID des Schlüssels ab, den Sie löschen möchten.

    Sie können die ID für einen angegebenen Schlüssel abrufen, indem Sie die Anforderung `GET /v2/keys/` absetzen oder indem Sie die Schlüssel im {{site.data.keyword.keymanagementserviceshort}}-Dashboard anzeigen.

3. Führen Sie den folgenden cURL-Befehl aus, um den Schlüssel und seinen Inhalt dauerhaft zu löschen.

    ```cURL
    curl -X DELETE \
      https://keyprotect.us-south.bluemix.net/api/v2/keys<key_ID> \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'prefer: <return_preference>'
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
        <td><em>key_ID</em></td>
        <td>Die eindeutige ID für den Schlüssel, der gelöscht werden soll.</td>
      </tr>
      <tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p>Ein Header, der das Serververhalten für <code>POST</code>- und <code>DELETE</code>-Operationen ändert.</p><p>Wenn Sie die Variable <em>return_preference</em> auf <code>return=minimal</code> festlegen, gibt der Service eine erfolgreiche Antwort auf das Löschen zurück. Wenn Sie die Variable <code>return=representation</code> festlegen, werden sowohl die Schlüsselinformationen als auch die Metadaten des Schlüssels zurückgegeben.</p></td>
      </tr>
      <caption style="caption-side:bottom;">Tabelle 1. Beschreibt die Variablen, die zum Löschen von Schlüsseln über die {{site.data.keyword.keymanagementserviceshort}}-API erforderlich sind.</caption>
    </table>

    Wenn die Variable _return_preference_ auf `return=representation` festgelegt wird, werden die Details der Anforderung `DELETE` im Entitätshauptteil der Antwort zurückgegeben. <!--After you delete a key, it enters the `Deactivated` key state. After 24 hours, if a key is not reinstated, the key transitions to the `Destroyed` state. The key contents are permanently erased and no longer accessible.--> Das folgende JSON-Objekt zeigt ein Beispiel für einen zurückgegebenen Wert.
    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.kms.key+json",
       "collectionTotal": 1
      },
    "resources": [
      {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "...",
          "description": "...",
          "state": 5,
          "crn": "...",
          "deleted": true,
          "algorithmType": "AES",
          "createdBy": "...",
          "deletedBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "deletionDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "nonactiveStateReason": 2,
          "extractable": true
        }
      ]
    }
    ```
    {: screen}

    Die [REST-API-Referenzdokumentation![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/apidocs/639){: new_window} zu {{site.data.keyword.keymanagementserviceshort}} enthält eine detaillierte Beschreibung zu den verfügbaren Parametern.
