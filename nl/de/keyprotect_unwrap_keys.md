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

# Wrapping von Schlüssel aufheben
{: #unwrapping-keys}

Sie als privilegierter Benutzer können das Wrapping Ihrer Datenverschlüsselungsschlüssel (DEK) aufheben, um mithilfe der {{site.data.keyword.keymanagementservicefull}}-API auf die Inhalte zuzugreifen. Beim Unwrapping wird der DEK entschlüsselt. Außerdem wird die Integrität seiner Inhalte geprüft. Die ursprünglichen Schlüsselinformationen werden an Ihren {{site.data.keyword.cloud_notm}}-Datenservice zurückgegeben.
{: shortdesc}

Informationen darüber, wie Key-Wrapping Sie unterstützt, die Sicherheit ruhender Daten in der Cloud zu gewährleisten, finden Sie in [Envelope-Verschlüsselung](/docs/services/keymgmt/keyprotect_envelope.html).

## Wrapping von Schlüsseln mithilfe der API aufheben
{: #api}

[Nach dem Absetzen eines Wrapping-Aufrufs für den Service](/docs/services/keymgmt/keyprotect_wrap_keys.html) können Sie das Wrapping eines bestimmten Datenverschlüsselungsschlüssels (DEK) aufheben, um auf seine Inhalte mithilfe eines `POST`-Aufrufs zum folgenden Endpunkt zuzugreifen:

```
https://keyprotect.us-south.bluemix.net/api/v2/keys<key_id>?action=unwrap
```
{: codeblock}

1. [Rufen Sie Ihren Service- und Authentifizierungsnachweis ab, um mit den Schlüsseln im Service zu arbeiten.](/docs/services/keymgmt/keyprotect_authentication.html)

2. Kopieren Sie die ID des Rootschlüssels, mit dem Sie die ursprüngliche Wrapping-Anforderung durchgeführt haben.

    Sie können die ID für einen Schlüssel abrufen, indem Sie die Anforderung `GET /v2/keys/` absetzen oder indem Sie die Schlüssel in der {{site.data.keyword.keymanagementserviceshort}}-GUI anzeigen.

3. Kopieren Sie den Wert `ciphertext`, der während der ursprünglichen Wrapping-Anforderung zurückgegeben wurde.

4. Führen Sie den folgenden cURL-Befehl aus, um die Schlüsselinformationen zu entschlüsseln und zu authentifizieren.

    ```cURL
    curl -X POST \
      'https://keyprotect.us-south.bluemix.net/api/v2/keys<key_ID>?action=unwrap' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
      "ciphertext": "<encrypted_data_key>",
      "aad": ["<additional_data>", "<additional_data>"]
    }'
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
        <td><em>key_ID</em></td>
        <td>Die eindeutige ID für den Rootschlüssel, der für das Einschließen (Wrapping) verwendet wurde. Damit Ihre Unwrapping-Anforderung erfolgreich ist, stellen Sie denselben Rootschlüssel bereit, der während der ursprünglichen Wrapping-Anforderung verwendet wurde.</td>
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
      <tr>
        <td><em>return_preference</em></td>
        <td><p>Ein Header, der das Serververhalten für <code>POST</code>- und <code>DELETE</code>-Operationen ändert.</p><p>Wenn Sie die Variable <em>return_preference</em> auf <code>return=minimal</code> setzen, werden im Entitätshauptteil der Antwort nur die Metadaten des Schlüssels zurückgegeben, wie zum Beispiel Schlüsselname und ID-Wert. Wenn Sie die Variable <code>return=representation</code> festlegen, werden sowohl die Schlüsselinformationen als auch die Metadaten des Schlüssels zurückgegeben.</p></td>
      </tr>
      <tr>
        <td><em>additional_data</em></td>
        <td>Optional: Die zusätzlichen Authentifizierungsdaten (AAD), die für die weitere Sicherung des Schlüssels verwendet werden. Jede Zeichenfolge kann bis zu 255 Zeichen enthalten. <br></br>Wichtig: Wenn AAD bei einer Wrapping-Aufruf für den Service angegeben wird, müssen Sie dieselben AAD während des Unwrap-Aufrufs verwenden.</td>
      </tr>
      <tr>
        <td><em>encrypted_data_key</em></td>
        <td>Der Wert <code>ciphertext</code>, der während der Wrapping-Operation zurückgegeben wurde.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabelle 1. Beschreibt die Variablen, die zum Aufheben des Key-Wrappings in {{site.data.keyword.keymanagementserviceshort}} erforderlich sind.</caption>
    </table>

    Die ursprünglichen Schlüsselinformationen werden im Entitätshauptteil der Antwort zurückgegeben. Das folgende JSON-Objekt zeigt ein Beispiel für einen zurückgegebenen Wert.

    ```
    {
      "plaintext": "s~Rz@kN9Fzv\\/hP*r3LY-?O@!!qdtj:L"
    }
    ```
    {:screen}
