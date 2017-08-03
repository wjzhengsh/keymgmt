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

# {{site.data.keyword.keymanagementserviceshort}} 시작하기

{{site.data.keyword.keymanagementservicelong}}를 사용하면
{{site.data.keyword.Bluemix_short}}의 앱에 대해 암호화된 키를 프로비저닝할 수 있습니다. 키의 라이프사이클을 관리하는 과정에서 클라우드 기반 HSM(Hardware Security Module)을 활용하여 정보의 도난을 방지하고 키를 보호할 수 있습니다.
{: shortdesc}

{{site.data.keyword.keymanagementserviceshort}}는
작성된 영역 내의 모든 앱에서 자동으로 사용 가능합니다. [서비스의
인스턴스를 작성한 후](https://console.ng.bluemix.net/catalog/services/key-protect/?taxonomyNavigation=apps){: new_window}, 다음 단계를 완료하여 시작 및 실행하십시오.

1. 기존 키를 작성하거나 업로드하려면 **키 추가**를 클릭하십시오.
    키의 세부사항을 지정하십시오.
<table>
      <tr>
        <th>설정</th>
        <th>설명</th>
      </tr>
      <tr>
        <td>이름</td>
        <td>키에 지정할, 사용자가 읽을 수 있는 별명입니다. 키의 용도 또는 키와 연관된 사용자와 같이, 키를 식별하는 데 도움이 되는 이름을 지정할 수 있습니다. </td>
      </tr>
      <tr>
        <td>알고리즘</td>
        <td>AES-GCM 알고리즘으로 대칭 키 암호화가 지원됩니다. </td>
      </tr>
      <tr>
        <td>키</td>
        <td>기존 키를 추가하는 경우에만 필요합니다. 키 자료는
{{site.data.keyword.keymanagementserviceshort}} 서비스에 저장하고자 하는
모든 유형의 데이터가 될 수 있습니다(인증서, RSA 키 등). </td>
      </tr>
        <caption style="caption-side:bottom;">표 1. 키 설정에 대한 설명</caption>
    </table>

2. 키의 세부사항을 모두 채웠으면 **키 추가**를 클릭하여 확인하십시오. 키는 즉시 사용 가능합니다. 새 키는 안전한 {{site.data.keyword.IBM}} 데이터 센터에 위치한 HSM(Hardware Security Module)에 의해 생성됩니다.
3. 키의 행에서 참조 ID를 복사하십시오. **ID** 값은 {{site.data.keyword.keymanagementserviceshort}} API에서 사용하는 ID입니다.
4. **선택사항**: 키를 삭제하려는 경우 키 자료는 삭제 후에 복구할 수 없다는 점을 기억하십시오. 키와 연관된 메타데이터는 {{site.data.keyword.keymanagementserviceshort}} 데이터베이스에 보관됩니다. 키를 삭제하려면 키의 행에서 **조치** 아이콘을 클릭한 후 다음 화면에서 삭제를 확인하십시오.

다음으로 수행할 작업:

이제 키를 사용하여 앱과 서비스를 코딩할 수 있습니다.

- {{site.data.keyword.keymanagementserviceshort}}의 키 저장소가 데이터 암호화 및 복호화를 수행하는 방법에 대한 예를 보려면 [Github의 샘플 앱을 확인 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/IBM-Bluemix/key-protect-helloworld-python ){: new_window}하십시오.
- 프로그래밍 방식의 키 관리에 대한 자세한 정보를 보려면 [{{site.data.keyword.keymanagementserviceshort}} API 참조 문서](https://console.ng.bluemix.net/apidocs/639)에서 코드 샘플을 확인하십시오.

## 관련 링크

- [{{site.data.keyword.keymanagementserviceshort}} REST API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/apidocs/639 ){: new_window}
- [{{site.data.keyword.keymanagementserviceshort}} admin REST API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs-admin-keyprotect.ng.bluemix.net/ ){: new_window}
- [클라우드 HSM 오퍼링 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.softlayer.com/ibm-cloud-hsm ){: new_window}
