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

# 使用身分及存取管理來管理使用者存取
{: #managing-access-iam}

{{site.data.keyword.keymanagementservicefull}} 支援由 {{site.data.keyword.Bluemix_notm}} 身分及存取管理控管的集中式存取控制系統，可協助您管理使用者和加密金鑰的存取。
{: shortdesc}

一項良好的作法是在您邀請新使用者加入帳戶或服務時授與存取權。例如，請考量下列準則：

- **藉由指派 IAM 角色，讓使用者可存取您帳戶中的資源。**
    為需要存取您帳戶中之加密金鑰的使用者建立新原則，而不是共用您的管理認證。如果您是帳戶的管理者，您會自動被指派有權存取帳戶下所有資源的管理原則。
- **以最小的需要範圍授與角色及許可權。**
    例如，如果使用者只需要存取指定空間內的金鑰高階視圖，請授與_檢視者_ 角色給該空間的該使用者。
- **定期審核能夠管理存取控制及刪除金鑰資源的人。**
    請記住，將_管理者_ 角色授與給使用者，表示該使用者除了可以破壞資源之外，還能修改其他使用者的服務原則。

## 角色及許可權
{: #roles}

使用 {{site.data.keyword.Bluemix_notm}} 身分及存取管理 (IAM)，您可以設定原則，以定義您的團隊成員的存取範圍。

為了簡化存取，{{site.data.keyword.keymanagementserviceshort}} 會與 IAM 角色一致，讓每個使用者根據使用者獲得指派的角色，而有不同的服務視圖。如果您是服務的安全管理者，可以指派對應至您想要授與給團隊成員之特定 {{site.data.keyword.keymanagementserviceshort}} 許可權的 IAM 角色。

下表顯示身分及存取角色如何對映至 {{site.data.keyword.keymanagementserviceshort}} 許可權：
<table>
  <tr>
    <th>角色</th>
    <th>說明</th>
    <th>動作</th>
  </tr>
  <tr>
    <td>檢視者</td>
    <td>檢視者可以存取金鑰的高階視圖。檢視者無法存取或修改金鑰詳細資料。</td>
    <td>
      <ul>
        <li>檢視金鑰</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>編輯者</td>
    <td>編輯者可以建立金鑰、修改金鑰，以及檢視金鑰詳細資料。</td>
    <td>
      <ul>
        <li>建立金鑰</li>
        <li>檢視金鑰</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>管理者</td>
    <td>管理者可以執行檢視者和編輯者可以執行的所有動作，包括能夠刪除金鑰、邀請新使用者和管理存取控制。</td>
    <td>
      <ul>
        <li>建立金鑰</li>
        <li>檢視金鑰</li>
        <li>刪除金鑰</li>
        <li>管理存取控制</li>
      </ul>
    </td>
  </tr>
  <caption style="caption-side:bottom;">表 1. 身分及存取角色與 {{site.data.keyword.keymanagementserviceshort}} 許可權的對映。</caption>
</table>

**附註**：IAM 使用者角色提供服務或服務實例層次的存取權。[Cloud Foundry 角色](/docs/iam/users_roles.html#cfroles)是分開的，並且定義組織或空間層次的存取權。

若要進一步瞭解 {{site.data.keyword.Bluemix_notm}} 身分及存取管理，請參閱[使用者角色及許可權](/docs/iam/users_roles.html#iamusermanpol)。

### 下一步為何？

帳戶擁有者及管理者可以邀請使用者，以及設定對應於使用者可執行之 {{site.data.keyword.keymanagementserviceshort}} 動作的服務原則。

- 如需在 {{site.data.keyword.Bluemix_notm}} 使用者介面中指派使用者角色的相關資訊，請參閱[已啟用身分及存取之服務的存取原則](/docs/iam/iamusermanage.html#iammanidaccser)。
- 若要瞭解授與進階許可權以存取特定加密金鑰，請參閱[使用 API 管理金鑰的存取](/docs/services/keymgmt/keyprotect_manage_access_api.html)。
