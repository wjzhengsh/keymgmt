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

# 存取 API
{: #access-api}

{{site.data.keyword.keymanagementservicefull}} 提供的 REST API 可與任何程式設計語言搭配使用，以儲存、擷取及產生金鑰。
{: shortdesc}

若要使用 API，您需要產生服務及鑑別認證。 

## 擷取存取記號
{: #retrieve_token}

您可以從 {{site.data.keyword.iamshort}} 擷取存取記號，以向 {{site.data.keyword.keymanagementserviceshort}} 進行鑑別。使用[服務 ID](/docs/iam/serviceid.html)，您可以代表 {{site.data.keyword.cloud_notm}} 上或外部的服務或應用程式使用 {{site.data.keyword.keymanagementserviceshort}} API，而不需要共用個人使用者認證。  

如果您要利用使用者認證進行鑑別，則可以在 [{{site.data.keyword.cloud_notm}} (bx) CLI ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](/docs/cloud-platform/cli/reference/bluemix_cli/get_started.html#getting-started){: new_window} 中執行 `bx iam oauth-tokens` 來擷取記號。
{: tip}

請完成下列步驟，以擷取存取記號：

1. 在 {{site.data.keyword.cloud_notm}} 主控台中，移至**管理** &gt; **安全** &gt; **身分及存取** &gt; **服務 ID**。請遵循[建立服務 ID](/docs/iam/serviceid.html#creating-a-service-id){: new_window} 的處理程序。
2. 使用**動作**功能表，以[定義新服務 ID 的存取原則](/docs/iam/serviceidaccess.html#assigning-new-access){: new_window}。 
    
    如需管理 {{site.data.keyword.keymanagementserviceshort}} 資源存取權的相關資訊，請參閱[角色及許可權](/docs/services/keymgmt/keyprotect_manage_access.md#roles)。
3. 使用 **API 金鑰**區段，以[建立要與服務 ID 相關聯的 API 金鑰](/docs/iam/serviceid_keys.html#creating-an-api-key-for-a-service-id){: new_window}。請將 API 金鑰下載至安全位置來進行儲存。
4. 呼叫 {{site.data.keyword.iamshort}} API 來擷取您的存取記號。

    ```cURL
    curl -X POST \
      "https://iam.bluemix.net/oidc/token" \
      -H "Content-Type: application/x-www-form-urlencoded" \
      -H "Accept: application/json" \
      -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<your_API_key>" \ 
    ```
    {: codeblock}

    在要求中，將 `<API_key>` 取代為您在步驟 3 中所建立的 API 金鑰。下列截斷範例顯示記號輸出：

    ```
    {
    "access_token": "eyJraWQiOiIyM...",
    "expiration": 1512161390,
    "expires_in": 3600,
    "refresh_token": "J1AzOrtC8yHVlcT...",
    "token_type": "Bearer"
    }
    ```
    {: screen}

    使用前面加上 _Bearer_ 記號類型的完整 `access_token` 值，以程式設計方式使用 {{site.data.keyword.keymanagementserviceshort}} API 來管理服務的金鑰。 

## 擷取實例 ID
{: #retrieve_instance_ID}

您可以使用 [{{site.data.keyword.cloud_notm}} (bx) CLI ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](/docs/cloud-platform/cli/reference/bluemix_cli/get_started.html#getting-started){: new_window}，來擷取 {{site.data.keyword.keymanagementserviceshort}} 服務實例的識別資訊。使用實例 ID 可管理您帳戶中指定 {{site.data.keyword.keymanagementserviceshort}} 實例內的加密金鑰。 

1. 使用 {{site.data.keyword.cloud_notm}} (bx) CLI 登入 {{site.data.keyword.cloud_notm}}。

    ```sh
    bx login 
    ```
    {: pre}

    **附註：**如果登入失敗，請執行 `bx login --sso` 指令再試一次。當您使用聯合 ID 登入時，需要 `--sso` 參數。如果使用這個選項，請前往 CLI 輸出中所列的鏈結，以產生一次性的通行碼。

2. 選取包含已佈建之 {{site.data.keyword.keymanagementserviceshort}} 實例的帳戶。

    您可以執行 `bx resource service-instances` 來列出帳戶中所佈建的所有服務實例。

3. 擷取可唯一識別 {{site.data.keyword.keymanagementserviceshort}} 服務實例的「雲端資源名稱 (CRN)」。 

    ```sh
    bx resource service-instance <instance_name> --id
    ```
    {: pre}

    將 `<instance_name>` 取代為指派給 {{site.data.keyword.keymanagementserviceshort}} 實例的唯一別名。下列截斷範例顯示 Bluemix CLI 輸出。_7e8fc048-5606-4259-ad71-92397b0fa3f7_ 值是範例實例 ID。

    ```
    crn:v1:bluemix:public:kms:us-south:a/7e8fc048-5606-4259-ad71-92397b0fa3f7
    ```
    {: screen}

## 形成 API 要求
{: #form_api_request}

對服務發出 API 呼叫時，會根據最初佈建 {{site.data.keyword.keymanagementserviceshort}} 實例的方式來建構 API 要求。 

若要建置您的要求，請將[地區服務端點](/docs/services/keymgmt/keyprotect_regions.html)與適當的鑑別認證配對。例如，如果您已建立 `us-south` 地區的服務實例，請使用下列端點及 API 標頭來瀏覽服務中的金鑰：

```cURL
curl -X GET \
    https://keyprotect.us-south.bluemix.net/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <access_token>' \
    -H 'bluemix-instance: <instance_ID>' \
```
{: codeblock}

### 下一步為何？

- 若要進一步瞭解以程式設計方式管理您的金鑰，[請參閱 {{site.data.keyword.keymanagementserviceshort}} API 參考資料文件以取得程式碼範例 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/apidocs/639){: new_window}。
- 若要查看 {{site.data.keyword.keymanagementserviceshort}} 中所儲存的金鑰如何運作來加密及解密資料的範例，請[試用 GitHub 中的範例應用程式 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}。
