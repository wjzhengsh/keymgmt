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

# Den Service bereitstellen
{: #provision}

Sie können eine Instanz von {{site.data.keyword.keymanagementservicefull}} bereitstellen, indem Sie die {{site.data.keyword.cloud_notm}}-Konsole oder die {{site.data.keyword.cloud_notm}}-CLI (bx) verwenden.
{: shortdesc}

## Bereitstellung über {{site.data.keyword.cloud_notm}}-Konsole durchführen
{: #gui}

Zur Bereitstellung einer Instanz von {{site.data.keyword.keymanagementserviceshort}} über die {{site.data.keyword.cloud_notm}}-Konsole müssen Sie die folgenden Schritte ausführen:

1. [Melden Sie sich bei Ihrem {{site.data.keyword.cloud_notm}}-Konto ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.bluemix.net/){: new_window} an.
2. Klicken Sie auf **Katalog**, um die Liste der Services anzuzeigen, die unter {{site.data.keyword.cloud_notm}} zur Verfügung stehen.
3. Blättern Sie im Navigationsbereich 'Alle Kategorien' zu **Plattform** und klicken Sie auf die Kategorie **Sicherheit**.
4. Klicken Sie in der Serviceliste auf die **{{site.data.keyword.keymanagementserviceshort}}**-Kachel.
5. Wählen Sie einen Serviceplan aus und klicken Sie auf **Erstellen**, um eine Instanz von {{site.data.keyword.keymanagementserviceshort}} im Konto, in der Region und in der Ressourcengruppe, bei denen Sie angemeldet sind, bereitzustellen.

## Bereitstellung über die {{site.data.keyword.cloud_notm}}-CLI (bx)
{: #cli}

Sie können eine Instanz von {{site.data.keyword.keymanagementserviceshort}} mithilfe der {{site.data.keyword.cloud_notm}}-CLI (bx) bereitstellen. 

### Eine Serviceinstanz in Ihrem Konto erstellen
{: #provision_acct_lvl}

Um den Zugriff auf Ihre Verschlüsselungsschlüssel mit [{{site.data.keyword.iamlong}}-Rollen](/docs/iam/users_roles.html#iamusermanpol) zu vereinfachen, können Sie eine oder mehrere Instanzen eines {{site.data.keyword.keymanagementserviceshort}}-Services in einem Konto erstellen, ohne eine Organisation oder einen Bereich anzugeben. 

1. Melden Sie sich bei {{site.data.keyword.cloud_notm}} mithilfe der [{{site.data.keyword.cloud_notm}}-CLI (bx) an.](/docs/cloud-platform/cli/reference/bluemix_cli/get_started.html#getting-started){: new_window}

    ```sh
    bx login 
    ```
    {: pre}
    **Hinweis:** Wenn die Anmeldung fehlschlägt, führen Sie den Befehl `bx login --sso` aus, um es erneut zu versuchen. Der Parameter `--sso` ist für die Anmeldung mit einer eingebundenen ID erforderlich. Rufen Sie bei Verwendung dieser Option den in der CLI-Ausgabe aufgeführten Link auf, um einen einmaligen Kenncode zu generieren.

2. Wählen Sie das Konto, die Region und die Ressourcengruppe aus, für die Sie eine {{site.data.keyword.keymanagementserviceshort}}-Serviceinstanz erstellen möchten.

    Sie können auch den folgenden Befehl verwenden, um die die Zielregion und die Ressourcengruppe festzulegen.

    ```sh
    bx target -r <region_name> -g <resource_group_name>
    ```
    {: pre}

3. Stellen Sie eine Instanz von {{site.data.keyword.keymanagementserviceshort}} in diesem Konto und in dieser Ressourcengruppe bereit.

    ```sh
    bx resource service-instance-create <instance_name> kms tiered-pricing
    ```
    {: pre}

    Ersetzen Sie `<instance_name>` mit einem eindeutigen Alias für Ihre Serviceinstanz.

4. Optional: Überprüfen Sie, ob die Serviceinstanz erfolgreich erstellt wurde.

    ```sh
    bx resource service-instances
    ```
    {: pre}

### Eine Serviceinstanz in einer Organisation und in einem Bereich erstellen
{: #provision_space_lvl}

Um den Zugriff auf Ihre Verschlüsselungsschlüssel mit [Cloud Foundry-Rollen](/docs/iam/users_roles.html#cfroles) zu vereinfachen, können Sie eine Instanz des {{site.data.keyword.keymanagementserviceshort}}-Services in einer Organisation und in einem Bereich erstellen.  

1. Melden Sie sich bei [{{site.data.keyword.cloud_notm}} mithilfe der [{{site.data.keyword.cloud_notm}}-CLI (bx) an.](/docs/cloud-platform/cli/reference/bluemix_cli/get_started.html#getting-started){: new_window}

    ```sh
    bx login 
    ```
    {: pre}
    **Hinweis:** Wenn die Anmeldung fehlschlägt, führen Sie den Befehl `bx login --sso` aus, um es erneut zu versuchen. Der Parameter `--sso` ist für die Anmeldung mit einer eingebundenen ID erforderlich. Rufen Sie bei Verwendung dieser Option den in der CLI-Ausgabe aufgeführten Link auf, um einen einmaligen Kenncode zu generieren.

2. Wählen Sie das Konto, die Region, die Organisation und den Bereich aus, für die Sie eine {{site.data.keyword.keymanagementserviceshort}}-Serviceinstanz erstellen möchten.

    Sie können auch den folgenden Befehl verwenden, um die Zielregion, die Organisation und den Bereich zu erstellen.

    ```sh
    bx target -r <region> -o <organization_name> -s <space_name>
    ```
    {: pre}

3. Stellen Sie eine Instanz von {{site.data.keyword.keymanagementserviceshort}} in diesem Konto, in dieser Region, in dieser Organisation und in diesem Bereich bereit.

    ```sh
    bx service create kms tiered-pricing <instance_name>
    ```
    {: pre}

    Ersetzen Sie `<instance_name>` mit einem eindeutigen Alias für Ihre Serviceinstanz.

4. Optional: Überprüfen Sie, ob die Serviceinstanz erfolgreich erstellt wurde.

    ```sh
    bx service list
    ```
    {: pre}


### Weitere Schritte

- Zur Anzeige eines Beispiels zur Art und Weise, in der Schlüsselspeicher in {{site.data.keyword.keymanagementserviceshort}} eingesetzt werden können, um Daten zu ver- und entschlüsseln, [überprüfen Sie die Beispielapp in GitHub ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.
- Weitere Informationen zum programmgesteuerten Management Ihrer Schlüssel [finden Sie in der API-Referenzdokumentation von {{site.data.keyword.keymanagementserviceshort}} für Codebeispiele ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
