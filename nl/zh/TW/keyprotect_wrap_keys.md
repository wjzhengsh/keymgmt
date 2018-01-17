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

# 包裝金鑰
{: #wrapping-keys}

如果您是特許使用者，則可以使用 {{site.data.keyword.keymanagementservicelong}} API，以利用主要金鑰來管理及保護加密金鑰。
{: shortdesc}

當您使用主要金鑰來包裝資料加密金鑰 (DEK) 時，{{site.data.keyword.keymanagementserviceshort}} 會結合多個演算法的長處，來保護已加密資料的隱私權及完整性。  

若要瞭解金鑰包裝如何協助您控制雲端中靜置資料的安全，請參閱[封套加密](/docs/services/keymgmt/keyprotect_envelope.html)。

## 使用 API 包裝金鑰
{: #api}

您可以使用您在 {{site.data.keyword.keymanagementserviceshort}} 中管理的主要金鑰來保護指定的資料加密金鑰 (DEK)。

**重要事項：**當您提供用於包裝的主要金鑰時，請確定主要金鑰是 256、384 或 512 位元，以讓包裝呼叫成功。如果您在服務中建立主要金鑰，則 {{site.data.keyword.keymanagementserviceshort}} 會從 AES-GCM 演算法所支援的 HSM 產生 256 位元金鑰。

[在服務中指定主要金鑰之後](/docs/services/keymgmt/keyprotect_create_keys.html)，即可對下列端點發出 `POST` 呼叫，以使用進階加密來包裝 DEK：

```
https://keyprotect.us-south.bluemix.net/api/v2/keys<key_ID>?action=wrap
```
{: codeblock}

1. [擷取服務及鑑別認證以在服務中使用金鑰](/docs/services/keymgmt/keyprotect_authentication.html)。

2. 複製您要管理及保護之 DEK 的金鑰資料。

    如果您具有 {{site.data.keyword.keymanagementserviceshort}} 服務實例的管理者或編輯者專用權，則[可以提出 `GET /v2/keys/<key_ID>` 要求來擷取特定金鑰的金鑰資料](/docs/services/keymgmt/keyprotect_view_keys.md#retrieve_key_api)。

3. 複製您要用於包裝之主要金鑰的 ID。

4. 執行下列 cURL 指令，以使用包裝作業來保護金鑰。

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

    若要在您帳戶的指定 Cloud Foundry 組織及空間內使用金鑰，請將 `Bluemix-Instance` 取代為適當的 `Bluemix-org` 及 `Bluemix-space` 標頭。[請參閱 {{site.data.keyword.keymanagementserviceshort}} API 參考資料文件以取得程式碼範例 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/apidocs/639){: new_window}。
    {: tip}

    根據下表取代範例要求中的變數。

    <table>
      <tr>
        <th>變數</th>
        <th>說明</th>
      </tr>
      <tr>
        <td><em>key_ID</em></td>
        <td>您要用於包裝之主要金鑰的唯一 ID。主要金鑰必須是 256、384 或 512 位元，以讓包裝呼叫成功。</td>
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
      <tr>
        <td><em>return_preference</em></td>
        <td><p>變更 <code>POST</code> 及 <code>DELETE</code> 行為之伺服器行為的標頭。</p><p>當您將 <em>return_preference</em> 變數設為 <code>return=minimal</code> 時，服務在回應實體內文中只會傳回金鑰 meta 資料（例如金鑰名稱及 ID 值）。當您將變數設為 <code>return=representation</code> 時，服務會傳回金鑰資料及金鑰 meta 資料。</p></td>
      </tr>
      <tr>
        <td><em>data_key</em></td>
        <td>選用項目：您要管理及保護之 DEK 的金鑰資料。<code>plaintext</code> 值必須以 base64 編碼。若要產生新的 DEK，請省略 <code>plaintext</code> 屬性。此服務會產生隨機純文字（32 個位元組），並包裝該值。</td>
      </tr>
      <tr>
        <td><em>additional_data</em></td>
        <td>選用項目：用來進一步保護金鑰的其他鑑別資料 (AAD)。每一個字串最多可以保留 255 個字元。如果您在對服務發出包裝呼叫時提供 AAD，則必須在後續解除包裝呼叫期間指定相同的 AAD。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. 說明在 {{site.data.keyword.keymanagementserviceshort}} 中包裝所指定金鑰所需的變數。</caption>
    </table>

    已包裝金鑰（包含以 base64 編碼的金鑰資料）會在回應實體內文中傳回。下列 JSON 物件顯示回覆值範例。

    ```
    {
      "plaintext": "s~Rz@kN9Fzv\\/hP*r3LY-?O@!!qdtj:L",
      "ciphertext": "eyJjaXBoZXJ0ZXh0Ijoic3VLSDNRcmdEZjdOZUw4Rkc4L2FKYjFPTWcyd3A2eDFvZlA4MEc0Z1B2RmNrV2g3cUlidHphYXU0eHpKWWoxZyIsImhhc2giOiJiMmUyODdkZDBhZTAwZGZlY2Q3OGJmMDUxYmNmZGEyNWJkNGUzMjBkYjBhN2FjNzVhMWYzZmNkMDZlMjAzZWYxNWM5MTY4N2JhODg2ZWRjZGE2YWVlMzFjYzk2MjNkNjA5YTRkZWNkN2E5Y2U3ZDc5ZTRhZGY1MWUyNWFhYWM5MjhhNzg3NmZjYjM2NDFjNTQzMTZjMjMwOGY2MThlZGM2OTE3MjAyYjA5YTdjMjA2YzkxNTBhOTk1NmUxYzcxMTZhYjZmNmQyYTQ4MzZiZTM0NTk0Y2IwNzJmY2RmYTk2ZSJ9"
      "aad": ["data1", "data2"]
    }
    ```
    {:screen}
