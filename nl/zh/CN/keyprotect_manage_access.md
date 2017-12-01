---

copyright:
  years: 2017
lastupdated: "2017-11-08"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# 使用 Identity and Access Management 管理用户访问权
{: #managing-access-iam}

{{site.data.keyword.keymanagementservicefull}} 支持由 {{site.data.keyword.iamlong}} 管理的集中访问控制系统，可帮助您管理加密密钥的用户和访问权。
{: shortdesc}

最佳作法是在您邀请新用户加入帐户或服务时，授予访问许可权。例如，考虑以下准则：

- **通过分配 IAM 角色，对帐户中的资源启用用户访问权。**
    为需要访问帐户中加密密钥的用户创建新策略，而不是共享管理凭证。如果您是帐户的管理员，您会自动授予管理策略，具有帐户下所有资源的访问权。
- **在所需最小作用域下授予角色和许可权。**
    例如，如果用户仅需要访问指定空间内的高级密钥视图，请授予用户该空间的_查看者_角色。
- **定期审计何人具有管理访问控制和删除密钥资源的能力。**
    记住向用户授予_管理员_角色意味着该用户除了可以销毁资源外，还可以修改其他用户的服务策略。

## 角色和许可权
{: #roles}

使用 {{site.data.keyword.iamshort}} (IAM) 可以设置策略，以定义团队成员的访问作用域。

为了简化访问，{{site.data.keyword.keymanagementserviceshort}} 与 IAM 角色保持一致，以便每个用户根据用户的角色，具有服务的不同视图。如果您是服务的安全管理员，那么您可以分配 IAM 角色，其对应于您要授权团队成员的特定 {{site.data.keyword.keymanagementserviceshort}} 许可权。

下表显示身份和访问角色如何映射到 {{site.data.keyword.keymanagementserviceshort}} 许可权：
<table>
  <tr>
    <th>角色</th>
    <th>描述</th>
    <th>操作</th>
  </tr>
  <tr>
    <td>查看者</td>
    <td>查看者可以访问密钥的高级视图。查看者无法访问或修改密钥详细信息。</td>
    <td>
      <ul>
        <li>查看密钥</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>编辑者</td>
    <td>编辑者可以创建密钥、修改密钥以及查看密钥详细信息。</td>
    <td>
      <ul>
        <li>创建密钥</li>
        <li>查看密钥</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>管理员</td>
    <td>管理员可以执行查看者和编辑者可以执行的所有操作，包括删除密钥、邀请新用户和管理访问控制的能力。</td>
    <td>
      <ul>
        <li>创建密钥</li>
        <li>查看密钥</li>
        <li>删除密钥</li>
        <li>管理访问控制</li>
      </ul>
    </td>
  </tr>
  <caption style="caption-side:bottom;">表 1. 身份和访问角色与 {{site.data.keyword.keymanagementserviceshort}} 许可权的映射。</caption>
</table>

**注**：IAM 用户角色在服务或服务实例级别提供访问权。[Cloud Foundry 角色](/docs/iam/users_roles.html#cfroles)是分开的，在组织或空间级别定义访问权。

要了解有关 {{site.data.keyword.iamshort}} 的信息，请查看[用户角色和许可权](/docs/iam/users_roles.html#iamusermanpol)。

### 后续工作

帐户所有者和管理员可以邀请用户并设置对应于用户可以执行的 {{site.data.keyword.keymanagementserviceshort}} 操作的服务策略。

- 有关在 {{site.data.keyword.cloud_notm}} UI 中分配用户角色的的更多信息，请参阅[启用身份和访问权的服务访问策略](/docs/iam/iamusermanage.html#iammanidaccser)。
- 要了解授予高级许可权以访问特定加密密钥的更多信息，请参阅[使用 API 管理密钥的访问权](/docs/services/keymgmt/keyprotect_manage_access_api.html)。
