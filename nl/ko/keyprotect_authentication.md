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

# 인증 신임 정보 생성
{: #authentication}

{{site.data.keyword.keymanagementservicefull}}는 키를 저장, 검색, 생성하기 위해 어떠한 프로그래밍 언어와도 함께 사용할 수 있는 REST API를 제공합니다.
{: shortdesc}

API 관련 작업을 수행하려면 서비스 및 인증 신임 정보를 생성해야 합니다. 

## 조직 및 영역 GUID 검색
{: #retrieve_GUIDs}

[{{site.data.keyword.Bluemix_notm}} CLI ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.bluemix.net/docs/cli/reference/bluemix_cli/index.html#getting-started)로 {{site.data.keyword.Bluemix_notm}} 조직 및 영역에 대한 식별 정보를 검색할 수 있습니다. 

1. {{site.data.keyword.Bluemix_notm}} CLI를 통해 {{site.data.keyword.Bluemix_notm}}에 로그인하십시오. 

    ```
    bx login [--sso]
    ```
    {: codeblock}

    `--sso` 매개변수는 연합 ID로 로그인할 때 필요합니다. 이 옵션을 사용하는 경우에는 CLI 출력에 나열된 링크로 이동하여 일회성 패스코드를 생성하십시오. 

2. {{site.data.keyword.keymanagementserviceshort}}
서비스 인스턴스를 포함하는 {{site.data.keyword.Bluemix_notm}} 조직
및 영역을 선택하십시오.

    CLI 출력의 조직과 영역의 이름을 기록해 두십시오. 또한 `bx target`을 실행하여 이 정보를 볼 수 있습니다. 

3. {{site.data.keyword.Bluemix_notm}} 조직 및 영역 GUID를
검색하십시오.

    ```
    bx iam org [organization_name] --guid
    bx iam space [space_name] --guid
    ```
    {: codeblock}
    _organization_name_ 및 _space_name_을 조직 및 영역에 지정된 고유 별명으로 대체하십시오.
## 인증 토큰 검색
{: #retrieve_token}

인증 토큰을 이용하면 {{site.data.keyword.keymanagementserviceshort}} API를 사용하여 키를 프로그래밍 방식으로 관리할 수 있습니다. 

**참고**: {{site.data.keyword.Bluemix_notm}} Identity and Access Management에서 관리하는 세부 단위의 액세스 제어를 사용하려면 서비스에 대한 호출을 작성할 때 IAM 토큰을 사용하십시오. 

1. {{site.data.keyword.Bluemix_notm}} CLI에서 {{site.data.keyword.keymanagementserviceshort}} 서비스가 포함된 조직 및 영역을 선택하십시오. 

2. 인증 토큰을 검색하고 표시하십시오. 

    ```
    bx iam oauth-tokens
    ```
    {: codeblock}

    일부가 표시된 다음 예제에서는 {{site.data.keyword.Bluemix_notm}} 토큰 출력을 보여줍니다. _Bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7_ 변수는 예제 액세스 토큰입니다. 

    ```
    IAM token: Bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7...
    UAA token: Bearer mjEyJhbGciOiJIUzI1Ni.chWyW1faWQiOiJJQkWs1...
    ```
    {: screen}

    `IAM` 또는 `UAA` Bearer 값을 이용하면 {{site.data.keyword.keymanagementserviceshort}} API를 사용하여 서비스의 키를 프로그래밍 방식으로 관리할 수 있습니다. 

### 다음에 수행할 작업

영역에서 키 관리를 시작하려면 [{{site.data.keyword.keymanagementserviceshort}}REST API 참조 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/apidocs/639){: new_window}를 참조하십시오. 
