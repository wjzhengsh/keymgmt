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

# 鍵のアンラッピング
{: #unwrapping-keys}

特権ユーザーの場合、{{site.data.keyword.keymanagementservicefull}} API を使用して、データ暗号化鍵 (DEK) をアンラップして、内容にアクセスすることができます。DEK をアンラップすると、暗号化解除して内容の保全性を確認し、元の鍵素材を {{site.data.keyword.cloud_notm}} データ・サービスに返します。
{: shortdesc}

鍵ラッピングが、クラウド内の保存データのセキュリティー管理にどのように役立つかについては、[エンベロープ暗号化](/docs/services/keymgmt/keyprotect_envelope.html)を参照してください。

## API を使用した鍵のアンラッピング
{: #api}

[サービスに対してラップ呼び出しを行った後](/docs/services/keymgmt/keyprotect_wrap_keys.html)、以下のエンドポイントへの `POST` 呼び出しを行うことにより、指定のデータ暗号化鍵 (DEK) をアンラップして、その内容にアクセスできます。

```
https://keyprotect.us-south.bluemix.net/api/v2/keys<key_id>?action=unwrap
```
{: codeblock}

1. [サービス内で鍵の処理を行うために、サービスおよび認証の資格情報を取得します。](/docs/services/keymgmt/keyprotect_authentication.html)

2. 最初のラップ要求を実行するために使用したルート鍵の ID をコピーします。

    `GET /v2/keys/` 要求を行うか、{{site.data.keyword.keymanagementserviceshort}} GUI に鍵を表示することで、鍵の ID を取得できます。

3. 最初のラップ要求時に返された `ciphertext` 値をコピーします。

4. 次の cURL コマンドを実行して、鍵の素材を暗号化解除して認証します。

    ```cURL
    curl -X POST \
      'https://keyprotect.us-south.bluemix.net/api/v2/keys<key_ID>?action=unwrap' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
      "ciphertext": "<encrypted_data_key>",
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
        <td>ラッピングに使用したルート鍵の固有 ID。アンラップ要求が成功するように、最初のラップ要求時に使用したのと同じルート鍵を指定します。</td>
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
        <td><em>additional_data</em></td>
        <td>オプション: 鍵をさらにセキュアにするために使用される追加認証データ (AAD)。各ストリングは、最大 255 文字を保持できます。<br></br>サービスに対してラップ呼び出を行ったときに AAD を提供した場合、アンラップ呼び出し時にも同じ AAD を指定する必要があります。</td>
      </tr>
      <tr>
        <td><em>encrypted_data_key</em></td>
        <td>ラップ操作時に返された <code>ciphertext</code> 値。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. {{site.data.keyword.keymanagementserviceshort}} で鍵をアンラップするために必要な変数についての説明</caption>
    </table>

    元の鍵の素材が、応答のエンティティー本体で返されます。以下の JSON オブジェクトは、返された値の例を示しています。

    ```
    {
      "plaintext": "s~Rz@kN9Fzv\\/hP*r3LY-?O@!!qdtj:L"
    }
    ```
    {:screen}
