---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# 데이터 소스에 연결
{: #sources}

{{site.data.keyword.discoveryshort}} 서비스를 통해 원격 소스에서 문서에 연결하여 크롤링할 수 있습니다.
{: shortdesc}

데이터 소스에 연결하고 해당 소스와 연관되도록 콜렉션을 구성하여 스케줄(원하는 경우)의 문서를 {{site.data.keyword.discoveryshort}} 서비스로 풀(pull)할 수 있습니다. 각 콜렉션은 하나의 데이터 소스를 사용하여 구성될 수 있습니다. {{site.data.keyword.discoveryshort}} 서비스는 크롤링이라는 프로세스를 사용하여 데이터 소스에서 문서를 풀(pull)합니다. 크롤링은 지정된 시작 위치에서 문서를 체계적으로 찾아보고 검색하는 프로세스입니다. 사용자가 명시적으로 지정한 항목만 {{site.data.keyword.discoveryshort}} 서비스에 의해 크롤링됩니다. 다음 유형의 데이터 소스를 크롤링할 수 있습니다.

-  [Box](/docs/services/discovery/connect.html#connectbox)
-  [Salesforce](/docs/services/discovery/connect.html#connectsf)
-  [Microsoft SharePoint Online](/docs/services/discovery/connect.html#connectsp)

{{site.data.keyword.discoveryshort}} 도구 또는 API를 사용하여 데이터 소스에 연결할 수 있습니다. {{site.data.keyword.discoveryshort}} 도구는 소스 시스템에 대한 이해가 덜 필요한 단순화된 연결 방법을 제공하고 API는 연결하는 소스에 대한 더 많은 이해를 필요로 하는 보다 세부적이고 구성 가능한 인터페이스를 제공합니다. 다음 프로세스 개요를 통해 이 문서에서 다음에 읽을 섹션을 알 수 있습니다.

1.  [일반 소스 요구사항](/docs/services/discovery/connect.html#gen_req)을 읽고 무엇이 필요한지에 대한 일반적인 사항을 이해하십시오.
2.  소스 시스템에 특정한 요구사항을 읽으십시오.
    -  [Box](/docs/services/discovery/connect.html#connectbox)
    -  [Salesforce](/docs/services/discovery/connect.html#connectsf)
    -  [Microsoft SharePoint Online](/docs/services/discovery/connect.html#connectsp)
3.  구성 선택사항에 따라 소스 구성 지시사항을 읽으십시오.
    -  [도구 사용](/docs/services/discovery/connect.html#source_tooling)
    -  [API 사용](/docs/services/discovery/connect.html#source_api)

## 일반 소스 요구사항
{: #gen_req}

다음 일반 요구사항은 모든 데이터 소스에 해당됩니다.

-  Box, Salesforce 및 SharePoint Online의 개별 문서 파일 크기 한계는 10MB입니다.
-  각 데이터 소스에 대한 인증 정보 및 파일 위치(또는 URL)가 필요합니다. 이는 일반적으로 데이터 소스의 개발자/시스템 관리자가 제공합니다.
-  크롤링할 데이터 소스의 리소스를 알아야 합니다. 이는 소스 관리자가 제공할 수 있습니다. Box 또는 Salesforce를 크롤링하는 경우 {{site.data.keyword.discoveryshort}} 도구를 사용하여 소스를 구성할 때 사용 가능한 리소스 목록이 표시됩니다.
-  데이터 소스를 크롤링할 때 데이터 소스의 리소스(API 호출)를 사용합니다. 호출 수는 크롤링하는 문서 수에 따라 다릅니다. 데이터 소스에 대해 적절한 레벨의 서비스(예: 엔터프라이즈)를 확보해야 하며 소스 시스템 관리자에게 자문을 받아야 합니다.
-  {{site.data.keyword.discoveryshort}}에서 다음 파일 유형을 수집할 수 있으며, 기타 모든 유형의 문서는 무시됩니다.
   -  Microsoft Word
   -  PDF
   -  HTML
   -  JSON
-  {{site.data.keyword.discoveryshort}} 소스 크롤링은 콜렉션에 저장되는 문서를 삭제하지 않습니다. 소스를 다시 크롤링하면 새 문서가 추가되고 업데이트된 문서가 현재 버전으로 수정되며 삭제된 문서는 마지막에 저장된 버전으로 남게 됩니다.

## Box
{: #connectbox}

Box 소스에 연결할 때 연결하려는 인스턴스가 엔터프라이즈 플랜 이상인지 확인하십시오.

다음과 같이 {{site.data.keyword.discoveryshort}}에 대한 작업을 수행하도록 Box 계정을 설정합니다.

1.  다음 사이트에서 새 Box 사용자 정의 애플리케이션을 작성하십시오. `https://app.box.com/developers/console`(회사 Box URL 사용)
1.  다음 중 하나를 수행하십시오.
    - **애플리케이션 액세스**에 `Enterprise`를 선택한 다음 기존 관리 사용자를 사용하여 계속하십시오.
      또는
    - **애플리케이션 액세스**에 `Application`을 선택한 다음 [Box API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.box.com/reference#create-app-user){: new_window}를 사용하여 새로 작성된 애플리케이션으로 `Application User`를 작성하십시오.
1.  다음 **애플리케이션 범위**를 사용으로 설정하십시오.
    - `Read and Write All Folders Stored In Box`
    - `Manage Users`
1.  다음 **고급 기능**을 사용으로 설정하십시오.
    - `Perform Actions as Users`
    - `Generate User Access Tokens`
1.  `https://app.box.com/developers/console`의 `Client ID`를 `API Key` 필드에 입력하여 관리자가 애플리케이션 클라이언트 ID를 승인하도록 하십시오. `https://app.box.com/master/settings/openbox`
1.  `public/private keypair`를 생성하십시오(컴퓨터에 다운로드됨).
1.  다운로드한 파일을 열고 해당 필드를 {{site.data.keyword.discoveryshort}}에 복사/붙여넣으십시오. {{site.data.keyword.discoveryshort}}에 복사할 때 `privateKey`의 끝에 있는 후미 줄 바꾸기 `\n`을 제거하십시오.

**참고:** {{site.data.keyword.discoveryshort}}는 사용자 정의 애플리케이션 크롤링 자체를 지원하지 않습니다(사용자 자신을 위장할 수 없음). 

Box 소스에 연결하려면 다음 인증 정보가 필요합니다. 이 인증 정보는 Box 관리자로부터 얻어야 합니다(이전 단계에서 Box 사용자 정의 애플리케이션을 설정하여 확보하지 않은 경우).

-  `client_id` - 해당 인증 정보가 연결되는 소스의 `client_id`입니다.    
-  `enterprise_id` - 해당 인증 정보가 연결되는 Box 사이트의 `enterprise_id`입니다.
-  `client_secret` - 해당 인증 정보가 연결되는 소스의 `client_secret`입니다. 이 값은 리턴되지 않으며 인증 정보를 작성하거나 수정할 때만 사용됩니다.
-  `public_key_id` - 해당 인증 정보가 연결되는 소스의 `public_key_id`입니다. 이 값은 리턴되지 않으며 인증 정보를 작성하거나 수정할 때만 사용됩니다.
-  `private_key` - 해당 인증 정보가 연결되는 소스의 `private_key`입니다. 이 값은 리턴되지 않으며 인증 정보를 작성하거나 수정할 때만 사용됩니다.
-  `passphrase` - 해당 인증 정보가 연결되는 소스의 `passphrase`입니다. 이 값은 리턴되지 않으며 인증 정보를 작성하거나 수정할 때만 사용됩니다.

인증 정보를 식별할 때 [Box 개발자 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.box.com/){: new_window}를 참조하는 것이 유용합니다.

다음은 Box를 크롤링할 때 고려할 기타 항목입니다.

-  Box 노트는 JSON 형식으로 저장되므로 지정된 폴더에 있는 모든 Box 노트는 {{site.data.keyword.discoveryshort}}에 의해 수집됩니다.
-  API를 사용하는 경우 크롤링할 각 폴더에 대한 폴더 ID및 연관된 소유자 ID 목록이 있어야 합니다. {{site.data.keyword.discoveryshort}} 도구를 사용하여 크롤링할 컨텐츠를 찾아보고 선택할 수 있습니다.

## Salesforce
{: #connectsf}

Salesforce 소스에 연결할 때 연결하려는 인스턴스가 엔터프라이즈 플랜 이상인지 확인하십시오.

Salesforce 소스에 연결하려면 다음 인증 정보가 필요합니다. 이 인증 정보는 Salesforce 관리자로부터 얻어야 합니다.
-  `url` - 해당 인증 정보가 연결되는 소스의 `url`입니다.
-  `username` - 해당 인증 정보가 연결되는 소스의 `username`입니다.
-  `password` - `password`는 Salesforce 비밀번호 및 유효한 Salesforce 보안 토큰이 연결된 상태로 구성됩니다. 이 값은 리턴되지 않으며 인증 정보를 작성하거나 수정할 때만 사용됩니다.

인증 정보를 식별할 때 [Salesforce 개발자 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.salesforce.com/docs/){: new_window}를 참조하는 것이 유용합니다.

다음은 Salesforce를 크롤링할 때 고려할 기타 항목입니다.

-  Knowledge Articles는 해당 **버전**이 `published` 상태이고 언어가 `en-us`인 경우에만 크롤링됩니다.
-  API를 사용하는 경우 크롤링할 Salesforce 오브젝트 목록이 있어야 합니다. {{site.data.keyword.discoveryshort}} 도구를 사용하여 크롤링할 컨텐츠를 찾아보고 선택할 수 있습니다.


## SharePoint Online
{: #connectsp}

Microsoft SharePoint Online 소스에 연결할 때 연결하려는 인스턴스가 엔터프라이즈(E1) 플랜 이상인지 확인하십시오.

SharePoint Online 소스에 연결하려면 다음 인증 정보가 필요합니다. 이 인증 정보는 SharePoint 관리자로부터 얻어야 합니다.

-  `organization_url` - 해당 인증 정보가 연결되는 소스의 `organization_url`입니다.
-  `site_collection.path` - 해당 인증 정보가 연결되는 소스의 `site_collection.path`입니다.
-  `username` - 해당 인증 정보가 연결되는 소스의 `client_id`입니다.
-  `password` - 해당 인증 정보가 연결되는 소스의 `password`입니다. 이 값은 리턴되지 않으며 인증 정보를 작성하거나 수정할 때만 사용됩니다.

인증 정보를 식별할 때 [Microsoft SharePoint 개발자 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.microsoft.com/en-us/sharepoint/dev/){: new_window}를 참조하는 것이 유용합니다.

다음은 Microsoft SharePoint Online을 크롤링할 때 고려할 기타 항목입니다.

-  SharePoint를 사용하는 경우 크롤링할 SharePoint 사이트 콜렉션 경로 목록이 있어야 합니다. {{site.data.keyword.discoveryshort}} 도구를 사용하여 크롤링할 컨텐츠를 찾아보고 선택할 수 있습니다. 전체 SharePoint Online 사이트를 크롤링하려는 경우 이 필드에 여러 경로(URL)를 선택하지 마십시오. 이 시나리오에서는 `site_collection.path` 필드에 `/`를 입력하십시오.

## 도구 사용
{: #source_tooling}

{{site.data.keyword.discoveryshort}} 도구를 사용하여 데이터 소스에 연결하는 작업은 특히 소스에 대한 콜렉션을 작성할 때 수행됩니다. 다음 단계를 수행하여 소스 콜렉션을 작성하고 이를 크롤링하십시오.

1.  {{site.data.keyword.discoveryshort}} 도구의 **데이터 관리** 페이지에서 **데이터 소스 연결**을 선택하십시오.
2.  연결할 데이터 소스를 선택하십시오.
3.  소스 인증 정보를 입력하고 연결을 클릭하십시오. 소스 시스템 관리자로부터 소스 인증 정보를 얻을 수 있습니다.
4.  크롤링할 데이터와 이를 동기화할 빈도를 선택하십시오.
5.  **오브젝트 저장 & 동기화**를 클릭하여 데이터 소스 크롤링을 시작하십시오. 그런 다음 문서가 콜렉션에 추가될 때 업데이트되는 콜렉션 상태 화면으로 경로 재지정됩니다.

크롤링하면 처음에 데이터를 동기화하고 이후에 지정된 빈도로 데이터를 동기화합니다.
**참고:** **동기화 설정** 화면에서 어떤 항목을 수정한 다음 **오브젝트 저장 및 동기화**를 클릭하면 크롤링이 시작됩니다(또는 이미 실행 중인 경우 다시 시작됨).

## API 사용
{: #source_api}

API를 사용하여 데이터 소스에 연결되는 콜렉션을 작성하려면 다음 프로세스를 사용하십시오.
1.  [소스 인증 정보 API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#credentials-api){: new_window}를 사용하여 연결하려는 소스에 대한 인증 정보를 작성하십시오. 새로 작성된 인증 정보에 대해 리턴된 **credential_id**를 기록해 두십시오.
2.  [구성 API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#configurations-api){: new_window}를 사용하여 새 구성을 작성하십시오. 이 구성에는 크롤링되어야 하는 항목을 정의하는 **source** 오브젝트가 포함되어야 합니다. **source** 오브젝트에는 이전에 기록해 둔 **credential_id**가 포함되어야 합니다.
    ```json
    "source" : {
      "type" : "salesforce",
      "credential_id" : "{credential_id}",
      "schedule" : {
        "enabled" : true,
        "time_zone" : "America/New_York",
        "frequency" : "weekly"
      },
      "options" : {
         "site_collections" : [ {
         "site_collection_path" : "/sites/TestSiteA",
         "limit" : 10
         } ]
      }
    }
    ```
    {: codeblock}
    새로 작성된 구성에 대해 리턴된 **configuration_id**를 기록해 두십시오.
3.  [콜렉션 API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#configurations-api){: new_window}를 사용하여 새 콜렉션을 작성하십시오. 콜렉션을 정의하는 오브젝트에는 이전에 기록해 둔 **configuration_id**가 포함되어야 합니다.

소스 크롤링은 콜렉션이 작성되는 즉시 시작되고 이후 지정된 빈도로 다시 수행됩니다.
**참고:** 구성의 **source** 오브젝트에서 어떤 항목을 수정하면 새 크롤링이 시작됩니다(또는 이미 실행 중인 경우 다시 시작됨).

## `customer_id` 지정
{:# source_customer_id}

수집된 {{site.data.keyword.discoveryshort}} 문서의 `customer_id` 필드는 API의 **user-data** 메소드에서 `customer_id`를 사용하여 컨텐츠를 삭제하는 데 사용될 수 있습니다. 데이터 소스에서 수신되는 문서에는 수집 시 자동으로 `customer_id`가 지정되지 않습니다. 애플리케이션에서 `customer_id`를 정의해야 하는 경우 소스 시스템에서 복사하거나 `customer_id`로 사용할 하나 이상의 수신 필드를 지정할 수 있습니다. 이를 수행하려면 소스에 연결하는 데 사용되는 구성을 수정해야 합니다.

1.  샘플 조회를 수행하고 `customer_id`로 사용할 필드를 식별하십시오.
2.  구성을 수정하십시오. `customer_id` 필드를 작성하려면 **정규화** 섹션을 추가해야 합니다.
    -  도구에서 콜렉션을 탐색하여 구성 섹션에서 **편집** 링크를 클릭하십시오. **정규화** 탭을 클릭하고 **복사** 정규화에 추가하여 `customer_id` 필드를 작성하십시오. 그런 다음 **적용 & 저장**을 클릭하십시오.
    ![복사 정규화](images/norm_copy.png)
    -  API를 사용하는 경우 다음 오브젝트를 **정규화** 배열"에 추가하십시오.
       ```json
       {
         "operation" : "copy",
         "source_field" : "{original_field_name}",
         "destination_field" : "customer_id"
       }
       ```
       {: codeblock}
3.  다음 스케줄된 크롤링은 `customer_id` 필드를 모든 문서에 추가합니다. 크롤링을 즉시 시작하려면 소스 구성을 수정하십시오(도구에서 **동기화 설정** 사용).

`customer_id`를 사용하여 삭제하는 작업에 대한 자세한 정보는 [정보 보안 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.bluemix.net/docs/services/discovery/information-security.html){: new_window}을 참조하십시오.
