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

# 建立主要金鑰
{: #create_root_keys}

您可以利用 {{site.data.keyword.keymanagementservicefull}}，以使用 {{site.data.keyword.keymanagementserviceshort}} GUI 或使用 {{site.data.keyword.keymanagementserviceshort}} API 透過程式設計方式，來建立主要金鑰。
{: shortdesc}

主要金鑰是用來保護雲端中已加密資料安全的對稱金鑰包裝金鑰。如需主要金鑰的相關資訊，請參閱[封套加密](/docs/services/keymgmt/keyprotect_envelope.html)。 

## 使用 GUI 建立主要金鑰
{: #create_root_key_GUI}

[在建立服務的實例之後](/docs/services/keymgmt/keyprotect_provision.html)，請完成下列步驟以使用 {{site.data.keyword.keymanagementserviceshort}} GUI 來建立主要金鑰。

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
        <td>要指派給您的金鑰且人類可閱讀的唯一別名。此名稱可以是協助您識別金鑰的任何內容，例如金鑰的用途，或是與金鑰相關聯的人。</td>
      </tr>
      <tr>
        <td>金鑰類型</td>
        <td>您要在 {{site.data.keyword.keymanagementserviceshort}} 中管理的[金鑰類型](/docs/services/keymgmt/keyprotect_envelope.html#key_types)。從金鑰類型清單中，選取<b>主要金鑰</b>。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. <b>產生新金鑰</b>設定的說明</caption>
    </table>

3. 當您填寫完金鑰的詳細資料時，請按一下**產生金鑰**以便確認。 

## 使用 API 建立主要金鑰
{: #create_root_key_API}

對下列端點發出 `POST` 呼叫來建立主要金鑰：

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
       "extractable": false
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
          <p>當您將 <code>extractable</code> 屬性設為 <code>false</code> 時，服務會建立一個主要金鑰，您可以將它用於 <code>wrap</code> 或 <code>unwrap</code> 作業。</p>
        </td>
      </tr>
        <caption style="caption-side:bottom;">表 1. 使用 {{site.data.keyword.keymanagementserviceshort}} API 新增主要金鑰所需的變數</caption>
    </table>

    成功的 `POST /v2/keys/` 回應會傳回您金鑰的 ID 值，以及其他 meta 資料。ID 是指派給您金鑰的唯一 ID，並用於後續的 {{site.data.keyword.keymanagementserviceshort}} API 呼叫。

3. 選用項目：執行下列呼叫來瀏覽 {{site.data.keyword.keymanagementserviceshort}} 服務實例中的金鑰，確認已建立金鑰。

    ```cURL
    curl -X GET \
      https://keyprotect.us-south.bluemix.net/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

**附註：**在您使用服務建立主要金鑰之後，金鑰會保留在 {{site.data.keyword.keymanagementserviceshort}} 的範圍內，而且無法擷取其金鑰資料。 

### 下一步為何？

- 若要進一步瞭解如何使用封套加密來保護金鑰，請參閱[包裝金鑰](/docs/services/keymgmt/keyprotect_wrap_keys.html)。
- 若要進一步瞭解以程式設計方式管理您的金鑰，[請參閱 {{site.data.keyword.keymanagementserviceshort}} API 參考資料文件以取得程式碼範例 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/apidocs/639){: new_window}。
