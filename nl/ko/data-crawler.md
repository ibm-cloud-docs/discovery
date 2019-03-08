---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-03"

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

# Data Crawler로 컨텐츠 추가
{: #adding-content-with-data-crawler}

Data Crawler를 사용하면 {{site.data.keyword.discoveryshort}} 서비스에 대한 컨텐츠의 업로드를 자동화할 수 있습니다.
{: shortdesc}

## Data Crawler로 데이터 크롤링

Data Crawler는 문서가 상주하는 저장소(예: 파일 공유, 데이터베이스, Microsoft SharePoint)에서 문서를 사용하고 {{site.data.keyword.discoveryshort}} 서비스로 사용될 클라우드에 문서를 푸시하는 데 도움을 주는 명령행 도구 입니다. 

{{site.data.keyword.discoveryshort}} 도구 또는 API를 사용하여 Box, Salesforce 및 Microsoft SharePoint Online 데이터 소스를 크롤링할 수 있습니다. 자세한 정보는 [데이터 소스에 연결](/docs/services/discovery/connect.html)을 참조하십시오.
{: tip}

## Data Crawler를 사용하는 경우

원격 시스템에서 수많은 파일의 관리 업로드를 수행하려고 하거나 지원되는 저장소(예: DB2 데이터베이스)에서 컨텐츠를 추출하려는 경우 Data Crawler를 사용해야 합니다.

Data Crawler는 로컬 드라이브에서 파일을 업로드하기 위한 솔루션으로 개발된 것은 아닙니다. 도구를 사용하거나 직접적인 API 호출을 사용하여 로컬 드라이브에서 파일을 업로드해야 합니다.
{: tip}

## Data Crawler 사용

1. [{{site.data.keyword.discoveryshort}} 서비스 구성](/docs/services/discovery/building.html#configuring-your-service)
1. 크롤링할 컨텐츠에 대한 액세스 권한이 있는 지원되는 Linux 시스템에서 [Data Crawler 다운로드 및 설치](/docs/services/discovery/data-crawler-install.html)
1. 컨텐츠에 [Data Crawler 연결](/docs/services/discovery/data-crawler-seeds.html)
1. {{site.data.keyword.discoveryshort}} 서비스에 연결하도록 [Data Crawler 구성](/docs/services/discovery/data-crawler-discovery.html)
1. [컨텐츠 크롤링](/docs/services/discovery/data-crawler-run.html)

[Data Crawler 시작하기](/docs/services/discovery/data-crawler-qs.html)에 있는 예를 따라 Data Crawler를 빠르게 시작할 수 있습니다.
