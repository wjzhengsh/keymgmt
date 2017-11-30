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

# 鍵の削除

{{site.data.keyword.cloud_notm}} スペースまたは {{site.data.keyword.keymanagementserviceshort}} サービス・インスタンスの管理者は、{{site.data.keyword.keymanagementservicefull}} を使用して暗号鍵とその内容を削除できます。
{: shortdesc}

**重要**: 鍵を削除すると、その内容と関連データが完全に廃棄されます。このアクションは、元に戻すことはできません。リソースを破棄することは、実稼働環境ではお勧めできませんが、テストや QA などの一時的な環境には便利な場合があります。

## GUI を使用した鍵の削除
{: #gui}

グラフィカル・インターフェースを使用して鍵のリソースを削除したい場合は、{{site.data.keyword.keymanagementserviceshort}} GUI を使用できます。

[サービス内に鍵を作成するか、既存の鍵をインポートした後](/docs/services/keymgmt/keyprotect_create_keys.html)、鍵を削除するには以下の手順を実行します。

1. [{{site.data.keyword.cloud_notm}} コンソール ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.bluemix.net/) にログインします。
2. {{site.data.keyword.cloud_notm}} ダッシュボードで、{{site.data.keyword.keymanagementserviceshort}} のプロビジョン済みインスタンスを選択します。
3. **「管理」**ペインに移動し、サービスの鍵を表示します。
4. 垂直省略符号アイコンをクリックして、削除する鍵に関するオプションのリストを開きます。
5. オプション・メニューから、**「鍵の削除 (Delete key)」**をクリックし、次の画面で鍵の削除を確認します。

## API を使用した鍵の削除
{: #api}

鍵とその内容を削除するには、次のエンドポイントへの `DELETE` 呼び出しを行います。

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID>
```

1. [サービスで鍵を処理するために、許可トークン、組織 GUID、およびスペース GUID を取得します](/docs/services/keymgmt/keyprotect_authentication.html)。

2. 削除する鍵の ID を取得します。

    `GET /v2/keys` 要求を行うか、{{site.data.keyword.keymanagementserviceshort}} ダッシュボードに鍵を表示することで、指定の鍵の ID を取得できます。

3. 次の cURL コマンドを実行して、鍵とその内容を完全に削除します。

    ```cURL
    curl -X DELETE \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID> \
      -H 'authorization: Bearer <OAuth_token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
      -H 'prefer: <return_preference>'
    ```
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
        <td><em>space_GUID</em></td>
        <td>{{site.data.keyword.cloud_notm}} スペースに割り当てられた固有 ID。</td>
      </tr>
      <tr>
        <td><em>organization_GUID</em></td>
        <td>{{site.data.keyword.cloud_notm}} 組織に割り当てられた固有 ID。</td>
      </tr>
      <tr>
        <td><em>key_ID</em></td>
        <td>削除する鍵の固有 ID。</td>
      </tr>
      <tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p><code>POST</code> および <code>DELETE</code> の操作に関するサーバーの動作を変更するヘッダー。</p><p><code>return=minimal</code> に設定すると、サービスは鍵のメタデータ (鍵の名前と <code>id</code> 値など) のみを応答のエンティティー本体で返します。<code>return=representation</code> に設定すると、サービスは鍵の素材と鍵のメタデータの両方を返します。</p></td>
      </tr>
      <caption style="caption-side:bottom;">表 1. {{site.data.keyword.keymanagementserviceshort}} API を使用して鍵を削除するために必要な変数についての説明</caption>
    </table>

    `DELETE` 要求の詳細は、応答のエンティティー本体で返されます。
