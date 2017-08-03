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

# 키 관리

{{site.data.keyword.keymanagementservicelong}} for {{site.data.keyword.Bluemix_short}}를 사용하여 키의 라이프사이클을 관리할 수 있습니다.
{: shortdesc}

가장 좋은 방법은 코드를 개발하면서 키를 안전하게 관리하는 것입니다. 예를 들어,
다른 보안 코딩 사례와 함께 다음 유형의 가이드라인을 고려하십시오.

- 키를 코드에 임베드할 때 보안 영향성을 고려하십시오.
- 앱과 리소스에 대한 프로그래밍 액세스를 위해서만 키를 작성하십시오. 보다 단순한 [사용자 권한 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.bluemix.net/docs/admin/patterns.html#userroles ){: new_window} 부여가 가능하면 키를 작성하지 마십시오.
- 키를 순환하고 사용하지 않는 키를 제거하십시오.
- 민감한 운영에는 다단계 인증을 사용하십시오.
- 각 앱의 키를 분리시켜 앱을 격리시키십시오.
- 매우 민감한 정보를 전송할 때는 프로그램 방식 API를 사용한 작업을 고려하십시오.

## {{site.data.keyword.keymanagementserviceshort}} API의 인증 신임 정보 생성
{: #authentication_api}

{{site.data.keyword.keymanagementservicelong_notm}}는
키를 저장, 검색, 생성하기 위해 어떠한 프로그래밍 언어와도 함께 사용할 수 있는 REST API를 제공합니다.

API 관련 작업을 수행하려면 인증 및 서비스 신임 정보를 생성해야 합니다.

1. Cloud Foundry CLI를 통해 {{site.data.keyword.Bluemix_notm}}에
로그인하십시오.

    ```
    cf login [a api.DomainName] [-sso]
    ```
    {: codeblock}

2. Key Protect 서비스 인스턴스가 포함된 {{site.data.keyword.Bluemix_notm}} 조직과 영역을 선택하십시오.
    CLI 출력의 조직과 영역의 이름을 기록해 두십시오. 또한 `cf
target`을 실행하여 이 정보를 볼 수 있습니다.
3. {{site.data.keyword.Bluemix_notm}} 조직 및 영역 GUID를
검색하십시오.

    ```
    cf org organization_name --guid
    cf space space_name --guid
    ```
    {: codeblock}

4. {{site.data.keyword.Bluemix_notm}} 액세스 토큰을 요청하십시오.

    ```
    cf oauth-token
    ```
    {: codeblock}

    일부가 표시된 다음 예제에서는 {{site.data.keyword.Bluemix_notm}} 토큰 출력을 보여줍니다. _bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7_ 변수는 예제 액세스 토큰입니다.

    ```
    bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7...
    ```
    {: screen}

다음으로 수행할 작업:

영역에서 키 관리를 시작하려면 {{site.data.keyword.keymanagementserviceshort}} [REST API 참조 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/apidocs/639 ){: new_window}를 참조하십시오.


## {{site.data.keyword.keymanagementserviceshort}} API로 키 작성
{: #codingapps}

{{site.data.keyword.keymanagementservicelong_notm}} API를 사용하여 기존 키를 보호하거나 새 키를 생성할 수 있습니다.

다음 엔드포인트에 **POST** 호출을 실행하여 키를 작성하거나 기존 키를 추가하십시오.

```
https://ibm-key-protect.edge.bluemix.net/api/v2/secrets
```
{: codeblock}

고유 키를 추가하기 전에 서비스를 사용해 보려는 경우 [샘플 앱 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/IBM-Bluemix/key-protect-helloworld-python ){: new_window}을 확인하십시오.

1. [서비스에서 키 관련 작업을 수행할 수 있도록 {{site.data.keyword.Bluemix_notm}} 액세스 토큰, 조직 GUID 및 영역 GUID를 검색하십시오](#authentication_api).

2. 다음 cURL 명령을 사용하여
[{{site.data.keyword.keymanagementserviceshort}}API](https://console.ng.bluemix.net/apidocs/639)를 호출하십시오.

  ```cURL
  curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: bluemix_access_token' --header 'Bluemix-Space: space_GUID' --header 'Bluemix-Org: organization_GUID' -d '{
    "metadata": {
"collectionType": "application/vnd.ibm.kms.secret+json",
      "collectionTotal": 1
    },
    "resources": [
      {
      "type": "application/vnd.ibm.kms.secret+json",
      "name": "key_alias",
      "description": "key_description",
      "expirationDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
      "payload": "key_contents"
      }
    ]
  }' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets'
  ```
  {: codeblock}

  다음 표에 따라 예제 요청의 변수를 대체하십시오.

  <table>
    <tr>
      <th>변수</th>
      <th>설명</th>
    </tr>
    <tr>
      <td><em>bluemix_access_token</em></td>
      <td>인증 토큰입니다. Bearer 값을 포함하여 토큰의 전체 컨텐츠를 cURL 요청에 포함시키십시오. </td>
    </tr>
    <tr>
      <td><em>space_GUID</em></td>
      <td>{{site.data.keyword.Bluemix_notm}} 영역의 ID입니다. </td>
    </tr>
    <tr>
      <td><em>organization_GUID</em></td>
      <td>{{site.data.keyword.Bluemix_notm}} 조직의 ID입니다. </td>
    </tr>
    <tr>
      <td><em>key_alias</em></td>
      <td>키를 쉽게 식별할 수 있도록 해 주는 사용자가 읽을 수 있는 이름입니다. </td>
    </tr>
    <tr>
      <td><em>key_description</em></td>
      <td>키의 자세한 설명입니다. </td>
    </tr>
    <tr>
      <td><em>YYYY-MM-DD</em><br><em>HH:MM:SS.SS</em></td>
      <td>선택사항: 시스템에서 키가 만료되는 날짜 및 시간입니다(RFC3339 형식).
<code>expirationDate</code> 속성이 생략되면 키가 만료되지 않습니다. </td>
    </tr>
    <tr>
      <td><em>key_contents</em></td>
      <td>{{site.data.keyword.keymanagementserviceshort}}에 저장할 키 자료(예: RSA 키)입니다. 새 키를 생성하려면 페이로드 속성 및 key_contents 변수를 생략하십시오. </td>
    </tr>
      <caption style="caption-side:bottom;">표 1. {{site.data.keyword.keymanagementserviceshort}} API를 통해 키를 추가하는 데 필요한 변수 </caption>
  </table>

3. {{site.data.keyword.Bluemix_notm}} 영역에서
키를 가져오는 다음 호출을 실행하여 키가 작성되었는지 확인하십시오.

  ```cURL
  curl -X GET --header 'Accept: application/json' --header 'Authorization: bluemix_access_token' --header 'Bluemix-Space: space_GUID' --header 'Bluemix-Org: organization_GUID' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets'
  ```
  {: codeblock}

## {{site.data.keyword.keymanagementserviceshort}} API로 키 보기
{: #viewingkeys_api}

{{site.data.keyword.Bluemix_notm}} 영역 관리자 또는 개발자인 경우에는
{{site.data.keyword.keymanagementservicelong_notm}} API를 통해 키의 컨텐츠를 볼 수 있습니다.

상위 레벨 보기의 경우, {{site.data.keyword.keymanagementserviceshort}} UI를 통해 영역에서 관리되는 키를 찾아볼 수 있습니다.

다음 엔드포인트에 대한 GET 호출을 실행하여 키에 대한 자세한 정보를 보십시오.

```
https://ibm-key-protect.edge.bluemix.net/api/v2/secrets/key_ID
```
{: codeblock}

1. {{site.data.keyword.keymanagementserviceshort}} UI의 보안 서비스 아래에서 키에 대한 일반 특성을 볼 수 있습니다. 정렬 가능한 열 헤더를 클릭하여 키를 찾아볼 수 있습니다.
2. 키의 행에서 **ID**를 복사하십시오. ID 값을 사용하여 자체 키 자료와 같은 API의 키에 대한 보다 자세한 정보에 액세스할 수 있습니다.
3. [서비스에서 키로 작업할 수 있도록 {{site.data.keyword.Bluemix_notm}} 액세스 토큰, 조직 GUID 및 영역 GUID를 검색하십시오. ](#authentication_api)
4. 다음 cURL 명령을 실행하여 키와 키 자료에 대한 세부사항을 가져오십시오.

  ```cURL
  curl -X GET --header 'Accept: application/json' --header 'Authorization: bluemix_access_token' --header 'Bluemix-Space: space_GUID' --header 'Bluemix-Org: organization_GUID' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets/key_ID'
  ```
  {: codeblock}

  다음 표에 따라 예제 요청의 변수를 대체하십시오.

  <table>
    <tr>
      <th>변수</th>
      <th>설명</th>
    </tr>
    <tr>
      <td><em>bluemix_access_token</em></td>
      <td>인증 토큰입니다. Bearer 값을 포함하여 토큰의 전체 컨텐츠를 cURL 요청에 포함시키십시오. </td>
    </tr>
    <tr>
      <td><em>space_GUID</em></td>
      <td>{{site.data.keyword.Bluemix_notm}} 영역에 지정되는 랜덤으로 생성된 ID입니다. </td>
    </tr>
    <tr>
      <td><em>organization_GUID</em></td>
      <td>{{site.data.keyword.Bluemix_notm}} 조직에 지정되는 랜덤으로 생성된 ID입니다. </td>
    </tr>
    <tr>
      <td><em>key_ID</em></td>
      <td>[2](https://console.bluemix.net/docs/services/keymgmt/managing.html#viewingkeys_api__keyid)단계에서 가져온 키에 대한 ID입니다. </td>
    </tr>
    <caption style="caption-side:bottom;">표 2. {{site.data.keyword.keymanagementserviceshort}} API를 통해 키 보기에 필요한 변수에 대한 설명 </caption>
  </table>

  키 자료는 응답 엔티티 본문에서 리턴됩니다. HSM(Hardware Security Module)에 의해 생성된 키는 Base-64 인코딩입니다.

## 키 및 액세스 감사
{: #viewkeyassignments}

{{site.data.keyword.keymanagementservicelong_notm}}는 암호화 키를 확인, 관리, 감사할 수 있는 중앙 집중식 시스템을 제공합니다. 키와 키에 대한 액세스 제한사항을 감사하여 자원의 보안을 유지하십시오.

정기적으로 키 구성 감사:

- 키가 작성된 시점을 확인하고 키를 순환할 시점인지 판별합니다.
- [{{site.data.keyword.cloudaccesstrailshort}}로 {{site.data.keyword.keymanagementserviceshort}}에 대한 API 호출을 모니터합니다. ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.bluemix.net/docs/services/AccessTrail/at_integration.html#at_integration_key_protect ){: new_window}
- 어떤 사용자에게 키에 대한 액세스 권한이 있으며 해당 액세스 레벨이 적합한지 검사합니다.

액세스 권한이 있는 사용자를 감사하려면 다음을 수행하십시오.

1. 영역 관리자로 계정 설정으로 이동하여 **조직
관리**를 선택하십시오.
2. {{site.data.keyword.keymanagementserviceshort}}
서비스 인스턴스가 포함된 영역을 열어서 액세스 권한이 있는 사용자를 검사하십시오.
3. 사용자를 추가해야 하는 경우에는 **팀 구성원 초대**로 이동하고 사용자에게 부여하고자 하는
{{site.data.keyword.keymanagementserviceshort}} 권한에 해당되는
{{site.data.keyword.Bluemix_notm}} 역할을 선택하십시오.

  <table>
    <tr>
      <th>{{site.data.keyword.Bluemix_notm}} 역할</th>
      <th>{{site.data.keyword.keymanagementserviceshort}}
권한</th>
    </tr>
    <tr>
      <td>영역 관리자</td>
      <td>영역 관리자는 키를 작성, 보기 및 삭제할 수 있습니다.</td>
    </tr>
    <tr>
      <td>개발자 </td>
      <td>개발자는 키를 작성하고 키 세부사항을 볼 수 있습니다.</td>
    </tr>
    <tr>
      <td>감사자 </td>
      <td>감사자는 키의 상위 레벨 보기에 액세스할 수 있습니다. </td>
    </tr>
    <caption style="caption-side:bottom;">표 3. {{site.data.keyword.Bluemix_notm}} 역할을 {{site.data.keyword.keymanagementserviceshort}} 권한으로 맵핑. </caption>
  </table>
