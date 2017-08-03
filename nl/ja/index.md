---

copyright:
  years: 2017
lastupdated: "2017-08-03"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# {{site.data.keyword.keymanagementserviceshort}} の概説

{{site.data.keyword.keymanagementservicelong}} は、{{site.data.keyword.Bluemix_short}} 上のアプリの暗号鍵をプロビジョンするときに役立ちます。鍵のライフサイクルを管理する際に、情報の盗難を防止するクラウド・ベースのハードウェア・セキュリティー・モジュール (HSM) によって鍵が保護されていることを認識していると役立つことがあります。{: shortdesc}

{{site.data.keyword.keymanagementserviceshort}} は、それが作成されたスペース内のすべてのアプリに対して自動的に使用可能になります。[サービスのインスタンスを作成した後](https://console.ng.bluemix.net/catalog/services/key-protect/?taxonomyNavigation=apps){: new_window}、以下の手順を実行して、稼働します。

1. 鍵を作成するか、既存の鍵をアップロードするために、**「鍵の追加」**をクリックします。
    鍵の詳細を以下のように指定します。
<table>
      <tr>
        <th>設定</th>
        <th>説明</th>
      </tr>
      <tr>
        <td>名前</td>
        <td>鍵に割り当てる、人間が読める別名。名前は、鍵の使用目的や鍵が関連付けられているユーザーなど、鍵の識別に役立つものであればどのようなものでも構いません。</td>
      </tr>
      <tr>
        <td>アルゴリズム</td>
        <td>対称鍵暗号化は、AES-GCM アルゴリズムによってサポートされます。</td>
      </tr>
      <tr>
        <td>鍵</td>
        <td>既存の鍵を追加する場合にのみ必須。鍵の素材には、証明書や RSA 鍵など、{{site.data.keyword.keymanagementserviceshort}} サービス内に保管したい任意のタイプのデータを使用できます。</td>
      </tr>
        <caption style="caption-side:bottom;">表 1. 鍵の設定の説明</caption>
    </table>

2. 鍵の詳細の入力が完了したら、**「鍵の追加」**をクリックして確認します。鍵は即時に使用可能になります。新規の鍵は、セキュアな {{site.data.keyword.IBM}} データ・センター内にあるハードウェア・セキュリティー・モジュールによって生成されます。
3. 鍵の行に参照 ID をコピーします。**ID** 値は、{{site.data.keyword.keymanagementserviceshort}} API で使用する ID です。
4. **オプション**: 鍵を削除する場合、鍵の素材はリカバリーできないことに留意してください。鍵に関連付けられているメタデータは、{{site.data.keyword.keymanagementserviceshort}} データベースに保管されます。鍵を削除するには、鍵の行内の**「アクション」**アイコンをクリックし、次の画面で削除を確認します。

次の作業:

これで、鍵を使用してアプリやサービスをコーディングできるようになりました。

- {{site.data.keyword.keymanagementserviceshort}} に保管されている鍵を使用してデータを暗号化および暗号化解除する方法の例は、[Github にあるサンプル・アプリで確認してください ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/IBM-Bluemix/key-protect-helloworld-python "外部リンク・アイコン"){: new_window}。
- 鍵のプログラマチックな管理について詳しくは、[{{site.data.keyword.keymanagementserviceshort}} API リファレンス資料](https://console.ng.bluemix.net/apidocs/639)に記載されているコード・サンプルを確認してください。

## 関連リンク

- [{{site.data.keyword.keymanagementserviceshort}} REST API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/apidocs/639 "外部リンク・アイコン"){: new_window}
- [{{site.data.keyword.keymanagementserviceshort}} 管理 REST API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs-admin-keyprotect.ng.bluemix.net/ "外部リンク・アイコン"){: new_window}
- [クラウド HSM オファリング ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.softlayer.com/ibm-cloud-hsm "外部リンク・アイコン"){: new_window}
