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

# 地區及位置
{: #regions-and-locations}

您可以指定地區服務端點，以使用 {{site.data.keyword.keymanagementservicelong_notm}} 服務來連接應用程式。
{: shortdesc}

## 可用的地區
{: #regions}

{{site.data.keyword.keymanagementserviceshort}} 可在下列地區中取得：

- 美國南部
- 英國  

## 服務端點
{: #endpoints}

如果您要以程式設計方式管理 {{site.data.keyword.keymanagementserviceshort}} 資源，請參閱下表，以決定要在連接至 [{{site.data.keyword.keymanagementserviceshort}} API](https://console.ng.bluemix.net/apidocs/639) 時使用的 API 端點： 

<table>
    <tr>
        <th>地區</th>
        <th>API 端點</th>
    </tr>
    <tr>
        <td>美國南部</td>
        <td>
            <code>https://keyprotect.us-south.bluemix.net</code>
        </td>
    </tr>
    <tr>
        <td>英國</td>
        <td>
            <code>https://keyprotect.eu-gb.bluemix.net</code>
        </td>
    </tr>
    <caption style="caption-side:bottom;">表 2. {{site.data.keyword.keymanagementserviceshort}} API 的可用端點</caption>
</table>

**附註：**對於存在於 Cloud Foundry 組織或空間內的 {{site.data.keyword.keymanagementserviceshort}} 服務實例，請使用舊式 `https://ibm-key-protect.edge.bluemix.net` 端點以與 {{site.data.keyword.keymanagementserviceshort}} API 互動。

如需向 {{site.data.keyword.keymanagementserviceshort}} 進行鑑別的相關資訊，請參閱[存取 API](/docs/services/keymgmt/keyprotect_authentication.html)。
