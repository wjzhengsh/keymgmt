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

# Encapsulage de clés
{: #wrapping-keys}

Si vous êtes un utilisateur privilégié, vous pouvez gérer et protéger vos clés de chiffrement avec une clé racine à l'aide de l'API {{site.data.keyword.keymanagementservicelong}}.
{: shortdesc}

Lorsque vous encapsulez une clé DEK (Data Encryption Key) avec une clé racine, {{site.data.keyword.keymanagementserviceshort}} associe la puissance de plusieurs algorithmes pour protéger la confidentialité et l'intégrité des données chiffrées.  

Pour découvrir comment l'encapsulage de clés peut vous aider à contrôler la sécurité des données au repos dans le cloud, reportez-vous à la rubrique [Chiffrement d'enveloppe](/docs/services/keymgmt/keyprotect_envelope.html).

## Encapsulage de clés à l'aide de l'API
{: #api}

Vous pouvez protéger la clé DEK indiquée avec une clé racine que vous gérez dans {{site.data.keyword.keymanagementserviceshort}}.

**Important :** Lorsque vous indiquez une clé racine pour l'encapsulage, vérifiez qu'il s'agit d'une clé racine de 256, 384 ou 512 bits pour que l'opération aboutisse. Si vous créez une clé racine dans le service, {{site.data.keyword.keymanagementserviceshort}} génère à partir de son module HSM une clé 256 bits prise en charge par l'algorithme AES-GCM.

[Après avoir désigné une clé racine dans le service](/docs/services/keymgmt/keyprotect_create_keys.html), vous pouvez encapsuler une clé DEK avec un chiffrement avancé en soumettant un appel `POST` au noeud final suivant :

```
https://keyprotect.us-south.bluemix.net/api/v2/keys<key_ID>?action=wrap
```
{: codeblock}

1. [Extrayez vos données d'authentification et de service afin d'utiliser les clés dans le service.](/docs/services/keymgmt/keyprotect_authentication.html)

2. Copiez les éléments de la clé DEK que vous souhaitez gérer et protéger.

    Si vous avez des privilèges d'administrateur et d'éditeur pour l'instance de service {{site.data.keyword.keymanagementserviceshort}}, [vous pouvez extraire le matériel relatif à la clé en soumettant une demande `GET /v2/keys/<key_ID>`](/docs/services/keymgmt/keyprotect_view_keys.md#retrieve_key_api).

3. Copiez l'ID de la clé racine que vous souhaitez utiliser pour l'encapsulage.

4. Exécutez la commande cURL suivante pour protéger la clé avec une opération d'encapsulage :

    ```cURL
    curl -X POST \
      'https://keyprotect.us-south.bluemix.net/api/v2/keys<key_ID>?action=wrap' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
      "plaintext": "<data_key>",
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
        <td>ID unique de la clé racine que vous souhaitez utiliser pour l'encapsulage. Pour que l'appel d'encapsulage aboutisse, la clé racine doit être une clé de 256, 384 ou 512 bits.</td>
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
        <td><em>data_key</em></td>
        <td>Facultatif : Matériel relatif à la clé DEK que vous souhaitez gérer et protéger. La valeur <code>plaintext</code> doit être codée en base64. Pour générer une clé DEK, omettez l'attribut <code>plaintext</code>. Le service génère un texte brut aléatoire (32 octets) et l'encapsule.</td>
      </tr>
      <tr>
        <td><em>additional_data</em></td>
        <td>Facultatif : Données d'authentification supplémentaires (AAD) utilisées pour renforcer la sécurité de la clé. Chaque chaîne peut inclure jusqu'à 255 caractères. Si vous indiquez des données d'authentification supplémentaires lorsque vous soumettez un appel d'encapsulage au service, vous devez indiquer les mêmes données d'authentification supplémentaires lors de l'appel de désencapsulage ultérieur.</td>
      </tr>
      <caption style="caption-side:bottom;">Tableau 1. Description des variables nécessaires pour encapsuler une clé spécifique dans {{site.data.keyword.keymanagementserviceshort}}.</caption>
    </table>

    La clé encapsulée qui contient le matériel relatif à la clé codée en base64 est renvoyée dans la section entity-body de la réponse. L'objet JSON suivant présente un exemple de valeur renvoyée.

    ```
    {
      "plaintext": "s~Rz@kN9Fzv\\/hP*r3LY-?O@!!qdtj:L",
      "ciphertext": "eyJjaXBoZXJ0ZXh0Ijoic3VLSDNRcmdEZjdOZUw4Rkc4L2FKYjFPTWcyd3A2eDFvZlA4MEc0Z1B2RmNrV2g3cUlidHphYXU0eHpKWWoxZyIsImhhc2giOiJiMmUyODdkZDBhZTAwZGZlY2Q3OGJmMDUxYmNmZGEyNWJkNGUzMjBkYjBhN2FjNzVhMWYzZmNkMDZlMjAzZWYxNWM5MTY4N2JhODg2ZWRjZGE2YWVlMzFjYzk2MjNkNjA5YTRkZWNkN2E5Y2U3ZDc5ZTRhZGY1MWUyNWFhYWM5MjhhNzg3NmZjYjM2NDFjNTQzMTZjMjMwOGY2MThlZGM2OTE3MjAyYjA5YTdjMjA2YzkxNTBhOTk1NmUxYzcxMTZhYjZmNmQyYTQ4MzZiZTM0NTk0Y2IwNzJmY2RmYTk2ZSJ9"
      "aad": ["data1", "data2"]
    }
    ```
    {:screen}
