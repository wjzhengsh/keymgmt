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

# Schlüssel einschließen
{: #wrapping-keys}

Sie als privilegierter Benutzer können Ihre Verschlüsselungsschlüssel mit dem Rootschlüssel mithilfe der {{site.data.keyword.keymanagementservicelong}}-API verwalten und schützen.
{: shortdesc}

Wenn Sie einen Datenverschlüsselungsschlüssel (DEK) mit einem Rootschlüssel einschließen, kombiniert {{site.data.keyword.keymanagementserviceshort}} die Stärke mehrerer Algorithmen, um den Datenschutz und die Integrität Ihrer verschlüsselten Daten zu gewährleisten.  

Informationen darüber, wie Key-Wrapping Sie unterstützt, die Sicherheit ruhender Daten in der Cloud zu gewährleisten, finden Sie in [Envelope-Verschlüsselung](/docs/services/keymgmt/keyprotect_envelope.html).

## Schlüssel mithilfe der API einschließen
{: #api}

Sie können einen bestimmten Datenverschlüsselungsschlüssel (DEK) mit einem Rootschlüssel schützen, den Sie in {{site.data.keyword.keymanagementserviceshort}} verwalten.

**Wichtig:** Wenn Sie einen Rootschlüssel für das Wrapping bereitstellen, stellen Sie sicher, dass der Rootschlüssel 256, 384 oder 512 Bit groß ist, damit der Wrapping-Aufruf erfolgreich ist. Wenn Sie einen Rootschlüssel im Service erstellen, generiert {{site.data.keyword.keymanagementserviceshort}} einen 256-Bit-Schlüssel aus den HSMs, der vom AES-GCM-Algorithmus unterstützt wird.

[Nach der Angabe eines Rootschlüssels im Service](/docs/services/keymgmt/keyprotect_create_keys.html) können Sie einen DEK mit der erweiterten Verschlüsselung mithilfe eines `POST`-Aufrufs zum folgenden Endpunkt einschließen:

```
https://keyprotect.us-south.bluemix.net/api/v2/keys<key_ID>?action=wrap
```
{: codeblock}

1. [Rufen Sie Ihren Service- und Authentifizierungsnachweis ab, um mit den Schlüsseln im Service zu arbeiten.](/docs/services/keymgmt/keyprotect_authentication.html)

2. Kopieren Sie die Schlüsselinformationen, die Sie verwalten und schützen möchten.

    Wenn Sie einen Administrator oder einen Bearbeiterzugriff für Ihre {{site.data.keyword.keymanagementserviceshort}}-Serviceinstanz haben, [können Sie die Schlüsselinformationen für einen bestimmten Schlüssel mit der Anforderung `GET /v2/keys/<key_ID>` abrufen](/docs/services/keymgmt/keyprotect_view_keys.md#retrieve_key_api).

3. Kopieren Sie die ID des Rootschlüssels, den Sie für das Wrapping verwenden möchten.

4. Führen Sie den folgenden cURL-Befehl aus, um den Schlüssel mit einer Wrapping-Operation zu schützen.

    ```cURL
    curl -X POST \
      'https://keyprotect.us-south.bluemix.net/api/v2/keys<key_ID>?action=wrap' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
      "plaintext": "<data_key>",
      "aad": ["<additional_data>", "<additional_data>"]
    }'
    ```
    {: codeblock}

    Um mit Schlüsseln in bestimmten Cloud Foundry-Organisationen und -Bereichen zu arbeiten, ersetzen Sie `Bluemix-Instance` durch die entsprechenden Header `Bluemix-org` und `Bluemix-space`. [Siehe auch die Codebeispiele in der {{site.data.keyword.keymanagementserviceshort}}-API-Referenzdokumentation ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
    {: tip}

    Ersetzen Sie die Variablen in der Beispielanforderung mithilfe der folgenden Tabelle.

    <table>
      <tr>
        <th>Variable</th>
        <th>Beschreibung</th>
      </tr>
      <tr>
        <td><em>key_ID</em></td>
        <td>Die eindeutige ID für den Rootschlüssel, der für das Einschließen (Wrapping) verwendet werden soll. Der Rootschlüssel muss 256, 384 oder 512 Bit groß sein, damit der Wrapping-Aufruf erfolgreich ist.</td>
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
        <td><em>data_key</em></td>
        <td>Optional: Die Schlüsselinformationen des DEK, den Sie verwalten und schützen möchten. Der Wert <code>plaintext</code> muss base64-codiert sein. Um einen neuen DEK zu generieren, lassen Sie das Attribut <code>plaintext</code> weg. Der Service generiert einen beliebigen Klartext (32 Byte) und schließt den Wert ein.</td>
      </tr>
      <tr>
        <td><em>additional_data</em></td>
        <td>Optional: Die zusätzlichen Authentifizierungsdaten (AAD), die für die weitere Sicherung des Schlüssels verwendet werden. Jede Zeichenfolge kann bis zu 255 Zeichen enthalten. Wenn AAD bei einer Wrapping-Aufruf für den Service angegeben wird, müssen Sie dieselben AAD während des nachfolgenden Unwrap-Aufrufs verwenden.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabelle 1. Beschreibt die Variablen, die zum Einschließen eines bestimmten Schlüssels in {{site.data.keyword.keymanagementserviceshort}} erforderlich sind.</caption>
    </table>

    Ihr eingeschlossener Schlüssel, der die base64-codierten Schlüsselinformationen enthält, wird in im Entitätshauptteil der Antwort zurückgegeben. Das folgende JSON-Objekt zeigt ein Beispiel für einen zurückgegebenen Wert.

    ```
    {
      "plaintext": "s~Rz@kN9Fzv\\/hP*r3LY-?O@!!qdtj:L",
      "ciphertext": "eyJjaXBoZXJ0ZXh0Ijoic3VLSDNRcmdEZjdOZUw4Rkc4L2FKYjFPTWcyd3A2eDFvZlA4MEc0Z1B2RmNrV2g3cUlidHphYXU0eHpKWWoxZyIsImhhc2giOiJiMmUyODdkZDBhZTAwZGZlY2Q3OGJmMDUxYmNmZGEyNWJkNGUzMjBkYjBhN2FjNzVhMWYzZmNkMDZlMjAzZWYxNWM5MTY4N2JhODg2ZWRjZGE2YWVlMzFjYzk2MjNkNjA5YTRkZWNkN2E5Y2U3ZDc5ZTRhZGY1MWUyNWFhYWM5MjhhNzg3NmZjYjM2NDFjNTQzMTZjMjMwOGY2MThlZGM2OTE3MjAyYjA5YTdjMjA2YzkxNTBhOTk1NmUxYzcxMTZhYjZmNmQyYTQ4MzZiZTM0NTk0Y2IwNzJmY2RmYTk2ZSJ9"
      "aad": ["data1", "data2"]
    }
    ```
    {:screen}
