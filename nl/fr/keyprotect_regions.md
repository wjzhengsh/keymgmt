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

# Régions et emplacements
{: #regions-and-locations}

Vous pouvez connecter vos applications au service {{site.data.keyword.keymanagementservicelong_notm}} en indiquant un noeud final de service régional.
{: shortdesc}

## Régions disponibles
{: #regions}

{{site.data.keyword.keymanagementserviceshort}} est disponible dans les régions suivantes :

- Sud des États-Unis
- Royaume Uni  

## Noeuds finaux de service
{: #endpoints}

Si vous gérez vos ressources {{site.data.keyword.keymanagementserviceshort}} via un programme, reportez-vous au tableau suivant pour déterminer les noeuds finaux d'API à utiliser lorsque vous vous connectez à l'[API {{site.data.keyword.keymanagementserviceshort}}](https://console.ng.bluemix.net/apidocs/639): 

<table>
    <tr>
        <th>Région</th>
        <th>Noeud final d'API</th>
    </tr>
    <tr>
        <td>Sud des Etats-Unis</td>
        <td>
            <code>https://keyprotect.us-south.bluemix.net</code>
        </td>
    </tr>
    <tr>
        <td>Royaume-Uni</td>
        <td>
            <code>https://keyprotect.eu-gb.bluemix.net</code>
        </td>
    </tr>
    <caption style="caption-side:bottom;">Tableau 2. Noeuds finaux disponibles pour l'API {{site.data.keyword.keymanagementserviceshort}}</caption>
</table>

**Remarque :** Pour les instances de service {{site.data.keyword.keymanagementserviceshort}} figurant dans une organisation ou un espace Cloud Foundry, utilisez le noeud final existant `https://ibm-key-protect.edge.bluemix.net` pour interagir avec l'API {{site.data.keyword.keymanagementserviceshort}}.

Pour plus d'informations sur l'authentification auprès de {{site.data.keyword.keymanagementserviceshort}}, voir la rubrique décrivant l'[accès à l'API](/docs/services/keymgmt/keyprotect_authentication.html).
