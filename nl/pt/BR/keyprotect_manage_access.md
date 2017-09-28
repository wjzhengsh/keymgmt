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

# Gerenciando o acesso de usuário com o Identity and Access Management
{: #managing-access-iam}

O {{site.data.keyword.keymanagementservicefull}} suporta um sistema de controle de acesso centralizado, governado pelo {{site.data.keyword.Bluemix_notm}} Identity and Access Management, para ajudá-lo a gerenciar os usuários e o acesso para suas chaves de criptografia.
{: shortdesc}

Uma boa prática é conceder permissões de acesso à medida que você convida novos usuários à sua conta ou serviço. Por exemplo, considere as diretrizes a seguir:

- **Ative o acesso de usuário aos recursos em sua conta designando funções do IAM.**
    Em vez de compartilhar suas credenciais de administrador, crie novas políticas para os usuários que precisam de acesso às chaves de criptografia em sua conta. Se você for o administrador para sua conta, será designado automaticamente a uma política de administrador com acesso a todos os recursos sob a conta.
- **Conceda funções e permissões no menor escopo necessário.**
    Por exemplo, se um usuário precisa acessar uma visualização de alto nível de chaves somente dentro de um espaço especificado, conceda a função de _Visualizador_ ao usuário para esse espaço.
- **Audite regularmente quem tem a capacidade para gerenciar o controle de acesso e excluir recursos de chave.**
    Lembre-se de que conceder uma função de _Administrador_ a um usuário significa que o usuário pode modificar políticas de serviço para outros usuários, além de destruir recursos.

## Funções e permissões
{: #roles}

Com o {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM), é possível configurar políticas que definem o escopo de acesso para membros de sua equipe.

Para simplificar o acesso, o {{site.data.keyword.keymanagementserviceshort}} é alinhado com as funções do IAM para que cada usuário tenha uma visualização diferente do serviço, de acordo com a função à qual o usuário é designado. Se você é um administrador de segurança para o seu serviço, é possível atribuir funções do IAM que correspondam às permissões específicas do {{site.data.keyword.keymanagementserviceshort}} que deseja conceder a membros de sua equipe.

A tabela a seguir mostra como as funções de identidade e acesso são mapeadas para as permissões do {{site.data.keyword.keymanagementserviceshort}}:
<table>
  <tr>
    <th>Função</th>
    <th>Descrição</th>
    <th>Ações</th>
  </tr>
  <tr>
    <td>Viewer</td>
    <td>Um visualizador pode acessar uma visualização de alto nível de chaves. Os visualizadores não podem acessar ou modificar os detalhes da chave.</td>
    <td>
      <ul>
        <li>Visualizar chaves</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Aplicativos</td>
    <td>Um editor pode criar chaves, modificar chaves e visualizar detalhes da chave.</td>
    <td>
      <ul>
        <li>Criar chaves</li>
        <li>Visualizar chaves</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Administrator</td>
    <td>Um administrador pode executar todas as ações que um visualizador e editor pode executar, incluindo a capacidade para excluir chaves, convidar novos usuários e gerenciar o controle de acesso. </td>
    <td>
      <ul>
        <li>Criar chaves</li>
        <li>Visualizar chaves</li>
        <li>Excluir chaves</li>
        <li>Gerenciar controle de acesso</li>
      </ul>
    </td>
  </tr>
  <caption style="caption-side:bottom;">Tabela 1. Mapeamento de funções de identidade e acesso para permissões do {{site.data.keyword.keymanagementserviceshort}}.</caption>
</table>

**Nota**: as funções de usuário do IAM fornecem acesso no nível de serviço ou de instância de serviço. As [funções do Cloud Foundry](/docs/iam/users_roles.html#cfroles) são separadas e definem o acesso no nível da organização ou do espaço.

Para saber mais sobre o {{site.data.keyword.Bluemix_notm}} Identity and Access Management, verifique [Funções e permissões de usuário](/docs/iam/users_roles.html#iamusermanpol).

### O que vem a seguir

Os proprietários e administradores de conta podem convidar usuários e configurar políticas de serviço que correspondem às ações do {{site.data.keyword.keymanagementserviceshort}} que os usuários podem executar.

- Para obter informações sobre como designar funções de usuário na UI do {{site.data.keyword.Bluemix_notm}}, veja [Políticas de acesso de serviço ativadas para identidade e acesso](/docs/iam/iamusermanage.html#iammanidaccser).
- Para aprender sobre como conceder permissões avançadas para acessar chaves de criptografia específicas, veja [Gerenciando acesso a chaves com a API](/docs/services/keymgmt/keyprotect_manage_access_api.html).
