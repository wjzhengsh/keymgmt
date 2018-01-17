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

# 打包密钥
{: #wrapping-keys}

如果您是特权用户，那么可以使用 {{site.data.keyword.keymanagementservicelong}} API 通过根密钥来管理和保护加密密钥。
{: shortdesc}

使用根密钥打包数据加密密钥 (DEK) 时，{{site.data.keyword.keymanagementserviceshort}} 结合了多种算法的优势来保护加密数据的隐私性和完整性。  

要了解密钥打包如何帮助您控制云中静态数据的安全性，请参阅[包络加密](/docs/services/keymgmt/keyprotect_envelope.html)。

## 使用 API 打包密钥
{: #api}

可以使用在 {{site.data.keyword.keymanagementserviceshort}} 中管理的根密钥来保护指定的数据加密密钥 (DEK)。

**重要信息：**提供用于打包的根密钥时，请确保根密钥为 256 位、384 位或 512 位，这样打包调用才能成功。如果在服务中创建根密钥，那么 {{site.data.keyword.keymanagementserviceshort}} 将从其 HSM 生成 AES-GCM 算法支持的 256 位密钥。

[指定服务中的根密钥后](/docs/services/keymgmt/keyprotect_create_keys.html)，可以对以下端点发出 `POST` 调用通过高级加密来打包 DEK：

```
https://keyprotect.us-south.bluemix.net/api/v2/keys<key_ID>?action=wrap
```
{: codeblock}

1. [检索服务和认证凭证以使用服务中的密钥](/docs/services/keymgmt/keyprotect_authentication.html)。

2. 复制要管理和保护的 DEK 的密钥资料。

    如果您具有对 {{site.data.keyword.keymanagementserviceshort}} 服务实例的管理员或编辑者特权，那么[可以通过发出 `GET /v2/keys/<key_ID>` 请求来检索特定密钥的密钥资料](/docs/services/keymgmt/keyprotect_view_keys.md#retrieve_key_api)。

3. 复制要用于打包的根密钥的标识。

4. 运行以下 cURL 命令以使用打包操作保护密钥。

    ```cURL
    curl -X POST \
      'https://keyprotect.us-south.bluemix.net/api/v2/keys<key_ID>?action=wrap' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
      "plaintext": "<data_key>",
      "aad": ["<additional_data>", "<additional_data>"]
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
        <td><em>key_ID</em></td>
        <td>要用于打包的根密钥的唯一标识。根密钥必须为 256 位、384 位或 512 位，这样打包调用才能成功。</td>
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
        <td>可选：用于跟踪和关联事务的唯一标识。</td>
      </tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p>标头，用于对 <code>POST</code> 和 <code>DELETE</code> 操作的服务器行为发出警报。</p><p>将 <em>return_preference</em> 变量设置为 <code>return=minimal</code> 时，服务在响应的 entity-body 中仅返回密钥元数据，如密钥名称和标识值。将该变量设置为 <code>return=representation</code> 时，服务会返回密钥资料和密钥元数据。</p></td>
      </tr>
      <tr>
        <td><em>data_key</em></td>
        <td>可选：要管理和保护的 DEK 的密钥资料。<code>plaintext</code> 值必须采用 base64 编码。要生成新的 DEK，请省略 <code>plaintext</code> 属性。服务会生成随机明文（32 个字节）并对该值进行打包。</td>
      </tr>
      <tr>
        <td><em>additional_data</em></td>
        <td>可选：用于进一步确保密钥安全的附加认证数据 (AAD)。每个字符串可含有最多 255 个字符。如果在向服务发出打包调用时提供了 AAD，那么在随后的解包调用期间必须指定同一 AAD。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. 描述对 {{site.data.keyword.keymanagementserviceshort}} 中的指定密钥进行打包所需的变量。</caption>
    </table>

    打包的密钥（包含 base64 编码的密钥资料）会在响应的 entity-body 中返回。以下 JSON 对象显示返回值示例。

    ```
    {
      "plaintext": "s~Rz@kN9Fzv\\/hP*r3LY-?O@!!qdtj:L",
      "ciphertext": "eyJjaXBoZXJ0ZXh0Ijoic3VLSDNRcmdEZjdOZUw4Rkc4L2FKYjFPTWcyd3A2eDFvZlA4MEc0Z1B2RmNrV2g3cUlidHphYXU0eHpKWWoxZyIsImhhc2giOiJiMmUyODdkZDBhZTAwZGZlY2Q3OGJmMDUxYmNmZGEyNWJkNGUzMjBkYjBhN2FjNzVhMWYzZmNkMDZlMjAzZWYxNWM5MTY4N2JhODg2ZWRjZGE2YWVlMzFjYzk2MjNkNjA5YTRkZWNkN2E5Y2U3ZDc5ZTRhZGY1MWUyNWFhYWM5MjhhNzg3NmZjYjM2NDFjNTQzMTZjMjMwOGY2MThlZGM2OTE3MjAyYjA5YTdjMjA2YzkxNTBhOTk1NmUxYzcxMTZhYjZmNmQyYTQ4MzZiZTM0NTk0Y2IwNzJmY2RmYTk2ZSJ9"
      "aad": ["data1", "data2"]
    }
    ```
    {:screen}
