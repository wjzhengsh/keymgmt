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

# 鍵の表示

{{site.data.keyword.keymanagementservicefull}} を使用して、暗号鍵の内容を表示できます。
{: shortdesc}

## GUI を使用した鍵の表示
{: #gui}

{{site.data.keyword.keymanagementserviceshort}} GUI を使用してサービスの鍵を表示するには、[{{site.data.keyword.keymanagementserviceshort}} の概説](/docs/services/keymgmt/index.html#managekey)を参照してください。

## API を使用した鍵の表示
{: #api}

{{site.data.keyword.keymanagementserviceshort}} API を使用して、鍵の内容を取得できます。

### ステップ 1: 鍵の集合の取得
{: #retrieve_keys_api}

概略を参照するために、次のエンドポイントへの `GET` 呼び出しを行って、スペースで管理されている鍵を表示できます。

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys
```
{: codeblock}

1. [サービスで鍵を処理するために、許可トークン、組織 GUID、およびスペース GUID を取得します](/docs/services/keymgmt/keyprotect_authentication.html)。
2. 次の cURL コマンドを実行して、鍵に関する一般的な特性を表示します。

    ```cURL
    curl -X GET \
    https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <OAuth_token>' \
    -H 'bluemix-org: <organization_GUID>' \
    -H 'bluemix-space: <space_GUID>' \
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
        <td><em>space_GUID</em></td>
        <td>{{site.data.keyword.Bluemix_notm}} スペースに割り当てられた固有 ID。</td>
      </tr>
      <tr>
        <td><em>organization_GUID</em></td>
        <td>{{site.data.keyword.Bluemix_notm}} 組織に割り当てられた固有 ID。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. {{site.data.keyword.keymanagementserviceshort}} API を使用して鍵を表示するために必要な変数についての説明</caption>
    </table>

    要求に成功すると、{{site.data.keyword.Bluemix_notm}} スペース内の使用可能な鍵の集合が返されます。

    ```
    {
      "metadata": {
"collectionType": "application/vnd.ibm.kms.key+json",
        "collectionTotal": 2
      },
    "resources": [
      {
      "id": "Key ID 1",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Key alias",
          "description": "Key description",
          "state": 1,
          "algorithmType": "AES",
          "createdBy": "v4 UUID of the user who creates the key",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "Key length",
            "mode": "GCM"
          }
        },
        {
          "id": "Key ID 2",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Key alias",
          "description": "Key description",
          "state": 1,
          "algorithmType": "AES",
          "createdBy": "v4 UUID of the user who creates the key",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "Key length",
            "mode": "GCM"
          }
        }
      ]
    }
    ```
    {:screen}

### ステップ 2: ID による鍵の取得
{: #retrieve_key_api}

特定の鍵に関する詳細情報を表示するには、次のエンドポイントに対して後続の `GET` 呼び出しを行います。

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID>
```
{: codeblock}

1. [サービスで鍵を処理するために、許可トークン、組織 GUID、およびスペース GUID を取得します](/docs/services/keymgmt/keyprotect_authentication.html)。
2. アクセスまたは管理する鍵の ID を取得します。

    この ID 値を使用して、鍵に関する詳細な情報 (鍵の素材自体など) にアクセスします。`GET v2/keys` 要求を行うか、{{site.data.keyword.keymanagementserviceshort}} GUI にアクセスすることで、指定した鍵の ID を取得できます。

3. 次の cURL コマンドを実行して、鍵と鍵の素材に関する詳細を取得します。

    ```cURL
    curl -X GET \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID> \
      -H 'accept: application/vnd.ibm.kms.secret+json' \
      -H 'authorization: Bearer <OAuth_token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
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
        <td><em>OAuth_token</em></td>
        <td>許可トークン。Bearer 値を含む、トークンの全コンテンツを cURL 要求に組み込みます。</td>
      </tr>
      <tr>
        <td><em>organization_GUID</em></td>
        <td>{{site.data.keyword.Bluemix_notm}} 組織に割り当てられた固有 ID。</td>
      </tr>
      <tr>
        <td><em>space_GUID</em></td>
        <td>{{site.data.keyword.Bluemix_notm}} スペースに割り当てられた固有 ID。</td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>オプション: トランザクションを追跡し、相互に関連付けるために使用される固有 ID。</td>
      </tr>
      <tr>
        <td><em>key_ID</em></td>
        <td>[ステップ 1](#retrieve_keys_api) で取得した鍵の ID。</td>
      </tr>
      <caption style="caption-side:bottom;">表 2. {{site.data.keyword.keymanagementserviceshort}} API を使用して指定の鍵を表示するために必要な変数についての説明</caption>
    </table>

    正常な応答は、鍵と鍵の素材に関する詳細を返します。以下の JSON オブジェクトは、返された値の例を示しています。

    ```
    {
        "metadata": {
"collectionTotal": 1,
            "collectionType": "application/vnd.ibm.kms.key+json"
        },
    "resources": [
      {
      "createdBy": "...",
                "creationDate": "...",
        "id":"...",
        "name":"...",
                "payload": "...",
                "state": 1,
                "type": "application/vnd.ibm.kms.key+json"
            }
        ]
    }
    ```
    {:screen}

    使用可能なパラメーターについて詳しくは、{{site.data.keyword.keymanagementserviceshort}} [REST API リファレンス資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/apidocs/639){: new_window} を参照してください。
