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

# 管理密钥

您可以通过使用 {{site.data.keyword.keymanagementservicelong}} for {{site.data.keyword.Bluemix_short}} 来管理密钥生命周期。
{: shortdesc}

一个好的作法是开发代码时安全地管理密钥。例如，在考虑其他安全编码实践时，请考虑以下类型的准则。


- 将密钥嵌入代码时考虑安全方面的影响。
- 仅针对通过编程方式访问应用程序和资源创建密钥。如果可授予更为简单的[用户许可权 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.bluemix.net/docs/admin/patterns.html#userroles "外部链接图标"){: new_window}，请勿创建密钥。
- 轮换使用密钥并除去未使用的密钥。
- 使用多因子认证执行敏感操作。
- 通过针对每个应用程序使用不同密钥将应用程序隔开。
- 传输高度敏感的信息时，考虑使用程序化 API。

## 生成 {{site.data.keyword.keymanagementserviceshort}} API 的认证凭证
{: #authentication_api}

{{site.data.keyword.keymanagementservicelong_notm}} 提供可与任何编程语言配合使用的 REST API，以存储、检索和生成密钥。

要使用 API，需要生成认证凭证和服务凭证。

1. 通过 Cloud Foundry CLI 登录到 {{site.data.keyword.Bluemix_notm}}。

    ```
    cf login [a api.DomainName] [-sso]
    ```
    {: codeblock}

2. 选择包含您的 Key Protect 服务实例的 {{site.data.keyword.Bluemix_notm}} 组织和空间。
请记下 CLI 输出中您的组织和空间的名称。也可以运行 `cf target` 来查看此信息。
3. 检索您的 {{site.data.keyword.Bluemix_notm}} 组织和空间 GUID。

    ```
    cf org organization_name --guid
    cf space space_name --guid
    ```
    {: codeblock}

4. 请求 {{site.data.keyword.Bluemix_notm}} 访问令牌。

    ```
cf oauth-token
```
    {: codeblock}

    下列截断示例显示 {{site.data.keyword.Bluemix_notm}} 令牌输出。_bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7_ 变量是示例访问令牌。

    ```
bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7...
```
    {: screen}

接下来执行的操作：

请参阅 {{site.data.keyword.keymanagementserviceshort}} [REST API 参考文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/apidocs/639 "外部链接图标"){: new_window} 以在空间中开始管理密钥。


## 使用 {{site.data.keyword.keymanagementserviceshort}} API 创建密钥
{: #codingapps}

您可以使用 {{site.data.keyword.keymanagementservicelong_notm}} API 保护现有密钥或生成新密钥。

通过对以下端点执行 **POST** 调用，创建密钥或添加现有密钥：

```
https://ibm-key-protect.edge.bluemix.net/api/v2/secrets
```
{: codeblock}

如果要在添加自己的密钥之前先试用服务，请查看[样本应用程序 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/IBM-Bluemix/key-protect-helloworld-python "外部链接图标"){: new_window}。

1. [检索 {{site.data.keyword.Bluemix_notm}} 访问令牌、组织 GUID 和空间 GUID 以在该服务中使用密钥](#authentication_api)。

2. 使用以下 cURL 命令调用 [{{site.data.keyword.keymanagementserviceshort}} API](https://console.ng.bluemix.net/apidocs/639)。

  ```cURL
  curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: bluemix_access_token' --header 'Bluemix-Space: space_GUID' --header 'Bluemix-Org: organization_GUID' -d '{
    "metadata": {
"collectionType": "application/vnd.ibm.kms.secret+json",
      "collectionTotal": 1
    },
    "resources": [
      {
      "type": "application/vnd.ibm.kms.secret+json",
      "name": "key_alias",
      "description": "key_description",
      "expirationDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
      "payload": "key_contents"
      }
    ]
  }' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets'
```
  {: codeblock}

  根据下表替换示例请求中的变量。

  <table>
    <tr>
      <th>变量</th>
      <th>描述</th>
    </tr>
    <tr>
      <td><em>bluemix_access_token</em></td>
      <td>您的授权令牌。请在 cURL 请求中包含令牌的完整内容，包括 Bearer 值。</td>
    </tr>
    <tr>
      <td><em>space_GUID</em></td>
      <td>{{site.data.keyword.Bluemix_notm}} 空间的标识。</td>
    </tr>
    <tr>
      <td><em>organization_GUID</em></td>
      <td>{{site.data.keyword.Bluemix_notm}} 组织的标识。</td>
    </tr>
    <tr>
      <td><em>key_alias</em></td>
      <td>密钥的可读名称，以便于轻松识别。</td>
    </tr>
    <tr>
      <td><em>key_description</em></td>
      <td>密钥的详细描述。</td>
    </tr>
    <tr>
      <td><em>YYYY-MM-DD</em><br><em>HH:MM:SS.SS</em></td>
      <td>可选：密钥在系统中到期的日期和时间（RFC3339 格式）。如果忽略了 <code>expirationDate</code> 属性，那么密钥不会到期。</td>
    </tr>
    <tr>
      <td><em>key_contents</em></td>
      <td>要在 {{site.data.keyword.keymanagementserviceshort}} 中存储的密钥资料（例如，RSA 密钥）。要生成新密钥，请省略 payload 属性和 key_contents 变量。</td>
    </tr>
      <caption style="caption-side:bottom;">表 1. 通过 {{site.data.keyword.keymanagementserviceshort}} API 添加密钥所需的变量</caption>
  </table>

3. 通过运行以下调用获取 {{site.data.keyword.Bluemix_notm}} 空间中的密钥，以验证是否创建了密钥。

  ```cURL
  curl -X GET --header 'Accept: application/json' --header 'Authorization: bluemix_access_token' --header 'Bluemix-Space: space_GUID' --header 'Bluemix-Org: organization_GUID' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets'
  ```
  {: codeblock}

## 使用 {{site.data.keyword.keymanagementserviceshort}} API 查看密钥
{: #viewingkeys_api}

如果您是 {{site.data.keyword.Bluemix_notm}} 空间管理员或开发者，可以通过 {{site.data.keyword.keymanagementservicelong_notm}} API 查看密钥内容。

对于高级别视图，可以通过 {{site.data.keyword.keymanagementserviceshort}} UI 浏览您的空间中管理的密钥。

通过对以下端点执行 GET 调用，查看有关密钥的详细信息：

```
https://ibm-key-protect.edge.bluemix.net/api/v2/secrets/key_ID
```
{: codeblock}

1. 从 {{site.data.keyword.keymanagementserviceshort}} UI 的安全服务下，可以查看有关密钥的常规特征。您可以通过单击可排序列标题浏览密钥。
2. 复制密钥行中的**标识**。标识值用于访问有关 API 中密钥的更多详细信息，例如密钥资料本身。
3. [检索 {{site.data.keyword.Bluemix_notm}} 访问令牌、组织 GUID 和空间 GUID 以在该服务中使用密钥。](#authentication_api)
4. 运行以下 cURL 命令以获取有关密钥和密钥资料的详细信息。

  ```cURL
  curl -X GET --header 'Accept: application/json' --header 'Authorization: bluemix_access_token' --header 'Bluemix-Space: space_GUID' --header 'Bluemix-Org: organization_GUID' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets/key_ID'
  ```
  {: codeblock}

  根据下表替换示例请求中的变量。

  <table>
    <tr>
      <th>变量</th>
      <th>描述</th>
    </tr>
    <tr>
      <td><em>bluemix_access_token</em></td>
      <td>您的授权令牌。请在 cURL 请求中包含令牌的完整内容，包括 Bearer 值。</td>
    </tr>
    <tr>
      <td><em>space_GUID</em></td>
      <td>指定给您的 {{site.data.keyword.Bluemix_notm}} 空间的随机生成的标识。</td>
    </tr>
    <tr>
      <td><em>organization_GUID</em></td>
      <td>指定给您的 {{site.data.keyword.Bluemix_notm}} 组织的随机生成的标识。</td>
    </tr>
    <tr>
      <td><em>key_ID</em></td>
      <td>针对步骤 [2](https://console.bluemix.net/docs/services/keymgmt/managing.html#viewingkeys_api__keyid) 中拉取的密钥的标识。</td>
    </tr>
    <caption style="caption-side:bottom;">表 2. 描述通过 {{site.data.keyword.keymanagementserviceshort}} API 查看密钥所需的变量。</caption>
  </table>

  密钥资料在响应的 entity-body 中返回。通过硬件安全模块 (HSM) 生成的密钥使用 base-64 编码。

## 审计密钥和访问权
{: #viewkeyassignments}

{{site.data.keyword.keymanagementservicelong_notm}} 提供查看、管理和审计加密密钥的集中式系统。审计您的密钥和密钥的访问限制，以确保资源安全。

定期审计密钥配置：

- 检查创建密钥的时间并确定是否需要轮询密钥。
- [使用 {{site.data.keyword.cloudaccesstrailshort}} 监视对 {{site.data.keyword.keymanagementserviceshort}} 的调用 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.bluemix.net/docs/services/AccessTrail/at_integration.html#at_integration_key_protect "外部链接图标"){: new_window}。
- 检查哪些用户对密钥具有访问权以及访问级别是否正确。

要审计具有访问权的用户，请执行以下操作：

1. 以空间管理员身份转至您的帐户设置，并选择**管理组织**。
2. 打开包含 {{site.data.keyword.keymanagementserviceshort}} 服务实例的空间，以检查哪些用户有权访问。
3. 如果需要添加用户，请转至**邀请团队成员**，然后选择与要授予该用户的 {{site.data.keyword.keymanagementserviceshort}} 许可权对应的 {{site.data.keyword.Bluemix_notm}} 角色：

  <table>
    <tr>
      <th>{{site.data.keyword.Bluemix_notm}} 角色</th>
      <th>{{site.data.keyword.keymanagementserviceshort}} 许可权</th>
    </tr>
    <tr>
      <td>空间管理员</td>
      <td>空间管理器可以创建、查看和删除密钥。</td>
    </tr>
    <tr>
      <td>开发人员</td>
      <td>开发人员可以创建密钥并查看密钥详细信息。</td>
    </tr>
    <tr>
      <td>审计员</td>
      <td>审计员可以访问密钥的高级视图。</td>
    </tr>
    <caption style="caption-side:bottom;">表 3. {{site.data.keyword.Bluemix_notm}} 角色与 {{site.data.keyword.keymanagementserviceshort}} 许可权的映射。</caption>
  </table>
