---

copyright:
  years: 2017
lastupdated: "2017-09-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Gestion de l'accès utilisateur avec Identity and Access Management
{: #managing-access-iam}

{{site.data.keyword.keymanagementservicefull}} prend en charge un système de contrôle d'accès centralisé, régi par {{site.data.keyword.Bluemix_notm}} Identity and Access Management, afin de vous aider à gérer les utilisateurs et les accès pour vos clés de chiffrement.
{: shortdesc}

Il est recommandé d'accorder les droits d'accès lorsque vous invitez de nouveaux utilisateurs dans votre compte ou service. Prenons par exemple les instructions suivantes : 

- **Autorisez l'accès utilisateur aux ressources de votre compte en affectant des rôles IAM.**
    Au lieu de partager vos données d'identification administrateur, créez de nouvelles règles pour les utilisateurs qui ont besoin d'accéder aux clés de chiffrement dans votre compte. Si vous êtes administrateur de votre compte, une règle d'administration vous est automatiquement affectée, qui vous donne accès à toutes les ressources situées sous le compte.
- **Accordez des rôles et des droits à la portée la plus restreinte possible.**
    Par exemple, si un utilisateur n'a besoin que d'accéder à une vue de haut niveau des clés dans un espace donné, accordez le rôle _Afficheur_ à l'utilisateur pour cet espace.
- **Effectuez un audit régulier des utilisateurs autorisés à gérer le contrôle d'accès et à supprimer des ressources de clé.**
    N'oubliez pas que l'affectation du rôle _Administrateur_ à un utilisateur lui donne le droit de modifier les règles de service d'autres utilisateurs, ainsi que de détruire des ressources.

## Rôles et droits
{: #roles}

{{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) permet de définir des règles qui déterminent la portée de l'accès pour les membres de votre équipe.

Pour simplifier l'accès, {{site.data.keyword.keymanagementserviceshort}} s'aligne sur les rôles IAM, afin que chaque utilisateur dispose d'une vue différente du service, selon le rôle qui lui est affecté. Si vous êtes l'administrateur de sécurité de votre service, vous pouvez affecter des rôles IAM qui correspondent aux droits {{site.data.keyword.keymanagementserviceshort}} spécifiques que vous voulez accorder aux membres de votre équipe.

Le tableau suivant montre la façon dont les rôles d'identité et d'accès sont mappés sur les droits {{site.data.keyword.keymanagementserviceshort}} :
<table>
  <tr>
    <th>Rôle</th>
    <th>Description</th>
    <th>Actions</th>
  </tr>
  <tr>
    <td>Afficheur</td>
    <td>Un afficheur peut accéder à une vue de haut niveau des clés. Il ne peut pas accéder aux détails d'une clé, ni les modifier.</td>
    <td>
      <ul>
        <li>Affichage de clés</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Editeur</td>
    <td>Un éditeur peut créer et modifier des clés, et afficher les détails d'une clé.</td>
    <td>
      <ul>
        <li>Création de clés</li>
        <li>Affichage de clés</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Administrateur</td>
    <td>Un administrateur peut effectuer toutes les actions qu'un afficheur et qu'un éditeur peuvent exécuter, notamment supprimer des clés, inviter de nouveaux utilisateurs et gérer le contrôle d'accès.</td>
    <td>
      <ul>
        <li>Création de clés</li>
        <li>Affichage de clés</li>
        <li>Suppression de clés</li>
        <li>Gestion du contrôle d'accès</li>
      </ul>
    </td>
  </tr>
  <caption style="caption-side:bottom;">Tableau 1. Mappage de rôles d'identité et d'accès sur les droits {{site.data.keyword.keymanagementserviceshort}}.</caption>
</table>

**Remarque** : les rôles utilisateur IAM fournissent un accès au niveau du service ou de l'instance de service. Les [rôles Cloud Foundry](/docs/iam/users_roles.html#cfroles) sont distincts et définissent l'accès au niveau de l'organisation ou de l'espace.

Pour en savoir plus sur {{site.data.keyword.Bluemix_notm}} Identity and Access Management, consultez la section [Rôles et droits utilisateur](/docs/iam/users_roles.html#iamusermanpol).

### Etapes suivantes

Les propriétaires de compte et les administrateurs peuvent inviter des utilisateurs et définir des règles de service qui correspondent aux actions {{site.data.keyword.keymanagementserviceshort}} que les utilisateurs peuvent exécuter.

- Pour plus d'informations sur l'affectation de rôles utilisateur dans l'interface utilisateur {{site.data.keyword.Bluemix_notm}}, voir [Règles d'identité et d'accès au service](/docs/iam/iamusermanage.html#iammanidaccser).
- Pour en savoir plus sur l'affectation de droits avancés pour accéder à des clés de chiffrement spécifiques, voir [Gestion de l'accès à des clés avec l'API](/docs/services/keymgmt/keyprotect_manage_access_api.html).
