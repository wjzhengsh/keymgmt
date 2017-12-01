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

# {{site.data.keyword.keymanagementserviceshort}} 시작하기

다음은 {{site.data.keyword.keymanagementservicefull}} 내에서 키를 생성, 입력하고 관리하는 데 필요한 단계입니다.
{: shortdesc}

## 전제조건
{: #prereqs }

{{site.data.keyword.keymanagementserviceshort}}는 올바른 권한으로 {{site.data.keyword.keymanagementserviceshort}}에 대한 API 호출을 작성할 수 있는 서비스와 앱에 사용 가능합니다. 키를 추가하기 전에 다음이 필요합니다.
- [IBM ID 및 비밀번호](https://console.bluemix.net/docs/admin/adminpublic.html#signing-up-for-bluemix){: new_window}
- [서비스의 인스턴스](https://console.ng.bluemix.net/catalog/services/key-protect/?taxonomyNavigation=apps){: new_window}

## 키 추가
{: #addkey }

다음 단계를 사용하여 새 키를 작성하거나 기존 키를 업로드할 수 있습니다.

1. [{{site.data.keyword.cloud_notm}} 콘솔에 로그인하십시오.](https://console.bluemix.net/catalog){: new_window}
2. **모든 카테고리** 링크 위에 마우스 커서를 올려놓아 화면이동 막대를 표시하십시오. **서비스 > 보안**으로 스크롤 다운하십시오. 앱과 서비스의 목록이 나타납니다.
3. **{{site.data.keyword.keymanagementserviceshort}}** 서비스 인스턴스를 두 번 클릭하십시오. 참고로, **조치** 아래에서 서비스의 이름을 바꾸거나 서비스를 삭제할 수 있습니다.

처음으로 키를 입력하거나 생성하는 경우에는 자동으로 **새 키 추가** 페이지로 이동됩니다. **새 키 생성**을 사용하여 {{site.data.keyword.keymanagementserviceshort}}에서 완전히 새로운 키를 생성할 수 있으며, **기존 키 입력**을 사용하여 서비스에 기존 키를 입력할 수 있습니다.

### 키 생성
{: #genkey }

다음 단계를 사용하여 {{site.data.keyword.keymanagementserviceshort}}에서 새 키를 생성하도록 하십시오. 

1. **새 키 생성** 아래에서 다음을 입력하여 {{site.data.keyword.keymanagementserviceshort}}에서 새 키를 생성하도록 하십시오.
    <table>
      <tr>
        <th>필드</th>
        <th>설명</th>
      </tr>
      <tr>
        <td>이름</td>
        <td>키에 지정할, 사용자가 읽을 수 있는 별명입니다. 키의 용도 또는 키와 연관된 사용자와 같이, 키를 식별하는 데 도움이 되는 이름을 지정할 수 있습니다.</td>
      </tr>
      <tr>
        <td>키 유형</td>
        <td>기본값은 표준 키입니다. 표준 키는 평문 데이터를 암호문으로 암호화하기 위한 데이터 암호화 키로서 사용됩니다.</td>
      </tr>
        <caption style="caption-side:bottom;">표 1. 새 키 생성 설정에 대한 설명</caption>
    </table>

2. **키 생성** 단추를 클릭하십시오. 키는 즉시 사용 가능합니다. 새 키는 안전한 {{site.data.keyword.IBM}} 데이터 센터에 위치한 HSM(Hardware Security Module)에 의해 생성됩니다.
3. 키의 행에서 참조 ID를 복사하십시오. **ID** 값은 {{site.data.keyword.keymanagementserviceshort}} API에서 사용하는 ID입니다.

### 기존 키 입력
{: #existkey }

다음 단계를 사용하여 Key Protect에 기존 키를 입력할 수 있습니다.

1. **기존 키 입력** 아래에서 다음을 입력하십시오.
    <table>
      <tr>
        <th>필드</th>
        <th>설명</th>
      </tr>
      <tr>
        <td>이름</td>
        <td>키에 지정할, 사용자가 읽을 수 있는 별명입니다. 키의 용도 또는 키와 연관된 사용자와 같이, 키를 식별하는 데 도움이 되는 이름을 지정할 수 있습니다.</td>
      </tr>
      <tr>
        <td>키 유형</td>
        <td>기본값은 표준 키입니다. 표준 키는 평문 데이터를 암호문으로 암호화하기 위한 데이터 암호화 키로서 사용됩니다.</td>
      </tr>
      <tr>
        <td>키 자료</td>
        <td>키 자료는 {{site.data.keyword.keymanagementserviceshort}} 서비스에 저장할 임의의 데이터 유형(예: 인증서, RSA 키)일 수 있습니다.</td>
      </tr>
        <caption style="caption-side:bottom;">표 2. 기존 키 입력 설정의 설명</caption>
    </table>

2. **새 키 추가** 단추를 클릭하십시오. 키는 즉시 사용 가능합니다.
3. 키의 행에서 참조 ID를 복사하십시오. **ID** 값은 {{site.data.keyword.keymanagementserviceshort}} API에서 사용하는 ID입니다.

## 키 관리
{: #managekey }

키를 생성하고 입력한 후에 이를 보려면 [키 추가](index.html#addkey)의 단계를 따르십시오. 사용자는 **키** 창으로 이동됩니다. 키는 작성한 날짜 순으로 표시되며 가장 최신 키가 목록의 맨 위에 표시됩니다.
<table>
      <tr>
        <th>열</th>
        <th>설명</th>
      </tr>
      <tr>
        <td>이름</td>
        <td>키에 지정된 읽을 수 있는 별명입니다.</td>
      </tr>
      <tr>
        <td>ID</td>
        <td>{{site.data.keyword.keymanagementserviceshort}}에서 키에 지정한 고유 키 ID입니다. </td>
      </tr>
      <tr>
        <td>상태</td>
        <td>NIST(National Institute of Standards and Technology) 키 상태 중 하나입니다(활성화 이전, 활성화됨, 비활성화됨 및 영구 삭제됨).<td>
      </tr>
      <tr>
        <td>작성 날짜 및 시간</td>
        <td>키가 작성된 날짜 및 시간입니다.</td>
      </tr>
      <tr>
        <td>유형</td>
        <td>기본값은 표준 키입니다.</td>
      </tr>
      <caption style="caption-side:bottom;">표 3. 키 설명 창</caption>
    </table>

### 다음에 수행할 작업

이제 키를 사용하여 앱과 서비스를 코딩할 수 있습니다.

- {{site.data.keyword.keymanagementserviceshort}}의 키 저장소가 데이터 암호화 및 복호화를 수행하는 방법에 대한 예를 보려면 [Github의 샘플 앱을 확인 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}하십시오.
- 프로그래밍 방식의 키 관리에 대한 자세한 정보를 보려면 [{{site.data.keyword.keymanagementserviceshort}} API 참조 문서](https://console.ng.bluemix.net/apidocs/639)에서 코드 샘플을 확인하십시오.

### 관련 링크

- [{{site.data.keyword.keymanagementserviceshort}} REST API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/apidocs/639){: new_window}
- [{{site.data.keyword.keymanagementserviceshort}} admin REST API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs-admin-keyprotect.ng.bluemix.net/){: new_window}
- [{{site.data.keyword.cloud_notm}} HSM 오퍼링 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.softlayer.com/ibm-cloud-hsm){: new_window}
- [{{site.data.keyword.keymanagementservicelong_notm}} SLA(Service Level Agreement) ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www-03.ibm.com/software/sla/sladb.nsf/sla/bm-7603-01){: new_window}
