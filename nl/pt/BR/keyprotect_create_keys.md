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

# Criando chaves

É possível gerenciar o ciclo de vida de suas chaves usando o {{site.data.keyword.keymanagementservicefull}}.
{: shortdesc}

Uma boa prática é gerenciar suas chaves com segurança conforme você desenvolve seu código. Por exemplo, pense sobre as diretrizes a seguir, juntamente com outras práticas de codificação segura.

- Considere as implicações de segurança ao integrar chaves em seu código.
- Crie chaves somente para acesso programático para seus apps e recursos. Não crie chaves quando puder conceder [permissões de usuário ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.bluemix.net/docs/admin/patterns.html#userroles){: new_window} mais simples.
- Gire as chaves e remova as chaves não utilizadas.
- Use autenticação multifatorial para operações sensitivas.
- Isole aplicativos tendo chaves separadas para cada aplicativo.
- Considere trabalhar com a API programática quando transferir informações altamente confidenciais.

Se você desejar tentar o serviço antes de incluir suas próprias chaves, verifique o [app de amostra ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}

## Criando chaves com a GUI
{: #gui}

Para incluir chaves em seu serviço com a GUI do {{site.data.keyword.keymanagementserviceshort}}, veja [Introdução ao {{site.data.keyword.keymanagementserviceshort}}](/docs/services/keymgmt/index.html#addkey).

## Criando chaves com a API
{: #api}

É possível usar a API do {{site.data.keyword.keymanagementserviceshort}} para assegurar programaticamente as chaves existentes ou gerar novas chaves.

Crie chaves ou importe as chaves existentes fazendo uma chamada `POST` para o terminal a seguir:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys
```
{: codeblock}

1. [Recupere seu token de autorização, GUID da organização e GUID do espaço para trabalhar com chaves no serviço.](/docs/services/keymgmt/keyprotect_authentication.html).

2. Chame a [{{site.data.keyword.keymanagementserviceshort}}API](https://console.ng.bluemix.net/apidocs/639) com o comando cURL a seguir.

    ```cURL
    curl -X POST \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
      -H 'authorization: Bearer <OAuth_token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
      -H 'content-type: application/vnd.ibm.kms.key+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
     "metadata": {
       "collectionType": "application/vnd.ibm.kms.key+json",
       "collectionTotal": 1
     },
     "resources": [
       {
       "type": "application/vnd.ibm.kms.key+json",
       "name": "<key_alias>",
       "description": "<key_description>",
       "expirationDate": "<YYYY-MM-DDTHH:MM:SS.SSZ>",
       "payload": "<key_material>"
       }
     ]
    }'
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
        <td>O identificador exclusivo que é designado à sua organização do {{site.data.keyword.Bluemix_notm}}. </td>
      </tr>
      <tr>
        <td><em>space_GUID</em></td>
        <td>O identificador exclusivo que é designado ao seu espaço do {{site.data.keyword.Bluemix_notm}}.</td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>O identificador exclusivo que é usado para rastrear e correlacionar transações.</td>
      </tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p>Um cabeçalho que altera o comportamento do servidor para as operações <code>POST</code> e <code>DELETE</code>.</p><p>Se configurado como <code>return=minimal</code>, o serviço retornará somente os metadados de chave, como o nome da chave e o valor <code>id</code>, no corpo da entidade de resposta. Se configurado como <code>return=representation</code>, o serviço retornará o material de chave e os metadados de chave.</p></td>
      </tr>
      <tr>
        <td><em>key_alias</em></td>
        <td>Um nome legível para fácil identificação de sua chave.</td>
      </tr>
      <tr>
        <td><em>key_description</em></td>
        <td>Uma descrição estendida de sua chave.</td>
      </tr>
      <tr>
        <td><em>AAAA-MM-DD</em><br><em>HH:MM:SS.SS</em></td>
        <td>Opcional: a data e hora em que a chave expira no sistema, no formato RFC 3339. Se o atributo <code>expirationDate</code> for omitido, a chave não expirará. </td>
      </tr>
      <tr>
        <td><em>key_material</em></td>
        <td>O material da chave, como uma chave RSA, que você deseja armazenar no {{site.data.keyword.keymanagementserviceshort}}. Para gerar uma nova chave, omita o atributo <code>payload</code> e a variável <em>key_material</em>.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabela 1. Variáveis necessárias para a inclusão de chaves por meio da API do {{site.data.keyword.keymanagementserviceshort}}</caption>
    </table>

    Uma resposta bem-sucedida retorna o valor `id` para sua chave, juntamente com outros metadados. O `id` é um identificador exclusivo designado à sua chave e usado para chamadas subsequentes.

3. **Opcional:** verifique se a chave foi criada executando a chamada a seguir para obter as chaves em seu espaço do {{site.data.keyword.Bluemix_notm}}.

    ```cURL
    curl -X GET \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <OAuth-token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
    ```
    {: codeblock}

### O que vem a seguir

Agora é possível usar suas chaves para codificar seus apps e serviços.

- Para detalhes integrais de cada solicitação e resposta REST, verifique o {{site.data.keyword.keymanagementserviceshort}} [documento de referência da API de REST ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
