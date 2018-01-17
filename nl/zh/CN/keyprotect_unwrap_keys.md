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

# 解包密钥
{: #unwrapping-keys}

如果您是特权用户，那么可以使用 {{site.data.keyword.keymanagementservicefull}} API 将数据加密密钥 (DEK) 解包以访问其内容。解包 DEK 会解密其内容并检查内容完整性，从而将原始密钥资料返回给 {{site.data.keyword.cloud_notm}} 数据服务。
{: shortdesc}

要了解密钥打包如何帮助您控制云中静态数据的安全性，请参阅[包络加密](/docs/services/keymgmt/keyprotect_envelope.html)。

## 使用 API 解包密钥
{: #api}

[对服务发出打包调用后](/docs/services/keymgmt/keyprotect_wrap_keys.html)，可以通过对以下端点发出 `POST` 调用来将指定的数据加密密钥 (DEK) 解包以访问其内容：

```
https://keyprotect.us-south.bluemix.net/api/v2/keys<key_id>?action=unwrap
```
{: codeblock}

1. [检索服务和认证凭证以使用服务中的密钥](/docs/services/keymgmt/keyprotect_authentication.html)。

2. 复制用于执行初始打包请求的根密钥的标识。

    可以发出 `GET /v2/keys/` 请求或在 {{site.data.keyword.keymanagementserviceshort}} GUI 中查看密钥，以检索密钥的标识。

3. 复制在初始打包请求期间返回的 `ciphertext` 值。

4. 运行以下 cURL 命令以对密钥资料进行解密和认证。

    ```cURL
    curl -X POST \
      'https://keyprotect.us-south.bluemix.net/api/v2/keys<key_ID>?action=unwrap' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
      "ciphertext": "<encrypted_data_key>",
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
        <td>用于打包的根密钥的唯一标识。要确保解包请求成功，请提供在初始打包请求期间使用的同一根密钥。</td>
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
        <td><em>additional_data</em></td>
        <td>可选：用于进一步确保密钥安全的附加认证数据 (AAD)。每个字符串可含有最多 255 个字符。<br></br>重要信息：如果在向服务发出打包调用时提供了 AAD，那么在解包调用期间必须指定同一 AAD。</td>
      </tr>
      <tr>
        <td><em>encrypted_data_key</em></td>
        <td>打包操作期间返回的 <code>ciphertext</code> 值。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. 描述对 {{site.data.keyword.keymanagementserviceshort}} 中的密钥进行解包所需的变量。</caption>
    </table>

    原始密钥资料会在响应的 entity-body 中返回。以下 JSON 对象显示返回值示例。

    ```
    {
      "plaintext": "s~Rz@kN9Fzv\\/hP*r3LY-?O@!!qdtj:L"
    }
    ```
    {:screen}
