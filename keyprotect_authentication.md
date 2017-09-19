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

# Generating authentication credentials
{: #authentication}

{{site.data.keyword.keymanagementservicefull}} provides a REST API that can be used with any programming language to store, retrieve, and generate keys.
{: shortdesc}

To work with the API, you need to generate your service and authentication credentials.

## Retrieving your org and space GUIDs
{: #retrieve_GUIDs}

You can retrieve the identifying information for your {{site.data.keyword.Bluemix_notm}} organization and space with the [{{site.data.keyword.Bluemix_notm}} CLI](https://console.bluemix.net/docs/cli/reference/bluemix_cli/index.html#getting-started).

1. Log in to {{site.data.keyword.Bluemix_notm}} though the {{site.data.keyword.Bluemix_notm}} CLI.

    ```
    bx login [--sso]
    ```
    {: codeblock}

    The `--sso` parameter is required when you log in with a federated ID. If this option is used, go to the link listed in the CLI output to generate a one-time passcode.

2. Select the {{site.data.keyword.Bluemix_notm}} org and space that contains your {{site.data.keyword.keymanagementserviceshort}} service instance.

    Note the names of your org and space in the CLI output. You can also run `bx target` to view this information.

3. Retrieve your {{site.data.keyword.Bluemix_notm}} org and space GUIDs.

    ```
    bx iam org [organization_name] --guid
    bx iam space [space_name] --guid
    ```
    {: codeblock}
    Replace _organization_name_ and _space_name_ with the unique alias you assigned to your organization and space.

## Retrieving your authorization token
{: #retrieve_token}

You can use an authorization token to programmatically manage your keys using the {{site.data.keyword.keymanagementserviceshort}} API.

**Note**: To enable granular access control governed by {{site.data.keyword.Bluemix_notm}} Identity and Access Management, use an IAM token when you make calls to the service.

1. In the {{site.data.keyword.Bluemix_notm}} CLI, select the org and space that contains your {{site.data.keyword.keymanagementserviceshort}} service.

2. Retrieve and display your authorization tokens.

    ```
    bx iam oauth-tokens
    ```
    {: codeblock}

    The following truncated example shows the {{site.data.keyword.Bluemix_notm}} token output. The _Bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7_ variable is an example access token.

    ```
    IAM token: Bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7...
    UAA token: Bearer mjEyJhbGciOiJIUzI1Ni.chWyW1faWQiOiJJQkWs1...
    ```
    {: screen}

    Use the `IAM` or `UAA` bearer value to programmatically manage keys in your service using the {{site.data.keyword.keymanagementserviceshort}} API.

### What's next

See the [{{site.data.keyword.keymanagementserviceshort}} REST API reference doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/apidocs/639){: new_window} to start managing keys in your space.
