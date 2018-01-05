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

# 鍵のラッピング
{: #wrapping-keys}

特権ユーザーの場合、{{site.data.keyword.keymanagementservicelong}} API を使用して、ルート鍵を使って暗号鍵を管理および保護することができます。
{: shortdesc}

ルート鍵を使用してデータ暗号鍵 (DEK) をラップすると、{{site.data.keyword.keymanagementserviceshort}} は複数のアルゴリズムの長所を組み合わせて、暗号化データのプライバシーおよび保全性を保護します。  

鍵ラッピングが、クラウド内の保存データのセキュリティー管理にどのように役立つかについては、[エンベロープ暗号化](/docs/services/keymgmt/keyprotect_envelope.html)を参照してください。

## API を使用した鍵のラッピング
{: #api}

{{site.data.keyword.keymanagementserviceshort}} 内で管理するルート鍵を使用して、指定されたデータ暗号化鍵 (DEK) を保護することができます。

**重要:** ラッピングのためにルート鍵を提供する場合、ラップ呼び出しが成功できるように、ルート鍵が 256 ビット、384 ビット、または 512 ビットであることを確認してください。サービス内にルート鍵を作成すると、{{site.data.keyword.keymanagementserviceshort}} は、AES-GCM アルゴリズムによってサポートされている HSM から 256 ビット鍵を生成します。

[サービス内でルート鍵を指定した後](/docs/services/keymgmt/keyprotect_create_keys.html)、以下のエンドポイントへの `POST` 呼び出しを行うことにより、拡張暗号化を使用して DEK をラップできます。

```
https://keyprotect.us-south.bluemix.net/api/v2/keys<key_ID>?action=wrap
```
{: codeblock}

1. [サービス内で鍵の処理を行うために、サービスおよび認証の資格情報を取得します。](/docs/services/keymgmt/keyprotect_authentication.html)

2. 管理および保護する DEK の鍵の素材をコピーします。

    {{site.data.keyword.keymanagementserviceshort}} サービス・インスタンスの管理者または編集者の特権を持っている場合、[`GET /v2/keys/<key_ID>` 要求を行うことで、特定の鍵の鍵素材を取得できます](/docs/services/keymgmt/keyprotect_view_keys.md#retrieve_key_api)。

3. ラッピングに使用するルート鍵の ID をコピーします。

4. 以下の cURL コマンドを実行し、ラップ操作を使用して鍵を保護します。

    ```cURL
    curl -X POST \
      'https://keyprotect.us-south.bluemix.net/api/v2/keys<key_ID>?action=wrap' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
      "plaintext": "<data_key>",
      "aad": ["<additional_data>", "<additional_data>"]
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
        <td><em>key_ID</em></td>
        <td>ラッピングに使用するルート鍵の固有 ID。ラップ呼び出しが成功するように、ルート鍵は 256 ビット、384 ビット、または 512 ビットでなければなりません。</td>
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
        <td><em>correlation_ID</em></td>
        <td>オプション: トランザクションを追跡し、相互に関連付けるために使用される固有 ID。</td>
      </tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p><code>POST</code> および <code>DELETE</code> の操作に関するサーバーの動作を変更するヘッダー。</p><p><em>return_preference</em> 変数を <code>return=minimal</code> に設定すると、サービスは鍵のメタデータ (鍵の名前や ID 値など) のみを応答のエンティティー本体で返します。変数を <code>return=representation</code> に設定すると、サービスは鍵の素材と鍵のメタデータの両方を返します。</p></td>
      </tr>
      <tr>
        <td><em>data_key</em></td>
        <td>オプション: 管理および保護する DEK の鍵の素材。<code>plaintext</code> 値は、base64 エンコードでなければなりません。新しい DEK を生成するには、<code>plaintext</code> 属性を省略します。サービスは、ランダム・プレーン・テキスト (32 バイト) を生成し、その値をラップします。</td>
      </tr>
      <tr>
        <td><em>additional_data</em></td>
        <td>オプション: 鍵をさらにセキュアにするために使用される追加認証データ (AAD)。各ストリングは、最大 255 文字を保持できます。サービスに対してラップ呼び出を行ったときに AAD を提供した場合は、後続のアンラップ呼び出し時にも同じ AAD を指定する必要があります。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. {{site.data.keyword.keymanagementserviceshort}} で指定の鍵をラップするために必要な変数についての説明</caption>
    </table>

    ラップされた鍵 (base64 エンコードの鍵素材を含む) が、応答のエンティティー本体で返されます。以下の JSON オブジェクトは、返された値の例を示しています。

    ```
    {
      "plaintext": "s~Rz@kN9Fzv\\/hP*r3LY-?O@!!qdtj:L",
      "ciphertext": "eyJjaXBoZXJ0ZXh0Ijoic3VLSDNRcmdEZjdOZUw4Rkc4L2FKYjFPTWcyd3A2eDFvZlA4MEc0Z1B2RmNrV2g3cUlidHphYXU0eHpKWWoxZyIsImhhc2giOiJiMmUyODdkZDBhZTAwZGZlY2Q3OGJmMDUxYmNmZGEyNWJkNGUzMjBkYjBhN2FjNzVhMWYzZmNkMDZlMjAzZWYxNWM5MTY4N2JhODg2ZWRjZGE2YWVlMzFjYzk2MjNkNjA5YTRkZWNkN2E5Y2U3ZDc5ZTRhZGY1MWUyNWFhYWM5MjhhNzg3NmZjYjM2NDFjNTQzMTZjMjMwOGY2MThlZGM2OTE3MjAyYjA5YTdjMjA2YzkxNTBhOTk1NmUxYzcxMTZhYjZmNmQyYTQ4MzZiZTM0NTk0Y2IwNzJmY2RmYTk2ZSJ9"
      "aad": ["data1", "data2"]
    }
    ```
    {:screen}
