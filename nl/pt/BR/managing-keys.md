---

copyright:
  years: 2017
lastupdated: "2017-08-03"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Gerenciando chaves

É possível gerenciar o ciclo de vida de suas chaves usando o {{site.data.keyword.keymanagementservicelong}}
for {{site.data.keyword.Bluemix_short}}.
{: shortdesc}

Uma boa prática é gerenciar suas chaves com segurança conforme
você desenvolve seu código. Por exemplo, pense sobre os tipos de
diretrizes a seguir, junto com outras práticas de codificação seguras.

- Considere as implicações de segurança ao integrar chaves em seu código.
- Crie chaves somente para acesso programático para seus apps e recursos. Não crie chaves quando puder conceder [permissões de usuário ![Íconede link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.bluemix.net/docs/admin/patterns.html#userroles "Ícone de link externo"){: new_window} mais simples.

- Gire as chaves e remova as chaves não utilizadas.
- Use autenticação multifatorial para operações sensitivas.
- Isole aplicativos tendo chaves separadas para cada aplicativo.
- Considere trabalhar com a API programática quando transferir informações altamente confidenciais.

## Gerando credenciais de autenticação para a API do {{site.data.keyword.keymanagementserviceshort}}
{: #authentication_api}

O {{site.data.keyword.keymanagementservicelong_notm}} fornece uma API de REST que pode ser usada com qualquer
linguagem de programação para armazenar, recuperar e gerar chaves.

Para trabalhar com a API, é necessário gerar suas
credenciais de autenticação e de serviço.

1. Efetue login no {{site.data.keyword.Bluemix_notm}} por meio da CLI do Cloud
Foundry.

    ```
    cf login [a api.DomainName] [-sso]
    ```
    {: codeblock}

2. Selecione a organização e o espaço do {{site.data.keyword.Bluemix_notm}} que contém sua instância do serviço Key Protect.
    Observe os nomes de sua organização e o espaço na saída da CLI. Também é possível executar `cf
target` para visualizar essas informações.
3. Recupere a sua organização do {{site.data.keyword.Bluemix_notm}} e
GUIDs de espaço.

    ```
    cf org organization_name --guid
    cf space space_name --guid
    ```
    {: codeblock}

4. Solicite um token de acesso do {{site.data.keyword.Bluemix_notm}}.

    ```
    cf oauth-token
    ```
    {: codeblock}

    O exemplo truncado a seguir mostra a saída de token do {{site.data.keyword.Bluemix_notm}}. A variável _bearer
mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7_ é um token
de acesso de exemplo.

    ```
    bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7...
    ```
    {: screen}

O que fazer em seguida:

Consulte o {{site.data.keyword.keymanagementserviceshort}} [documento de referência da API de REST ![Ícone de linkexterno](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/apidocs/639 "Ícone de link externo"){: new_window} para iniciar o gerenciamento de chaves em seu espaço.



## Criando chaves com a API do {{site.data.keyword.keymanagementserviceshort}}
{: #codingapps}

É possível usar a API do {{site.data.keyword.keymanagementservicelong_notm}} para proteger chaves existentes ou para gerar novas chaves.

Crie novas chaves ou inclua chaves existentes criando uma chamada **POST** para o terminal a seguir:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/secrets
```
{: codeblock}

Se desejar experimentar o serviço antes de incluir suas próprias chaves, verifique o aplicativo de amostra do [ ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de linkexterno")](https://github.com/IBM-Bluemix/key-protect-helloworld-python "Ícone de linkexterno"){: new_window}.


1. [Recupere seu token de acesso, seu GUID da organização e seu GUID do espaço do {{site.data.keyword.Bluemix_notm}} para trabalhar com chaves no serviço](#authentication_api).

2. Chame a [{{site.data.keyword.keymanagementserviceshort}}API](https://console.ng.bluemix.net/apidocs/639) com o comando cURL a seguir.

  ```cURL
  curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: bluemix_access_token' --header 'Bluemix-Space: space_GUID' --header 'Bluemix-Org: organization_GUID' -d '{
    "metadata": {
      "collectionType": "application/vnd.ibm.kms.secret+json",
      "collectionTotal": 1
    },
    "resources": [
      {
      "type": "application/vnd.ibm.kms.secret+json",
      "name": "key_alias",
      "description": "key_description",
      "expirationDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
      "payload": "key_contents"
      }
    ]
  }' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets'
  ```
  {: codeblock}

  Substitua as variáveis na solicitação de exemplo de acordo com a tabela a seguir.
  <table>
    <tr>
      <th>Variável</th>
      <th>Descrição</th>
    </tr>
    <tr>
      <td><em>bluemix_access_token</em></td>
      <td>Seu token de autorização. Inclua o conteúdo integral do token, incluindo o valor do portador, na solicitação cURL.</td>
    </tr>
    <tr>
      <td><em>space_GUID</em></td>
      <td>O identificador para o seu espaço do {{site.data.keyword.Bluemix_notm}}.</td>
    </tr>
    <tr>
      <td><em>organization_GUID</em></td>
      <td>O identificador para sua organização do {{site.data.keyword.Bluemix_notm}}. </td>
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
      <td>Opcional: a data e hora em que a chave expira no sistema, no formato RFC3339. Se o atributo <code>expirationDate</code> for omitido, a
chave não expirará. </td>
    </tr>
    <tr>
      <td><em>key_contents</em></td>
      <td>O material da chave, como uma chave RSA, que você deseja armazenar no {{site.data.keyword.keymanagementserviceshort}}. Para gerar uma nova chave, omita o atributo payload e a variável key_contents.</td>
    </tr>
      <caption style="caption-side:bottom;">Tabela 1. Variáveis necessárias para a inclusão de chaves por meio da API do {{site.data.keyword.keymanagementserviceshort}}</caption>
  </table>

3. Verifique se a chave foi criada executando a chamada a seguir para obter as chaves em seu espaço do {{site.data.keyword.Bluemix_notm}}.

  ```cURL
  curl -X GET --header 'Accept: application/json' --header 'Authorization: bluemix_access_token' --header 'Bluemix-Space: space_GUID' --header 'Bluemix-Org: organization_GUID' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets'
  ```
  {: codeblock}

## Visualizando chaves com a API do {{site.data.keyword.keymanagementserviceshort}}
{: #viewingkeys_api}

Será possível visualizar o conteúdo de suas chaves por meio da API do {{site.data.keyword.keymanagementservicelong_notm}} se você for um desenvolvedor ou gerenciador de espaço do {{site.data.keyword.Bluemix_notm}}.

Para obter uma visualização de alto nível, é possível procurar
chaves que são gerenciadas em seu espaço por meio da UI do {{site.data.keyword.keymanagementserviceshort}}.

Visualize informações detalhadas sobre suas chaves fazendo uma chamada GET para o terminal a seguir:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/secrets/key_ID
```
{: codeblock}

1. Na UI do {{site.data.keyword.keymanagementserviceshort}}, em Serviços de segurança, é possível visualizar características gerais sobre suas chaves. É possível procurar as chaves clicando nos cabeçalhos das colunas classificáveis.
2. Copie o **ID** na linha da chave. O valor do ID é usado para acessar informações mais detalhadas
sobre a chave na API, tais como o próprio material da chave.
3. [Recupere seu token de acesso do {{site.data.keyword.Bluemix_notm}}, o GUID da organização e o GUID de espaço para trabalhar com chaves no serviço.](#authentication_api)
4. Execute o comando cURL a seguir para obter detalhes sobre a chave e o material da chave.

  ```cURL
  curl -X GET --header 'Accept: application/json' --header 'Authorization: bluemix_access_token' --header 'Bluemix-Space: space_GUID' --header 'Bluemix-Org: organization_GUID' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets/key_ID'
  ```
  {: codeblock}

  Substitua as variáveis na solicitação de exemplo de acordo com a tabela a seguir.
  <table>
    <tr>
      <th>Variável</th>
      <th>Descrição</th>
    </tr>
    <tr>
      <td><em>bluemix_access_token</em></td>
      <td>Seu token de autorização. Inclua o conteúdo integral do token, incluindo o valor do portador, na solicitação cURL.</td>
    </tr>
    <tr>
      <td><em>space_GUID</em></td>
      <td>O identificador gerado aleatoriamente que é designado ao seu espaço do
{{site.data.keyword.Bluemix_notm}}.</td>
    </tr>
    <tr>
      <td><em>organization_GUID</em></td>
      <td>O identificador gerado aleatoriamente que é designado à sua organização do {{site.data.keyword.Bluemix_notm}}.</td>
    </tr>
    <tr>
      <td><em>key_ID</em></td>
      <td>O identificador para a chave extraída na etapa [2](https://console.bluemix.net/docs/services/keymgmt/managing.html#viewingkeys_api__keyid).</td>
    </tr>
    <caption style="caption-side:bottom;">Tabela 2. Descreve as variáveis necessárias para visualizar chaves por meio da API do {{site.data.keyword.keymanagementserviceshort}}.</caption>
  </table>

  O material da chave é retornado no corpo da entidade da resposta. As chaves que são geradas pelos módulos de segurança de hardware (HSMs)
são codificadas em base 64.

## Auditando as chaves e o acesso
{: #viewkeyassignments}

O {{site.data.keyword.keymanagementservicelong_notm}} fornece um sistema centralizado para visualizar, gerenciar e auditar suas chaves de criptografia. Audite as suas chaves e as restrições de acesso às chaves para garantir
a segurança de seus recursos.

Audite a configuração de chaves com regularidade:

- Examine quando as chaves foram criadas e determine se é hora de girar a chave.
- [Monitore as chamadas API para o {{site.data.keyword.keymanagementserviceshort}} com o
{{site.data.keyword.cloudaccesstrailshort}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.bluemix.net/docs/services/AccessTrail/at_integration.html#at_integration_key_protect "Ícone de link externo"){: new_window}.
- Inspecione quais usuários têm acesso a chaves e se o nível de acesso é apropriado.

Para auditar usuários com acesso:

1. Como um gerenciador de espaço, acesse suas configurações de conta e selecione
**Gerenciar organizações**.
2. Abra o espaço que contém a instância de serviço do {{site.data.keyword.keymanagementserviceshort}}
para inspecionar quais usuários têm acesso.
3. Se for necessário incluir usuários, acesse **Convidar membros da equipe** e selecione as
funções do {{site.data.keyword.Bluemix_notm}} que correspondem às permissões
do {{site.data.keyword.keymanagementserviceshort}}
que você deseja conceder ao usuário:

  <table>
    <tr>
      <th>funções do {{site.data.keyword.Bluemix_notm}}</th>
      <th>Permissões do {{site.data.keyword.keymanagementserviceshort}}</th>
    </tr>
    <tr>
      <td>Gerenciador de espaço</td>
      <td>Um gerenciador de espaço pode criar, visualizar e excluir chaves.</td>
    </tr>
    <tr>
      <td>Desenvolvedor</td>
      <td>Um desenvolvedor pode criar chaves e visualizar detalhes de chave.</td>
    </tr>
    <tr>
      <td>Auditor</td>
      <td>Um auditor pode acessar uma visualização de chaves de alto nível. </td>
    </tr>
    <caption style="caption-side:bottom;">Tabela 3. Mapeamento de funções do {{site.data.keyword.Bluemix_notm}} para permissões do {{site.data.keyword.keymanagementserviceshort}}.</caption>
  </table>
