---

copyright:
  years: 2017
lastupdated: "2017-11-08"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Provisioning the {{site.data.keyword.keymanagementserviceshort}} service
{: #provision}

You can create a secure instance of {{site.data.keyword.keymanagementservicefull}} by using the {{site.data.keyword.cloud_notm}} console or the {{site.data.keyword.cloud_notm}} (bx) CLI.
{: shortdesc}

## Provisioning from the {{site.data.keyword.cloud_notm}} console
{: #gui}

To provision an instance of {{site.data.keyword.keymanagementserviceshort}} from the {{site.data.keyword.cloud_notm}} console, complete the following steps.

1. [Log in to your {{site.data.keyword.cloud_notm}} account ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/){: new_window}.
2. Click **Catalog** to view the list of services that are available on {{site.data.keyword.cloud_notm}}.
3. Select the **Services** category, and click the **{{site.data.keyword.keymanagementserviceshort}}** tile.
5. Select a service plan, and click **Create** to provision a {{site.data.keyword.keymanagementserviceshort}} service instance in the {{site.data.keyword.cloud_notm}} org and space where you are logged in.

## Provisioning from the {{site.data.keyword.cloud_notm}} (bx) CLI
{: #cli}

You can provision an instance of {{site.data.keyword.keymanagementserviceshort}} by using the {{site.data.keyword.cloud_notm}} (bx) CLI. [Download and install the command line tool on your system](https://clis.ng.bluemix.net/ui/home.html){: new_window} to complete the following steps.

1. Log in to the {{site.data.keyword.cloud_notm}} CLI.

    ```sh
    bx login [--sso]
    ```
    {: codeblock}
    **Note**: The `--sso` parameter is required when you log in with a federated ID. If this option is used, go to the link listed in the CLI output to generate a one-time passcode.

2. Select the {{site.data.keyword.cloud_notm}} org and space where you would like to create a {{site.data.keyword.keymanagementserviceshort}} service instance.

    You can also use the following command to set your target org and space.

    ```sh
    bx target [-o organization_name] [-s space_name]
    ```
    {: codeblock}

3. Provision an instance of {{site.data.keyword.keymanagementserviceshort}} within that region, organization, and space.

    ```sh
    bx service create ibm_key_management TieredPricing [instance_name]
    ```
    {: codeblock}

    Replace _instance_name_ with a unique alias for your service instance.

4. Verify that the service instance was created successfully.

    ```sh
    bx service list
    ```
    {: codeblock}


### What's next

Now you can use your keys to code your apps and services.

- To see an example of how keys store in {{site.data.keyword.keymanagementserviceshort}} can work to encrypt and decrypt data, [check out the sample app in GitHub ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.
- To find out more about programmatically managing your keys, [check out the {{site.data.keyword.keymanagementserviceshort}} API reference doc for code samples ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
