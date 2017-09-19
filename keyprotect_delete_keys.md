---

copyright:
  years: 2017
lastupdated: "2017-09-19"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Deleting keys

You can use {{site.data.keyword.keymanagementservicefull}} to delete an encryption key and its contents, if you are an admin for your {{site.data.keyword.Bluemix_notm}} space or {{site.data.keyword.keymanagementserviceshort}} service instance.
{: shortdesc}

**Important**: When you delete a key, you permanently shred its contents and associated data. The action cannot be reversed. Destroying resources is not recommended for production environments, but might be useful for temporary environments such as testing or QA.

## Deleting keys with the GUI
{: #gui}

To delete key resources in your service with the {{site.data.keyword.keymanagementserviceshort}} GUI, see [Getting Started with {{site.data.keyword.keymanagementserviceshort}}](index.html#deletekey).

## Deleting keys with the API
{: #api}

To delete a key and its contents, make a `DELETE` call to the following endpoint:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID>
```

1. [Retrieve your authorization token, org GUID, and space GUID to work with keys in the service.](#authentication_api)

2. Retrieve the ID of the key you would like to delete.

    You can retrieve the ID for a specified key by making a `GET /v2/keys` request, or by viewing your keys in the {{site.data.keyword.keymanagementserviceshort}} dashboard.

3. Run the following cURL command to permanently delete the key and its contents.

    ```cURL
    curl -X DELETE \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID> \
      -H 'authorization: Bearer <OAuth_token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
      -H 'prefer: <return_preference>'
    ```
    Replace the variables in the example request according to the following table.
    <table>
      <tr>
        <th>Variable</th>
        <th>Description</th>
      </tr>
      <tr>
        <td><em>OAuth_token</em></td>
        <td>Your authorization token. Include the full contents of the token, including the Bearer value, in the cURL request.</td>
      </tr>
      <tr>
        <td><em>space_GUID</em></td>
        <td>The unique identifier that is assigned to your {{site.data.keyword.Bluemix_notm}} space.</td>
      </tr>
      <tr>
        <td><em>organization_GUID</em></td>
        <td>The unique identifier that is assigned to your {{site.data.keyword.Bluemix_notm}} org.</td>
      </tr>
      <tr>
        <td><em>key_ID</em></td>
        <td>The unique identifier for the key that you would like to delete.</td>
      </tr>
      <tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p>A header that alters server behavior for <code>POST</code> and <code>DELETE</code> operations.</p><p>If set to <code>return=minimal</code>, the service returns only the key metadata, such as the key name and <code>id</code> value, in the response entity-body. If set to <code>return=representation</code>, the service returns the both the key material and key metadata.</p></td>
      </tr>
      <caption style="caption-side:bottom;">Table 1. Describes the variables needed to delete keys through the {{site.data.keyword.keymanagementserviceshort}} API.</caption>
    </table>

    The details of the `DELETE` request are returned in the response entity-body.
