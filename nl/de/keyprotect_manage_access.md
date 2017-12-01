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

# Benutzerzugriff mit Identity and Access Management verwalten
{: #managing-access-iam}

{{site.data.keyword.keymanagementservicefull}} unterstützt ein zentralisiertes Zugriffssteuerungssystem, das mit {{site.data.keyword.iamlong}} reguliert wird, um Sie bei der Verwaltung von Benutzern und beim Zugriff auf Ihre Verschlüsselungsschlüssel zu unterstützen.
{: shortdesc}

Es hat sich bewährt, Zugriffsberechtigungen zu erteilen, während Sie neue Benutzer zur Nutzung Ihres Kontos oder Service einladen. Beachten Sie hierbei z. B. die folgenden Leitlinien:

- **Aktivieren Sie den Benutzerzugriff auf die Ressourcen in Ihrem Konto, indem Sie IAM-Rollen zuweisen.**
    Anstatt Ihre Administratorberechtigungsnachweise gemeinsam zu nutzen, sollten Sie neue Richtlinien für die Benutzer erstellen, die Zugriff auf die Verschlüsselungsschlüssel in Ihrem Konto benötigen. Wenn Sie der Administrator Ihres Kontos sind, dann wird Ihnen automatisch eine Administratorrichtlinie mit Zugriff auf alle Ressourcen zugewiesen, die sich unter Ihrem Konto befinden.
- **Erteilen Sie Rollen und Berechtigungen für den kleinsten erforderlichen Geltungsbereich.**
    Wenn ein Benutzer beispielsweise nur Zugriff auf eine übergeordnete Ansicht der Schlüssel in einem bestimmten Bereich benötigt, dann ordnen Sie ihm die Rolle _Anzeigeberechtigter_ für diesen Bereich zu.
- **Überprüfen Sie in regelmäßigen Zeitabständen, wer zur Verwaltung der Zugriffssteuerung und zum Löschen von Schlüsselressourcen berechtigt ist.**
    Beachten Sie dabei, dass die Erteilung einer Rolle als _Administrator_ für einen Benutzer bedeutet, dass dieser Benutzer Servicerichtlinien für andere Benutzer ändern und außerdem Ressourcen löschen kann.

## Rollen und Berechtigungen
{: #roles}

Mit {{site.data.keyword.iamshort}} (IAM) können Sie Richtlinien festlegen, mit denen der Geltungsbereich des Zugriffs für die Mitglieder Ihres Teams definiert werden.

Zur Vereinfachung des Zugriffs orientiert sich {{site.data.keyword.keymanagementserviceshort}} an den IAM-Rollen, sodass jeder Benutzer über eine andere Ansicht des Service verfügt, und zwar abhängig von der Rolle, die diesem Benutzer zugewiesen wurde. Wenn Sie der Sicherheitsadministrator für Ihren Service sind, dann können Sie IAM-Rollen zuweisen, die den speziellen {{site.data.keyword.keymanagementserviceshort}}-Berechtigungen entsprechen, die Sie Mitgliedern Ihres Teams erteilen wollen.

In der folgenden Tabelle erhalten Sie Informationen dazu, wie die Identitäts- und Zugriffsrollen den {{site.data.keyword.keymanagementserviceshort}}-Berechtigungen zugeordnet werden:
<table>
  <tr>
    <th>Rolle</th>
    <th>Beschreibung</th>
    <th>Aktionen</th>
  </tr>
  <tr>
    <td>Anzeigeberechtigter</td>
    <td>Ein Anzeigeberechtigter kann auf eine übergeordnete Ansicht der Schlüssel zugreifen. Anzeigeberechtigte können weder auf die Schlüsseldetails zugreifen noch die Schlüsseldetails ändern.</td>
    <td>
      <ul>
        <li>Schlüssel anzeigen</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Editor</td>
    <td>Ein Editor kann Schlüssel erstellen und ändern und außerdem die Schlüsseldetails anzeigen.</td>
    <td>
      <ul>
        <li>Schlüssel erstellen</li>
        <li>Schlüssel anzeigen</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Administrator</td>
    <td>Ein Administrator kann alle Aktionen ausführen, die ein Anzeigeberechtigter und ein Editor ausführen können. Dies umfasst auch die Berechtigung zum Löschen von Schlüsseln, zum Einladen neuer Benutzer und zum Verwalten der Zugriffssteuerung. </td>
    <td>
      <ul>
        <li>Schlüssel erstellen</li>
        <li>Schlüssel anzeigen</li>
        <li>Schlüssel löschen</li>
        <li>Zugriffssteuerung verwalten</li>
      </ul>
    </td>
  </tr>
  <caption style="caption-side:bottom;">Tabelle 1. Zuordnung von Identitäts- und Zugriffsrollen zu {{site.data.keyword.keymanagementserviceshort}}-Berechtigungen</caption>
</table>

**Anmerkung**: IAM-Benutzerrollen bieten Zugriff auf Service- und auf Serviceinstanzebene. [Cloud Foundry-Rollen](/docs/iam/users_roles.html#cfroles) sind separat und definieren den Zugriff auf Organisations- oder Bereichsebene.

Weitere Informationen zu {{site.data.keyword.iamshort}} finden Sie im Abschnitt zu den [Benutzerrollen und Berechtigungen](/docs/iam/users_roles.html#iamusermanpol).

### Weitere Schritte

Kontoeigner und Administratoren können Benutzer einladen und Servicerichtlinien festlegen, die den {{site.data.keyword.keymanagementserviceshort}}-Aktionen entsprechen, die die Benutzer ausführen können.

- Informationen zur Zuweisung von Benutzerrollen in der grafischen Benutzerschnittstelle von {{site.data.keyword.cloud_notm}} finden Sie im Abschnitt zu den [Identitäts- und zugriffsaktivierten Servicezugriffsrichtlinien](/docs/iam/iamusermanage.html#iammanidaccser).
- Informationen zum Erteilen erweiterter Berechtigungen für den Zugriff auf bestimmte Verschlüsselungsschlüssel finden Sie im Abschnitt zum [Verwalten des Zugriffs auf Schlüssel mit der API](/docs/services/keymgmt/keyprotect_manage_access_api.html).
