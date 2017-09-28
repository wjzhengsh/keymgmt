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

# 疑難排解

以下是使用 {{site.data.keyword.keymanagementservicefull}} 的常見疑難排解問題的回答。
{: shortdesc}

## 無法建立或刪除金鑰
{: #unabletomanagekeys}

如果無法執行 {{site.data.keyword.keymanagementserviceshort}} 動作，請確認您具有正確的授權。

### 症狀

當您存取 {{site.data.keyword.keymanagementserviceshort}} 使用者介面時，無法檢視新增或刪除金鑰的選項。

### 解決問題

請向管理者確認已將適當空間中的正確角色指派給您。如需角色的相關資訊，請參閱[角色及許可權](/docs/services/keymgmt/keyprotect_manage_access.html#roles)。

## 從測試版轉換成一般組件 (GA)
{: #ts_planconversion}

測試版使用者需要變更為標準定價模型，才能繼續使用 {{site.data.keyword.keymanagementserviceshort}} 服務。

### 症狀

如果您是測試版使用者，您需要將定價方案變更為分層式定價模型，以便繼續在 {{site.data.keyword.keymanagementserviceshort}} 儲存金鑰。

### 解決問題

{{site.data.keyword.keymanagementserviceshort}} 服務有兩種定價模型：輕量型和累進分層式。身為管理者，請確認已選取累進分層式模型。如果您不想要移轉到分層式模型，請確定所有金鑰和服務實例在淘汰之前已移除。[如需相關資訊，請參閱 {{site.data.keyword.keymanagementserviceshort}} 一般組件公告 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")]("https://www.ibm.com/blogs/bluemix/2016/12/dallas-key-protect-ga/" "https://www.ibm.com/blogs/bluemix/2016/12/dallas-key-protect-ga/"){: new_window}。

若要變更定價方案，請執行下列動作：

1. 移至 {{site.data.keyword.keymanagementserviceshort}} 使用者介面然後選取**方案**標籤。
2. 選取**累進分層式定價**。每個月使用的作用中金鑰的成本細目會出現在表格中。分層式模型會根據在帳戶層次每個月的作用中金鑰數計算定價。
3. 若要確認方案變更，請按一下**儲存**。

## 取得 {{site.data.keyword.keymanagementserviceshort}} 的協助及支援
{: #ts_gettinghelp}

如果您在使用 {{site.data.keyword.keymanagementservicefull_notm}} 時發生問題或有疑問，可以搜尋資訊或透過討論區提問來取得協助。您也可以開立支援問題單。

使用討論區提問時，請標記您的問題，以便 {{site.data.keyword.IBM_notm}} {{site.data.keyword.Bluemix_notm}} 開發團隊能看到它。

- 如果您有使用 {{site.data.keyword.keymanagementserviceshort}} 的相關技術問題，請將問題張貼在 [Stack Overflow ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://stackoverflow.com/search?q=key-protect+ibm-bluemix){: new_window}，並使用 "ibm-bluemix" 和 "key-protect" 來標記您的問題。
- 若是服務及開始使用指示的相關問題，請使用 [IBM developerWorks dW Answers ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/answers/topics/key-protect/?smartspace=bluemix){: new_window} 討論區。請包含 "bluemix" 和 "key-protect" 標籤。

如需使用討論區的詳細資料，請參閱[取得協助 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.bluemix.net/docs/support/index.html#getting-help){: new_window}。

如需開立 {{site.data.keyword.IBM_notm}} 支援問題單的相關資訊，或支援層次與問題單嚴重性的相關資訊，請參閱[與支援中心聯絡 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.bluemix.net/docs/support/index.html#contacting-support){: new_window}。
