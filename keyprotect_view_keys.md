---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-31"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Viewing keys
{: #viewing-keys}

{{site.data.keyword.keymanagementservicefull}} provides a centralized system to view, manage, and audit your encryption keys. Audit your keys and access restrictions to keys to ensure the security of your resources.
{: shortdesc}

Audit your key configuration regularly:

- Examine when keys were created and determine whether it's time to rotate the key.
- [Monitor API calls to {{site.data.keyword.keymanagementserviceshort}} with {{site.data.keyword.cloudaccesstrailshort}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/services/cloud-activity-tracker/svcs/kp_at.html#kp_at){: new_window}.
- Inspect which users have access to keys and if the level of access is appropriate.

For more information about auditing access to your resources, see [Managing user access with Cloud IAM](/docs/services/keymgmt/keyprotect_manage_access.html).

## Viewing keys with the GUI
{: #gui}

If you prefer to inspect the keys in your service by using a graphical interface, you can use the {{site.data.keyword.keymanagementserviceshort}} dashboard.

[After you create or import your existing keys into the service](/docs/services/keymgmt/keyprotect_create_keys.html), complete the following steps to view your keys.

1. [Log in to the {{site.data.keyword.cloud_notm}} console ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/).
2. From your {{site.data.keyword.cloud_notm}} dashboard, select your provisioned instance of {{site.data.keyword.keymanagementserviceshort}}.
3. Browse the general characteristics of your keys from the {{site.data.keyword.keymanagementserviceshort}} dashboard:

    <table>
      <tr>
        <th>Column</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Name</td>
        <td>The unique, human-readable alias that was assigned to your key.</td>
      </tr>
      <tr>
        <td>ID</td>
        <td>A unique key ID that was assigned to your key by the {{site.data.keyword.keymanagementserviceshort}} service. You can use the ID value to make calls to the service with the [{{site.data.keyword.keymanagementserviceshort}} API](https://console.ng.bluemix.net/apidocs/639).</td>
      </tr>
      <tr>
        <td>State</td>
        <td>The [key state](/docs/services/keymgmt/keyprotect_states.html) based on [NIST Special Publication 800-57, Recommendation for Key Management ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf). These states include <i>Pre-active</i>, <i>Active</i>, <i>Deactivated</i>, and <i>Destroyed</i>.</td>
      </tr>
      <tr>
        <td>Type</td>
        <td>The [key type](/docs/services/keymgmt/keyprotect_envelope.html#key_types) that describes your key's designated purpose within the service.</td>
      </tr>
      <caption style="caption-side:bottom;">Table 1. Description of the <b>Keys</b> table</caption>
    </table>

## Viewing keys with the API
{: #api}

You can retrieve the contents of your keys by using the {{site.data.keyword.keymanagementserviceshort}} API.

### Step 1: Retrieve a collection of keys
{: #retrieve_keys_api}

For a high-level view, you can browse keys that are managed in your provisioned instance of {{site.data.keyword.keymanagementserviceshort}} by making a `GET` call to the following endpoint:

```
https://keyprotect.us-south.bluemix.net/api/v2/keys
```
{: codeblock}

1. [Retrieve your service and authentication credentials to work with keys in the service.](/docs/services/keymgmt/keyprotect_authentication.html)
2. Run the following cURL command to view general characteristics about your keys.

    ```cURL
    curl -X GET \
    https://keyprotect.us-south.bluemix.net/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <IAM_token>' \
    -H 'bluemix-instance: <instance_ID>' \
    -H 'correlation-id: <correlation_ID>' \
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
      <caption style="caption-side:bottom;">Table 2. Describes the variables needed to view keys with the {{site.data.keyword.keymanagementserviceshort}} API.</caption>
    </table>

    A successful `POST /v2/keys/` request returns a collection of keys available in your {{site.data.keyword.keymanagementserviceshort}} service instance.

    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.collection+json",
        "collectionTotal": 2
      },
      "resources": [
        {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Standard key",
          "description": "...",
          "state": 1,
          "crn": "...",
          "algorithmType": "AES",
          "createdBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "256",
            "mode": "GCM"
          },
          "extractable": true
        },
        {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Root key",
          "description": "...",
          "state": 1,
          "crn": "...",
          "algorithmType": "AES",
          "createdBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "256",
            "mode": "GCM"
          },
          "extractable": false
        }
      ]
    }
    ```
    {:screen}

### Step 2: Retrieve a key by ID
{: #retrieve_key_api}

To view detailed information about a specific key, you can make a subsequent `GET` call to the following endpoint:

```
https://keyprotect.us-south.bluemix.net/api/v2/keys/<key_ID>
```
{: codeblock}

1. [Retrieve your service and authentication credentials to work with keys in the service.](/docs/services/keymgmt/keyprotect_authentication.html)
2. Retrieve the ID of the key you would like to access or manage.

    The ID value is used to access detailed information about the key, such as the key material itself. You can retrieve the ID for a specified key by making a `GET v2/keys` request, or by accessing the {{site.data.keyword.keymanagementserviceshort}} GUI.

3. Run the following cURL command to get details about your key and the key material.

    ```cURL
    curl -X GET \
      https://keyprotect.us-south.bluemix.net/api/v2/keys/<key_ID> \
      -H 'accept: application/vnd.ibm.kms.key+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

    Replace the variables in the example request according to the following table.

    <table>
      <tr>
        <th>Variable</th>
        <th>Description</th>
      </tr>
      <tr>
        <td><em>IAM_token</em></td>
        <td>Your authorization token. Include the full contents of the `IAM` token, including the Bearer value, in the cURL request.</td>
      </tr>
      <tr>
        <td><em>instance_ID</em></td>
        <td>The unique identifier that is assigned to your {{site.data.keyword.keymanagementserviceshort}} service instance. </td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>Optional: The unique identifier that is used to track and correlate transactions.</td>
      </tr>
      <tr>
        <td><em>key_ID</em></td>
        <td>The identifier for the key that you retrieved in [step 1](#retrieve_keys_api).</td>
      </tr>
      <caption style="caption-side:bottom;">Table 3. Describes the variables needed to view a specified key with the {{site.data.keyword.keymanagementserviceshort}} API.</caption>
    </table>

    A successful `GET v2/keys/<key_ID>` response returns details about your key and the key material. The following JSON object shows an example returned value for a standard key.

    ```
    {
        "metadata": {
            "collectionTotal": 1,
            "collectionType": "application/vnd.ibm.kms.key+json"
        },
        "resources": [
        {
            "id": "...",
            "type": "application/vnd.ibm.kms.key+json",
            "name": "Standard key",
            "description": "...",
            "state": 1,
            "crn": "...",
            "algorithmType": "AES",
            "payload": "...",
            "createdBy": "...",
            "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
            "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
            "algorithmMetadata": {
                "bitLength": "256",
                "mode": "GCM"
            },
            "extractable": true
        }
      ]
    }
    ```
    {:screen}

    For a detailed description of the available parameters, see the {{site.data.keyword.keymanagementserviceshort}} [REST API reference doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
