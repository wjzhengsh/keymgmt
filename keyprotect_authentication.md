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

# Accessing the API
{: #access-api}

{{site.data.keyword.keymanagementservicefull}} provides a REST API that can be used with any programming language to store, retrieve, and generate keys.
{: shortdesc}

To work with the API, you need to generate your service and authentication credentials. 

## Retrieving an access token
{: #retrieve_token}

You can authenticate with {{site.data.keyword.keymanagementserviceshort}} by retrieving an access token from {{site.data.keyword.iamshort}}. With a [service ID](/docs/iam/serviceid.html), you can work with the {{site.data.keyword.keymanagementserviceshort}} API on behalf of your service or application on or outside {{site.data.keyword.cloud_notm}}, without needing to share your personal user credentials.  

If you want to authenticate with your user credentials, you can retrieve your token by running `bx iam oauth-tokens` in the [{{site.data.keyword.cloud_notm}} (bx) CLI ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/cloud-platform/cli/reference/bluemix_cli/get_started.html#getting-started){: new_window}.
{: tip}

Complete the following steps to retrieve an access token:

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** &gt; **Security** &gt; **Identity and Access** &gt; **Service IDs**. Follow the process to [create a service ID.](/docs/iam/serviceid.html#creating-a-service-id){: new_window}
2. Use the **Actions** menu to [define an access policy for your new service ID.](/docs/iam/serviceidaccess.html#assigning-new-access){: new_window} 
    
    For more information about managing access for your {{site.data.keyword.keymanagementserviceshort}} resources, see [Roles and permissions](/docs/services/keymgmt/keyprotect_manage_access.md#roles).
3. Use the **API keys** section to [create an API key to associate with the service ID.](/docs/iam/serviceid_keys.html#creating-an-api-key-for-a-service-id){: new_window} Save your API key by downloading it to a secure location.
4. Call the {{site.data.keyword.iamshort}} API to retrieve your access token.

    ```cURL
    curl -X POST \
      "https://iam.bluemix.net/oidc/token" \
      -H "Content-Type: application/x-www-form-urlencoded" \
      -H "Accept: application/json" \
      -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<your_API_key>" \ 
    ```
    {: codeblock}

    In the request, replace `<API_key>` with the API key that you created in step 3. The following truncated example shows the token output:

    ```
    {
    "access_token": "eyJraWQiOiIyM...",
    "expiration": 1512161390,
    "expires_in": 3600,
    "refresh_token": "J1AzOrtC8yHVlcT...",
    "token_type": "Bearer"
    }
    ```
    {: screen}

    Use the full `access_token` value, prefixed by the _Bearer_ token type, to programmatically manage keys for your service using the {{site.data.keyword.keymanagementserviceshort}} API. 

## Retrieving your instance ID
{: #retrieve_instance_ID}

You can retrieve the identifying information for your {{site.data.keyword.keymanagementserviceshort}} service instance by using the [{{site.data.keyword.cloud_notm}} (bx) CLI ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/cloud-platform/cli/reference/bluemix_cli/get_started.html#getting-started){: new_window}. Use an instance ID to manage your encryption keys within a specified instance of {{site.data.keyword.keymanagementserviceshort}} in your account. 

If your service instance exists within a Cloud Foundry org and space, retrieve your org and space GUIDs to interact with the {{site.data.keyword.keymanagementserviceshort}} API. You can retrieve your org and space GUIDs by running the `bx iam org <organization_name> --guid` and `bx iam space <space_name> --guid` commands in the {{site.data.keyword.cloud_notm}} (bx) CLI.
{: tip}

1. Log in to {{site.data.keyword.cloud_notm}} with the {{site.data.keyword.cloud_notm}} (bx) CLI.

    ```sh
    bx login 
    ```
    {: pre}

    **Note:** If the login fails, run the `bx login --sso` command to try again. The `--sso` parameter is required when you log in with a federated ID. If this option is used, go to the link listed in the CLI output to generate a one-time passcode.

2. Select the account that contains your provisioned instance of {{site.data.keyword.keymanagementserviceshort}}.

    You can run `bx resource service-instances` to list all service instances that are provisioned in your account.

3. Retrieve the Cloud Resource Name (CRN) that uniquely identifies your {{site.data.keyword.keymanagementserviceshort}} service instance. 

    ```sh
    bx resource service-instance <instance_name> --id
    ```
    {: pre}

    Replace `<instance_name>` with the unique alias that you assigned to your instance of {{site.data.keyword.keymanagementserviceshort}}. The following truncated example shows the Bluemix CLI output. The _7e8fc048-5606-4259-ad71-92397b0fa3f7_ value is an example instance ID.

    ```
    crn:v1:bluemix:public:kms:us-south:a/7e8fc048-5606-4259-ad71-92397b0fa3f7
    ```
    {: screen}

## Forming your API request
{: #form_api_request}

When you make an API call to the service, structure your API request according to how you initially provisioned your instance of {{site.data.keyword.keymanagementserviceshort}}. 

To build your request, pair a [regional service endpoint](/docs/services/keymgmt/keyprotect_regions.html) with the appropriate authentication credentials. For example, if you created a service instance for the `us-south` region, use the following endpoint and API headers to browse keys in your service:

```cURL
curl -X GET \
    https://keyprotect.us-south.bluemix.net/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <access_token>' \
    -H 'bluemix-instance: <instance_ID>' \
```
{: codeblock}

### What's next

- To find out more about programmatically managing your keys, [check out the {{site.data.keyword.keymanagementserviceshort}} API reference doc for code samples ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
- To see an example of how keys stored in {{site.data.keyword.keymanagementserviceshort}} can work to encrypt and decrypt data, [check out the sample app in GitHub ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.
