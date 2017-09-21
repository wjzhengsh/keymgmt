---

copyright:
  years: 2017
lastupdated: "2017-09-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Viewing keys

You can view the contents of your encryption keys with {{site.data.keyword.keymanagementservicefull}}.
{: shortdesc}

## Viewing keys with the GUI
{: #gui}

To browse the keys in your service with the {{site.data.keyword.keymanagementserviceshort}} GUI, see [Getting Started with {{site.data.keyword.keymanagementserviceshort}}](/docs/services/keymgmt/index.html#managekey).

## Viewing keys with the API
{: #api}

You can retrieve the contents of your keys by using the {{site.data.keyword.keymanagementserviceshort}} API.

### Step 1: Retrieve a collection of keys
{: #retrieve_keys_api}

For a high-level view, you can browse keys that are managed in your space by making a `GET` call to the following endpoint:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys
```
{: codeblock}

1. [Retrieve your authorization token, org GUID, and space GUID to work with keys in the service.](/docs/services/keymgmt/keyprotect_authentication.html)
2. Run the following cURL command to view general characteristics about your keys.

    ```cURL
    curl -X GET \
    https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <OAuth_token>' \
    -H 'bluemix-org: <organization_GUID>' \
    -H 'bluemix-space: <space_GUID>' \
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
        <td><em>space_GUID</em></td>
        <td>The unique identifier that is assigned to your {{site.data.keyword.Bluemix_notm}} space.</td>
      </tr>
      <tr>
        <td><em>organization_GUID</em></td>
        <td>The unique identifier that is assigned to your {{site.data.keyword.Bluemix_notm}} org.</td>
      </tr>
      <caption style="caption-side:bottom;">Table 1. Describes the variables needed to view keys through the {{site.data.keyword.keymanagementserviceshort}} API.</caption>
    </table>

    A successful request returns a collection of keys available in your {{site.data.keyword.Bluemix_notm}} space.

    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.kms.key+json",
        "collectionTotal": 2
      },
      "resources": [
        {
          "id": "Key ID 1",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Key alias",
          "description": "Key description",
          "state": 1,
          "algorithmType": "AES",
          "createdBy": "v4 UUID of the user who creates the key",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "Key length",
            "mode": "GCM"
          }
        },
        {
          "id": "Key ID 2",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Key alias",
          "description": "Key description",
          "state": 1,
          "algorithmType": "AES",
          "createdBy": "v4 UUID of the user who creates the key",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "Key length",
            "mode": "GCM"
          }
        }
      ]
    }
    ```
    {:screen}

### Step 2: Retrieve a key by ID
{: #retrieve_key_api}

To view detailed information about a specific key, you can make a subsequent `GET` call to the following endpoint:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID>
```
{: codeblock}

1. [Retrieve your authorization token, org GUID, and space GUID to work with keys in the service.](/docs/services/keymgmt/keyprotect_authentication.html)
2. Retrieve the ID of the key you would like to access or manage.

    The ID value is used to access detailed information about the key, such as the key material itself. You can retrieve the ID for a specified key by making a `GET v2/keys` request, or by accessing the {{site.data.keyword.keymanagementserviceshort}} GUI.

3. Run the following cURL command to get details about your key and the key material.

    ```cURL
    curl -X GET \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID> \
      -H 'accept: application/vnd.ibm.kms.secret+json' \
      -H 'authorization: Bearer <OAuth_token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
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
        <td><em>OAuth_token</em></td>
        <td>Your authorization token. Include the full contents of the token, including the Bearer value, in the cURL request.</td>
      </tr>
      <tr>
        <td><em>organization_GUID</em></td>
        <td>The unique identifier that is assigned to your {{site.data.keyword.Bluemix_notm}} org.</td>
      </tr>
      <tr>
        <td><em>space_GUID</em></td>
        <td>The unique identifier that is assigned to your {{site.data.keyword.Bluemix_notm}} space.</td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>Optional: The unique identifier that is used to track and correlate transactions.</td>
      </tr>
      <tr>
        <td><em>key_ID</em></td>
        <td>The identifier for the key that you retrieved in [step 1](#retrieve_keys_api).</td>
      </tr>
      <caption style="caption-side:bottom;">Table 2. Describes the variables needed to view a specified key through the {{site.data.keyword.keymanagementserviceshort}} API.</caption>
    </table>

    A successful response returns details about your key and the key material. The following JSON object shows an example returned value.

    ```
    {
        "metadata": {
            "collectionTotal": 1,
            "collectionType": "application/vnd.ibm.kms.key+json"
        },
        "resources": [
            {
                "createdBy": "...",
                "creationDate": "...",
                "id": "...",
                "name": "...",
                "payload": "...",
                "state": 1,
                "type": "application/vnd.ibm.kms.key+json"
            }
        ]
    }
    ```
    {:screen}

    For a detailed description of the available parameters, see the {{site.data.keyword.keymanagementserviceshort}} [REST API reference doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
