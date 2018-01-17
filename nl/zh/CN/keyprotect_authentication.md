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

# 访问 API
{: #access-api}

{{site.data.keyword.keymanagementservicefull}} 提供可与任何编程语言配合使用的 REST API，以存储、检索和生成密钥。
{: shortdesc}

要使用该 API，您需要生成您的服务和认证凭证。 

## 检索访问令牌
{: #retrieve_token}

您可通过在 {{site.data.keyword.iamshort}} 中检索访问令牌，向 {{site.data.keyword.keymanagementserviceshort}} 进行认证。使用[服务标识](/docs/iam/serviceid.html)，可以代表服务或应用程序在 {{site.data.keyword.cloud_notm}} 上或其外部使用 {{site.data.keyword.keymanagementserviceshort}} API，而无需共享您的个人用户凭证。  

如果要使用用户凭证进行认证，可以通过在 [{{site.data.keyword.cloud_notm}} (bx) CLI ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](/docs/cloud-platform/cli/reference/bluemix_cli/get_started.html#getting-started){: new_window} 中运行 `bx iam oauth-tokens` 来检索令牌。
{: tip}

要检索访问令牌，请完成以下步骤：

1. 在 {{site.data.keyword.cloud_notm}} 控制台中，转至**管理** &gt; **安全性** &gt; **身份和访问权** &gt; **服务标识**。请遵循[创建服务标识](/docs/iam/serviceid.html#creating-a-service-id){: new_window}的过程。
2. 使用**操作**菜单来[为新服务标识定义访问策略](/docs/iam/serviceidaccess.html#assigning-new-access){: new_window}。 
    
    有关管理 {{site.data.keyword.keymanagementserviceshort}} 资源访问权的更多信息，请参阅[角色和许可权](/docs/services/keymgmt/keyprotect_manage_access.md#roles)。
3. 使用 **API 密钥**部分来[创建要与服务标识关联的 API 密钥](/docs/iam/serviceid_keys.html#creating-an-api-key-for-a-service-id){: new_window}。通过将 API 密钥下载到安全位置来保存该密钥。
4. 调用 {{site.data.keyword.iamshort}} API 来检索访问令牌。

    ```cURL
    curl -X POST \
      "https://iam.bluemix.net/oidc/token" \
      -H "Content-Type: application/x-www-form-urlencoded" \
      -H "Accept: application/json" \
      -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<your_API_key>" \ 
    ```
    {: codeblock}

    在请求中，将 `<API_key>` 替换为在步骤 3 中创建的 API 密钥。以下截断的示例显示令牌输出：

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

    使用完整的 `access_token` 值（以 _Bearer_ 令牌类型为前缀）通过 {{site.data.keyword.keymanagementserviceshort}} API 以编程方式管理服务的密钥。 

## 检索实例标识
{: #retrieve_instance_ID}

可以使用 [{{site.data.keyword.cloud_notm}} (bx) CLI ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](/docs/cloud-platform/cli/reference/bluemix_cli/get_started.html#getting-started){: new_window} 来检索 {{site.data.keyword.keymanagementserviceshort}} 服务实例的识别信息。使用实例标识来管理帐户中指定 {{site.data.keyword.keymanagementserviceshort}} 实例内的加密密钥。 

1. 通过 {{site.data.keyword.cloud_notm}} (bx) CLI 登录到 {{site.data.keyword.cloud_notm}}。

    ```sh
    bx login 
    ```
    {: pre}

    **注：**如果登录失败，请运行 `bx login --sso` 命令重试。使用联合标识登录时需要 `--sso` 参数。如果使用此选项，请转至 CLI 输出中列出的链接以生成一次性密码。

2. 选择包含所供应 {{site.data.keyword.keymanagementserviceshort}} 实例的帐户。

    可以运行 `bx resource service-instances` 来列出帐户中供应的所有服务实例。

3. 检索唯一标识 {{site.data.keyword.keymanagementserviceshort}} 服务实例的云资源名称 (CRN)。 

    ```sh
    bx resource service-instance <instance_name> --id
    ```
    {: pre}

    将 `<instance_name>` 替换为指定给 {{site.data.keyword.keymanagementserviceshort}} 实例的唯一别名。以下截断的示例显示 Bluemix CLI 输出。_7e8fc048-5606-4259-ad71-92397b0fa3f7_ 值是示例实例标识。

    ```
    crn:v1:bluemix:public:kms:us-south:a/7e8fc048-5606-4259-ad71-92397b0fa3f7
    ```
    {: screen}

## 构成 API 请求
{: #form_api_request}

对服务发出 API 调用时，请根据初始供应 {{site.data.keyword.keymanagementserviceshort}} 实例的方式来构造 API 请求。 

要构建请求，请将[区域服务端点](/docs/services/keymgmt/keyprotect_regions.html)与相应的认证凭证配合使用。例如，如果为 `us-south` 区域创建了服务实例，请使用以下端点和 API 头浏览服务中的密钥：

```cURL
curl -X GET \
    https://keyprotect.us-south.bluemix.net/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <access_token>' \
    -H 'bluemix-instance: <instance_ID>' \
```
{: codeblock}

### 后续工作

- 要了解有关以编程方式管理密钥的更多信息，请[查看 {{site.data.keyword.keymanagementserviceshort}} API 参考文档以获取代码样本 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/apidocs/639){: new_window}。
- 要查看 {{site.data.keyword.keymanagementserviceshort}} 中存储的密钥如何对数据进行加密和解密的示例，请[查看 GitHub 中的样本应用程序 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}。
