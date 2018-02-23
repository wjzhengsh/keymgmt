---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-23"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Creating root keys
{: #create_root_keys}

You can use {{site.data.keyword.keymanagementservicefull}} to create root keys by using the {{site.data.keyword.keymanagementserviceshort}} GUI, or programmatically with the {{site.data.keyword.keymanagementserviceshort}} API.
{: shortdesc}

Root keys are symmetric key-wrapping keys used to protect the security of encrypted data in the cloud. For more information about root keys, see [Envelope encryption](/docs/services/keymgmt/keyprotect_envelope.html). 

## Creating root keys with the GUI
{: #create_root_key_GUI}

[After you create an instance of the service](/docs/services/keymgmt/keyprotect_provision.html), complete the following steps to create a root key with the {{site.data.keyword.keymanagementserviceshort}} GUI.

1. [Log in to the {{site.data.keyword.cloud_notm}} console ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/).
2. From your {{site.data.keyword.cloud_notm}} dashboard, select your provisioned instance of {{site.data.keyword.keymanagementserviceshort}}.
2. To create a new key, click **Add key** and select the **Generate a new key** window.

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
        <td>The [type of key](/docs/services/keymgmt/keyprotect_envelope.html#key_types) that you would like to manage in {{site.data.keyword.keymanagementserviceshort}}. From the list of key types, select <b>Root key</b>.</td>
      </tr>
      <caption style="caption-side:bottom;">Table 1. Description of the <b>Generate new key</b> settings</caption>
    </table>

3. When you are finished filling out the key's details, click **Generate key** to confirm. 

## Creating root keys with the API
{: #create_root_key_API}

Create a root key by making a `POST` call to the following endpoint:

```
https://keyprotect.<region>.bluemix.net/api/v2/keys
```
{: codeblock}

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/services/keymgmt/keyprotect_authentication.html).

2. Call the [{{site.data.keyword.keymanagementserviceshort}} API](https://console.ng.bluemix.net/apidocs/639) with the following cURL command.

    ```cURL
    curl -X POST \
      https://keyprotect.<region>.bluemix.net/api/v2/keys \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key+json' \
      -H 'correlation-id: <correlation_ID>' \
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
       "extractable": false
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
        <td><em>region</em></td>
        <td>The region abbreviation, such as <code>us-south</code> or <code>eu-gb</code>, that represents the geographic area where your {{site.data.keyword.keymanagementserviceshort}} service instance resides. See <a href="/docs/keyprotect_regions.html#endpoints">Regional service endpoints</a> for more information.</td>
      </tr>
      <tr>
        <td><em>IAM_token</em></td>
        <td>Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the <code>IAM</code> token, including the Bearer value, in the cURL request. For more information, see <a href="/docs/services/keymgmt/keyprotect_authentication.html#retrieve_token">Retrieving an access token</a>.</td>
      </tr>
      <tr>
        <td><em>instance_ID</em></td>
        <td>The unique identifier that is assigned to your {{site.data.keyword.keymanagementserviceshort}} service instance. For more information, see <a href="/docs/services/keymgmt/keyprotect_authentication.html#retrieve_instance_ID">Retrieving an instance ID</a>.</td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>The unique identifier that is used to track and correlate transactions.</td>
      </tr>
      <tr>
        <td><em>key_alias</em></td>
        <td>A unique, human-readable name for easy identification of your key.</td>
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
        <td><em>key_type</em></td>
        <td>
          <p>A boolean value that determines whether the key material can leave the service.</p>
          <p>When you set the <code>extractable</code> attribute to <code>false</code>, the service creates a root key that you can use for <code>wrap</code> or <code>unwrap</code> operations.</p>
        </td>
      </tr>
        <caption style="caption-side:bottom;">Table 1. Variables needed to add a root key with the {{site.data.keyword.keymanagementserviceshort}} API</caption>
    </table>

    A successful `POST /v2/keys/` response returns the ID value for your key, along with other metadata. The ID is a unique identifier that is assigned to your key and is used for subsequent calls to the {{site.data.keyword.keymanagementserviceshort}} API .

3. Optional: Verify that the key was created by running the following call to browse the keys in your {{site.data.keyword.keymanagementserviceshort}} service instance.

    ```cURL
    curl -X GET \
      https://keyprotect.<region>.bluemix.net/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

**Note:** After you create a root key with the service, the key stays within the bounds of {{site.data.keyword.keymanagementserviceshort}}, and its key material cannot be retrieved. 

### What's next

- To find out more about protecting keys with envelope encryption, check out [Wrapping keys](/docs/services/keymgmt/keyprotect_wrap_keys.html).
- To find out more about programmatically managing your keys, [check out the {{site.data.keyword.keymanagementserviceshort}} API reference doc for code samples ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
