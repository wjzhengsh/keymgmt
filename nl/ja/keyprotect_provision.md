---

copyright:
  years: 2017
lastupdated: "2017-09-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# {{site.data.keyword.keymanagementserviceshort}} サービスのプロビジョニング
{: #provision}

{{site.data.keyword.Bluemix_notm}} コンソールまたは {{site.data.keyword.Bluemix_notm}} CLI を使用して、{{site.data.keyword.keymanagementservicefull}} のセキュア・インスタンスを作成できます。
{: shortdesc}

## {{site.data.keyword.Bluemix_notm}} コンソールからのプロビジョニング
{: #gui}

{{site.data.keyword.Bluemix_notm}} コンソールから {{site.data.keyword.keymanagementserviceshort}} のインスタンスをプロビジョンするには、以下の手順を実行します。

1. [{{site.data.keyword.Bluemix_notm}} アカウント ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.bluemix.net/){: new_window} にログインします。
2. **「カタログ」**をクリックして、{{site.data.keyword.Bluemix_notm}} 上で使用可能なサービスのリストを表示します。
3. **「サービス」**カテゴリーを選択して、**{{site.data.keyword.keymanagementserviceshort}}** タイルをクリックします。
5. サービス・プランを選択し、**「作成」**をクリックして、ログインしている {{site.data.keyword.Bluemix_notm}} 組織およびスペース内の {{site.data.keyword.keymanagementserviceshort}} サービス・インスタンスをプロビジョンします。

## {{site.data.keyword.Bluemix_notm}} CLI からのプロビジョニング
{: #cli}

{{site.data.keyword.Bluemix_notm}} CLI を使用して、{{site.data.keyword.keymanagementserviceshort}} のインスタンスをプロビジョンできます。[コマンド・ライン・ツールをダウンロードしてシステムにインストール](https://clis.ng.bluemix.net/ui/home.html){: new_window}し、以下の手順を実行します。

1. {{site.data.keyword.Bluemix_notm}} CLI にログインします。

    ```sh
    bx login [--sso]
    ```
    {: codeblock}
    **注:** フェデレーテッド ID を使用してログインする場合は、`--sso` パラメーターが必要です。このオプションを使用する場合、CLI 出力にリストされたリンクにアクセスして、ワンタイム・パスコードを生成します。2. {{site.data.keyword.keymanagementserviceshort}} サービス・インスタンスを作成する {{site.data.keyword.Bluemix_notm}} 組織およびスペースを選択します。

    次のコマンドを使用して、ターゲット組織およびスペースを設定することもできます。

    ```sh
    bx target [-o organization_name] [-s space_name]
    ```
    {: codeblock}

3. その地域、組織、およびスペース内の {{site.data.keyword.keymanagementserviceshort}} のインスタンスをプロビジョンします。

    ```sh
    bx service create ibm_key_management TieredPricing [instance_name]
    ```
    {: codeblock}

    _instance_name_ を、サービス・インスタンスの固有の別名に置き換えます。

4. サービス・インスタンスが正常に作成されたことを確認します。

    ```sh
    bx service list
    ```
    {: codeblock}


### 次に行うこと

これで、鍵を使用してアプリやサービスをコーディングできるようになりました。

- {{site.data.keyword.keymanagementserviceshort}} に保管されている鍵を使用してデータを暗号化および暗号化解除する方法の例は、[GitHub にあるサンプル・アプリで確認してください ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}。
- プログラムでの鍵の管理について詳しくは、[{{site.data.keyword.keymanagementserviceshort}} API リファレンス資料に記載されているコード・サンプル ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/apidocs/639){: new_window} を確認してください。
