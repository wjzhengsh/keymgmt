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

# API へのアクセス
{: #access-api}

{{site.data.keyword.keymanagementservicefull}} が提供する REST API を使用すると、任意のプログラミング言語を使用して、鍵の保管、取得、および生成を行うことができます。
{: shortdesc}

API で作業するには、サービス資格情報と認証資格情報を生成する必要があります。 

## アクセス・トークンの取得
{: #retrieve_token}

{{site.data.keyword.iamshort}} からアクセス・トークンを取得して、{{site.data.keyword.keymanagementserviceshort}} で認証できます。[サービス ID](/docs/iam/serviceid.html) を使用して、{{site.data.keyword.cloud_notm}} 上または外部にあるサービスまたはアプリケーションの代わりに、{{site.data.keyword.keymanagementserviceshort}} API で作業できます。個人のユーザー資格情報を共有する必要はありません。  

ユーザー資格情報で認証する場合は、[{{site.data.keyword.cloud_notm}} (bx) CLI ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/cloud-platform/cli/reference/bluemix_cli/get_started.html#getting-started){: new_window} で `bx iam oauth-tokens` を実行することによって、トークンを取得できます。
{: tip}

アクセス・トークンを取得するには、以下の手順を実行します。

1. {{site.data.keyword.cloud_notm}} コンソールで、**「管理」** &gt; **「セキュリティー」** &gt; **「ID およびアクセス」** &gt; **「サービス ID」**に移動します。[サービス ID の作成](/docs/iam/serviceid.html#creating-a-service-id){: new_window}のプロセスに従います。
2. **「アクション」**メニューを使用して、[新しいサービス ID のアクセス・ポリシーを定義します。](/docs/iam/serviceidaccess.html#assigning-new-access){: new_window} 
    
{{site.data.keyword.keymanagementserviceshort}} リソースに対するアクセス権限の管理について詳しくは、[役割と許可](/docs/services/keymgmt/keyprotect_manage_access.md#roles)を参照してください。
3. **「API キー」**セクションを使用して、[サービス ID に関連付ける API キーを作成します](/docs/iam/serviceid_keys.html#creating-an-api-key-for-a-service-id){: new_window}。API キーをダウンロードして、安全な場所に保存します。
4. {{site.data.keyword.iamshort}} API を呼び出して、アクセス・トークンを取得します。

    ```cURL
    curl -X POST \
      "https://iam.bluemix.net/oidc/token" \
      -H "Content-Type: application/x-www-form-urlencoded" \
      -H "Accept: application/json" \
      -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<your_API_key>" \ 
    ```
    {: codeblock}

    要求内の `<API_key>` を、ステップ 3 で作成した API キーに置き換えます。以下の省略された例は、トークンの出力を示しています。

    ```
    {
    "access_token": "eyJraWQiOiIyM...",
    "expiration": 1512161390,
    "expires_in": 3600,
    "refresh_token": "J1AzOrtC8yHVlcT...",
    "token_type": "Bearer"
    }
    ```
    {: screen}

    完全な `access_token` 値 (接頭部に _Bearer_ トークン・タイプが付いている) を使用して、サービス用の鍵を {{site.data.keyword.keymanagementserviceshort}} API を使ってプログラムで管理します。 

## インスタンス ID の取得
{: #retrieve_instance_ID}

{{site.data.keyword.keymanagementserviceshort}} サービス・インスタンスの識別情報を、[{{site.data.keyword.cloud_notm}} (bx) CLI ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/cloud-platform/cli/reference/bluemix_cli/get_started.html#getting-started){: new_window} を使用して取得できます。アカウントでは、インスタンス ID を使用して、{{site.data.keyword.keymanagementserviceshort}} の指定インスタンス内の暗号鍵を管理します。 

1. {{site.data.keyword.cloud_notm}} (bx) CLI を使用して、{{site.data.keyword.cloud_notm}} にログインします。

    ```sh
    bx login 
    ```
    {: pre}

    **注:** ログインに失敗した場合は、`bx login --sso` コマンドを実行して、再試行してください。フェデレーテッド ID を使用してログインする場合は、`--sso` パラメーターが必要です。 このオプションを使用する場合、CLI 出力にリストされたリンクにアクセスして、ワンタイム・パスコードを生成します。

2. {{site.data.keyword.keymanagementserviceshort}} のプロビジョン済みインスタンスを含むアカウントを選択します。

    `bx resource service-instances` を実行すると、アカウント内でプロビジョンされたすべてのサービス・インスタンスをリストできます。

3. {{site.data.keyword.keymanagementserviceshort}} サービス・インスタンスを一意的に識別するクラウド・リソース名 (CRN) を取得します。 

    ```sh
    bx resource service-instance <instance_name> --id
    ```
    {: pre}

    `<instance_name>` を、{{site.data.keyword.keymanagementserviceshort}} のインスタンスに割り当てた固有の別名に置き換えます。次の省略された例に、Bluemix CLI 出力を示しています。 _7e8fc048-5606-4259-ad71-92397b0fa3f7_ 値は、インスタンス ID の例です。

    ```
    crn:v1:bluemix:public:kms:us-south:a/7e8fc048-5606-4259-ad71-92397b0fa3f7
    ```
    {: screen}

## API 要求の作成
{: #form_api_request}

サービスに対して API 呼び出しを行う場合、{{site.data.keyword.keymanagementserviceshort}} のインスタンスを最初にプロビジョンした方法に応じて、API 要求を構成します。 

要求を作成するには、[地域のサービス・エンドポイント](/docs/services/keymgmt/keyprotect_regions.html)と適切な認証資格情報を組み合わせます。例えば、`us-south` 地域のサービス・インスタンスを作成した場合は、以下のエンドポイントと API ヘッダーを使用して、サービス内の鍵を表示します。

```cURL
curl -X GET \
    https://keyprotect.us-south.bluemix.net/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <access_token>' \
    -H 'bluemix-instance: <instance_ID>' \
```
{: codeblock}

### 次に行うこと

- プログラムでの鍵の管理について詳しくは、[{{site.data.keyword.keymanagementserviceshort}} API リファレンス資料に記載されているコード・サンプル ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/apidocs/639){: new_window} を確認してください。
- {{site.data.keyword.keymanagementserviceshort}} に保管されている鍵を使用してデータを暗号化および暗号化解除する方法の例は、[GitHub にあるサンプル・アプリで確認してください ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}。
