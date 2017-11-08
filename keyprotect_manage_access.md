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

# Managing user access with Identity and Access Management
{: #managing-access-iam}

{{site.data.keyword.keymanagementservicefull}} supports a centralized access control system, governed by {{site.data.keyword.iamlong}}, to help you manage users and access for your encryption keys.
{: shortdesc}

A good practice is to grant access permissions as you invite new users to your account or service. For example, consider the following guidelines:

- **Enable user access to the resources in your account by assigning IAM roles.**
    Rather than sharing your admin credentials, create new policies for users who need access to the encryption keys in your account. If you are the admin for your account, you are automatically assigned an admin policy with access to all resources under the account.
- **Grant roles and permissions at the smallest scope needed.**
    For example, if a user only needs to access a high-level view of keys within a specified space, grant the _Viewer_ role to the user for that space.
- **Regularly audit who has the ability to manage access control and delete key resources.**
    Remember that granting an _Administrator_ role to a user means that the user can modify service policies for other users, in addition to destroying resources.

## Roles and permissions
{: #roles}

With {{site.data.keyword.iamshort}} (IAM), you can set policies that define the scope of access for members of your team.

To simplify access, {{site.data.keyword.keymanagementserviceshort}} aligns with IAM roles so that each user has a different view of the service, according to the role the user is assigned. If you are a security admin for your service, you can assign IAM roles that correspond to the specific {{site.data.keyword.keymanagementserviceshort}} permissions you want to grant to members of your team.

The following table shows how identity and access roles map to {{site.data.keyword.keymanagementserviceshort}} permissions:
<table>
  <tr>
    <th>Role</th>
    <th>Description</th>
    <th>Actions</th>
  </tr>
  <tr>
    <td>Viewer</td>
    <td>A viewer can access a high-level view of keys. Viewers cannot access or modify key details.</td>
    <td>
      <ul>
        <li>View keys</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Editor</td>
    <td>An editor can create keys, modify keys, and view key details.</td>
    <td>
      <ul>
        <li>Create keys</li>
        <li>View keys</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Administrator</td>
    <td>An administrator can perform all actions that a viewer and editor can perform, including the ability to delete keys, invite new users, and manage access control. </td>
    <td>
      <ul>
        <li>Create keys</li>
        <li>View keys</li>
        <li>Delete keys</li>
        <li>Manage access control</li>
      </ul>
    </td>
  </tr>
  <caption style="caption-side:bottom;">Table 1. Mapping of identity and access roles to {{site.data.keyword.keymanagementserviceshort}} permissions.</caption>
</table>

**Note**: IAM user roles provide access at the service or service instance level. [Cloud Foundry roles](/docs/iam/users_roles.html#cfroles) are separate and define access at the organization or the space level.

To learn more about {{site.data.keyword.iamshort}}, check out [User roles and permissions](/docs/iam/users_roles.html#iamusermanpol).

### What's next

Account owners and admins can invite users and set service policies that correspond to the {{site.data.keyword.keymanagementserviceshort}} actions the users can perform.

- For information about assigning user roles in the {{site.data.keyword.cloud_notm}} UI, see [Identity and access-enabled service access policies](/docs/iam/iamusermanage.html#iammanidaccser).
- To learn about granting advanced permissions to access specific encryption keys, see [Managing access to keys with the API](/docs/services/keymgmt/keyprotect_manage_access_api.html).
