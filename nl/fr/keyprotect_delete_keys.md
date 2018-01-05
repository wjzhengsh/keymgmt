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

# Suppression de clés
{: #deleting-keys}

Vous pouvez utiliser {{site.data.keyword.keymanagementservicefull}} pour supprimer une clé de chiffrement et son contenu, si vous êtes administrateur de l'espace {{site.data.keyword.cloud_notm}} ou de l'instance de service {{site.data.keyword.keymanagementserviceshort}}.
{: shortdesc}

**Important :** : lorsque vous supprimez une clé, vous détruisez définitivement son contenu et les données associées. L'action est irréversible. La destruction de ressources n'est pas recommandée dans les environnements de production, mais peut être utile dans les environnements temporaires tels que les environnements de test ou d'assurance qualité.

## Suppression de clés avec l'interface graphique utilisateur
{: #gui}

Si vous préférez supprimer vos clés de chiffrement à l'aide d'une interface graphique, vous pouvez utiliser l'interface graphique utilisateur {{site.data.keyword.keymanagementserviceshort}}.

[Après avoir créé ou importé vos clés existantes dans le service](/docs/services/keymgmt/keyprotect_create_keys.html), procédez comme suit pour supprimer une clé :

1. [Connectez-vous à la console {{site.data.keyword.cloud_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.bluemix.net/).
2. Dans le tableau de bord {{site.data.keyword.cloud_notm}}, sélectionnez l'instance {{site.data.keyword.keymanagementserviceshort}} mise à disposition.
3. Utilisez le tableau **Clés** pour parcourir les clés du service.
4. Cliquez sur l'icône pour ouvrir la liste des options de la clé à supprimer..
5. Dans le menu d'options, cliquez sur **Supprimer la clé** et confirmez la suppression dans l'écran suivant.

Une fois supprimée, la clé passe à l'état _Détruit_. Les clés qui se trouvent dans cet état sont irrécupérables. Les métadonnées associées à la clé, comme la date de suppression de la clé, sont conservées dans la base de données {{site.data.keyword.keymanagementserviceshort}}. 

## Suppression de clés avec l'API
{: #api}

Pour supprimer une clé et son contenu, effectuez un appel `DELETE` vers le noeud final suivant :

```
https://keyprotect.us-south.bluemix.net/api/v2/keys<key_ID>
```

1. [Extrayez vos données d'authentification et de service afin d'utiliser les clés dans le service.](/docs/services/keymgmt/keyprotect_authentication.html)

2. Extrayez l'ID de la clé à supprimer.

    Vous pouvez extraire l'ID d'une clé spécifique en soumettant une demande `GET /v2/keys/` ou en affichant vos clés dans le tableau de bord {{site.data.keyword.keymanagementserviceshort}}.

3. Exécutez la commande cURL suivante pour supprimer définitivement la clé et son contenu :

    ```cURL
    curl -X DELETE \
      https://keyprotect.us-south.bluemix.net/api/v2/keys<key_ID> \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'prefer: <return_preference>'
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
        <td><em>key_ID</em></td>
        <td>Identificateur unique de la clé à supprimer.</td>
      </tr>
      <tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p>En-tête qui modifie le comportement du serveur pour les opérations <code>POST</code> et <code>DELETE</code>.</p><p>Lorsque vous affectez la valeur <code>return=minimal</code> à la variable <em>return_preference</em>, le service renvoie une réponse indiquant que la suppression a abouti. Si cette valeur a pour valeur <code>return=representation</code>, le service renvoie à la fois le matériel relatif à la clé et ses métadonnées.</p></td>
      </tr>
      <caption style="caption-side:bottom;">Tableau 1. Variables requises pour supprimer des clés via l'API {{site.data.keyword.keymanagementserviceshort}}.</caption>
    </table>

    Si la variable _return_preference_ a pour valeur `return=representation`, les détails de la demande `DELETE` sont renvoyés dans la section entity-body de la réponse. <!--After you delete a key, it enters the `Deactivated` key state. After 24 hours, if a key is not reinstated, the key transitions to the `Destroyed` state. The key contents are permanently erased and no longer accessible.--> L'objet JSON suivant présente un exemple de valeur renvoyée.
    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.kms.key+json",
       "collectionTotal": 1
      },
    "resources": [
      {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "...",
          "description": "...",
          "state": 5,
          "crn": "...",
          "deleted": true,
          "algorithmType": "AES",
          "createdBy": "...",
          "deletedBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "deletionDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "nonactiveStateReason": 2,
          "extractable": true
        }
      ]
    }
    ```
    {: screen}

    Pour obtenir une description détaillée des paramètres disponibles, consultez la [documentation de référence de l'API REST {{site.data.keyword.keymanagementserviceshort}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
