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

# 開始使用 {{site.data.keyword.keymanagementserviceshort}}

{{site.data.keyword.keymanagementservicelong}} 可協助您在 {{site.data.keyword.Bluemix_short}} 為應用程式佈建加密金鑰。當您管理金鑰的生命週期時，可以因為知道金鑰受到保護資訊免遭竊取的雲端型硬體安全模組 (HSM) 保護而受益。
{: shortdesc}

{{site.data.keyword.keymanagementserviceshort}} 建立所在空間內的所有應用程式都可自動使用該服務。[在建立服務的實例之後](https://console.ng.bluemix.net/catalog/services/key-protect/?taxonomyNavigation=apps){: new_window}，請完成下列步驟以開始進行：

1. 若要建立金鑰或上傳現有金鑰，請按一下**新增金鑰**。指定金鑰的詳細資料：
    <table>
      <tr>
        <th>設定</th>
        <th>說明</th>
      </tr>
      <tr>
        <td>名稱</td>
        <td>要指派給您的金鑰且人類可閱讀的別名。此名稱可以是協助您識別金鑰的任何內容，例如金鑰的用途，或是與金鑰相關聯的人。</td>
      </tr>
      <tr>
        <td>演算法</td>
        <td>AES-GCM 演算法支援對稱金鑰加密。</td>
      </tr>
      <tr>
        <td>金鑰</td>
        <td>只有在您新增現有的金鑰時需要。金鑰資料可以是您要儲存在 {{site.data.keyword.keymanagementserviceshort}} 服務中的任何類型的資料，例如憑證或 RSA 金鑰。</td>
      </tr>
        <caption style="caption-side:bottom;">表 1. 金鑰設定的說明</caption>
    </table>

2. 當您填寫完金鑰的詳細資料，請按一下**新增金鑰**以便確認。金鑰立即可用。新金鑰是由位於安全 {{site.data.keyword.IBM}} 資料中心的硬體安全模組所建立。
3. 複製金鑰列中的參照 ID。**ID** 值是您在 {{site.data.keyword.keymanagementserviceshort}} API 中使用的 ID。
4. **選用**：如果想要刪除金鑰，請記住無法復原金鑰資料。與金鑰相關聯的 meta 資料保存在 {{site.data.keyword.keymanagementserviceshort}} 資料庫中。若要刪除金鑰，請按一下金鑰列中的**動作**圖示，並在下一個畫面中確認刪除。

下一步為何：

現在，您可以使用金鑰來編碼應用程式及服務。

- 若要查看 {{site.data.keyword.keymanagementserviceshort}} 中儲存的金鑰如何運作來加密及解密資料，請[試用 Github 中的範例應用程式 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/IBM-Bluemix/key-protect-helloworld-python "外部鏈結圖示"){: new_window}。
- 若要進一步瞭解以程式設計方式管理您的金鑰，請參閱 [{{site.data.keyword.keymanagementserviceshort}} API 參考資料文件](https://console.ng.bluemix.net/apidocs/639)裡的程式碼範例。

## 相關鏈結

- [{{site.data.keyword.keymanagementserviceshort}} REST API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/apidocs/639 "外部鏈結圖示"){: new_window}
- [{{site.data.keyword.keymanagementserviceshort}} 管理 REST API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs-admin-keyprotect.ng.bluemix.net/ "外部鏈結圖示"){: new_window}
- [Cloud HSM 供應項目 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.softlayer.com/ibm-cloud-hsm "外部鏈結圖示"){: new_window}
