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

# Einführung in {{site.data.keyword.keymanagementserviceshort}}

Mit {{site.data.keyword.keymanagementservicelong}} können Sie verschlüsselte Schlüssel für Apps für {{site.data.keyword.Bluemix_short}} bereitstellen. Bei der Verwaltung des Lebenszyklus Ihrer Schlüssel kommt es Ihnen zugute, dass die Schlüssel durch cloudbasierte Hardwaresicherheitsmodule (HSMs) gesichert sind, die gegen Informationsdiebstahl schützen.
{: shortdesc}

{{site.data.keyword.keymanagementserviceshort}} ist automatisch für alle Apps in dem Bereich verfügbar, in dem es erstellt wird. [Führen Sie nach dem Erstellen einer Instanz dieses Service](https://console.ng.bluemix.net/catalog/services/key-protect/?taxonomyNavigation=apps){: new_window} die folgenden Schritte aus, um mit der Arbeit zu beginnen:

1. Klicken Sie auf **Schlüssel hinzufügen**, um einen Schlüssel zu erstellen oder einen vorhandenen Schlüssel hochzuladen.
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
      <tr>
        <td>Algorithmus</td>
        <td>Die Verschlüsselung symmetrischer Schlüssel wird durch den AES-GCM-Algorithmus unterstützt.</td>
      </tr>
      <tr>
        <td>Schlüssel</td>
        <td>Nur erforderlich, wenn Sie einen vorhandenen Schlüssel hinzufügen. Bei den Schlüsselinformationen kann es sich um einen beliebigen Typ von Daten handeln, die Sie im {{site.data.keyword.keymanagementserviceshort}}-Service speichern möchten (z. B. ein Zertifikats- oder RSA-Schlüssel). </td>
      </tr>
        <caption style="caption-side:bottom;">Tabelle 1. Beschreibung der Schlüsseleinstellungen</caption>
    </table>

2. Nach der Angabe der Details zum Schlüssel klicken Sie zur Bestätigung auf **Schlüssel hinzufügen**. Schlüssel stehen sofort zur Verfügung. Neue Schlüssel werden von Hardwaresicherheitsmodulen (HSMs) generiert, die sich in geschützten {{site.data.keyword.IBM}} Rechenzentren befinden.
3. Kopieren Sie die Referenz-ID in der Zeile des Schlüssels. Der **ID**-Wert ist die Kennung, die Sie in der {{site.data.keyword.keymanagementserviceshort}}-API verwenden.
4. **Optional**: Wenn Sie einen Schlüssel löschen möchten, sollten Sie beachten, dass Schlüsselinformationen nicht wiederherstellbar sind. Die zugehörigen Metadaten für den Schlüssel werden in der {{site.data.keyword.keymanagementserviceshort}}-Datenbank aufbewahrt. Um einen Schlüssel zu löschen, klicken Sie auf das Symbol **Aktionen** in der Zeile des Schlüssels und bestätigen Sie das Löschen in der anschließenden Anzeige.

Weitere Schritte:

Sie können Ihre Schlüssel nun verwenden, um Ihre Apps und Services zu codieren.

- Ein Beispiel dafür, wie in {{site.data.keyword.keymanagementserviceshort}} gespeicherte Schlüssel beim Verschlüsseln und Entschlüsseln von Daten funktionieren, finden Sie in der [Beispiel-App in Github ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/IBM-Bluemix/key-protect-helloworld-python "Symbol für externen Link"){: new_window}.
- Weitere Informationen zur programmgestützten Verwaltung Ihrer Schlüssel finden Sie in den Codebeispielen in der [API-Referenzdokumentation zu {{site.data.keyword.keymanagementserviceshort}}](https://console.ng.bluemix.net/apidocs/639).

## Zugehörige Links

- [{{site.data.keyword.keymanagementserviceshort}}-REST-API ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/apidocs/639 "Symbol für externen Link"){: new_window}
- [{{site.data.keyword.keymanagementserviceshort}}-Admin-REST-API ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs-admin-keyprotect.ng.bluemix.net/ "Symbol für externen Link"){: new_window}
- [Cloud-HSM-Angebot ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.softlayer.com/ibm-cloud-hsm "Symbol für externen Link"){: new_window}
