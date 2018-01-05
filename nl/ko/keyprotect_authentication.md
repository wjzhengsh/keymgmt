---

copyright:
  years: 2017
lastupdated: "2017-12-15"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# API에 액세스
{: #access-api}

{{site.data.keyword.keymanagementservicefull}}는 키를 저장, 검색, 생성하기 위해 어떠한 프로그래밍 언어와도 함께 사용할 수 있는 REST API를 제공합니다.
{: shortdesc}

API 관련 작업을 수행하려면 서비스 및 인증 신임 정보를 생성해야 합니다. 

## 액세스 토큰 검색
{: #retrieve_token}

{{site.data.keyword.iamshort}}에서 액세스 토큰을 검색하여 {{site.data.keyword.keymanagementserviceshort}}에 인증할 수 있습니다. [서비스 ID](/docs/iam/serviceid.html)를 사용하면 개인 사용자 신임 정보를 공유하지 않고도 {{site.data.keyword.cloud_notm}}에서 또는 그 외부에서 서비스나 애플리케이션 대신 {{site.data.keyword.keymanagementserviceshort}} API에 대한 작업을 수행할 수 있습니다.  

사용자 신임 정보로 인증하려는 경우 [{{site.data.keyword.cloud_notm}} (bx) CLI![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](/docs/cloud-platform/cli/reference/bluemix_cli/get_started.html#getting-started){: new_window}에서 `bx iam oauth-tokens`를 실행하여 토큰을 검색할 수 있습니다.
{: tip}

다음 단계를 완료하여 액세스 토큰을 검색하십시오.

1. {{site.data.keyword.cloud_notm}} 콘솔에서 **관리** &gt; **보안** &gt; **ID 및 액세스** &gt; **서비스 ID**로 이동하십시오. 프로세스에 따라 [서비스 ID를 작성](/docs/iam/serviceid.html#creating-a-service-id){: new_window}하십시오.
2. **조치** 메뉴를 사용하여 [새 서비스 ID의 액세스 정책을 정의](/docs/iam/serviceidaccess.html#assigning-new-access){: new_window}하십시오. 
    
    {{site.data.keyword.keymanagementserviceshort}} 리소스의 액세스 관리에 대한 자세한 정보는 [역할 및 권한](/docs/services/keymgmt/keyprotect_manage_access.md#roles)을 참조하십시오.
3. **API 키** 섹션을 사용하여 [서비스 ID와 연관시킬 API 키를 작성](/docs/iam/serviceid_keys.html#creating-an-api-key-for-a-service-id){: new_window}하십시오. 보안 위치로 API 키를 다운로드하여 저장하십시오.
4. {{site.data.keyword.iamshort}} API를 호출하여 액세스 토큰을 검색하십시오.

    ```cURL
    curl -X POST \
      "https://iam.bluemix.net/oidc/token" \
      -H "Content-Type: application/x-www-form-urlencoded" \
      -H "Accept: application/json" \
      -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<your_API_key>" \ 
    ```
    {: codeblock}

    요청에서 `<API_key>`를 3단계에서 작성한 API로 바꾸십시오. 다음 잘린 예는 토큰 출력을 표시합니다.

    ```
    {
    "access_token": "eyJraWQiOiIyM...",
    "expiration": 1512161390,
    "expires_in": 3600,
    "refresh_token": "J1AzOrtC8yHVlcT...",
    "token_type": "Bearer"
    }
    ```
    {: screen}

    전체 `access_token` 값(_Bearer_ 토큰 유형이 접두부임)을 사용하여 {{site.data.keyword.keymanagementserviceshort}} API로 서비스의 키를 프로그래밍 방식으로 관리하십시오. 

## 인스턴스 ID 검색
{: #retrieve_instance_ID}

[{{site.data.keyword.cloud_notm}} (bx) CLI![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](/docs/cloud-platform/cli/reference/bluemix_cli/get_started.html#getting-started){: new_window}를 사용하여 {{site.data.keyword.keymanagementserviceshort}} 서비스 인스턴스에 대한 식별 정보를 검색할 수 있습니다. 계정에서 {{site.data.keyword.keymanagementserviceshort}}의 지정된 인스턴스 내 암호화 키를 관리하려면 인스턴스 ID를 사용하십시오. 

1. {{site.data.keyword.cloud_notm}} (bx) CLI를 사용하여 {{site.data.keyword.cloud_notm}}에 로그인하십시오.

    ```sh
    bx login 
    ```
    {: pre}

    **참고:** 로그인에 실패하면 `bx login --sso` 명령을 실행하여 다시 시도하십시오. `--sso` 매개변수는 연합 ID로 로그인할 때 필요합니다. 이 옵션을 사용하는 경우에는 CLI 출력에 나열된 링크로 이동하여 일회성 패스코드를 생성하십시오.

2. {{site.data.keyword.keymanagementserviceshort}}의 프로비저닝된 인스턴스가 포함된 계정을 선택하십시오.

    `bx resource service-instances`를 실행하여 계정에 프로비저닝된 모든 서비스 인스턴스를 나열할 수 있습니다.

3. {{site.data.keyword.keymanagementserviceshort}} 서비스 인스턴스를 고유하게 식별하는 클라우드 리소스 이름(CRN)을 검색하십시오. 

    ```sh
    bx resource service-instance <instance_name> --id
    ```
    {: pre}

    `<instance_name>`을 {{site.data.keyword.keymanagementserviceshort}}의 인스턴스에 지정한 고유 별명으로 바꾸십시오. 다음 잘린 예는 Bluemix CLI 출력을 표시합니다. _7e8fc048-5606-4259-ad71-92397b0fa3f7_ 값은 인스턴스 ID 예입니다.

    ```
    crn:v1:bluemix:public:kms:us-south:a/7e8fc048-5606-4259-ad71-92397b0fa3f7
    ```
    {: screen}

## API 요청 구성
{: #form_api_request}

서비스에 대한 API 호출을 작성할 때 처음에 {{site.data.keyword.keymanagementserviceshort}}의 인스턴스를 프로비저닝한 방법에 따라 API 요청을 구조화하십시오. 

요청을 빌드하려면 [지역 서비스 엔드포인트](/docs/services/keymgmt/keyprotect_regions.html)를 해당 인증 신임 정보와 쌍으로 묶으십시오. 예를 들어, `us-south` 지역의 서비스 인스턴스를 작성한 경우 다음 엔드포인트 및 API 헤더를 사용하여 서비스에서 키를 찾아보십시오.

```cURL
curl -X GET \
    https://keyprotect.us-south.bluemix.net/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <access_token>' \
    -H 'bluemix-instance: <instance_ID>' \
```
{: codeblock}

### 다음에 수행할 작업

- 프로그래밍 방식의 키 관리에 대한 자세한 정보를 찾으려면 [{{site.data.keyword.keymanagementserviceshort}} API 참조 문서에서 코드 샘플 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/apidocs/639){: new_window}을 확인하십시오.
- 데이터를 암호화하고 복호화하기 위해 {{site.data.keyword.keymanagementserviceshort}}에 저장된 키가 작동하는 방식에 대한 예를 보려면 [GitHub에서 샘플 앱 확인![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}을 수행하십시오.
