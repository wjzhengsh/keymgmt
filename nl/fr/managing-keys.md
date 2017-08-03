---

copyright:
  years: 2017
lastupdated: "2017-08-03"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Gestion des clés

Vous pouvez gérer le cycle de vie de vos clés en utilisant {{site.data.keyword.keymanagementservicelong}} for {{site.data.keyword.Bluemix_short}}.
{: shortdesc}

Il est recommandé de gérer vos clés de manière sécurisée lors de la phase de développement de votre code. Pensez par exemple aux types d'instructions suivantes, parmi d'autres pratiques de codage sécurisées.

- Lorsque vous intégrez des clés à votre code, tenez compte des implications sur la sécurité.
- Créez des clés uniquement en vue d'un accès par programmation à vos applis et ressources. Ne créez pas de clés lorsque vous pouvez accorder des [droits utilisateur![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.bluemix.net/docs/admin/patterns.html#userroles){: new_window}, plus simples.
- Renouvelez les clés et supprimez les clés non utilisées.
- Utilisez l'authentification multi-facteur pour les opérations sensibles.
- Isolez les applications en définissant des clés distinctes pour chacune.
- Envisagez d'utiliser l'API par programmation quand vous transférez des informations très sensibles.

## Génération de données d'authentification pour l'API {{site.data.keyword.keymanagementserviceshort}}
{: #authentication_api}

{{site.data.keyword.keymanagementservicelong_notm}} fournit une méthode d'API REST qui peut être utilisée avec tout langage de programmation pour stocker, extraire et générer des clés.

Pour utiliser l'API, vous devez générer vos données d'authentification et de service.

1. Connectez-vous à {{site.data.keyword.Bluemix_notm}} via l'interface de ligne de commande Cloud Foundry.

    ```
    cf login [a api.DomainName] [-sso]
    ```
    {: codeblock}

2. Sélectionnez l'organisation {{site.data.keyword.Bluemix_notm}} et l'espace qui contient votre instance de service Key Protect.
    Notez les noms de votre organisation et de votre espace dans la sortie d'interface de ligne de commande. Vous pouvez aussi exécuter `cf
target` pour afficher ces informations.
3. Extrayez les identificateurs globaux uniques de votre organisation et de votre espace {{site.data.keyword.Bluemix_notm}}.

    ```
    cf org nom_organisation --guid
    cf space nom_espace --guid
    ```
    {: codeblock}

4. Demandez un jeton d'accès {{site.data.keyword.Bluemix_notm}}.

    ```
    cf oauth-token
    ```
    {: codeblock}

    L'extrait d'exemple suivant montre la sortie de jeton {{site.data.keyword.Bluemix_notm}}. La variable _bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7_ est un jeton d'accès exemple.

    ```
    bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7...
    ```
    {: screen}

Que faire ensuite :

Consultez la {{site.data.keyword.keymanagementserviceshort}} [documentation de référence de l'API REST ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.ng.bluemix.net/apidocs/639){: new_window} pour commencer à gérer des clés dans votre espace.


## Création de clés avec l'API {{site.data.keyword.keymanagementserviceshort}}
{: #codingapps}

Vous pouvez utiliser l'API {{site.data.keyword.keymanagementservicelong_notm}} pour sécuriser les clés existantes ou pour générer de nouvelles clés.

Créez des clés ou ajoutez des clés existantes en effectuant un appel **POST** dans le noeud final suivant :

```
https://ibm-key-protect.edge.bluemix.net/api/v2/secrets
```
{: codeblock}

Si vous désirez essayer le service avant d'ajouter vos propres clés, examinez l'[exemple d'application ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.

1. [Extrayez votre jeton d'accès {{site.data.keyword.Bluemix_notm}}, l'identificateur global unique de l'organisation, ainsi que celui de l'espace, pour utiliser des clés dans le service](#authentication_api).

2. Appelez l'API [{{site.data.keyword.keymanagementserviceshort}}](https://console.ng.bluemix.net/apidocs/639) à l'aide de la commande cURL suivante.

  ```cURL
  curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: jeton_d'accès_bluemix' --header 'Bluemix-Space: identificateur_unique_espace' --header 'Bluemix-Org: identificateur_unique_organisation' -d '{
    "metadata": {
      "collectionType": "application/vnd.ibm.kms.secret+json",
      "collectionTotal": 1
    },
    "resources": [
      {
      "type": "application/vnd.ibm.kms.secret+json",
      "name": "alias_clé",
      "description": "description_clé",
      "expirationDate": "AAAA-MM-JJTHH:MM:SS.SSZ",
      "payload": "contenu_clé"
      }
    ]
  }' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets'
  ```
  {: codeblock}

  Remplacez les variables dans la demande exemple en fonction du tableau suivant.
  <table>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><em>jeton_accès_bluemix</em></td>
      <td>Votre jeton d'autorisation. Incluez le contenu complet du jeton, y-compris la valeur Bearer, dans la demande cURL.</td>
    </tr>
    <tr>
      <td><em>identificateur_global_unique_espace</em></td>
      <td>Identificateur de votre espace {{site.data.keyword.Bluemix_notm}}.</td>
    </tr>
    <tr>
      <td><em>identificateur_global_unique_organisation</em></td>
      <td>Identificateur pour votre organisation {{site.data.keyword.Bluemix_notm}}. </td>
    </tr>
    <tr>
      <td><em>alias_clé</em></td>
      <td>Nom lisible pour une identification facile de votre clé.</td>
    </tr>
    <tr>
      <td><em>description_clé</em></td>
      <td>Description étendue de votre clé.</td>
    </tr>
    <tr>
      <td><em>AAAA-MM-JJ</em><br><em>HH:MM:SS.SS</em></td>
      <td>Facultatif : date et heure d'expiration de la clé dans le système, au format RFC3339. Si l'attribut <code>expirationDate</code> est omis, la clé n'expire pas. </td>
    </tr>
    <tr>
      <td><em>contenu_clé</em></td>
      <td>Matériel relatif à la clé, comme une clé RSA, que vous voulez stocker dans {{site.data.keyword.keymanagementserviceshort}}. Pour générer une nouvelle clé, omettez l'attribut payload et la variable contenu_clé.</td>
    </tr>
      <caption style="caption-side:bottom;">Tableau 1. Variables requises pour ajouter des clés via l'API {{site.data.keyword.keymanagementserviceshort}}</caption>
  </table>

3. Vérifiez que la clé a été a créée en exécutant l'appel ci-après pour obtenir les clés de votre espace {{site.data.keyword.Bluemix_notm}}.

  ```cURL
  curl -X GET --header 'Accept: application/json' --header 'Authorization: jeton_d'accès_bluemix' --header 'Bluemix-Space: identificateur_espace' --header 'Bluemix-Org: identificateur_organisation' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets'
  ```
  {: codeblock}

## Affichage des clés avec l'API {{site.data.keyword.keymanagementserviceshort}}
{: #viewingkeys_api}

Vous pouvez voir le contenu de vos clés via l'API {{site.data.keyword.keymanagementservicelong_notm}}, si vous êtes un développeur ou un gestionnaire d'espace {{site.data.keyword.Bluemix_notm}}.

Pour une vue de haut niveau, vous pouvez parcourir les clés qui sont gérées dans votre espace via l'interface utilisateur {{site.data.keyword.keymanagementserviceshort}}.

Examinez les informations détaillées sur vos clés en effectuant un appel GET au noeud final suivant :

```
https://ibm-key-protect.edge.bluemix.net/api/v2/secrets/ID_clé
```
{: codeblock}

1. Dans l'interface utilisateur {{site.data.keyword.keymanagementserviceshort}}, sous Services de sécurité, vous pouvez observer les caractéristiques générales de vos clés. Vous pouvez parcourir les clés en cliquant sur les en-têtes de colonnes triables.
2. Copiez l'**ID** dans la ligne de la clé. La valeur d'ID est utilisée pour accéder à des informations plus détaillées relatives à la clé dans l'API, comme le matériel relatif à la clé, par exemple.
3. [Extrayez votre jeton d'accès, votre identificateur global unique d'organisation {{site.data.keyword.Bluemix_notm}} et votre identificateur global unique d'espace pour utiliser les clés dans le service.](#authentication_api)
4. Exécutez la commande cURL suivante pour obtenir des détails sur votre clé et sur le matériel relatif à la clé.

  ```cURL
  curl -X GET --header 'Accept: application/json' --header 'Authorization: jeton_d'accès_bluemix' --header 'Bluemix-Space: identificateur_espace' --header 'Bluemix-Org: identificateur_organisation' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets/ID_clé'
  ```
  {: codeblock}

  Remplacez les variables dans la demande exemple en fonction du tableau suivant.
  <table>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><em>jeton_accès_bluemix</em></td>
      <td>Votre jeton d'autorisation. Incluez le contenu complet du jeton, y-compris la valeur Bearer, dans la demande cURL.</td>
    </tr>
    <tr>
      <td><em>identificateur_global_unique_espace</em></td>
      <td>Identificateur aléatoire généré et affecté à votre espace {{site.data.keyword.Bluemix_notm}}.</td>
    </tr>
    <tr>
      <td><em>identificateur_global_unique_organisation</em></td>
      <td>Identificateur généré de façon aléatoire qui est affecté à votre organisation {{site.data.keyword.Bluemix_notm}}.</td>
    </tr>
    <tr>
      <td><em>ID_clé</em></td>
      <td>Identificateur de votre clé que vous avez extrait à l'étape [2](https://console.bluemix.net/docs/services/keymgmt/managing.html#viewingkeys_api__keyid).</td>
    </tr>
    <caption style="caption-side:bottom;">Tableau 2. Variables requises pour afficher les clés via l'API {{site.data.keyword.keymanagementserviceshort}}.</caption>
  </table>

  Le matériel relatif à la clé est retourné dans la section entity-body de la réponse. Les clés, qui sont générées par des modules HSM (Hardware Security Module), sont codées en base 64.

## Audit des clés et des accès
{: #viewkeyassignments}

{{site.data.keyword.keymanagementservicelong_notm}} fournit un système centralisé pour afficher et gérer vos clés de chiffrement et en effectuer un audit. Cette dernière opération ainsi que les restrictions d'accès aux clés vous permettent d'assurer la sécurité de vos ressources.

Effectuez un audit régulier de la configuration de vos clés :

- Voyez quand les clés ont été créées et déterminez s'il n'est pas temps de les renouveler.
- [Surveillez les appels d'API à {{site.data.keyword.keymanagementserviceshort}} à l'aide d'{{site.data.keyword.cloudaccesstrailshort}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.bluemix.net/docs/services/AccessTrail/at_integration.html#at_integration_key_protect){: new_window}.
- Vérifiez quels sont les utilisateurs qui ont accès aux clés et assurez-vous que leur niveau d'accès est approprié.

Pour effectuer un audit des utilisateurs disposant d'un accès, procédez comme suit.

1. En tant que gestionnaire d'espace, allez dans les paramètres de votre compte et sélectionnez **Gérer les organisations**.
2. Ouvrez l'espace qui contient l'instance de service {{site.data.keyword.keymanagementserviceshort}} pour vérifier quels sont les utilisateurs qui y ont accès.
3. Si vous avez besoin d'ajouter des utilisateurs, accédez à **Inviter des membres d'équipe** et sélectionnez les rôles {{site.data.keyword.Bluemix_notm}} qui correspondent aux droits {{site.data.keyword.keymanagementserviceshort}} que vous voulez accorder à l'utilisateur :

  <table>
    <tr>
      <th>Rôles {{site.data.keyword.Bluemix_notm}}</th>
      <th>Droits {{site.data.keyword.keymanagementserviceshort}}</th>
    </tr>
    <tr>
      <td>Gestionnaire d'espace</td>
      <td>Un gestionnaire d'espace peut créer, afficher et supprimer des clés.</td>
    </tr>
    <tr>
      <td>Développeur</td>
      <td>Un développeur peut créer des clés et afficher les détails de ces clés.</td>
    </tr>
    <tr>
      <td>Auditeur</td>
      <td>Un auditeur peut accéder à une vue de haut niveau des clés. </td>
    </tr>
    <caption style="caption-side:bottom;">Tableau 3. Mappage de rôles {{site.data.keyword.Bluemix_notm}} à des permissions {{site.data.keyword.keymanagementserviceshort}}.</caption>
  </table>
