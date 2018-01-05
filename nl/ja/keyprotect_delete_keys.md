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

# 鍵の削除
{: #deleting-keys}

{{site.data.keyword.cloud_notm}} スペースまたは {{site.data.keyword.keymanagementserviceshort}} サービス・インスタンスの管理者は、{{site.data.keyword.keymanagementservicefull}} を使用して暗号鍵とその内容を削除できます。
{: shortdesc}

**重要:** 鍵を削除すると、その内容と関連データが完全に廃棄されます。 このアクションは、元に戻すことはできません。 リソースを破棄することは、実稼働環境ではお勧めできませんが、テストや QA などの一時的な環境には便利な場合があります。

## GUI を使用した鍵の削除
{: #gui}

グラフィカル・インターフェースを使用して暗号鍵を削除したい場合は、{{site.data.keyword.keymanagementserviceshort}} GUI を使用できます。

[サービス内に鍵を作成するか、既存の鍵をインポートした後](/docs/services/keymgmt/keyprotect_create_keys.html)、鍵を削除するには以下の手順を実行します。

1. [{{site.data.keyword.cloud_notm}} コンソール ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.bluemix.net/) にログインします。
2. {{site.data.keyword.cloud_notm}} ダッシュボードで、{{site.data.keyword.keymanagementserviceshort}} のプロビジョン済みインスタンスを選択します。
3. **「鍵 (Keys)」**テーブルを使用して、サービス内の鍵を表示します。
4. ⋮ アイコンをクリックして、削除する鍵に関するオプションのリストを開きます。
5. オプション・メニューから、**「鍵の削除 (Delete key)」**をクリックし、次の画面で鍵の削除を確認します。

鍵を削除した後、鍵は_破棄_ 状態に遷移します。この状態の鍵は、リカバリーできなくなっています。鍵の削除日など、鍵に関連付けられているメタデータは、{{site.data.keyword.keymanagementserviceshort}} データベースに保管されます。

## API を使用した鍵の削除
{: #api}

鍵とその内容を削除するには、次のエンドポイントへの `DELETE` 呼び出しを行います。

```
https://keyprotect.us-south.bluemix.net/api/v2/keys<key_ID>
```

1. [サービス内で鍵の処理を行うために、サービスおよび認証の資格情報を取得します。](/docs/services/keymgmt/keyprotect_authentication.html)

2. 削除する鍵の ID を取得します。

    `GET /v2/keys/` 要求を行うか、{{site.data.keyword.keymanagementserviceshort}} ダッシュボードに鍵を表示することで、指定の鍵の ID を取得できます。

3. 次の cURL コマンドを実行して、鍵とその内容を完全に削除します。

    ```cURL
    curl -X DELETE \
      https://keyprotect.us-south.bluemix.net/api/v2/keys<key_ID> \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'prefer: <return_preference>'
    ```
    {: codeblock}
  
    アカウントの指定された Cloud Foundry 組織およびスペース内で鍵の処理を行うには、`Bluemix-Instance` を、適切な `Bluemix-org` および `Bluemix-space` のヘッダーに置き換えます。[{{site.data.keyword.keymanagementserviceshort}} API リファレンス資料に記載されているコード・サンプル ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/apidocs/639){: new_window} を参照してください。{: tip}

    次の表に従って、例の要求内の変数を置き換えてください。
    <table>
      <tr>
        <th>変数</th>
        <th>説明</th>
      </tr>
      <tr>
        <td><em>IAM_token</em></td>
        <td>許可トークン。 Bearer 値を含む、<code>IAM</code> トークンの全コンテンツを cURL 要求に組み込みます。</td>
      </tr>
      <tr>
        <td><em>instance_ID</em></td>
        <td>{{site.data.keyword.keymanagementserviceshort}} サービス・インスタンスに割り当てられた固有 ID。 </td>
      </tr>
      <tr>
        <td><em>key_ID</em></td>
        <td>削除する鍵の固有 ID。</td>
      </tr>
      <tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p><code>POST</code> および <code>DELETE</code> の操作に関するサーバーの動作を変更するヘッダー。</p><p><em>return_preference</em> 変数を <code>return=minimal</code> に設定すると、サービスは, 成功した削除応答を返します。変数を <code>return=representation</code> に設定すると、サービスは鍵の素材と鍵のメタデータの両方を返します。</p></td>
      </tr>
      <caption style="caption-side:bottom;">表 1. {{site.data.keyword.keymanagementserviceshort}} API を使用して鍵を削除するために必要な変数についての説明</caption>
    </table>

    _return_preference_ 変数を `return=representation` に設定すると、`DELETE` 要求の詳細が、応答のエンティティー本体で返されます。<!--After you delete a key, it enters the `Deactivated` key state. After 24 hours, if a key is not reinstated, the key transitions to the `Destroyed` state. The key contents are permanently erased and no longer accessible.--> 以下の JSON オブジェクトは、返された値の例を示しています。
    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.kms.key+json",
       "collectionTotal": 1
      },
    "resources": [
      {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "...",
          "description": "...",
          "state": 5,
          "crn": "...",
          "deleted": true,
          "algorithmType": "AES",
          "createdBy": "...",
          "deletedBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "deletionDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "nonactiveStateReason": 2,
          "extractable": true
        }
      ]
    }
    ```
    {: screen}

    使用可能なパラメーターについて詳しくは、{{site.data.keyword.keymanagementserviceshort}} [REST API リファレンス資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/apidocs/639){: new_window} を参照してください。
