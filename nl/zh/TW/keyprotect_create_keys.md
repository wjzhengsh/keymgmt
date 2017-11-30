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

# 建立金鑰

您可以使用 {{site.data.keyword.keymanagementservicefull}} 來管理金鑰的生命週期。
{: shortdesc}

有一項不錯的作法是在您開發程式碼時安全地管理您的金鑰。例如，思考下列準則，以及其他安全編碼作法。

- 將金鑰嵌入您的程式碼時請考量安全問題。
- 只在對您的應用程式及資源進行程式化存取時才建立金鑰。不要在可以授與更簡單的[使用者許可權 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.bluemix.net/docs/admin/patterns.html#userroles){: new_window} 時建立金鑰。
- 輪換金鑰並移除未用的金鑰。
- 對機密作業使用多因子鑑別。
- 使每一個應用程式具有各自金鑰，隔離應用程式。
- 考量在傳送高度機密性資訊時使用程式化 API。

如果您想要在新增自己的金鑰之前先試用服務，請試用[範例應用程式 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}。

## 使用 GUI 建立金鑰
{: #gui}

若要使用 {{site.data.keyword.keymanagementserviceshort}} GUI 新增金鑰至您的服務，請參閱[開始使用 {{site.data.keyword.keymanagementserviceshort}}](/docs/services/keymgmt/index.html#addkey)。

## 使用 API 建立金鑰
{: #api}

您可以使用 {{site.data.keyword.keymanagementserviceshort}} API，以程式設計方式保護現有金鑰的安全或產生新金鑰。

對下列端點進行 `POST` 呼叫來建立金鑰或匯入現有金鑰：

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys
```
{: codeblock}

1. [擷取您的授權記號、組織 GUID 及空間 GUID 以在服務中使用金鑰](/docs/services/keymgmt/keyprotect_authentication.html)。

2. 使用下列 cURL 指令，呼叫 [{{site.data.keyword.keymanagementserviceshort}}API](https://console.ng.bluemix.net/apidocs/639)。

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
        <td>用來追蹤及關聯交易的唯一 ID。</td>
      </tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p>變更 <code>POST</code> 及 <code>DELETE</code> 行為之伺服器行為的標頭。</p><p>如果設為 <code>return=minimal</code>，服務在回應實體內文中只會傳回金鑰 meta 資料（例如金鑰名稱和 <code>id</code> 值）。如果設為 <code>return=representation</code>，服務會傳回金鑰資料和金鑰 meta 資料。</p></td>
      </tr>
      <tr>
        <td><em>key_alias</em></td>
        <td>方便識別金鑰且人類可讀的名稱。</td>
      </tr>
      <tr>
        <td><em>key_description</em></td>
        <td>金鑰的延伸說明。</td>
      </tr>
      <tr>
        <td><em>YYYY-MM-DD</em><br><em>HH:MM:SS.SS</em></td>
        <td>選用項目：系統中金鑰到期的日期和時間，以 RFC 3339 格式表示。如果省略 <code>expirationDate</code> 屬性，則金鑰不會到期。</td>
      </tr>
      <tr>
        <td><em>key_material</em></td>
        <td>您想要儲存在 {{site.data.keyword.keymanagementserviceshort}} 的金鑰資料，例如 RSA 金鑰。若要產生新的金鑰，請省略 <code>payload</code> 屬性及 <em>key_material</em> 變數。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. 透過 {{site.data.keyword.keymanagementserviceshort}} API 新增金鑰所需的變數</caption>
    </table>

    成功回應會傳回您金鑰的 `id` 值，以及其他 meta 資料。`id` 是指派給您的金鑰的唯一 ID，並用於後續的呼叫。

3. **選用項目：**藉由執行下列呼叫取得 {{site.data.keyword.cloud_notm}} 空間中的金鑰，確認已建立金鑰。

    ```cURL
    curl -X GET \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <OAuth-token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
    ```
    {: codeblock}

### 下一步為何？

現在，您可以使用金鑰來編碼應用程式及服務。

- 如需每一個 REST 要求和回應的完整資料，請參閱 {{site.data.keyword.keymanagementserviceshort}} [REST API 參考資料文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/apidocs/639){: new_window}。
