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

# 创建标准密钥
{: #create_standard_keys}

可以使用 {{site.data.keyword.keymanagementserviceshort}} GUI 来创建标准加密密钥，也可以使用 {{site.data.keyword.keymanagementserviceshort}} API 以编程方式来创建标准加密密钥。
{: shortdesc}

## 使用 GUI 创建标准密钥
{: #create_standard_key_GUI}

[创建服务的实例后](/docs/services/keymgmt/keyprotect_provision.html)，请完成以下步骤以使用 {{site.data.keyword.keymanagementserviceshort}} GUI 来创建标准密钥。

1. [登录到 {{site.data.keyword.cloud_notm}} 控制台 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.bluemix.net/)。
2. 从 {{site.data.keyword.cloud_notm}} 仪表板，选择 {{site.data.keyword.keymanagementserviceshort}} 的已供应实例。
2. 要创建新密钥，请单击**添加密钥**，然后选择**生成新密钥**窗口。

    指定密钥的详细信息：


    <table>
      <tr>
        <th>设置</th>
        <th>描述</th>
      </tr>
      <tr>
        <td>名称</td>
        <td>要指定给密钥的可读别名。此名称可以是有助于识别密钥的任何名称，例如密钥的用途或密钥关联的对象。</td>
      </tr>
      <tr></tr>
        <td>密钥类型</td>
        <td>要在 {{site.data.keyword.keymanagementserviceshort}} 中管理的[密钥类型](/docs/services/keymgmt/keyprotect_envelope.html#key_types)。从密钥类型列表中，选择<b>标准密钥</b>。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. <b>生成新密钥</b>设置的描述</caption>
    </table>

3. 填写完密钥详细信息后，单击**生成密钥**以进行确认。 

## 使用 API 创建标准密钥
{: #create_standard_key_API}

通过对以下端点发出 `POST` 调用来创建标准密钥：

```
https://keyprotect.us-south.bluemix.net/api/v2/keys
```
{: codeblock}

1. [检索服务和认证凭证以使用服务中的密钥](/docs/services/keymgmt/keyprotect_authentication.html)。

2. 使用以下 cURL 命令调用 [{{site.data.keyword.keymanagementserviceshort}} API](https://console.ng.bluemix.net/apidocs/639)。

    ```cURL
    curl -X POST \
      https://keyprotect.us-south.bluemix.net/api/v2/keys \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
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
       "extractable": true
       }
     ]
    }'
    ```
    {: codeblock}

    要使用帐户中指定 Cloud Foundry 组织和空间内的密钥，请将 `Bluemix-Instance` 替换为相应的 `Bluemix-org` 和 `Bluemix-space` 头。[请参阅 {{site.data.keyword.keymanagementserviceshort}} API 参考文档以获取代码样本 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/apidocs/639){: new_window}。
    {: tip}

    根据下表替换示例请求中的变量。
    <table>
      <tr>
        <th>变量</th>
        <th>描述</th>
      </tr>
      <tr>
        <td><em>IAM_token</em></td>
        <td>您的授权令牌。在 cURL 请求中包含 <code>IAM</code> 令牌的完整内容，包括 Bearer 值。</td>
      </tr>
      <tr>
        <td><em>instance_ID</em></td>
        <td>指定给您的 {{site.data.keyword.keymanagementserviceshort}} 服务实例的唯一标识。</td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>用于跟踪和关联事务的唯一标识。</td>
      </tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p>可选：标头，用于对 <code>POST</code> 和 <code>DELETE</code> 操作的服务器行为发出警报。</p><p>将 <em>return_preference</em> 变量设置为 <code>return=minimal</code> 时，服务在响应的 entity-body 中仅返回密钥元数据，如密钥名称和标识值。将该变量设置为 <code>return=representation</code> 时，服务会返回标准密钥的密钥资料和密钥元数据。</p></td>
      </tr>
      <tr>
        <td><em>key_alias</em></td>
        <td>密钥的人类可以阅读的唯一名称，以便可轻松识别密钥。</td>
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
        <td><em>key_type</em></td>
        <td>
          <p>布尔值，用于确定密钥资料是否可以离开服务。</p>
          <p>将 <code>extractable</code> 属性设置为 <code>true</code> 时，服务会创建可存储在应用程序或服务中的标准密钥。</p>
        </td>
      </tr>
        <caption style="caption-side:bottom;">表 2. 使用 {{site.data.keyword.keymanagementserviceshort}} API 添加标准密钥所需的变量</caption>
    </table>

    成功的 `POST /v2/keys/` 响应会返回密钥的标识值以及其他元数据。标识是指定给密钥的唯一标识，用于后续调用 {{site.data.keyword.keymanagementserviceshort}} API。

3. 可选：通过运行以下调用来获取 {{site.data.keyword.keymanagementserviceshort}} 服务实例中的密钥，以验证是否创建了密钥。

    ```cURL
    curl -X GET \
      https://keyprotect.us-south.bluemix.net/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}


### 后续工作

- 要了解有关以编程方式管理密钥的更多信息，请[查看 {{site.data.keyword.keymanagementserviceshort}} API 参考文档以获取代码样本 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/apidocs/639){: new_window}。
- 要查看 {{site.data.keyword.keymanagementserviceshort}} 中存储的密钥如何对数据进行加密和解密的示例，请[查看 GitHub 中的样本应用程序 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}。
