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

# Auf die API zugreifen
{: #access-api}

{{site.data.keyword.keymanagementservicefull}} stellt eine REST-API bereit, die mit jeder Programmiersprache verwendet werden kann, um Schlüssel zu speichern, abzurufen und zu generieren.
{: shortdesc}

Um mit der API zu arbeiten, müssen Sie eigene Service- und Authentifizierungsnachweise generieren. 

## Ein Zugriffstoken abrufen
{: #retrieve_token}

Die Authentifizierung mit {{site.data.keyword.keymanagementserviceshort}} erfolgt durch das Abrufen eines Zugriffstokens aus {{site.data.keyword.iamshort}}. Sie können mit einer [Service-ID](/docs/iam/serviceid.html) mit der {{site.data.keyword.keymanagementserviceshort}}-API für Ihren Service oder für Ihre Anwendung sowie außerhalb von {{site.data.keyword.cloud_notm}} arbeiten, ohne Ihren persönlichen Benutzerberechtigungsnachweis freizugeben.  

Bei einer Authentifizierung mit Ihrem Benutzerberechtigungsnachweis können Sie Ihr Token abrufen, indem Sie `bx iam oauth-tokens` in der [{{site.data.keyword.cloud_notm}}-CLI (bx) ausführen ![Symbol für externen Link](../../icons/launch-glyph.svg "External link icon")](/docs/cloud-platform/cli/reference/bluemix_cli/get_started.html#getting-started){: new_window}.
{: tip}

Führen Sie die folgenden Schritte aus, um ein Zugriffstoken abzurufen:

1. Gehen Sie in der {{site.data.keyword.cloud_notm}}-Konsole zu **Verwalten** &gt; **Sicherheit** &gt; **Identität und Zugriff** &gt; **Service-IDs**. Befolgen Sie die Anweisungen, um [eine Service-ID zu erstellen.](/docs/iam/serviceid.html#creating-a-service-id){: new_window}
2. Verwenden Sie das Menü **Aktionen**, um [eine Zugriffsrichtlinie für Ihre neue Service-ID zu definieren.](/docs/iam/serviceidaccess.html#assigning-new-access){: new_window} 
    
    Weitere Informationen zum Verwalten des Zugriffs für Ihre {{site.data.keyword.keymanagementserviceshort}}-Ressourcen finden Sie in [Rollen und Berechtigungen](/docs/services/keymgmt/keyprotect_manage_access.md#roles).
3. Verwenden Sie den Abschnitt **API-Schlüssel**, um [einen API-Schlüssel zu erstellen, der der Service-ID zugeordnet wird.](/docs/iam/serviceid_keys.html#creating-an-api-key-for-a-service-id){: new_window} Speichern Sie Ihren API-Schlüssel, indem Sie ihn an eine sichere Position herunterladen.
4. Rufen Sie die {{site.data.keyword.iamshort}}-API auf, um Ihr Zugriffstoken abzurufen.

    ```cURL
    curl -X POST \
      "https://iam.bluemix.net/oidc/token" \
      -H "Content-Type: application/x-www-form-urlencoded" \
      -H "Accept: application/json" \
      -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<your_API_key>" \ 
    ```
    {: codeblock}

    Ersetzen Sie in der Anforderung `<API_key>` durch den API-Schlüssel, den Sie in Schritt 3 erstellt haben. Das folgende abgeschnittene Beispiel zeigt die Token-Ausgabe:

    ```
    {
    "access_token": "eyJraWQiOiIyM...",
    "expiration": 1512161390,
    "expires_in": 3600,
    "refresh_token": "J1AzOrtC8yHVlcT...",
    "token_type": "Bearer"
    }
    ```
    {: screen}

    Verwenden Sie den vollständigen Wert `access_token` mit dem Präfixtyp _Trägertoken_, um die Schlüssel für Ihren Service programmgesteuert mit der {{site.data.keyword.keymanagementserviceshort}}-API zu verwalten. 

## Instanz-ID abrufen
{: #retrieve_instance_ID}

Sie können die Identifikationsinformationen für Ihre {{site.data.keyword.keymanagementserviceshort}}-Serviceinstanz abrufen, wenn Sie die [{{site.data.keyword.cloud_notm}}-CLI (bx) ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](/docs/cloud-platform/cli/reference/bluemix_cli/get_started.html#getting-started){: new_window} nutzen. Verwenden Sie eine Instanz-ID, um Ihre Verschlüsselungsschlüssel in einer bestimmten Instanz von {{site.data.keyword.keymanagementserviceshort}} in Ihrem Konto zu verwalten. 

1. Melden Sie sich bei {{site.data.keyword.cloud_notm}} über die {{site.data.keyword.cloud_notm}}-CLI (bx) an.

    ```sh
    bx login 
    ```
    {: pre}

    **Hinweis:** Wenn die Anmeldung fehlschlägt, führen Sie den Befehl `bx login --sso` aus, um es erneut zu versuchen. Der Parameter `--sso` ist für die Anmeldung mit einer eingebundenen ID erforderlich. Rufen Sie bei Verwendung dieser Option den in der CLI-Ausgabe aufgeführten Link auf, um einen einmaligen Kenncode zu generieren.

2. Wählen Sie das Konto aus, das Ihre bereitgestellte Instanz von {{site.data.keyword.keymanagementserviceshort}} enthält.

    Führen Sie `bx resource service-instances` aus, um alle Serviceinstanzen aufzulisten, die in Ihrem Konto bereitgestellt sind.

3. Rufen Sie den Cloudressourcennamen (CRN) ab, der Ihre {{site.data.keyword.keymanagementserviceshort}}-Serviceinstanz eindeutig identifiziert. 

    ```sh
    bx resource service-instance <instance_name> --id
    ```
    {: pre}

    Ersetzen Sie `<instance_name>` mit dem eindeutigen Alias, den Sie Ihrer Instanz von {{site.data.keyword.keymanagementserviceshort}} zugeordnet haben. Im folgenden gekürzten Beispiel sehen Sie die Bluemix-CLI-Ausgabe. Der Wert _7e8fc048-5606-4259-ad71-92397b0fa3f7_ ist eine Beispielinstanz-ID.

    ```
    crn:v1:bluemix:public:kms:us-south:a/7e8fc048-5606-4259-ad71-92397b0fa3f7
    ```
    {: screen}

## API-Anforderung formulieren
{: #form_api_request}

Wenn Sie einen API-Aufruf für den Service absetzen, strukturieren Sie Ihre API-Anforderung auf dieselbe Weise, wie Sie Ihre ursprüngliche Instanz von {{site.data.keyword.keymanagementserviceshort}} bereitgestellt haben. 

Um Ihre Anforderung zu erstellen, paaren Sie einen [regionalen Serviceendpunkt](/docs/services/keymgmt/keyprotect_regions.html) mit dem entsprechenden Authentifizierungsnachweis. Beispiel: Wenn Sie eine Serviceinstanz für die Region `us-south` erstellen, verwenden Sie den folgenden Endpunkt und diese API-Header, um die Schlüssel in Ihrem Service zu durchsuchen:

```cURL
curl -X GET \
    https://keyprotect.us-south.bluemix.net/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <access_token>' \
    -H 'bluemix-instance: <instance_ID>' \
```
{: codeblock}

### Weitere Schritte

- Weitere Informationen zum programmgesteuerten Management Ihrer Schlüssel [finden Sie in der API-Referenzdokumentation von {{site.data.keyword.keymanagementserviceshort}} für Codebeispiele ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
- Zur Anzeige eines Beispiels zur Art und Weise, in der Schlüsselspeicher in {{site.data.keyword.keymanagementserviceshort}} eingesetzt werden können, um Daten zu ver- und entschlüsseln, [überprüfen Sie die Beispielapp in GitHub ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.
