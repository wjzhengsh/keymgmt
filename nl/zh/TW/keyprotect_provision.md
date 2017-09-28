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

# 佈建 {{site.data.keyword.keymanagementserviceshort}} 服務
{: #provision}

您可以使用 {{site.data.keyword.Bluemix_notm}} 主控台或 {{site.data.keyword.Bluemix_notm}} CLI 建立 {{site.data.keyword.keymanagementservicefull}} 的安全實例。
{: shortdesc}

## 從 {{site.data.keyword.Bluemix_notm}} 主控台佈建
{: #gui}

若要從 {{site.data.keyword.Bluemix_notm}} 主控台佈建 {{site.data.keyword.keymanagementserviceshort}} 的實例，請完成下列步驟。

1. [登入 {{site.data.keyword.Bluemix_notm}} 帳戶 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.bluemix.net/){: new_window}。
2. 按一下**型錄**以檢視 {{site.data.keyword.Bluemix_notm}} 上可用的服務清單。
3. 選取**服務**種類，然後按一下 **{{site.data.keyword.keymanagementserviceshort}}** 磚。
5. 選取服務方案，然後按一下**建立**以在您登入的 {{site.data.keyword.Bluemix_notm}} 組織及空間中佈建 {{site.data.keyword.keymanagementserviceshort}} 服務實例。

## 從 {{site.data.keyword.Bluemix_notm}} CLI 佈建
{: #cli}

您可以使用 {{site.data.keyword.Bluemix_notm}} CLI 佈建 {{site.data.keyword.keymanagementserviceshort}} 的實例。[在您的系統下載並安裝指令行工具](https://clis.ng.bluemix.net/ui/home.html){: new_window}，以完成下列步驟。

1. 登入 {{site.data.keyword.Bluemix_notm}} CLI。

    ```sh
    bx login [--sso]
    ```
    {: codeblock}
    **附註**：當您使用聯合 ID 登入時，需要 `--sso` 參數。如果使用這個選項，請前往 CLI 輸出中所列的鏈結，以產生一次性的通行碼。

2. 選取您要建立 {{site.data.keyword.keymanagementserviceshort}} 服務實例的 {{site.data.keyword.Bluemix_notm}} 組織及空間。

    您也可以使用下列指令來設定目標組織及空間。

    ```sh
    bx target [-o organization_name] [-s space_name]
    ```
    {: codeblock}

3. 在該地區、組織及空間內佈建 {{site.data.keyword.keymanagementserviceshort}} 的實例。

    ```sh
    bx service create ibm_key_management TieredPricing [instance_name]
    ```
    {: codeblock}

    將 _instance_name_ 取代為服務實例的唯一別名。

4. 確認已順利建立服務實例。

    ```sh
    bx service list
    ```
    {: codeblock}


### 下一步為何？

現在，您可以使用金鑰來編碼應用程式及服務。

- 若要查看 {{site.data.keyword.keymanagementserviceshort}} 中儲存的金鑰如何運作來加密及解密資料，請[試用 GitHub 中的範例應用程式 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}。
- 若要進一步瞭解以程式設計方式管理您的金鑰，[請參閱 {{site.data.keyword.keymanagementserviceshort}} API 參考資料文件以取得程式碼範例 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/apidocs/639){: new_window}。
