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

# 鍵の状態
{: #key_states}

{{site.data.keyword.keymanagementservicefull}} は、[NIST SP 800-57 for key states ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf){: new_window} によるセキュリティー・ガイドラインに従っています。
{: shortdesc}

鍵は、ライフサイクルの間に、以下の一連の 4 つの状態を遷移する可能性があります。
- _アクティベーション前_。鍵は、最初に_アクティベーション前_ 状態で作成されます。
- _アクティブ_。鍵は、アクティベーション日に即時に_アクティブ_ 状態に遷移します。アクティベーション日が指定されない鍵は、即時にアクティブになり、有効期限が切れるか破棄されるまでアクティブのままです。
- _非アクティブ化_。鍵は、有効期限が割り当てられている場合、期限日付に_非アクティブ化_ 状態に遷移します。この状態では、鍵は暗号化によってデータを保護することはできず、_破棄_ 状態にのみ遷移できます。
- _破棄_。削除された鍵は、_破棄_ 状態になります。この状態の鍵は、リカバリーできません。
