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

# 鍵の管理

{{site.data.keyword.keymanagementservicelong}} for {{site.data.keyword.Bluemix_short}} を使用して、鍵のライフサイクルを管理できます。{: shortdesc}

コードの開発時、鍵は安全に管理してください。例えば、他の安全なコーディング手法に加えて、以下のタイプのガイドラインを考慮してください。


- 鍵をコードに埋め込む際は、セキュリティーの影響を検討する。
- アプリおよびリソースにプログラムでアクセスする目的でのみ、鍵を作成する。より簡単な[ユーザー許可![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.bluemix.net/docs/admin/patterns.html#userroles "外部リンク・アイコン"){: new_window} を付与できる場合は、鍵は作成しない。
- 鍵を入れ替え、未使用の鍵は削除する。
- 機密性の高い操作については、多元的な認証を使用する。
- 各アプリに対して別々の鍵を設定することで、アプリを隔離する。
- 非常に機密性の高い情報を転送する場合は、プログラマチック API での処理を検討する。

## {{site.data.keyword.keymanagementserviceshort}} API の認証資格情報の生成
{: #authentication_api}

{{site.data.keyword.keymanagementservicelong_notm}} が提供する REST API を使用すると、任意のプログラミング言語を使用して、鍵の保管、取得、および生成を行うことができます。

API で作業するには、認証資格情報とサービス資格情報を生成する必要があります。

1. Cloud Foundry CLI を使用して、{{site.data.keyword.Bluemix_notm}} にログインします。

    ```
    cf login [a api.DomainName] [-sso]
    ```
    {: codeblock}

2. Key Protect サービス・インスタンスを含む {{site.data.keyword.Bluemix_notm}} の組織およびスペースを選択します。
    CLI 出力に表示される組織およびスペースの名前をメモしてください。この情報は `cf target` を実行して表示することもできます。
3. {{site.data.keyword.Bluemix_notm}} 組織およびスペース GUID を取得します。

    ```
    cf org organization_name --guid
    cf space space_name --guid
    ```
    {: codeblock}

4. {{site.data.keyword.Bluemix_notm}} アクセス・トークンを要求します。

    ```
cf oauth-token
```
    {: codeblock}

    次の省略された例に、{{site.data.keyword.Bluemix_notm}} トークン出力を示しています。_bearer
mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7_ 変数は、アクセス・トークンの例です。


    ```
bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7...```
    {: screen}

次に行うこと:

{{site.data.keyword.keymanagementserviceshort}} [REST API リファレンス資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/apidocs/639 "外部リンク・アイコン"){: new_window} を参照して、スペース内の鍵の管理を開始してください。


## {{site.data.keyword.keymanagementserviceshort}} API を使用した鍵の作成
{: #codingapps}

{{site.data.keyword.keymanagementservicelong_notm}} API を使用して、既存の鍵を保護したり、新規の鍵を生成したりできます。

以下のエンドポイントへの **POST** 呼び出しを行うことにより、鍵の作成または既存の鍵の追加を行います。

```
https://ibm-key-protect.edge.bluemix.net/api/v2/secrets```
{: codeblock}

自分の鍵を追加する前にサービスを試したい場合は、[サンプル・アプリ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/IBM-Bluemix/key-protect-helloworld-python "外部リンク・アイコン"){: new_window} を確認してください。

1. [サービスで鍵を処理するために、{{site.data.keyword.Bluemix_notm}} のアクセス・トークン、組織 GUID、およびスペース GUID を取得します](#authentication_api)。

2. 以下の cURL コマンドで [{{site.data.keyword.keymanagementserviceshort}} API](https://console.ng.bluemix.net/apidocs/639) を呼び出します。

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
  }' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets'```
  {: codeblock}

  次の表に従って、例の要求内の変数を置き換えてください。

  <table>
    <tr>
      <th>変数</th>
      <th>説明</th>
    </tr>
    <tr>
      <td><em>bluemix_access_token</em></td>
      <td>許可トークン。Bearer 値を含む、トークンの全コンテンツを cURL 要求に組み込みます。</td>
    </tr>
    <tr>
      <td><em>space_GUID</em></td>
      <td>{{site.data.keyword.Bluemix_notm}} スペースの ID。</td>
    </tr>
    <tr>
      <td><em>organization_GUID</em></td>
      <td>{{site.data.keyword.Bluemix_notm}} 組織の ID。</td>
    </tr>
    <tr>
      <td><em>key_alias</em></td>
      <td>鍵を簡単に識別するための、人間が理解できる名前。</td>
    </tr>
    <tr>
      <td><em>key_description</em></td>
      <td>鍵の詳しい説明。</td>
    </tr>
    <tr>
      <td><em>YYYY-MM-DD</em><br><em>HH:MM:SS.SS</em></td>
      <td>オプション: システム内の鍵の有効期限が切れる日時 (RFC3339 形式)。<code>expirationDate</code> 属性を省略した場合、鍵の有効期限は切れません。</td>
    </tr>
    <tr>
      <td><em>key_contents</em></td>
      <td>{{site.data.keyword.keymanagementserviceshort}} に保管する鍵の素材 (RSA 鍵など)。新規の鍵を生成するには、payload 属性と key_contents 変数は省略します。</td>
    </tr>
      <caption style="caption-side:bottom;">表 1. {{site.data.keyword.keymanagementserviceshort}} API を使用して鍵を追加するために必要な変数</caption>
  </table>

3. 次の呼び出しを実行して、{{site.data.keyword.Bluemix_notm}} スペース内の鍵を取得することにより、鍵が作成されたことを確認します。

  ```cURL
  curl -X GET --header 'Accept: application/json' --header 'Authorization: bluemix_access_token' --header 'Bluemix-Space: space_GUID' --header 'Bluemix-Org: organization_GUID' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets'
  ```
  {: codeblock}

## {{site.data.keyword.keymanagementserviceshort}} API を使用した鍵の表示
{: #viewingkeys_api}

{{site.data.keyword.Bluemix_notm}} スペースの管理者または開発者は、{{site.data.keyword.keymanagementservicelong_notm}} API を使用して鍵の内容を表示できます。

概要を参照するために、{{site.data.keyword.keymanagementserviceshort}} UI を使用して、スペースで管理されている鍵を表示できます。

以下のエンドポイントへの GET 呼び出しを行うことにより、鍵に関する詳細情報を表示します。

```
https://ibm-key-protect.edge.bluemix.net/api/v2/secrets/key_ID
```
{: codeblock}

1. {{site.data.keyword.keymanagementserviceshort}} UI のセキュリティー・サービスで、鍵に関する一般的な特性を表示できます。ソート可能な列ヘッダーをクリックして、鍵を表示できます。
2. 鍵の行に **ID** をコピーします。この ID 値を使用して、API で鍵に関するより詳細な情報 (鍵の素材自体など) にアクセスします。
3. [サービスで鍵を処理するために、{{site.data.keyword.Bluemix_notm}} アクセス・トークン、組織 GUID、およびスペース GUID を取得します。](#authentication_api)
4. 次の cURL コマンドを実行して、鍵と鍵の素材に関する詳細を取得します。

  ```cURL
  curl -X GET --header 'Accept: application/json' --header 'Authorization: bluemix_access_token' --header 'Bluemix-Space: space_GUID' --header 'Bluemix-Org: organization_GUID' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets/key_ID'
  ```
  {: codeblock}

  次の表に従って、例の要求内の変数を置き換えてください。

  <table>
    <tr>
      <th>変数</th>
      <th>説明</th>
    </tr>
    <tr>
      <td><em>bluemix_access_token</em></td>
      <td>許可トークン。Bearer 値を含む、トークンの全コンテンツを cURL 要求に組み込みます。</td>
    </tr>
    <tr>
      <td><em>space_GUID</em></td>
      <td>{{site.data.keyword.Bluemix_notm}} スペースに割り当てられたランダム生成の ID。
</td>
    </tr>
    <tr>
      <td><em>organization_GUID</em></td>
      <td>{{site.data.keyword.Bluemix_notm}} 組織に割り当てられたランダム生成の ID。
</td>
    </tr>
    <tr>
      <td><em>key_ID</em></td>
      <td>ステップ [2](https://console.bluemix.net/docs/services/keymgmt/managing.html#viewingkeys_api__keyid) でプルアップした鍵の ID。</td>
    </tr>
    <caption style="caption-side:bottom;">表 2. {{site.data.keyword.keymanagementserviceshort}} API を使用して鍵を表示するために必要な変数についての説明</caption>
  </table>

  鍵の素材は、応答のエンティティー本体で返されます。ハードウェア・セキュリティー・モジュール (HSM) によって生成される鍵は、base-64 でエンコードされています。

## 鍵およびアクセスの監査
{: #viewkeyassignments}

{{site.data.keyword.keymanagementservicelong_notm}} により、
暗号鍵を表示、管理、監査する集中システムが提供されます。
鍵と鍵へのアクセス制限を監査して、リソースのセキュリティーを確保します。

定期的に鍵の構成を監査するために、以下を行います。

- いつ鍵が作成されたかを調べ、鍵を回転する時期かどうかを判断します。
- [{{site.data.keyword.cloudaccesstrailshort}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン") を使用して、{{site.data.keyword.keymanagementserviceshort}} への API 呼び出しをモニターします](https://console.bluemix.net/docs/services/AccessTrail/at_integration.html#at_integration_key_protect "外部リンク・アイコン"){: new_window}。
- どのユーザーが鍵へのアクセス権限を持っているか、アクセス権限のレベルは適切かどうかを検査します。

次のアクセス権を持つユーザーを監査するには、以下のようにします。

1. スペース管理者のアクセス権を持つユーザーを監査するには、アカウント設定に移動し、**「組織の管理」**を選択します。
2. {{site.data.keyword.keymanagementserviceshort}} サービス・インスタンスを含むスペースを開いて、どのユーザーがアクセス権限を持っているか調べます。
3. ユーザーを追加する必要がある場合、**「チーム・メンバーの招待」**に進み、以下のように、そのユーザーに付与する {{site.data.keyword.keymanagementserviceshort}} の許可に対応する {{site.data.keyword.Bluemix_notm}} の役割を選択します。

  <table>
    <tr>
      <th>{{site.data.keyword.Bluemix_notm}} 役割</th>
      <th>{{site.data.keyword.keymanagementserviceshort}} 許可</th>
    </tr>
    <tr>
      <td>スペース管理者</td>
      <td>スペース管理者は、鍵を作成、表示、および削除できる。</td>
    </tr>
    <tr>
      <td>開発者</td>
      <td>開発者は、鍵を作成し、鍵の詳細を表示できる。</td>
    </tr>
    <tr>
      <td>監査員</td>
      <td>監査員は、鍵の高レベルのビューにアクセスできる。</td>
    </tr>
    <caption style="caption-side:bottom;">表 3. {{site.data.keyword.keymanagementserviceshort}} 許可への {{site.data.keyword.Bluemix_notm}} 役割のマッピング</caption>
  </table>
