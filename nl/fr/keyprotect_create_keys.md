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

# Création de clés

Vous pouvez gérer le cycle de vie de vos clés à l'aide d'{{site.data.keyword.keymanagementservicefull}}.
{: shortdesc}

Il est recommandé de gérer vos clés de manière sécurisée lors de la phase de développement de votre code. Pensez par exemple aux instructions suivantes, parmi d'autres pratiques de codage sécurisées.

- Lorsque vous intégrez des clés à votre code, tenez compte des implications sur la sécurité.
- Créez des clés uniquement en vue d'un accès par programmation à vos applis et ressources. Ne créez pas de clés lorsque vous pouvez accorder des [droits utilisateur![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.bluemix.net/docs/admin/patterns.html#userroles){: new_window}, plus simples.
- Renouvelez les clés et supprimez les clés non utilisées.
- Utilisez l'authentification multi-facteur pour les opérations sensibles.
- Isolez les applications en définissant des clés distinctes pour chacune.
- Envisagez d'utiliser l'API par programmation quand vous transférez des informations très sensibles.

Si vous désirez essayer le service avant d'ajouter vos propres clés, examinez l'[exemple d'application ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.

## Création de clés avec l'interface graphique utilisateur
{: #gui}

Pour ajouter des clés à votre service avec l'interface graphique utilisateur {{site.data.keyword.keymanagementserviceshort}}, voir [Initiation à {{site.data.keyword.keymanagementserviceshort}}](/docs/services/keymgmt/index.html#addkey).

## Création de clés avec l'API
{: #api}

Vous pouvez utiliser l'API {{site.data.keyword.keymanagementserviceshort}} pour sécuriser à l'aide d'un programme les clés existantes ou pour générer de nouvelles clés.

Créez des clés ou importez des clés existantes en effectuant un appel `POST` vers le noeud final suivant :

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys
```
{: codeblock}

1. [Extrayez votre jeton d'autorisation, l'identificateur global unique de l'organisation, ainsi que celui de l'espace, pour utiliser des clés dans le service.](/docs/services/keymgmt/keyprotect_authentication.html).

2. Appelez l'API [{{site.data.keyword.keymanagementserviceshort}}](https://console.ng.bluemix.net/apidocs/639) à l'aide de la commande cURL suivante.

    ```cURL
    curl -X POST \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
      -H 'authorization: Bearer <OAuth_token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
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
       "payload": "<key_material>"
       }
     ]
    }'
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
        <td>Identificateur unique qui est affecté à votre organisation {{site.data.keyword.cloud_notm}}. </td>
      </tr>
      <tr>
        <td><em>space_GUID</em></td>
        <td>Identificateur unique qui est affecté à votre espace {{site.data.keyword.cloud_notm}}.</td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>Identificateur unique qui est utilisé pour suivre et corréler des transactions.</td>
      </tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p>En-tête qui modifie le comportement du serveur pour les opérations <code>POST</code> et <code>DELETE</code>.</p><p>Si cette option est définie sur <code>return=minimal</code>, le service renvoie uniquement les métadonnées de clé, telles que le nom de la clé et la valeur <code>id</code>, dans la section entity-body de la réponse. Si cette option est définie sur <code>return=representation</code>, le service renvoie à la fois le matériel relatif à la clé et ses métadonnées.</p></td>
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
        <td>Matériel relatif à la clé, comme une clé RSA, que vous voulez stocker dans {{site.data.keyword.keymanagementserviceshort}}. Pour générer une nouvelle clé, omettez l'attribut <code>payload</code> et la variable <em>key_material</em>.</td>
      </tr>
      <caption style="caption-side:bottom;">Tableau 1. Variables requises pour ajouter des clés via l'API {{site.data.keyword.keymanagementserviceshort}}</caption>
    </table>

    Une réponse réussie renvoie la valeur `id` pour votre clé, ainsi que d'autres métadonnées. `id` est un identificateur unique qui est affecté à votre clé et utilisé pour les appels ultérieurs.

3. **Facultatif :** vérifiez que la clé a été a créée en exécutant l'appel ci-après pour obtenir les clés de votre espace {{site.data.keyword.cloud_notm}}.

    ```cURL
    *    curl -X GET \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <OAuth-token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
    ```
    {: codeblock}

### Etapes suivantes

Vous pouvez désormais utiliser vos clés pour coder vos applications et services.

- Pour obtenir tous les détails relatifs à chaque demande et réponse REST, consultez la {{site.data.keyword.keymanagementserviceshort}} [documentation de référence de l'API REST ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
