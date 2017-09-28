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

# Fehlerbehebung

Hier finden Sie die Antworten auf allgemeine Fragen zur Fehlerbehebung bei der Verwendung von {{site.data.keyword.keymanagementservicefull}}.
{: shortdesc}

## Schlüssel können nicht erstellt oder gelöscht werden
{: #unabletomanagekeys}

Wenn Sie keine {{site.data.keyword.keymanagementserviceshort}}-Aktionen ausführen können, prüfen Sie, ob Sie über die richtige Berechtigung verfügen.

### Symptome

Wenn Sie auf die {{site.data.keyword.keymanagementserviceshort}}-Benutzerschnittstelle zugreifen, können Sie die Optionen zum Hinzufügen oder Löschen von Schlüsseln nicht anzeigen.

### Problemlösung

Wenden Sie sich an Ihren Administrator und prüfen Sie, ob Ihnen die richtige Rolle im entsprechenden Bereich zugewiesen wurde. Weitere Informationen zu Rollen finden Sie in [Rollen und Berechtigungen](/docs/services/keymgmt/keyprotect_manage_access.html#roles).

## Beta-nach-GA-Konvertierung
{: #ts_planconversion}

Benutzer der Betaversion müssen zur weiteren Nutzung des Service {{site.data.keyword.keymanagementserviceshort}} zum Standardpreismodell wechseln.

### Symptome

Wenn Sie ein Benutzer der Betaversion sind, müssen Sie Ihren Preistarif ändern und zum Modell der gestaffelten Preisgestaltung wechseln, um weiterhin Schlüssel in {{site.data.keyword.keymanagementserviceshort}} speichern zu können.

### Problemlösung

Der Service {{site.data.keyword.keymanagementserviceshort}} verfügt über zwei Preismodelle: ein Lite-Modell und ein Modell der gestaffelten Preisstruktur. Als Administrator müssen Sie prüfen, ob das Modell der gestaffelten Tier-Preisstruktur ausgewählt wurde. Wenn Sie keine Migration auf das gestaffelte Modell durchführen möchten, müssen Sie sicherstellen, dass alle Schlüssel und Serviceinstanzen vor der Einstellung der Unterstützung entfernt werden. [Weitere Informationen finden Sie in der {{site.data.keyword.keymanagementserviceshort}}-GA-Ankündigung ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")]("https://www.ibm.com/blogs/bluemix/2016/12/dallas-key-protect-ga/" "https://www.ibm.com/blogs/bluemix/2016/12/dallas-key-protect-ga/"){: new_window}.

Gehen Sie wie folgt vor, um den Preistarif zu ändern:

1. Rufen Sie die Benutzerschnittstelle von {{site.data.keyword.keymanagementserviceshort}} auf und wählen Sie die Registerkarte **Pläne** aus.
2. Wählen Sie **Gestaffelte Preisstruktur** aus.
    Die Aufgliederung der Kosten in aktive Schlüssel, die pro Monat genutzt werden, ist in der Tabelle aufgeführt. Beim gestaffelten Modell wird der Tarif auf Basis der Anzahl der aktiven Schlüssel pro Monat auf Kontoebene berechnet.
3. Klicken Sie auf **Speichern**, um die Planänderung zu bestätigen.

## Hilfe und Unterstützung für {{site.data.keyword.keymanagementserviceshort}} anfordern
{: #ts_gettinghelp}

Sollten bei der Verwendung von {{site.data.keyword.keymanagementservicefull_notm}} Probleme auftreten oder Fragen entstehen, können Sie nach Informationen suchen, oder Fragen in einem Forum stellen. Sie haben auch die Möglichkeit, ein Support-Ticket zu öffnen.

Wenn Sie in den Foren eine Frage stellen, versehen Sie Ihre Frage mit einem Tag, sodass sie von den {{site.data.keyword.IBM_notm}} {{site.data.keyword.Bluemix_notm}}-Entwicklungsteams gesehen wird.

- Bei technischen Fragen zu {{site.data.keyword.keymanagementserviceshort}} posten Sie Ihre Fragen in [Stack Overflow ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://stackoverflow.com/search?q=key-protect+ibm-bluemix){: new_window} und kennzeichnen Sie die Fragen mit den Tags "ibm-bluemix" und "key-protect".
- Antworten auf Fragen zum Service und Anweisungen für den Einstieg erhalten Sie über das Forum [IBM developerWorks dW Answers ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/answers/topics/key-protect/?smartspace=bluemix){: new_window}. Geben Sie die Tags "bluemix"
und "key-protect" an.

Weitere Details zur Nutzung der Foren finden Sie unter [Hilfe anfordern ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.bluemix.net/docs/support/index.html#getting-help){: new_window}.

Informationen zum Öffnen eines {{site.data.keyword.IBM_notm}} Support-Tickets bzw. zu Supportebenen und zur Priorität von Tickets finden Sie in [Kontaktaufnahme mit dem Support![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.bluemix.net/docs/support/index.html#contacting-support){: new_window}.
