---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-03-07"

subcollection: discovery

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:pre: .pre}
{:important: .important}
{:deprecated: .deprecated}
{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:hide-dashboard: .hide-dashboard}
{:apikey: data-credential-placeholder='apikey'} 
{:url: data-credential-placeholder='url'}
{:curl: #curl .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:go: .ph data-hd-programlang='go'}

# 데이터 소스에 연결
{: #sources}

{{site.data.keyword.discoveryshort}} 서비스를 통해 원격 소스에서 문서에 연결하여 크롤링할 수 있습니다.
{: shortdesc}

데이터 소스에 연결하고 해당 소스와 연관되도록 콜렉션을 구성하여 스케줄(원하는 경우)의 문서를 {{site.data.keyword.discoveryshort}} 서비스로 풀(pull)할 수 있습니다. {{site.data.keyword.discoveryshort}} 도구를 사용하는 경우 각 콜렉션은 하나의 데이터 소스로 구성될 수 있고, API를 사용하는 경우 다중 데이터 소스에서 단일 콜렉션으로 문서를 전송할 수 있습니다. {{site.data.keyword.discoveryshort}} 서비스는 크롤링이라는 프로세스를 사용하여 데이터 소스에서 문서를 풀(pull)합니다. 크롤링은 지정된 시작 위치에서 문서를 체계적으로 찾아보고 검색하는 프로세스입니다. 사용자가 명시적으로 지정한 항목만 {{site.data.keyword.discoveryshort}} 서비스에 의해 크롤링됩니다. 다음 유형의 데이터 소스를 크롤링할 수 있습니다.

-  [Box](/docs/services/discovery?topic=discovery-sources#connectbox)
-  [Salesforce](/docs/services/discovery?topic=discovery-sources#connectsf)
-  [Microsoft SharePoint Online](/docs/services/discovery?topic=discovery-sources#connectsp)
-  [Microsoft SharePoint 2016 온프레미스](/docs/services/discovery?topic=discovery-sources#connectsp_op)
-  [Web Crawl](/docs/services/discovery?topic=discovery-sources#connectwebcrawl)(베타)
-  [IBM Cloud Object Storage](/docs/services/discovery?topic=discovery-sources#connectcos)

{{site.data.keyword.discoveryshort}} 도구 또는 API를 사용하여 데이터 소스에 연결할 수 있습니다. {{site.data.keyword.discoveryshort}} 도구는 소스 시스템에 대한 이해가 덜 필요한 단순화된 연결 방법을 제공하고 API는 연결하는 소스에 대한 더 많은 이해를 필요로 하는 보다 세부적이고 구성 가능한 인터페이스를 제공합니다. 다음 프로세스 개요를 통해 이 문서에서 다음에 읽을 섹션을 알 수 있습니다.

1.  [일반 소스 요구사항](/docs/services/discovery?topic=discovery-sources#gen_req)을 읽고 무엇이 필요한지에 대한 일반적인 사항을 이해하십시오.
2.  소스 시스템에 특정한 요구사항을 읽으십시오.
    -  [Box](/docs/services/discovery?topic=discovery-sources#connectbox)
    -  [Salesforce](/docs/services/discovery?topic=discovery-sources#connectsf)
    -  [Microsoft SharePoint Online](/docs/services/discovery?topic=discovery-sources#connectsp)
    -  [Microsoft SharePoint 2016 온프레미스](/docs/services/discovery?topic=discovery-sources#connectsp_op)
    -  [Web Crawl](/docs/services/discovery?topic=discovery-sources#connectwebcrawl)(베타)
    -  [IBM Cloud Object Storage](/docs/services/discovery?topic=discovery-sources#connectcos)
3.  구성 선택사항에 따라 소스 구성 지시사항을 읽으십시오.
    -  [도구 사용](/docs/services/discovery?topic=discovery-sources#source_tooling)
    -  [API 사용](/docs/services/discovery?topic=discovery-sources#source_api)

온프레미스 데이터 소스를 선택한 경우 먼저 IBM Secure Gateway를 설치하고 구성해야 합니다. 자세한 정보는 [온프레미스 데이터를 위한 IBM Secure Gateway 설치](/docs/services/discovery?topic=discovery-sources#gateway)를 참조하십시오.

## 일반 소스 요구사항
{: #gen_req}

다음 일반 요구사항은 모든 데이터 소스에 해당됩니다.

-  Box, Salesforce, SharePoint Online, SharePoint 2016, IBM Cloud Object Storage 및 Web Crawl의 개별 문서 파일 크기는 10MB로 제한됩니다.
-  각 데이터 소스에 대한 인증 정보 및 파일 위치(또는 URL)가 필요합니다. 이는 일반적으로 데이터 소스의 개발자/시스템 관리자가 제공합니다.
-  크롤링할 데이터 소스의 리소스를 알아야 합니다. 이는 소스 관리자가 제공할 수 있습니다. Box 또는 Salesforce를 크롤링하는 경우 {{site.data.keyword.discoveryshort}} 도구를 사용하여 소스를 구성할 때 사용 가능한 리소스 목록이 표시됩니다.
-  {{site.data.keyword.discoveryshort}} 도구를 사용하는 경우 콜렉션은 단일 데이터 소스로 구성될 수 있습니다. API를 사용하는 경우 다중 데이터 소스의 문서는 단일 콜렉션으로 전송될 수 있습니다. 
-  데이터 소스를 크롤링할 때 데이터 소스의 리소스(API 호출)를 사용합니다. API 호출 수는 크롤링되어야 하는 문서 수에 따라 다릅니다. 데이터 소스에 대해 적절한 레벨의 서비스 라이센스(예: 엔터프라이즈)를 확보해야 하며 소스 시스템 관리자에게 자문을 받아야 합니다.
-  {{site.data.keyword.discoveryshort}} 소스 크롤링은 콜렉션에 저장되는 문서를 삭제하지 않습니다. 소스를 다시 크롤링하면 새 문서가 추가되고 업데이트된 문서가 현재 버전으로 수정되며 삭제된 문서는 마지막에 저장된 버전으로 남게 됩니다.
-  {{site.data.keyword.discoveryshort}}에서 다음 파일 유형을 수집할 수 있으며, 기타 모든 문서 유형은 무시됩니다.

콜렉션 | Lite 플랜 | 고급 플랜 
---------------- | ------------------------------ | ------------------------------------------- 
[SDU(Smart Document Understanding)](/docs/services/discovery?topic=discovery-release-notes#22jan19) 릴리스 전에 특히 {{site.data.keyword.discoveryfull}}에 대해 작성되는 기존 콜렉션 | Microsoft Word, PDF, HTML, JSON | Microsoft Word, PDF, HTML, JSON     
[SDU](/docs/services/discovery?topic=discovery-sdu#sdu) 릴리스 후에 작성되는 콜렉션 | PDF, Word, PowerPoint, Excel, JSON\*, HTML\* | PDF, Word, PowerPoint, Excel, PNG\*\*, TIFF\*\*, JPG\*\*, JSON\*, HTML\* 
    
\* JSON 및 HTML 문서는 {{site.data.keyword.discoveryfull}}에서 지원되지만 SDU 편집기를 사용하여 편집할 수 없습니다. HTML 및 JSON 문서의 구성을 변경하려면 API를 사용해야 합니다. 자세한 정보는 [API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/discovery/){: new_window}를 참조하십시오.

\*\* 개별 이미지 파일(PNG, TIFF, JPG)은 스캔되고 텍스트(해당 경우)가 추출됩니다. PDF, Word, PowerPoint 및 Excel 파일에 임베드된 PNG, TIFF 및 JPEG 이미지도 스캔되고 텍스트(해당 경우)가 추출됩니다. 

## Box
{: #connectbox}

{{site.data.keyword.discoveryfull}}에 연결하려면 새 Box 사용자 정의 애플리케이션을 작성해야 합니다. 작성하는 Box 애플리케이션에는 엔터프라이즈 레벨 또는 애플리케이션 레벨 액세스가 필요합니다. 

-  조직의 Box 관리자가 아닌 경우 [**애플리케이션 레벨** 액세스](/docs/services/discovery?topic=discovery-sources#applevelbox)가 권장됩니다. 애플리케이션을 승인할 관리자가 필요합니다. 
-  조직의 Box 관리자인 경우 [**엔터프라이즈 레벨** 액세스](/docs/services/discovery?topic=discovery-sources#entlevelbox)가 권장됩니다. 

Box 업데이트가 있는 경우 Box 액세스 설정 단계는 변경될 수 있습니다. 업데이트는 [Box 개발자 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.box.com/){: new_window}를 참조하십시오.
{: note}

### 애플리케이션 레벨 액세스 설정
{: #applevelbox}

1.   `https://app.box.com/developers/console`로 이동하고(회사의 Box URL 사용) **새 앱 작성**을 클릭하십시오.
1.   **새 앱 작성** 화면에서 **엔터프라이즈 통합**을 선택하고 **다음**을 클릭하십시오.
1.   **인증 방법** 화면에서 **OAuth 2.0 with JWT(서버 인증)**을 선택하고 **다음**을 클릭하십시오.
1.   앱의 이름을 지정하고 **앱 작성** 단추를 클릭하십시오. Box 앱이 작성되면 **앱 보기**를 클릭하십시오.
1.   앱을 보면서 **애플리케이션**으로 **애플리케이션 액세스**를 선택하십시오. 계속하는 중에 기존 관리 사용자를 사용할 수 있으며, 새 사용자를 작성할 필요가 없습니다.
1.   페이지의 **애플리케이션 범위** 섹션까지 아래로 스크롤하여 다음 선택란을 사용으로 설정하십시오.  
     - `Read and write all folders stored in Box`
     - `Manage Users`
1.   **고급 기능** 섹션까지 아래로 스크롤하여 다음 전환을 사용으로 설정하십시오.
     - `Perform Actions as Users`
     - `Generate User Access Tokens` 
1.  **변경사항 저장** 단추를 클릭하십시오. 

이후 일부 단계에는 조직의 Box 계정 관리자의 지원이 필요합니다. 조직의 Box 관리자가 아닌 경우 Box 개발자의 콘솔을 열고 **계정 설정** > **계정 세부사항** > **설정** 아래의 내용을 확인하여 관리자를 식별할 수 있습니다.

1.  [관리자 단계] **새 앱 권한 부여** 단추를 클릭하여 `https://app.box.com/master/settings/openbox`에서 애플리케이션 클라이언트 ID에 권한을 부여하십시오.
1.  [관리자 단계] `https://app.box.com/developers/console`의 **API 키** 필드에 **클라이언트 ID**를 입력한 후 **권한 부여** 단추를 클릭하십시오.
1.  [관리자 단계] 애플리케이션용 개발자 토큰을 검색하십시오. 이를 수행하려면 `https://app.box.com/developers/console`로 이동하고 **개발자 토큰** 섹션으로 스크롤하여 토큰을 생성하십시오.
1.  이제 관리자가 애플리케이션에 권한을 부여함에 따라 `https://developer.box.com/reference#page-create-an-enterprise-user`로 이동하고 API 참조 페이지를 사용하여 앱 사용자를 작성하십시오.

   앱 사용자를 작성하기 위한 curl 예:

   ```bash
    curl https://api.box.com/2.0/users -H "Authorization: Bearer ACCESS_TOKEN" -d '{"name": "NedStark", "is_platform_access_only": true}' -X POST
   ```
   {: pre}

1.  새로 작성된 **id** 필드 컨텐츠를 복사하여 Box 애플리케이션을 {{site.data.keyword.discoveryfull}}에 연결하는 비관리자에게 이를 제공하십시오. 
1.  앱 사용자가 작성되면 크롤링하려는 폴더는 앱 사용자와 공유되어야 하고 앱 사용자에게는 이 폴더의 `Viewer` 권한이 제공되어야 합니다. 여기에는 위의 curl 명령 응답으로부터 받은 앱 사용자 로그인 이름이 필요합니다. 예를 들면, `"login":"AppUser_737729_jmUo@boxdevedition.com"`입니다.
1.  Box 개발자 콘솔 `https://app.box.com/developers/console`로 돌아가서 **공개 키 추가 및 관리** 섹션까지 아래로 스크롤하십시오. **공개/개인 키 쌍 생성**을 클릭하고 키 쌍 파일을 다운로드하십시오. 파일을 여십시오.
1.  키 쌍 파일에서 다음 필드를 잘라내어 {{site.data.keyword.discoveryshort}} 도구에 붙여넣으십시오.
    -  `client_id`
    -  `enterprise_id`
    -  `client_secret` 
    -  `public_key_id` 
    -  `private_key` 
    -  `passphrase` 

### 엔터프라이즈 레벨 액세스 설정
{: #entlevelbox}

1.  `https://app.box.com/developers/console`로 이동하고(회사의 Box URL 사용) **새 앱 작성**을 클릭하십시오.
1.  **새 앱 작성** 화면에서 **엔터프라이즈 통합**을 선택하고 **다음**을 클릭하십시오.
1.  **인증 방법** 화면에서 **OAuth 2.0 with JWT(서버 인증)**을 선택하고 **다음**을 클릭하십시오.
1.  앱의 이름을 지정하고 **앱 작성** 단추를 클릭하십시오. Box 앱이 작성되면 **앱 보기**를 클릭하십시오.
1.  앱을 보면서 **엔터프라이즈**로 **애플리케이션 액세스**를 선택하십시오. 계속하는 중에 기존 관리 사용자를 사용할 수 있으며, 새 사용자를 작성할 필요가 없습니다.
1.  페이지의 **애플리케이션 범위** 섹션까지 아래로 스크롤하여 다음 선택란을 사용으로 설정하십시오.  
    - `Read and write all folders stored in Box`
    - `Manage Users`
    - `Manage Enterprise Properties`
1.  **고급 기능** 섹션까지 아래로 스크롤하여 다음 전환을 사용으로 설정하십시오.
    - `Perform Actions as Users`
    - `Generate User Access Tokens` 
1.  **변경사항 저장** 단추를 클릭하십시오. 

`새로 고치기`는 엔터프라이즈 레벨 액세스에서만 지원됩니다.
{: note}

Box 앱 설정을 변경하면 앱을 `Reauthorize`하여 변경사항이 적용됩니다.
{: tip}

이후 일부 단계에는 조직의 Box 계정 관리자의 지원이 필요합니다. 조직의 Box 관리자가 아닌 경우 Box 개발자의 콘솔을 열고 **계정 설정** > **계정 세부사항** > **설정** 아래의 내용을 확인하여 관리자를 식별할 수 있습니다.

1.  [관리자 단계] **관리 콘솔** > **엔터프라이즈 설정** > **앱**으로 이동하고 `Custom applications`으로 스크롤하여 애플리케이션 클라이언트 ID에 권한을 부여하십시오. URL의 예는 `https://app.box.com/master/settings/openbox`입니다.
1.  [관리자 단계] `https://app.box.com/developers/console`의 **API 키** 필드에 **클라이언트 ID**를 입력한 후 **권한 부여** 단추를 클릭하십시오.
1.  Box 개발자 콘솔 `https://app.box.com/developers/console`로 돌아가서 **공개 키 추가 및 관리** 섹션까지 아래로 스크롤하십시오. **공개/개인 키 쌍 생성**을 클릭하고 키 쌍 파일을 다운로드하십시오. 파일을 여십시오.
1.  키 쌍 파일에서 다음 필드를 잘라내어 {{site.data.keyword.discoveryshort}} 도구에 붙여넣으십시오.
    -  `client_id`
    -  `enterprise_id`
    -  `client_secret` 
    -  `public_key_id` 
    -  `private_key` 
    -  `passphrase` 

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
-  `site_collection_path` - 해당 인증 정보가 연결되는 소스의 `site_collection_path`입니다.
-  `username` - 해당 인증 정보가 연결되는 소스의 `client_id`입니다. 이 사용자는 크롤링하고 인덱싱되어야 할 모든 사이트 및 목록에 대한 액세스 권한이 있어야 합니다.
-  `password` - 해당 인증 정보가 연결되는 소스의 `password`입니다. 이 값은 리턴되지 않으며 인증 정보를 작성하거나 수정할 때만 사용됩니다.

인증 정보를 식별할 때 [Microsoft SharePoint 개발자 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.microsoft.com/en-us/sharepoint/dev/){: new_window}를 참조하는 것이 유용합니다.

다음은 Microsoft SharePoint Online을 크롤링할 때 고려할 기타 항목입니다.

-  SharePoint를 크롤링하려면 `Crawl User` 계정에는 `SiteCollection Administrator` 권한이 있어야 합니다.
-  SharePoint를 크롤링하는 경우 크롤링할 SharePoint 사이트 콜렉션 경로 목록이 필요합니다. {{site.data.keyword.discoveryshort}}는 입력으로 폴더 경로를 지원하지 않습니다. 

## Web Crawl
{: #connectwebcrawl}

이 베타 기능은 비밀번호가 필요하지 않은 공개 웹 사이트를 크롤링하는 데 사용될 수 있습니다. {{site.data.keyword.discoveryshort}}가 웹 사이트, 언어 및 홉 수와 동기화하는 주기를 선택할 수 있습니다. 

-  `Sync my data` - 매 5분, 매시간, 매일, 매주 또는 매월 동기화하도록 선택할 수 있습니다. 
-  `Select language` -지원되는 언어 목록에서 웹 사이트의 언어를 선택하십시오. {{site.data.keyword.discoveryshort}}에서 지원되는 언어 목록은 [언어 지원](/docs/services/discovery?topic=discovery-language-support#supported-languages)을 참조하십시오. 각 언어마다 별도의 콜렉션을 작성하는 것이 좋습니다.
-  `URL group to sync` - URL을 입력하고 더하기 부호를 클릭하여 이 URL을 URL 그룹에 추가하십시오. 이 URL 그룹에 적합한 **크롤링 설정**을 지정하려면 ![Cog](images/icon_settings.png) 아이콘을 클릭하십시오. 시작 URL에서 표시되는 연속 링크의 수인 **최대 홉**을 선택할 수 있습니다(시작 URL은 `0`임). 기본 홉 수는 `2`이고 최대값은 `20`입니다(API를 사용하는 경우 최대값은 `1000`임). 

이 베타 릴리스의 경우 웹 페이지 수가 제한됩니다. 이에 따라 웹 크롤러는 지정된 모든 웹 사이트를 크롤링하여 최대 홉 수에 도달하지 않을 수 있습니다.
{: note}

다른 URL에 다른 **크롤링 설정**이 필요한 경우 **URL 그룹 추가**를 클릭하고 새 그룹을 작성하십시오. 필요한 만큼 URL 그룹을 작성할 수 있습니다.
{: tip}

## SharePoint 2016 온프레미스
{: #connectsp_op}

Microsoft SharePoint 2016(SharePoint Server 2016이라고도 함)은 온프레미스 데이터 소스입니다. 여기에 연결하려면 먼저 IBM Secure Gateway를 설치하고 구성해야 합니다. 자세한 정보는 [온프레미스 데이터를 위한 IBM Secure Gateway 설치](/docs/services/discovery?topic=discovery-sources#gateway)를 참조하십시오.
{: note}

SharePoint 2016 데이터 소스에 연결하려면 다음 인증 정보가 필요합니다. 이 인증 정보는 SharePoint 관리자로부터 얻어야 합니다.

-  `username` - 해당 인증 정보가 연결되는 소스의 `client_id`입니다. 이 사용자는 크롤링하고 인덱싱되어야 할 모든 사이트 및 목록에 대한 액세스 권한이 있어야 합니다.
-  `password` - 해당 인증 정보가 연결되는 소스의 `password`입니다. 이 값은 리턴되지 않으며 인증 정보를 작성하거나 수정할 때만 사용됩니다.
-  `web_application_url` - SharePoint 2016 `web_application_url`입니다(예: https://sharepointwebapp.com:8443). 포트가 제공되지 않으면 기본값은 포트 `80`(http용) 및 포트 `443`(https용)입니다. 
-  `domain` - SharePoint 2016 계정의 `domain`입니다.

인증 정보를 식별할 때 [Microsoft SharePoint 개발자 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.microsoft.com/en-us/sharepoint/dev/){: new_window}를 참조하는 것이 유용합니다.

다음은 Microsoft SharePoint 2016을 크롤링할 때 고려할 기타 항목입니다.

-  SharePoint 2016을 크롤링하려면 `Crawl User` 계정에는 `SiteCollection Administrator` 권한이 있어야 합니다.
-  SharePoint를 크롤링하는 경우 크롤링할 SharePoint 사이트 콜렉션 경로 목록이 필요합니다. {{site.data.keyword.discoveryshort}}는 입력으로 폴더 경로를 지원하지 않습니다. 

## IBM Cloud Object Storage
{: #connectcos}

IBM Cloud Object Storage 소스에 연결하는 경우 다음 인증 정보가 필요합니다. 인증 정보는 IBM Cloud Object Storage 관리자가 제공해야 합니다.

-  `endpoint` - IBM Cloud Object Storage 데이터와 상호 작용하는 데 사용되는 `endpoint`입니다.
-  `access_key_id` - IBM Cloud Object Storage 인스턴스가 작성될 때 얻은 `access_key_id`입니다.
-  `secret_access_key` - IBM Cloud Object storage 인스턴스가 작성될 때 얻은 요청에 서명하는 `secret_access_key`입니다.

이 정보를 입력한 후 데이터와 동기화할 주기를 선택하고 동기화할 버킷을 선택할 수 있습니다. 

다음은 IBM Cloud Object Storage를 크롤링할 때 고려할 기타 항목입니다.

-  이 커넥터는 개인용 엔드포인트의 크롤링을 지원하지 않습니다. 
-  모든 버킷이 선택되면 약간의 성능 문제가 발생합니다. 해당 경우 문서가 인덱싱을 완료하기 전에 지연이 발생할 수 있습니다. 

## 도구 사용
{: #source_tooling}

{{site.data.keyword.discoveryshort}} 도구를 사용하여 데이터 소스에 연결하는 작업은 특히 소스에 대한 콜렉션을 작성할 때 수행됩니다. 다음 단계를 수행하여 소스 콜렉션을 작성하고 이를 크롤링하십시오.

1.  {{site.data.keyword.discoveryshort}} 도구의 **데이터 관리** 페이지에서 **데이터 소스 연결**을 선택하십시오.
2.  연결할 데이터 소스를 선택하십시오. 온프레미스 데이터 소스를 선택한 경우 먼저 IBM Secure Gateway를 설치해야 합니다. 자세한 정보는 [온프레미스 데이터를 위한 IBM Secure Gateway 설치](/docs/services/discovery?topic=discovery-sources#gateway)를 참조하십시오. 
3.  소스 인증 정보를 입력하고 연결을 클릭하십시오. 소스 시스템 관리자로부터 소스 인증 정보를 얻을 수 있습니다.
4.  크롤링할 데이터와 이를 동기화할 빈도를 선택하십시오. 동기화 옵션은 다음과 같습니다. 
    -  매 5분: 5분마다 실행됩니다.
    -  매시: 매시간 실행됩니다.
    -  매일: 지정된 시간대의 매일 00:00 - 06:00 사이에 실행됩니다.
    -  매주: 지정된 시간대의 일요일 00:00 - 06:00 사이에 실행됩니다.
    -  매월: 지정된 시간대의 매달 첫 번째 일요일 00:00 - 06:00 사이에 실행됩니다.
    
    크롤링 상태 예:
    
    ```json
    "crawl_status" : {
    "source_crawl" : {
      "status" : "completed",
      "next_crawl" : "2019-02-10T05:00:00-05:00"
    }
    ```
5.  **오브젝트 저장 & 동기화**를 클릭하여 데이터 소스 크롤링을 시작하십시오. 그런 다음 문서가 콜렉션에 추가될 때 업데이트되는 콜렉션 상태 화면으로 경로 재지정됩니다.

크롤링하면 처음에 데이터를 동기화하고 이후에 지정된 빈도로 데이터를 동기화합니다.
**참고:** **동기화 설정** 화면에서 어떤 항목을 수정한 다음 **오브젝트 저장 및 동기화**를 클릭하면 크롤링이 시작됩니다(또는 이미 실행 중인 경우 다시 시작됨).

## API 사용
{: #source_api}

API를 사용하여 데이터 소스에 연결되는 콜렉션을 작성하려면 다음 프로세스를 사용하십시오.

온프레미스 데이터 소스에 연결할 계획인 경우 먼저 IBM Secure Gateway를 설치해야 합니다. 자세한 정보는 [온프레미스 데이터를 위한 IBM Secure Gateway 설치](/docs/services/discovery?topic=discovery-sources#gateway)를 참조하십시오. 

다음 예제에서는 SharePoint 데이터 소스를 사용합니다.

1.  [소스 인증 정보 API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/discovery#create-credentials){: new_window}를 사용하여 연결하려는 소스에 대한 인증 정보를 작성하십시오. 새로 작성된 인증 정보에 대해 리턴된 **credential_id**를 기록해 두십시오.
2.  [구성 API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/discovery#add-configuration){: new_window}를 사용하여 새 구성을 작성하십시오. 이 구성에는 크롤링되어야 하는 항목을 정의하는 **source** 오브젝트가 포함되어야 합니다. **source** 오브젝트에는 이전에 기록해 둔 **credential_id**가 포함되어야 합니다.
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
3.  [콜렉션 API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/discovery#create-a-collection){: new_window}를 사용하여 새 콜렉션을 작성하십시오. 콜렉션을 정의하는 오브젝트에는 이전에 기록해 둔 **configuration_id**가 포함되어야 합니다.

소스 크롤링은 콜렉션이 작성되는 즉시 시작되고 이후 지정된 빈도로 다시 수행됩니다.
**참고:** 구성의 **source** 오브젝트에서 어떤 항목을 수정하면 새 크롤링이 시작됩니다(또는 이미 실행 중인 경우 다시 시작됨).

### `customer_id` 지정
{: #source_customer_id}

수집된 {{site.data.keyword.discoveryshort}} 문서의 `customer_id` 필드는 API의 **user-data** 메소드에서 `customer_id`를 사용하여 컨텐츠를 삭제하는 데 사용될 수 있습니다. 데이터 소스에서 수신되는 문서에는 수집 시 자동으로 `customer_id`가 지정되지 않습니다. 애플리케이션에서 `customer_id`를 정의해야 하는 경우 소스 시스템에서 복사하거나 `customer_id`로 사용할 하나 이상의 수신 필드를 지정할 수 있습니다. 이를 수행하려면 소스에 연결하는 데 사용되는 구성을 수정해야 합니다.

1.  샘플 조회를 수행하고 `customer_id`로 사용할 필드를 식별하십시오.
2.  구성을 수정하십시오. `customer_id` 필드를 작성하려면 **정규화** 섹션을 추가해야 합니다.
    -  도구에서 콜렉션을 탐색하여 구성 섹션에서 **편집** 링크를 클릭하십시오. **정규화** 탭을 클릭하고 **복사** 정규화에 추가하여 `customer_id` 필드를 작성하십시오. 그런 다음 **적용 & 저장**을 클릭하십시오.
    ![복사 정규화](images/norm_copy.png)
    -  API를 사용하는 경우 다음 오브젝트를 **정규화** 배열에 추가하십시오.
       ```json
       {
         "operation" : "copy",
         "source_field" : "{original_field_name}",
         "destination_field" : "customer_id"
       }
       ```
       {: codeblock}
3.  다음 스케줄된 크롤링은 `customer_id` 필드를 모든 문서에 추가합니다. 크롤링을 즉시 시작하려면 소스 구성을 수정하십시오(도구에서 **동기화 설정** 사용).

`customer_id`를 사용하여 삭제하는 작업에 대한 자세한 정보는 [정보 보안](/docs/services/discovery?topic=discovery-information-security#information-security)을 참조하십시오.

## 온프레미스 데이터를 위한 IBM Secure Gateway 설치 
{: #gateway}

온프레미스 데이터 소스에 연결하려면 먼저 IBM Secure Gateway를 다운로드하고, 설치하고, 구성해야 합니다. 첫 번째 온프레미스 데이터 소스를 위한 IBM Secure Gateway를 설치한 후에는 이 프로세스를 반복할 필요가 없습니다.

1.  {{site.data.keyword.discoveryshort}} 도구의 **데이터 관리** 페이지에서 **데이터 소스 연결**을 선택하십시오.
1.  연결할 데이터 소스를 선택하십시오. 온프레미스 데이터 소스를 선택하는 경우 **온프레미스 네트워크에 연결** 섹션으로 이동한 후 **연결** 단추를 클릭하십시오.
1.  **Secure Gateway Client 다운로드 및 설치** 화면에서 적합한 IBM Secure Gateway 버전을 다운로드하십시오.
1.  다운로드를 완료한 후 **Secure Gateway를 다운로드하고 계속 진행** 단추를 클릭하십시오. 설치 중에 Secure Gateway Client에서 프롬프트될 때 화면에 제공되는 **게이트웨이 ID** 및 **토큰**이 필요합니다. 설치 지시사항은 Secure Gateway 문서에 있는 [클라이언트 설치 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com/docs/services/SecureGateway/securegateway_install.html#installing-the-client){: new_window}를 참조하십시오. 
1.  Secure Gateway Client가 실행되는 머신에서 http://localhost:9003을 통해 Secure Gateway 대시보드를 여십시오.
1.  대시보드에서 **ACL 추가**를 클릭하십시오. 각 SharePoint 콜렉션의 엔드포인트 URL을 **액세스 허용** 목록에 추가하십시오. 예를 들면, 호스트 이름: `mycompany.sharepoint.com`과 포트: `80`입니다.
1.  {{site.data.keyword.discoveryshort}} 도구로 돌아가서 **계속**을 클릭하십시오. 연결되면 `Connection successful` 메시지가 표시됩니다. 연결되지 않은 경우 Secure Gateway 대시보드를 열고 **액세스 허용** 목록의 엔드포인트가 올바른지 확인하십시오.

연결되면 온프레미스 데이터 소스의 인증 정보 입력을 시작할 수 있습니다. 

## 데이터 소스 연결 및 데이터 격리
{: #source_isolation}

[외부 데이터 소스에 연결](/docs/services/discovery?topic=discovery-sources#sources)하면 서비스 인스턴스의 데이터 격리가 줄어듭니다. 소스와 서비스 간의 전환 중에 데이터를 격리할 수 없기 때문입니다. 기타 모든 격리(휴지, 관리, 조회)가 전부 유지됩니다. 서비스와 데이터 소스 간 및 서비스와 데이터 소스 내 모든 인플라이트 통신은 TLS v1.2를 사용하여 암호화됩니다. TLS 인증서의 개인 키는 AES-256-GCM을 사용하여 휴지 중에 암호화되고, 서비스 인증서는 3년마다 만료되고, 인증서 폐기 목록은 매월 업데이트됩니다. 모든 인증서는 TLS v1.2를 사용하여 암호화된 연결을 통해 전송되고 AES-256을 사용하여 휴지 중에 암호화됩니다. 해당 데이터 소스에 대한 연결은 해당 데이터 소스에서 지원되는 모든 보안 프로토콜을 사용합니다. 
