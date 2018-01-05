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

# Importation de clés standard
{: #import_standard_keys}

Vous pouvez ajouter des clés de chiffrement existantes à l'aide de l'interface graphique {{site.data.keyword.keymanagementserviceshort}} ou à l'aide d'un programme via l'API {{site.data.keyword.keymanagementserviceshort}}.

## Importation de clés standard à l'aide de l'interface graphique
{: #import_standard_key_GUI}

[Après avoir créé une instance du service](/docs/services/keymgmt/keyprotect_provision.html), procédez comme suit pour entrer votre clé standard existante à l'aide de l'interface graphique {{site.data.keyword.keymanagementserviceshort}}.

1. [Connectez-vous à la console {{site.data.keyword.cloud_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/).
2. Dans votre tableau de bord {{site.data.keyword.cloud_notm}}, sélectionnez l'instance {{site.data.keyword.keymanagementserviceshort}} mise à disposition.
2. Pour importer une nouvelle clé, cliquez sur **Add key** et sélectionnez la fenêtre **Enter existing key**.

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
        <td>[Type de clé](/docs/services/keymgmt/keyprotect_envelope.html#key_types) que vous souhaitez gérer dans {{site.data.keyword.keymanagementserviceshort}}. Dans la liste des types de clé, sélectionnez <b>Standard Key</b>.</td>
      </tr>
      <tr>
        <td>Key material</td>
        <td>Matériel relatif à la clé, comme une clé symétrique, que vous souhaitez gérer dans le service. La clé doit être codée en base64.</td>
      </tr>
      <caption style="caption-side:bottom;">Tableau 1. Description des paramètres <b>Generate new key</b></caption>
    </table>

3. Une fois les détails de la clé indiqués, cliquez sur **Generate new key** pour confirmer l'opération. 

## Création de clés standard à l'aide de l'API 
{: #create_standard_key_API}

Créez une clé standard en soumettant un appel `POST` au noeud final suivant :

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
      -H 'prefer: <return_preference>' \
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
       "payload": "<key_material>",
       "extractable": true
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
        <td><em>return_preference</em></td>
        <td><p>Facultatif : En-tête qui modifie le comportement du serveur pour les opérations <code>POST</code> et <code>DELETE</code>.</p><p>Lorsque vous affectez la valeur <code>return=minimal</code> à la variable <em>return_preference</em>, le service renvoie uniquement les métadonnées de la clé, comme le nom et l'ID de la clé, dans la section entity-body de la réponse. Si cette variable a pour valeur <code>return=representation</code>, le service renvoie à la fois le matériel relatif à la clé et ses métadonnées pour la clé standard.</p></td>
      </tr>
      <tr>
        <td><em>key_alias</em></td>
        <td>Nom lisible pour une identification facile de votre clé.</td>
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
        <td><em>key_material</em></td>
        <td>Matériel relatif à la clé, comme une clé symétrique, que vous souhaitez gérer dans le service. La clé doit être codée en base64.</td>
      </tr>
      <tr>
        <td><em>key_type</em></td>
        <td>
          <p>Valeur booléenne qui détermine si le matériel relatif à la clé peut quitter le service.</p>
          <p>Lorsque vous affectez la valeur <code>true</code> à l'attribut <code>extractable</code>, le service désigne la clé en tant que clé standard que vous pouvez stocker dans vos applications ou services.</p>
        </td>
      </tr>
        <caption style="caption-side:bottom;">Tableau 2. Variables requises pour ajouter des clés standard à l'aide de l'API {{site.data.keyword.keymanagementserviceshort}} </caption>
    </table>

    Une réponse `POST /v2/keys/` qui aboutit renvoie la valeur de l'ID de la clé, ainsi que d'autres métadonnées. L'ID est un identificateur unique qui est affecté à la clé et qui est utilisé pour les appels adressés ultérieurement à {{site.data.keyword.keymanagementserviceshort}}.

3. Facultatif : Vérifiez que la clé a été ajoutée en exécutant l'appel suivant pour parcourir les clés de l'instance de service {{site.data.keyword.keymanagementserviceshort}}.

    ```cURL
    curl -X GET \
      https://keyprotect.us-south.bluemix.net/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}


### Etapes suivantes

- Pour en savoir plus sur la gestion de vos clés à l'aide d'un programme, [reportez- vous à la documentation de référence de l'API {{site.data.keyword.keymanagementserviceshort}} afin d'obtenir des exemples de code ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
- Pour obtenir un exemple expliquant comment les clés stockées dans {{site.data.keyword.keymanagementserviceshort}} peuvent fonctionner pour chiffrer et déchiffrer des données, [reportez-vous à l'exemple d'application disponible dans GitHub ![icône Lien externe](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.
