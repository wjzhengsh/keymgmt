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

# Zugriff auf Schlüssel mit API verwalten
{: #managing-access-api}

Mit {{site.data.keyword.iamlong}} können Sie die differenzierte Zugriffssteuerung für Ihre Schlüsselressourcen aktivieren, indem Sie die Zugriffsrichtlinien erstellen und ändern.
{: shortdesc}

Auf dieser Seite werden Sie durch verschiedene Szenarios zur Verwaltung des Zugriffs auf Ihre Schlüsselressourcen mithilfe der [API für das Zugriffsmanagement ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://iampap.ng.bluemix.net/v1/docs/#!/Access_Policies/){: new_window} geführt.


Vorbereitende Schritte:
- [IAM-Token und Bereichs-GUID abrufen](/docs/services/keymgmt/keyprotect_authentication.html)
- [Schlüssel-ID zur Angabe der Ressourcen abrufen](/docs/services/keymgmt/keyprotect_view_keys.html)
- [Konto-ID zur Angabe des Geltungsbereichs für den Zugriff abrufen](keyprotect_manage_access_api.html#retrieve_account_ID)
- [Benutzer-ID des Benutzers abrufen, dessen Zugriff geändert werden soll](keyprotect_manage_access_api.html#retrieve_user_ID)

## Neue Zugriffsrichtlinie erstellen
{: #create_policy}

Zur Aktivierung der Zugriffssteuerung für einen bestimmten Schlüssel können Sie eine Anforderung an {{site.data.keyword.iamshort}} senden, indem Sie den folgenden Befehl ausführen. Wiederholen Sie den Befehl für jede Zugriffsrichtlinie.

```cURL
curl -X POST \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
  "roles": [
    {
      "id": "crn:v1:bluemix:public:iam::::role:<IAM_role>"
    }
  ],
  "resources": [
    {
      "serviceName": "IBM Key Protect",
      "region": "us-south",
      "resourceType": "key",
      "resource": "<key_ID>",
      "accountId": "<account_ID>",
      "spaceId": "<space_GUID>"
    }
  ]
}'
```
{: codeblock}

Ersetzen Sie `<account_ID>`, `<user_ID>`, `<Admin_IAM_token>`, `<IAM_role>`, `<space_GUID>` und `<key_ID>` durch die entsprechenden Werte.

**Optional:** Überprüfen Sie, ob die Richtlinie erfolgreich erstellt wurde.

```cURL
curl -X GET \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}


## Zugriffsrichtlinie aktualisieren
{: #update_policy}

Sie können eine abgerufene Richtlinien-ID verwenden, um eine vorhandene Richtlinie für einen Benutzer zu ändern. Senden Sie eine Anforderung an {{site.data.keyword.iamshort}}, indem Sie den folgenden Befehl ausführen:

```cURL
curl -X PUT \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies/<policy_ID> \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'If-Match': <ETag_ID> \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
  "roles": [
    {
      "id": "crn:v1:bluemix:public:iam::::role:<IAM_role>"
    }
  ],
  "resources": [
    {
      "serviceName": "IBM Key Protect",
      "region": "us-south",
      "resourceType": "key",
      "resource": "<key_ID>",
      "accountId": "<account_ID>",
      "spaceId": "<space_GUID>"
    }
  ]
}'
```
{: codeblock}

Ersetzen Sie `<account_ID>`, `<user_ID>`, `<policy_ID>`, `<Admin_IAM_token>`, `<ETag_ID>`, `<IAM_role>`, `<space_GUID>` und `<key_ID>` durch die entsprechenden Werte.

**Optional:** Überprüfen Sie, ob die Richtlinie erfolgreich aktualisiert wurde.

```cURL
curl -X GET \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

## Zugriffsrichtlinie löschen
{: #delete_policy}

Sie können eine abgerufene Richtlinien-ID verwenden, um eine vorhandene Richtlinie für einen Benutzer zu löschen. Senden Sie eine Anforderung an {{site.data.keyword.iamshort}}, indem Sie den folgenden Befehl ausführen:

```cURL
curl -X DELETE \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies/<policy_ID> \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

Ersetzen Sie `<account_ID>`, `<user_ID>`, `<policy_ID>` und `<Admin_IAM_token>` durch die entsprechenden Werte.

**Optional:** Überprüfen Sie, ob die Richtlinie erfolgreich gelöscht wurde.

```cURL
curl -X GET \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

## Konto-ID abrufen
{: #retrieve_account_id}

1. Melden Sie sich bei der Bluemix-CLI an.
    ```sh
    bx login [--sso]
    ```
    {: codeblock}

    **Anmerkung**: Der Parameter `--sso` ist für die Anmeldung mit einer eingebundenen ID erforderlich. Rufen Sie bei Verwendung dieser Option den in der CLI-Ausgabe aufgeführten Link auf, um einen einmaligen Kenncode zu generieren.

    Als Ergebnis werden die Identifikationsinformationen für Ihr Konto angezeigt.

    ```sh
    Authentifizieren...
    OK

    Konto auswählen (oder zum Überspringen die Eingabetaste drücken):

    1. Beispielkonto (b6hnh3560ehqjkf89s4ba06i367801e)
    Zahl eingeben> 1
    Als Ziel ausgewähltes Konto Beispielkonto (b6hnh3560ehqjkf89s4ba06i367801e)

    API-Endpunkt:   https://api.ng.bluemix.net (API-Version: 2.75.0)
    Region:         us-south
    Benutzer:       admin
    Konto:          Beispielkonto (b6hnh3560ehqjkf89s4ba06i367801e)
    ```
    {: screen}
2. Kopieren Sie den Wert für die eigene Konto-ID.

## Benutzer-ID abrufen
{: #retrieve_user_id}

1. [Fordern Sie den Benutzer zur Angabe seines IAM-Tokens auf](/docs/services/keymgmt/keyprotect_authentication.html#retrieve_token).
    Die Struktur des IAM-Tokens lautet wie folgt:

    ```sh
    IAM-Token: Bearer <value>.<value>.<value>
    ```
    {: screen}

2. Kopieren Sie den mittleren Wert und führen Sie den folgenden Befehl aus:
    ```sh
    echo -n "<value>" | base64 --decode
    ```
    {: codeblock}

    Als Ergebnis wird das folgende oder ein vergleichbares JSON-Objekt angezeigt:
   ```json
   {
        "iam_id":"...",
        "id":"...",
        "realmid":"...",
        "identifier":"...",
        "given_name":"...",
        "family_name":"...",
        "name":"...",
        "email":"...",
        "sub":"...",
        "account":{
            "bss":"..."},
            "iat":...,
            "exp":...,
            "iss":"...",
            "grant_type":"...",
            "scope":"...",
            "client_id":"..."
        }
   }
   ```
   {: screen}

4. Kopieren Sie den Wert der Eigenschaft `id`.
