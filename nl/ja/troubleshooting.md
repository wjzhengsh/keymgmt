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

# トラブルシューティング

{{site.data.keyword.keymanagementservicefull}} の使用に関する一般的なトラブルシューティングの質問への回答を示します。
{: shortdesc}

## 鍵の作成または削除ができない
{: #unabletomanagekeys}

{{site.data.keyword.keymanagementserviceshort}} アクションを実行できない場合は、正しい権限を付与されているか確認してください。

### 症状

{{site.data.keyword.keymanagementserviceshort}} ユーザー・インターフェースにアクセスしたときに、鍵の追加や削除のためのオプションを表示できない。

### 問題の解決

該当スペースにおける正しい役割を割り当てられているかどうか、スペース管理者に確認してください。役割について詳しくは、[鍵およびアクセスの監査](managing-keys.html#viewkeyassignments)を参照してください。

## ベータ版から General Assembly (GA) への変換
{: #ts_planconversion}

{{site.data.keyword.keymanagementserviceshort}} サービスを継続的に使用するには、ベータ版のユーザーは標準価格モデルに変更する必要があります。

### 症状

ベータ版のユーザーの場合、{{site.data.keyword.keymanagementserviceshort}} への鍵の保管を継続するには、価格プランを段階制の価格モデルに変更する必要があります。

### 問題の解決

{{site.data.keyword.keymanagementserviceshort}} サービスには、ライトと累進階層の 2 種類の価格モデルがあります。組織またはスペースの管理者として、累進階層モデルを選択済みであることを確認してください。段階制モデルへの移行を希望しない場合は、非推奨になる前に、すべての鍵とサービス・インスタンスを必ず削除してください。[詳しくは、{{site.data.keyword.keymanagementserviceshort}} General Assembly に関する発表を参照してください ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")]( "https://www.ibm.com/blogs/bluemix/2016/12/dallas-key-protect-ga/"){: new_window}。

価格プランを変更するには、以下を行います。

1. {{site.data.keyword.keymanagementserviceshort}} ユーザー・インターフェースに移動し、**「プラン」**タブを選択します。
2. **「累進階層の価格 (Graduated Tier Pricing)」**を選択します。1 カ月当たりに使用されるアクティブ鍵の費用の明細が表に示されます。段階制モデルでは、アカウント・レベルで 1 カ月当たりのアクティブ鍵の数に基づいて価格を計算します。
3. プランの変更を確認するには、**「保存」**をクリックします。

## {{site.data.keyword.keymanagementserviceshort}} のヘルプおよびサポートの利用
{: #ts_gettinghelp}

{{site.data.keyword.keymanagementservicefull_notm}} の使用に関して問題や質問がある場合は、情報を検索したり、フォーラムで質問したりして、支援を得ることができます。サポート・チケットを開くこともできます。

フォーラムを使用して質問するときは、{{site.data.keyword.IBM_notm}} {{site.data.keyword.Bluemix_notm}} 開発チームの目に止まるように、質問にタグを付けてください。


- {{site.data.keyword.keymanagementserviceshort}} について技術的な質問がある場合は、[Stack Overflow ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://stackoverflow.com/search?q=key-protect+ibm-bluemix "外部リンク・アイコン"){: new_window} に質問を投稿し、その質問に「ibm-bluemix」と「key-protect」のタグを付けてください。
- サービスや使用開始の手順についての質問には、[IBM developerWorks dW Answers ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.ibm.com/answers/topics/key-protect/?smartspace=bluemix "外部リンク・アイコン"){: new_window} フォーラムを使用してください。「bluemix」と「key-protect」のタグを付けてください。

フォーラムの使用について詳しくは、[ヘルプの利用 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.bluemix.net/docs/support/index.html#getting-help "外部リンク・アイコン"){: new_window} を参照してください。

{{site.data.keyword.IBM_notm}} サポート・チケットのオープンや、サポート・レベルおよびチケットの重大度については、[サポートへの問い合わせ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.bluemix.net/docs/support/index.html#contacting-support "外部リンク・アイコン"){: new_window} を参照してください。
