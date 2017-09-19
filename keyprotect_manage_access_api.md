---

copyright:
  years: 2017
lastupdated: "2017-09-18"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Managing access to keys with the API
{: #managing-access-api}

With {{site.data.keyword.Bluemix}} Identity and Access Management, you can enable granular access control for your key resources by creating and modifying access policies.
{: shortdesc}

This page walks you through several scenarios for managing access to your key resources with the [Access Management API](https://iampap.ng.bluemix.net/v1/docs/#!/Access_Policies/){: new_window}.


Before you begin:
- [Retrieve your IAM token and space GUID](keyprotect_authentication.html)
- [Retrieve the key ID to specify the resource](keyprotect_view_keys.html#get_keys)
- [Retrieve the account ID to specify the scope of access](#retrieve_account_ID)
- [Retrieve the user ID of the user whose access you would like to modify](#retrieve_user_ID)

## Creating a new access policy
{: #create_policy}

To enable access control for a specific key, you can send a request to {{site.data.keyword.Bluemix_notm}} Identity and Access Management by running the following command. Repeat the command for each access policy.

```cURL
curl -X POST \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies \
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
      "region": "us-south",
      "resourceType": "key",
      "resource": "<key_ID>",
      "accountId": "<account_ID>",
      "spaceId": "<space_GUID>"
    }
  ]
}'
```
{: codeblock}

Replace `<account_ID>`, `<user_ID>`, `<Admin_IAM_token>`, `<IAM_role>`, `<space_GUID>` and `<key_ID>` with the appropriate values.

**Optional:** Verify that the policy was successfully created.

```cURL
curl -X GET \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}


## Updating an access policy
{: #update_policy}

You can use a retrieved policy ID to modify an existing policy for a user. Send a request to {{site.data.keyword.Bluemix_notm}} Identity and Access Management by running the following command:

```cURL
curl -X PUT \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies/<policy_ID> \
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
      "region": "us-south",
      "resourceType": "key",
      "resource": "<key_ID>",
      "accountId": "<account_ID>",
      "spaceId": "<space_GUID>"
    }
  ]
}'
```
{: codeblock}

Replace `<account_ID>`, `<user_ID>`, `<policy_ID>`, `<Admin_IAM_token>`, `<ETag_ID>`, `<IAM_role>`, `<space_GUID>` and `<key_ID>` with the appropriate values.

**Optional:** Verify that the policy was successfully updated.

```cURL
curl -X GET \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

## Deleting an access policy
{: #delete_policy}

You can use a retrieved policy ID to delete an existing policy for a user. Send a request to {{site.data.keyword.Bluemix_notm}} Identity and Access Management by running the following command:

```cURL
curl -X DELETE \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies/<policy_ID> \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

Replace `<account_ID>`, `<user_ID>`, `<policy_ID>`, and  `<Admin_IAM_token>` with the appropriate values.

**Optional:** Verify that the policy was successfully deleted.

```cURL
curl -X GET \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

## Retrieving the account ID
{: #retrieve_account_id}

1. Log in to the {{site.data.keyword.Bluemix_notm}} CLI.
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

1. [Ask the user to provide his or her IAM token](keyprotect_authentication.html#get_token).
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
