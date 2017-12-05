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

# Initiation à {{site.data.keyword.keymanagementserviceshort}}

Vous trouverez ci-dessous les étapes requises pour générer, saisir et gérer des clés dans {{site.data.keyword.keymanagementservicefull}}.
{: shortdesc}

## Conditions préalables requises
{: #prereqs }

{{site.data.keyword.keymanagementserviceshort}} est disponible pour les services et applications qui peuvent, avec l'autorisation appropriée, effectuer un appel d'API vers {{site.data.keyword.keymanagementserviceshort}}. Vous aurez besoin des éléments suivants avant d'ajouter une clé.
- [Un IBMid et un mot de passe](https://console.bluemix.net/docs/admin/adminpublic.html#signing-up-for-bluemix){: new_window}
- [Une instance du service](https://console.ng.bluemix.net/catalog/services/key-protect/?taxonomyNavigation=apps){: new_window}

## Ajout d'une clé
{: #addkey }

Procédez comme suit pour créer une clé ou télécharger une clé existante.

1. [Connectez-vous à la console {{site.data.keyword.cloud_notm}}.](https://console.bluemix.net/catalog){: new_window}
2. Survolez le lien **Toutes les catégories** pour faire apparaître la barre de défilement. Faites défiler l'écran jusqu'à **Services > Sécurité**. Une liste de vos applications et services s'affiche.
3. Cliquez deux fois sur votre instance de service **{{site.data.keyword.keymanagementserviceshort}}**. Notez que vous pouvez renommer ou supprimer le service sous **Actions**.

Vous êtes automatiquement redirigé vers la page **Ajouter une nouvelle clé** si vous saisissez ou générez une clé pour la première fois. L'option **Générer une nouvelle clé** est utilisée pour générer une toute nouvelle clé dans {{site.data.keyword.keymanagementserviceshort}}, tandis que **Saisir une clé existante** permet de saisir une clé existante dans le service.

### Génération d'une clé
{: #genkey }

Procédez comme suit pour que {{site.data.keyword.keymanagementserviceshort}} génère une nouvelle clé.

1. Saisissez les informations suivantes sout **Générer une nouvelle clé** pour que {{site.data.keyword.keymanagementserviceshort}} crée un nouvelle clé.
    <table>
      <tr>
        <th>Zone</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Nom</td>
        <td>Alias lisible à affecter à votre clé. Choisissez un nom qui vous aidera à identifier la clé (en rapport avec le rôle joué par cette clé ou la personne à qui est-elle associée, par exemple).</td>
      </tr>
      <tr>
        <td>Type de clé</td>
        <td>Par défaut, il s'agit de la clé standard. Une clé standard est utilisée comme clé de chiffrement de données pour chiffrer vos données de texte brut en texte chiffré.</td>
      </tr>
        <caption style="caption-side:bottom;">Tableau 1. Description des paramètres de l'option Générer une nouvelle clé</caption>
    </table>

2. Cliquez sur le bouton **Générer une clé**. Les clés sont immédiatement disponibles. Les nouvelles clés sont générées par des modules HSM (Hardware Security Module) résidant dans des centres de données {{site.data.keyword.IBM}} sécurisés.
3. Copiez l'identificateur de référence dans la ligne de la clé. La valeur **ID** est l'identificateur que vous utilisez dans l'API {{site.data.keyword.keymanagementserviceshort}}.

### Saisie d'une clé existante
{: #existkey }

Procédez comme suit pour saisir une clé existante dans Key Protect.

1. Entrez les informations suivantes sous **Saisir une clé existante**.
    <table>
      <tr>
        <th>Zone</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Nom</td>
        <td>Alias lisible à affecter à votre clé. Choisissez un nom qui vous aidera à identifier la clé (en rapport avec le rôle joué par cette clé ou la personne à qui est-elle associée, par exemple).</td>
      </tr>
      <tr>
        <td>Type de clé</td>
        <td>Par défaut, il s'agit de la clé standard. Une clé standard est utilisée comme clé de chiffrement de données pour chiffrer vos données de texte brut en texte chiffré.</td>
      </tr>
      <tr>
        <td>Matériel relatif à la clé</td>
        <td>Il peut s'agir de tout type de données que vous souhaitez stocker dans le service {{site.data.keyword.keymanagementserviceshort}}, comme un certificat ou une clé RSA.</td>
      </tr>
        <caption style="caption-side:bottom;">Tableau 2. Description des paramètres de l'option Saisir une clé existante</caption>
    </table>

2. Cliquez sur le bouton **Ajouter une nouvelle clé**. Les clés sont immédiatement disponibles.
3. Copiez l'identificateur de référence dans la ligne de la clé. La valeur **ID** est l'identificateur que vous utilisez dans l'API {{site.data.keyword.keymanagementserviceshort}}.

## Gestion de vos clés
{: #managekey }

Pour afficher vos clés une fois que vous les avez générées et saisies, suivez les étapes indiquées sous [Ajout d'une clé](index.html#addkey). Vous êtes redirigé vers la fenêtre **Clés**. Vos clés s'affichent selon leur ordre de création, la plus récente apparaissant en haut de la liste.
<table>
      <tr>
        <th>Colonne</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Nom</td>
        <td>Alias affecté à votre clé et lisible par les utilisateurs.</td>
      </tr>
      <tr>
        <td>ID</td>
        <td>ID de clé unique affecté à votre clé par {{site.data.keyword.keymanagementserviceshort}}.</td>
      </tr>
      <tr>
        <td>Statut</td>
        <td>Un des états du National Institute of Standards and Technology (NIST) pour la clé : Pré-activation, Actif, Désactivé et Détruit.<td>
      </tr>
      <tr>
        <td>Créée</td>
        <td>Date et heure auxquelles la clé a été créée.</td>
      </tr>
      <tr>
        <td>Type</td>
        <td>La valeur par défaut est une clé standard.</td>
      </tr>
      <caption style="caption-side:bottom;">Tableau 3. Description de la fenêtre Clés</caption>
    </table>

### Etapes suivantes

Vous pouvez désormais utiliser vos clés pour coder vos applications et services.

- Pour consulter un exemple de la manière dont le magasin de clés dans {{site.data.keyword.keymanagementserviceshort}} peut être utilisé pour chiffrer et déchiffrer des données, reportez-vous à l'[exemple d'application dans Github ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.
- Pour plus d'informations sur la gestion de vos clés par voie de programmation, reportez-vous à la [documentation de référence de l'API {{site.data.keyword.keymanagementserviceshort}}](https://console.ng.bluemix.net/apidocs/639) pour consulter des exemples de code.

### Liens connexes

- [API REST {{site.data.keyword.keymanagementserviceshort}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.ng.bluemix.net/apidocs/639){: new_window}
- [API REST admin de {{site.data.keyword.keymanagementserviceshort}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs-admin-keyprotect.ng.bluemix.net/){: new_window}
- [Offre {{site.data.keyword.cloud_notm}} HSM ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.softlayer.com/ibm-cloud-hsm){: new_window}
- [{{site.data.keyword.keymanagementservicelong_notm}} Accord sur les niveaux de service ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www-03.ibm.com/software/sla/sladb.nsf/sla/bm-7603-01){: new_window}
