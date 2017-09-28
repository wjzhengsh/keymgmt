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

# 認証資格情報の生成
{: #authentication}

{{site.data.keyword.keymanagementservicefull}} が提供する REST API を使用すると、任意のプログラミング言語を使用して、鍵の保管、取得、および生成を行うことができます。{: shortdesc}

API で作業するには、サービス資格情報と認証資格情報を生成する必要があります。

## 組織およびスペースの GUID の取得
{: #retrieve_GUIDs}

[{{site.data.keyword.Bluemix_notm}} CLI ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.bluemix.net/docs/cli/reference/bluemix_cli/index.html#getting-started) を使用して、{{site.data.keyword.Bluemix_notm}} 組織およびスペースの ID 情報を取得できます。

1. {{site.data.keyword.Bluemix_notm}} CLI を使用して、{{site.data.keyword.Bluemix_notm}} にログインします。

    ```
    bx login [--sso]
    ```
    {: codeblock}

    フェデレーテッド ID を使用してログインする場合は、`--sso` パラメーターが必要です。このオプションを使用する場合、CLI 出力にリストされたリンクにアクセスして、ワンタイム・パスコードを生成します。

2. {{site.data.keyword.keymanagementserviceshort}} サービス・インスタンスを含む {{site.data.keyword.Bluemix_notm}} 組織およびスペースを選択します。

    CLI 出力に表示される組織およびスペースの名前をメモしてください。この情報は `bx target` を実行して表示することもできます。

3. {{site.data.keyword.Bluemix_notm}} 組織およびスペース GUID を取得します。

    ```
    bx iam org [organization_name] --guid
    bx iam space [space_name] --guid
    ```
    {: codeblock}
    _organization_name_ および _space_name_ を、組織およびスペースに割り当てた固有の別名に置き換えます。
## 許可トークンの取得
{: #retrieve_token}

許可トークンを使用すると、{{site.data.keyword.keymanagementserviceshort}} API を使用してプログラムで鍵を管理できます。

**注**: {{site.data.keyword.Bluemix_notm}} Identity and Access Management によって管理される細分化されたアクセス制御を有効にするには、サービスへの呼び出しを行うときに IAM トークンを使用します。

1. {{site.data.keyword.Bluemix_notm}} CLI で、{{site.data.keyword.keymanagementserviceshort}} サービスを含む組織およびスペースを選択します。

2. 許可トークンを取得し、表示します。

    ```
    bx iam oauth-tokens
    ```
    {: codeblock}

    次の省略された例に、{{site.data.keyword.Bluemix_notm}} トークン出力を示しています。_Bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7_ 変数は、アクセス・トークンの例です。

    ```
    IAM token: Bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7...
    UAA token: Bearer mjEyJhbGciOiJIUzI1Ni.chWyW1faWQiOiJJQkWs1...
    ```
    {: screen}

    {{site.data.keyword.keymanagementserviceshort}} API を使用してサービスの鍵をプログラムで管理するには、`IAM` または `UAA` のベアラー値を使用します。

### 次に行うこと

[{{site.data.keyword.keymanagementserviceshort}}REST API リファレンス資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/apidocs/639){: new_window} を参照して、スペース内の鍵の管理を開始してください。
