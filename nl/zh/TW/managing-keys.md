---

copyright:
  years: 2017
lastupdated: "2017-08-03"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# 管理金鑰

您可以使用 {{site.data.keyword.keymanagementservicelong}} for {{site.data.keyword.Bluemix_short}} 來管理金鑰的生命週期。
{: shortdesc}

有一項不錯的作法是在您開發程式碼時安全地管理您的金鑰。例如，思考下列類型的準則，以及其他安全編碼作法。

- 將金鑰嵌入您的程式碼時請考量安全問題。
- 只在對您的應用程式及資源進行程式化存取時才建立金鑰。不要在可以授與更簡單的[使用者許可權 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.bluemix.net/docs/admin/patterns.html#userroles "外部鏈結圖示"){: new_window} 時建立金鑰。
- 輪換金鑰並移除未用的金鑰。
- 對機密作業使用多重因素鑑別。
- 使每一個應用程式具有各自金鑰，隔離應用程式。
- 考量在傳送高度機密性資訊時使用程式化 API。

## 產生 {{site.data.keyword.keymanagementserviceshort}} API 的鑑別認證
{: #authentication_api}

{{site.data.keyword.keymanagementservicelong_notm}} 提供的 REST API 可與任何程式設計語言搭配使用，以儲存、擷取及產生金鑰。

若要使用 API，您需要產生鑑別及服務認證。

1. 透過 Cloud Foundry CLI 登入 {{site.data.keyword.Bluemix_notm}}。

    ```
    cf login [a api.DomainName] [-sso]
    ```
    {: codeblock}

2. 選取包含 Key Protect 服務實例的 {{site.data.keyword.Bluemix_notm}} 組織及空間。記下 CLI 輸出中的組織及空間名稱。您也可以執行 `cf target` 以檢視此資訊。
3. 擷取 {{site.data.keyword.Bluemix_notm}} 組織及空間 GUID。

    ```
    cf org organization_name --guid
    cf space space_name --guid
    ```
    {: codeblock}

4. 要求 {{site.data.keyword.Bluemix_notm}} 存取記號。

    ```
    cf oauth-token
    ```
    {: codeblock}

    下列截斷範例顯示 {{site.data.keyword.Bluemix_notm}} 記號輸出。_bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7_ 變數是範例存取記號。

    ```
    bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7...
    ```
    {: screen}

下一步：

請參閱 {{site.data.keyword.keymanagementserviceshort}} [REST API 參考資料文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/apidocs/639 "外部鏈結圖示"){: new_window} 以開始在空間中管理金鑰。


## 使用 {{site.data.keyword.keymanagementserviceshort}} API 建立金鑰
{: #codingapps}

您可以使用 {{site.data.keyword.keymanagementservicelong_notm}} API，來保護現有金鑰的安全或產生新金鑰。

對下列端點進行 **POST** 呼叫來建立金鑰或新增現有金鑰：

```
https://ibm-key-protect.edge.bluemix.net/api/v2/secrets
```
{: codeblock}

如果您想要在新增自己的金鑰之前先試用服務，請試用[範例應用程式 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/IBM-Bluemix/key-protect-helloworld-python "外部鏈結圖示"){: new_window}。

1. [擷取您的 {{site.data.keyword.Bluemix_notm}} 存取記號、組織 GUID 及空間 GUID 以在服務中使用金鑰](#authentication_api)。

2. 使用下列 cURL 指令，呼叫 [{{site.data.keyword.keymanagementserviceshort}}API](https://console.ng.bluemix.net/apidocs/639)。

  ```cURL
  curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: bluemix_access_token' --header 'Bluemix-Space: space_GUID' --header 'Bluemix-Org: organization_GUID' -d '{
    "metadata": {
      "collectionType": "application/vnd.ibm.kms.secret+json",
      "collectionTotal": 1
    },
    "resources": [
      {
      "type": "application/vnd.ibm.kms.secret+json",
      "name": "key_alias",
      "description": "key_description",
      "expirationDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
      "payload": "key_contents"
      }
    ]
  }' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets'
  ```
  {: codeblock}

  根據下表取代範例要求中的變數。
  <table>
    <tr>
      <th>變數</th>
      <th>說明</th>
    </tr>
    <tr>
      <td><em>bluemix_access_token</em></td>
      <td>您的授權記號。請在 cURL 要求包含記號的完整內容，包括 Bearer 值。</td>
    </tr>
    <tr>
      <td><em>space_GUID</em></td>
      <td>您的 {{site.data.keyword.Bluemix_notm}} 空間的 ID。</td>
    </tr>
    <tr>
      <td><em>organization_GUID</em></td>
      <td>您的 {{site.data.keyword.Bluemix_notm}} 組織的 ID。</td>
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
      <td>選用項目：系統中金鑰到期的日期和時間，以 RFC3339 格式表示。如果省略 <code>expirationDate</code> 屬性，則金鑰不會到期。</td>
    </tr>
    <tr>
      <td><em>key_contents</em></td>
      <td>您想要儲存在 {{site.data.keyword.keymanagementserviceshort}} 的金鑰資料，例如 RSA 金鑰。若要產生新的金鑰，請省略 payload 屬性及 key_contents 變數。</td>
    </tr>
      <caption style="caption-side:bottom;">表 1. 透過 {{site.data.keyword.keymanagementserviceshort}} API 新增金鑰所需的變數</caption>
  </table>

3. 藉由執行下列呼叫取得 {{site.data.keyword.Bluemix_notm}} 空間中的金鑰，驗證已建立金鑰。

  ```cURL
  curl -X GET --header 'Accept: application/json' --header 'Authorization: bluemix_access_token' --header 'Bluemix-Space: space_GUID' --header 'Bluemix-Org: organization_GUID' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets'
  ```
  {: codeblock}

## 使用 {{site.data.keyword.keymanagementserviceshort}} API 檢視金鑰
{: #viewingkeys_api}

如果您是 {{site.data.keyword.Bluemix_notm}} 空間管理員或開發人員，可以透過 {{site.data.keyword.keymanagementservicelong_notm}} API 檢視金鑰的內容。

如需高階視圖，您可以透過 {{site.data.keyword.keymanagementserviceshort}} 使用者介面瀏覽空間中管理的金鑰。

對下列端點進行 GET 呼叫來檢視金鑰的詳細資訊：

```
https://ibm-key-protect.edge.bluemix.net/api/v2/secrets/key_ID
```
{: codeblock}

1. 從 {{site.data.keyword.keymanagementserviceshort}} 使用者介面的「安全」服務下，您可以檢視有關金鑰的一般性質。您可以按一下可排序的直欄標頭來瀏覽金鑰。
2. 複製金鑰列中的 **ID**。ID 值是用來在 API 中存取金鑰的其他詳細資訊，例如金鑰資料本身。
3. [擷取您的 {{site.data.keyword.Bluemix_notm}} 存取記號、組織 GUID 及空間 GUID 來使用服務中的金鑰。](#authentication_api)
4. 執行下列 cURL 指令，以取得金鑰的詳細資料及金鑰資料。

  ```cURL
  curl -X GET --header 'Accept: application/json' --header 'Authorization: bluemix_access_token' --header 'Bluemix-Space: space_GUID' --header 'Bluemix-Org: organization_GUID' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets/key_ID'
  ```
  {: codeblock}

  根據下表取代範例要求中的變數。
  <table>
    <tr>
      <th>變數</th>
      <th>說明</th>
    </tr>
    <tr>
      <td><em>bluemix_access_token</em></td>
      <td>您的授權記號。請在 cURL 要求包含記號的完整內容，包括 Bearer 值。</td>
    </tr>
    <tr>
      <td><em>space_GUID</em></td>
      <td>指派給您的 {{site.data.keyword.Bluemix_notm}} 空間的隨機產生 ID。</td>
    </tr>
    <tr>
      <td><em>organization_GUID</em></td>
      <td>指派給您的 {{site.data.keyword.Bluemix_notm}} 組織的隨機產生 ID。</td>
    </tr>
    <tr>
      <td><em>key_ID</em></td>
      <td>您在步驟 [2](https://console.bluemix.net/docs/services/keymgmt/managing.html#viewingkeys_api__keyid) 中取回之金鑰的 ID。</td>
    </tr>
    <caption style="caption-side:bottom;">表 2. 說明透過 {{site.data.keyword.keymanagementserviceshort}} API 檢視金鑰所需的變數。</caption>
  </table>

  金鑰資料會在回應實體主體中傳回。硬體安全模組 (HSM) 所產生的金鑰是以 base-64 編碼。

## 審核金鑰及存取
{: #viewkeyassignments}

{{site.data.keyword.keymanagementservicelong_notm}} 提供集中化的系統，以便檢視、管理及審核您的加密金鑰。請審核您的金鑰及對於金鑰的存取權限制，以確保資源安全。

定期審核您的金鑰配置：

- 檢查金鑰的建立時間，並決定是否應該輪替金鑰。
- [使用 {{site.data.keyword.cloudaccesstrailshort}} 監視對 {{site.data.keyword.keymanagementserviceshort}} 的 API 呼叫 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.bluemix.net/docs/services/AccessTrail/at_integration.html#at_integration_key_protect "外部鏈結圖示"){: new_window}。
- 檢查哪些使用者可以存取金鑰，以及存取層次是否適當。

若要以存取權審核使用者，請執行下列動作：

1. 以空間管理員的身分，移至帳戶設定，然後選取**管理組織**。
2. 開啟包含 {{site.data.keyword.keymanagementserviceshort}} 服務實例的空間，以檢查哪些使用者具有存取權。
3. 如果需要新增使用者，請移至**邀請團隊成員**，然後選取 {{site.data.keyword.Bluemix_notm}} 角色，這些角色對應於您要授與使用者的 {{site.data.keyword.keymanagementserviceshort}} 許可權。

  <table>
    <tr>
      <th>{{site.data.keyword.Bluemix_notm}} 角色</th>
      <th>{{site.data.keyword.keymanagementserviceshort}} 許可權</th>
    </tr>
    <tr>
      <td>空間管理員</td>
      <td>空間管理員可以建立、檢視及刪除金鑰。</td>
    </tr>
    <tr>
      <td>開發人員</td>
      <td>開發人員可以建立金鑰及檢視金鑰詳細資料。</td>
    </tr>
    <tr>
      <td>審核員</td>
      <td>審核員可以存取高層次的金鑰視圖。</td>
    </tr>
    <caption style="caption-side:bottom;">表 3. {{site.data.keyword.Bluemix_notm}} 角色與 {{site.data.keyword.keymanagementserviceshort}} 許可權的對映。</caption>
  </table>
