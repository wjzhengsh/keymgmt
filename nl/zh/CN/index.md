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

# {{site.data.keyword.keymanagementserviceshort}} 入门

在 {{site.data.keyword.keymanagementservicefull}} 中生成、输入和管理密钥需要以下步骤。
{: shortdesc}

## 先决条件
{: #prereqs }

对于通过正确授权，可向 {{site.data.keyword.keymanagementserviceshort}} 发出 API 调用的服务和应用程序来说，可以使用 {{site.data.keyword.keymanagementserviceshort}}。在添加密钥之前，您需要以下内容：
- [IBM 标识和密码](https://console.bluemix.net/docs/admin/adminpublic.html#signing-up-for-bluemix){: new_window}
- [服务的实例](https://console.ng.bluemix.net/catalog/services/key-protect/?taxonomyNavigation=apps){: new_window}

## 添加密钥
{: #addkey }

使用以下步骤来创建新密钥或上传现有密钥。

1. [登录到 {{site.data.keyword.cloud_notm}} 控制台。](https://console.bluemix.net/catalog){: new_window}
2. 将鼠标悬停在**所有类别**链接上，以使滚动条出现。向下滚动到**服务 > 安全**。此时将显示应用程序和服务的列表。
3. 双击 **{{site.data.keyword.keymanagementserviceshort}}** 服务实例。请注意，在**操作**下，您可以重命名或删除服务。

如果您第一次输入或生成密钥，那么您将自动位于**添加新密钥**页面。**生成新密钥**用于在 {{site.data.keyword.keymanagementserviceshort}} 中生成新密钥，而**输入现有密钥**用于将现有密钥输入到服务中。

### 生成密钥
{: #genkey }

使用以下步骤让 {{site.data.keyword.keymanagementserviceshort}} 生成新密钥。

1. 在**生成新密钥**下输入以下内容，让 {{site.data.keyword.keymanagementserviceshort}} 创建新密钥。
    <table>
      <tr>
        <th>字段</th>
        <th>描述</th>
      </tr>
      <tr>
        <td>名称</td>
        <td>要指定给密钥的可读别名。此名称可以是有助于识别密钥的任何名称，例如密钥的用途或密钥关联的对象。</td>
      </tr>
      <tr>
        <td>密钥类型</td>
        <td>缺省值为标准密钥。标准密钥用作数据加密密钥，以将纯文本数据加密为密文。</td>
      </tr>
        <caption style="caption-side:bottom;">表 1. 生成新密钥设置的描述</caption>
    </table>

2. 单击**生成密钥**按钮。密钥将立即可用。新密钥通过位于安全 {{site.data.keyword.IBM}} 数据中心的硬件安全模块生成。
3. 复制密钥行中的引用标识。**标识**值是在 {{site.data.keyword.keymanagementserviceshort}} API 中使用的标识。

### 输入现有密钥
{: #existkey }

使用以下步骤，将现有密钥输入到 Key Protect。

1. 在**输入现有密钥**下输入以下内容。
    <table>
      <tr>
        <th>字段</th>
        <th>描述</th>
      </tr>
      <tr>
        <td>名称</td>
        <td>要指定给密钥的可读别名。此名称可以是有助于识别密钥的任何名称，例如密钥的用途或密钥关联的对象。</td>
      </tr>
      <tr>
        <td>密钥类型</td>
        <td>缺省值为标准密钥。标准密钥用作数据加密密钥，以将纯文本数据加密为密文。</td>
      </tr>
      <tr>
        <td>密钥资料</td>
        <td>密钥资料可以是要存储在 {{site.data.keyword.keymanagementserviceshort}} 服务中的任何类型的数据，例如证书或 RSA 密钥。</td>
      </tr>
        <caption style="caption-side:bottom;">表 2. 输入新密钥设置的描述</caption>
    </table>

2. 单击**添加新密钥**按钮。密钥将立即可用。
3. 复制密钥行中的引用标识。**标识**值是在 {{site.data.keyword.keymanagementserviceshort}} API 中使用的标识。

## 管理密钥
{: #managekey }

要在生成和输入密钥后查看密钥，请遵循[添加密钥](index.html#addkey)下的步骤。您将位于**密钥**窗口。您的密钥将按照创建日期的顺序显示，最新的密钥位于列表最顶部。
<table>
      <tr>
        <th>列</th>
        <th>描述</th>
      </tr>
      <tr>
        <td>名称</td>
        <td>分配给密钥的可读别名。</td>
      </tr>
      <tr>
        <td>标识</td>
        <td>{{site.data.keyword.keymanagementserviceshort}} 分配给密钥的唯一密钥标识。</td>
      </tr>
      <tr>
        <td>状态</td>
        <td>其中一个美国国家标准技术学会 (NIST) 密钥状态 - 预激活、活动、已停用和已销毁。<td>
      </tr>
      <tr>
        <td>创建时间</td>
        <td>创建密钥的日期和时间。</td>
      </tr>
      <tr>
        <td>类型</td>
        <td>缺省值为标准密钥。</td>
      </tr>
      <caption style="caption-side:bottom;">表 3. 密钥窗口的描述</caption>
    </table>

### 后续工作

现在，可使用密钥对应用程序和服务进行编码。

- 要查看 {{site.data.keyword.keymanagementserviceshort}} 中的密钥存储库如何对数据进行加密和解密的示例，请[查看 Github 中的样本应用程序 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}。
- 要查找有关以编程方式管理密钥的更多信息，请参阅 [{{site.data.keyword.keymanagementserviceshort}} API 参考文档](https://console.ng.bluemix.net/apidocs/639)，以获取代码样本。

### 相关链接

- [{{site.data.keyword.keymanagementserviceshort}}REST API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/apidocs/639){: new_window}
- [{{site.data.keyword.keymanagementserviceshort}} 管理 REST API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://docs-admin-keyprotect.ng.bluemix.net/){: new_window}
- [{{site.data.keyword.cloud_notm}} HSM 产品 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.softlayer.com/ibm-cloud-hsm){: new_window}
- [{{site.data.keyword.keymanagementservicelong_notm}} 服务级别协议![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www-03.ibm.com/software/sla/sladb.nsf/sla/bm-7603-01){: new_window}
