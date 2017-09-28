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

# 刪除金鑰

如果您是 {{site.data.keyword.Bluemix_notm}} 空間或 {{site.data.keyword.keymanagementserviceshort}} 服務實例的管理者，可以使用 {{site.data.keyword.keymanagementservicefull}} 來刪除加密金鑰及其內容。
{: shortdesc}

**重要事項**：當您刪除金鑰時，會永久地清除其內容和相關聯的資料。無法回復此動作。不建議針對正式作業環境破壞資源，但可能適用於測試或 QA 等暫時性環境。

## 使用 GUI 刪除金鑰
{: #gui}

如果您偏好使用圖形介面來刪除金鑰資源，可以使用 {{site.data.keyword.keymanagementserviceshort}} GUI。

[在建立金鑰或將現有金鑰匯入到服務之後](/docs/services/keymgmt/keyprotect_create_keys.html)，請完成下列步驟來刪除金鑰：

1. [登入 {{site.data.keyword.Bluemix_notm}} 主控台 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.bluemix.net/)。
2. 從 {{site.data.keyword.Bluemix_notm}} 儀表板，選取 {{site.data.keyword.keymanagementserviceshort}} 的佈建實例。
3. 導覽至**管理**窗格以瀏覽服務中的金鑰。
4. 按一下圖示以開啟您要刪除之金鑰的選項清單。
5. 從選項功能表，按一下**刪除金鑰**並在下一個畫面中確認刪除金鑰。

## 使用 API 刪除金鑰
{: #api}

若要刪除金鑰及其內容，請對下列端點進行 `DELETE` 呼叫：

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID>
```

1. [擷取您的授權記號、組織 GUID 及空間 GUID 以在服務中使用金鑰](/docs/services/keymgmt/keyprotect_authentication.html)。

2. 擷取您想要刪除之金鑰的 ID。

    您可以擷取指定金鑰的 ID，方法是提出 `GET /v2/keys` 要求，或在 {{site.data.keyword.keymanagementserviceshort}} 儀表板中檢視金鑰。

3. 執行下列 cURL 指令，以永久地刪除金鑰及其內容。

    ```cURL
    curl -X DELETE \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID> \
      -H 'authorization: Bearer <OAuth_token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
      -H 'prefer: <return_preference>'
    ```
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
        <td><em>space_GUID</em></td>
        <td>指派給您的 {{site.data.keyword.Bluemix_notm}} 空間的唯一 ID。</td>
      </tr>
      <tr>
        <td><em>organization_GUID</em></td>
        <td>指派給您的 {{site.data.keyword.Bluemix_notm}} 組織的唯一 ID。</td>
      </tr>
      <tr>
        <td><em>key_ID</em></td>
        <td>您要刪除之金鑰的唯一 ID。</td>
      </tr>
      <tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p>變更 <code>POST</code> 及 <code>DELETE</code> 行為之伺服器行為的標頭。</p><p>如果設為 <code>return=minimal</code>，服務在回應實體內文中只會傳回金鑰 meta 資料（例如金鑰名稱和 <code>id</code> 值）。如果設為 <code>return=representation</code>，服務會傳回金鑰資料和金鑰 meta 資料。</p></td>
      </tr>
      <caption style="caption-side:bottom;">表 1. 說明透過 {{site.data.keyword.keymanagementserviceshort}} API 刪除金鑰所需的變數。</caption>
    </table>

    `DELETE` 要求的詳細資料會在回應實體內文中傳回。
