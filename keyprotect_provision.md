---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-18"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Provisioning the service
{: #provision}

You can create an instance of {{site.data.keyword.keymanagementservicefull}} by using the {{site.data.keyword.cloud_notm}} console or the {{site.data.keyword.cloud_notm}} (bx) CLI.
{: shortdesc}

## Provisioning from the {{site.data.keyword.cloud_notm}} console
{: #gui}

To provision an instance of {{site.data.keyword.keymanagementserviceshort}} from the {{site.data.keyword.cloud_notm}} console, complete the following steps.

1. [Log in to your {{site.data.keyword.cloud_notm}} account ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/){: new_window}.
2. Click **Catalog** to view the list of services that are available on {{site.data.keyword.cloud_notm}}.
3. From the All Categories navigation pane, scroll to **Platform** and click the **Security** category.
4. From the list of services, click the **{{site.data.keyword.keymanagementserviceshort}}** tile.
5. Select a service plan, and click **Create** to provision an instance of {{site.data.keyword.keymanagementserviceshort}} in the account, region, and resource group where you are logged in.

## Provisioning from the {{site.data.keyword.cloud_notm}} (bx) CLI
{: #cli}

You can provision an instance of {{site.data.keyword.keymanagementserviceshort}} by using the {{site.data.keyword.cloud_notm}} (bx) CLI. 

### Creating a service instance within your account
{: #provision_acct_lvl}

To simplify access to your encryption keys with [{{site.data.keyword.iamlong}} roles](/docs/iam/users_roles.html#iamusermanpol), you can create one or more instances of the {{site.data.keyword.keymanagementserviceshort}} service within an account, without needing to specify an org and space. 

1. Log in to {{site.data.keyword.cloud_notm}} through the [{{site.data.keyword.cloud_notm}} (bx) CLI.](/docs/cloud-platform/cli/reference/bluemix_cli/get_started.html#getting-started){: new_window}

    ```sh
    bx login 
    ```
    {: pre}
    **Note:** If the login fails, run the `bx login --sso` command to try again. The `--sso` parameter is required when you log in with a federated ID. If this option is used, go to the link listed in the CLI output to generate a one-time passcode.

2. Select the account, region, and resource group where you would like to create a {{site.data.keyword.keymanagementserviceshort}} service instance.

    You can use the following command to set your target region and resource group.

    ```sh
    bx target -r <region_name> -g <resource_group_name>
    ```
    {: pre}

3. Provision an instance of {{site.data.keyword.keymanagementserviceshort}} within that account and resource group.

    ```sh
    bx resource service-instance-create <instance_name> kms tiered-pricing
    ```
    {: pre}

    Replace `<instance_name>` with a unique alias for your service instance.

4. Optional: Verify that the service instance was created successfully.

    ```sh
    bx resource service-instances
    ```
    {: pre}

### Creating a service instance within an org and space
{: #provision_space_lvl}

To manage access to your encryption keys with [Cloud Foundry roles](/docs/iam/users_roles.html#cfroles), you can create an instance of the {{site.data.keyword.keymanagementserviceshort}} service within a specified organization and space.  

1. Log in to [{{site.data.keyword.cloud_notm}} through the [{{site.data.keyword.cloud_notm}} (bx) CLI.](/docs/cloud-platform/cli/reference/bluemix_cli/get_started.html#getting-started){: new_window}

    ```sh
    bx login 
    ```
    {: pre}
    **Note:** If the login fails, run the `bx login --sso` command to try again. The `--sso` parameter is required when you log in with a federated ID. If this option is used, go to the link listed in the CLI output to generate a one-time passcode.

2. Select the account, region, organization, and space where you would like to create a {{site.data.keyword.keymanagementserviceshort}} service instance.

    You can use the following command to set your target region, org, and space.

    ```sh
    bx target -r <region> -o <organization_name> -s <space_name>
    ```
    {: pre}

3. Provision an instance of {{site.data.keyword.keymanagementserviceshort}} within that account, region, organization, and space.

    ```sh
    bx service create kms tiered-pricing <instance_name>
    ```
    {: pre}

    Replace `<instance_name>` with a unique alias for your service instance.

4. Optional: Verify that the service instance was created successfully.

    ```sh
    bx service list
    ```
    {: pre}


### What's next

- To see an example of how keys stored in {{site.data.keyword.keymanagementserviceshort}} can work to encrypt and decrypt data, [check out the sample app in GitHub ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.
- To find out more about programmatically managing your keys, [check out the {{site.data.keyword.keymanagementserviceshort}} API reference doc for code samples ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
