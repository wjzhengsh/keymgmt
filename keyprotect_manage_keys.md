---

copyright:
  years: 2017
lastupdated: "2017-07-20"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Managing keys

You can manage the lifecycle of your keys by using {{site.data.keyword.keymanagementservicelong}} for {{site.data.keyword.Bluemix_short}}.
{: shortdesc}

A good practice is to manage your keys securely as you develop your code. For example, think about the following types of guidelines, along with other secure coding practices.

- Consider security implications when you embed keys into your code.
- Create keys only for programmatic access to your apps and resources. Do not create keys when you can grant simpler [user permissions ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/docs/admin/patterns.html#userroles){: new_window}.
- Rotate keys and remove unused keys.
- Use multifactor authentication for sensitive operations.
- Isolate apps by having separate keys for each app.
- Consider working with the programmatic API when you transfer highly sensitive information.

## Generating authentication credentials for the {{site.data.keyword.keymanagementserviceshort}} API
{: #authentication_api}

{{site.data.keyword.keymanagementservicelong_notm}} provides a REST API that can be used with any programming language to store, retrieve, and generate keys.

To work with the API, you need to generate your authentication and service credentials.

1. Log in to {{site.data.keyword.Bluemix_notm}} though the Cloud Foundry CLI.

    ```
    cf login [a api.DomainName] [-sso]
    ```
    {: codeblock}

2. Select the {{site.data.keyword.Bluemix_notm}} org and space that contains your Key Protect service instance.
    Note the names of your org and space in the CLI output. You can also run `cf target` to view this information.
3. Retrieve your {{site.data.keyword.Bluemix_notm}} org and space GUIDs.

    ```
    cf org organization_name --guid
    cf space space_name --guid
    ```
    {: codeblock}

4. Request a {{site.data.keyword.Bluemix_notm}} access token.

    ```
    cf oauth-token
    ```
    {: codeblock}

    The following truncated example shows the {{site.data.keyword.Bluemix_notm}} token output. The _bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7_ variable is an example access token.

    ```
    bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7...
    ```
    {: screen}

What to do next:

See the {{site.data.keyword.keymanagementserviceshort}} [REST API reference doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/apidocs/639){: new_window} to start managing keys in your space.


## Creating keys with the {{site.data.keyword.keymanagementserviceshort}} API
{: #codingapps}

You can use the {{site.data.keyword.keymanagementservicelong_notm}} API to secure existing keys or to generate new keys.

Create keys or add existing keys by making a **POST** call to the following endpoint:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/secrets
```
{: codeblock}

If you want to try out the service before you add your own keys, check out the [sample app ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.

1. [Retrieve your {{site.data.keyword.Bluemix_notm}} access token, org GUID, and space GUID to work with keys in the service](#authentication_api).

2. Call the [{{site.data.keyword.keymanagementserviceshort}} API](https://console.ng.bluemix.net/apidocs/639) with the following cURL command.

  ```cURL
  curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: bluemix_access_token' --header 'Bluemix-Space: space_GUID' --header 'Bluemix-Org: organization_GUID' -d '{
    "metadata": {
      "collectionType": "application/vnd.ibm.kms.secret+json",
      "collectionTotal": 1
    },
    "resources": [
      {
      "type": "application/vnd.ibm.kms.secret+json",
      "name": "key_alias",
      "description": "key_description",
      "expirationDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
      "payload": "key_contents"
      }
    ]
  }' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets'
  ```
  {: codeblock}

  Replace the variables in the example request according to the following table.
  <table>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><em>bluemix_access_token</em></td>
      <td>Your authorization token. Include the full contents of the token, including the Bearer value, in the cURL request.</td>
    </tr>
    <tr>
      <td><em>space_GUID</em></td>
      <td>The identifier for your {{site.data.keyword.Bluemix_notm}} space.</td>
    </tr>
    <tr>
      <td><em>organization_GUID</em></td>
      <td>The identifier for your {{site.data.keyword.Bluemix_notm}} org. </td>
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
      <td>Optional: The date and time that the key expires in the system, in RFC3339 format. If the <code>expirationDate</code> attribute is omitted, the key does not expire. </td>
    </tr>
    <tr>
      <td><em>key_contents</em></td>
      <td>The key material, such as an RSA key, that you want to store in {{site.data.keyword.keymanagementserviceshort}}. To generate a new key, omit the payload attribute and key_contents variable.</td>
    </tr>
      <caption style="caption-side:bottom;">Table 1. Variables needed to add keys through the {{site.data.keyword.keymanagementserviceshort}} API</caption>
  </table>

3. Verify that the key was created by running the following call to get the keys in your {{site.data.keyword.Bluemix_notm}} space.

  ```cURL
  curl -X GET --header 'Accept: application/json' --header 'Authorization: bluemix_access_token' --header 'Bluemix-Space: space_GUID' --header 'Bluemix-Org: organization_GUID' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets'
  ```
  {: codeblock}

## Viewing keys with the {{site.data.keyword.keymanagementserviceshort}} API
{: #viewingkeys_api}

You can view the contents of your keys though the {{site.data.keyword.keymanagementservicelong_notm}} API, if you are a {{site.data.keyword.Bluemix_notm}} space manager or developer.

For a high-level view, you can browse keys that are managed in your space through the {{site.data.keyword.keymanagementserviceshort}} UI.

View detailed information about your keys by making a GET call to the following endpoint:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/secrets/key_ID
```
{: codeblock}

1. From the {{site.data.keyword.keymanagementserviceshort}} UI, under Security services, you can view general characteristics about your keys. You can browse keys by clicking the sortable column headers.
2. Copy the **ID** in the row of the key. The ID value is used to access more detailed information about the key in the API, such as the key material itself.
3. [Retrieve your {{site.data.keyword.Bluemix_notm}} access token, org GUID, and space GUID to work with keys in the service.](#authentication_api)
4. Run the following cURL command to get details about your key and the key material.

  ```cURL
  curl -X GET --header 'Accept: application/json' --header 'Authorization: bluemix_access_token' --header 'Bluemix-Space: space_GUID' --header 'Bluemix-Org: organization_GUID' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets/key_ID'
  ```
  {: codeblock}

  Replace the variables in the example request according to the following table.
  <table>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><em>bluemix_access_token</em></td>
      <td>Your authorization token. Include the full contents of the token, including the Bearer value, in the cURL request.</td>
    </tr>
    <tr>
      <td><em>space_GUID</em></td>
      <td>The randomly generated identifier that is assigned to your {{site.data.keyword.Bluemix_notm}} space.</td>
    </tr>
    <tr>
      <td><em>organization_GUID</em></td>
      <td>The randomly generated identifier that is assigned to your {{site.data.keyword.Bluemix_notm}} org.</td>
    </tr>
    <tr>
      <td><em>key_ID</em></td>
      <td>The identifier for your key that you pulled up in step [2](#viewingkeys_api).</td>
    </tr>
    <caption style="caption-side:bottom;">Table 2. Describes the variables needed to view keys through the {{site.data.keyword.keymanagementserviceshort}} API.</caption>
  </table>

  The key material is returned in the response entity-body. Keys that are generated by hardware security modules (HSMs) are base-64 encoded.

## Auditing keys and access
{: #viewkeyassignments}

{{site.data.keyword.keymanagementservicelong_notm}} provides a centralized system to view, manage, and audit your encryption keys. Audit your keys and access restrictions to keys to ensure the security of your resources.

Audit your key configuration regularly:

- Examine when keys were created and determine whether it's time to rotate the key.
- [Monitor API calls to {{site.data.keyword.keymanagementserviceshort}} with {{site.data.keyword.cloudaccesstrailshort}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/docs/services/AccessTrail/at_integration.html#at_integration_key_protect){: new_window}.
- Inspect which users have access to keys and if the level of access is appropriate.

To audit users with access:

1. As a space manager, go to your account settings and select **Manage Organizations**.
2. Open the space that contains the {{site.data.keyword.keymanagementserviceshort}} service instance to inspect which users have access.
3. If you need to add users, go to **Invite Team Members** and select the {{site.data.keyword.Bluemix_notm}} roles that correspond to the {{site.data.keyword.keymanagementserviceshort}} permissions that you want to grant to the user:

  <table>
    <tr>
      <th>{{site.data.keyword.Bluemix_notm}} roles</th>
      <th>{{site.data.keyword.keymanagementserviceshort}} permissions</th>
    </tr>
    <tr>
      <td>Space manager</td>
      <td>A space manager can create, view, and delete keys.</td>
    </tr>
    <tr>
      <td>Developer</td>
      <td>A developer can create keys and view key details.</td>
    </tr>
    <tr>
      <td>Auditor</td>
      <td>An auditor can access a high-level view of keys. </td>
    </tr>
    <caption style="caption-side:bottom;">Table 3. Mapping of {{site.data.keyword.Bluemix_notm}} roles to {{site.data.keyword.keymanagementserviceshort}} permissions.</caption>
  </table>
