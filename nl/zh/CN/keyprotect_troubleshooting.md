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

# 故障诊断

下面是有关使用 {{site.data.keyword.keymanagementservicefull}} 的一些常见故障诊断问题的答案。
{: shortdesc}

## 无法创建或删除密钥
{: #unabletomanagekeys}

如果无法执行 {{site.data.keyword.keymanagementserviceshort}} 操作，请验证您是否具有正确授权。

### 症状

访问 {{site.data.keyword.keymanagementserviceshort}} 用户界面时，不能查看添加密钥或删除密钥选项。

### 解决问题

向您的管理员验证是否已在适当的空间中为您分配了正确的角色。有关角色的更多信息，请参阅[角色和许可权](/docs/services/keymgmt/keyprotect_manage_access.html#roles)。

## 从 beta 转换为通用版本 (GA)
{: #ts_planconversion}

Beta 用户需要更改为标准定价模型，才能继续使用 {{site.data.keyword.keymanagementserviceshort}} 服务。

### 症状

如果您是 beta 用户，那么需要将定价套餐更改为分层定价模型，才能继续在 {{site.data.keyword.keymanagementserviceshort}} 中存储密钥。

### 解决问题

{{site.data.keyword.keymanagementserviceshort}} 服务具有两个定价模型：Lite 和累进分层。以管理员身份，验证是否选择了累进分层模型。如果不想迁移到分层模型，请确保在弃用之前除去所有密钥和服务实例。[请参阅 {{site.data.keyword.keymanagementserviceshort}} 通用版本声明以获取更多信息 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/blogs/bluemix/2016/12/dallas-key-protect-ga/){: new_window}。

要更改定价套餐，请执行以下操作：

1. 转至 {{site.data.keyword.keymanagementserviceshort}} 用户界面，并选择**套餐**选项卡。
2. 选择**累进层定价**。这将以表形式显示每月使用的活动密钥的成本细目。分层模型在帐户级别基于每月的活动密钥数来计算定价。
3. 要确认套餐更改，请单击**保存**。

## 获取 {{site.data.keyword.keymanagementserviceshort}} 的帮助和支持
{: #ts_gettinghelp}

如果您在使用 {{site.data.keyword.keymanagementservicefull_notm}} 时有任何疑问或遇到任何问题，您可以在论坛中搜索相关信息或进行提问来获取帮助。还可以提交支持凭单。

使用论坛进行提问时，请使用适当的标记来标注您的问题，以方便 {{site.data.keyword.cloud_notm}} 开发团队识别。

- 如果有关于 {{site.data.keyword.keymanagementserviceshort}} 的技术问题，请将您的问题发布到 [Stack Overflow ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://stackoverflow.com/search?q=key-protect+ibm-bluemix){: new_window} 上，并使用“ibm-bluemix”和“key-protect”标记您的问题。
- 有关服务的问题和入门指示信息，请使用 [IBM developerWorks dW Answers ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/answers/topics/key-protect/?smartspace=bluemix){: new_window} 论坛。请包括“bluemix”和“key-protect”标记。

有关使用论坛的更多详细信息，请参阅[获取帮助 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.bluemix.net/docs/support/index.html#getting-help){: new_window}。

有关提交 {{site.data.keyword.IBM_notm}} 支持凭单或支持级别和凭单严重性的信息，请参阅[联系支持人员 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.bluemix.net/docs/support/index.html#contacting-support){: new_window}。
