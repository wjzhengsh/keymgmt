---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-03"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Wrapping keys
{: #wrapping-keys}

You can manage and protect your encryption keys with a root key by using the {{site.data.keyword.keymanagementservicelong}} API, if you are a privileged user.
{: shortdesc}

When you wrap a data encryption key (DEK) with a root key, {{site.data.keyword.keymanagementserviceshort}} combines the strength of multiple algorithms to protect the privacy and the integrity of your encrypted data.  

To learn how key wrapping helps you control the security of at-rest data in the cloud, see [Envelope encryption](/docs/services/keymgmt/keyprotect_envelope.html).

## Wrapping keys by using the API
{: #api}

You can protect a specified data encryption key (DEK) with a root key that you manage in {{site.data.keyword.keymanagementserviceshort}}.

**Important:** When you supply a root key for wrapping, ensure that the root key is 256, 384, or 512 bits so that the wrap call can succeed. If you create a root key in the service, {{site.data.keyword.keymanagementserviceshort}} generates a 256-bit key from its HSMs, supported by the AES-GCM algorithm.

[After you designate a root key in the service](/docs/services/keymgmt/keyprotect_create_keys.html), you can wrap a DEK with advanced encryption by making a `POST` call to the following endpoint:

```
https://keyprotect.us-south.bluemix.net/api/v2/keys/<key_ID>?action=wrap
```
{: codeblock}

1. [Retrieve your service and authentication credentials to work with keys in the service.](/docs/services/keymgmt/keyprotect_authentication.html)

2. Copy the key material of the DEK that you want to manage and protect.

    If you have administrator or editor privileges for your {{site.data.keyword.keymanagementserviceshort}} service instance, [you can retrieve the key material for a specific key by making a `GET /v2/keys/<key_ID>` request](/docs/services/keymgmt/keyprotect_view_keys.md#retrieve_key_api).

3. Copy the ID of the root key that you want to use for wrapping.

4. Run the following cURL command to protect the key with a wrap operation.

    ```cURL
    curl -X POST \
      'https://keyprotect.us-south.bluemix.net/api/v2/keys/<key_ID>?action=wrap' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
      "plaintext": "<data_key>",
      "aad": ["<additional_data>", "<additional_data>"]
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
        <td><em>key_ID</em></td>
        <td>The unique identifier for the root key that you want to use for wrapping.</td>
      </tr>
      <tr>
        <td><em>IAM_token</em></td>
        <td>Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the <code>IAM</code> token, including the Bearer value, in the cURL request. For more information, <a href="/docs/services/keymgmt/keyprotect_authentication.html#retrieve_token">see Retrieving an access token</a>.</td>
      </tr>
      <tr>
        <td><em>instance_ID</em></td>
        <td>The unique identifier that is assigned to your {{site.data.keyword.keymanagementserviceshort}} service instance. For more information, <a href="/docs/services/keymgmt/keyprotect_authentication.html#retrieve_instance_ID">see Retrieving an instance ID</a>.</td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>Optional: The unique identifier that is used to track and correlate transactions.</td>
      </tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p>A header that alters server behavior for <code>POST</code> and <code>DELETE</code> operations.</p><p>When you set the <em>return_preference</em> variable to <code>return=minimal</code>, the service returns only the key metadata, such as the key name and ID value, in the response entity-body. When you set the variable to <code>return=representation</code>, the service returns the both the key material and key metadata.</p></td>
      </tr>
      <tr>
        <td><em>data_key</em></td>
        <td>Optional: The key material of the DEK that you want to manage and protect. The <code>plaintext</code> value must be base64 encoded. To generate a new DEK, omit the <code>plaintext</code> attribute. The service generates a random plaintext (32 bytes) and wraps that value.</td>
      </tr>
      <tr>
        <td><em>additional_data</em></td>
        <td>Optional: The additional authentication data (AAD) that is used to further secure the key. Each string can hold up to 255 characters. If you supply AAD when you make a wrap call to the service, you must specify the same AAD during the subsequent unwrap call.</td>
      </tr>
      <caption style="caption-side:bottom;">Table 1. Describes the variables needed to wrap a specified key in {{site.data.keyword.keymanagementserviceshort}}.</caption>
    </table>

    Your wrapped key, containing the base64 encoded key material, is returned in the response entity-body. The following JSON object shows an example returned value.

    ```
    {
      "plaintext": "VGhpcyBpcyBhIHNlY3JldCBtZXNzYWdlLg==",
      "ciphertext": "eyJjaXBoZXJ0ZXh0Ijoic3VLSDNRcmdEZjdOZUw4Rkc4L2FKYjFPTWcyd3A2eDFvZlA4MEc0Z1B2RmNrV2g3cUlidHphYXU0eHpKWWoxZyIsImhhc2giOiJiMmUyODdkZDBhZTAwZGZlY2Q3OGJmMDUxYmNmZGEyNWJkNGUzMjBkYjBhN2FjNzVhMWYzZmNkMDZlMjAzZWYxNWM5MTY4N2JhODg2ZWRjZGE2YWVlMzFjYzk2MjNkNjA5YTRkZWNkN2E5Y2U3ZDc5ZTRhZGY1MWUyNWFhYWM5MjhhNzg3NmZjYjM2NDFjNTQzMTZjMjMwOGY2MThlZGM2OTE3MjAyYjA5YTdjMjA2YzkxNTBhOTk1NmUxYzcxMTZhYjZmNmQyYTQ4MzZiZTM0NTk0Y2IwNzJmY2RmYTk2ZSJ9"
      "aad": ["data1", "data2"]
    }
    ```
    {:screen}