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

# Affichage des clés

Vous pouvez afficher le contenu de vos clés de chiffrement avec {{site.data.keyword.keymanagementservicefull}}.
{: shortdesc}

## Affichage des clés avec l'interface graphique utilisateur
{: #gui}

Pour parcourir les clés de votre service avec l'interface graphique utilisateur {{site.data.keyword.keymanagementserviceshort}}, voir [Initiation à {{site.data.keyword.keymanagementserviceshort}}](/docs/services/keymgmt/index.html#managekey).

## Affichage des clés avec l'API
{: #api}

Vous pouvez extraire le contenu de vos clés à l'aide de l'API {{site.data.keyword.keymanagementserviceshort}}.

### Etape 1 : Extraction d'une collection de clés
{: #retrieve_keys_api}

Pour une vue de haut niveau, vous pouvez parcourir les clés qui sont gérées dans votre espace en effectuant un appel `GET` vers le noeud final suivant :

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys
```
{: codeblock}

1. [Extrayez votre jeton d'autorisation, l'identificateur global unique de l'organisation, ainsi que celui de l'espace, pour utiliser des clés dans le service.](/docs/services/keymgmt/keyprotect_authentication.html).
2. Exécutez la commande cURL suivante pour afficher les caractéristiques générales de vos clés.

    ```cURL
    curl -X GET \
    https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <OAuth_token>' \
    -H 'bluemix-org: <organization_GUID>' \
    -H 'bluemix-space: <space_GUID>' \
    ```
    {: codeblock}

    Remplacez les variables dans la demande exemple en fonction du tableau suivant.
    <table>
      <tr>
        <th>Variable</th>
        <th>Description</th>
      </tr>
      <tr>
        <td><em>OAuth_token</em></td>
        <td>Votre jeton d'autorisation. Incluez le contenu complet du jeton, y-compris la valeur Bearer, dans la demande cURL.</td>
      </tr>
      <tr>
        <td><em>space_GUID</em></td>
        <td>Identificateur unique qui est affecté à votre espace {{site.data.keyword.cloud_notm}}.</td>
      </tr>
      <tr>
        <td><em>organization_GUID</em></td>
        <td>Identificateur unique qui est affecté à votre organisation {{site.data.keyword.cloud_notm}}.</td>
      </tr>
      <caption style="caption-side:bottom;">Tableau 2. Variables requises pour afficher les clés via l'API {{site.data.keyword.keymanagementserviceshort}}.</caption>
    </table>

    Une demande réussie renvoie une collection de clés disponibles dans votre espace {{site.data.keyword.cloud_notm}}.

    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.kms.key+json",
        "collectionTotal": 2
      },
    "resources": [
      {
          "id": "Key ID 1",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Key alias",
          "description": "Key description",
          "state": 1,
          "algorithmType": "AES",
          "createdBy": "v4 UUID of the user who creates the key",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "Key length",
            "mode": "GCM"
          }
        },
        {
          "id": "Key ID 2",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Key alias",
          "description": "Key description",
          "state": 1,
          "algorithmType": "AES",
          "createdBy": "v4 UUID of the user who creates the key",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "Key length",
            "mode": "GCM"
          }
        }
      ]
    }
    ```
    {:screen}

### Etape 2 : Extraction d'une clé via son ID
{: #retrieve_key_api}

Pour afficher des informations détaillées sur une clé spécifique, vous pouvez effectuer un appel `GET` ultérieur vers le noeud final suivant :

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID>
```
{: codeblock}

1. [Extrayez votre jeton d'autorisation, l'identificateur global unique de l'organisation, ainsi que celui de l'espace, pour utiliser des clés dans le service.](/docs/services/keymgmt/keyprotect_authentication.html).
2. Extrayez l'ID de la clé à gérer ou à laquelle vous souhaitez accéder.

    La valeur d'ID est utilisée pour accéder à des informations détaillées sur la clé, comme le matériel relatif à la clé, par exemple. Vous pouvez extraire l'ID d'une clé spécifique en lançant une demande `GET /v2/keys`, ou en accédant à l'interface graphique utilisateur {{site.data.keyword.keymanagementserviceshort}}.

3. Exécutez la commande cURL suivante pour obtenir des détails sur votre clé et sur le matériel relatif à la clé.

    ```cURL
    curl -X GET \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID> \
      -H 'accept: application/vnd.ibm.kms.secret+json' \
      -H 'authorization: Bearer <OAuth_token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

    Remplacez les variables dans la demande exemple en fonction du tableau suivant.

    <table>
      <tr>
        <th>Variable</th>
        <th>Description</th>
      </tr>
      <tr>
        <td><em>OAuth_token</em></td>
        <td>Votre jeton d'autorisation. Incluez le contenu complet du jeton, y-compris la valeur Bearer, dans la demande cURL.</td>
      </tr>
      <tr>
        <td><em>organization_GUID</em></td>
        <td>Identificateur unique qui est affecté à votre organisation {{site.data.keyword.cloud_notm}}.</td>
      </tr>
      <tr>
        <td><em>space_GUID</em></td>
        <td>Identificateur unique qui est affecté à votre espace {{site.data.keyword.cloud_notm}}.</td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>Facultatif: identificateur unique qui est utilisé pour suivre et corréler des transactions.</td>
      </tr>
      <tr>
        <td><em>key_ID</em></td>
        <td>Identificateur de la clé que vous avez extraite à l'[étape 1](#retrieve_keys_api).</td>
      </tr>
      <caption style="caption-side:bottom;">Tableau 2. Variables requises pour afficher une clé spécifique via l'API {{site.data.keyword.keymanagementserviceshort}}.</caption>
    </table>

    Une réponse réussie renvoie des détails sur votre clé et sur le matériel relatif à la clé. L'objet JSON suivant présente un exemple de valeur renvoyée.

    ```
    {
        "metadata": {
            "collectionTotal": 1,
            "collectionType": "application/vnd.ibm.kms.key+json"
        },
    "resources": [
      {
                "createdBy": "...",
                "creationDate": "...",
                "id": "...",
                "name": "...",
                "payload": "...",
                "state": 1,
                "type": "application/vnd.ibm.kms.key+json"
            }
        ]
    }
    ```
    {:screen}

    Pour obtenir une description détaillée des paramètres disponibles, consultez la {{site.data.keyword.keymanagementserviceshort}} [documentation de référence de l'API REST ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
