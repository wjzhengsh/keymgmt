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

# 키 상태
{: #key_states}

{{site.data.keyword.keymanagementservicefull}}는 [키 상태와 관련된 NIST SP 800-57 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf){: new_window}의 보안 가이드라인을 따릅니다.
{: shortdesc}

키는 자체 라이프사이클에서 일련의 4개 상태 간에 이동할 수 있습니다.
- _활성화 이전_. 처음에 키는 _활성화 이전_ 상태로 작성됩니다.
- _활성화됨_. 키는 활성화 날짜에 즉시 _활성화됨_ 상태로 이동됩니다. 활성화 날짜가 없는 키는 즉시 활성화되며, 만료되거나 영구 삭제될 때까지 활성화된 상태를 유지합니다.
- _비활성화됨_. 키는 만기 날짜에 _비활성화됨_ 상태로 이동됩니다(만기 날짜가 지정된 경우). 이 상태에서 키는 데이터를 암호로 보호할 수 없으며 오직 _영구 삭제됨_ 상태로만 이동이 가능합니다.
- _영구 삭제됨_. 삭제된 키는 _영구 삭제됨_ 상태입니다. 이 상태의 키는 복구가 불가능합니다.
