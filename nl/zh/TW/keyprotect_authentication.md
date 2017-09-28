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

# 產生鑑別認證
{: #authentication}

{{site.data.keyword.keymanagementservicefull}} 提供的 REST API 可與任何程式設計語言搭配使用，以儲存、擷取及產生金鑰。
{: shortdesc}

若要使用 API，您需要產生服務及鑑別認證。

## 擷取組織及空間 GUID
{: #retrieve_GUIDs}

您可以使用 [{{site.data.keyword.Bluemix_notm}} CLI ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.bluemix.net/docs/cli/reference/bluemix_cli/index.html#getting-started) 擷取 {{site.data.keyword.Bluemix_notm}} 組織及空間的識別資訊。

1. 透過 {{site.data.keyword.Bluemix_notm}} CLI 登入 {{site.data.keyword.Bluemix_notm}}。

    ```
    bx login [--sso]
    ```
    {: codeblock}

    當您使用聯合 ID 登入時，需要 `--sso` 參數。如果使用這個選項，請前往 CLI 輸出中所列的鏈結，以產生一次性的通行碼。

2. 選取包含 {{site.data.keyword.keymanagementserviceshort}} 服務實例的 {{site.data.keyword.Bluemix_notm}} 組織及空間。

    記下 CLI 輸出中的組織及空間名稱。您也可以執行 `bx target` 以檢視此資訊。

3. 擷取 {{site.data.keyword.Bluemix_notm}} 組織及空間 GUID。

    ```
    bx iam org [organization_name] --guid
    bx iam space [space_name] --guid
    ```
    {: codeblock}
    請將 _organization_name_ 和 _space_name_ 取代為指派給您的組織及空間的唯一別名。

## 擷取授權記號
{: #retrieve_token}

您可以使用授權記號，使用 {{site.data.keyword.keymanagementserviceshort}} API 以程式化的方式來管理金鑰。

**附註**：若要啟用由 {{site.data.keyword.Bluemix_notm}} 身分及存取控制控管的精細存取控制，在呼叫服務時請使用 IAM 記號。

1. 在 {{site.data.keyword.Bluemix_notm}} CLI 中，選取包含 {{site.data.keyword.keymanagementserviceshort}} 服務的組織及空間。

2. 擷取及顯示您的授權記號。

    ```
    bx iam oauth-tokens
    ```
    {: codeblock}

    下列截斷範例顯示 {{site.data.keyword.Bluemix_notm}} 記號輸出。_Bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7_ 變數是範例存取記號。

    ```
    IAM token: Bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7...
    UAA token: Bearer mjEyJhbGciOiJIUzI1Ni.chWyW1faWQiOiJJQkWs1...
    ```
    {: screen}

    使用 `IAM` 或 `UAA` bearer 值，以程式設計方式，使用 {{site.data.keyword.keymanagementserviceshort}} API 管理服務中的金鑰。

### 下一步為何？

請參閱 [{{site.data.keyword.keymanagementserviceshort}}REST API 參考資料文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/apidocs/639){: new_window} 以開始在空間中管理金鑰。
