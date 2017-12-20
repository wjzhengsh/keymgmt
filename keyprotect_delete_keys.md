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

# Deleting keys
{: #deleting-keys}

You can use {{site.data.keyword.keymanagementservicefull}} to delete an encryption key and its contents, if you are an admin for your {{site.data.keyword.cloud_notm}} space or {{site.data.keyword.keymanagementserviceshort}} service instance.
{: shortdesc}

**Important:** When you delete a key, you permanently shred its contents and associated data. The action cannot be reversed. Destroying resources is not recommended for production environments, but might be useful for temporary environments such as testing or QA.

## Deleting keys with the GUI
{: #gui}

If you prefer to delete your encryption keys by using a graphical interface, you can use the {{site.data.keyword.keymanagementserviceshort}} GUI.

[After you create or import your existing keys into the service](/docs/services/keymgmt/keyprotect_create_keys.html), complete the following steps to delete a key:

1. [Log in to the {{site.data.keyword.cloud_notm}} console ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/).
2. From the {{site.data.keyword.cloud_notm}} dashboard, select your provisioned instance of {{site.data.keyword.keymanagementserviceshort}}.
3. Use the **Keys** table to browse the keys in your service.
4. Click the ⋮ icon to open a list of options for the key that you want to delete.
5. From the options menu, click **Delete key** and confirm the key deletion in the next screen.

After you delete a key, the key transitions to the _Destroyed_ state. Keys in this state are no longer recoverable. Metadata that is associated with the key, such as the key's deletion date, is kept in the {{site.data.keyword.keymanagementserviceshort}} database.

## Deleting keys with the API
{: #api}

To delete a key and its contents, make a `DELETE` call to the following endpoint:

```
https://keyprotect.us-south.bluemix.net/api/v2/keys<key_ID>
```

1. [Retrieve your service and authentication credentials to work with keys in the service.](/docs/services/keymgmt/keyprotect_authentication.html)

2. Retrieve the ID of the key that you would like to delete.

    You can retrieve the ID for a specified key by making a `GET /v2/keys/` request, or by viewing your keys in the {{site.data.keyword.keymanagementserviceshort}} dashboard.

3. Run the following cURL command to permanently delete the key and its contents.

    ```cURL
    curl -X DELETE \
      https://keyprotect.us-south.bluemix.net/api/v2/keys<key_ID> \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'prefer: <return_preference>'
    ```
    {: codeblock}
  
    To work with keys within a specified Cloud Foundry org and space in your account, replace `Bluemix-Instance` with the appropriate `Bluemix-org` and `Bluemix-space` headers. [See the {{site.data.keyword.keymanagementserviceshort}} API reference doc for code samples ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
    {: tip}

    Replace the variables in the example request according to the following table.
    <table>
      <tr>
        <th>Variable</th>
        <th>Description</th>
      </tr>
      <tr>
        <td><em>IAM_token</em></td>
        <td>Your authorization token. Include the full contents of the <code>IAM</code> token, including the Bearer value, in the cURL request.</td>
      </tr>
      <tr>
        <td><em>instance_ID</em></td>
        <td>The unique identifier that is assigned to your {{site.data.keyword.keymanagementserviceshort}} service instance. </td>
      </tr>
      <tr>
        <td><em>key_ID</em></td>
        <td>The unique identifier for the key that you would like to delete.</td>
      </tr>
      <tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p>A header that alters server behavior for <code>POST</code> and <code>DELETE</code> operations.</p><p>When you set the <em>return_preference</em> variable to <code>return=minimal</code>, the service returns a successful deletion response. When you set the variable to <code>return=representation</code>, the service returns the both the key material and key metadata.</p></td>
      </tr>
      <caption style="caption-side:bottom;">Table 1. Describes the variables needed to delete keys through the {{site.data.keyword.keymanagementserviceshort}} API.</caption>
    </table>

    If the _return_preference_ variable is set to `return=representation`, the details of the `DELETE` request are returned in the response entity-body. <!--After you delete a key, it enters the `Deactivated` key state. After 24 hours, if a key is not reinstated, the key transitions to the `Destroyed` state. The key contents are permanently erased and no longer accessible.--> The following JSON object shows an example returned value.
    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.kms.key+json",
        "collectionTotal": 1
      },
      "resources": [
        {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "...",
          "description": "...",
          "state": 5,
          "crn": "...",
          "deleted": true,
          "algorithmType": "AES",
          "createdBy": "...",
          "deletedBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "deletionDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "nonactiveStateReason": 2,
          "extractable": true
        }
      ]
    }
    ```
    {: screen}

    For a detailed description of the available parameters, see the {{site.data.keyword.keymanagementserviceshort}} [REST API reference doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/apidocs/639){: new_window}.