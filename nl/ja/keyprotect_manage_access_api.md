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

# API を使用した鍵へのアクセス権限の管理
{: #managing-access-api}

{{site.data.keyword.iamlong}} を使用すると、アクセス・ポリシーを作成および変更することによって、鍵リソースに対する細分化されたアクセス制御を有効にすることができます。
{: shortdesc}

このページでは、[Access Management API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://iampap.ng.bluemix.net/v1/docs/#!/Access_Policies/){: new_window} を使用して鍵リソースへのアクセス権限を管理するためのシナリオをいくつか紹介します。


開始する前に、以下を行います。
- [IAM トークンおよびスペース GUID を取得します](/docs/services/keymgmt/keyprotect_authentication.html)
- [リソースを指定するために鍵 ID を取得します](/docs/services/keymgmt/keyprotect_view_keys.html)
- [アクセスの有効範囲を指定するためにアカウント ID を取得します](keyprotect_manage_access_api.html#retrieve_account_ID)
- [アクセス権限を変更するユーザーのユーザー ID を取得します](keyprotect_manage_access_api.html#retrieve_user_ID)

## 新規アクセス・ポリシーの作成
{: #create_policy}

特定の鍵に対するアクセス制御を有効にするには、以下のコマンドを実行して、{{site.data.keyword.iamshort}} に要求を送信します。アクセス・ポリシーごとにコマンドを繰り返します。

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

`<account_ID>`、`<user_ID>`、`<Admin_IAM_token>`、`<IAM_role>`、`<space_GUID>`、および `<key_ID>` を適切な値に置き換えます。

**オプション:** ポリシーが正常に作成されたことを確認します。

```cURL
curl -X GET \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}


## アクセス・ポリシーの更新
{: #update_policy}

取得したポリシー ID を使用して、ユーザーの既存のポリシーを変更できます。以下のコマンドを実行して、{{site.data.keyword.iamshort}} に要求を送信します。

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

`<account_ID>`、`<user_ID>`、`<policy_ID>`、`<Admin_IAM_token>`、`<ETag_ID>`、`<IAM_role>`、`<space_GUID>`、および `<key_ID>` を適切な値に置き換えます。

**オプション:** ポリシーが正常に更新されたことを確認します。

```cURL
curl -X GET \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

## アクセス・ポリシーの削除
{: #delete_policy}

取得したポリシー ID を使用して、ユーザーの既存のポリシーを削除できます。以下のコマンドを実行して、{{site.data.keyword.iamshort}} に要求を送信します。

```cURL
curl -X DELETE \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies/<policy_ID> \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

`<account_ID>`、`<user_ID>`、`<policy_ID>`、および `<Admin_IAM_token>` を適切な値に置き換えます。

**オプション:** ポリシーが正常に削除されたことを確認します。

```cURL
curl -X GET \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

## アカウント ID の取得
{: #retrieve_account_id}

1. Bluemix CLI にログインします。
    ```sh
    bx login [--sso]
    ```
    {: codeblock}

    **注:** フェデレーテッド ID を使用してログインする場合は、`--sso` パラメーターが必要です。このオプションを使用する場合、CLI 出力にリストされたリンクにアクセスして、ワンタイム・パスコードを生成します。

    結果に、アカウントの ID 情報が表示されます。

    ```sh
    Authenticating...
    OK

    Select an account (or press enter to skip):

    1. sample-account (b6hnh3560ehqjkf89s4ba06i367801e)
    Enter a number> 1
    Targeted account sample-acount (b6hnh3560ehqjkf89s4ba06i367801e)

    API endpoint:   https://api.ng.bluemix.net (API version: 2.75.0)
    Region:         us-south
    User:           admin
    Account:        sample-account (b6hnh3560ehqjkf89s4ba06i367801e)
    ```
    {: screen}
2. アカウント ID の値をコピーします。

## ユーザー ID の取得
{: #retrieve_user_id}

1. [ユーザーに IAM トークンを提供するように依頼します](/docs/services/keymgmt/keyprotect_authentication.html#retrieve_token)。IAM トークンの構造は次のとおりです。

    ```sh
    IAM token: Bearer <value>.<value>.<value>
    ```
    {: screen}

2. 中央の値をコピーして、次のコマンドを実行します。
    ```sh
    echo -n "<value>" | base64 --decode
    ```
    {: codeblock}

    結果に、以下のような JSON オブジェクトが表示されます。
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

4. `id` プロパティーの値をコピーします。
