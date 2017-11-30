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

# 使用 API 管理金鑰的存取
{: #managing-access-api}

使用 {{site.data.keyword.iamlong}}，您可以建立及修改存取原則，為金鑰資源啟用精細的存取控制。
{: shortdesc}

此頁面帶領您查看數個情境，使用[存取管理 API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://iampap.ng.bluemix.net/v1/docs/#!/Access_Policies/){: new_window} 管理金鑰資源的存取。


開始之前：
- [擷取 IAM 記號及空間 GUID](/docs/services/keymgmt/keyprotect_authentication.html)
- [擷取金鑰 ID 以指定資源](/docs/services/keymgmt/keyprotect_view_keys.html)
- [擷取帳戶 ID 以指定存取範圍](keyprotect_manage_access_api.html#retrieve_account_ID)
- [擷取您要修改其存取權的使用者 ID](keyprotect_manage_access_api.html#retrieve_user_ID)

## 建立新的存取原則
{: #create_policy}

若要啟用特定金鑰的存取控制，您可以藉由執行下列指令，傳送要求至 {{site.data.keyword.iamshort}}。請針對每個存取原則重複指令。

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

將 `<account_ID>`、`<user_ID>`、`<Admin_IAM_token>`、`<IAM_role>`、`<space_GUID>` 及 `<key_ID>` 取代為適當的值。

**選用項目：**確認已順利建立原則。

```cURL
curl -X GET \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}


## 更新存取原則
{: #update_policy}

您可以使用擷取到的原則 ID，以修改使用者的現有原則。藉由執行下列指令，傳送要求至 {{site.data.keyword.iamshort}}：

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

將 `<account_ID>`、`<user_ID>`、`<policy_ID>`、`<Admin_IAM_token>`、`<ETag_ID>`、`<IAM_role>`、`<space_GUID>` 及 `<key_ID>` 取代為適當的值。

**選用項目：**確認已順利更新原則。

```cURL
curl -X GET \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

## 刪除存取原則
{: #delete_policy}

您可以使用擷取到的原則 ID，以刪除使用者的現有原則。藉由執行下列指令，傳送要求至 {{site.data.keyword.iamshort}}：

```cURL
curl -X DELETE \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies/<policy_ID> \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

將 `<account_ID>`、`<user_ID>`、`<policy_ID>` 及 `<Admin_IAM_token>` 取代為適當的值。

**選用項目：**確認已順利刪除原則。

```cURL
curl -X GET \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

## 擷取帳戶 ID
{: #retrieve_account_id}

1. 登入 Bluemix CLI。
    ```sh
    bx login [--sso]
    ```
    {: codeblock}

    **附註**：當您使用聯合 ID 登入時，需要 `--sso` 參數。如果使用這個選項，請前往 CLI 輸出中所列的鏈結，以產生一次性的通行碼。

    結果會顯示您帳戶的識別資訊。

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
2. 複製帳戶 ID 的值。

## 擷取使用者 ID
{: #retrieve_user_id}

1. [要求使用者提供 IAM 記號](/docs/services/keymgmt/keyprotect_authentication.html#retrieve_token)。IAM 記號結構如下：

    ```sh
    IAM token: Bearer <value>.<value>.<value>
    ```
    {: screen}

2. 複製下列的中間值，並執行下列指令：
    ```sh
    echo -n "<value>" | base64 --decode
    ```
    {: codeblock}

    結果顯示類似於下列內容的 JSON 物件：
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

4. 複製 `id` 內容的值。
