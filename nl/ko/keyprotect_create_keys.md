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

# 키 작성

{{site.data.keyword.keymanagementservicefull}}를 사용하여 키의 라이프사이클을 관리할 수 있습니다.
{: shortdesc}

가장 좋은 방법은 코드를 개발하면서 키를 안전하게 관리하는 것입니다. 예를 들어, 기타 보안 코딩 사례와 함께 다음 가이드라인에 대해 고려하십시오. 

- 키를 코드에 임베드할 때 보안 영향성을 고려하십시오. 
- 앱과 리소스에 대한 프로그래밍 액세스를 위해서만 키를 작성하십시오. 보다 단순한 [사용자 권한 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.bluemix.net/docs/admin/patterns.html#userroles){: new_window} 부여가 가능하면 키를 작성하지 마십시오. 
- 키를 순환하고 사용하지 않는 키를 제거하십시오. 
- 민감한 운영에는 다단계 인증을 사용하십시오. 
- 각 앱의 키를 분리시켜 앱을 격리시키십시오.
- 매우 민감한 정보를 전송할 때는 프로그램 방식 API를 사용한 작업을 고려하십시오. 

자체 키를 추가하기 전에 서비스를 사용해 보려면 [샘플 앱 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}을 확인하십시오. 

## GUI로 키 작성
{: #gui}

{{site.data.keyword.keymanagementserviceshort}} GUI로 서비스에 키를 추가하려면 [{{site.data.keyword.keymanagementserviceshort}} 시작하기](/docs/services/keymgmt/index.html#addkey)를 참조하십시오. 

## API로 키 작성
{: #api}

{{site.data.keyword.keymanagementserviceshort}} API를 사용하여 프로그램 방식으로 기존 키를 보호하거나 새 키를 생성할 수 있습니다. 

다음 엔드포인트에 대한 `POST` 호출을 작성하여 키를 작성하거나 기존 키를 가져오십시오. 

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys
```
{: codeblock}

1. [서비스의 키 관련 작업을 수행하기 위한 인증 토큰, 조직 GUID 및 영역 GUID를 검색하십시오.](/docs/services/keymgmt/keyprotect_authentication.html)

2. 다음 cURL 명령을 사용하여 [{{site.data.keyword.keymanagementserviceshort}}API](https://console.ng.bluemix.net/apidocs/639)를 호출하십시오. 

    ```cURL
    curl -X POST \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
      -H 'authorization: Bearer <OAuth_token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
      -H 'content-type: application/vnd.ibm.kms.key+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
     "metadata": {
"collectionType": "application/vnd.ibm.kms.key+json",
       "collectionTotal": 1
     },
    "resources": [
      {
      "type": "application/vnd.ibm.kms.key+json",
       "name": "<key_alias>",
       "description": "<key_description>",
       "expirationDate": "<YYYY-MM-DDTHH:MM:SS.SSZ>",
       "payload": "<key_material>"
       }
     ]
    }'
    ```
    {: codeblock}

    다음 표에 따라 예제 요청의 변수를 대체하십시오.
    <table>
      <tr>
        <th>변수</th>
        <th>설명</th>
      </tr>
      <tr>
        <td><em>OAuth_token</em></td>
        <td>인증 토큰입니다. Bearer 값을 포함하여 토큰의 전체 컨텐츠를 cURL 요청에 포함시키십시오. </td>
      </tr>
      <tr>
        <td><em>organization_GUID</em></td>
        <td>{{site.data.keyword.Bluemix_notm}} 조직에 지정된 고유 ID입니다. </td>
      </tr>
      <tr>
        <td><em>space_GUID</em></td>
        <td>{{site.data.keyword.Bluemix_notm}} 영역에 지정된 고유 ID입니다. </td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>트랜잭션을 추적하고 상관시키는 데 사용되는 고유 ID입니다. </td>
      </tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p><code>POST</code> 및 <code>DELETE</code> 오퍼레이션에 대한 서버 작동을 변경하는 헤더입니다. </p><p><code>return=minimal</code>로 설정된 경우, 서비스는 응답 엔티티-본문에서 키 이름 및 <code>id</code> 값 등의 키 메타데이터만 리턴합니다. <code>return=representation</code>로 설정된 경우, 서비스는 키 자료와 키 메타데이터를 모두 리턴합니다. </p></td>
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
        <td>선택사항: 시스템에서 키가 만료되는 날짜 및 시간입니다(RFC 3339 형식). <code>expirationDate</code> 속성이 생략되면 키가 만료되지 않습니다. </td>
      </tr>
      <tr>
        <td><em>key_material</em></td>
        <td>{{site.data.keyword.keymanagementserviceshort}}에 저장할 키 자료(예: RSA 키)입니다. 새 키를 생성하려면 <code>payload</code> 속성과 <em>key_material</em> 변수를 생략하십시오. </td>
      </tr>
      <caption style="caption-side:bottom;">표 1. {{site.data.keyword.keymanagementserviceshort}} API를 통해 키를 추가하는 데 필요한 변수 </caption>
    </table>

    성공한 응답은 기타 메타데이터와 함께 키에 대한 `id` 값을 리턴합니다. `id`는 키에 지정되었으며 후속 호출에 사용되는 고유 ID입니다. 

3. **선택사항:** {{site.data.keyword.Bluemix_notm}} 영역에서 키를 가져오기 위한 다음 호출을 실행하여 키가 작성되었는지 확인하십시오. 

    ```cURL
    curl -X GET \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <OAuth-token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
    ```
    {: codeblock}

### 다음에 수행할 작업

이제 키를 사용하여 앱과 서비스를 코딩할 수 있습니다. 

- 각 REST 요청과 응답에 대한 전체 세부사항은 {{site.data.keyword.keymanagementserviceshort}} [REST API 참조 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/apidocs/639){: new_window}를 참조하십시오. 
