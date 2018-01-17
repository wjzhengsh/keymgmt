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

# 建立標準金鑰
{: #create_standard_keys}

您可以使用 {{site.data.keyword.keymanagementserviceshort}} GUI 或使用 {{site.data.keyword.keymanagementserviceshort}} API 透過程式設計方式，來建立標準加密金鑰。
{: shortdesc}

## 使用 GUI 建立標準金鑰
{: #create_standard_key_GUI}

[在建立服務的實例之後](/docs/services/keymgmt/keyprotect_provision.html)，請完成下列步驟以使用 {{site.data.keyword.keymanagementserviceshort}} GUI 來建立標準金鑰。

1. [登入 {{site.data.keyword.cloud_notm}} 主控台 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.bluemix.net/)。
2. 從 {{site.data.keyword.cloud_notm}} 儀表板，選取已佈建的 {{site.data.keyword.keymanagementserviceshort}} 實例。
2. 若要建立新的金鑰，請按一下**新增金鑰**，然後選取**產生新金鑰**視窗。

    指定金鑰的詳細資料：

    <table>
      <tr>
        <th>設定</th>
        <th>說明</th>
      </tr>
      <tr>
        <td>名稱</td>
        <td>要指派給您的金鑰且人類可閱讀的別名。此名稱可以是協助您識別金鑰的任何內容，例如金鑰的用途，或是與金鑰相關聯的人。</td>
      </tr>
      <tr></tr>
        <td>金鑰類型</td>
        <td>您要在 {{site.data.keyword.keymanagementserviceshort}} 中管理的[金鑰類型](/docs/services/keymgmt/keyprotect_envelope.html#key_types)。從金鑰類型清單中，選取<b>標準金鑰</b>。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. <b>產生新金鑰</b>設定的說明</caption>
    </table>

3. 當您填寫完金鑰的詳細資料時，請按一下**產生金鑰**以便確認。 

## 使用 API 建立標準金鑰
{: #create_standard_key_API}

對下列端點發出 `POST` 呼叫來建立標準金鑰：

```
https://keyprotect.us-south.bluemix.net/api/v2/keys
```
{: codeblock}

1. [擷取服務及鑑別認證以在服務中使用金鑰](/docs/services/keymgmt/keyprotect_authentication.html)。

2. 使用下列 cURL 指令，呼叫 [{{site.data.keyword.keymanagementserviceshort}}API](https://console.ng.bluemix.net/apidocs/639)。

    ```cURL
    curl -X POST \
      https://keyprotect.us-south.bluemix.net/api/v2/keys \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
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
       "extractable": true
       }
     ]
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
        <td><em>IAM_token</em></td>
        <td>您的授權記號。請在 cURL 要求中包含 <code>IAM</code> 記號的完整內容，包括 Bearer 值。</td>
      </tr>
      <tr>
        <td><em>instance_ID</em></td>
        <td>指派給您的 {{site.data.keyword.keymanagementserviceshort}} 服務實例的唯一 ID。</td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>用來追蹤及關聯交易的唯一 ID。</td>
      </tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p>選用項目：變更 <code>POST</code> 及 <code>DELETE</code> 作業之伺服器行為的標頭。</p><p>當您將 <em>return_preference</em> 變數設為 <code>return=minimal</code> 時，服務在回應實體內文中只會傳回金鑰 meta 資料（例如金鑰名稱及 ID 值）。當您將變數設為 <code>return=representation</code> 時，服務會傳回標準金鑰的金鑰資料及金鑰 meta 資料。</p></td>
      </tr>
      <tr>
        <td><em>key_alias</em></td>
        <td>方便識別金鑰且人類可閱讀的唯一名稱。</td>
      </tr>
      <tr>
        <td><em>key_description</em></td>
        <td>金鑰的延伸說明。</td>
      </tr>
      <tr>
        <td><em>YYYY-MM-DD</em><br><em>HH:MM:SS.SS</em></td>
        <td>選用項目：系統中的金鑰到期的日期和時間，以 RFC 3339 格式表示。如果省略 <code>expirationDate</code> 屬性，則金鑰不會到期。</td>
      </tr>
      <tr>
        <td><em>key_type</em></td>
        <td>
          <p>決定金鑰資料是否可以離開服務的布林值。</p>
          <p>當您將 <code>extractable</code> 屬性設為 <code>true</code> 時，服務會建立標準金鑰，您可以將它儲存在應用程式或服務中。</p>
        </td>
      </tr>
        <caption style="caption-side:bottom;">表 2. 使用 {{site.data.keyword.keymanagementserviceshort}} API 新增標準金鑰所需的變數</caption>
    </table>

    成功的 `POST /v2/keys/` 回應會傳回您金鑰的 ID 值，以及其他 meta 資料。ID 是指派給您金鑰的唯一 ID，並用於後續的 {{site.data.keyword.keymanagementserviceshort}} API 呼叫。

3. 選用項目：執行下列呼叫來取得 {{site.data.keyword.keymanagementserviceshort}} 服務實例中的金鑰，確認已建立金鑰。

    ```cURL
    curl -X GET \
      https://keyprotect.us-south.bluemix.net/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}


### 下一步為何？

- 若要進一步瞭解以程式設計方式管理您的金鑰，[請參閱 {{site.data.keyword.keymanagementserviceshort}} API 參考資料文件以取得程式碼範例 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/apidocs/639){: new_window}。
- 若要查看 {{site.data.keyword.keymanagementserviceshort}} 中所儲存的金鑰如何運作來加密及解密資料的範例，請[試用 GitHub 中的範例應用程式 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}。
