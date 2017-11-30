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

# 檢視金鑰

您可以使用 {{site.data.keyword.keymanagementservicefull}} 檢視加密金鑰的內容。
{: shortdesc}

## 使用 GUI 檢視金鑰
{: #gui}

若要使用 {{site.data.keyword.keymanagementserviceshort}} GUI 瀏覽服務中的金鑰，請參閱[開始使用 {{site.data.keyword.keymanagementserviceshort}}](/docs/services/keymgmt/index.html#managekey)。

## 使用 API 檢視金鑰
{: #api}

您可以使用 {{site.data.keyword.keymanagementserviceshort}} API 擷取金鑰的內容。

### 步驟 1：擷取金鑰集合
{: #retrieve_keys_api}

如需高階視圖，您可以對下列端點進行 `GET` 呼叫，以瀏覽空間中管理的金鑰。

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys
```
{: codeblock}

1. [擷取您的授權記號、組織 GUID 及空間 GUID 以在服務中使用金鑰](/docs/services/keymgmt/keyprotect_authentication.html)。
2. 執行下列 cURL 指令，以檢視金鑰的一般性質。

    ```cURL
    curl -X GET \
    https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <OAuth_token>' \
    -H 'bluemix-org: <organization_GUID>' \
    -H 'bluemix-space: <space_GUID>' \
    ```
    {: codeblock}

    根據下表取代範例要求中的變數。<table>
      <tr>
        <th>變數</th>
        <th>說明</th>
      </tr>
      <tr>
        <td><em>OAuth_token</em></td>
        <td>您的授權記號。請在 cURL 要求包含記號的完整內容，包括 Bearer 值。</td>
      </tr>
      <tr>
        <td><em>space_GUID</em></td>
        <td>指派給您的 {{site.data.keyword.cloud_notm}} 空間的唯一 ID。</td>
      </tr>
      <tr>
        <td><em>organization_GUID</em></td>
        <td>指派給您的 {{site.data.keyword.cloud_notm}} 組織的唯一 ID。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. 說明透過 {{site.data.keyword.keymanagementserviceshort}} API 檢視金鑰所需的變數。</caption>
    </table>

    成功要求會傳回您的 {{site.data.keyword.cloud_notm}} 空間中可用的金鑰集合。

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

### 步驟 2：依 ID 擷取金鑰
{: #retrieve_key_api}

若要檢視特定金鑰的詳細資訊，後續可以對下列端點進行 `GET` 呼叫：

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID>
```
{: codeblock}

1. [擷取您的授權記號、組織 GUID 及空間 GUID 以在服務中使用金鑰](/docs/services/keymgmt/keyprotect_authentication.html)。
2. 擷取您想要存取或管理之金鑰的 ID。

    ID 值是用來存取金鑰的詳細資訊，例如金鑰資料本身。您可以擷取指定金鑰的 ID，方法是提出 `GET v2/keys` 要求，或存取 {{site.data.keyword.keymanagementserviceshort}} GUI。

3. 執行下列 cURL 指令，以取得金鑰的詳細資料及金鑰資料。

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

    根據下表取代範例要求中的變數。

    <table>
      <tr>
        <th>變數</th>
        <th>說明</th>
      </tr>
      <tr>
        <td><em>OAuth_token</em></td>
        <td>您的授權記號。請在 cURL 要求包含記號的完整內容，包括 Bearer 值。</td>
      </tr>
      <tr>
        <td><em>organization_GUID</em></td>
        <td>指派給您的 {{site.data.keyword.cloud_notm}} 組織的唯一 ID。</td>
      </tr>
      <tr>
        <td><em>space_GUID</em></td>
        <td>指派給您的 {{site.data.keyword.cloud_notm}} 空間的唯一 ID。</td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>選用項目：用來追蹤及關聯交易的唯一 ID。</td>
      </tr>
      <tr>
        <td><em>key_ID</em></td>
        <td>您在[步驟 1](#retrieve_keys_api) 中擷取之金鑰的 ID。</td>
      </tr>
      <caption style="caption-side:bottom;">表 2. 說明透過 {{site.data.keyword.keymanagementserviceshort}} API 檢視指定金鑰所需的變數。</caption>
    </table>

    成功回應會傳回金鑰的詳細資料及金鑰資料。下列 JSON 物件顯示傳回值的範例。

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
                "id": "...",
                "name": "...",
                "payload": "...",
                "state": 1,
                "type": "application/vnd.ibm.kms.key+json"
            }
        ]
    }
    ```
    {:screen}

    如需可用參數的詳細說明，請參閱 {{site.data.keyword.keymanagementserviceshort}} [REST API 參考資料文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/apidocs/639){: new_window}。
