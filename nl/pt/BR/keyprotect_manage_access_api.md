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

# Gerenciando acesso a chaves com a API
{: #managing-access-api}

Com o {{site.data.keyword.Bluemix}} Identity and Access Management, é possível ativar o controle de acesso granular para seus recursos de chave criando e modificando políticas de acesso.
{: shortdesc}

Esta página conduz pelos vários cenários para gerenciar o acesso aos recursos de chave com a [API de gerenciamento de acesso![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://iampap.ng.bluemix.net/v1/docs/#!/Access_Policies/){: new_window}.


Antes de começar:
- [Recupere seu GUID de token e espaço do IAM](/docs/services/keymgmt/keyprotect_authentication.html)
- [Recupere o ID de chave para especificar o recurso](/docs/services/keymgmt/keyprotect_view_keys.html)
- [Recupere o ID da conta para especificar o escopo de acesso](keyprotect_manage_access_api.html#retrieve_account_ID)
- [Recupere o ID do usuário do usuário cujo acesso você gostaria de modificar](keyprotect_manage_access_api.html#retrieve_user_ID)

## Criando uma nova política de acesso
{: #create_policy}

Para ativar o controle de acesso para uma chave específica, é possível enviar uma solicitação para o {{site.data.keyword.Bluemix_notm}} Identity and Access Management executando o comando a seguir. Repita o comando para cada política de acesso.

```cURL
curl -X POST \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
  "roles": [
    {
      "id": "crn:v1:bluemix:public:iam::::role:<IAM_role>"
    }
  ],
  "resources": [
    {
      "serviceName": "IBM Key Protect",
      "region": "us-south",
      "resourceType": "key",
      "resource": "<key_ID>",
      "accountId": "<account_ID>",
      "spaceId": "<space_GUID>"
    }
  ]
}'
```
{: codeblock}

Substitua `<account_ID>`, `<user_ID>`, `<Admin_IAM_token>`, `<IAM_role>`, `<space_GUID>` e `<key_ID>` pelos valores apropriados.

**Opcional:** verifique se a política foi criada com êxito.

```cURL
curl -X GET \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}


## Atualizando uma política de acesso
{: #update_policy}

É possível usar um ID de política recuperado para modificar uma política existente para um usuário. Envie uma solicitação para o {{site.data.keyword.Bluemix_notm}} Identity and Access Management executando o comando a seguir:

```cURL
curl -X PUT \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies/<policy_ID> \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'If-Match': <ETag_ID> \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
  "roles": [
    {
      "id": "crn:v1:bluemix:public:iam::::role:<IAM_role>"
    }
  ],
  "resources": [
    {
      "serviceName": "IBM Key Protect",
      "region": "us-south",
      "resourceType": "key",
      "resource": "<key_ID>",
      "accountId": "<account_ID>",
      "spaceId": "<space_GUID>"
    }
  ]
}'
```
{: codeblock}

Substitua `<account_ID>`, `<user_ID>`, `<policy_ID>`, `<Admin_IAM_token>`, `<ETag_ID>`, `<IAM_role>`, `<space_GUID>` e `<key_ID>` pelos valores apropriados.

**Opcional:** verifique se a política foi atualizada com êxito.

```cURL
curl -X GET \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

## Excluindo uma política de acesso
{: #delete_policy}

É possível usar um ID de política recuperado para excluir uma política existente para um usuário. Envie uma solicitação para o {{site.data.keyword.Bluemix_notm}} Identity and Access Management executando o comando a seguir:

```cURL
curl -X DELETE \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies/<policy_ID> \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

Substitua `<account_ID>`, `<user_ID>`, `<policy_ID>` e `<Admin_IAM_token>` pelos valores apropriados.

**Opcional:** verifique se a política foi excluída com êxito.

```cURL
curl -X GET \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

## Recuperando o ID da conta
{: #retrieve_account_id}

1. Efetue login na CLI do {{site.data.keyword.Bluemix_notm}}.
    ```sh
    bx login [--sso]
    ```
    {: codeblock}

    **Nota**: o parâmetro `--sso` é necessário ao efetuar login com um ID federado. Se essa opção for usada, acesse o link listado na saída da CLI para gerar uma senha descartável.

    O resultado exibe as informações de identificação para sua conta.

    ```sh
    Authenticating...
    OK

    Selecionar uma conta (ou pressionar Enter para ignorar):

    1. sample-account (b6hnh3560ehqjkf89s4ba06i367801e)
    Enter a number> 1
    Targeted account sample-acount (b6hnh3560ehqjkf89s4ba06i367801e)

    API endpoint:   https://api.ng.bluemix.net (API version: 2.75.0)
    Region:         us-south
    User:           admin
    Account:        sample-account (b6hnh3560ehqjkf89s4ba06i367801e)
    ```
    {: screen}
2. Copie o valor para seu ID da conta.

## Recuperando o ID do usuário
{: #retrieve_user_id}

1. [Peça ao usuário para fornecer seu token do IAM](/docs/services/keymgmt/keyprotect_authentication.html#retrieve_token).
    A estrutura de token do IAM é a seguinte:

    ```sh
    IAM token: Bearer <value>.<value>.<value>
    ```
    {: screen}

2. Copie o valor médio e execute o comando a seguir:
    ```sh
    echo -n "<value>" | base64 --decode
    ```
    {: codeblock}

    O resultado mostra um objeto JSON semelhante ao seguinte:
   ```json
   {
        "iam_id":"...",
        "id":"...",
        "realmid":"...",
        "identifier":"...",
        "given_name":"...",
        "family_name":"...",
        "name":"...",
        "email":"...",
        "sub":"...",
        "account":{
            "bss":"..."},
            "iat":...,
            "exp":...,
            "iss":"...",
            "grant_type":"...",
            "scope":"...",
            "client_id":"..."
        }
   }
   ```
   {: screen}

4. Copie o valor da propriedade `id`.
