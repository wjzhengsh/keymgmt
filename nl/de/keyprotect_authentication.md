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

# Authentifizierungsnachweise generieren
{: #authentication}

{{site.data.keyword.keymanagementservicefull}} stellt eine REST-API bereit, die mit jeder Programmiersprache verwendet werden kann, um Schlüssel zu speichern, abzurufen und zu generieren.
{: shortdesc}

Um mit der API zu arbeiten, müssen Sie eigene Service- und Authentifizierungsnachweise generieren.

## Organisations- und Bereichs-GUIDs abrufen
{: #retrieve_GUIDs}

Sie können die Identifikationsinformationen für Ihre {{site.data.keyword.cloud_notm}}-Organisation und den entsprechenden Bereich mit der [{{site.data.keyword.cloud_notm}}-CLI ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.bluemix.net/docs/cli/reference/bluemix_cli/index.html#getting-started) abrufen.

1. Melden Sie sich über die {{site.data.keyword.cloud_notm}}-CLI (bx) bei {{site.data.keyword.cloud_notm}} an.

    ```
    bx login [--sso]
    ```
    {: codeblock}

    Der Parameter `--sso` ist für die Anmeldung mit einer eingebundenen ID erforderlich. Rufen Sie bei Verwendung dieser Option den in der CLI-Ausgabe aufgeführten Link auf, um einen einmaligen Kenncode zu generieren.

2. Wählen Sie die {{site.data.keyword.cloud_notm}}-Organisation und den entsprechenden Bereich mit Ihrer {{site.data.keyword.keymanagementserviceshort}}-Serviceinstanz aus.

    Notieren Sie sich die Namen Ihrer Organisation und Ihres Bereichs in der CLI-Ausgabe. Sie können auch `bx target` ausführen, um diese Informationen anzuzeigen.

3. Rufen Sie Ihre {{site.data.keyword.cloud_notm}}-Organisations- und Bereichs-GUIDs ab.

    ```
    bx iam org [organization_name] --guid
    bx iam space [space_name] --guid
    ```
    {: codeblock}
    Ersetzen Sie _organization_name_ und _space_name_ durch den eindeutigen Alias, den Sie Ihrer Organisation und dem entsprechenden Bereich zugewiesen haben.

## Berechtigungstoken abrufen
{: #retrieve_token}

Mit einem Berechtigungstoken können Sie Ihre Schlüssel programmgesteuert mithilfe der {{site.data.keyword.keymanagementserviceshort}}-API verwalten.

**Hinweis**: Zur Aktivierung der differenzierten Zugriffssteuerung mithilfe von {{site.data.keyword.iamshort}} müssen Sie ein IAM-Token verwenden, um Aufrufe an den Service durchzuführen.

1. Wählen Sie in der {{site.data.keyword.cloud_notm}}-CLI die Organisation und den Bereich aus, die Ihren {{site.data.keyword.keymanagementserviceshort}}-Service enthalten.

2. Rufen Sie Ihre Berechtigungstokens ab und zeigen Sie sie an.

    ```
    bx iam oauth-tokens
    ```
    {: codeblock}

    Im folgenden gekürzten Beispiel sehen Sie die {{site.data.keyword.cloud_notm}}-Tokenausgabe. Die Variable _Bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7_ ist ein Beispiel für ein Zugriffstoken.

    ```
    IAM token: Bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7...
    UAA token: Bearer mjEyJhbGciOiJIUzI1Ni.chWyW1faWQiOiJJQkWs1...
    ```
    {: screen}

    Verwenden Sie den Bearerwert `IAM` oder `UAA` zum programmgesteuerten Management von Schlüsseln in Ihrem Service mithilfe der {{site.data.keyword.keymanagementserviceshort}}-API.

### Weitere Schritte

Rufen Sie die [REST-API-Referenzdokumentation für {{site.data.keyword.keymanagementserviceshort}}![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/apidocs/639){: new_window} auf, um mit dem Management von Schlüsseln in Ihrem Bereich zu beginnen.
