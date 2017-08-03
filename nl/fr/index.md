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

# Initiation à {{site.data.keyword.keymanagementserviceshort}}

{{site.data.keyword.keymanagementservicelong}} vous permet de mettre à disposition des clés chiffrées pour les applications dans {{site.data.keyword.Bluemix_short}}. Dans le cadre de la gestion du cycle de vie de vos clés, sachez que vos clés sont sécurisées par des modules HSM (Hardware Security Module) basés sur le cloud qui vous protègent contre le vol d'informations.
{: shortdesc}

{{site.data.keyword.keymanagementserviceshort}} est automatiquement disponible pour toutes les applications au sein de l'espace dans lequel il a été créé. [Après avoir créé une instance du service](https://console.ng.bluemix.net/catalog/services/key-protect/?taxonomyNavigation=apps){: new_window}, procédez comme suit pour rendre ce service opérationnel :

1. Pour créer ou envoyer par téléchargement une clé existante, cliquez sur **Ajouter une clé**.
    Spécifiez les détails relatifs à la clé :
    <table>
      <tr>
        <th>Paramètre</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Nom</td>
        <td>Alias lisible à affecter à votre clé. Choisissez un nom qui vous aidera à identifier la clé (en rapport avec le rôle joué par cette clé ou la personne à qui est-elle associée, par exemple).</td>
      </tr>
      <tr>
        <td>Algorithme</td>
        <td>Le chiffrement de clé symétrique est pris en charge par l'algorithme AES-GCM.</td>
      </tr>
      <tr>
        <td>Clé</td>
        <td>Requis uniquement si vous ajoutez une clé existante. Ce peut être tout type de données que vous voulez stocker dans le service {{site.data.keyword.keymanagementserviceshort}}, comme un certificat ou une clé RSA, par exemple.</td>
      </tr>
        <caption style="caption-side:bottom;">Tableau 1. Description des paramètres de clé</caption>
    </table>

2. Lorsque vous avez fini de soumettre les informations sur la clé, cliquez sur **Ajouter une clé** pour confirmer l'opération. Les clés sont immédiatement disponibles. Les nouvelles clés sont générées par des modules HSM (Hardware Security Module) résidant dans des centres de données {{site.data.keyword.IBM}} sécurisés.
3. Copiez l'identificateur de référence dans la ligne de la clé. La valeur **ID** est l'identificateur que vous utilisez dans l'API {{site.data.keyword.keymanagementserviceshort}}.
4. **Facultatif **: si vous désirez supprimer une clé, rappelez-vous que son matériel n'est pas récupérable. Les métadonnées qui sont associées à la clé sont conservées dans la base de données {{site.data.keyword.keymanagementserviceshort}}. Pour supprimer une clé, cliquez sur l'icône **Actions** dans la ligne de la clé puis confirmez la suppression à l'écran suivant.

Suite :

Vous pouvez désormais utiliser vos clés pour coder vos applications et services.

- Pour consulter un exemple de la manière dont le magasin de clés dans {{site.data.keyword.keymanagementserviceshort}} peut être utilisé pour chiffrer et déchiffrer des données, reportez-vous à l'[exemple d'application dans Github ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.
- Pour plus d'informations sur la gestion de vos clés par voie de programmation, reportez-vous à la [documentation de référence de l'API {{site.data.keyword.keymanagementserviceshort}}](https://console.ng.bluemix.net/apidocs/639) pour consulter des exemples de code.

## Liens connexes

- [API REST {{site.data.keyword.keymanagementserviceshort}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.ng.bluemix.net/apidocs/639){: new_window}
- [API REST admin de {{site.data.keyword.keymanagementserviceshort}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs-admin-keyprotect.ng.bluemix.net/){: new_window}
- [Offre HSM sur le cloud ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.softlayer.com/ibm-cloud-hsm){: new_window}
