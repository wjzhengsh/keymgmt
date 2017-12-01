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

# 创建密钥

您可以通过使用 {{site.data.keyword.keymanagementservicefull}} 来管理密钥生命周期。
{: shortdesc}

一个好的作法是开发代码时安全地管理密钥。例如，在考虑其他安全编码实践时，请考虑以下准则。


- 将密钥嵌入代码时考虑安全方面的影响。
- 仅针对通过编程方式访问应用程序和资源创建密钥。如果可授予更为简单的[用户许可权 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.bluemix.net/docs/admin/patterns.html#userroles){: new_window}，请勿创建密钥。
- 轮换使用密钥并除去未使用的密钥。
- 使用多因子认证执行敏感操作。
- 通过针对每个应用程序使用不同密钥将应用程序隔开。
- 传输高度敏感的信息时，考虑使用程序化 API。

如果要在添加自己的密钥之前先试用服务，请查看[样本应用程序 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}

## 使用 GUI 创建密钥
{: #gui}

要使用 {{site.data.keyword.keymanagementserviceshort}} GUI 向服务添加密钥，请参阅 [{{site.data.keyword.keymanagementserviceshort}} 入门](/docs/services/keymgmt/index.html#addkey)。

## 使用 API 创建密钥
{: #api}

您可以使用 {{site.data.keyword.keymanagementserviceshort}} API 以编程方式保护现有密钥或生成新密钥。

通过对以下端点执行 `POST` 调用，创建密钥或导入现有密钥：

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys
```
{: codeblock}

1. [检索授权令牌、组织 GUID 和空间 GUID 以在该服务中使用密钥。](/docs/services/keymgmt/keyprotect_authentication.html)

2. 使用以下 cURL 命令调用 [{{site.data.keyword.keymanagementserviceshort}} API](https://console.ng.bluemix.net/apidocs/639)。

    ```cURL
    curl -X POST \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
      -H 'authorization: Bearer <OAuth_token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
      -H 'content-type: application/vnd.ibm.kms.key+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
     "metadata": {
"collectionType": "application/vnd.ibm.kms.key+json",
       "collectionTotal": 1
     },
    "resources": [
      {
      "type": "application/vnd.ibm.kms.key+json",
       "name": "<key_alias>",
       "description": "<key_description>",
       "expirationDate": "<YYYY-MM-DDTHH:MM:SS.SSZ>",
       "payload": "<key_material>"
       }
     ]
    }'
    ```
    {: codeblock}

    根据下表替换示例请求中的变量。<table>
      <tr>
        <th>变量</th>
        <th>描述</th>
      </tr>
      <tr>
        <td><em>OAuth_token</em></td>
        <td>您的授权令牌。请在 cURL 请求中包含令牌的完整内容，包括 Bearer 值。</td>
      </tr>
      <tr>
        <td><em>organization_GUID</em></td>
        <td>指定给您的 {{site.data.keyword.cloud_notm}} 组织的唯一标识。</td>
      </tr>
      <tr>
        <td><em>space_GUID</em></td>
        <td>指定给您的 {{site.data.keyword.cloud_notm}} 空间的唯一标识。</td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>用于跟踪和关联事务的唯一标识。</td>
      </tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p>标头，用于对 <code>POST</code> 和 <code>DELETE</code> 操作的服务器行为发出警报。</p><p>如果设置为 <code>return=minimal</code>，那么该服务仅会在响应 entity-body 中返回密钥元数据，如密钥名称和 <code>id</code> 值。如果设置为 <code>return=representation</code>，那么该服务会返回密钥资料和密钥元数据。</p></td>
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
        <td>可选：密钥在系统中到期的日期和时间（RFC 3339 格式）。如果忽略了 <code>expirationDate</code> 属性，那么密钥不会到期。</td>
      </tr>
      <tr>
        <td><em>key_material</em></td>
        <td>要在 {{site.data.keyword.keymanagementserviceshort}} 中存储的密钥资料（例如，RSA 密钥）。要生成新密钥，请省略 <code>payload</code> 属性和 <em>key_material</em> 变量。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. 通过 {{site.data.keyword.keymanagementserviceshort}} API 添加密钥所需的变量</caption>
    </table>

    成功的响应返回密钥的 `id` 值以及其他元数据。`id` 是分配给密钥的唯一标识，用于后续调用。

3. **可选：**通过运行以下调用获取 {{site.data.keyword.cloud_notm}} 空间中的密钥，以验证是否创建了密钥。

    ```cURL
    curl -X GET \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <OAuth-token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
    ```
    {: codeblock}

### 后续工作

现在，可使用密钥对应用程序和服务进行编码。

- 有关每个 REST 请求和响应的完整详细信息，请检查 {{site.data.keyword.keymanagementserviceshort}} [REST API 参考文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/apidocs/639){: new_window}。
