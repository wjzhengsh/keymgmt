---

copyright:
  years: 2017
lastupdated: "2017-11-08"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Gerando credenciais de autenticação
{: #authentication}

O {{site.data.keyword.keymanagementservicefull}} fornece uma API de REST que pode ser usada com qualquer
linguagem de programação para armazenar, recuperar e gerar chaves.
{: shortdesc}

Para trabalhar com a API, é necessário gerar suas credenciais de serviço e autenticação.

## Recuperando seus GUIDs de organização e espaço
{: #retrieve_GUIDs}

É possível recuperar informações de identificação para sua organização e espaço do {{site.data.keyword.cloud_notm}} com a CLI do [{{site.data.keyword.cloud_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.bluemix.net/docs/cli/reference/bluemix_cli/index.html#getting-started).

1. Efetue login no {{site.data.keyword.cloud_notm}} por meio da CLI do {{site.data.keyword.cloud_notm}} (bx).

    ```
    bx login [--sso]
    ```
    {: codeblock}

    O parâmetro `--sso` é necessário quando você efetua login com um ID federado. Se essa opção for usada, acesse o link listado na saída da CLI para gerar uma senha descartável.

2. Selecione a organização e o espaço do {{site.data.keyword.cloud_notm}} que contêm a sua instância de serviço {{site.data.keyword.keymanagementserviceshort}}.

    Observe os nomes de sua organização e o espaço na saída da CLI. Também é possível executar o `bx target` para visualizar essas informações.

3. Recupere a sua organização do {{site.data.keyword.cloud_notm}} e
GUIDs de espaço.

    ```
    bx iam org [organization_name] --guid
    bx iam space [space_name] --guid
    ```
    {: codeblock}
    Substitua _organization_name_ e _space_name_ pelo alias exclusivo designado para a sua organização e seu espaço.

## Recuperando o token de autorização
{: #retrieve_token}

É possível usar um token de autorização para gerenciar programaticamente suas chaves usando a API do {{site.data.keyword.keymanagementserviceshort}}.

**Nota**: para permitir o controle de acesso granular governado pelo {{site.data.keyword.iamshort}}, use um token IAM ao fazer chamadas para o serviço.

1. Na CLI do {{site.data.keyword.cloud_notm}}, selecione a organização e o espaço que contêm seu serviço {{site.data.keyword.keymanagementserviceshort}}.

2. Recupere e exiba seus tokens de autorização.

    ```
    bx iam oauth-tokens
    ```
    {: codeblock}

    O exemplo truncado a seguir mostra a saída de token do {{site.data.keyword.cloud_notm}}. A variável _Bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7_ é um token de acesso de exemplo.

    ```
    Token do IAM: Portador mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7...
    Token do UAA: Portador mjEyJhbGciOiJIUzI1Ni.chWyW1faWQiOiJJQkWs1...
    ```
    {: screen}

    Use o valor do portador `IAM` ou `UAA` para gerenciar programaticamente as chaves em seu serviço usando a API do {{site.data.keyword.keymanagementserviceshort}}.

### O que vem a seguir

Consulte o [{{site.data.keyword.keymanagementserviceshort}}documento de referência da API de REST ![Ícone de linkexterno](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/apidocs/639){: new_window} para iniciar o gerenciamento de chaves em seu espaço.

