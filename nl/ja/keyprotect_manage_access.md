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

# Identity and Access Management を使用したユーザーのアクセス権限の管理
{: #managing-access-iam}

{{site.data.keyword.keymanagementservicefull}} では、暗号鍵のユーザーおよびアクセス権限の管理に役立つように、{{site.data.keyword.iamlong}} によって管理される集中アクセス制御システムをサポートしています。
{: shortdesc}

新規ユーザーをアカウントまたはサービスに招待する際にアクセス許可を付与することをお勧めします。例えば、以下のガイドラインについて考慮してください。

- **IAM 役割を割り当てることで、アカウントのリソースに対するユーザーのアクセス権限を有効にします。** 管理者の資格情報を共有するのではなく、管理者アカウントの暗号鍵にアクセスする必要があるユーザー向けに新規ポリシーを作成します。アカウントの管理者には、アカウント内のすべてのリソースに対してアクセス権限を持つ管理者ポリシーが自動的に割り当てられます。
- **必要最小限の有効範囲で、役割および許可を付与します。** 例えば、ユーザーが指定のスペース内の鍵の概略にのみアクセスする必要がある場合、そのユーザーには、そのスペースに対する_閲覧者_ 役割のみを付与します。
- **アクセス制御の管理および鍵リソースの削除の権限を持つユーザーを定期的に監査します。** ユーザーに対して_管理者_ 役割を付与することは、そのユーザーは他のユーザーのサービス・ポリシーを変更できるだけでなく、リソースを破棄することもできることを意味します。

## 役割と許可
{: #roles}

{{site.data.keyword.iamshort}} (IAM) を使用して、チームのメンバーに対してアクセス権限の有効範囲を定義するポリシーを設定できます。

アクセスを簡素化するために、{{site.data.keyword.keymanagementserviceshort}} は IAM 役割と調整し、ユーザーが割り当てられている役割に応じて、各ユーザーが異なるビューのサービスを持つようにします。サービスのセキュリティー管理者は、チームのメンバーに付与する特定の {{site.data.keyword.keymanagementserviceshort}} 許可に対応する IAM 役割を割り当てることができます。

次の表は、ID とアクセス役割が {{site.data.keyword.keymanagementserviceshort}} 許可にどのようにマップされるかを示しています。
<table>
  <tr>
    <th>役割</th>
    <th>説明</th>
    <th>アクション</th>
  </tr>
  <tr>
    <td>閲覧者</td>
    <td>閲覧者は、鍵の概略にアクセスできます。閲覧者は、鍵の詳細へのアクセスおよび変更はできません。</td>
    <td>
      <ul>
        <li>鍵の表示</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>編集者</td>
    <td>編集者は、鍵の作成、鍵の変更、および鍵の詳細の表示を行えます。</td>
    <td>
      <ul>
        <li>鍵の作成</li>
        <li>鍵の表示</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>管理者</td>
    <td>管理者は、鍵の削除、新規ユーザーの招待、およびアクセス制御の管理を含め、閲覧者および編集者が実行できるすべてのアクションを実行できます。</td>
    <td>
      <ul>
        <li>鍵の作成</li>
        <li>鍵の表示</li>
        <li>鍵の削除</li>
        <li>アクセス制御の管理</li>
      </ul>
    </td>
  </tr>
  <caption style="caption-side:bottom;">表 1. ID とアクセス役割の {{site.data.keyword.keymanagementserviceshort}} 許可へのマッピング。</caption>
</table>

**注**: IAM ユーザー役割は、サービス・レベルまたはサービス・インスタンス・レベルでアクセス権限を提供します。[Cloud Foundry 役割](/docs/iam/users_roles.html#cfroles)は、これとは別個のもので、組織レベルまたはスペース・レベルでアクセス権限を定義します。

{{site.data.keyword.iamshort}} について詳しくは、[ユーザーの役割と許可](/docs/iam/users_roles.html#iamusermanpol)を確認してください。

### 次に行うこと

アカウントの所有者および管理者は、ユーザーを招待し、ユーザーが実行できる {{site.data.keyword.keymanagementserviceshort}} アクションに対応するサービス・ポリシーを設定できます。

- {{site.data.keyword.cloud_notm}} UI でのユーザー役割の割り当てについては、[ID およびアクセス対応サービスのアクセス・ポリシー (Identity and access-enabled service access policies)](/docs/iam/iamusermanage.html#iammanidaccser) を参照してください。
- 特定の暗号鍵にアクセスするための高度な許可の付与については、[API を使用した鍵へのアクセス権限の管理](/docs/services/keymgmt/keyprotect_manage_access_api.html)を参照してください。
