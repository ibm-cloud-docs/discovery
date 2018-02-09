---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-09"

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

# Discovery 定價方案

{{site.data.keyword.discoveryfull}} 服務提供三個方案，提供不同層次的資源及功能來符合您的需求。
{: shortdesc}

**專用資料使用案例**有下列限制和價格：

| 精簡                     |  標準             | 進階              | 超值             |
|--------------------------|-------------------|-------------------|-------------------|
| 每月最多 2,000 份並行文件\*|每月最多 100,000 份並行文件\*<br/> 每月每 1,000 份並行文件 10 美元（0.0139 美元/1000 份文件/小時)\*\*\*<br/> 每月免費 2,000 份文件\*\*\*\*  | **保留環境**</br>基本費率每月 1,000 美元<br/> 每月最多 1,000,000 份文件\*<br/> 每月每 1,000 份並行文件 5 美元（0.00694 美元/1000 份文件/小時）\*\*\*<br/> 包括每月 100,000 份文件\*\*\*\*</br> 若為較大的環境，請聯絡[銷售人員 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/marketing/iwm/dre/signup?source=MAIL-watson){: new_window}。| **超值方案**提供一個以上 Watson 服務的單一承租戶實例給開發人員和組織，以達到更好的隔離與安全。這些方案在現有的共用平台上提供運算層次隔離，以及傳送中與靜止的端對端加密資料。如需相關資訊或要購買超值方案，請聯絡[銷售人員 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://ibm.biz/contact-wdc-premium){: new_window} |
| 200MB\*\*                  |10GB\*\*  | 80GB\*\* |-|
| 最多 2 個集合      |最多 4 個集合 | 最多 100 個集合 |-|
| 最多 1 個 {{site.data.keyword.knowledgestudiofull}} 自訂模型     |最多 1 個 {{site.data.keyword.knowledgestudioshort}} 自訂模型     | 無限個 {{site.data.keyword.knowledgestudioshort}} 自訂模型<br/>包括 1 個 {{site.data.keyword.knowledgestudioshort}} 自訂模型<br/>每月每個 {{site.data.keyword.knowledgestudioshort}} 模型另付 800 美元|-|

**附註：**在所有方案中，每月前 1,000 個 {{site.data.keyword.discoverynewsshort}} 查詢免費。第 1,000 個之後，{{site.data.keyword.discoverynewsshort}} 查詢的每個查詢收費 0.10 美元。

**附註：**精簡方案服務在閒置 30 天之後會遭到刪除。精簡方案的每個組織會分配一個免費環境。

 \* 文件限制假設磁碟上的平均文件大小為 100KB。這是集合內的文件大小，經過轉換及強化之後，其大小可能與原始輸入明顯不同。您可以使用 `environments` 或 `collections` API，或是使用工具，來檢視已儲存的文件數和已使用的儲存空間總量。

 \*\* 如果磁碟上的文件平均大於 100KB，在達到取最大文件限制之前，您就會達到方案的儲存空間限制。

 \*\*\* 「價格」是以一個批次 1,000 份文件儲存在服務中的時數為依據（稱為「千份文件-小時」）。您應該在定價計算機中輸入這個數字 (`number of documents * number of hours those documents are stored in a month / 1000`)。

 \*\*\*\* 免費數量是依據一個月儲存之文件的對等數量。例如，在「標準」方案中，免費數量相當於 2,000 份文件 * 720 小時 / 1000 份文件批次 = 1440 千份文件-小時。

**範例：**「標準」方案的使用者整個月儲存 4,000 份文件。向他們收費的方式如下：

- `4000 documents * 720 hours (in a month) / 1000 = 2,880` 已耗用的千份文件-小時

- `2,880 - 1,440 (free document hours) = 1,440` 可收費的千份文件-小時

- `1,440 * $0.0139`（每千份文件-小時的價格） = `$20.00`（該月份）

**附註：**計算每小時的帳單金額時，儲存的文件總數會在計算中捨入至最接近的 1,000。比方說，如果您 1 小時儲存了 4,678 份文件，則會捨入為 5,000，導致向該帳戶收取 5 千份文件-小時的費用。

**附註：**對於強化不另外收費。

如需 {{site.data.keyword.Bluemix_notm}} 安全的相關資訊，請參閱 [{{site.data.keyword.Bluemix_notm}} 服務說明 ![外部圖示鏈結](../../icons/launch-glyph.svg "外部鏈結圖示")](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=IBM+Bluemix+Service+Description){: new_window}.

## 從前一個定價方案轉換

在 **2017 年 8 月 1 日**之前訂閱方案的客戶已移轉至其中一個新方案。

- 先前使用 30 天免費試用方案的客戶已移轉至**精簡**方案。
  由於這項轉移，現有的使用者可能已達到或已超出精簡方案限制，亦即文件數 _(2000)_、儲存空間 _(200Mb)_ 或集合數 _(2)_。如果您已超出**精簡**方案的限制，則無法將任何其他內容新增至該服務，但仍然可以查詢集合。您可以使用 {{site.data.keyword.discoveryshort}} 工具或 API 來檢視所有這些限制的現行狀態。若要能夠繼續將內容新增至 {{site.data.keyword.discoveryshort}} 實例，您必須執行下列其中一項：
  - 移除集合及（或）文件，使其不超出**精簡**方案的限制。
    可以透過 API 使用 [delete-doc ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-doc){: new_window} 方法個別刪除文件，或利用工具或 API，使用 [delete-collection ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-collection){: new_window} 方法來刪除整個集合。
  - 將方案升級至符合儲存空間需求的層次。
- 大小為 **`1`**、**`2`** 或 **`3`** 環境的客戶已自動移轉至**進階**方案。
  如果您已移至「進階」層級但具有不到 100,000 份文件和 4 個集合，則可以移至「標準」層級以減少成本。這需要在「標準」方案中建立新的 Discovery 實例，並將資料重新汲取到新的實例。您可以透過工具、API 或「資料搜索器」來進行汲取。

如需其他定價資訊，請參閱 [{{site.data.keyword.discoveryshort}} 型錄 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window}。
