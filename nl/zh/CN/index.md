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

# {{site.data.keyword.keymanagementserviceshort}} 入门

{{site.data.keyword.keymanagementservicelong}} 可帮助您为 {{site.data.keyword.Bluemix_short}} 中的应用程序供应加密的密钥。您在管理密钥的生命周期时，了解您的密钥受到基于云的硬件安全模块 (HSM) 的保护从而可防止信息被盗这一点很有好处。
{: shortdesc}

{{site.data.keyword.keymanagementserviceshort}} 可自动提供给已创建该服务的空间中的所有应用程序。[创建此服务的实例后](https://console.ng.bluemix.net/catalog/services/key-protect/?taxonomyNavigation=apps){: new_window}，请完成以下步骤以快速入门和熟悉运用：

1. 要创建或上传现有密钥，请单击**添加密钥**。
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
      <tr>
        <td>算法</td>
        <td>AES-GCM 算法支持对称密钥加密。</td>
      </tr>
      <tr>
        <td>密钥</td>
        <td>仅在添加现有密钥时才需要。密钥资料可以是要存储在 {{site.data.keyword.keymanagementserviceshort}} 服务中的任何类型的数据，例如证书或 RSA 密钥。</td>
      </tr>
        <caption style="caption-side:bottom;">表 1. 密钥设置的描述</caption>
    </table>

2. 当您完成填写密钥详细信息时，请单击**添加密钥**以进行确认。密钥将立即可用。新密钥通过位于安全 {{site.data.keyword.IBM}} 数据中心的硬件安全模块生成。
3. 复制密钥行中的引用标识。**标识**值是在 {{site.data.keyword.keymanagementserviceshort}} API 中使用的标识。
4. **可选**：如果要删除密钥，请记住密钥资料不可恢复。与密钥关联的元数据保存在 {{site.data.keyword.keymanagementserviceshort}} 数据库中。要删除密钥，请单击密钥行中的**操作**图标并在下一个屏幕中确认删除。

后续步骤：

现在，可使用密钥对应用程序和服务进行编码。

- 要查看 {{site.data.keyword.keymanagementserviceshort}} 中的密钥存储库如何对数据进行加密和解密的示例，请[查看 Github 中的样本应用程序 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/IBM-Bluemix/key-protect-helloworld-python "外部链接图标"){: new_window}。
- 要查找有关以编程方式管理密钥的更多信息，请参阅 [{{site.data.keyword.keymanagementserviceshort}} API 参考文档](https://console.ng.bluemix.net/apidocs/639)，以获取代码样本。

## 相关链接

- [{{site.data.keyword.keymanagementserviceshort}}REST API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/apidocs/639 "外部链接图标"){: new_window}
- [{{site.data.keyword.keymanagementserviceshort}} 管理 REST API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://docs-admin-keyprotect.ng.bluemix.net/ "外部链接图标"){: new_window}
- [Cloud HSM 产品 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.softlayer.com/ibm-cloud-hsm "外部链接图标"){: new_window}
