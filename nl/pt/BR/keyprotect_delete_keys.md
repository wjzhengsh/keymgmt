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

# Excluindo chaves

É possível usar o {{site.data.keyword.keymanagementservicefull}} para excluir uma chave de criptografia e seus conteúdos, se você é um administrador para o espaço do {{site.data.keyword.Bluemix_notm}} ou instância de serviço {{site.data.keyword.keymanagementserviceshort}}.
{: shortdesc}

**Importante**: ao excluir uma chave, você fragmenta permanentemente seus conteúdos e dados associados. A ação não pode ser invertida. A destruição de recursos não é recomendada para ambientes de produção, mas pode ser útil para ambientes temporários, como de teste ou QA.

## Excluindo chaves com a GUI
{: #gui}

Se você preferir excluir seus recursos de chave usando uma interface gráfica, será possível usar a GUI do {{site.data.keyword.keymanagementserviceshort}}.

[Depois de criar ou importar suas chaves existentes para o serviço](/docs/services/keymgmt/keyprotect_create_keys.html), conclua as etapas a seguir para excluir uma chave:

1. [Efetue login no console do {{site.data.keyword.Bluemix_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.bluemix.net/).
2. No painel do {{site.data.keyword.Bluemix_notm}}, selecione sua instância provisionada do {{site.data.keyword.keymanagementserviceshort}}.
3. Navegue para a área de janela **Gerenciar** para procurar as chaves em seu serviço.
4. Clique no ícone ⋮ para abrir uma lista de opções para a chave que você gostaria de excluir.
5. No menu de opções, clique em **Excluir chave** e confirme a exclusão da chave na próxima tela.

## Excluindo chaves com a API
{: #api}

Para excluir uma chave e seus conteúdos, faça uma chamada `DELETE` para o terminal a seguir:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID>
```

1. [Recupere seu token de autorização, GUID da organização e GUID do espaço para trabalhar com chaves no serviço.](/docs/services/keymgmt/keyprotect_authentication.html)

2. Recupere o ID da chave que você gostaria de excluir.

    É possível recuperar o ID para uma chave especificada fazendo uma chamada `GET /v2/keys` ou visualizando suas chaves no painel do {{site.data.keyword.keymanagementserviceshort}}.

3. Execute o comando cURL a seguir para excluir permanentemente a chave e seus conteúdos.

    ```cURL
    curl -X DELETE \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID> \
      -H 'authorization: Bearer <OAuth_token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
      -H 'prefer: <return_preference>'
    ```
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
      <tr>
        <td><em>key_ID</em></td>
        <td>O identificador exclusivo para a chave que você gostaria de excluir.</td>
      </tr>
      <tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p>Um cabeçalho que altera o comportamento do servidor para as operações <code>POST</code> e <code>DELETE</code>.</p><p>Se configurado como <code>return=minimal</code>, o serviço retornará somente os metadados de chave, como o nome da chave e o valor <code>id</code>, no corpo da entidade de resposta. Se configurado como <code>return=representation</code>, o serviço retornará o material de chave e os metadados de chave.</p></td>
      </tr>
      <caption style="caption-side:bottom;">Tabela 1. Descreve as variáveis necessárias para excluir chaves por meio da API do {{site.data.keyword.keymanagementserviceshort}}.</caption>
    </table>

    Os detalhes da solicitação `DELETE` são retornados no corpo da entidade de resposta.
