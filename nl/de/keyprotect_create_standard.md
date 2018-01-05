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

# Standardschlüssel erstellen
{: #create_standard_keys}

Sie können einen Standardverschlüsselungsschlüssel mit der {{site.data.keyword.keymanagementserviceshort}}-GUI oder programmgesteuert mit der {{site.data.keyword.keymanagementserviceshort}}-API erstellen.
{: shortdesc}

## Standardschlüssel mit der GUI erstellen
{: #create_standard_key_GUI}

[Führen Sie nach dem Erstellen einer Instanz dieses Services](/docs/services/keymgmt/keyprotect_provision.html) die folgenden Schritte aus, um einen Standardschlüssel mit der {{site.data.keyword.keymanagementserviceshort}}-GUI zu erstellen.

1. [Melden Sie sich bei der {{site.data.keyword.cloud_notm}}-Konsole ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.bluemix.net/) an.
2. Wählen Sie im {{site.data.keyword.cloud_notm}}-Dashboard die bereitgestellte Instanz von {{site.data.keyword.keymanagementserviceshort}} aus.
2. Um einen neuen Schlüssel zu erstellen, klicken Sie auf **Schlüssel hinzufügen** und wählen Sie das Fenster **Neuen Schlüssel generieren** aus.

    Geben Sie die Schlüsseldetails an:

    <table>
      <tr>
        <th>Einstellung</th>
        <th>Beschreibung</th>
      </tr>
      <tr>
        <td>Name</td>
        <td>Ein lesbarer Alias, der Ihrem Schlüssel zugewiesen werden soll. Dies kann ein beliebiger Name sein. Er sollte so gewählt sein, dass Sie mit seiner Hilfe den Schlüssel eindeutig erkennen können. Der Name kann z. B. die Art der Schlüsselverwendung bezeichnen oder die Person, der der Schlüssel zugeordnet ist.</td>
      </tr>
      <tr></tr>
        <td>Schlüsseltyp</td>
        <td>Der [Schlüsseltyp](/docs/services/keymgmt/keyprotect_envelope.html#key_types), den Sie in {{site.data.keyword.keymanagementserviceshort}} verwalten möchten. Wählen Sie aus der Liste der Schlüsseltypen <b>Standardschlüssel</b> aus.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabelle 1. Beschreibung der Einstellungen <b>Neuen Schlüssel generieren</b></caption>
    </table>

3. Geben Sie die Details zum Schlüssel ein und klicken Sie dann zum Bestätigen auf **Schlüssel generieren**. 

## Standardschlüssel mit der API erstellen
{: #create_standard_key_API}

Erstellen Sie einen Standardschlüssel, indem Sie einen `POST`-Aufruf zum folgenden Endpunkt absetzen:

```
https://keyprotect.us-south.bluemix.net/api/v2/keys
```
{: codeblock}

1. [Rufen Sie Ihren Service- und Authentifizierungsnachweis ab, um mit den Schlüsseln im Service zu arbeiten.](/docs/services/keymgmt/keyprotect_authentication.html).

2. Rufen Sie die [{{site.data.keyword.keymanagementserviceshort}}-API](https://console.ng.bluemix.net/apidocs/639) mit dem folgenden cURL-Befehl auf.

    ```cURL
    curl -X POST \
      https://keyprotect.us-south.bluemix.net/api/v2/keys \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
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
       "extractable": true
       }
     ]
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
        <td><em>IAM_token</em></td>
        <td>Ihr Berechtigungstoken. Nehmen Sie den vollständigen Inhalt des <code>IAM</code>-Tokens einschließlich des Werts für Bearer in die cURL-Anforderung auf.</td>
      </tr>
      <tr>
        <td><em>instance_ID</em></td>
        <td>Die eindeutige ID, die Ihrer {{site.data.keyword.keymanagementserviceshort}}-Serviceinstanz zugewiesen ist.</td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>Die eindeutige ID, die zum Überwachen und Korrelieren von Transaktionen verwendet wird.</td>
      </tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p>Optional: Ein Header, der das Serververhalten für <code>POST</code>- und <code>DELETE</code>-Operationen ändert.</p><p>Wenn Sie die Variable <em>return_preference</em> auf <code>return=minimal</code> setzen, werden im Entitätshauptteil der Antwort nur die Metadaten des Schlüssels zurückgegeben, wie zum Beispiel Schlüsselname und ID-Wert. Wenn Sie die Variable <code>return=representation</code> festlegen, werden sowohl die Schlüsselinformationen als auch die Metadaten Ihres Standardschlüssels zurückgegeben.</p></td>
      </tr>
      <tr>
        <td><em>key_alias</em></td>
        <td>Ein eindeutiger, lesbarer Name zur einfachen Identifikation Ihres Schlüssels.</td>
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
        <td><em>key_type</em></td>
        <td>
          <p>Ein boolescher Wert, der bestimmt, ob die Schlüsselinformationen den Service verlassen dürfen.</p>
          <p>Wenn das Attribut <code>extractable</code> auf <code>true</code> festgelegt wird, erstellt der Service einen Standardschlüssel, den Sie in Ihren Apps oder Services speichern können.</p>
        </td>
      </tr>
        <caption style="caption-side:bottom;">Tabelle 2. Variablen, die erforderlich sind, um einen Standardschlüssel mithilfe der {{site.data.keyword.keymanagementserviceshort}}-API hinzuzufügen</caption>
    </table>

    Mit der erfolgreichen Antwort `POST /v2/keys/` werden der ID-Wert für Ihren Schlüssel sowie andere Metadaten zurückgegeben. Die ID ist eine eindeutige Kennung, die Ihrem Schlüssel zugeordnet ist und die für alle nachfolgenden Aufrufe für die {{site.data.keyword.keymanagementserviceshort}}-API verwendet wird.

3. Optional: Stellen Sie sicher, dass der Schlüssel durch Ausführen des folgenden Aufrufs zum Abrufen der Schlüssel in Ihrer {{site.data.keyword.keymanagementserviceshort}}-Serviceinstanz erstellt wurde.

    ```cURL
    curl -X GET \
      https://keyprotect.us-south.bluemix.net/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}


### Weitere Schritte

- Weitere Informationen zum programmgesteuerten Management Ihrer Schlüssel [finden Sie in der API-Referenzdokumentation von {{site.data.keyword.keymanagementserviceshort}} für Codebeispiele ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
- Zur Anzeige eines Beispiels zur Art und Weise, in der Schlüsselspeicher in {{site.data.keyword.keymanagementserviceshort}} eingesetzt werden können, um Daten zu ver- und entschlüsseln, [überprüfen Sie die Beispielapp in GitHub ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.
