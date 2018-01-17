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

# 区域和位置
{: #regions-and-locations}

您可以通过指定区域服务端点来连接应用程序和 {{site.data.keyword.keymanagementservicelong_notm}} 服务。
{: shortdesc}

## 可用区域
{: #regions}

{{site.data.keyword.keymanagementserviceshort}} 在以下区域中可用：

- 美国南部
- 英国  

## 服务端点
{: #endpoints}

如果是以编程方式管理 {{site.data.keyword.keymanagementserviceshort}} 资源，请参阅下表以确定连接到 [{{site.data.keyword.keymanagementserviceshort}} API](https://console.ng.bluemix.net/apidocs/639) 时要使用的 API 端点： 

<table>
    <tr>
        <th>区域</th>
        <th>API 端点</th>
    </tr>
    <tr>
        <td>美国南部</td>
        <td>
            <code>https://keyprotect.us-south.bluemix.net</code>
        </td>
    </tr>
    <tr>
        <td>英国</td>
        <td>
            <code>https://keyprotect.eu-gb.bluemix.net</code>
        </td>
    </tr>
    <caption style="caption-side:bottom;">表 2. {{site.data.keyword.keymanagementserviceshort}} API 的可用端点</caption>
</table>

**注：**对于 Cloud Foundry 组织或空间内存在的 {{site.data.keyword.keymanagementserviceshort}} 服务实例，请使用旧的 `https://ibm-key-protect.edge.bluemix.net` 端点来与 {{site.data.keyword.keymanagementserviceshort}} API 进行交互。

有关向 {{site.data.keyword.keymanagementserviceshort}} 进行认证的信息，请参阅[访问 API](/docs/services/keymgmt/keyprotect_authentication.html)。
