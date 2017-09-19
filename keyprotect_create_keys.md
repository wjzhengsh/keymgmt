---

copyright:
  years: 2017
lastupdated: "2017-09-18"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Creating keys

You can manage the lifecycle of your keys by using {{site.data.keyword.keymanagementservicefull}}.
{: shortdesc}

A good practice is to manage your keys securely as you develop your code. For example, think about the following guidelines, along with other secure coding practices.

- Consider security implications when you embed keys into your code.
- Create keys only for programmatic access to your apps and resources. Do not create keys when you can grant simpler [user permissions ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/docs/admin/patterns.html#userroles){: new_window}.
- Rotate keys and remove unused keys.
- Use multifactor authentication for sensitive operations.
- Isolate apps by having separate keys for each app.
- Consider working with the programmatic API when you transfer highly sensitive information.

If you want to try out the service before you add your own keys, check out the [sample app ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}

## Creating keys with the GUI
{: #gui}

To add keys to your service with the {{site.data.keyword.keymanagementserviceshort}} GUI, see [Getting Started with {{site.data.keyword.keymanagementserviceshort}}](index.html#managekey).

## Creating keys with the API
{: #api}

You can use the {{site.data.keyword.keymanagementserviceshort}} API to programatically secure existing keys or generate new keys.

Create keys or import existing keys by making a `POST` call to the following endpoint:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys
```
{: codeblock}

1. [Retrieve your authorization token, org GUID, and space GUID to work with keys in the service](#authentication_api).

2. Call the [{{site.data.keyword.keymanagementserviceshort}} API](https://console.ng.bluemix.net/apidocs/639) with the following cURL command.

    ```cURL
    curl -X POST \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
      -H 'authorization: Bearer <OAuth_token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
      -H 'content-type: application/vnd.ibm.kms.key+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
     "metadata": {
       "collectionType": "application/vnd.ibm.kms.key+json",
       "collectionTotal": 1
     },
     "resources": [
       {
       "type": "application/vnd.ibm.kms.key+json",
       "name": "<key_alias>",
       "description": "<key_description>",
       "expirationDate": "<YYYY-MM-DDTHH:MM:SS.SSZ>",
       "payload": "<key_material>"
       }
     ]
    }'
    ```
    {: codeblock}

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
        <td><em>organization_GUID</em></td>
        <td>The unique identifier that is assigned to your {{site.data.keyword.Bluemix_notm}} org. </td>
      </tr>
      <tr>
        <td><em>space_GUID</em></td>
        <td>The unique identifier that is assigned to your {{site.data.keyword.Bluemix_notm}} space.</td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>The unique identifier that is used to track and correlate transactions.</td>
      </tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p>A header that alters server behavior for <code>POST</code> and <code>DELETE</code> operations.</p><p>If set to <code>return=minimal</code>, the service returns only the key metadata, such as the key name and <code>id</code> value, in the response entity-body. If set to <code>return=representation</code>, the service returns the both the key material and key metadata.</p></td>
      </tr>
      <tr>
        <td><em>key_alias</em></td>
        <td>A human-readable name for easy identification of your key.</td>
      </tr>
      <tr>
        <td><em>key_description</em></td>
        <td>An extended description of your key.</td>
      </tr>
      <tr>
        <td><em>YYYY-MM-DD</em><br><em>HH:MM:SS.SS</em></td>
        <td>Optional: The date and time that the key expires in the system, in RFC 3339 format. If the <code>expirationDate</code> attribute is omitted, the key does not expire. </td>
      </tr>
      <tr>
        <td><em>key_material</em></td>
        <td>The key material, such as an RSA key, that you want to store in {{site.data.keyword.keymanagementserviceshort}}. To generate a new key, omit the <code>payload</code> attribute and <em>key_contents</em> variable.</td>
      </tr>
      <caption style="caption-side:bottom;">Table 1. Variables needed to add keys through the {{site.data.keyword.keymanagementserviceshort}} API</caption>
    </table>

    A successful response returns the `id` value for your key, along with other metadata. The `id` is a unique identifier that is assigned to your key and is used for subsequent calls.

3. **Optional:** Verify that the key was created by running the following call to get the keys in your {{site.data.keyword.Bluemix_notm}} space.

    ```cURL
    curl -X GET \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <OAuth-token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
    ```
    {: codeblock}

### What's next

Now you can use your keys to code your apps and services.

- For full details of each REST request and response, check out the {{site.data.keyword.keymanagementserviceshort}} [REST API reference doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
