---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-18"

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

# 使用資料搜索器新增內容

資料搜索器可讓您將內容自動上傳至 {{site.data.keyword.discoveryshort}} 服務。
{: shortdesc}

## 使用資料搜索器搜索資料

「資料搜索器」是一種指令行工具，可協助您從文件所在的儲存庫（例如：檔案共用、資料庫、Microsoft SharePoint&reg;）取得文件，並將它們推送至雲端，以供 {{site.data.keyword.discoveryshort}} 服務使用。

## 何時使用資料搜索器

如果您想要以受管理方式從遠端系統上傳大量檔案，或想要從支援的儲存庫（例如 DB2 資料庫）中擷取內容，則應該使用「資料搜索器」。

「資料搜索器」並未預期成為從本端磁碟機上傳檔案的解決方案。從本端磁碟機上傳檔案應該使用工具或使用直接 API 呼叫來完成。
{: tip}

## 使用資料搜索器

1. [配置 {{site.data.keyword.discoveryshort}} 服務](/docs/services/discovery/building.html#configuring-your-service)
1. 在能夠存取您要搜索之內容的受支援 Linux 系統上[下載及安裝資料搜索器](/docs/services/discovery/data-crawler-install.html)。
1. [連接資料搜索器](/docs/services/discovery/data-crawler-seeds.html)至您的內容。
1. [配置資料搜索器](/docs/services/discovery/data-crawler-discovery.html)以連接至 {{site.data.keyword.discoveryshort}} 服務。
1. [搜索內容](/docs/services/discovery/data-crawler-run.html)。

遵循下列範例，您就可以很快開始使用「資料搜索器」：[開始使用資料搜索器](/docs/services/discovery/data-crawler-qs.html)
