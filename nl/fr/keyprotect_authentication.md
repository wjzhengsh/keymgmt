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

# Accès à l'API
{: #access-api}

{{site.data.keyword.keymanagementservicefull}} fournit une méthode d'API REST qui peut être utilisée avec n'importe quel langage de programmation pour stocker, extraire et générer des clés.
{: shortdesc}

Pour utiliser l'API, vous devez générer vos données d'authentification et de service. 

## Extraction d'un jeton d'accès
{: #retrieve_token}

Vous pouvez vous authentifier auprès de {{site.data.keyword.keymanagementserviceshort}} en extrayant un jeton d'accès de {{site.data.keyword.iamshort}}. Avec un [ID de service](/docs/iam/serviceid.html), vous pouvez utiliser l'API {{site.data.keyword.keymanagementserviceshort}} au nom du service ou de l'application au sein ou en dehors de l'environnement {{site.data.keyword.cloud_notm}} sans avoir à partager vos données d'identification utilisateur personnelles.  

Si vous souhaitez vous authentifier avec vos données d'identification utilisateur, vous pouvez extraire votre jeton en exécutant `bx iam oauth-tokens` dans l'interface de ligne de commande [{{site.data.keyword.cloud_notm}} (bx) ![icône de lien externe](../../icons/launch-glyph.svg "External link icon")](/docs/cloud-platform/cli/reference/bluemix_cli/get_started.html#getting-started){: new_window}.
{: tip}

Pour extraire un jeton d'accès, procédez comme suit :

1. Dans la console {{site.data.keyword.cloud_notm}}, accédez à  **Gérer** &gt; **Sécurité** &gt; **Identity and Access** &gt; **ID de service**. Suivez la procédure indiquée pour [créer un ID de service.](/docs/iam/serviceid.html#creating-a-service-id){: new_window}
2. Utilisez le menu **Actions** pour [définir une règle d'accès pour le nouvel ID de service.](/docs/iam/serviceidaccess.html#assigning-new-access){: new_window} 
    
Pour plus d'informations sur la gestion des accès pour les ressources {{site.data.keyword.keymanagementserviceshort}}, voir [Rôles et droits](/docs/services/keymgmt/keyprotect_manage_access.md#roles).
3. Utilisez la section **Clés d'API** pour [créer une clé d'API à associer à l'ID de service.](/docs/iam/serviceid_keys.html#creating-an-api-key-for-a-service-id){: new_window} Sauvegardez la clé d'API en la téléchargeant dans un emplacement sécurisé.
4. Appelez l'API {{site.data.keyword.iamshort}} pour extraire votre jeton d'accès.

    ```cURL
    curl -X POST \
      "https://iam.bluemix.net/oidc/token" \
      -H "Content-Type: application/x-www-form-urlencoded" \
      -H "Accept: application/json" \
      -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<your_API_key>" \
    ```
    {: codeblock}

    Dans la demande, remplacez `<API_key>` par la clé d'API que vous avez créée à l'étape 3. L'exemple partiel suivant présente la sortie du jeton :

    ```
    {
    "access_token": "eyJraWQiOiIyM...",
    "expiration": 1512161390,
    "expires_in": 3600,
    "refresh_token": "J1AzOrtC8yHVlcT...",
    "token_type": "Bearer"
    }
    ```
    {: screen}

    Utilisez l'ensemble de la valeur `access_token` avec le préfixe du type de jeton _Bearer_ pour gérer les clés de votre service à l'aide d'un programme via l'API {{site.data.keyword.keymanagementserviceshort}}. 

## Extraction de l'ID d'instance
{: #retrieve_instance_ID}

Vous pouvez extraire les informations d'identification de votre instance de service {{site.data.keyword.keymanagementserviceshort}} via l'interface de ligne de commande [{{site.data.keyword.cloud_notm}} (bx) ![icône Lien externe](../../icons/launch-glyph.svg "External link icon")](/docs/cloud-platform/cli/reference/bluemix_cli/get_started.html#getting-started){: new_window}. Utilisez un ID d'instance pour gérer vos clés de chiffrement au sein d'une instance {{site.data.keyword.keymanagementserviceshort}} spécifique dans votre compte.  

1. Connectez-vous à {{site.data.keyword.cloud_notm}} avec l'interface de ligne de commande {{site.data.keyword.cloud_notm}} (bx).

    ```sh
    bx login 
    ```
    {: pre}

    **Remarque :** Si la procédure de connexion échoue, exécutez la commande `bx login --sso` pour effectuer une nouvelle tentative. Le paramètre `--sso` est requis quand vous vous connectez avec un ID fédéré. Si cette option est utilisée, accédez au lien répertorié dans la sortie d'interface de ligne de commande pour générer un code d'accès unique.

2. Sélectionnez le compte qui inclut l'instance {{site.data.keyword.keymanagementserviceshort}} mise à disposition.

    Vous pouvez exécuter `bx resource service-instances` pour répertorier toutes les instances mises à disposition dans votre compte.

3. Extrayez le nom CRN (Cloud Resource Name) qui identifie de manière unique l'instance de service {{site.data.keyword.keymanagementserviceshort}}. 

    ```sh
    bx resource service-instance <instance_name> --id
    ```
    {: pre}

    Remplacez `<instance_name>` par l'alias unique que vous avez affecté à votre instance {{site.data.keyword.keymanagementserviceshort}}. L'exemple partiel suivant présente la sortie de l'interface de ligne de commande Bluemix. La valeur _7e8fc048-5606-4259-ad71-92397b0fa3f7_ est un exemple d'ID d'instance.

    ```
    crn:v1:bluemix:public:kms:us-south:a/7e8fc048-5606-4259-ad71-92397b0fa3f7
    ```
    {: screen}

## Mise en forme de la demande d'API
{: #form_api_request}

Lorsque vous soumettez un appel d'API au service, structurez votre demande d'API en fonction de la manière dont votre instance {{site.data.keyword.keymanagementserviceshort}} a été initialement mise à disposition. 

Pour générer une demande, associez un [noeud final de service régional](/docs/services/keymgmt/keyprotect_regions.html) aux données d'authentification appropriées. Par exemple, si  vous avez créé une instance de service pour la région `us-south`, utilisez le noeud final et les en-têtes API ci-dessous pour parcourir les clés du service :

```cURL
curl -X GET \
    https://keyprotect.us-south.bluemix.net/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <access_token>' \
    -H 'bluemix-instance: <instance_ID>' \
```
{: codeblock}

### Etapes suivantes

- Pour en savoir plus sur la gestion de vos clés à l'aide d'un programme, [reportez-vous à la documentation de référence de l'API {{site.data.keyword.keymanagementserviceshort}} afin d'obtenir des exemples de code ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
- Pour obtenir un exemple expliquant comment les clés stockées dans {{site.data.keyword.keymanagementserviceshort}} peuvent fonctionner pour chiffrer et déchiffrer des données, [reportez-vous à l'exemple d'application disponible dans GitHub ![icône Lien externe](../../icons/launch-glyph.svg "icône Lien externe")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.
