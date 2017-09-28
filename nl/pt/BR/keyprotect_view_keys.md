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

# Visualizando chaves

É possível visualizar os conteúdos de suas chaves de criptografia com o {{site.data.keyword.keymanagementservicefull}}.
{: shortdesc}

## Visualizando chaves com a GUI
{: #gui}

Para procurar as chaves em seu serviço com a GUI do {{site.data.keyword.keymanagementserviceshort}}, veja [Introdução ao {{site.data.keyword.keymanagementserviceshort}}](/docs/services/keymgmt/index.html#managekey).

## Visualizando chaves com a API
{: #api}

É possível recuperar os conteúdos de suas chaves usando a API do {{site.data.keyword.keymanagementserviceshort}}.

### Etapa 1: recuperar uma coleção de chaves
{: #retrieve_keys_api}

Para uma visualização de alto nível, é possível procurar chaves que são gerenciadas em seu espaço fazendo uma chamada `GET` para o terminal a seguir:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys
```
{: codeblock}

1. [Recupere seu token de autorização, GUID da organização e GUID do espaço para trabalhar com chaves no serviço.](/docs/services/keymgmt/keyprotect_authentication.html)
2. Execute o comando cURL a seguir para visualizar características gerais sobre suas chaves.

    ```cURL
    curl -X GET \
    https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <OAuth_token>' \
    -H 'bluemix-org: <organization_GUID>' \
    -H 'bluemix-space: <space_GUID>' \
    ```
    {: codeblock}

    Substitua as variáveis na solicitação de exemplo de acordo com a tabela a seguir.
    <table>
      <tr>
        <th>Variável</th>
        <th>Descrição</th>
      </tr>
      <tr>
        <td><em>OAuth_token</em></td>
        <td>Seu token de autorização. Inclua o conteúdo integral do token, incluindo o valor do portador, na solicitação cURL.</td>
      </tr>
      <tr>
        <td><em>space_GUID</em></td>
        <td>O identificador exclusivo que é designado ao seu espaço do {{site.data.keyword.Bluemix_notm}}.</td>
      </tr>
      <tr>
        <td><em>organization_GUID</em></td>
        <td>O identificador exclusivo que é designado à sua organização do {{site.data.keyword.Bluemix_notm}}.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabela 1. Descreve as variáveis necessárias para visualizar chaves por meio da API do {{site.data.keyword.keymanagementserviceshort}}.</caption>
    </table>

    Uma solicitação bem-sucedida retorna uma coleção de chaves disponíveis em seu espaço do {{site.data.keyword.Bluemix_notm}}.

    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.kms.key+json",
        "collectionTotal": 2
      },
    "resources": [
      {
          "id": "Key ID 1",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Key alias",
          "description": "Key description",
          "state": 1,
          "algorithmType": "AES",
          "createdBy": "v4 UUID of the user who creates the key",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "Key length",
            "mode": "GCM"
          }
        },
        {
          "id": "Key ID 2",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Key alias",
          "description": "Key description",
          "state": 1,
          "algorithmType": "AES",
          "createdBy": "v4 UUID of the user who creates the key",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "Key length",
            "mode": "GCM"
          }
        }
      ]
    }
    ```
    {:screen}

### Etapa 2: recuperar uma chave por ID
{: #retrieve_key_api}

Para visualizar informações detalhadas sobre uma chave específica, é possível fazer uma chamada `GET` subsequente para o terminal a seguir:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID>
```
{: codeblock}

1. [Recupere seu token de autorização, GUID da organização e GUID do espaço para trabalhar com chaves no serviço.](/docs/services/keymgmt/keyprotect_authentication.html)
2. Recupere o ID da chave que você gostaria de acessar ou gerenciar.

    O valor do ID é usado para acessar informações detalhadas sobre a chave, como o próprio material da chave. É possível recuperar o ID para uma chave especificada fazendo uma solicitação `GET v2/keys` ou acessando a GUI do {{site.data.keyword.keymanagementserviceshort}}.

3. Execute o comando cURL a seguir para obter detalhes sobre a chave e o material da chave.

    ```cURL
    curl -X GET \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID> \
      -H 'accept: application/vnd.ibm.kms.secret+json' \
      -H 'authorization: Bearer <OAuth_token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

    Substitua as variáveis na solicitação de exemplo de acordo com a tabela a seguir.


    <table>
      <tr>
        <th>Variável</th>
        <th>Descrição</th>
      </tr>
      <tr>
        <td><em>OAuth_token</em></td>
        <td>Seu token de autorização. Inclua o conteúdo integral do token, incluindo o valor do portador, na solicitação cURL.</td>
      </tr>
      <tr>
        <td><em>organization_GUID</em></td>
        <td>O identificador exclusivo que é designado à sua organização do {{site.data.keyword.Bluemix_notm}}.</td>
      </tr>
      <tr>
        <td><em>space_GUID</em></td>
        <td>O identificador exclusivo que é designado ao seu espaço do {{site.data.keyword.Bluemix_notm}}.</td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>Opcional: o identificador exclusivo que é usado para rastrear e correlacionar transações.</td>
      </tr>
      <tr>
        <td><em>key_ID</em></td>
        <td>O identificador para a chave que você recuperou na [etapa 1](#retrieve_keys_api).</td>
      </tr>
      <caption style="caption-side:bottom;">Tabela 2. Descreve as variáveis necessárias para visualizar uma chave especificada por meio da API do {{site.data.keyword.keymanagementserviceshort}}.</caption>
    </table>

    Uma resposta bem-sucedida retorna detalhes sobre a chave e o material da chave. O objeto JSON a seguir mostra um valor retornado de exemplo.

    ```
    {
        "metadata": {
            "collectionTotal": 1,
            "collectionType": "application/vnd.ibm.kms.key+json"
        },
    "resources": [
      {
                "createdBy": "...",
                "creationDate": "...",
                "id": "...",
                "name": "...",
                "payload": "...",
                "state": 1,
                "type": "application/vnd.ibm.kms.key+json"
            }
        ]
    }
    ```
    {:screen}

    Para obter uma descrição detalhada dos parâmetros disponíveis, veja o {{site.data.keyword.keymanagementserviceshort}} [documento de referência da API de REST ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
