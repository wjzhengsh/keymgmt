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

# 删除密钥
{: #deleting-keys}

如果您是 {{site.data.keyword.cloud_notm}} 空间或 {{site.data.keyword.keymanagementserviceshort}} 服务实例的管理员，那么您可以使用 {{site.data.keyword.keymanagementservicefull}} 来删除加密密钥及其内容。
{: shortdesc}

**重要信息**：删除密钥时，会永久粉碎其内容和关联的数据。该操作无法撤销。不建议对生产环境进行销毁资源操作，但是对临时环境（如测试或 QA）可能很有用。

## 使用 GUI 删除密钥
{: #gui}

如果想要使用图形界面来删除加密密钥，那么可以使用 {{site.data.keyword.keymanagementserviceshort}} GUI。

[在您创建密钥或将现有密钥导入服务后](/docs/services/keymgmt/keyprotect_create_keys.html)，请完成以下步骤以删除密钥：

1. [登录到 {{site.data.keyword.cloud_notm}} 控制台 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.bluemix.net/)。
2. 在 {{site.data.keyword.cloud_notm}} 仪表板中，选择供应的 {{site.data.keyword.keymanagementserviceshort}} 实例。
3. 使用**密钥**表以浏览服务中的密钥。
4. 单击 ⋮ 图标以针对要删除的密钥打开选项列表。
5. 从选项菜单中，单击**删除密钥**并在下一个屏幕确认密钥删除。

删除密钥后，该密钥会转变为_已销毁_状态。处于此状态的密钥不再可恢复。与密钥关联的元数据（例如，密钥的删除日期）会保存在 {{site.data.keyword.keymanagementserviceshort}} 数据库中。

## 使用 API 删除密钥
{: #api}

要删除密钥及其内容，请向以下端点发出 `DELETE` 调用：

```
https://keyprotect.us-south.bluemix.net/api/v2/keys<key_ID>
```

1. [检索服务和认证凭证以使用服务中的密钥](/docs/services/keymgmt/keyprotect_authentication.html)。

2. 检索要删除的密钥的标识。

    可以发出 `GET /v2/keys/` 请求或在 {{site.data.keyword.keymanagementserviceshort}} 仪表板中查看密钥，以检索指定密钥的标识。

3. 运行以下 cURL 命令以永久地删除密钥及其内容。

    ```cURL
    curl -X DELETE \
      https://keyprotect.us-south.bluemix.net/api/v2/keys<key_ID> \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'prefer: <return_preference>'
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
        <td><em>key_ID</em></td>
        <td>您要删除的密钥的唯一标识。</td>
      </tr>
      <tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p>标头，用于对 <code>POST</code> 和 <code>DELETE</code> 操作的服务器行为发出警报。</p><p>将 <em>return_preference</em> 变量设置为 <code>return=minimal</code> 时，服务会返回成功删除响应。将该变量设置为 <code>return=representation</code> 时，服务会返回密钥资料和密钥元数据。</p></td>
      </tr>
      <caption style="caption-side:bottom;">表 1. 描述通过 {{site.data.keyword.keymanagementserviceshort}} API 删除密钥所需的变量。</caption>
    </table>

    如果将 _return_preference_ 变量设置为 `return=representation`，那么会在响应的 entity-body 中返回 `DELETE` 请求的详细信息。<!--After you delete a key, it enters the `Deactivated` key state. After 24 hours, if a key is not reinstated, the key transitions to the `Destroyed` state. The key contents are permanently erased and no longer accessible.--> 以下 JSON 对象显示返回值示例。
    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.kms.key+json",
       "collectionTotal": 1
     },
    "resources": [
      {
      "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "...",
          "description": "...",
          "state": 5,
          "crn": "...",
          "deleted": true,
          "algorithmType": "AES",
          "createdBy": "...",
          "deletedBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "deletionDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "nonactiveStateReason": 2,
          "extractable": true
        }
      ]
    }
    ```
    {: screen}

    有关可用参数的详细描述，请参阅 {{site.data.keyword.keymanagementserviceshort}} [REST API 参考文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/apidocs/639){: new_window}。
