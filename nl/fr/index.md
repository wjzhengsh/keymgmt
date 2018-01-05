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

# Initiation à {{site.data.keyword.keymanagementserviceshort}}

{{site.data.keyword.keymanagementservicefull}} permet de mettre à disposition des clés chiffrées pour des applications au sein des services {{site.data.keyword.cloud_notm}}. Ce tutoriel explique comment créer et ajouter des clés cryptographiques à l'aide du tableau de bord {{site.data.keyword.keymanagementserviceshort}} pour pouvoir gérer le chiffrement de données à partir d'un même emplacement central.
{: shortdesc}

## Initiation aux clés de chiffrement
{: #get_started_keys}

Dans le tableau de bord {{site.data.keyword.keymanagementserviceshort}}, vous pouvez créer des clés pour la cryptographie ou importer des clés existantes. 

Sélectionnez l'un des deux types de clé :

<dl>
  <dt>Root keys (Clés racine)</dt>
    <dd>Les clés racine sont des clés d'encapsulage de clés symétriques que vous pouvez gérer dans leur intégralité dans {{site.data.keyword.keymanagementserviceshort}}. Vous pouvez utiliser une clé racine pour protéger d'autres clés cryptographiques avec un mécanisme de chiffrement avancé.</dd>
  <dt>Standard keys (Clés standard)</dt>
    <dd>Les clés standard sont des clés symétriques utilisées pour la cryptographie. Vous pouvez utiliser une clé standard pour chiffrer et déchiffrer directement des données.</dd>
</dl>

## Création de clés
{: #creating_keys}

[Une fois que vous avez créé une instance {{site.data.keyword.keymanagementserviceshort}}](https://console.ng.bluemix.net/catalog/services/key-protect/?taxonomyNavigation=apps), vous êtes prêt à désigner des clés dans le service. 

Pour créer votre première clé cryptographique, procédez comme suit : 

1. Dans le tableau de bord {{site.data.keyword.keymanagementserviceshort}}, cliquez sur **Gérer** &gt; **Add key**.
2. Pour créer une clé, sélectionnez la fenêtre **Generate a new key**.

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
        <td>[Type de clé](/docs/services/keymgmt/keyprotect_envelope.html#key_types) que vous souhaitez gérer dans {{site.data.keyword.keymanagementserviceshort}}. </td>
      </tr>
      <caption style="caption-side:bottom;">Tableau 1. Description des paramètres de génération d'une nouvelle clé</caption>
    </table>

3. Une fois les détails de la clé indiqués, cliquez sur **Generate new key** pour confirmer l'opération. 

Les clés créées dans le service sont des clés symétriques de 256 bits prises en charge par l'algorithme AES-GCM. Pour renforcer la sécurité, elles sont générées par des modules HSM (Hardware Security Module) certifiés FIPS 140-2 niveau 2 résidant dans des centres de données {{site.data.keyword.cloud_notm}} sécurisés. 

## Ajout de clés existantes
{: #adding_keys}

Vous pouvez bénéficier des avantages du mécanisme BYOK (Bring Your Own Key) en intégrant vos propres clés au service. 

Pour ajouter une clé existante, procédez comme suit :

1. Dans le tableau de bord {{site.data.keyword.keymanagementserviceshort}}, cliquez sur **Gérer** &gt; **Add key**.
2. Pour charger une clé existante, sélectionnez la fenêtre **Enter existing key**.

    Spécifiez les détails relatifs à la clé :

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
        <td>[Type de clé](/docs/services/keymgmt/keyprotect_envelope.html#key_types) que vous souhaitez gérer dans {{site.data.keyword.keymanagementserviceshort}}. </td>
      </tr>
      <tr>
        <td>Key material</td>
        <td>Obligatoire uniquement si vous ajoutez une clé existante. Le matériel relatif à la clé peut être n'importe quel type de données, comme une clé symétrique, que vous souhaitez stocker dans le service {{site.data.keyword.keymanagementserviceshort}}. La clé que vous indiquez doit être codée en base64.</td>
      </tr>
      <caption style="caption-side:bottom;">Tableau 2. Description des paramètres de saisie d'une clé existante</caption>
    </table>

3. Une fois les détails de la clé indiqués, cliquez sur **Add new key** pour confirmer l'opération. 

Dans le tableau de bord {{site.data.keyword.keymanagementserviceshort}}, vous pouvez examiner les caractéristiques générales des nouvelles clés. 

## Etapes suivantes

Vous pouvez désormais utiliser vos clés pour coder vos applications et services.

- Pour en savoir plus sur la gestion des clés à l'aide d'un programme, [reportez-vous à la documentation de référence de l'API {{site.data.keyword.keymanagementserviceshort}} afin d'obtenir des exemples de code ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
- Pour obtenir un exemple expliquant comment les clés stockées dans {{site.data.keyword.keymanagementserviceshort}} peuvent fonctionner pour chiffrer et déchiffrer des données, [reportez-vous à l'exemple d'application disponible dans GitHub ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.
- Pour plus d'informations sur l'intégration du service {{site.data.keyword.keymanagementserviceshort}} à d'autres solutions de données de cloud, [reportez-vous à documentation relative à l'intégration](/docs/services/keymgmt/keyprotect_integration.html).
