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

# Traitement des incidents

Vous trouverez ici les réponses aux questions fréquentes liées au
traitement des incidents concernant l'utilisation d'{{site.data.keyword.keymanagementservicefull}}.
{: shortdesc}

## Impossible de créer ou de supprimer des clés
{: #unabletomanagekeys}

Si vous ne parvenez pas à effectuer des actions {{site.data.keyword.keymanagementserviceshort}}, vérifiez que vous
disposez des autorisations appropriées.

### Symptômes

Quand vous accédez à l'interface utilisateur {{site.data.keyword.keymanagementserviceshort}}, vous ne pouvez pas afficher les options d'ajout ou de suppression de clés.

### Résolution du problème

Vérifiez auprès de votre administrateur qu'il vous a attribué le rôle adéquat dans l'espace applicable. Pour plus d'informations sur les rôles, voir [Rôles et droits](/docs/services/keymgmt/keyprotect_manage_access.html#roles).

## Conversion de la version bêta en version GA (disponibilité générale)
{: #ts_planconversion}

Les utilisateurs de la version bêta doivent changer le modèle de tarification standard pour continuer à utiliser le service {{site.data.keyword.keymanagementserviceshort}}.

### Symptômes

Si vous êtes un utilisateur de la version bêta, vous devez changer votre modèle de tarification pour le modèle de tarification différenciée afin de pouvoir continuer à stocker des clés dans {{site.data.keyword.keymanagementserviceshort}}.

### Résolution du problème

Le service {{site.data.keyword.keymanagementserviceshort}} propose deux modèles de tarification : un modèle léger et un modèle de tarification à tranches graduées. En tant qu'administrateur, vérifiez que le modèle à tranches graduées a été sélectionné. Si vous ne souhaitez pas migrer vers le modèle de tarification différenciée, assurez-vous que toutes les clés et instances de service sont supprimées avant qu'elles ne deviennent obsolètes. [Pour plus d'informations, voir l'annonce de disponibilité générale de {{site.data.keyword.keymanagementserviceshort}} ![icône Lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2016/12/dallas-key-protect-ga/){: new_window}.

Pour changer de modèle de tarification :

1. Accédez à l'interface utilisateur {{site.data.keyword.keymanagementserviceshort}} et sélectionnez l'onglet **Plans**.
2. Sélectionnez **Tarification différenciée**.
    La répartition du coût en clés actives utilisées par mois est présentée sous forme de tableau. Le modèle à tranches graduées calcule le tarif en fonction du nombre de clés actives par mois au niveau du compte.
3. Pour confirmer le changement de plan, cliquez sur **Sauvegarder**.

## Aide et support pour {{site.data.keyword.keymanagementserviceshort}}
{: #ts_gettinghelp}

Si vous rencontrez des problèmes ou des questions lors de l'utilisation d'{{site.data.keyword.keymanagementservicefull_notm}}, vous pouvez rechercher des informations ou poser des questions via un forum. Vous pouvez également ouvrir un ticket de demande de service.

Quand vous utilisez les forums pour poser une question, prenez soin d'étiqueter cette dernière de façon à ce qu'elle soit vue par les équipes de développement {{site.data.keyword.cloud_notm}}.

- En cas de questions d'ordre technique sur {{site.data.keyword.keymanagementserviceshort}}, postez votre question sur le forum [Stack Overflow ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://stackoverflow.com/search?q=key-protect+ibm-bluemix){: new_window} en lui adjoignant les balises "ibm-bluemix" et "key-protect".
- Pour des questions relatives au service et aux instructions de mise en route, utilisez le forum [IBM developerWorks dW Answers ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developer.ibm.com/answers/topics/key-protect/?smartspace=bluemix){: new_window} forum. Incluez les balises "bluemix" et "key-protect".

Pour plus d'informations sur l'utilisation des forums, voir la rubrique expliquant [comment obtenir de l'aide ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.bluemix.net/docs/support/index.html#getting-help){: new_window}.

Pour plus d'informations sur l'ouverture d'un ticket de demande de service {{site.data.keyword.IBM_notm}}, sur les niveaux de support disponibles ou les niveaux de gravité des tickets, voir la rubrique expliquant [comment contacter le support![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.bluemix.net/docs/support/index.html#contacting-support){: new_window}.
