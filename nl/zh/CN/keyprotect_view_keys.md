---

copyright:
  years: 2017
lastupdated: "2017-09-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# 查看密钥

使用 {{site.data.keyword.keymanagementservicefull}}，可以查看加密密钥的内容。
{: shortdesc}

## 使用 GUI 查看密钥
{: #gui}

要使用 {{site.data.keyword.keymanagementserviceshort}} GUI 浏览服务中的密钥，请参阅 [{{site.data.keyword.keymanagementserviceshort}} 入门](/docs/services/keymgmt/index.html#managekey)。

## 使用 API 查看密钥
{: #api}

您可以通过使用 {{site.data.keyword.keymanagementserviceshort}} API 来检索密钥的内容。


### 步骤 1：检索密钥的集合
{: #retrieve_keys_api}

对于高级视图，可以通过向以下端点发出 `GET` 调用，浏览在空间中管理的密钥。

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys
```
{: codeblock}

1. [检索授权令牌、组织 GUID 和空间 GUID 以在该服务中使用密钥。](/docs/services/keymgmt/keyprotect_authentication.html)
2. 运行以下 cURL 命令以查看密钥的常规特征。

    ```cURL
    curl -X GET \
    https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <OAuth_token>' \
    -H 'bluemix-org: <organization_GUID>' \
    -H 'bluemix-space: <space_GUID>' \
    ```
    {: codeblock}

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
        <td>指定给您的 {{site.data.keyword.Bluemix_notm}} 空间的唯一标识。</td>
      </tr>
      <tr>
        <td><em>organization_GUID</em></td>
        <td>指定给您的 {{site.data.keyword.Bluemix_notm}} 组织的唯一标识。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. 描述通过 {{site.data.keyword.keymanagementserviceshort}} API 查看密钥所需的变量。</caption>
    </table>

    成功的请求会返回 {{site.data.keyword.Bluemix_notm}} 空间中可用的密钥集合。

    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.kms.key+json",
        "collectionTotal": 2
      },
    "resources": [
      {
      "id": "Key ID 1",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Key alias",
          "description": "Key description",
          "state": 1,
          "algorithmType": "AES",
          "createdBy": "v4 UUID of the user who creates the key",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "Key length",
            "mode": "GCM"
          }
        },
        {
          "id": "Key ID 2",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Key alias",
          "description": "Key description",
          "state": 1,
          "algorithmType": "AES",
          "createdBy": "v4 UUID of the user who creates the key",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "Key length",
            "mode": "GCM"
          }
        }
      ]
    }
    ```
    {:screen}

### 步骤 2：按标识检索密钥
{: #retrieve_key_api}

要查看特定密钥的详细信息，您可以对以下端点发出后续 `GET` 调用：

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID>
```
{: codeblock}

1. [检索授权令牌、组织 GUID 和空间 GUID 以在该服务中使用密钥。](/docs/services/keymgmt/keyprotect_authentication.html)
2. 检索您要服务或管理的密钥的标识。

    标识值用于访问密钥的更多详细信息，例如密钥资料本身。您可以发出 `GET /v2/keys` 请求或访问 {{site.data.keyword.keymanagementserviceshort}} GUI，以检索指定密钥的标识。

3. 运行以下 cURL 命令以获取有关密钥和密钥资料的详细信息。

    ```cURL
    curl -X GET \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID> \
      -H 'accept: application/vnd.ibm.kms.secret+json' \
      -H 'authorization: Bearer <OAuth_token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
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
        <td><em>OAuth_token</em></td>
        <td>您的授权令牌。请在 cURL 请求中包含令牌的完整内容，包括 Bearer 值。</td>
      </tr>
      <tr>
        <td><em>organization_GUID</em></td>
        <td>指定给您的 {{site.data.keyword.Bluemix_notm}} 组织的唯一标识。</td>
      </tr>
      <tr>
        <td><em>space_GUID</em></td>
        <td>指定给您的 {{site.data.keyword.Bluemix_notm}} 空间的唯一标识。</td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>可选：用于跟踪和关联事务的唯一标识。</td>
      </tr>
      <tr>
        <td><em>key_ID</em></td>
        <td>您在[步骤 1](#retrieve_keys_api) 中检索到的密钥的标识。</td>
      </tr>
      <caption style="caption-side:bottom;">表 2. 描述通过 {{site.data.keyword.keymanagementserviceshort}} API 查看指定密钥所需的变量。</caption>
    </table>

    成功的响应返回有关密钥和密钥资料的详细信息。以下 JSON 对象显示返回值示例。

    ```
    {
        "metadata": {
            "collectionTotal": 1,
            "collectionType": "application/vnd.ibm.kms.key+json"
        },
        "resources": [
            {
                "createdBy": "...",
                "creationDate": "...",
                "id": "...",
                "name": "...",
                "payload": "...",
                "state": 1,
                "type": "application/vnd.ibm.kms.key+json"
            }
        ]
    }
    ```
    {:screen}

    有关可用参数的详细描述，请参阅 {{site.data.keyword.keymanagementserviceshort}} [REST API 参考文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/apidocs/639){: new_window}。
