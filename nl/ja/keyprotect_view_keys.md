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

# 鍵の表示
{: #viewing-keys}

{{site.data.keyword.keymanagementservicefull}} により、
暗号鍵を表示、管理、監査する集中システムが提供されます。 鍵と鍵へのアクセス制限を監査して、リソースのセキュリティーを確保します。
{: shortdesc}

定期的に鍵の構成を監査するために、以下を行います。

- いつ鍵が作成されたかを調べ、鍵を回転する時期かどうかを判断します。
- [{{site.data.keyword.cloudaccesstrailshort}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン") を使用して、{{site.data.keyword.keymanagementserviceshort}} への API 呼び出しをモニターします](/docs/services/cloud-activity-tracker/svcs/kp_at.html#kp_at){: new_window}。
- どのユーザーが鍵へのアクセス権限を持っているか、アクセス権限のレベルは適切かどうかを検査します。

リソースへのアクセス権限の監査について詳しくは、[Cloud IAM を使用したユーザーのアクセス権限の管理](/docs/services/keymgmt/keyprotect_manage_access.html)を参照してください。

## GUI を使用した鍵の表示
{: #gui}

グラフィカル・インターフェースを使用してサービス内の鍵を検査したい場合は、{{site.data.keyword.keymanagementserviceshort}} ダッシュボードを使用できます。

[サービス内に鍵を作成するか、既存の鍵をインポートした後](/docs/services/keymgmt/keyprotect_create_keys.html)、以下の手順を実行して、鍵を表示します。

1. [{{site.data.keyword.cloud_notm}} コンソール ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.bluemix.net/) にログインします。
2. {{site.data.keyword.cloud_notm}} ダッシュボードで、{{site.data.keyword.keymanagementserviceshort}} のプロビジョン済みインスタンスを選択します。
3. {{site.data.keyword.keymanagementserviceshort}} ダッシュボードで、以下のような鍵の一般的な特性を参照します。

    <table>
      <tr>
        <th>列</th>
        <th>説明</th>
      </tr>
      <tr>
        <td>名前</td>
        <td>鍵に割り当てられた、人間が理解できる固有の別名。</td>
      </tr>
      <tr>
        <td>ID</td>
        <td>{{site.data.keyword.keymanagementserviceshort}} サービスによって鍵に割り当てられた固有の鍵 ID。この ID 値を使用して、[{{site.data.keyword.keymanagementserviceshort}} API](https://console.ng.bluemix.net/apidocs/639) でサービスを呼び出すことができます。</td>
      </tr>
      <tr>
        <td>状態</td>
        <td>[NIST Special Publication 800-57, Recommendation for Key Management ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf) に基づく[鍵の状態](/docs/services/keymgmt/keyprotect_states.html)。状態には、<i>アクティブ化前</i>、<i>アクティブ</i>、<i>非アクティブ化</i>、および <i>破棄</i> があります。</td>
      </tr>
      <tr>
        <td>タイプ</td>
        <td>サービス内の鍵の指定された目的を説明する、[鍵のタイプ](/docs/services/keymgmt/keyprotect_envelope.html#key_types)。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. <b>「鍵 (Keys)」</b>テーブルの説明</caption>
    </table>

## API を使用した鍵の表示
{: #api}

{{site.data.keyword.keymanagementserviceshort}} API を使用して、鍵の内容を取得できます。

### ステップ 1: 鍵の集合の取得
{: #retrieve_keys_api}

概要を参照するために、次のエンドポイントへの `GET` 呼び出しを行って、{{site.data.keyword.keymanagementserviceshort}} のプロビジョン済みインスタンスで管理されている鍵を表示できます。

```
https://key-protect.us-south.bluemix.net/api/v2/keys
```
{: codeblock}

1. [サービス内で鍵の処理を行うために、サービスおよび認証の資格情報を取得します。](/docs/services/keymgmt/keyprotect_authentication.html)
2. 次の cURL コマンドを実行して、鍵に関する一般的な特性を表示します。

    ```cURL
    curl -X GET \
    https://key-protect.us-south.bluemix.net/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <IAM_token>' \
    -H 'bluemix-instance: <instance_ID>' \
    -H 'correlation-id: <correlation_ID>' \
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
        <td><em>correlation_ID</em></td>
        <td>オプション: トランザクションを追跡し、相互に関連付けるために使用される固有 ID。</td>
      </tr>
      <caption style="caption-side:bottom;">表 2. {{site.data.keyword.keymanagementserviceshort}} API を使用して鍵を表示するために必要な変数についての説明</caption>
    </table>

    `POST /v2/keys/` 要求に成功すると、{{site.data.keyword.keymanagementserviceshort}} サービス・インスタンス内の使用可能な鍵の集合が返されます。

    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.collection+json",
        "collectionTotal": 2
      },
    "resources": [
      {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Standard key",
          "description": "...",
          "state": 1,
          "crn": "...",
          "algorithmType": "AES",
          "createdBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "256",
            "mode": "GCM"
          },
          "extractable": true
        },
        {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Root key",
          "description": "...",
          "state": 1,
          "crn": "...",
          "algorithmType": "AES",
          "createdBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "256",
            "mode": "GCM"
          },
          "extractable": false
        }
      ]
    }
    ```
    {:screen}

### ステップ 2: ID による鍵の取得
{: #retrieve_key_api}

特定の鍵に関する詳細情報を表示するには、次のエンドポイントに対して後続の `GET` 呼び出しを行います。

```
https://key-protect.us-south.bluemix.net/api/v2/keys<key_ID>
```
{: codeblock}

1. [サービス内で鍵の処理を行うために、サービスおよび認証の資格情報を取得します。](/docs/services/keymgmt/keyprotect_authentication.html)
2. アクセスまたは管理する鍵の ID を取得します。

    この ID 値を使用して、鍵に関する詳細な情報 (鍵の素材自体など) にアクセスします。 `GET v2/keys` 要求を行うか、{{site.data.keyword.keymanagementserviceshort}} GUI にアクセスすることで、指定した鍵の ID を取得できます。

3. 次の cURL コマンドを実行して、鍵と鍵の素材に関する詳細を取得します。

    ```cURL
    curl -X GET \
      https://key-protect.us-south.bluemix.net/api/v2/keys<key_ID> \
      -H 'accept: application/vnd.ibm.kms.key+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

    次の表に従って、例の要求内の変数を置き換えてください。

    <table>
      <tr>
        <th>変数</th>
        <th>説明</th>
      </tr>
      <tr>
        <td><em>IAM_token</em></td>
        <td>許可トークン。 Bearer 値を含む、`IAM` トークンの全コンテンツを cURL 要求に組み込みます。</td>
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
        <td><em>key_ID</em></td>
        <td>[ステップ 1](#retrieve_keys_api) で取得した鍵の ID。</td>
      </tr>
      <caption style="caption-side:bottom;">表 3. {{site.data.keyword.keymanagementserviceshort}} API を使用して指定の鍵を表示するために必要な変数についての説明</caption>
    </table>

    正常な `GET v2/keys/<key_ID>` 応答は、鍵と鍵の素材に関する詳細を返します。 以下の JSON オブジェクトは、標準鍵の戻り値の例を示しています。

    ```
    {
        "metadata": {
            "collectionTotal": 1,
            "collectionType": "application/vnd.ibm.kms.key+json"
        },
    "resources": [
      {
            "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Standard key",
          "description": "...",
          "state": 1,
          "crn": "...",
            "algorithmType": "AES",
            "payload": "...",
            "createdBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
                "bitLength": "256",
            "mode": "GCM"
            },
            "extractable": true
        }
      ]
    }
    ```
    {:screen}

    使用可能なパラメーターについて詳しくは、{{site.data.keyword.keymanagementserviceshort}} [REST API リファレンス資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/apidocs/639){: new_window} を参照してください。
