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

# 키 삭제

{{site.data.keyword.cloud_notm}} 영역 또는 {{site.data.keyword.keymanagementserviceshort}} 서비스 인스턴스의 관리자인 경우에는 {{site.data.keyword.keymanagementservicefull}}를 사용하여 암호화 키와 해당 컨텐츠를 삭제할 수 있습니다.
{: shortdesc}

**중요사항**: 키를 삭제하면 해당 컨텐츠과 연관 데이터가 영구 삭제됩니다. 이 조치는 되돌릴 수 없습니다. 프로덕션 환경의 경우에는 리소스 영구 삭제가 권장되지 않지만, 테스트나 QA 등의 임시 환경의 경우에는 유용할 수 있습니다.

## GUI로 키 삭제
{: #gui}

그래픽 인터페이스를 사용한 키 리소스 삭제를 원하는 경우에는 {{site.data.keyword.keymanagementserviceshort}} GUI를 사용할 수 있습니다.

[키를 새로 작성하거나 기존 키를 서비스로 가져온 후](/docs/services/keymgmt/keyprotect_create_keys.html) 다음 단계를 완료하여 키를 삭제하십시오.

1. [{{site.data.keyword.cloud_notm}} 콘솔 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.bluemix.net/)에 로그인하십시오. 
2. {{site.data.keyword.cloud_notm}} 대시보드에서 {{site.data.keyword.keymanagementserviceshort}}의 프로비저닝된 인스턴스를 선택하십시오.
3. **관리** 분할창으로 이동하여 서비스의 키를 찾아보십시오.
4. 수직 생략 기호 아이콘을 클릭하여 삭제할 키에 대한 옵션의 목록을 여십시오. 
5. 옵션 메뉴에서 **키 삭제**를 클릭한 후 다음 화면에서 키 삭제를 확인하십시오.

## API로 키 삭제
{: #api}

키와 해당 컨텐츠를 삭제하려면 다음 엔드포인트에 대해 `DELETE` 호출을 작성하십시오.

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID>
```

1. [서비스의 키 관련 작업을 위한 인증 토큰, 조직 GUID 및 영역 GUID를 검색](/docs/services/keymgmt/keyprotect_authentication.html)하십시오.

2. 삭제할 키의 ID를 검색하십시오.

    `GET /v2/keys` 요청을 작성하거나 {{site.data.keyword.keymanagementserviceshort}} 대시보드에서 키를 확인하여 지정된 키의 ID를 검색할 수 있습니다.

3. 다음 cURL 명령을 실행하여 키와 해당 컨텐츠를 영구 삭제하십시오.

    ```cURL
    curl -X DELETE \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID> \
      -H 'authorization: Bearer <OAuth_token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
      -H 'prefer: <return_preference>'
    ```
    다음 표에 따라 예제 요청의 변수를 대체하십시오.
    <table>
      <tr>
        <th>변수</th>
        <th>설명</th>
      </tr>
      <tr>
        <td><em>OAuth_token</em></td>
        <td>인증 토큰입니다. Bearer 값을 포함하여 토큰의 전체 컨텐츠를 cURL 요청에 포함시키십시오.</td>
      </tr>
      <tr>
        <td><em>space_GUID</em></td>
        <td>{{site.data.keyword.cloud_notm}} 영역에 지정된 고유 ID입니다.</td>
      </tr>
      <tr>
        <td><em>organization_GUID</em></td>
        <td>{{site.data.keyword.cloud_notm}} 조직에 지정된 고유 ID입니다.</td>
      </tr>
      <tr>
        <td><em>key_ID</em></td>
        <td>삭제할 키의 고유 ID입니다.</td>
      </tr>
      <tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p><code>POST</code> 및 <code>DELETE</code> 오퍼레이션에 대한 서버 작동을 변경하는 헤더입니다.</p><p><code>return=minimal</code>로 설정된 경우, 서비스는 응답 엔티티-본문에서 키 이름 및 <code>id</code> 값 등의 키 메타데이터만 리턴합니다. <code>return=representation</code>로 설정된 경우, 서비스는 키 자료와 키 메타데이터를 모두 리턴합니다.</p></td>
      </tr>
      <caption style="caption-side:bottom;">표 1. {{site.data.keyword.keymanagementserviceshort}} API를 통해 키를 삭제하는 데 필요한 변수를 설명합니다.</caption>
    </table>

    `DELETE` 요청의 세부사항은 응답 엔티티-본문에서 리턴됩니다.
