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

# 生成认证凭证
{: #authentication}

{{site.data.keyword.keymanagementservicefull}} 提供可与任何编程语言配合使用的 REST API，以存储、检索和生成密钥。
{: shortdesc}

要使用 API，需要生成服务和认证凭证。

## 检索组织和空间 GUID
{: #retrieve_GUIDs}

您可以使用 [{{site.data.keyword.cloud_notm}} CLI ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.bluemix.net/docs/cli/reference/bluemix_cli/index.html#getting-started) 检索 {{site.data.keyword.cloud_notm}} 组织和空间的识别信息。

1. 通过 {{site.data.keyword.cloud_notm}} (bx) CLI 登录到 {{site.data.keyword.cloud_notm}}。

    ```
    bx login [--sso]
    ```
    {: codeblock}

    使用联合标识登录时需要 `--sso` 参数。如果使用此选项，请转至 CLI 输出中列出的链接以生成一次性密码。

2. 选择包含您的 {{site.data.keyword.keymanagementserviceshort}} 服务实例的 {{site.data.keyword.cloud_notm}} 组织和空间。

    请记下 CLI 输出中您的组织和空间的名称。也可以运行 `bx target` 来查看此信息。

3. 检索您的 {{site.data.keyword.cloud_notm}} 组织和空间 GUID。

    ```
    bx iam org [organization_name] --guid
    bx iam space [space_name] --guid
    ```
    {: codeblock}
    将 _organization_name_ 和 _space_name_ 替换为您分配给组织和空间的唯一别名。

## 检索授权令牌
{: #retrieve_token}

您可以使用授权令牌，通过 {{site.data.keyword.keymanagementserviceshort}} API，以编程方式管理密钥。

**注**：要启用 {{site.data.keyword.iamshort}} 管理的精确访问控制，请在调用服务时使用 IAM 令牌。

1. 在 {{site.data.keyword.cloud_notm}} CLI 中，选择包含 {{site.data.keyword.keymanagementserviceshort}} 服务的组织和空间。

2. 检索并显示授权令牌。

    ```
    bx iam oauth-tokens
    ```
    {: codeblock}

    下列截断示例显示 {{site.data.keyword.cloud_notm}} 令牌输出。_Bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7_ 变量是示例访问令牌。

    ```
    IAM token: Bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7...
    UAA token: Bearer mjEyJhbGciOiJIUzI1Ni.chWyW1faWQiOiJJQkWs1...
    ```
    {: screen}

    使用 `IAM` 或 `UAA` 不记名值，通过 {{site.data.keyword.keymanagementserviceshort}} API，以编程方式管理服务中的密钥。

### 后续工作

请参阅 [{{site.data.keyword.keymanagementserviceshort}}REST API 参考文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/apidocs/639){: new_window} 以在空间中开始管理密钥。
