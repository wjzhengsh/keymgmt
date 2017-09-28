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

# {{site.data.keyword.keymanagementserviceshort}} 서비스 프로비저닝
{: #provision}

{{site.data.keyword.Bluemix_notm}} 콘솔이나 {{site.data.keyword.Bluemix_notm}} CLI를 사용하여 {{site.data.keyword.keymanagementservicefull}}의 보안 인스턴스를 작성할 수 있습니다.
{: shortdesc}

## {{site.data.keyword.Bluemix_notm}} 콘솔에서 프로비저닝
{: #gui}

{{site.data.keyword.Bluemix_notm}} 콘솔에서 {{site.data.keyword.keymanagementserviceshort}}의 인스턴스를 프로비저닝하려면 다음 단계를 완료하십시오. 

1. [{{site.data.keyword.Bluemix_notm}} 계정 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.bluemix.net/){: new_window}에 로그인하십시오. 
2. **카탈로그**를 클릭하여 {{site.data.keyword.Bluemix_notm}}에서 사용 가능한 서비스의 목록을 보십시오. 
3. **서비스** 카테고리를 선택하고 **{{site.data.keyword.keymanagementserviceshort}}** 제목을 클릭하십시오. 
5. 서비스 플랜을 선택하고 **작성**을 클릭하여 자신이 로그인된 {{site.data.keyword.Bluemix_notm}} 조직과 영역에서 {{site.data.keyword.keymanagementserviceshort}} 서비스 인스턴스를 프로비저닝하십시오. 

## {{site.data.keyword.Bluemix_notm}} CLI에서 프로비저닝
{: #cli}

{{site.data.keyword.Bluemix_notm}} CLI를 사용하여 {{site.data.keyword.keymanagementserviceshort}}의 인스턴스를 프로비저닝할 수 있습니다. 다음 단계를 완료할 수 있도록 [시스템에 명령행 도구를 다운로드하고 설치](https://clis.ng.bluemix.net/ui/home.html){: new_window}하십시오. 

1. {{site.data.keyword.Bluemix_notm}} CLI에 로그인하십시오. 

    ```sh
    bx login [--sso]
    ```
    {: codeblock}
    **참고**: `--sso` 매개변수는 연합 ID로 로그인할 때 필요합니다. 이 옵션을 사용하는 경우에는 CLI 출력에 나열된 링크로 이동하여 일회성 패스코드를 생성하십시오.
2. {{site.data.keyword.keymanagementserviceshort}} 서비스 인스턴스가 작성될 {{site.data.keyword.Bluemix_notm}} 조직 및 영역을 선택하십시오. 

    다음 명령을 사용하여 대상 조직 및 영역을 설정할 수도 있습니다. 

    ```sh
    bx target [-o organization_name] [-s space_name]
    ```
    {: codeblock}

3. 해당 지역, 조직 및 영역 내에서 {{site.data.keyword.keymanagementserviceshort}}의 인스턴스를 프로비저닝하십시오. 

    ```sh
    bx service create ibm_key_management TieredPricing [instance_name]
    ```
    {: codeblock}

    _instance_name_을 서비스 인스턴스의 고유 별명으로 대체하십시오. 

4. 서비스 인스턴스 작성이 완료되었는지 확인하십시오. 

    ```sh
    bx service list
    ```
    {: codeblock}


### 다음에 수행할 작업

이제 키를 사용하여 앱과 서비스를 코딩할 수 있습니다. 

- 데이터를 암호화하고 복호화하기 위한 {{site.data.keyword.keymanagementserviceshort}}의 키 저장소의 작동 방법에 대한 예를 보려면 [GitHub에서 샘플 앱을 확인 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}하십시오. 
- 프로그래밍 방식의 키 관리에 대한 자세한 정보를 찾으려면 [{{site.data.keyword.keymanagementserviceshort}} API 참조 문서에서 코드 샘플 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/apidocs/639){: new_window}을 확인하십시오. 
