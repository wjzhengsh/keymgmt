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

# Suppression de clés

Vous pouvez utiliser {{site.data.keyword.keymanagementservicefull}} pour supprimer une clé de chiffrement et son contenu, si vous êtes administrateur de votre espace {{site.data.keyword.cloud_notm}} ou instance de service {{site.data.keyword.keymanagementserviceshort}}.
{: shortdesc}

**Important** : lorsque vous supprimez une clé, vous détruisez définitivement son contenu et les données associées. L'action est irréversible. La destruction de ressources n'est pas recommandée dans les environnements de production, mais peut être utile dans les environnements temporaires tels que les environnements de test ou d'assurance qualité.

## Suppression de clés avec l'interface graphique utilisateur
{: #gui}

Si vous préférez supprimer vos ressources de clé à l'aide d'une interface graphique, vous pouvez utiliser l'interface graphique utilisateur {{site.data.keyword.keymanagementserviceshort}}.

[Après avoir créé ou importé vos clés existantes dans le service](/docs/services/keymgmt/keyprotect_create_keys.html), procédez comme suit pour supprimer une clé :

1. [Connectez-vous à la console {{site.data.keyword.cloud_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.bluemix.net/).
2. Dans votre tableau de bord {{site.data.keyword.cloud_notm}}, sélectionnez votre instance de {{site.data.keyword.keymanagementserviceshort}} à disposition.
3. Accédez au panneau **Gérer** pour parcourir les clés de votre service.
4. Cliquez sur l'icône en forme d'ellipse verticale ipour ouvrir la liste des options de la clé à supprimer..
5. Dans le menu d'options, cliquez sur **Supprimer la clé** et confirmez la suppression dans l'écran suivant.

## Suppression de clés avec l'API
{: #api}

Pour supprimer une clé et son contenu, effectuez un appel `DELETE` vers le noeud final suivant :

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID>
```

1. [Extrayez votre jeton d'autorisation, l'identificateur global unique de l'organisation, ainsi que celui de l'espace, pour utiliser des clés dans le service.](/docs/services/keymgmt/keyprotect_authentication.html).

2. Extrayez l'ID de la clé à supprimer.

    Vous pouvez extraire l'ID d'une clé spécifique en lançant une demande `GET /v2/keys`, ou en affichant vos clés dans le tableau de bord {{site.data.keyword.keymanagementserviceshort}}.

3. Exécutez la commande cURL suivante pour supprimer définitivement la clé et son contenu.

    ```cURL
    curl -X DELETE \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID> \
      -H 'authorization: Bearer <OAuth_token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
      -H 'prefer: <return_preference>'
    ```
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
      <tr>
        <td><em>key_ID</em></td>
        <td>Identificateur unique de la clé à supprimer.</td>
      </tr>
      <tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p>En-tête qui modifie le comportement du serveur pour les opérations <code>POST</code> et <code>DELETE</code>.</p><p>Si cette option est définie sur <code>return=minimal</code>, le service renvoie uniquement les métadonnées de clé, telles que le nom de la clé et la valeur <code>id</code>, dans la réponse entité-corps. Si cette option est définie sur <code>return=representation</code>, le service renvoie à la fois le contenu de la clé et ses métadonnées.</p></td>
      </tr>
      <caption style="caption-side:bottom;">Tableau 1. Variables requises pour supprimer des clés via l'API {{site.data.keyword.keymanagementserviceshort}}.</caption>
    </table>

    Les détails de la demande `DELETE` sont renvoyés dans la section entity-body de la réponse.
