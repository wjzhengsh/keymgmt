---

copyright:
  years: 2017
lastupdated: "2017-10-16"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Tutorial for {{site.data.keyword.keymanagementserviceshort}}

You can use the {{site.data.keyword.keymanagementservicefull}} service to manage keys for your existing apps or services in {{site.data.keyword.cloud_notm}}.
{: shortdesc}

<!-- Content is being drafted. Post-GA. The tutorial section shows in staging only.-->

## Lesson 1: Decrypting a secret message by using the {{site.data.keyword.keymanagementserviceshort}} service

The {{site.data.keyword.keymanagementservicelong_notm}} provides you with a centralized environment to store, sort, and manage your encryption keys on the {{site.data.keyword.cloud_notm}}.

<dl>
  <dt>Objectives</dt>
    <dd>This tutorial includes an encrypted file. You can decrypt the file by using the keys that are stored in your {{site.data.keyword.keymanagementserviceshort}} service. When you retrieve the keys, the AES 256-encrypted message is revealed.
    <p>This tutorial walks you through the following scenarios:</p>
      <ul>
        <li>Adding keys to your {{site.data.keyword.keymanagementserviceshort}} instance.</li>
        <li>Generating authentication information for your API calls and coding it into a sample app.</li>
        <li>Decrypting the encrypted file.</li>
      </ul>
    </dd>
  <dt>Audience</dt>
    <dd>This tutorial is intended for users who are new to the {{site.data.keyword.keymanagementserviceshort}} service.</dd>
  <dt>Time required</dt>
    <dd>XX minutes</dd>
  <dt>Prerequisites</dt>
    <dd>
      <ul>
        <li>Create an instance of {{site.data.keyword.keymanagementserviceshort}} in your space.</li>
        <li>Download and install the [Bluemix CLI](https://console.bluemix.net/docs/cli/index.html#downloads) for your operating system, which is used to interact with {{site.data.keyword.cloud_notm}} from the command line.</li>
      </dd>
</dl>

1. In a terminal window, clone the [{{site.data.keyword.keymanagementserviceshort}} sample app ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window} to your local environment with the following command:

    ```
    git clone git@github.com/IBM-Bluemix/key-protect-helloworld-python.git
    ```
    {: codeblock}

2. Change into the newly created directory to begin working with the app files.

    ```
    cd key-protect-helloworld-python
    ```
    {: codeblock}

3. Run the `login` command to log in to {{site.data.keyword.cloud_notm}}.

    ```
    bx login
    ```
    {: codeblock}

4. Retrieve your authorization token to begin working with the {{site.data.keyword.keymanagementserviceshort}} API.

    ```
    bx iam oauth-tokens
    ```
    {: codeblock}

5. Retrieve the GUIDs for your {{site.data.keyword.cloud_notm}} org and space to use in the API header.
    You can run the `cf target` command to retrieve the org and space names that are required for the command.

    ```
    bx iam org organization_name --guid
    bx iam space space_name --guid
    ```
    {: codeblock}

6. Locally, edit the `auth.json` file with your {{site.data.keyword.cloud_notm}} credentials that were retrieved in the previous steps.

    ```json
    {
      "host": "ibm-key-protect.edge.bluemix.net",
      "token": "Bearer authorization_token",
      "org": "organization_GUID",
      "space": "space_GUID"
    }
    ```
    {: codeblock}

7. In the code editor, open the `manifest.yml` file. Change the variable `application-name` to something unique to give your app a route.

    ```
    applications: -
    path: .
    memory: 256M
    instances: 1
    name: <application-name>
    memory: 128M
    ```
    {: codeblock}

    To check whether your URL is unique, run the following command.

    ```
    bx app route-check <application-name> mybluemix.net
    ```
    {: codeblock}
    {: tip}

8. Push the sample app to {{site.data.keyword.cloud_notm}}

    ```
    bx app push
    ```
    {: codeblock}

9. In a browser window, access the external route of your sample app at `application-name.mybluemix.net`.
10. Click **Decrypt the secret message**. The app uses the keys to decrypt the `secretmessage.txt` file and reveals the message.

You successful created a {{site.data.keyword.keymanagementserviceshort}} instance and used keys to decrypt a secret message. To learn about encrypting stored files, continue to lesson two.
