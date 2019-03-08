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

# 搜索資料儲存庫
{: #crawling-your-data-repository}

在適當地配置搜索器選項之後，您可以針對資料儲存庫執行搜索。
{: shortdesc}

除非您需要存取只有 `root` 可以讀取的檔案，否則絕不要以 `root` 身分執行搜索器。
{: tip}

執行下列指令：`crawler`

搜索器會提示您提供文件來說明要執行的作業。除了其他搜索選項之外，您還可以執行測試搜索或執行搜索。

## 執行測試搜索

執行下列指令：`crawler testit`

這會執行測試搜索，它只會搜索種子 URL 並顯示任何放入佇列的 URL。如果種子 URL 產生可檢索的內容（例如，它是文件），則該內容將傳送至輸出配接器，並將內容列印至畫面。如果種子 URL 擷取使 URL 放入佇列，將會顯示那些 URL，且不會將內容傳送至輸出配接器。依預設，會顯示五個放入佇列的 URL。

您也可以指定自訂配置檔作為 testit 指令的選項，例如：`crawler testit --config [config/myconfigfile.conf]`

`--config` 選項中所傳入的配置檔路徑必須是完整路徑。也就是說，它必須採用相對格式（例如 `config/myconfigfile.conf` 或 `./myconfigfile.conf`）或絕對路徑（例如 `/path/to/config/myconfigfile.conf`）。

此外，您還可以設定所顯示之放入佇列的 URL 數目的限制，作為 testit 指令的一個選項，例如：`crawler testit --limit [number]`

## 執行搜索

執行下列指令：`crawler crawl`

這會使用預設配置檔 (`crawler.conf`) 執行搜索。

您也可以指定自訂配置檔作為 crawl 指令的選項，例如：`crawler crawl --config [config/myconfigfile.conf]`

`--config` 選項中所傳入的配置檔路徑必須是完整路徑。也就是說，它必須採用相對格式（例如 `config/myconfigfile.conf` 或 `./myconfigfile.conf`）或絕對路徑（例如 `/path/to/config/myconfigfile.conf`）。

## 重新啟動搜索

執行下列指令：`crawler restart`

此指令透過使用預設配置檔 (`crawler.conf`) 啟動新搜索，來執行重新啟動搜索。

您也可以指定自訂配置檔作為 restart 指令的選項，例如：`crawler restart --config [config/myconfigfile.conf]`

`--config` 選項中所傳入的配置檔路徑必須是完整路徑。也就是說，它必須採用相對格式（例如 `config/myconfigfile.conf` 或 `./myconfigfile.conf`）或絕對路徑（例如 `/path/to/config/myconfigfile.conf`）。

## 繼續搜索

執行下列指令：`crawler resume`

此指令會使用預設配置檔 (`crawler.conf`) 從停止搜索處繼續搜索。

您也可以指定自訂配置檔作為 resume 指令的選項，例如：`crawler resume --config [config/myconfigfile.conf]`

`--config` 選項中所傳入的配置檔路徑必須是完整路徑。也就是說，它必須採用相對格式（例如 `config/myconfigfile.conf` 或 `./myconfigfile.conf`）或絕對路徑（例如 `/path/to/config/myconfigfile.conf`）。

## 重新整理搜索

執行下列指令：`crawler refresh`

此指令會使用預設配置檔 (`crawler.conf`) 重新整理先前的搜索。

您也可以指定自訂配置檔作為 refresh 指令的選項，例如：`crawler refresh --config [config/myconfigfile.conf]`

`--config` 選項中所傳入的配置檔路徑必須是完整路徑。也就是說，它必須採用相對格式（例如 `config/myconfigfile.conf` 或 `./myconfigfile.conf`）或絕對路徑（例如 `/path/to/config/myconfigfile.conf`）。
