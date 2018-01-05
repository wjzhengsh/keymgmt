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

# ルート鍵のインポート
{: #import_root_keys}

{{site.data.keyword.keymanagementservicefull}} では、{{site.data.keyword.keymanagementserviceshort}} GUI を使用して、あるいは {{site.data.keyword.keymanagementserviceshort}} API を使用してプログラムで、既存のルート鍵を保護することができます。
{: shortdesc}

ルート鍵は、クラウド内の暗号化データのセキュリティーを保護するために使用される対称鍵ラップ鍵です。ルート鍵について詳しくは、[エンベロープ暗号化](/docs/services/keymgmt/keyprotect_envelope.html)を参照してください。 

## GUI を使用したルート鍵のインポート
{: #import_root_key_GUI}

[サービスのインスタンスを作成した後](/docs/services/keymgmt/keyprotect_provision.html)、以下の手順を実行して、{{site.data.keyword.keymanagementserviceshort}} GUI で既存のルート鍵を追加します。

1. [{{site.data.keyword.cloud_notm}} コンソール ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.bluemix.net/) にログインします。
2. {{site.data.keyword.cloud_notm}} ダッシュボードで、{{site.data.keyword.keymanagementserviceshort}} のプロビジョン済みインスタンスを選択します。
2. 鍵をインポートするには、**「鍵の追加」**をクリックして、**「既存の鍵の入力 (Enter existing key)」**ウィンドウを選択します。

    鍵の詳細を以下のように指定します。

    <table>
      <tr>
        <th>設定</th>
        <th>説明</th>
      </tr>
      <tr>
        <td>名前</td>
        <td>鍵に割り当てる、人間が理解できる固有の別名。名前は、鍵の使用目的や鍵が関連付けられているユーザーなど、鍵の識別に役立つものであればどのようなものでも構いません。</td>
      </tr>
      <tr>
        <td>鍵のタイプ</td>
        <td>{{site.data.keyword.keymanagementserviceshort}} で管理する[鍵のタイプ](/docs/services/keymgmt/keyprotect_envelope.html#key_types)。鍵のタイプのリストから、<b>「ルート鍵」</b>を選択します。</td>
      </tr>
      <tr>
        <td>鍵の素材</td>
        <td>
          <p>サービスで保管および管理する、base64 エンコードの鍵素材 (既存の鍵ラップ鍵など)。</p>
        <p>鍵の素材が以下の要件に適合していることを確認してください。</p>
        <p><ul>
            <li>鍵は 256 ビット、384 ビット、または 512 ビットでなければならない。</li>
            <li>データのバイト数 (例えば、256 ビットの場合は 32 バイト) は、base64 エンコードを使用してエンコードされていなければならない。</li>
          </ul></p>
        </td>
      </tr>
      <caption style="caption-side:bottom;">表 1. <b>「既存の鍵の入力 (Enter existing key)」</b>の設定の説明</caption>
    </table>

3. 鍵の詳細の記入が完了したら、**「新しい鍵の追加 (Add new key)」**をクリックして確認します。 

## API を使用したルート鍵のインポート
{: #import_root_key_API}

以下のエンドポイントへの `POST` 呼び出しを行うことにより、既存のルート鍵を追加します。

```
https://keyprotect.us-south.bluemix.net/api/v2/keys
```
{: codeblock}

1. [サービス内で鍵の処理を行うために、サービスおよび認証の資格情報を取得します。](/docs/services/keymgmt/keyprotect_authentication.html)

2. 以下の cURL コマンドで [{{site.data.keyword.keymanagementserviceshort}} API](https://console.ng.bluemix.net/apidocs/639) を呼び出します。

    ```cURL
    curl -X POST \
      https://keyprotect.us-south.bluemix.net/api/v2/keys \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key+json' \
      -H 'correlation-id: <correlation_ID>' \
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
       "payload": "<key_material>",
       "extractable": false
       }
     ]
    }'
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
        <td>{{site.data.keyword.keymanagementserviceshort}} サービス・インスタンスに割り当てられた固有 ID。</td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>トランザクションを追跡し、相互に関連付けるために使用される固有 ID。</td>
      </tr>
      <tr>
        <td><em>key_alias</em></td>
        <td>鍵を簡単に識別するための、人間が理解できる固有の名前。</td>
      </tr>
      <tr>
        <td><em>key_description</em></td>
        <td>鍵の詳しい説明。</td>
      </tr>
      <tr>
        <td><em>YYYY-MM-DD</em><br><em>HH:MM:SS.SS</em></td>
        <td>オプション: システム内の鍵の有効期限が切れる日時 (RFC 3339 形式)。 <code>expirationDate</code> 属性を省略した場合、鍵の有効期限は切れません。</td>
      </tr>
      <tr>
        <td><em>key_material</em></td>
        <td>
          <p>サービスで保管および管理する、base64 エンコードの鍵素材 (既存の鍵ラップ鍵など)。</p>
        <p>鍵の素材が、以下の要件に適合していることを確認してください。</p>
        <p><ul>
            <li>鍵は 256 ビット、384 ビット、または 512 ビットでなければならない。</li>
            <li>データのバイト数 (例えば、256 ビットの場合は 32 バイト) は、base64 エンコードを使用してエンコードされていなければならない。</li>
          </ul></p>
        </td>
      </tr>
      <tr>
        <td><em>key_type</em></td>
        <td>
          <p>鍵の素材をサービスの外に出すことができるかどうかを決定するブール値。</p>
          <p><code>extractable</code> 属性を <code>false</code> に設定すると、サービスはその鍵を、<code>wrap</code> または <code>unwrap</code> の操作に使用できるルート鍵として指定します。</p>
        </td>
      </tr>
        <caption style="caption-side:bottom;">表 1. {{site.data.keyword.keymanagementserviceshort}} API を使用してルート鍵を追加するために必要な変数</caption>
    </table>

    正常な `POST /v2/keys/` 応答では、鍵の ID 値を、他のメタデータと共に返します。 この ID は、鍵に割り当てられた固有の ID で、{{site.data.keyword.keymanagementserviceshort}} API に対する以降の呼び出しに使用されます。

3. オプション: 次の呼び出しを実行して {{site.data.keyword.keymanagementserviceshort}} サービス・インスタンス内の鍵を表示し、鍵が追加されたことを確認します。

    ```cURL
    curl -X GET \
      https://keyprotect.us-south.bluemix.net/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

**注:** 既存のルート鍵をサービスに追加すると、鍵は {{site.data.keyword.keymanagementserviceshort}} の境界内にとどまり、その鍵の素材を取り出すことはできません。 

### 次に行うこと

- エンベロープ暗号化を使用した鍵の保護について詳しくは、[鍵のラッピング](/docs/services/keymgmt/keyprotect_wrap_keys.html)を確認してください。
- プログラムでの鍵の管理について詳しくは、[{{site.data.keyword.keymanagementserviceshort}} API リファレンス資料に記載されているコード・サンプル ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/apidocs/639){: new_window} を確認してください。
