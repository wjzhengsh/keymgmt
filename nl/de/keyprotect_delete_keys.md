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

# Schlüssel löschen

Sie können {{site.data.keyword.keymanagementservicefull}} verwenden, um einen Verschlüsselungsschlüssel und seinen Inhalt zu löschen, wenn Sie der Administrator Ihres {{site.data.keyword.cloud_notm}}-Bereichs oder der {{site.data.keyword.keymanagementserviceshort}}-Serviceinstanz sind.
{: shortdesc}

**Wichtig**: Wenn Sie einen Schlüssel löschen, dann werden sein Inhalt und die zugehörigen Daten permanent zerstört. Die Aktion kann nicht rückgängig gemacht werden. Das Löschen von Ressourcen wird in Produktionsumgebungen nicht empfohlen. Diese Vorgehensweise kann jedoch in temporären Umgebungen (z. B. in Testumgebungen oder QA-Umgebungen) von Nutzen sein.

## Schlüssel mit GUI löschen
{: #gui}

Wenn Sie die Löschung von Schlüsselressourcen über eine grafische Oberfläche bevorzugen, dann können Sie hierzu die {{site.data.keyword.keymanagementserviceshort}}-GUI verwenden.

[Nach dem Erstellen oder Importieren der vorhandenen Schlüssel in den Service](/docs/services/keymgmt/keyprotect_create_keys.html) müssen Sie die folgenden Schritte ausführen, um einen Schlüssel zu löschen:

1. [Melden Sie sich bei der {{site.data.keyword.cloud_notm}}-Konsole ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.bluemix.net/) an.
2. Wählen Sie im {{site.data.keyword.cloud_notm}}-Dashboard die bereitgestellte Instanz von {{site.data.keyword.keymanagementserviceshort}} aus.
3. Navigieren Sie zum Fenster **Verwalten**, um die Schlüssel in Ihrem Service zu suchen.
4. Klicken Sie auf das Symbol mit den senkrechten Auslassungszeichen, um eine Liste der Optionen für den Schlüssel zu öffnen, der gelöscht werden soll.
5. Klicken Sie im Auswahlmenü auf **Schlüssel löschen** und bestätigen Sie die Schlüssellöschung in der nächsten Anzeige.

## Schlüssel mit API löschen
{: #api}

Um einen Schlüssel und seinen Inhalt zu löschen, müssen Sie einen `DELETE`-Aufruf für den folgenden Endpunkt ausführen:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID>
```

1. [Rufen Sie das Berechtigungstoken, die Organisations-GUID und die Bereichs-GUID ab, um im Service mit Schlüsseln arbeiten zu können.](/docs/services/keymgmt/keyprotect_authentication.html)

2. Rufen Sie die ID des Schlüssels ab, den Sie löschen möchten.

    Sie können die ID für einen angegebenen Schlüssel abrufen, indem Sie die Anforderung `GET /v2/keys` absetzen oder indem Sie die Schlüssel im {{site.data.keyword.keymanagementserviceshort}}-Dashboard anzeigen.

3. Führen Sie den folgenden cURL-Befehl aus, um den Schlüssel und seinen Inhalt dauerhaft zu löschen.

    ```cURL
    curl -X DELETE \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID> \
      -H 'authorization: Bearer <OAuth_token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
      -H 'prefer: <return_preference>'
    ```
    Ersetzen Sie die Variablen in der Beispielanforderung mithilfe der Angaben in der folgenden Tabelle.
    <table>
      <tr>
        <th>Variable</th>
        <th>Beschreibung</th>
      </tr>
      <tr>
        <td><em>OAuth_token</em></td>
        <td>Ihr Berechtigungstoken. Nehmen Sie den vollständigen Inhalt des Tokens einschließlich des Werts für Bearer in die cURL-Anforderung auf.</td>
      </tr>
      <tr>
        <td><em>space_GUID</em></td>
        <td>Die eindeutige ID, die Ihrem {{site.data.keyword.cloud_notm}}-Bereich zugewiesen ist.</td>
      </tr>
      <tr>
        <td><em>organization_GUID</em></td>
        <td>Die eindeutige ID, die Ihrer {{site.data.keyword.cloud_notm}}-Organisation zugewiesen ist.</td>
      </tr>
      <tr>
        <td><em>key_ID</em></td>
        <td>Die eindeutige ID für den Schlüssel, der gelöscht werden soll.</td>
      </tr>
      <tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p>Ein Header, der das Serververhalten für <code>POST</code>- und <code>DELETE</code>-Operationen ändert.</p><p>Bei Verwendung der Einstellung <code>return=minimal</code> gibt der Service im Entitätshauptteil der Antwort nur die Schlüsselmetadaten zurück, z. B. den Schlüsselnamen und den Wert für <code>id</code>. Wird <code>return=representation</code> verwendet, dann gibt der Service sowohl die Schlüsselinformationen als auch die Schlüsselmetadaten zurück.</p></td>
      </tr>
      <caption style="caption-side:bottom;">Tabelle 1. Beschreibt die Variablen, die zum Löschen von Schlüsseln über die {{site.data.keyword.keymanagementserviceshort}}-API erforderlich sind.</caption>
    </table>

    Die Details der Anforderung `DELETE` werden im Entitätshauptteil der Antwort zurückgegeben.
