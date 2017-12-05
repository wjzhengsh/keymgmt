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

# Génération de données d'authentification
{: #authentication}

{{site.data.keyword.keymanagementservicefull}} fournit une méthode d'API REST qui peut être utilisée avec tout langage de programmation pour stocker, extraire et générer des clés.
{: shortdesc}

Pour utiliser l'API, vous devez générer vos données d'authentification et de service.

## Extraction de vos identificateurs globaux uniques d'organisation et d'espace
{: #retrieve_GUIDs}

Vous pouvez extraire les informations d'identification pour votre espace et votre organisation {{site.data.keyword.cloud_notm}} avec l'[interface de ligne de commande {{site.data.keyword.cloud_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.bluemix.net/docs/cli/reference/bluemix_cli/index.html#getting-started).

1. Connectez-vous à {{site.data.keyword.cloud_notm}} vie l'interface de ligne de commande {{site.data.keyword.cloud_notm}} (bx).

    ```
    bx login [--sso]
    ```
    {: codeblock}

    Le paramètre `--sso` est requis quand vous vous connectez avec un ID fédéré. Si cette option est utilisée, allez sur le lien répertorié dans la sortie d'interface de ligne de commande pour générer un code d'accès unique.

2. Sélectionnez l'organisation et l'espace {{site.data.keyword.cloud_notm}} qui contient votre instance de service {{site.data.keyword.keymanagementserviceshort}}.

    Notez les noms de votre organisation et de votre espace dans la sortie d'interface de ligne de commande. Vous pouvez aussi exécuter `bx target` pour afficher ces informations.

3. Extrayez les identificateurs globaux uniques de votre organisation et de votre espace {{site.data.keyword.cloud_notm}}.

    ```
    bx iam org [organization_name] --guid
    bx iam space [space_name] --guid
    ```
    {: codeblock}
    Remplacez _organization_name_ et _space_name_ par l'alias unique que vous avez affecté à votre organisation et à votre espace.

## Extraction de votre jeton d'autorisation
{: #retrieve_token}

Vous pouvez utiliser un jeton d'autorisation pour gérer vos clés à l'aide d'un programme via l'API {{site.data.keyword.keymanagementserviceshort}}.

**Remarque** : Pour activer le contrôle d'accès granulaire régi par {{site.data.keyword.iamshort}}, utilisez un jeton IAM lorsque vous passez des appels au service.

1. Dans l'interface de ligne de commande {{site.data.keyword.cloud_notm}}, sélectionnez l'organisation et l'espace contenant votre service {{site.data.keyword.keymanagementserviceshort}}.

2. Extrayez et affichez vos jetons d'autorisation.

    ```
    bx iam oauth-tokens
    ```
    {: codeblock}

    L'extrait d'exemple suivant montre la sortie de jeton {{site.data.keyword.cloud_notm}}. La variable _Bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7_ est un jeton d'accès exemple.

    ```
    IAM token: Bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7...
    UAA token: Bearer mjEyJhbGciOiJIUzI1Ni.chWyW1faWQiOiJJQkWs1...
    ```
    {: screen}

    Utilisez la valeur bearer `IAM` ou `UAA` pour gérer les clés à l'aide d'un programme dans votre service via l'API {{site.data.keyword.keymanagementserviceshort}}.

### Etapes suivantes

Consultez la [{{site.data.keyword.keymanagementserviceshort}}documentation de référence de l'API REST ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.ng.bluemix.net/apidocs/639){: new_window} pour commencer à gérer des clés dans votre espace.
