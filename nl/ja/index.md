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

# {{site.data.keyword.keymanagementserviceshort}} の概説

{{site.data.keyword.keymanagementservicefull}} 内の鍵の生成、入力、および管理を行うために必要な手順を以下に示します。
{: shortdesc}

## 前提条件
{: #prereqs }

{{site.data.keyword.keymanagementserviceshort}} をサービスやアプリで使用すると、正しい許可を使用して、{{site.data.keyword.keymanagementserviceshort}} に対する API 呼び出しを行うことができます。鍵を追加する前に、以下のものが必要です。
- [IBM ID とパスワード](https://console.bluemix.net/docs/admin/adminpublic.html#signing-up-for-bluemix){: new_window}
- [サービスのインスタンス](https://console.ng.bluemix.net/catalog/services/key-protect/?taxonomyNavigation=apps){: new_window}

## 鍵の追加
{: #addkey }

以下の手順を使用して、新しい鍵を作成するか、既存の鍵をアップロードします。

1. [{{site.data.keyword.cloud_notm}} コンソールにログインします。](https://console.bluemix.net/catalog){: new_window}
2. **「すべてのカテゴリー」**リンクの上にカーソルを移動して、スクロール・バーを表示します。**「サービス」>「セキュリティー」**にスクロールダウンします。アプリおよびサービスのリストが表示されます。
3. **{{site.data.keyword.keymanagementserviceshort}}** サービス・インスタンスをダブルクリックします。**「アクション」**の下で、サービスの名前変更や削除を行えます。

初めて鍵を入力または生成している場合は、**「新しい鍵の追加 (Add a new key)」**ページが自動的に表示されます。{{site.data.keyword.keymanagementserviceshort}} に真新しい鍵を生成するには**「新しい鍵の生成 (Generate New Key)」**を使用し、既存の鍵をサービスに入力するには**「既存の鍵の入力 (Enter Existing Key)」**を使用します。

### 鍵の生成
{: #genkey }

以下の手順を使用して、{{site.data.keyword.keymanagementserviceshort}} で新しい鍵を生成します。

1. {{site.data.keyword.keymanagementserviceshort}} で新しい鍵を作成するために、**「新しい鍵の生成 (Generate new key)」**で以下を入力します。<table>
      <tr>
        <th>フィールド</th>
        <th>説明</th>
      </tr>
      <tr>
        <td>名前</td>
        <td>鍵に割り当てる、人間が読める別名。名前は、鍵の使用目的や鍵が関連付けられているユーザーなど、鍵の識別に役立つものであればどのようなものでも構いません。</td>
      </tr>
      <tr>
        <td>鍵のタイプ</td>
        <td>デフォルトでは「標準」鍵になります。標準鍵は、プレーン・テキスト・データを暗号化して暗号文にするためのデータ暗号化鍵として使用されます。</td>
      </tr>
        <caption style="caption-side:bottom;">表 1. 「新しい鍵の生成 (Generate new key)」の設定の説明</caption>
    </table>

2. **「鍵の生成 (Generate key)」**ボタンをクリックします。鍵は即時に使用可能になります。新規の鍵は、セキュアな {{site.data.keyword.IBM}} データ・センター内にあるハードウェア・セキュリティー・モジュールによって生成されます。
3. 鍵の行に参照 ID をコピーします。**ID** 値は、{{site.data.keyword.keymanagementserviceshort}} API で使用する ID です。

### 既存の鍵の入力
{: #existkey }

以下の手順を使用して、既存の鍵を Key Protect に入力します。

1. **「既存の鍵の入力 (Enter existing key)」**の下で以下を入力します。<table>
      <tr>
        <th>フィールド</th>
        <th>説明</th>
      </tr>
      <tr>
        <td>名前</td>
        <td>鍵に割り当てる、人間が読める別名。名前は、鍵の使用目的や鍵が関連付けられているユーザーなど、鍵の識別に役立つものであればどのようなものでも構いません。</td>
      </tr>
      <tr>
        <td>鍵のタイプ</td>
        <td>デフォルトでは「標準」鍵になります。標準鍵は、プレーン・テキスト・データを暗号化して暗号文にするためのデータ暗号化鍵として使用されます。</td>
      </tr>
      <tr>
        <td>鍵の素材</td>
        <td>鍵の素材には、証明書や RSA 鍵など、{{site.data.keyword.keymanagementserviceshort}} サービス内に保管したい任意のタイプのデータを使用できます。</td>
      </tr>
        <caption style="caption-side:bottom;">表 2. 「既存の鍵の入力 (Enter existing key)」の設定の説明</caption>
    </table>

2. **「新しい鍵の追加 (Add a new key)」**ボタンをクリックします。鍵は即時に使用可能になります。
3. 鍵の行に参照 ID をコピーします。**ID** 値は、{{site.data.keyword.keymanagementserviceshort}} API で使用する ID です。

## 鍵の管理
{: #managekey }

鍵を生成して入力した後で鍵を確認するには、[「鍵の追加 (Adding a key)」](index.html#addkey)の下で以下の手順を実行します。**「鍵 (Keys)」**ウィンドウが表示されます。鍵は、最新の鍵をリストの先頭にして、作成日順に表示されます。
<table>
      <tr>
        <th>列</th>
        <th>説明</th>
      </tr>
      <tr>
        <td>名前</td>
        <td>鍵に割り当てられた、人間が読める別名。</td>
      </tr>
      <tr>
        <td>ID</td>
        <td>{{site.data.keyword.keymanagementserviceshort}} によって鍵に割り当てられた固有の鍵 ID。</td>
      </tr>
      <tr>
        <td>状況</td>
        <td>米国連邦情報・技術局 (NIST) の鍵の状態 (アクティベーション前、アクティブ、非アクティブ化、破棄) のいずれか。<td>
      </tr>
      <tr>
        <td>作成</td>
        <td>鍵が作成された日付と時刻。</td>
      </tr>
      <tr>
        <td>タイプ</td>
        <td>デフォルトは「標準」鍵です。</td>
      </tr>
      <caption style="caption-side:bottom;">表 3. 「鍵 (Keys)」ウィンドウの説明</caption>
    </table>

### 次に行うこと

これで、鍵を使用してアプリやサービスをコーディングできるようになりました。

- {{site.data.keyword.keymanagementserviceshort}} に保管されている鍵を使用してデータを暗号化および暗号化解除する方法の例は、[Github にあるサンプル・アプリで確認してください ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}。
- 鍵のプログラマチックな管理について詳しくは、[{{site.data.keyword.keymanagementserviceshort}} API リファレンス資料](https://console.ng.bluemix.net/apidocs/639)に記載されているコード・サンプルを確認してください。

### 関連リンク

- [{{site.data.keyword.keymanagementserviceshort}} REST API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/apidocs/639){: new_window}
- [{{site.data.keyword.keymanagementserviceshort}} 管理 REST API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs-admin-keyprotect.ng.bluemix.net/){: new_window}
- [{{site.data.keyword.cloud_notm}} HSM オファリング ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.softlayer.com/ibm-cloud-hsm){: new_window}
- [{{site.data.keyword.keymanagementservicelong_notm}}サービス・レベル・アグリーメント ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www-03.ibm.com/software/sla/sladb.nsf/sla/bm-7603-01){: new_window}
