---

copyright:
  years: 2015, 2017, 2019
lastupdated: "2019-02-08"

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

# Data Crawler로 컨텐츠 추가
{: #adding-content-with-data-crawler}

Data Crawler를 사용하면 {{site.data.keyword.discoveryshort}} 서비스에 대한 컨텐츠의 업로드를 자동화할 수 있습니다.
{: shortdesc}

Data Crawler는 파일 공유 또는 데이터베이스를 크롤링하기 위해서만 사용되어야 합니다. 기타 모든 경우에는 적합한 {{site.data.keyword.discoveryshort}} 커넥터를 사용해야 합니다. 자세한 사항은 [데이터 소스에 연결](/docs/services/discovery?topic=discovery-sources#sources)을 참조하십시오. {{site.data.keyword.discoveryshort}} 커넥터에서 지원되는 데이터 소스를 사용하여 Data Crawler를 사용하는 경우 Data Crawler에 대한 지원이 더 이상 제공되지 않습니다.
{: important}

## Data Crawler로 데이터 크롤링
{: #dc-crawling}

Data Crawler는 문서가 상주하는 저장소(예: 파일 공유, 데이터베이스)에서 문서를 사용하고 {{site.data.keyword.discoveryshort}} 서비스로 사용될 클라우드에 문서를 푸시하는 데 도움을 주는 명령행 도구 입니다. 

Data Crawler는 파일 공유 또는 데이터베이스를 크롤링하기 위해서만 사용되어야 합니다. 기타 모든 경우에는 Box, SharePoint, Salesforce, IBM Cloud Object Storage 또는 Web Crawl에 적합한 {{site.data.keyword.discoveryshort}} 커넥터를 사용해야 합니다. 자세한 사항은 [데이터 소스에 연결](/docs/services/discovery?topic=discovery-sources#sources)을 참조하십시오. {{site.data.keyword.discoveryshort}} 커넥터에서 지원되는 데이터 소스를 사용하여 Data Crawler를 사용하는 경우 Data Crawler에 대한 지원이 더 이상 제공되지 않습니다.
{: important}

## Data Crawler를 사용하는 경우
{: #dc-use}

원격 시스템에서 수많은 파일의 관리 업로드를 수행하려고 하거나 지원되는 저장소(예: DB2 데이터베이스)에서 컨텐츠를 추출하려는 경우 Data Crawler를 사용해야 합니다.

Data Crawler는 로컬 드라이브에서 파일을 업로드하기 위한 솔루션으로 개발된 것은 아닙니다. 도구를 사용하거나 직접적인 API 호출을 사용하여 로컬 드라이브에서 파일을 업로드해야 합니다. 수많은 파일을 {{site.data.keyword.discoveryshort}}에 업로드할 수 있는 다른 옵션은 GitHub의 [discovery-files ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/IBM/discovery-files){: new_window}입니다.
{: note}

## Data Crawler 사용
{: #dc-using}

1. [{{site.data.keyword.discoveryshort}} 서비스 구성](/docs/services/discovery?topic=discovery-configservice#configservice)
1. 크롤링할 컨텐츠에 대한 액세스 권한이 있는 지원되는 Linux 시스템에서 [Data Crawler 다운로드 및 설치](/docs/services/discovery?topic=discovery-downloading-and-installing-the-data-crawler#downloading-and-installing-the-data-crawler)
1. 컨텐츠에 [Data Crawler 연결](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-connector-and-seed-options)
1. {{site.data.keyword.discoveryshort}} 서비스에 연결하도록 [Data Crawler 구성](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-the-data-crawler)
1. [컨텐츠 크롤링](/docs/services/discovery?topic=discovery-crawling-your-data-repository#crawling-your-data-repository)

[Data Crawler 시작하기](/docs/services/discovery?topic=discovery-getting-started-with-the-data-crawler#getting-started-with-the-data-crawler)에 있는 예를 따라 Data Crawler를 빠르게 시작할 수 있습니다.
