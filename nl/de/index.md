---

copyright:
  years: 2017
lastupdated: "2017-09-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Einführung in {{site.data.keyword.keymanagementserviceshort}}

Im Folgenden sind die Schritte aufgeführt, die zum Generieren, zur Eingabe und zum Management von Schlüsseln in {{site.data.keyword.keymanagementservicelong}} ausgeführt werden müssen.
{: shortdesc}

## Voraussetzungen
{: #prereqs }

{{site.data.keyword.keymanagementserviceshort}} steht für Services und Apps zur Verfügung, mit denen Sie (sofern die erforderliche Berechtigung vorliegt) API-Aufrufe an {{site.data.keyword.keymanagementserviceshort}} ausführen können. Bevor Sie einen Schlüssel hinzufügen können, benötigen Sie Folgendes.
- [IBMid und Kennwort](https://console.bluemix.net/docs/admin/adminpublic.html#signing-up-for-bluemix){: new_window}
- [Instanz des Service](https://console.ng.bluemix.net/catalog/services/key-protect/?taxonomyNavigation=apps){: new_window}

## Schlüssel hinzufügen
{: #addkey }

Führen Sie die folgenden Schritte aus, um einen neuen Schlüssel zu erstellen oder einen vorhandenen Schlüssel hochzuladen.

1. [Melden Sie sich bei der Bluemix-Konsole an.](https://console.bluemix.net/catalog){: new_window}
2. Positionieren Sie den Mauszeiger auf dem Link **Alle Kategorien**, um die Schiebeleiste einzublenden. Blättern Sie nach unten bis zu **Services > Sicherheit**. Daraufhin wird eine Liste Ihrer Apps und Services angezeigt.
3. Doppelklicken Sie auf die Serviceinstanz für **Key Protect**. Beachten Sie hierbei, dass der Service unter **Aktionen** umbenannt oder gelöscht werden kann.

Wenn Sie einen Schlüssel zum ersten Mal eingeben oder generieren, dann wird automatisch die Seite **Neuen Schlüssel hinzufügen** aufgerufen. Die Option **Neuen Schlüssel generieren** wird verwendet, um einen neuen Schlüssel in {{site.data.keyword.keymanagementserviceshort}} zu generieren, und die Option **Vorhandenen Schlüssel eingeben** wird verwendet, um einen bereits vorhandenen Schlüssel in den Service einzugeben.

### Schlüssel generieren
{: #genkey }

Führen Sie die folgenden Schritte aus, um einen neuen Schlüssel mit Key Protect zu generieren.

1. Geben Sie unter **Neuen Schlüssel generieren** Folgendes ein, damit Key Protect einen neuen Schlüssel generiert.
    <table>
      <tr>
        <th>Feld</th>
        <th>Beschreibung</th>
      </tr>
      <tr>
        <td>Name</td>
        <td>Ein lesbarer Alias, der Ihrem Schlüssel zugewiesen werden soll. Dies kann ein beliebiger Name sein. Er sollte so gewählt sein, dass Sie mit seiner Hilfe den Schlüssel eindeutig erkennen können. Der Name kann z. B. die Art der Schlüsselverwendung bezeichnen oder die Person, der der Schlüssel zugeordnet ist.</td>
      </tr>
      <tr>
        <td>Schlüsseltyp</td>
        <td>Standardmäßig wird der Schlüsseltyp 'Standard' verwendet. Ein Standardschlüssel wird als Datenverschlüsselungsschlüssel zur Verschlüsselung Ihrer unverschlüsselten Daten in verschlüsseltem Text verwendet.</td>
      </tr>
        <caption style="caption-side:bottom;">Tabelle 1. Beschreibung der Einstellungen für 'Neuen Schlüssel generieren'</caption>
    </table>

2. Klicken Sie auf die Schaltfläche **Schlüssel generieren**. Schlüssel stehen sofort zur Verfügung. Neue Schlüssel werden von Hardwaresicherheitsmodulen (HSMs) generiert, die sich in geschützten {{site.data.keyword.IBM}} Rechenzentren befinden.
3. Kopieren Sie die Referenz-ID in der Zeile des Schlüssels. Der **ID**-Wert ist die Kennung, die Sie in der {{site.data.keyword.keymanagementserviceshort}}-API verwenden.

### Vorhandenen Schlüssel eingeben
{: #existkey }

Führen Sie die folgenden Schritte aus, um einen vorhandenen Schlüssel in Key Protect einzugeben.

1. Geben Sie unter **Vorhandenen Schlüssel eingeben** Folgendes ein.
    <table>
      <tr>
        <th>Feld</th>
        <th>Beschreibung</th>
      </tr>
      <tr>
        <td>Name</td>
        <td>Ein lesbarer Alias, der Ihrem Schlüssel zugewiesen werden soll. Dies kann ein beliebiger Name sein. Er sollte so gewählt sein, dass Sie mit seiner Hilfe den Schlüssel eindeutig erkennen können. Der Name kann z. B. die Art der Schlüsselverwendung bezeichnen oder die Person, der der Schlüssel zugeordnet ist.</td>
      </tr>
      <tr>
        <td>Schlüsseltyp</td>
        <td>Standardmäßig wird der Schlüsseltyp 'Standard' verwendet. Ein Standardschlüssel wird als Datenverschlüsselungsschlüssel zur Verschlüsselung Ihrer unverschlüsselten Daten in verschlüsseltem Text verwendet.</td>
      </tr>
      <tr>
        <td>Schlüsselinformationen</td>
        <td>Die Schlüsselinformationen können als Daten eines beliebigen Typs definiert werden, die Sie im {{site.data.keyword.keymanagementserviceshort}}-Service speichern wollen, z. B. als Zertifikat oder RSA-Schlüssel.</td>
      </tr>
        <caption style="caption-side:bottom;">Tabelle 2. Beschreibung der Einstellungen für 'Vorhandenen Schlüssel eingeben'</caption>
    </table>

2. Klicken Sie auf die Schaltfläche **Neuen Schlüssel hinzufügen**. Schlüssel stehen sofort zur Verfügung.
3. Kopieren Sie die Referenz-ID in der Zeile des Schlüssels. Der **ID**-Wert ist die Kennung, die Sie in der {{site.data.keyword.keymanagementserviceshort}}-API verwenden.

## Schlüssel verwalten
{: #managekey }

Um die von Ihnen generierten und eingegebenen Schlüssel anzuzeigen, müssen Sie die unter [Schlüssel hinzufügen](index.html#addkey) aufgeführten Schritte ausführen. Dabei befinden Sie sich im Fenster **Schlüssel**. Ihre Schlüssel werden sortiert nach ihrem Erstellungsdatum aufgelistet, wobei der neueste Schlüssel an oberster Stelle der Liste steht.
<table>
      <tr>
        <th>Spalte</th>
        <th>Beschreibung</th>
      </tr>
      <tr>
        <td>Name</td>
        <td>Ein lesbarer Alias, der Ihrem Schlüssel zugewiesen wurde.</td>
      </tr>
      <tr>
        <td>ID</td>
        <td>Eine eindeutige Schlüssel-ID, die Ihrem Schlüssel von Key Protect zugewiesen wurde.</td>
      </tr>
      <tr>
        <td>Status</td>
        <td>Einer der NIST-Schlüsselstatus (NIST = National Institute of Standards and Technology). Diese lauten wie folgt: 'Pre-activation' (Vor Aktivierung), 'Active' (Aktiv), 'Deactivated' (Inaktiviert) und 'Destroyed' (Gelöscht).<td>
      </tr>
      <tr>
        <td>Erstellt</td>
        <td>Der Zeitpunkt (Datum und Uhrzeit), zu dem der Schlüssel erstellt wurde.</td>
      </tr>
      <tr>
        <td>Typ</td>
        <td>Standardmäßig wird der Schlüsseltyp 'Standard' verwendet.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabelle 3. Beschreibung des Fensters 'Schlüssel'</caption>
    </table>

### Weitere Schritte

Sie können Ihre Schlüssel nun verwenden, um Ihre Apps und Services zu codieren.

- Ein Beispiel dafür, wie in {{site.data.keyword.keymanagementserviceshort}} gespeicherte Schlüssel beim Verschlüsseln und Entschlüsseln von Daten funktionieren, finden Sie in der [Beispiel-App in Github ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.
- Weitere Informationen zur programmgestützten Verwaltung Ihrer Schlüssel finden Sie in den Codebeispielen in der [API-Referenzdokumentation zu {{site.data.keyword.keymanagementserviceshort}}](https://console.ng.bluemix.net/apidocs/639).

### Zugehörige Links

- [{{site.data.keyword.keymanagementserviceshort}}-REST-API ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/apidocs/639){: new_window}
- [{{site.data.keyword.keymanagementserviceshort}}-Admin-REST-API ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs-admin-keyprotect.ng.bluemix.net/){: new_window}
- [Cloud-HSM-Angebot ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.softlayer.com/ibm-cloud-hsm){: new_window}
- [{{site.data.keyword.keymanagementservicelong_notm}} Service Level Agreement ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www-03.ibm.com/software/sla/sladb.nsf/sla/bm-7603-01){: new_window}
