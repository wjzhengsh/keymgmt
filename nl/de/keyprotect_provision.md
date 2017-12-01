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

# {{site.data.keyword.keymanagementserviceshort}}-Service bereitstellen
{: #provision}

Sie können eine sichere Instanz von {{site.data.keyword.keymanagementservicefull}} bereitstellen, indem Sie die {{site.data.keyword.cloud_notm}}-Konsole oder die {{site.data.keyword.cloud_notm}}-CLI (bx) verwenden.
{: shortdesc}

## Bereitstellung über {{site.data.keyword.cloud_notm}}-Konsole durchführen
{: #gui}

Zur Bereitstellung einer Instanz von {{site.data.keyword.keymanagementserviceshort}} über die {{site.data.keyword.cloud_notm}}-Konsole müssen Sie die folgenden Schritte ausführen:

1. [Melden Sie sich bei Ihrem {{site.data.keyword.cloud_notm}}-Konto ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.bluemix.net/){: new_window} an.
2. Klicken Sie auf **Katalog**, um die Liste der Services anzuzeigen, die unter {{site.data.keyword.cloud_notm}} zur Verfügung stehen.
3. Wählen Sie die Kategorie **Services** aus und klicken Sie dann auf die **{{site.data.keyword.keymanagementserviceshort}}**-Kachel.
5. Wählen Sie einen Serviceplan aus und klicken Sie dann auf **Erstellen**, um eine {{site.data.keyword.keymanagementserviceshort}}-Serviceinstanz in der {{site.data.keyword.cloud_notm}}-Organisation und in dem entsprechenden Bereich bereitzustellen, in der bzw. dem Sie angemeldet sind.

## Bereitstellung über die {{site.data.keyword.cloud_notm}}-CLI (bx)
{: #cli}

Sie können eine Instanz von {{site.data.keyword.keymanagementserviceshort}} mithilfe der {{site.data.keyword.cloud_notm}}-CLI (bx) bereitstellen. [Laden Sie das Befehlszeilentool auf Ihr System herunter und installieren Sie es](https://clis.ng.bluemix.net/ui/home.html){: new_window}, um die folgenden Schritte auszuführen.

1. Melden Sie sich bei der {{site.data.keyword.cloud_notm}}-CLI an.

    ```sh
    bx login [--sso]
    ```
    {: codeblock}
    **Anmerkung**: Der Parameter `--sso` ist für die Anmeldung mit einer eingebundenen ID erforderlich. Rufen Sie bei Verwendung dieser Option den in der CLI-Ausgabe aufgeführten Link auf, um einen einmaligen Kenncode zu generieren.

2. Wählen Sie die {{site.data.keyword.cloud_notm}}-Organisation und den entsprechenden Bereich aus, in der bzw. dem die {{site.data.keyword.keymanagementserviceshort}}-Serviceinstanz erstellt werden soll.

    Sie können auch den folgenden Befehl verwenden, um die Zielorganisation und den Zielbereich festzulegen.

    ```sh
    bx target [-o organization_name] [-s space_name]
    ```
    {: codeblock}

3. Stellen Sie eine Instanz von {{site.data.keyword.keymanagementserviceshort}} in dieser Region, Organisation und in diesem Bereich bereit.

    ```sh
    bx service create kms TieredPricing [instance_name]
    ```
    {: codeblock}

    Ersetzen Sie _instance_name_ durch einen eindeutigen Alias für Ihre Serviceinstanz.

4. Überprüfen Sie, ob die Serviceinstanz erfolgreich erstellt wurde.

    ```sh
    bx service list
    ```
    {: codeblock}


### Weitere Schritte

Sie können Ihre Schlüssel nun verwenden, um Ihre Apps und Services zu codieren.

- Zur Anzeige eines Beispiels zur Art und Weise, in der Schlüsselspeicher in {{site.data.keyword.keymanagementserviceshort}} eingesetzt werden können, um Daten zu ver- und entschlüsseln, [überprüfen Sie die Beispielapp in GitHub ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.
- Weitere Informationen zum programmgesteuerten Management Ihrer Schlüssel [finden Sie in der API-Referenzdokumentation von {{site.data.keyword.keymanagementserviceshort}} für Codebeispiele ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
