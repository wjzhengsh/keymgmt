---

copyright:
  years: 2017
lastupdated: "2017-08-03"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Schlüssel verwalten

Sie können den Lebenszyklus Ihrer Schlüssel mithilfe von {{site.data.keyword.keymanagementservicelong}} für {{site.data.keyword.Bluemix_short}} verwalten.
{: shortdesc}

Bewährt hat sich die sichere Verwaltung Ihrer Schlüssel während der Entwicklung des Codes. Beachten Sie neben einigen anderen sicheren Verfahren der Codierungspraxis zum Beispiel auch Leitlinien wie die folgenden.

- Berücksichtigen Sie Auswirkungen auf die Sicherheit, wenn Sie Schlüssel in Ihren Code einbetten.
- Erstellen Sie Schlüssel nur für den programmgestützten Zugriff auf Ihre Apps und Ressourcen. Erstellen Sie keine Schlüssel, wenn Sie einfachere [Benutzerberechtigungen![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.bluemix.net/docs/admin/patterns.html#userroles "Symbol für externen Link"){: new_window} erstellen können.
- Wechseln Sie Schlüssel regelmäßig (Schlüsselrotation) und entfernen Sie nicht genutzte Schlüssel.
- Verwenden Sie eine Mehrfaktorauthentifizierung für kritische Operationen.
- Isolieren Sie Apps, indem Sie separate Schlüssel für jede App verwalten.
- Ziehen Sie die Verwendung der programmgesteuerten API in Betracht, wenn Sie besonders sensible Informationen übertragen.

## Authentifizierungsnachweise für die {{site.data.keyword.keymanagementserviceshort}}-API generieren
{: #authentication_api}

{{site.data.keyword.keymanagementservicelong_notm}} stellt eine REST-API bereit, die mit jeder Programmiersprache verwendet werden kann, um Schlüssel zu speichern, abzurufen und zu generieren.

Um mit der API zu arbeiten, müssen Sie eigene Authentifizierungs- und Serviceberechtigungsnachweise generieren.

1. Melden Sie sich über die Cloud Foundry-CLI bei {{site.data.keyword.Bluemix_notm}} an.

    ```
    cf login [a api.DomainName] [-sso]
    ```
    {: codeblock}

2. Wählen Sie die Organisation und den Bereich von {{site.data.keyword.Bluemix_notm}} aus, in denen Ihre Key Protect-Serviceinstanz enthalten ist. Notieren Sie sich die Namen Ihrer Organisation und Ihres Bereichs in der CLI-Ausgabe. Sie können auch `cf target` ausführen, um diese Informationen anzuzeigen.
3. Rufen Sie Ihre {{site.data.keyword.Bluemix_notm}}-Organisations- und Bereichs-GUIDs ab.

    ```
    cf org organization_name --guid
    cf space space_name --guid
    ```
    {: codeblock}

4. Fordern Sie ein {{site.data.keyword.Bluemix_notm}}-Zugriffstoken an.

    ```
    cf oauth-token
    ```
    {: codeblock}

    Im folgenden gekürzten Beispiel sehen Sie die {{site.data.keyword.Bluemix_notm}}-Tokenausgabe. Die Variable _bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7_ ist ein Beispiel für ein Zugriffstoken.

    ```
    bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7...
    ```
    {: screen}

Weitere Schritte:

Die [REST-API-Referenzdokumentation![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/apidocs/639 "Symbol für externen Link"){: new_window} zu {{site.data.keyword.keymanagementserviceshort}} enthält Informationen zur Verwaltung von Schlüsseln in Ihrem Bereich.


## Schlüssel mit der {{site.data.keyword.keymanagementserviceshort}}-API erstellen
{: #codingapps}

Mit der {{site.data.keyword.keymanagementservicelong_notm}}-API können Sie vorhandene Schlüssel schützen oder neue Schlüssel generieren.

Um Schlüssel zu erstellen oder vorhandene Schlüssel hinzuzufügen, senden Sie einen **POST**-Aufruf an den folgenden Endpunkt:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/secrets
```
{: codeblock}

Wenn Sie den Service zuerst testen möchten, bevor Sie eigene Schlüssel hinzufügen, können Sie die [Beispiel-App![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/IBM-Bluemix/key-protect-helloworld-python "Symbol für externen Link"){: new_window} verwenden.

1. [Rufen Sie Ihr {{site.data.keyword.Bluemix_notm}}-Zugriffstoken, die Organisations-GUID und die Bereichs-GUID ab, um mit den Schlüsseln im Service zu arbeiten.](#authentication_api).

2. Rufen Sie die [{{site.data.keyword.keymanagementserviceshort}}-API](https://console.ng.bluemix.net/apidocs/639) mit dem folgenden cURL-Befehl auf.

  ```cURL
  curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: Bluemix-Zugriffstoken' --header 'Bluemix-Space: Bereichs-GUID' --header 'Bluemix-Org: Organisations-GUID' -d '{
    "metadata": {
      "collectionType": "application/vnd.ibm.kms.secret+json",
      "collectionTotal": 1
    },
    "resources": [
      {
      "type": "application/vnd.ibm.kms.secret+json",
      "name": "key_alias",
      "description": "key_description",
      "expirationDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
      "payload": "key_contents"
      }
    ]
  }' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets'
  ```
  {: codeblock}

  Ersetzen Sie die Variablen in der Beispielanforderung mithilfe der folgenden Tabelle.
  <table>
    <tr>
      <th>Variable</th>
      <th>Beschreibung</th>
    </tr>
    <tr>
      <td><em>Bluemix-Zugriffstoken</em></td>
      <td>Ihr Berechtigungstoken. Nehmen Sie den vollständigen Inhalt des Tokens einschließlich des Werts für Bearer in die cURL-Anforderung auf.</td>
    </tr>
    <tr>
      <td><em>Bereichs-GUID</em></td>
      <td>Die Kennung für Ihren {{site.data.keyword.Bluemix_notm}}-Bereich.</td>
    </tr>
    <tr>
      <td><em>Organisations-GUID</em></td>
      <td>Die Kennung für Ihre {{site.data.keyword.Bluemix_notm}}-Organisation.</td>
    </tr>
    <tr>
      <td><em>Schlüsselalias</em></td>
      <td>Ein lesbarer Name zur einfachen Identifikation Ihres Schlüssels.</td>
    </tr>
    <tr>
      <td><em>Schlüsselbeschreibung</em></td>
      <td>Eine erweiterte Beschreibung Ihres Schlüssels.</td>
    </tr>
    <tr>
      <td><em>JJJJ-MM-TT</em><br><em>HH:MM:SS.SS</em></td>
      <td>Optional: Der Zeitpunkt (Datum und Uhrzeit), an dem der Schlüssel im System abläuft, im RFC3339-Format. Wenn das Attribut <code>expirationDate</code> fehlt, bleibt der Schlüssel unbegrenzt gültig. </td>
    </tr>
    <tr>
      <td><em>Schlüsselinhalt</em></td>
      <td>Die Schlüsselinformationen (z. B. ein RSA-Schlüssel), die Sie in {{site.data.keyword.keymanagementserviceshort}} speichern möchten. Lassen Sie für die Generierung eines neuen Schlüssels das Attribut payload und die Variable key_contents weg. </td>
    </tr>
      <caption style="caption-side:bottom;">Tabelle 1. Für das Hinzufügen von Schlüsseln über die {{site.data.keyword.keymanagementserviceshort}}-API erforderliche Variablen</caption>
  </table>

3. Stellen Sie sicher, dass der Schlüssel durch Ausführen des folgenden Aufrufs zum Abrufen der Schlüssel in Ihrem {{site.data.keyword.Bluemix_notm}}-Bereich erstellt wurde.

  ```cURL
  curl -X GET --header 'Accept: application/json' --header 'Authorization: Bluemix-Zugriffstoken' --header 'Bluemix-Space: Bereichs-GUID' --header 'Bluemix-Org: Organisations-GUID' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets'
  ```
  {: codeblock}

## Schlüssel mit der {{site.data.keyword.keymanagementserviceshort}}-API anzeigen
{: #viewingkeys_api}

Sie können den Inhalt Ihrer Schlüssel über die {{site.data.keyword.keymanagementservicelong_notm}}-API anzeigen, wenn Sie ein {{site.data.keyword.Bluemix_notm}}-Bereichsmanager oder -Entwickler sind.

Für eine übergeordnete Ansicht können Sie die Schlüssel durchsuchen, die in Ihrem Bereich über die Benutzerschnittstelle von {{site.data.keyword.keymanagementserviceshort}} verwaltet werden.

Um detaillierte Informationen zu Ihren Schlüsseln anzuzeigen, senden Sie einen GET-Aufruf an den folgenden Endpunkt:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/secrets/key_ID
```
{: codeblock}

1. In der Benutzerschnittstelle von {{site.data.keyword.keymanagementserviceshort}} können Sie bei den Sicherheitsservices allgemeine Merkmale zu Ihren Schlüsseln anzeigen. Sie können Schlüssel durchsuchen, indem Sie auf die Überschriften der sortierbaren Spalten klicken.
2. Kopieren Sie die **ID** in der Zeile des Schlüssels. Der ID-Wert wird für den Zugriff auf ausführlichere Informationen zu dem Schlüssel in der API (z. B. die Schlüsselinformationen selbst) verwendet.
3. [Rufen Sie Ihr {{site.data.keyword.Bluemix_notm}}-Zugriffstoken, die Organisations-GUID und die Bereichs-GUID ab, um mit den Schlüsseln im Service zu arbeiten.](#authentication_api)
4. Führen Sie den folgenden cURL-Befehl aus, um Details zu Ihrem Schlüssel und die Schlüsselinformationen abzurufen.

  ```cURL
  curl -X GET --header 'Accept: application/json' --header 'Authorization: Bluemix-Zugriffstoken' --header 'Bluemix-Space: Bereichs-GUID' --header 'Bluemix-Org: Organisations-GUID' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets/Schlüssel-ID'
  ```
  {: codeblock}

  Ersetzen Sie die Variablen in der Beispielanforderung mithilfe der folgenden Tabelle.
  <table>
    <tr>
      <th>Variable</th>
      <th>Beschreibung</th>
    </tr>
    <tr>
      <td><em>Bluemix-Zugriffstoken</em></td>
      <td>Ihr Berechtigungstoken. Nehmen Sie den vollständigen Inhalt des Tokens einschließlich des Werts für Bearer in die cURL-Anforderung auf.</td>
    </tr>
    <tr>
      <td><em>Bereichs-GUID</em></td>
      <td>Die zufällig generierte ID, die Ihrem {{site.data.keyword.Bluemix_notm}}-Bereich zugewiesen ist.</td>
    </tr>
    <tr>
      <td><em>Organisations-GUID</em></td>
      <td>Die zufällig generierte ID, die Ihrer {{site.data.keyword.Bluemix_notm}}-Organisation zugewiesen ist. </td>
    </tr>
    <tr>
      <td><em>Schlüssel-ID</em></td>
      <td>Die Kennung für Ihren Schlüssel, die Sie in Schritt [2](https://console.bluemix.net/docs/services/keymgmt/managing.html#viewingkeys_api__keyid) abgerufen haben.</td>
    </tr>
    <caption style="caption-side:bottom;">Tabelle 2. Beschreibt die Variablen, die zum Anzeigen von Schlüsseln über die {{site.data.keyword.keymanagementserviceshort}}-API erforderlich sind. </caption>
  </table>

  Die Schlüsselinformationen werden im Entitätshauptteil der Antwort zurückgegeben. Von den Hardwaresicherheitsmodulen (HSMs) generierte Schlüssel verfügen über eine Base64-Codierung.

## Schlüssel und Zugriff prüfen
{: #viewkeyassignments}

{{site.data.keyword.keymanagementservicelong_notm}} stellt ein zentrales System zum Anzeigen, Verwalten und Prüfen Ihrer Verschlüsselungsschlüssel bereit. Prüfen Sie Ihre Schlüssel und Zugriffsbeschränkungen für Schlüssel, um die Sicherheit Ihrer Ressourcen sicherzustellen.

Prüfen Sie Ihre Schlüsselkonfiguration regelmäßig:

- Untersuchen Sie, wann die Schlüssel erstellt wurden und stellen Sie fest, ob es an der Zeit ist, den Schlüssel zu wechseln.
- [Überwachen Sie API-Aufrufe für {{site.data.keyword.keymanagementserviceshort}} mit {{site.data.keyword.cloudaccesstrailshort}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.bluemix.net/docs/services/AccessTrail/at_integration.html#at_integration_key_protect "Symbol für externen Link"){: new_window}.
- Untersuchen Sie, welche Benutzer auf Schlüssel zugreifen können, und ob entsprechende Zugriffsberechtigungen erteilt wurden.

Gehen Sie wie folgt vor, um für Benutzer mit Zugriff ein Audit durchzuführen:

1. Rufen Sie als Bereichsmanager Ihre Kontoeinstellungen auf und wählen Sie **Organisationen verwalten** aus.
2. Öffnen Sie den Bereich, der die {{site.data.keyword.keymanagementserviceshort}}-Serviceinstanz enthält, um zu prüfen, welche Benutzer Zugriff haben.
3. Wenn Benutzer hinzugefügt werden müssen, rufen Sie **Teammitglieder einladen** auf und wählen Sie die {{site.data.keyword.Bluemix_notm}}-Rollen aus, die den {{site.data.keyword.keymanagementserviceshort}}-Berechtigungen entsprechen, die Sie dem betreffenden Benutzer erteilen möchten.

  <table>
    <tr>
      <th>{{site.data.keyword.Bluemix_notm}}-Rollen</th>
      <th>{{site.data.keyword.keymanagementserviceshort}}-Berechtigungen</th>
    </tr>
    <tr>
      <td>Bereichsmanager</td>
      <td>Ein Bereichsmanager kann Schlüssel erstellen, anzeigen und löschen.</td>
    </tr>
    <tr>
      <td>Entwickler</td>
      <td>Ein Entwickler kann Schlüssel erstellen und Schlüsseldetails anzeigen.</td>
    </tr>
    <tr>
      <td>Auditor</td>
      <td>Ein Auditor kann auf eine übergeordnete Ansicht der Schlüssel zugreifen. </td>
    </tr>
    <caption style="caption-side:bottom;">Tabelle 3. Zuordnung von {{site.data.keyword.Bluemix_notm}}-Rollen zu {{site.data.keyword.keymanagementserviceshort}}-Berechtigungen.</caption>
  </table>
