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

# 密钥状态
{: #key_states}

{{site.data.keyword.keymanagementservicefull}} 遵循 [ 密钥状态的 NIST SP 800-57 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf){: new_window} 所提出的安全准则。
{: shortdesc}

密钥可在其生命周期的四个状态的序列中变化：
- _预激活_。密钥最初以_预激活_状态创建。
- _活动_。密钥在激活日期会立即变为_活动_状态。没有激活日期的密钥会立即变为活动状态，并保持活动状态直到到期或已销毁。
- _已停用_。密钥在其到期日期（如果指定的话）会变为_已停用_状态。在此状态下，密钥无法以密码保护数据且仅可以变为_已销毁_状态。
- _已销毁_。已删除的密钥处于_已销毁_状态。处于此状态的密钥不可恢复。
