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

# 查看密钥
{: #viewing-keys}

{{site.data.keyword.keymanagementservicefull}} 提供查看、管理和审计加密密钥的集中式系统。审计您的密钥和密钥的访问限制，以确保资源安全。
{: shortdesc}

定期审计密钥配置：

- 检查创建密钥的时间并确定是否需要轮询密钥。
- [使用 {{site.data.keyword.cloudaccesstrailshort}} 监视对 {{site.data.keyword.keymanagementserviceshort}} 的 API 调用 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](/docs/services/cloud-activity-tracker/svcs/kp_at.html#kp_at){: new_window}。
- 检查哪些用户对密钥具有访问权以及访问级别是否正确。

有关审计对资源的访问权的更多信息，请参阅[使用 Cloud IAM 管理用户访问权](/docs/services/keymgmt/keyprotect_manage_access.html)。

## 使用 GUI 查看密钥
{: #gui}

如果想要使用图形界面来检查服务中的密钥，那么可以使用 {{site.data.keyword.keymanagementserviceshort}} 仪表板。

[创建密钥或将现有密钥导入服务后](/docs/services/keymgmt/keyprotect_create_keys.html)，请完成以下步骤以查看密钥。

1. [登录到 {{site.data.keyword.cloud_notm}} 控制台 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.bluemix.net/)。
2. 从 {{site.data.keyword.cloud_notm}} 仪表板，选择 {{site.data.keyword.keymanagementserviceshort}} 的已供应实例。
3. 在 {{site.data.keyword.keymanagementserviceshort}} 仪表板中，浏览密钥的常规特征：

    <table>
      <tr>
        <th>列</th>
        <th>描述</th>
      </tr>
      <tr>
        <td>名称</td>
        <td>指定给密钥的人类可以阅读的唯一别名。</td>
      </tr>
      <tr>
        <td>标识</td>
        <td>{{site.data.keyword.keymanagementserviceshort}} 服务指定给密钥的唯一密钥标识。可以使用标识值通过 [{{site.data.keyword.keymanagementserviceshort}} API](https://console.ng.bluemix.net/apidocs/639) 来调用服务。</td>
      </tr>
      <tr>
        <td>状态</td>
        <td>[密钥状态](/docs/services/keymgmt/keyprotect_states.html)，基于 [NIST Special Publication 800-57 Recommendation for Key Management ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf)。这些状态包括<i>预激活</i>、<i>活动</i>、<i>已停用</i>和<i>已销毁</i>。</td>
      </tr>
      <tr>
        <td>类型</td>
        <td>[密钥类型](/docs/services/keymgmt/keyprotect_envelope.html#key_types)，用于描述服务中密钥的指定用途。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. <b>密钥</b>表的描述</caption>
    </table>

## 使用 API 查看密钥
{: #api}

您可以通过使用 {{site.data.keyword.keymanagementserviceshort}} API 来检索密钥的内容。


### 步骤 1：检索密钥的集合
{: #retrieve_keys_api}

.对于高级视图，可以通过向以下端点发出 `GET` 调用，浏览在供应的 {{site.data.keyword.keymanagementserviceshort}} 实例中管理的密钥：

```
https://key-protect.us-south.bluemix.net/api/v2/keys
```
{: codeblock}

1. [检索服务和认证凭证以使用服务中的密钥](/docs/services/keymgmt/keyprotect_authentication.html)。
2. 运行以下 cURL 命令以查看密钥的常规特征。

    ```cURL
    curl -X GET \
    https://key-protect.us-south.bluemix.net/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <IAM_token>' \
    -H 'bluemix-instance: <instance_ID>' \
    -H 'correlation-id: <correlation_ID>' \
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
        <td>可选：用于跟踪和关联事务的唯一标识。</td>
      </tr>
      <caption style="caption-side:bottom;">表 2. 描述通过 {{site.data.keyword.keymanagementserviceshort}} API 查看密钥所需的变量。</caption>
    </table>

    成功的 `POST /v2/keys/` 请求会返回 {{site.data.keyword.keymanagementserviceshort}} 服务实例中可用的密钥的集合。

    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.collection+json",
        "collectionTotal": 2
      },
    "resources": [
      {
      "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Standard key",
          "description": "...",
          "state": 1,
          "crn": "...",
          "algorithmType": "AES",
          "createdBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "256",
            "mode": "GCM"
          },
          "extractable": true
        },
        {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Root key",
          "description": "...",
          "state": 1,
          "crn": "...",
          "algorithmType": "AES",
          "createdBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "256",
            "mode": "GCM"
          },
          "extractable": false
        }
      ]
    }
    ```
    {:screen}

### 步骤 2：按标识检索密钥
{: #retrieve_key_api}

要查看特定密钥的详细信息，您可以对以下端点发出后续 `GET` 调用：

```
https://key-protect.us-south.bluemix.net/api/v2/keys<key_ID>
```
{: codeblock}

1. [检索服务和认证凭证以使用服务中的密钥](/docs/services/keymgmt/keyprotect_authentication.html)。
2. 检索您要服务或管理的密钥的标识。

    标识值用于访问密钥的更多详细信息，例如密钥资料本身。您可以发出 `GET /v2/keys` 请求或访问 {{site.data.keyword.keymanagementserviceshort}} GUI，以检索指定密钥的标识。

3. 运行以下 cURL 命令以获取有关密钥和密钥资料的详细信息。

    ```cURL
    curl -X GET \
      https://key-protect.us-south.bluemix.net/api/v2/keys<key_ID> \
      -H 'accept: application/vnd.ibm.kms.key+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

    根据下表替换示例请求中的变量。

    <table>
      <tr>
        <th>变量</th>
        <th>描述</th>
      </tr>
      <tr>
        <td><em>IAM_token</em></td>
        <td>您的授权令牌。在 cURL 请求中包含 `IAM` 令牌的完整内容，包括 Bearer 值。</td>
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
        <td><em>key_ID</em></td>
        <td>您在[步骤 1](#retrieve_keys_api) 中检索到的密钥的标识。</td>
      </tr>
      <caption style="caption-side:bottom;">表 3. 描述通过 {{site.data.keyword.keymanagementserviceshort}} API 查看指定密钥所需的变量。</caption>
    </table>

    成功的 `GET v2/keys/<key_ID>` 响应会返回有关密钥和密钥资料的详细信息。以下 JSON 对象显示标准密钥的示例返回值。

    ```
    {
        "metadata": {
            "collectionTotal": 1,
            "collectionType": "application/vnd.ibm.kms.key+json"
        },
    "resources": [
      {
      "id": "...",
            "type": "application/vnd.ibm.kms.key+json",
            "name": "Standard key",
            "description": "...",
            "state": 1,
            "crn": "...",
            "algorithmType": "AES",
            "payload": "...",
            "createdBy": "...",
            "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
            "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
            "algorithmMetadata": {
                "bitLength": "256",
                "mode": "GCM"
            },
            "extractable": true
        }
      ]
    }
    ```
    {:screen}

    有关可用参数的详细描述，请参阅 {{site.data.keyword.keymanagementserviceshort}} [REST API 参考文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/apidocs/639){: new_window}。
