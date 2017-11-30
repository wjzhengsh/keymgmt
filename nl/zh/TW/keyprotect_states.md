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

# 金鑰狀態
{: #key_states}

{{site.data.keyword.keymanagementservicefull}} 遵循 [NIST SP 800-57 對於金鑰狀態 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf){: new_window} 的安全準則。
{: shortdesc}

金鑰可能會在其生命週期中，在一系列四種狀態移動：
- _啟動前 (Pre-activation)_。金鑰一開始是以_啟動前_ 狀態建立。
- _作用中 (Active)_。金鑰在啟動日立即進入_作用中_ 狀態。沒有啟動日的金鑰，會立即變為作用中，並維持作用中一直到它們到期或被破壞為止。
- _取消啟動 (Deactivated)_。金鑰在到期日（如果已指派的話）立即進入_取消啟動_ 狀態。在這個狀態下，金鑰無法以加密方式保護資料，且只能進入_已破壞_ 狀態。
- _已破壞 (Destroyed)_。已刪除的金鑰處於_已破壞_ 狀態。在這個狀態下無法回復金鑰。
