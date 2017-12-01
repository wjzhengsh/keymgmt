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

# 供应 {{site.data.keyword.keymanagementserviceshort}} 服务
{: #provision}

您可以使用 {{site.data.keyword.cloud_notm}} 控制台或 {{site.data.keyword.cloud_notm}} (bx) CLI 创建 {{site.data.keyword.keymanagementservicefull}} 的安全实例。
{: shortdesc}

## 从 {{site.data.keyword.cloud_notm}} 控制台供应
{: #gui}

要从 {{site.data.keyword.cloud_notm}} 控制台供应 {{site.data.keyword.keymanagementserviceshort}} 的实例，请完成以下步骤。

1. [登录到 {{site.data.keyword.cloud_notm}} 帐户 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.bluemix.net/){: new_window}。
2. 单击**目录**以查看 {{site.data.keyword.cloud_notm}} 上可用的服务列表。
3. 选择**服务**类别，然后单击 **{{site.data.keyword.keymanagementserviceshort}}** 磁贴。
5. 选择服务套餐，然后单击**创建**，以在您登录的 {{site.data.keyword.cloud_notm}} 组织和空间中供应 {{site.data.keyword.keymanagementserviceshort}} 服务实例。

## 从 {{site.data.keyword.cloud_notm}} (bx) CLI 供应
{: #cli}

您可以使用 {{site.data.keyword.cloud_notm}} (bx) CLI 来供应 {{site.data.keyword.keymanagementserviceshort}} 的实例。[在系统上下载并安装命令行工具](https://clis.ng.bluemix.net/ui/home.html){: new_window}以完成以下步骤。

1. 登录到 {{site.data.keyword.cloud_notm}} CLI。

    ```sh
    bx login [--sso]
    ```
    {: codeblock}
    **注**：使用联合标识登录时需要 `--sso` 参数。如果使用此选项，请转至 CLI 输出中列出的链接以生成一次性密码。

2. 选择要创建 {{site.data.keyword.keymanagementserviceshort}} 服务实例的 {{site.data.keyword.cloud_notm}} 组织和空间。

    您还可以使用以下命令来设置目标组织和空间。

    ```sh
    bx target [-o organization_name] [-s space_name]
    ```
    {: codeblock}

3. 在该区域、组织和空间内供应 {{site.data.keyword.keymanagementserviceshort}} 的实例。

    ```sh
    bx service create kms TieredPricing [instance_name]
    ```
    {: codeblock}

    将 _instance_name_ 替换为服务实例的唯一别名。

4. 验证已成功创建服务实例。

    ```sh
    bx service list
    ```
    {: codeblock}


### 后续工作

现在，可使用密钥对应用程序和服务进行编码。

- 要查看 {{site.data.keyword.keymanagementserviceshort}} 中的密钥存储库如何对数据进行加密和解密的示例，请[查看 GitHub 中的样本应用程序 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}。
- 要查找有关以编程方式管理密钥的更多信息，请[检查 {{site.data.keyword.keymanagementserviceshort}} API 参考文档以获取代码样本 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/apidocs/639){: new_window}。
