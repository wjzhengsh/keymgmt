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

# 使用 Cloud IAM 管理用户访问权
{: #managing-access-iam}

{{site.data.keyword.keymanagementservicefull}} 支持由 {{site.data.keyword.iamlong}} 管理的集中访问控制系统，可帮助您管理加密密钥的用户和访问权。
{: shortdesc}

最佳作法是在您邀请新用户加入帐户或服务时，授予访问许可权。例如，考虑以下准则：

- **通过分配 Cloud IAM 角色，启用对帐户中资源的用户访问权。**
    为需要访问帐户中加密密钥的用户创建新策略，而不是共享管理凭证。如果您是帐户的管理员，那么会自动分配有_管理员_策略，具有对该帐户下所有资源的访问权。
- **在所需最小作用域下授予角色和许可权。**
    例如，如果用户仅需要访问指定空间内密钥的高级视图，请向该用户授予该空间的_读者_角色。
- **定期审计何人具有管理访问控制和删除密钥资源的能力。**
    请记住，向用户授予_管理员_角色意味着该用户除了可以销毁资源外，还可以修改其他用户的服务策略。

## 角色和许可权
{: #roles}

使用 {{site.data.keyword.iamshort}} (IAM) 可以管理和定义帐户中用户和资源的访问权。

为了简化访问，{{site.data.keyword.keymanagementserviceshort}} 与 Cloud IAM 角色保持一致，以便每个用户都能根据为该用户分配的角色来查看该服务的不同方面。如果您是服务的安全管理员，那么可以分配对应于您要授予团队成员的特定 {{site.data.keyword.keymanagementserviceshort}} 许可权的 Cloud IAM 角色。

下表显示身份和访问角色如何映射到 {{site.data.keyword.keymanagementserviceshort}} 许可权：
<table>
  <tr>
    <th>服务访问角色</th>
    <th>描述</th>
    <th>操作</th>
  </tr>
  <tr>
    <td>读者</td>
    <td>读者可以浏览密钥的高级视图并执行打包和解包操作。读者无法访问或修改密钥资料。</td>
    <td>
      <ul>
        <li>查看密钥</li>
        <li>打包密钥</li>
        <li>解包密钥</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>作者</td>
    <td>作者可以创建密钥、修改密钥以及访问密钥资料。</td>
    <td>
      <ul>
        <li>创建密钥</li>
        <li>查看密钥</li>
        <li>打包密钥</li>
        <li>解包密钥</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>管理员</td>
    <td>管理员可以执行读者和作者可执行的所有操作，包括能够删除密钥、邀请新用户以及为其他用户分配访问策略。</td>
    <td>
      <ul>
        <li>读者或作者可以执行的所有操作</li>
        <li>删除密钥</li>
        <li>分配访问策略</li>
      </ul>
    </td>
  </tr>
  <caption style="caption-side:bottom;">表 1. 身份和访问角色与 {{site.data.keyword.keymanagementserviceshort}} 许可权的映射。</caption>
</table>

**注**：Cloud IAM 用户角色提供的是服务或服务实例级别的访问权。[Cloud Foundry 角色](/docs/iam/users_roles.html#cfroles)是分开的，在组织或空间级别定义访问权。

要了解有关 {{site.data.keyword.iamshort}} 的更多信息，请查看[用户角色和许可权](/docs/iam/users_roles.html#iamusermanpol)。

### 后续工作

帐户所有者和管理员可以邀请用户并设置对应于用户可以执行的 {{site.data.keyword.keymanagementserviceshort}} 操作的服务策略。

- 有关在 {{site.data.keyword.cloud_notm}} UI 中分配用户角色的信息，请参阅[管理 IAM 访问权](/docs/iam/iamusermanage.html#iamusermanage)。
- 要了解授予高级许可权以访问特定加密密钥的更多信息，请参阅[使用 API 管理密钥的访问权](/docs/services/keymgmt/keyprotect_manage_access_api.html)。
