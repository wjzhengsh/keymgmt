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

# Création de clés racine
{: #create_root_keys}

Vous pouvez utiliser {{site.data.keyword.keymanagementservicefull}} pour créer des clés racine à l'aide de l'interface graphique {{site.data.keyword.keymanagementserviceshort}} ou d'un programme via l'API {{site.data.keyword.keymanagementserviceshort}}.
{: shortdesc}

Les clés racine sont des clés symétriques d'encapsulage de clés qui permettent de protéger les données chiffrées dans le cloud. Pour plus d'informations sur les clés racine, voir la rubrique [Chiffrement d'enveloppe](/docs/services/keymgmt/keyprotect_envelope.html). 

## Création de clés racine avec l'interface graphique
{: #create_root_key_GUI}

[Après avoir créé une instance du service](/docs/services/keymgmt/keyprotect_provision.html), procédez comme suit pour créer une clé standard avec l'interface graphique {{site.data.keyword.keymanagementserviceshort}}.

1. [Connectez-vous à la console {{site.data.keyword.cloud_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.bluemix.net/).
2. Dans votre tableau de bord {{site.data.keyword.cloud_notm}}, sélectionnez l'instance {{site.data.keyword.keymanagementserviceshort}} mise à disposition.
2. Pour créer une clé, cliquez sur **Add key** et sélectionnez la fenêtre **Generate a new key**.

    Indiquez les détails relatifs à la clé :

    <table>
      <tr>
        <th>Paramètre</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Name</td>
        <td>Alias unique et lisible à affecter à votre clé. Choisissez un nom qui permet d'identifier plus facilement la clé (en rapport avec la fonction remplie par cette clé ou la personne à laquelle la clé est associée, par exemple).</td>
      </tr>
      <tr>
        <td>Key type</td>
        <td>[Type de clé](/docs/services/keymgmt/keyprotect_envelope.html#key_types) que vous souhaitez gérer dans {{site.data.keyword.keymanagementserviceshort}}. Dans la liste des types de clés, sélectionnez <b>Root key</b>.</td>
      </tr>
      <caption style="caption-side:bottom;">Tableau 1. Description des paramètres <b>Generate new key</b></caption>
    </table>

3. Une fois les détails de la clé indiqués, cliquez sur **Generate new key** pour confirmer l'opération. 

## Création de clés racine avec l'API
{: #create_root_key_API}

Créez une clé racine en soumettant une demande `POST` au noeud final suivant :

```
https://keyprotect.us-south.bluemix.net/api/v2/keys
```
{: codeblock}

1. [Extrayez vos données d'authentification et de service afin d'utiliser les clés dans le service](/docs/services/keymgmt/keyprotect_authentication.html).

2. Appelez l'API [{{site.data.keyword.keymanagementserviceshort}}](https://console.ng.bluemix.net/apidocs/639) à l'aide de la commande cURL suivante :

    ```cURL
    curl -X POST \
      https://keyprotect.us-south.bluemix.net/api/v2/keys \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key+json' \
      -H 'correlation-id: <correlation_ID>' \
      -d '{
     "metadata": {
       "collectionType": "application/vnd.ibm.kms.key+json",
       "collectionTotal": 1
     },
     "resources": [
       {
       "type": "application/vnd.ibm.kms.key+json",
       "name": "<key_alias>",
       "description": "<key_description>",
       "expirationDate": "<YYYY-MM-DDTHH:MM:SS.SSZ>",
       "extractable": false
       }
     ]
    }'
    ```
    {: codeblock}

    Pour utiliser les clés dans une organisation et un espace Cloud Foundry spécifiques de votre compte, remplacez `Bluemix-Instance` par les en-têtes `Bluemix-org` et `Bluemix-space` appropriés. [Pour obtenir des exemples de code, voir la documentation de référence de l'API {{site.data.keyword.keymanagementserviceshort}} ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
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
        <td>Identificateur unique qui est utilisé pour suivre et corréler des transactions.</td>
      </tr>
      <tr>
        <td><em>key_alias</em></td>
        <td>Nom unique et lisible permettant d'identifier facilement votre clé.</td>
      </tr>
      <tr>
        <td><em>key_description</em></td>
        <td>Description étendue de votre clé.</td>
      </tr>
      <tr>
        <td><em>YYYY-MM-DD</em><br><em>HH:MM:SS.SS</em></td>
        <td>Facultatif : date et heure d'expiration de la clé dans le système, au format RFC 3339. Si l'attribut <code>expirationDate</code> est omis, la clé n'expire pas. </td>
      </tr>
      <tr>
        <td><em>key_type</em></td>
        <td>
          <p>Valeur booléenne qui détermine si le matériel relatif à la clé peut quitter le service.</p>
          <p>Lorsque vous affectez l'attribut <code>false</code> à <code>extractable</code>, le service crée une clé racine que vous pouvez utiliser pour des opérations <code>wrap</code> ou <code>unwrap</code>.</p>
        </td>
      </tr>
        <caption style="caption-side:bottom;">Tableau 1. Variables requises pour ajouter des clés racine avec l'API {{site.data.keyword.keymanagementserviceshort}} </caption>
    </table>

    Une réponse `POST /v2/keys/` qui aboutit renvoie la valeur de l'ID de la clé, ainsi que d'autres métadonnées. L'ID est un identificateur unique qui est affecté à la clé et qui est utilisé pour les appels adressés ultérieurement à {{site.data.keyword.keymanagementserviceshort}}.

3. Facultatif : Vérifiez que la clé a été créée en exécutant l'appel suivant pour parcourir les clés de l'instance de service {{site.data.keyword.keymanagementserviceshort}}.

    ```cURL
    curl -X GET \
      https://keyprotect.us-south.bluemix.net/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

**Remarque :** Lorsque vous créez une clé racine avec le service, la clé reste dans les limites de {{site.data.keyword.keymanagementserviceshort}} et son matériel ne peut pas être extrait.  

### Etapes suivantes

- Pour plus d'informations sur la protection de clés à l'aide du chiffrement d'enveloppe, voir la rubrique relative à [l'encapsulage de clés](/docs/services/keymgmt/keyprotect_wrap_keys.html).
- Pour en savoir plus sur la gestion de vos clés à l'aide d'un programme, [reportez-vous à la documentation de référence de l'API {{site.data.keyword.keymanagementserviceshort}} afin d'obtenir des exemples de code ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
