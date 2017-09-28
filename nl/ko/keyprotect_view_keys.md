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

# 키 보기

{{site.data.keyword.keymanagementservicefull}}로 암호화 키의 컨텐츠를 볼 수 있습니다.
{: shortdesc}

## GUI로 키 보기
{: #gui}

{{site.data.keyword.keymanagementserviceshort}} GUI로 서비스의 키를 찾아보려면 [{{site.data.keyword.keymanagementserviceshort}} 시작하기](/docs/services/keymgmt/index.html#managekey)를 참조하십시오. 

## API로 키 보기
{: #api}

{{site.data.keyword.keymanagementserviceshort}} API를 사용하여 키의 컨텐츠를 검색할 수 있습니다. 

### 1단계: 키의 콜렉션 검색
{: #retrieve_keys_api}

상위 레벨 보기의 경우에는 다음 엔드포인트에 대한 `GET` 호출을 작성하여 영역에서 관리되는 키를 찾아볼 수 있습니다. 

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys
```
{: codeblock}

1. [서비스의 키 관련 작업을 위한 인증 토큰, 조직 GUID 및 영역 GUID를 검색](/docs/services/keymgmt/keyprotect_authentication.html)하십시오. 
2. 다음 cURL 명령을 실행하여 키에 대한 일반 특성을 보십시오. 

    ```cURL
    curl -X GET \
    https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <OAuth_token>' \
    -H 'bluemix-org: <organization_GUID>' \
    -H 'bluemix-space: <space_GUID>' \
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
        <td><em>space_GUID</em></td>
        <td>{{site.data.keyword.Bluemix_notm}} 영역에 지정된 고유 ID입니다. </td>
      </tr>
      <tr>
        <td><em>organization_GUID</em></td>
        <td>{{site.data.keyword.Bluemix_notm}} 조직에 지정된 고유 ID입니다. </td>
      </tr>
      <caption style="caption-side:bottom;">표 1. {{site.data.keyword.keymanagementserviceshort}} API를 통해 키를 보는 데 필요한 변수를 설명합니다. </caption>
    </table>

    성공한 요청은 {{site.data.keyword.Bluemix_notm}} 영역에서 사용 가능한 키의 콜렉션을 리턴합니다. 

    ```
    {
      "metadata": {
"collectionType": "application/vnd.ibm.kms.key+json",
        "collectionTotal": 2
      },
    "resources": [
      {
      "id": "Key ID 1",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Key alias",
          "description": "Key description",
          "state": 1,
          "algorithmType": "AES",
          "createdBy": "v4 UUID of the user who creates the key",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "Key length",
            "mode": "GCM"
          }
        },
        {
          "id": "Key ID 2",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Key alias",
          "description": "Key description",
          "state": 1,
          "algorithmType": "AES",
          "createdBy": "v4 UUID of the user who creates the key",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "Key length",
            "mode": "GCM"
          }
        }
      ]
    }
    ```
    {:screen}

### 2단계: ID별로 키 검색
{: #retrieve_key_api}

특정 키에 대한 자세한 정보를 보기 위해 다음 엔드포인트에 대한 후속 `GET` 호출을 작성할 수 있습니다. 

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID>
```
{: codeblock}

1. [서비스의 키 관련 작업을 위한 인증 토큰, 조직 GUID 및 영역 GUID를 검색](/docs/services/keymgmt/keyprotect_authentication.html)하십시오. 
2. 액세스하거나 관리할 키의 ID를 검색하십시오. 

    ID 값을 사용하여 키 자료와 같은 키에 대한 자세한 정보에 액세스할 수 있습니다. `GET v2/keys` 요청을 작성하거나 {{site.data.keyword.keymanagementserviceshort}} GUI에 액세스하여 지정된 키에 대한 ID를 검색할 수 있습니다. 

3. 다음 cURL 명령을 실행하여 키와 키 자료에 대한 세부사항을 가져오십시오. 

    ```cURL
    curl -X GET \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID> \
      -H 'accept: application/vnd.ibm.kms.secret+json' \
      -H 'authorization: Bearer <OAuth_token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
      -H 'correlation-id: <correlation_ID>' \
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
        <td>선택사항: 트랜잭션을 추적하고 상관시키는 데 사용되는 고유 ID입니다. </td>
      </tr>
      <tr>
        <td><em>key_ID</em></td>
        <td>[1단계](#retrieve_keys_api)에서 검색한 키에 대한 ID입니다. </td>
      </tr>
      <caption style="caption-side:bottom;">표 2. {{site.data.keyword.keymanagementserviceshort}} API를 통해 지정된 키를 보는 데 필요한 변수에 대해 설명합니다. </caption>
    </table>

    성공한 응답은 키와 키 자료에 대한 세부사항을 리턴합니다. 다음 JSON 오브젝트는 예제 리턴값을 표시합니다. 

    ```
    {
        "metadata": {
        "collectionTotal": 1,
            "collectionType": "application/vnd.ibm.kms.key+json"
        },
    "resources": [
      {
      "createdBy": "...",
                "creationDate": "...",
                "id": "...",
                "name": "...",
                "payload": "...",
                "state": 1,
                "type": "application/vnd.ibm.kms.key+json"
            }
        ]
    }
    ```
    {:screen}

    사용 가능한 매개변수에 대한 자세한 설명은 {{site.data.keyword.keymanagementserviceshort}} [REST API 참조 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/apidocs/639){: new_window}를 참조하십시오. 
