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

# Importing standard keys
{: #import_standard_keys}

You can add your existing encryption keys with the {{site.data.keyword.keymanagementserviceshort}} GUI, or programmatically with the {{site.data.keyword.keymanagementserviceshort}} API.

## Importing standard keys with the GUI
{: #import_standard_key_GUI}

[After you create an instance of the service](/docs/services/keymgmt/keyprotect_provision.html), complete the following steps to enter your existing standard key with the {{site.data.keyword.keymanagementserviceshort}} GUI.

1. [Log in to the {{site.data.keyword.cloud_notm}} console ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/).
2. From your {{site.data.keyword.cloud_notm}} dashboard, select your provisioned instance of {{site.data.keyword.keymanagementserviceshort}}.
2. To import a new key, click **Add key** and select the **Enter existing key** window.

    Specify the key's details:

    <table>
      <tr>
        <th>Setting</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Name</td>
        <td>A unique, human-readable alias to assign to your key. The name can be anything to help you identify the key, such as what the key is used for or who the key is associated with.</td>
      </tr>
      <tr>
        <td>Key type</td>
        <td>The [type of key](/docs/services/keymgmt/keyprotect_envelope.html#key_types) that you would like to manage in {{site.data.keyword.keymanagementserviceshort}}. From the list of key types, select <b>Standard key</b>.</td>
      </tr>
      <tr>
        <td>Key material</td>
        <td>The key material, such as a symmetric key, that you want to manage in the service. The key must be base64 encoded.</td>
      </tr>
      <caption style="caption-side:bottom;">Table 1. Description of the <b>Generate new key</b> settings</caption>
    </table>

3. When you are finished filling out the key's details, click **Generate key** to confirm. 

## Creating standard keys with the API
{: #create_standard_key_API}

Create a standard key by making a `POST` call to the following endpoint:

```
https://keyprotect.us-south.bluemix.net/api/v2/keys
```
{: codeblock}

1. [Retrieve your service and authentication credentials to work with keys in the service.](/docs/services/keymgmt/keyprotect_authentication.html).

2. Call the [{{site.data.keyword.keymanagementserviceshort}} API](https://console.ng.bluemix.net/apidocs/639) with the following cURL command.

    ```cURL
    curl -X POST \
      https://keyprotect.us-south.bluemix.net/api/v2/keys \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
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
       "payload": "<key_material>",
       "extractable": true
       }
     ]
    }'
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
        <td>The unique identifier that is assigned to your {{site.data.keyword.keymanagementserviceshort}} service instance.</td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>The unique identifier that is used to track and correlate transactions.</td>
      </tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p>Optional: A header that alters server behavior for <code>POST</code> and <code>DELETE</code> operations.</p><p>When you set the <em>return_preference</em> variable to <code>return=minimal</code>, the service returns only the key metadata, such as the key name and ID value, in the response entity-body. When you set the variable to <code>return=representation</code>, the service returns the both the key material and key metadata for your standard key.</p></td>
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
        <td>The key material, such as a symmetric key, that you want to manage in the service. The key must be base64 encoded.</td>
      </tr>
      <tr>
        <td><em>key_type</em></td>
        <td>
          <p>A boolean value that determines whether the key material can leave the service.</p>
          <p>When you set the <code>extractable</code> attribute to <code>true</code>, the service designates the key as a standard key that you can store in your apps or services.</p>
        </td>
      </tr>
        <caption style="caption-side:bottom;">Table 2. Variables needed to add a standard key with the {{site.data.keyword.keymanagementserviceshort}} API</caption>
    </table>

    A successful `POST /v2/keys/` response returns the ID value for your key, along with other metadata. The ID is a unique identifier that is assigned to your key and is used for subsequent calls to the {{site.data.keyword.keymanagementserviceshort}} API .

3. Optional: Verify that the key was added by running the following call to get the keys in your {{site.data.keyword.keymanagementserviceshort}} service instance.

    ```cURL
    curl -X GET \
      https://keyprotect.us-south.bluemix.net/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}


### What's next

- To find out more about programmatically managing your keys, [check out the {{site.data.keyword.keymanagementserviceshort}} API reference doc for code samples ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
- To see an example of how keys stored in {{site.data.keyword.keymanagementserviceshort}} can work to encrypt and decrypt data, [check out the sample app in GitHub ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.
