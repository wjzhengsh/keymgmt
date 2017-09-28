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

# 開始使用 {{site.data.keyword.keymanagementserviceshort}}

以下是在 {{site.data.keyword.keymanagementservicelong}} 內產生、輸入和管理金鑰所需的步驟。
{: shortdesc}

## 必要條件
{: #prereqs }

{{site.data.keyword.keymanagementserviceshort}} 可供服務及應用程式使用，它們在有正確授權的情況下，可以對 {{site.data.keyword.keymanagementserviceshort}} 進行 API 呼叫。您將需要先有下列各項才能新增金鑰。
- [IBM ID 及密碼](https://console.bluemix.net/docs/admin/adminpublic.html#signing-up-for-bluemix){: new_window}
- [服務的實例](https://console.ng.bluemix.net/catalog/services/key-protect/?taxonomyNavigation=apps){: new_window}

## 新增金鑰
{: #addkey }

請使用下列步驟來建立新的金鑰，或上傳現有金鑰。

1. [登入 Bluemix 主控台。](https://console.bluemix.net/catalog){: new_window}
2. 將滑鼠游標移到**所有種類**鏈結，以顯示捲軸。向下捲動至**服務 > 安全**。會顯示應用程式及服務的清單。
3. 按兩下 **Key Protect** 服務實例。請注意，在**動作**下，您可以重新命名或刪除服務。

如果您第一次輸入或產生金鑰，將會自動到**新增金鑰**頁面。**產生新金鑰**用來在 {{site.data.keyword.keymanagementserviceshort}} 中產生全新的金鑰，而**輸入現有服務**用來將現有金鑰輸入到服務中。

### 產生金鑰
{: #genkey }

請使用下列步驟，讓 Key Protect 產生新的金鑰。

1. 在**產生新金鑰**下輸入下列各項，讓 Key Protect 建立新的金鑰。
    <table>
      <tr>
        <th>欄位</th>
        <th>說明</th>
      </tr>
      <tr>
        <td>名稱</td>
        <td>要指派給您的金鑰且人類可閱讀的別名。此名稱可以是協助您識別金鑰的任何內容，例如金鑰的用途，或是與金鑰相關聯的人。</td>
      </tr>
      <tr>
        <td>金鑰類型</td>
        <td>預設為標準金鑰。標準金鑰用來作為資料加密金鑰，將您的純文字資料加密成密文。</td>
      </tr>
        <caption style="caption-side:bottom;">表 1. 「產生新金鑰」設定的說明</caption>
    </table>

2. 按一下**產生金鑰**按鈕。金鑰立即可用。新金鑰是由位於安全 {{site.data.keyword.IBM}} 資料中心的硬體安全模組所建立。
3. 複製金鑰列中的參照 ID。**ID** 值是您在 {{site.data.keyword.keymanagementserviceshort}} API 中使用的 ID。

### 輸入現有金鑰
{: #existkey }

請使用下列步驟，以將現有金鑰鍵入到 Key Protect。

1. 在**輸入現有金鑰**下輸入下列各項。
    <table>
      <tr>
        <th>欄位</th>
        <th>說明</th>
      </tr>
      <tr>
        <td>名稱</td>
        <td>要指派給您的金鑰且人類可閱讀的別名。此名稱可以是協助您識別金鑰的任何內容，例如金鑰的用途，或是與金鑰相關聯的人。</td>
      </tr>
      <tr>
        <td>金鑰類型</td>
        <td>預設為標準金鑰。標準金鑰用來作為資料加密金鑰，將您的純文字資料加密成密文。</td>
      </tr>
      <tr>
        <td>金鑰資料</td>
        <td>金鑰資料可以是您要儲存在 {{site.data.keyword.keymanagementserviceshort}} 服務中的任何類型的資料，例如憑證或 RSA 金鑰。</td>
      </tr>
        <caption style="caption-side:bottom;">表 2. 「輸入現有金鑰」設定的說明</caption>
    </table>

2. 按一下**新增金鑰**按鈕。金鑰立即可用。
3. 複製金鑰列中的參照 ID。**ID** 值是您在 {{site.data.keyword.keymanagementserviceshort}} API 中使用的 ID。

## 管理金鑰
{: #managekey }

若要在產生並輸入金鑰之後看到您的金鑰，請遵循[新增金鑰](index.html#addkey)下的步驟。您將在**金鑰**窗。您的金鑰會以建立日期順序顯示，最新的金鑰在清單的上方。
<table>
      <tr>
        <th>直欄</th>
        <th>說明</th>
      </tr>
      <tr>
        <td>名稱</td>
        <td>指派給您的金鑰且人類可閱讀的別名。</td>
      </tr>
      <tr>
        <td>ID</td>
        <td>Key Protect 指派給您的金鑰的唯一金鑰 ID。</td>
      </tr>
      <tr>
        <td>狀態</td>
        <td>美國國家標準技術研究院 (NIST) 的其中一個金鑰狀態 - 啟動前、作用中、取消啟動和已破壞。<td>
      </tr>
      <tr>
        <td>建立日期</td>
        <td>建立金鑰的日期和時間。</td>
      </tr>
      <tr>
        <td>類型</td>
        <td>預設為標準金鑰。</td>
      </tr>
      <caption style="caption-side:bottom;">表 3. 「金鑰」視窗的說明</caption>
    </table>

### 下一步為何？

現在，您可以使用金鑰來編碼應用程式及服務。

- 若要查看 {{site.data.keyword.keymanagementserviceshort}} 中儲存的金鑰如何運作來加密及解密資料，請[試用 Github 中的範例應用程式 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}。
- 若要進一步瞭解以程式設計方式管理您的金鑰，請參閱 [{{site.data.keyword.keymanagementserviceshort}} API 參考資料文件](https://console.ng.bluemix.net/apidocs/639)裡的程式碼範例。

### 相關鏈結

- [{{site.data.keyword.keymanagementserviceshort}} REST API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/apidocs/639){: new_window}
- [{{site.data.keyword.keymanagementserviceshort}} 管理 REST API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs-admin-keyprotect.ng.bluemix.net/){: new_window}
- [Cloud HSM 供應項目 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.softlayer.com/ibm-cloud-hsm){: new_window}
- [{{site.data.keyword.keymanagementservicelong_notm}} 服務水準合約 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www-03.ibm.com/software/sla/sladb.nsf/sla/bm-7603-01){: new_window}
