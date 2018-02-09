---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-08"

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

# 開始使用資料搜索器

本主題說明如何使用資料搜索器從本端檔案系統汲取檔案，來與 {{site.data.keyword.discoveryfull}} 服務搭配使用。
{: shortdesc}

在嘗試這項作業之前，請先在 {{site.data.keyword.Bluemix}} 中建立一個 {{site.data.keyword.discoveryshort}} 服務實例。為了完成本手冊，您需要使用與所建立之服務實例相關聯的認證。

## 建立環境

使用 bash POST /v1/environments 方法來建立環境。請將環境視為要儲存所有文件箱的倉儲。下列範例會建立一個稱為 `my-first-environment` 的環境：

將 `{username}` 和 `{password}` 取代為您的服務認證。

```bash
curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
```
{: pre}

API 傳回的回應包括諸如環境 ID、環境狀態以及環境使用的儲存體數量等資訊。在環境狀態變成 `ready` 之前，請不要進行下一步。當您建立環境時，如果狀態傳回 `status:pending`，請使用 `GET /v1/environments/{environment_id}` 方法來檢查狀態，直到它已備妥為止。在此範例中，請將 `{username}` 和 `{password}` 取代為您的服務認證，並將 `{environment_id}` 取代為您建立環境時所傳回的環境 ID。

```bash
curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}?version=2017-11-07
```
{: pre}

## 建立集合

接下來，使用 `POST /v1/environments/{environment_id}/collections` 方法來建立集合。請將集合視為儲存您環境中文件的箱子。這個範例會在前一個步驟所建立的環境中，建立一個稱為 `my-first-collection` 的集合，並使用下列預設配置：

-   將 `{username}` 和 `{password}` 取代為您的服務認證。
-   將 `{environment_id}` 取代為您在步驟 1 中建立之環境的環境 ID。

建立集合之前，您必須先取得預設配置的 ID。若要尋找預設的 `configuration_id`，請使用 `GET /v1/environments/{environment_id}/configurations` 方法：

```bash
curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07
```
{: pre}

一旦您具有預設配置 ID，即可使用它來建立集合。請將 `{configuration_id}` 取代為您環境的預設配置 ID。

```bash
curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{"name": "my-first-collection", "description": "exploring collections", "configuration_id":"{configuration_id}" , "language": "en_us"}' https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07
```
{: pre}

API 傳回的回應包括諸如集合 ID、集合狀態以及集合使用的儲存體數量等資訊。在集合狀態變成 `online` 之前，請不要進行下一步。當您建立集合時，如果狀態傳回 `status:pending`，請使用 `GET /v1/environments/{environment_id}/collections/{collection_id}` 方法來檢查狀態，直到它已備妥為止。在此範例中，請將 `{username}` 和 `{password}` 取代為您的服務認證，將 `{environment_id}` 取代為您的環境 ID，並將 `{collection_id}` 取代為此步驟先前傳回的集合 ID。

```bash
curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07
```
{: pre}

## 下載範例文件
下載這些文件：

-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示" title="外部鏈結圖示" class="style-scope doc-content"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示" title="外部鏈結圖示" class="style-scope doc-content"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示" title="外部鏈結圖示" class="style-scope doc-content"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示" title="外部鏈結圖示" class="style-scope doc-content"></a>

## 下載並安裝資料搜索器

1.  驗證系統必備項目

    -   Java Runtime Environment 第 8 版或更新版本

        **附註：**`JAVA_HOME` 環境變數必須正確設定，或完全不設定，才能執行「搜索器」。
    -   Red Hat Enterprise Linux 6 或 7，或 Ubuntu Linux 15 或 16。為了達到最佳效能，「資料搜索器」應該在自己的 Linux 實例上執行，不論它是虛擬機器、容器或硬體。
    -   Linux 系統上最少有 2 GB RAM

1.  開啟瀏覽器，並登入 [{{site.data.keyword.Bluemix_notm}} 帳戶 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net){: new_window}。
1.  從 {{site.data.keyword.Bluemix_notm}} 儀表板中，選取您先前建立的 {{site.data.keyword.discoveryshort}} 服務。
1.  在**預期用途**下，針對您的系統選取適當的下載鏈結（DEB、RPM 或 ZIP），以下載「資料搜索器」。
1.  以管理者身分，使用適當的指令來安裝您下載的保存檔：

    -   在使用 rpm 套件的 Red Hat 及 CentOS 之類的系統上，請使用如下的指令：`rpm -i /full/path/to/rpm/package/rpm-file-name`
    -   在使用 deb 套件的 Ubuntu 及 Debian 之類的系統上，請使用如下的指令：`dpkg -i /full/path/to/deb/package/deb-file-name`
    -   「搜索器 Script」會安裝至 `{installation directory}/bin`；例如，`/opt/ibm/crawler/bin`。請確定 `{installation_directory}/bin` 位於 `PATH` 環境變數中，「搜索器」指令才能正確運作。

    「搜索器 Script」也會安裝至 `/usr/local/bin`，因此這也可以新增至 `PATH` 環境變數。
    {: tip}

## 建立工作目錄

將 `{installation_directory}/share/examples/config` 目錄的內容複製到系統上的工作目錄，例如 `/home/config`。

**警告：**請勿直接修改提供的配置範例檔。請複製後再進行編輯。如果您直接編輯範例檔，則在升級「資料搜索器」時可能會改寫您的配置，或在解除安裝時可能會將其移除。

**附註：**本手冊如參照 `config` 目錄中的檔案（例如 `config/crawler.conf`），是參照您工作目錄中的該檔案，而「非」已安裝的 `{installation_directory}/share/examples/config` 目錄中的檔案。

## 配置搜索選項

若要設定「資料搜索器」來搜索儲存庫，您必須指定要搜索的本端系統檔案，以及在搜索完成之後所搜索檔案的集合要傳送至哪個 {{site.data.keyword.discoveryshort}} 服務。

1.  **`filesystem-seed.conf`** - 在文字編輯器中開啟 `seeds/filesystem-seed.con` 檔案。請將位於 `name-"url"` 屬性正下方的 `value` 屬性修改成您想要搜索的檔案路徑。例如：`value-"sdk-fs:///TMP/MY_TEST_DATA/"`

    **附註：**URL 必須以 `sdk-fs://` 開頭。因此比方說，若要搜索 `/home/watson/mydocs`，此 URL 的值會是 `sdk-fs:///home/watson/mydocs` - 第三個 / 是必要的！

    儲存並關閉檔案。

1.  **`discovery_service.conf`** - 在文字編輯器中開啟 `discovery/discovery_service.conf` 檔案。修改您先前在 {{site.data.keyword.Bluemix_notm}} 上建立的 {{site.data.keyword.discoveryshort}} 服務特有的下列值：

    -   `environment_id` - {{site.data.keyword.discoveryshort}} 服務環境 ID。
    -   `collection_id` - {{site.data.keyword.discoveryshort}} 服務集合 ID。
    -   `configuration_id` - {{site.data.keyword.discoveryshort}} 服務配置 ID。
    -   `configuration` - 這個 `discovery_service.conf` 檔案的完整路徑位置，例如，`/home/config/discovery/discovery_service.conf`。
    -   `username` - {{site.data.keyword.discoveryshort}} 服務的使用者名稱認證。
    -   `password` - {{site.data.keyword.discoveryshort}} 服務的密碼認證。
1.  **`crawler.conf`** - 在文字編輯器中開啟 `config/crawler.conf` 檔案。

    -   如下所示，針對 {{site.data.keyword.discoveryshort}} 服務設定 `output_adapter` 的 `class` 和 `config` 選項：

        ```bash
        class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

        config - "discovery_service"

        discovery_service {
          include "discovery/discovery_service.conf"
        }
        ```
        {: pre}

1.  修改這些檔案之後，您就可以開始搜索資料。

## 搜索資料

執行下列指令：`crawler crawl --config [config/crawler.conf]`

這會使用配置檔 `crawler.conf` 來執行搜索。

**附註：**`--config` 選項中所傳入的配置檔路徑必須是完整路徑。也就是說，它必須採用相對格式（例如 `config/crawler.conf` 或 `./crawler.conf`）或絕對路徑（例如 `/path/to/config/crawler.conf`）。

## 搜尋文件

最後，請使用 `GET /v1/environments/{environment_id}/collections/{collection_id}/query` 方法來搜尋您的文件集合。下列範例會傳回所有稱為 `IBM` 的實體：

-   將 `{username}` 和 `{password}` 取代為您的服務認證。
-   將 `{environment_id}` 取代為您在步驟 1 中建立之環境的環境 ID。
-   將 `{collection_id}` 取代為您在步驟 2 中建立之集合的集合 ID。

```bash
curl -u "{username}":"{password}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&query-enriched_text.entities.text:IBM'
```
{: pre}

## 結果

您目前已在所建立的環境和集合中順利查詢文件。現在，您可以在集合中新增更多文件來開始進行自訂作業。
