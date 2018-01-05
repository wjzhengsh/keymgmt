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

# Affichage des clés
{: #viewing-keys}

{{site.data.keyword.keymanagementservicefull}} fournit un système centralisé pour afficher et gérer vos clés de chiffrement et en effectuer un audit. Cette dernière opération ainsi que les restrictions d'accès aux clés vous permettent d'assurer la sécurité de vos ressources.
{: shortdesc}

Effectuez un audit régulier de la configuration de vos clés :

- Voyez quand les clés ont été créées et déterminez s'il n'est pas temps de les renouveler.
- [Surveillez les appels d'API à {{site.data.keyword.keymanagementserviceshort}} à l'aide d'{{site.data.keyword.cloudaccesstrailshort}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](/docs/services/cloud-activity-tracker/svcs/kp_at.html#kp_at){: new_window}.
- Vérifiez quels sont les utilisateurs qui ont accès aux clés et assurez-vous que leur niveau d'accès est approprié.

Pour plus d'informations sur l'audit d'accès à vos ressources, voir la [gestion de l'accès utilisateur avec Cloud IAM](/docs/services/keymgmt/keyprotect_manage_access.html).

## Affichage des clés avec l'interface graphique utilisateur
{: #gui}

Si vous préférez examiner les clés de votre service à l'aide d'une interface graphique, vous pouvez utiliser le tableau de bord {{site.data.keyword.keymanagementserviceshort}}.

[Après avoir créé ou importé les clés existantes dans le service](/docs/services/keymgmt/keyprotect_create_keys.html), vous pouvez les afficher en procédant comme suit :

1. [Connectez-vous à la console {{site.data.keyword.cloud_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.bluemix.net/).
2. Dans votre tableau de bord {{site.data.keyword.cloud_notm}}, sélectionnez votre instance de {{site.data.keyword.keymanagementserviceshort}} à disposition.
3. Parcourez les caractéristiques générales de vos clés dans le tableau de bord {{site.data.keyword.keymanagementserviceshort}} :

    <table>
      <tr>
        <th>Colonne</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Nom</td>
        <td>Alias unique et lisible qui est affecté à votre clé.</td>
      </tr>
      <tr>
        <td>ID</td>
        <td>ID de clé unique affecté à votre clé par {{site.data.keyword.keymanagementserviceshort}}. Vous pouvez utiliser la valeur de l'ID pour appeler le service avec l'[API {{site.data.keyword.keymanagementserviceshort}}](https://console.ng.bluemix.net/apidocs/639).</td>
      </tr>
      <tr>
        <td>Etat</td>
        <td>[Etat des clés](/docs/services/keymgmt/keyprotect_states.html) basé sur le document [NIST Special Publication 800-57, Recommendation for Key Management ![icône Lien externe](../../icons/launch-glyph.svg "External link icon")](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf). Ces états sont <i>Pré-actif</i>, <i>Actif</i>, <i>Désactivé</i> et <i>Détruit</i>.</td>
      </tr>
      <tr>
        <td>Type</td>
        <td>[Type de clé](/docs/services/keymgmt/keyprotect_envelope.html#key_types) qui décrit la fonction définie de la clé dans le service.</td>
      </tr>
      <caption style="caption-side:bottom;">Tableau 1. Description du tableau <b>Clés</b></caption>
    </table>

## Affichage des clés avec l'API
{: #api}

Vous pouvez extraire le contenu de vos clés à l'aide de l'API {{site.data.keyword.keymanagementserviceshort}}.

### Etape 1 : Extraction d'une collection de clés
{: #retrieve_keys_api}

Pour obtenir une vue globale, vous pouvez parcourir les clés qui sont gérées dans votre instance {{site.data.keyword.keymanagementserviceshort}} en soumettant une demande `GET` au noeud final suivant :

```
https://key-protect.us-south.bluemix.net/api/v2/keys
```
{: codeblock}

1. [Extrayez vos données d'authentification et de service afin d'utiliser les clés dans le service.](/docs/services/keymgmt/keyprotect_authentication.html)
2. Exécutez la commande cURL suivante pour afficher les caractéristiques générales de vos clés :

    ```cURL
    curl -X GET \
    https://key-protect.us-south.bluemix.net/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <IAM_token>' \
    -H 'bluemix-instance: <instance_ID>' \
    -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

    Pour utiliser les clés dans une organisation et un espace Cloud Foundry de votre compte, remplacez `Bluemix-Instance` par les en-têtes `Bluemix-org` et `Bluemix-space` appropriés. [Pour obtenir des exemples de code, voir la documentation de référence de l'API {{site.data.keyword.keymanagementserviceshort}} ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
    {: tip}

    Remplacez les variables dans l'exemple de demande en fonction du tableau suivant :
    <table>
      <tr>
        <th>Variable</th>
        <th>Description</th>
      </tr>
      <tr>
        <td><em>IAM_token</em></td>
        <td>Votre jeton d'autorisation. Incluez l'ensemble du contenu du jeton <code>IAM</code>, y compris la valeur Bearer, dans la demande cURL.</td>
      </tr>
      <tr>
        <td><em>instance_ID</em></td>
        <td>Identificateur unique affecté à votre instance de service {{site.data.keyword.keymanagementserviceshort}}. </td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>Facultatif: identificateur unique qui est utilisé pour suivre et corréler des transactions.</td>
      </tr>
      <caption style="caption-side:bottom;">Tableau 2. Variables requises pour afficher des clés avec l'API {{site.data.keyword.keymanagementserviceshort}}.</caption>
    </table>

    Une demande `POST /v2/keys/` qui aboutit renvoie une collection de clés disponibles dans votre instance de service {{site.data.keyword.keymanagementserviceshort}}.

    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.collection+json",
        "collectionTotal": 2
      },
    "resources": [
      {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Standard key",
          "description": "...",
          "state": 1,
          "crn": "...",
          "algorithmType": "AES",
          "createdBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "256",
            "mode": "GCM"
          },
          "extractable": true
        },
        {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Root key",
          "description": "...",
          "state": 1,
          "crn": "...",
          "algorithmType": "AES",
          "createdBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "256",
            "mode": "GCM"
          },
          "extractable": false
        }
      ]
    }
    ```
    {:screen}

### Etape 2 : Extraction d'une clé via son ID
{: #retrieve_key_api}

Pour afficher des informations détaillées sur une clé spécifique, vous pouvez effectuer un appel `GET` ultérieur vers le noeud final suivant :

```
https://key-protect.us-south.bluemix.net/api/v2/keys<key_ID>
```
{: codeblock}

1. [Extrayez vos données d'authentification et de service afin d'utiliser les clés dans le service.](/docs/services/keymgmt/keyprotect_authentication.html)
2. Extrayez l'ID de la clé que vous souhaitez gérer ou à laquelle vous souhaitez accéder.

    La valeur d'ID permet d'accéder à des informations détaillées sur la clé, comme le matériel relatif à la clé, par exemple. Vous pouvez extraire l'ID d'une clé spécifique en lançant une demande `GET /v2/keys`, ou en accédant à l'interface graphique utilisateur {{site.data.keyword.keymanagementserviceshort}}.

3. Exécutez la commande cURL suivante pour obtenir des détails sur votre clé et sur le matériel relatif à la clé.

    ```cURL
    curl -X GET \
      https://key-protect.us-south.bluemix.net/api/v2/keys<key_ID> \
      -H 'accept: application/vnd.ibm.kms.key+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

    Remplacez les variables dans l'exemple de demande en fonction du tableau suivant :

    <table>
      <tr>
        <th>Variable</th>
        <th>Description</th>
      </tr>
      <tr>
        <td><em>IAM_token</em></td>
        <td>Votre jeton d'autorisation. Incluez l'ensemble du contenu du jeton `IAM`, y compris la valeur Bearer, dans la demande cURL.</td>
      </tr>
      <tr>
        <td><em>instance_ID</em></td>
        <td>Identificateur unique affecté à votre instance de service {{site.data.keyword.keymanagementserviceshort}}. </td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>Facultatif: identificateur unique qui est utilisé pour suivre et corréler des transactions.</td>
      </tr>
      <tr>
        <td><em>key_ID</em></td>
        <td>Identificateur de la clé que vous avez extraite à l'[étape 1](#retrieve_keys_api).</td>
      </tr>
      <caption style="caption-side:bottom;">Tableau 3. Variables requises pour afficher une clé spécifique avec l'API {{site.data.keyword.keymanagementserviceshort}}.</caption>
    </table>

    Une réponse `GET v2/keys/<key_ID>` qui aboutit renvoie des détails sur votre clé et sur le matériel relatif à la clé. L'objet JSON suivant présente un exemple de valeur renvoyée pour une clé standard :

    ```
    {
        "metadata": {
            "collectionTotal": 1,
            "collectionType": "application/vnd.ibm.kms.key+json"
        },
    "resources": [
      {
            "id": "...",
            "type": "application/vnd.ibm.kms.key+json",
            "name": "Standard key",
            "description": "...",
            "state": 1,
            "crn": "...",
            "algorithmType": "AES",
            "payload": "...",
            "createdBy": "...",
            "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
            "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
            "algorithmMetadata": {
                "bitLength": "256",
                "mode": "GCM"
            },
            "extractable": true
        }
      ]
    }
    ```
    {:screen}

    Pour obtenir une description détaillée des paramètres disponibles, consultez la [documentation de référence de l'API REST {{site.data.keyword.keymanagementserviceshort}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
