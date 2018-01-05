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

# Désencapsulage de clés
{: #unwrapping-keys}

Si vous êtes un utilisateur privilégié, vous pouvez désencapsuler une clé DEK pour accéder à son contenu via l'API {{site.data.keyword.keymanagementservicefull}}. La procédure de désencapsulage déchiffre le contenu d'une clé DEK et vérifie l'intégrité de son contenu en renvoyant le matériel de la clé d'origine au service de données {{site.data.keyword.cloud_notm}}.
{: shortdesc}

Pour découvrir comment l'encapsulage de clés peut vous aider à contrôler la sécurité des données au repos dans le cloud, reportez-vous à la rubrique [Chiffrement d'enveloppe](/docs/services/keymgmt/keyprotect_envelope.html).

## Désencapsulage de clés à l'aide de l'API
{: #api}

[Après avoir soumis un appel d'encapsulage au service](/docs/services/keymgmt/keyprotect_wrap_keys.html), vous pouvez désencapsuler une clé DEK donnée pour accéder à son contenu en soumettant un appel `POST` au noeud final suivant :

```
https://keyprotect.us-south.bluemix.net/api/v2/keys<key_id>?action=unwrap
```
{: codeblock}

1. [Extrayez vos données d'authentification et de service afin d'utiliser les clés dans le service.](/docs/services/keymgmt/keyprotect_authentication.html)

2. Copiez l'ID de la clé racine que vous avez utilisée pour exécuter la demande initiale en boucle.

    Vous pouvez extraire l'ID d'une clé en soumettant une demande `GET /v2/keys/` ou en affichant vos clés dans l'interface graphique {{site.data.keyword.keymanagementserviceshort}}.

3. Copiez la valeur `ciphertext` renvoyée lors de la demande d'encapsulage initiale.

4. Exécutez la commande cURL suivante pour déchiffrer et authentifier le matériel relatif à la clé :

    ```cURL
    curl -X POST \
      'https://keyprotect.us-south.bluemix.net/api/v2/keys<key_ID>?action=unwrap' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
      "ciphertext": "<encrypted_data_key>",
      "aad": ["<additional_data>", "<additional_data>"]
    }'
    ```
    {: codeblock}

    Pour utiliser les clés dans une organisation et un espace Cloud Foundry spécifiques de votre compte, remplacez `Bluemix-Instance` par les en-têtes `Bluemix-org` et `Bluemix-space` appropriés. [Pour obtenir des exemples de code, voir la documentation de référence de l'API {{site.data.keyword.keymanagementserviceshort}} ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
    {: tip}

    Remplacez les variables dans l'exemple de demande en fonction du tableau suivant :
    <table>
      <tr>
        <th>Variable</th>
        <th>Description</th>
      </tr>
      <tr>
        <td><em>key_ID</em></td>
        <td>ID unique de la clé racine que vous souhaitez utiliser pour l'encapsulage. Pour que la demande de désencapsulage aboutisse, indiquez la même clé racine que celle utilisée lors de la demande d'encapsulage initiale.</td>
      </tr>
      <tr>
        <td><em>IAM_token</em></td>
        <td>Votre jeton d'autorisation. Incluez l'ensemble du contenu du jeton <code>IAM</code>, y compris la valeur Bearer, dans la demande cURL.</td>
      </tr>
       <tr>
        <td><em>instance_ID</em></td>
        <td>Identificateur unique affecté à votre instance de service {{site.data.keyword.keymanagementserviceshort}}. </td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>Facultatif: identificateur unique qui est utilisé pour suivre et corréler des transactions.</td>
      </tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p>En-tête qui modifie le comportement du serveur pour les opérations <code>POST</code> et <code>DELETE</code>.</p><p>Lorsque vous affectez la valeur <code>return=minimal</code> à la variable <em>return_preference</em>, le service renvoie uniquement les métadonnées de la clé, comme le nom et l'ID de la clé, dans la section entity-body de la réponse. Si la variable a pour valeur <code>return=representation</code>, le service renvoie à la fois le matériel relatif à la clé et ses métadonnées.</p></td>
      </tr>
      <tr>
        <td><em>additional_data</em></td>
        <td>Facultatif : Données d'authentification supplémentaires (AAD) utilisées pour sécuriser davantage la clé. Chaque chaîne peut inclure jusqu'à 255 caractères. <br></br>Important : Si vous indiquez des données d'authentification supplémentaires lorsque vous soumettez un appel d'encapsulage au service, vous devez indiquer les mêmes données lors de l'appel de désencapsulage. </td>
      </tr>
      <tr>
        <td><em>encrypted_data_key</em></td>
        <td>Valeur <code>ciphertext</code> renvoyée lors d'une opération d'encapsulage.</td>
      </tr>
      <caption style="caption-side:bottom;">Tableau 1. Décrit les variables requises pour désencapsuler les clés dans {{site.data.keyword.keymanagementserviceshort}}.</caption>
    </table>

    Le matériel relatif à la clé d'origine est renvoyé dans la section entity-body de la réponse. L'objet JSON suivant présente un exemple de valeur renvoyée.

    ```
    {
      "plaintext": "s~Rz@kN9Fzv\\/hP*r3LY-?O@!!qdtj:L"
    }
    ```
    {:screen}
