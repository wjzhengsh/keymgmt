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

# 檢視金鑰
{: #viewing-keys}

{{site.data.keyword.keymanagementservicefull}} 提供集中化的系統，以便檢視、管理及審核您的加密金鑰。請審核您的金鑰及對於金鑰的存取權限制，以確保資源安全。
{: shortdesc}

定期審核您的金鑰配置：

- 檢查金鑰的建立時間，並決定是否應該輪替金鑰。
- [使用 {{site.data.keyword.cloudaccesstrailshort}} 監視 {{site.data.keyword.keymanagementserviceshort}} 的 API 呼叫 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/cloud-activity-tracker/svcs/kp_at.html#kp_at){: new_window}。
- 檢查哪些使用者可以存取金鑰，以及存取層次是否適當。

如需審核資源存取權的相關資訊，請參閱[使用 Cloud IAM 管理使用者存取](/docs/services/keymgmt/keyprotect_manage_access.html)。

## 使用 GUI 檢視金鑰
{: #gui}

如果您偏好使用圖形介面來檢查服務中的金鑰，則可以使用 {{site.data.keyword.keymanagementserviceshort}} 儀表板。

[在建立金鑰或將現有金鑰匯入到服務之後](/docs/services/keymgmt/keyprotect_create_keys.html)，請完成下列步驟來檢視金鑰。

1. [登入 {{site.data.keyword.cloud_notm}} 主控台 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.bluemix.net/)。
2. 從 {{site.data.keyword.cloud_notm}} 儀表板，選取已佈建的 {{site.data.keyword.keymanagementserviceshort}} 實例。
3. 從 {{site.data.keyword.keymanagementserviceshort}} 儀表板，瀏覽金鑰的一般特徵：

    <table>
      <tr>
        <th>直欄</th>
        <th>說明</th>
      </tr>
      <tr>
        <td>名稱</td>
        <td>已指派給您的金鑰且人類可閱讀的唯一別名。</td>
      </tr>
      <tr>
        <td>ID</td>
        <td>{{site.data.keyword.keymanagementserviceshort}} 服務已指派給您金鑰的唯一金鑰 ID。您可以使用 ID 值，利用 [{{site.data.keyword.keymanagementserviceshort}} API](https://console.ng.bluemix.net/apidocs/639) 來呼叫服務。</td>
      </tr>
      <tr>
        <td>狀態</td>
        <td>根據 [NIST 特殊出版品 800-57 的金鑰管理建議 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf) 的[金鑰狀態](/docs/services/keymgmt/keyprotect_states.html)。這些狀態包括<i>啟動前</i>、<i>作用中</i>、<i>取消啟動</i> 及<i>已破壞</i>。</td>
      </tr>
      <tr>
        <td>類型</td>
        <td>說明服務內金鑰指定用途的[金鑰類型](/docs/services/keymgmt/keyprotect_envelope.html#key_types)。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. <b>金鑰</b>表格的說明</caption>
    </table>

## 使用 API 檢視金鑰
{: #api}

您可以使用 {{site.data.keyword.keymanagementserviceshort}} API 擷取金鑰的內容。

### 步驟 1：擷取金鑰集合
{: #retrieve_keys_api}

如需高階視圖，您可以對下列端點發出 `GET` 呼叫，來瀏覽已佈建之 {{site.data.keyword.keymanagementserviceshort}} 實例中管理的金鑰：

```
https://key-protect.us-south.bluemix.net/api/v2/keys
```
{: codeblock}

1. [擷取服務及鑑別認證以在服務中使用金鑰](/docs/services/keymgmt/keyprotect_authentication.html)。
2. 執行下列 cURL 指令，以檢視金鑰的一般特徵。

    ```cURL
    curl -X GET \
    https://key-protect.us-south.bluemix.net/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <IAM_token>' \
    -H 'bluemix-instance: <instance_ID>' \
    -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

    若要在您帳戶的指定 Cloud Foundry 組織及空間內使用金鑰，請將 `Bluemix-Instance` 取代為適當的 `Bluemix-org` 及 `Bluemix-space` 標頭。[請參閱 {{site.data.keyword.keymanagementserviceshort}} API 參考資料文件以取得程式碼範例 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/apidocs/639){: new_window}。
    {: tip}

    根據下表取代範例要求中的變數。
    <table>
      <tr>
        <th>變數</th>
        <th>說明</th>
      </tr>
      <tr>
        <td><em>IAM_token</em></td>
        <td>您的授權記號。請在 cURL 要求中包含 <code>IAM</code> 記號的完整內容，包括 Bearer 值。</td>
      </tr>
      <tr>
        <td><em>instance_ID</em></td>
        <td>指派給您的 {{site.data.keyword.keymanagementserviceshort}} 服務實例的唯一 ID。</td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>選用項目：用來追蹤及關聯交易的唯一 ID。</td>
      </tr>
      <caption style="caption-side:bottom;">表 2. 說明使用 {{site.data.keyword.keymanagementserviceshort}} API 檢視金鑰所需的變數。</caption>
    </table>

    成功的 `POST /v2/keys/` 要求會傳回您的 {{site.data.keyword.keymanagementserviceshort}} 服務實例中可用的金鑰集合。

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

### 步驟 2：依 ID 擷取金鑰
{: #retrieve_key_api}

若要檢視特定金鑰的詳細資訊，後續可以對下列端點發出 `GET` 呼叫：

```
https://key-protect.us-south.bluemix.net/api/v2/keys<key_ID>
```
{: codeblock}

1. [擷取服務及鑑別認證以在服務中使用金鑰](/docs/services/keymgmt/keyprotect_authentication.html)。
2. 擷取您想要存取或管理之金鑰的 ID。

    ID 值是用來存取金鑰的詳細資訊，例如金鑰資料本身。您可以擷取指定金鑰的 ID，方法是提出 `GET v2/keys` 要求，或存取 {{site.data.keyword.keymanagementserviceshort}} GUI。

3. 執行下列 cURL 指令，以取得金鑰的詳細資料及金鑰資料。

    ```cURL
    curl -X GET \
      https://key-protect.us-south.bluemix.net/api/v2/keys<key_ID> \
      -H 'accept: application/vnd.ibm.kms.key+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
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
        <td><em>IAM_token</em></td>
        <td>您的授權記號。請在 cURL 要求中包含 `IAM` 記號的完整內容，包括 Bearer 值。</td>
      </tr>
      <tr>
        <td><em>instance_ID</em></td>
        <td>指派給您的 {{site.data.keyword.keymanagementserviceshort}} 服務實例的唯一 ID。</td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>選用項目：用來追蹤及關聯交易的唯一 ID。</td>
      </tr>
      <tr>
        <td><em>key_ID</em></td>
        <td>您在[步驟 1](#retrieve_keys_api) 中擷取之金鑰的 ID。</td>
      </tr>
      <caption style="caption-side:bottom;">表 3. 說明使用 {{site.data.keyword.keymanagementserviceshort}} API 檢視指定金鑰所需的變數。</caption>
    </table>

    成功的 `GET v2/keys/<key_ID>` 回應會傳回金鑰的詳細資料及金鑰資料。下列 JSON 物件顯示標準金鑰的回覆值範例。

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

    如需可用參數的詳細說明，請參閱 {{site.data.keyword.keymanagementserviceshort}} [REST API 參考資料文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/apidocs/639){: new_window}。
