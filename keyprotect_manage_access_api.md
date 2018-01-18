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

# Managing access to keys with the API
{: #managing-access-api}

With {{site.data.keyword.iamlong}}, you can enable granular access control for your encryption keys by creating and modifying access policies.
{: shortdesc}

This page walks you through several scenarios for managing access to your key resources with the [Access Management API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://iampap.ng.bluemix.net/v1/docs/#!/Access_Policies/){: new_window}.


Before you begin:
- [Retrieve your IAM token and instance ID](/docs/services/keymgmt/keyprotect_authentication.html)
- [Retrieve the key ID to specify the resource](/docs/services/keymgmt/keyprotect_view_keys.html)
- [Retrieve the account ID to specify the scope of access](keyprotect_manage_access_api.html#retrieve_account_ID)
- [Retrieve the user ID of the user whose access you would like to modify](keyprotect_manage_access_api.html#retrieve_user_ID)

## Creating a new access policy
{: #create_policy}

To enable access control for a specific key, you can send a request to {{site.data.keyword.iamshort}} by running the following command. Repeat the command for each access policy.

```cURL
curl -X POST \
  https://iam.bluemix.net/acms/v1/scopes/a/<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
  "roles": [
    {
      "id": "crn:v1:bluemix:public:iam::::role:<IAM_role>"
    }
  ],
  "resources": [
    {
      "serviceName": "IBM Key Protect",
      "accountId": "<account_ID>",
      "region": "us-south",
      "serviceInstance": "<instance_ID>",
      "resourceType": "key",
      "resource": "<key_ID>"
    }
  ]
}'
```
{: codeblock}

If you need to manage access to keys within a specified Cloud Foundry org and space, replace `serviceInstance` with `organizationId` and `spaceId`. To learn more, see the [Access Management API reference doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://iampap.ng.bluemix.net/v1/docs/#!/Access_Policies/){: new_window}. 
{: tip}

Replace `<user_ID>`, `<Admin_IAM_token>`, `<IAM_role>`, `<account_ID>`, `<instance_ID>` and `<key_ID>` with the appropriate values.

**Optional:** Verify that the policy was successfully created.

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a/<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}


## Updating an access policy
{: #update_policy}

You can use a retrieved policy ID to modify an existing policy for a user. Send a request to {{site.data.keyword.iamshort}} by running the following command:

```cURL
curl -X PUT \
  https://iam.bluemix.net/acms/v1/scopes/a/<account_ID>/users/<user_ID>/policies/<policy_ID> \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'If-Match': <ETag_ID> \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
  "roles": [
    {
      "id": "crn:v1:bluemix:public:iam::::role:<IAM_role>"
    }
  ],
  "resources": [
    {
      "serviceName": "IBM Key Protect",
      "accountId": "<account_ID>",
      "region": "us-south",
      "serviceInstance": "<instance_ID>",
      "resourceType": "key",
      "resource": "<key_ID>"
    }
  ]
}'
```
{: codeblock}

Replace `<user_ID>`, `<Admin_IAM_token>`, `<IAM_role>`, `<account_ID>`, `<instance_ID>` and `<key_ID>` with the appropriate values.

**Optional:** Verify that the policy was successfully updated.

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a/<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

## Deleting an access policy
{: #delete_policy}

You can use a retrieved policy ID to delete an existing policy for a user. Send a request to {{site.data.keyword.iamshort}} by running the following command:

```cURL
curl -X DELETE \
  https://iam.bluemix.net/acms/v1/scopes/a/<account_ID>/users/<user_ID>/policies/<policy_ID> \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

Replace `<account_ID>`, `<user_ID>`, `<policy_ID>`, and  `<Admin_IAM_token>` with the appropriate values.

**Optional:** Verify that the policy was successfully deleted.

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a/<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

## Retrieving the account ID
{: #retrieve_account_id}

1. Log in to the {{site.data.keyword.cloud_notm}} (bx) CLI.
    ```sh
    bx login [--sso]
    ```
    {: codeblock}

    **Note**: The `--sso` parameter is required when you log in with a federated ID. If this option is used, go to the link listed in the CLI output to generate a one-time passcode.

    The result displays the identifying information for your account.

    ```sh
    Authenticating...
    OK

    Select an account (or press enter to skip):

    1. sample-account (b6hnh3560ehqjkf89s4ba06i367801e)
    Enter a number> 1
    Targeted account sample-acount (b6hnh3560ehqjkf89s4ba06i367801e)

    API endpoint:   https://api.ng.bluemix.net (API version: 2.75.0)
    Region:         us-south
    User:           admin
    Account:        sample-account (b6hnh3560ehqjkf89s4ba06i367801e)
    ```
    {: screen}
2. Copy the value for your account ID.

## Retrieving the user ID
{: #retrieve_user_id}

1. [Ask the user to provide his or her IAM token](/docs/services/keymgmt/keyprotect_authentication.html#retrieve_token).
    The IAM token structure is as follows:

    ```sh
    IAM token: Bearer <value>.<value>.<value>
    ```
    {: screen}

2. Copy the middle value and run the following command:
    ```sh
    echo -n "<value>" | base64 --decode
    ```
    {: codeblock}

    The result shows a JSON object similar to the following:
   ```json
   {
        "iam_id":"...",
        "id":"...",
        "realmid":"...",
        "identifier":"...",
        "given_name":"...",
        "family_name":"...",
        "name":"...",
        "email":"...",
        "sub":"...",
        "account":{
            "bss":"..."},
            "iat":...,
            "exp":...,
            "iss":"...",
            "grant_type":"...",
            "scope":"...",
            "client_id":"..."
        }
   }
   ```
   {: screen}

4. Copy the value of the `id` property.