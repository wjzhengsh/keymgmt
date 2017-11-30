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

# 鍵の作成

{{site.data.keyword.keymanagementservicefull}} を使用して、鍵のライフサイクルを管理できます。
{: shortdesc}

コードの開発時、鍵は安全に管理してください。例えば、他の安全なコーディング手法に加えて、以下のガイドラインを考慮してください。

- 鍵をコードに埋め込む際は、セキュリティーの影響を検討する。
- アプリおよびリソースにプログラムでアクセスする目的でのみ、鍵を作成する。より簡単な[ユーザー許可![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.bluemix.net/docs/admin/patterns.html#userroles){: new_window} を付与できる場合は、鍵は作成しない。
- 鍵を入れ替え、未使用の鍵は削除する。
- 機密性の高い操作については、多元的な認証を使用する。
- 各アプリに対して別々の鍵を設定することで、アプリを隔離する。
- 非常に機密性の高い情報を転送する場合は、プログラマチック API での処理を検討する。

自分の鍵を追加する前にサービスを試したい場合は、[サンプル・アプリ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window} を確認してください。

## GUI を使用した鍵の作成
{: #gui}

{{site.data.keyword.keymanagementserviceshort}} GUI を使用してサービスに鍵を追加するには、[{{site.data.keyword.keymanagementserviceshort}} の概説](/docs/services/keymgmt/index.html#addkey)を参照してください。

## API を使用した鍵の作成
{: #api}

{{site.data.keyword.keymanagementserviceshort}} API を使用して、プログラムで既存の鍵を保護したり、新規の鍵を生成したりできます。

以下のエンドポイントへの `POST` 呼び出しを行うことにより、鍵の作成または既存の鍵のインポートを行います。

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys
```
{: codeblock}

1. [サービスで鍵を処理するために、許可トークン、組織 GUID、およびスペース GUID を取得します](/docs/services/keymgmt/keyprotect_authentication.html)。

2. 以下の cURL コマンドで [{{site.data.keyword.keymanagementserviceshort}} API](https://console.ng.bluemix.net/apidocs/639) を呼び出します。

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

    次の表に従って、例の要求内の変数を置き換えてください。
<table>
      <tr>
        <th>変数</th>
        <th>説明</th>
      </tr>
      <tr>
        <td><em>OAuth_token</em></td>
        <td>許可トークン。Bearer 値を含む、トークンの全コンテンツを cURL 要求に組み込みます。</td>
      </tr>
      <tr>
        <td><em>organization_GUID</em></td>
        <td>{{site.data.keyword.cloud_notm}} 組織に割り当てられた固有 ID。</td>
      </tr>
      <tr>
        <td><em>space_GUID</em></td>
        <td>{{site.data.keyword.cloud_notm}} スペースに割り当てられた固有 ID。</td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>トランザクションを追跡し、相互に関連付けるために使用される固有 ID。</td>
      </tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p><code>POST</code> および <code>DELETE</code> の操作に関するサーバーの動作を変更するヘッダー。</p><p><code>return=minimal</code> に設定すると、サービスは鍵のメタデータ (鍵の名前と <code>id</code> 値など) のみを応答のエンティティー本体で返します。<code>return=representation</code> に設定すると、サービスは鍵の素材と鍵のメタデータの両方を返します。</p></td>
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
        <td>オプション: システム内の鍵の有効期限が切れる日時 (RFC 3339 形式)。<code>expirationDate</code> 属性を省略した場合、鍵の有効期限は切れません。</td>
      </tr>
      <tr>
        <td><em>key_material</em></td>
        <td>{{site.data.keyword.keymanagementserviceshort}} に保管する鍵の素材 (RSA 鍵など)。新しい鍵を生成するには、<code>payload</code> 属性と <em>key_material</em> 変数を省略します。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. {{site.data.keyword.keymanagementserviceshort}} API を使用して鍵を追加するために必要な変数</caption>
    </table>

    正常な応答では、鍵の `id` 値を、他のメタデータと共に返します。`id` は、鍵に割り当てられた固有 ID であり、以降の呼び出しで使用されます。

3. **オプション:** 次の呼び出しを実行して、{{site.data.keyword.cloud_notm}} スペース内の鍵を取得することにより、鍵が作成されたことを確認します。

    ```cURL
    curl -X GET \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <OAuth-token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
    ```
    {: codeblock}

### 次に行うこと

これで、鍵を使用してアプリやサービスをコーディングできるようになりました。

- 各 REST 要求と応答の詳細については、{{site.data.keyword.keymanagementserviceshort}}[REST API リファレンス資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/apidocs/639){: new_window} で確認してください。
