---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-18"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Regions and locations
{: #regions-and-locations}

You can connect your applications with the {{site.data.keyword.keymanagementservicelong_notm}} service by specifying a regional service endpoint.
{: shortdesc}

## Available regions
{: #regions}

{{site.data.keyword.keymanagementserviceshort}} is available in the following regions:

- US South
- United Kingdom  

## Service endpoints
{: #endpoints}

If you are managing your {{site.data.keyword.keymanagementserviceshort}} resources programmatically, see the following table to determine the API endpoints to use when you connect to the [{{site.data.keyword.keymanagementserviceshort}} API](https://console.ng.bluemix.net/apidocs/639): 

<table>
    <tr>
        <th>Region</th>
        <th>API endpoint</th>
    </tr>
    <tr>
        <td>US South</td>
        <td>
            <code>https://keyprotect.us-south.bluemix.net</code>
        </td>
    </tr>
    <tr>
        <td>United Kingdom</td>
        <td>
            <code>https://keyprotect.eu-gb.bluemix.net</code>
        </td>
    </tr>
    <caption style="caption-side:bottom;">Table 2. Available endpoints for the {{site.data.keyword.keymanagementserviceshort}} API</caption>
</table>

**Note:** For {{site.data.keyword.keymanagementserviceshort}} service instances that exist within a Cloud Foundry org or space, use the legacy `https://ibm-key-protect.edge.bluemix.net` endpoint to interact with the {{site.data.keyword.keymanagementserviceshort}} API.

For information about authenticating with {{site.data.keyword.keymanagementserviceshort}}, see [Accessing the API](/docs/services/keymgmt/keyprotect_authentication.html).