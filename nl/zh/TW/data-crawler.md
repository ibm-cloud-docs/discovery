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

# 使用資料搜索器新增內容
{: #adding-content-with-data-crawler}

資料搜索器可讓您將內容自動上傳至 {{site.data.keyword.discoveryshort}} 服務。
{: shortdesc}

「資料搜索器」應該只用來搜索檔案共用或資料庫，針對所有其他用途，您應使用適當的 {{site.data.keyword.discoveryshort}} 連接器。如需詳細資訊，請參閱[連接至資料來源](/docs/services/discovery?topic=discovery-sources#sources)。如果您將「資料搜索器」用於 {{site.data.keyword.discoveryshort}} 連接器支援的資料來源，則不再為其提供協助。
{: important}

## 使用資料搜索器搜索資料
{: #dc-crawling}

「資料搜索器」是一種指令行工具，可協助您從文件所在的儲存庫（例如：檔案共用、資料庫）取得文件，並將其推送至雲端，以供 {{site.data.keyword.discoveryshort}} 服務使用。

「資料搜索器」應該只用來搜索檔案共用或資料庫，針對所有其他用途，您應該要為 Box、SharePoint、Salesforce、IBM Cloud Object Storage 或網路搜索使用適當的 {{site.data.keyword.discoveryshort}} 連接器。如需詳細資訊，請參閱[連接至資料來源](/docs/services/discovery?topic=discovery-sources#sources)。如果您將「資料搜索器」用於 {{site.data.keyword.discoveryshort}} 連接器支援的資料來源，則不再為其提供協助。
{: important}

## 何時使用資料搜索器
{: #dc-use}

如果您想要以受管理方式從遠端系統上傳大量檔案，或想要從支援的儲存庫（例如 Db2 資料庫）擷取內容，則應該使用「資料搜索器」。

「資料搜索器」並不是要成為從本端磁碟機上傳檔案的解決方案。從本端磁碟機上傳檔案應該使用工具或使用直接 API 呼叫來完成。
將大量檔案上傳至 {{site.data.keyword.discoveryshort}} 的另一個選項，就是 GitHub 上的 [discovery-files ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/IBM/discovery-files){: new_window}。
{: note}

## 使用資料搜索器
{: #dc-using}

1. [配置 {{site.data.keyword.discoveryshort}} 服務](/docs/services/discovery?topic=discovery-configservice#configservice)
1. 在能夠存取您要搜索之內容的受支援 Linux 系統上，[下載並安裝資料搜索器](/docs/services/discovery?topic=discovery-downloading-and-installing-the-data-crawler#downloading-and-installing-the-data-crawler)。
1. [連接資料搜索器](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-connector-and-seed-options)至您的內容。
1. [配置資料搜索器](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-the-data-crawler)以連接至 {{site.data.keyword.discoveryshort}} 服務。
1. [搜索內容](/docs/services/discovery?topic=discovery-crawling-your-data-repository#crawling-your-data-repository)。

遵循下列範例，您就可以很快開始使用「資料搜索器」：[開始使用資料搜索器](/docs/services/discovery?topic=discovery-getting-started-with-the-data-crawler#getting-started-with-the-data-crawler)
