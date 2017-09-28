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

# Mise à disposition du service {{site.data.keyword.keymanagementserviceshort}}
{: #provision}

Vous pouvez créer une instance sécurisée d'{{site.data.keyword.keymanagementservicefull}} à l'aide de la console {{site.data.keyword.Bluemix_notm}} ou de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

## Mise à disposition à partir de la console {{site.data.keyword.Bluemix_notm}}
{: #gui}

Pour mettre à disposition une instance de {{site.data.keyword.keymanagementserviceshort}} à partir de la console {{site.data.keyword.Bluemix_notm}}, procédez comme suit. 

1. [Connectez-vous à votre compte {{site.data.keyword.Bluemix_notm}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/){: new_window}.
2. Cliquez sur **Catalogue** pour afficher la liste des services disponibles sur {{site.data.keyword.Bluemix_notm}}.
3. Sélectionnez la catégorie **Services**, puis cliquez sur la vignette **{{site.data.keyword.keymanagementserviceshort}}**.
5. Sélectionnez un plan de service, puis cliquez sur **Créer** pour mettre à disposition une instance de service {{site.data.keyword.keymanagementserviceshort}} dans l'espace et l'organisation {{site.data.keyword.Bluemix_notm}} auxquels vous êtes connecté.

## Mise à disposition à partir de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}
{: #cli}

Vous pouvez mettre à disposition une instance de {{site.data.keyword.keymanagementserviceshort}} à l'aide de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}. [Téléchargez et installez l'outil de ligne de commande sur votre système](https://clis.ng.bluemix.net/ui/home.html){: new_window} pour exécuter les étapes suivantes.

1. Connectez-vous à l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

    ```sh
    bx login [--sso]
    ```
    {: codeblock}
    **Remarque** : le paramètre `--sso` est requis quand vous vous connectez avec un ID fédéré. Si cette option est utilisée, allez sur le lien répertorié dans la sortie d'interface de ligne de commande pour générer un code d'accès unique.
2. Sélectionnez l'espace et l'organisation {{site.data.keyword.Bluemix_notm}} où vous souhaitez créer une instance de service {{site.data.keyword.keymanagementserviceshort}}.

    Vous pouvez également utiliser la commande suivante pour définir vos espace et organisation cible.

    ```sh
    bx target [-o organization_name] [-s space_name]
    ```
    {: codeblock}

3. Mettez à disposition une instance de {{site.data.keyword.keymanagementserviceshort}} dans ces région, organisation et espace.

    ```sh
    bx service create ibm_key_management TieredPricing [instance_name]
    ```
    {: codeblock}

    Remplacez _instance_name_ par un alias unique pour votre instance de service.

4. Vérifiez que l'instance de service a été créée.

    ```sh
    bx service list
    ```
    {: codeblock}


### Etapes suivantes

Vous pouvez désormais utiliser vos clés pour coder vos applications et services. 

- Pour consulter un exemple de la manière dont le magasin de clés dans {{site.data.keyword.keymanagementserviceshort}} peut être utilisé pour chiffrer et déchiffrer des données, reportez-vous à l'[exemple d'application dans GitHub ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.
- Pour en savoir plus sur la gestion de vos clés à l'aide d'un programme, [consultez la documentation de référence de l'API {{site.data.keyword.keymanagementserviceshort}} afin d'obtenir des exemples de code ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
