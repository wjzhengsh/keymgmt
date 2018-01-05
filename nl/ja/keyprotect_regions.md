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

# 地域とロケーション
{: #regions-and-locations}

地域のサービス・エンドポイントを指定することによって、アプリケーションを {{site.data.keyword.keymanagementservicelong_notm}} サービスに接続できます。
{: shortdesc}

## 使用可能な地域
{: #regions}

{{site.data.keyword.keymanagementserviceshort}} は、次の地域で使用できます。

- 米国南部
- 英国  

## サービス・エンドポイント
{: #endpoints}

{{site.data.keyword.keymanagementserviceshort}} リソースをプログラムで管理している場合は、次の表を参照して、[{{site.data.keyword.keymanagementserviceshort}} API](https://console.ng.bluemix.net/apidocs/639) への接続時に使用する API エンドポイントを判断してください。 

<table>
    <tr>
        <th>地域</th>
        <th>API エンドポイント</th>
    </tr>
    <tr>
        <td>米国南部</td>
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
    <caption style="caption-side:bottom;">表 2. {{site.data.keyword.keymanagementserviceshort}} API の使用可能なエンドポイント</caption>
</table>

**注:** Cloud Foundry 組織またはスペース内に存在する {{site.data.keyword.keymanagementserviceshort}} サービス・インスタンスの場合は、既存の `https://ibm-key-protect.edge.bluemix.net` エンドポイントを使用して、{{site.data.keyword.keymanagementserviceshort}} API と相互作用します。

{{site.data.keyword.keymanagementserviceshort}} での認証については、[API へのアクセス](/docs/services/keymgmt/keyprotect_authentication.html)を参照してください。
