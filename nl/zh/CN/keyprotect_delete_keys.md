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

# 删除密钥

如果您是 {{site.data.keyword.cloud_notm}} 空间或 {{site.data.keyword.keymanagementserviceshort}} 服务实例的管理员，那么您可以使用 {{site.data.keyword.keymanagementservicefull}} 来删除加密密钥及其内容。
{: shortdesc}

**重要事项**：当您删除密钥时，您会永久地销毁其内容和相关联的数据。该操作无法撤销。不建议对生产环境进行销毁资源操作，但是对临时环境（如测试或 QA）可能很有用。

## 使用 GUI 删除密钥
{: #gui}

如果您想要使用图形界面来删除密钥资源，那么您可以使用 {{site.data.keyword.keymanagementserviceshort}} GUI。

[在您创建密钥或将现有密钥导入服务后](/docs/services/keymgmt/keyprotect_create_keys.html)，请完成以下步骤以删除密钥：

1. [登录到 {{site.data.keyword.cloud_notm}} 控制台 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.bluemix.net/)。
2. 从 {{site.data.keyword.cloud_notm}} 仪表板，选择 {{site.data.keyword.keymanagementserviceshort}} 的已供应实例。
3. 导航到**管理**窗格以在服务中浏览密钥。
4. 单击垂直省略符图标以针对您要删除的密钥，打开选项列表。
5. 从选项菜单中，单击**删除密钥**并在下一个屏幕确认密钥删除。

## 使用 API 删除密钥
{: #api}

要删除密钥及其内容，请向以下端点发出 `DELETE` 调用：

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID>
```

1. [检索授权令牌、组织 GUID 和空间 GUID 以在该服务中使用密钥。](/docs/services/keymgmt/keyprotect_authentication.html)

2. 检索您要删除的密钥的标识。

    您可以发出 `GET /v2/keys` 请求或在 {{site.data.keyword.keymanagementserviceshort}} 仪表板中查看密钥，以检索指定密钥的标识。

3. 运行以下 cURL 命令以永久地删除密钥及其内容。

    ```cURL
    curl -X DELETE \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID> \
      -H 'authorization: Bearer <OAuth_token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
      -H 'prefer: <return_preference>'
    ```
    根据下表替换示例请求中的变量。
    <table>
      <tr>
        <th>变量</th>
        <th>描述</th>
      </tr>
      <tr>
        <td><em>OAuth_token</em></td>
        <td>您的授权令牌。请在 cURL 请求中包含令牌的完整内容，包括 Bearer 值。</td>
      </tr>
      <tr>
        <td><em>space_GUID</em></td>
        <td>指定给您的 {{site.data.keyword.cloud_notm}} 空间的唯一标识。</td>
      </tr>
      <tr>
        <td><em>organization_GUID</em></td>
        <td>指定给您的 {{site.data.keyword.cloud_notm}} 组织的唯一标识。</td>
      </tr>
      <tr>
        <td><em>key_ID</em></td>
        <td>您要删除的密钥的唯一标识。</td>
      </tr>
      <tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p>标头，用于对 <code>POST</code> 和 <code>DELETE</code> 操作的服务器行为发出警报。</p><p>如果设置为 <code>return=minimal</code>，那么该服务仅会在响应 entity-body 中返回密钥元数据，如密钥名称和 <code>id</code> 值。如果设置为 <code>return=representation</code>，那么该服务会返回密钥资料和密钥元数据。</p></td>
      </tr>
      <caption style="caption-side:bottom;">表 1. 描述通过 {{site.data.keyword.keymanagementserviceshort}} API 删除密钥所需的变量。</caption>
    </table>

    `DELETE` 请求的详细信息在响应的 entity-body 中返回。
