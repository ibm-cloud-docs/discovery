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

# 連接至資料來源
{: #sources}

{{site.data.keyword.discoveryshort}} 服務可讓您從遠端來源連接至文件並搜索文件。
{: shortdesc}

您可以配置集合來建立與資料來源的關聯，藉以連接至該資料來源，並（視需要）依排程將文件取回到 {{site.data.keyword.discoveryshort}} 服務。若是使用 {{site.data.keyword.discoveryshort}} 工具，每個集合可以各配置一個資料來源，若是使用 API，可以將多個資料來源的文件傳送至單一集合中。{{site.data.keyword.discoveryshort}} 服務使用一個稱為「搜索」的處理程序，從資料來源取回文件。搜索是指系統性地從指定之開始位置瀏覽及擷取文件的處理程序。只有您明確指定的項目，{{site.data.keyword.discoveryshort}} 服務才會加以搜索。可以搜索的資料來源類型如下：

-  [Box](/docs/services/discovery?topic=discovery-sources#connectbox)
-  [Salesforce](/docs/services/discovery?topic=discovery-sources#connectsf)
-  [Microsoft SharePoint Online](/docs/services/discovery?topic=discovery-sources#connectsp)
-  [Microsoft SharePoint 2016 On-Premise](/docs/services/discovery?topic=discovery-sources#connectsp_op)
-  [Web 搜索](/docs/services/discovery?topic=discovery-sources#connectwebcrawl)（測試版）
-  [IBM Cloud Object Storage](/docs/services/discovery?topic=discovery-sources#connectcos)

您可以使用 {{site.data.keyword.discoveryshort}} 工具或 API 來連接至資料來源。{{site.data.keyword.discoveryshort}} 工具提供的簡化連線方法不需要太瞭解來源系統，而 API 則提供更精細且可高度配置的介面，這需要對您所要連接的來源有較深入的瞭解。下列處理程序概觀可讓您知道接下來要閱讀本文件的哪幾節：

1.  閱讀[一般來源需求](/docs/services/discovery?topic=discovery-sources#gen_req)，可大概瞭解您需要哪些項目。
2.  閱讀來源系統的特定需求：
    -  [Box](/docs/services/discovery?topic=discovery-sources#connectbox)
    -  [Salesforce](/docs/services/discovery?topic=discovery-sources#connectsf)
    -  [Microsoft SharePoint Online](/docs/services/discovery?topic=discovery-sources#connectsp)
    -  [Microsoft SharePoint 2016 On-Premise](/docs/services/discovery?topic=discovery-sources#connectsp_op)
    -  [Web 搜索](/docs/services/discovery?topic=discovery-sources#connectwebcrawl)（測試版）
    -  [IBM Cloud Object Storage](/docs/services/discovery?topic=discovery-sources#connectcos)
3.  根據您的配置選項，閱讀來源配置指示：
    -  [使用工具](/docs/services/discovery?topic=discovery-sources#source_tooling)
    -  [使用 API](/docs/services/discovery?topic=discovery-sources#source_api)

如果選取內部部署資料來源，您必須先安裝及配置 IBM Secure Gateway。如需相關資訊，請參閱[為內部部署資料安裝 IBM Secure Gateway](/docs/services/discovery?topic=discovery-sources#gateway)。

## 一般來源需求
{: #gen_req}

下列一般需求適用於所有資料來源：

-  Box、Salesforce、SharePoint Online、SharePoint 2016、IBM Cloud Object Storage 和 Web 搜索的個別文件檔案大小限制為 10MB。
-  您將需要每一個資料來源的認證和檔案位置（或 URL），這些通常是由資料來源的開發人員/系統管理者提供。
-  您需要知道要搜索資料來源的哪些資源。這可以由來源管理者提供。如果是搜索 Box 或 Salesforce，則在使用 {{site.data.keyword.discoveryshort}} 工具配置來源時會出現一份可用的資源清單。
-  若是使用 {{site.data.keyword.discoveryshort}} 工具，一個集合可以配置單一資料來源。若是使用 API，可以將多個資料來源的文件傳送至單一集合中。
-  搜索資料來源將使用資料來源的資源（API 呼叫）。API 呼叫數目取決於需要搜索的文件數目。必須為資料來源取得適當的服務授權層級（例如「企業」），且必須諮詢來源系統管理者。
-  {{site.data.keyword.discoveryshort}} 來源搜索不會刪除已儲存在集合中的文件。重新搜索來源時，會新增新的文件、將已更新的文件修改為現行版本，而已刪除的文件則會保留為前次儲存的版本。
-  {{site.data.keyword.discoveryshort}} 可汲取下列檔案類型，並且會忽略所有其他文件類型：

集合 | 精簡方案 | 進階方案 
---------------- | ------------------------------ | ------------------------------------------- 
在[智慧型文件理解 (SDU)](/docs/services/discovery?topic=discovery-release-notes#22jan19) 版本之前，專為 {{site.data.keyword.discoveryfull}} 建立的現有集合  | Microsoft Word、PDF、HTML、JSON | Microsoft Word、PDF、HTML、JSON     
在 [SDU](/docs/services/discovery?topic=discovery-sdu#sdu) 版本之後建立的集合 | PDF、Word、PowerPoint、Excel、JSON\*、HTML\* | PDF、Word、PowerPoint、Excel、PNG\*\*、TIFF\*\*、JPG\*\*、JSON\*、HTML\* 
    
\* {{site.data.keyword.discoveryfull}} 可支援 JSON 和 HTML 文件，但您無法使用 SDU 編輯器來編輯這些文件。若要變更 HTML 和 JSON 文件的配置，您需要使用 API。如需相關資訊，請參閱 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery/){: new_window}。

\*\* 將會掃描個別影像檔（PNG、TIFF、JPG），並擷取文字（若有的話）。另外也會掃描內嵌在 PDF、Word、PowerPoint 和 Excel 檔案中的 PNG、TIFF 和 JPEG 影像，並擷取文字（若有的話）。

## Box
{: #connectbox}

您需要建立新的 Box 自訂應用程式來連接至 {{site.data.keyword.discoveryfull}}。您建立的 Box 應用程式需要「企業」層級或「應用程式」層級存取。

-  如果您不是組織的 Box 管理者，建議使用[**「應用程式」層級**存取](/docs/services/discovery?topic=discovery-sources#applevelbox)。您需要管理者核准您的應用程式。
-  如果您是組織的 Box 管理者，建議使用[**「企業」層級**存取](/docs/services/discovery?topic=discovery-sources#entlevelbox)。

如果有 Box 更新，設定 Box 存取的步驟可能會變更。請參閱 [Box 開發者說明文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.box.com/){: new_window}，查看是否有更新項目。
{: note}

### 設定「應用程式」層級存取
{: #applevelbox}

1.   導覽至 `https://app.box.com/developers/console`（請使用您公司的 Box URL），然後按一下**建立新的應用程式**。
1.   從**建立新的應用程式**畫面，選取**企業整合**，並按**下一步**。
1.   在**鑑別方法**畫面中，選取 **OAuth 2.0 與 JWT（伺服器鑑別）**，並按**下一步**。
1.   為您的應用程式命名，然後按一下**建立應用程式**按鈕。建立 Box 應用程式之後，按一下**檢視您的應用程式**。
1.   檢視應用程式時，將**應用程式存取**選取為**應用程式**。您可以使用現有的受管理使用者繼續進行；不需要建立新的使用者。
1.   向下捲動至頁面的**應用程式範圍**區段，並啟用下列勾選框： 
     - `讀取及寫入 Box 中儲存的所有資料夾`
     - `管理使用者`
1.   向下捲動至**進階功能**區段，並啟用下列切換：
     - `以使用者身分執行動作`
     - `產生使用者存取記號` 
1.  按一下**儲存變更**按鈕。

接下來幾個步驟需要組織的 Box 帳戶管理者協助。如果您不是組織 Box 管理者，可以開啟 Box 開發人員的主控台，在**帳戶設定** > **帳戶詳細資料** > **設定**之下查看，以識別管理者。

1.  [管理者步驟] 在 `https://app.box.com/master/settings/openbox` 中按一下**授權新的應用程式**按鈕，以授權您的應用程式用戶端 ID。
1.  [管理者步驟] 從 `https://app.box.com/developers/console`，在 **API 金鑰**欄位中鍵入**用戶端 ID**，然後按一下**授權**按鈕。
1.  [管理者步驟] 擷取應用程式的開發人員記號。若要執行此作業，請導覽至 `https://app.box.com/developers/console`，捲動至**開發人員記號**區段，並產生您的記號。
1.  現在應用程式已由管理者授權，請導覽至 `https://developer.box.com/reference#page-create-an-enterprise-user`，使用 API 參考資料頁面來建立「應用程式使用者」。

   建立「應用程式使用者」的 Curl 範例：

   ```bash
    curl https://api.box.com/2.0/users -H "Authorization: Bearer ACCESS_TOKEN" -d '{"name": "NedStark", "is_platform_access_only": true}' -X POST
   ```
   {: pre}

1.  複製新產生的 **id** 欄位內容，並提供給將 Box 應用程式連接至 {{site.data.keyword.discoveryfull}} 的非管理者。
1.  建立「應用程式使用者」之後，必須將您要搜索的資料夾與該「應用程式使用者」共用，且必須提供那些資料夾的`檢視者`權限給該「應用程式使用者」。這需要上述 curl 指令回應的「應用程式使用者」登入名稱。範例：`"login":"AppUser_737729_jmUo@boxdevedition.com"`。
1.  回到 Box 開發人員主控台 `https://app.box.com/developers/console`，並捲動至**新增及管理公開金鑰**區段。按一下**產生公開/私密金鑰組**，並下載您的金鑰組檔案。開啟檔案。
1.  從金鑰組檔案剪下下列欄位，並貼在 {{site.data.keyword.discoveryshort}} 工具中。
    -  `client_id`
    -  `enterprise_id`
    -  `client_secret` 
    -  `public_key_id` 
    -  `private_key` 
    -  `passphrase` 

### 設定「企業」層級存取
{: #entlevelbox}

1.  導覽至 `https://app.box.com/developers/console`（請使用您公司的 Box URL），然後按一下**建立新的應用程式**。
1.  從**建立新的應用程式**畫面，選取**企業整合**，並按**下一步**。
1.  在**鑑別方法**畫面中，選取 **OAuth 2.0 與 JWT（伺服器鑑別）**，並按**下一步**。
1.  為您的應用程式命名，然後按一下**建立應用程式**按鈕。建立 Box 應用程式之後，按一下**檢視您的應用程式**。
1.  檢視應用程式時，將**應用程式存取**選取為**企業**。您可以使用現有的受管理使用者繼續進行；不需要建立新的使用者。
1.  向下捲動至頁面的**應用程式範圍**區段，並啟用下列勾選框： 
    - `讀取及寫入 Box 中儲存的所有資料夾`
    - `管理使用者`
    - `管理企業內容`
1.  向下捲動至**進階功能**區段，並啟用下列切換：
    - `以使用者身分執行動作`
    - `產生使用者存取記號` 
1.  按一下**儲存變更**按鈕。

只有「企業」層級存取可支援重新整理 (`Refresh`)。
{: note}

如果您變更 Box 應用程式設定，請重新授權 (`Reauthorize`) 應用程式，使變更生效。
{: tip}

接下來幾個步驟需要組織的 Box 帳戶管理者協助。如果您不是組織 Box 管理者，可以開啟 Box 開發人員的主控台，在**帳戶設定** > **帳戶詳細資料** > **設定**之下查看，以識別管理者。

1.  [管理者步驟] 導覽至**管理主控台** > **企業設定** > **應用程式**，並捲動至`自訂應用程式`，以授權您的應用程式用戶端 ID。URL 範例：`https://app.box.com/master/settings/openbox`。
1.  [管理者步驟] 從 `https://app.box.com/developers/console`，在 **API 金鑰**欄位中鍵入**用戶端 ID**，然後按一下**授權**按鈕。
1.  回到 Box 開發人員主控台 `https://app.box.com/developers/console`，並捲動至**新增及管理公開金鑰**區段。按一下**產生公開/私密金鑰組**，並下載您的金鑰組檔案。開啟檔案。
1.  從金鑰組檔案剪下下列欄位，並貼在 {{site.data.keyword.discoveryshort}} 工具中。
    -  `client_id`
    -  `enterprise_id`
    -  `client_secret` 
    -  `public_key_id` 
    -  `private_key` 
    -  `passphrase` 

搜索 Box 時要考量的其他項目：

-  Box 附註是以 JSON 格式儲存，因此，{{site.data.keyword.discoveryshort}} 會汲取所指定資料夾中的任何 Box 附註。
-  使用 API 時，您需要有一份清單，列出您要搜索之每個資料夾的「資料夾 ID」及相關聯的「擁有者 ID」。{{site.data.keyword.discoveryshort}} 工具可讓您瀏覽並選取要搜索的內容。

## Salesforce
{: #connectsf}

連接至 Salesforce 來源時，請確定您計劃要連接的實例是「企業」方案或更高版本。

需要下列認證才能連接至 Salesforce 來源，應該向您的 Salesforce 管理者取得認證：
-  `url` - 這些認證所連接來源的 `url`。
-  `username` - 這些認證所連接來源的 `username`。
-  `password` - `password` 包含 Salesforce 密碼，並連結一個有效的 Salesforce 安全記號。絕不會傳回此值，而且只有在建立或修改認證時才會使用此值。

識別認證時，參考 [Salesforce 開發人員文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.salesforce.com/docs/){: new_window} 可能有幫助。

當搜索 Salesforce 時要注意的其他項目：

-  只有當知識庫文章的**版本**為 `published`，且其語言為 `en-us` 時，才會搜索它們。
-  使用 API 時，您需要具有要搜索的 Salesforce 物件清單。{{site.data.keyword.discoveryshort}} 工具可讓您瀏覽並選取要搜索的內容。

## SharePoint Online
{: #connectsp}

連接至 Microsoft SharePoint Online 來源時，請確定您計劃要連接的實例是「企業 (E1)」方案或更高版本。

需要下列認證才能連接至 SharePoint Online 來源，應該向您的 SharePoint 管理者取得認證：

-  `organization_url` - 這些認證所連接來源的 `organization_url`。
-  `site_collection_path` - 這些認證所連接來源的 `site_collection_path`。
-  `username` - 這些認證所連接來源的 `client_id`。此使用者必須有權存取需要搜索及檢索的所有網站和清單。
-  `password` - 這些認證所連接來源的 `password`。絕不會傳回此值，而且只有在建立或修改認證時才會使用此值。

識別認證時，參考 [Microsoft SharePoint 開發人員文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.microsoft.com/en-us/sharepoint/dev/){: new_window} 可能有幫助。

搜索 Microsoft SharePoint Online 時要注意的其他項目：

-  若要搜索 SharePoint，`搜索使用者`帳戶必須要有`網站收集管理者`權限。
-  搜索 SharePoint 時，您需要有所要搜索的 SharePoint 網站收集路徑清單。{{site.data.keyword.discoveryshort}} 不支援資料夾路徑做為輸入值。

## Web 搜索
{: #connectwebcrawl}

此測試版特性可用來搜索不需要密碼的公開網站。您可以選取 {{site.data.keyword.discoveryshort}} 與網站同步的頻率、語言和躍點數目。

-  `同步我的資料` - 您可以選擇每隔 5 分鐘、每小時、每日、每週或每月同步一次。 
-  `選取語言` - 從支援的語言清單中選擇網站的語言。如需 {{site.data.keyword.discoveryshort}} 支援的語言清單，請參閱[語言支援](/docs/services/discovery?topic=discovery-language-support#supported-languages)。建議您針對每個語言各建立一個集合。
-  `要同步的 URL 群組` - 輸入您的 URL，然後按一下加號，將其新增至 URL 群組。若要指定此 URL 群組的**搜索設定**，請按一下 ![齒輪](images/icon_settings.png) 圖示。您可以設定**躍點上限**，這是從起始 URL（起始 URL 為 `0`）開始連接的連續鏈結數目。躍點的預設數目為 `2`，上限為 `20`（若是使用 API，則上限為 `1000`）。 

就此測試版而言，所搜索的網頁數會有限制，所以 Web 搜索器可能無法搜索指定的所有網站，而達到躍點數上限。
{: note}

如果您需要為其他 URL 使用不同的**搜索設定**，請按一下**新增 URL 群組**，並建立新的群組。您可以依需要建立任意數量的 URL 群組。
{: tip}

## SharePoint 2016 On-Premise
{: #connectsp_op}

Microsoft SharePoint 2016（又稱為 SharePoint Server 2016）是一種內部部署資料來源。若要連接至此來源，您必須先安裝並配置 IBM Secure Gateway。如需相關資訊，請參閱[為內部部署資料安裝 IBM Secure Gateway](/docs/services/discovery?topic=discovery-sources#gateway)。
{: note}

需要下列認證才能連接至 SharePoint 2016 資料來源，應該向您的 SharePoint 管理者取得這些認證：

-  `username` - 這些認證所連接來源的 `client_id`。此使用者必須有權存取需要搜索及檢索的所有網站和清單。
-  `password` - 這些認證所連接來源的 `password`。絕不會傳回此值，而且只有在建立或修改認證時才會使用此值。
-  `web_application_url` - SharePoint 2016 `web_application_url`；例如，https://sharepointwebapp.com:8443。若未提供埠號，則預設為埠 `80` 用於 http，而埠 `443` 用於 https。
-  `domain` - SharePoint 2016 帳戶的 `domain`。

識別認證時，參考 [Microsoft SharePoint 開發人員文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.microsoft.com/en-us/sharepoint/dev/){: new_window} 可能有幫助。

搜索 Microsoft SharePoint 2016 時要注意的其他事項：

-  若要搜索 SharePoint 2016，`搜索使用者`帳戶必須要有`網站收集管理者`權限。
-  搜索 SharePoint 時，您需要有所要搜索的 SharePoint 網站收集路徑清單。{{site.data.keyword.discoveryshort}} 不支援資料夾路徑做為輸入值。

## IBM Cloud Object Storage
{: #connectcos}

連接至 IBM Cloud Object Storage 來源時，需要下列認證，應該向您的 IBM Cloud Object Storage 管理者取得這些認證：

-  `endpoint` - `endpoint` 可用來與 IBM Cloud Object Storage 資料互動。
-  `access_key_id` - 建立 IBM Cloud Object Storage 實例時，會取得 `access_key_id`。
-  `secret_access_key` - 建立 IBM Cloud Object Storage 實例時，會取得可簽署要求的 `secret_access_key`。

輸入此資訊之後，您可以選擇同步資料的頻率，並選取您想要同步至哪個儲存區。

搜索 IBM Cloud Object Storage 時要注意的其他事項：

-  此連接器不支援搜索專用端點。
-  如果選取所有儲存區，會有輕微的效能問題。在此情況下，文件在完成檢索之前可能會有些延遲。

## 使用工具
{: #source_tooling}

使用 {{site.data.keyword.discoveryshort}} 工具連接至資料來源時，需要特別為來源建立集合來執行。執行下列步驟以建立來源集合並對其進行搜索：

1.  從 {{site.data.keyword.discoveryshort}} 工具的**管理資料**頁面中，選取**連接資料來源**。
2.  選取您要連接的資料來源。如果您已選取內部部署資料來源，則需要先安裝 IBM Secure Gateway。如需相關資訊，請參閱[為內部部署資料安裝 IBM Secure Gateway](/docs/services/discovery?topic=discovery-sources#gateway)。 
3.  輸入您的來源認證，然後按一下「連接」。必須向來源系統管理者取得您的來源認證。
4.  選擇您要搜索的資料及其同步頻率。同步選項：
    -  每隔 5 分鐘：每隔 5 分鐘執行一次
    -  每小時：每小時執行一次
    -  每日：每天在指定時區的 00:00 到 06:00 執行
    -  每週：每週在指定時區的星期日 00:00 到 06:00 執行
    -  每月：每月在指定時區的當月第一個星期日 00:00 到 06:00 執行
    
    搜索狀態範例：
    
    ```json
    "crawl_status" : {
    "source_crawl" : {
      "status" : "completed",
      "next_crawl" : "2019-02-10T05:00:00-05:00"
    }
    ```
5.  按一下**儲存 & 同步物件**，開始搜索您的資料來源。然後，系統會將您重新導向至集合狀態畫面，當文件新增至集合時此畫面就會更新。

搜索一開始會使資料同步，然後依照您指定的頻率進行同步。**附註：**如果您在**同步設定**畫面中修改任何項目，然後按一下**儲存並同步物件**，則會在該時間啟動搜索（如果已經在執行，則重新啟動）。

## 使用 API
{: #source_api}

使用下列處理程序，可以使用 API 來建立連接至資料來源的集合。

如果您計劃要連接至內部部署資料來源，則需要先安裝 IBM Secure Gateway。如需相關資訊，請參閱[為內部部署資料安裝 IBM Secure Gateway](/docs/services/discovery?topic=discovery-sources#gateway)。 

下列範例使用 SharePoint 資料來源。

1.  使用[來源認證 API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery#create-credentials){: new_window} 來建立您要連接之來源的認證。記錄新建認證的所傳回 **credential_id**。
2.  使用[配置 API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery#add-configuration){: new_window} 來建立新的配置。此配置必須包含一個 **source** 物件來定義要搜索的內容。**source** 物件必須包含您先前記錄的 **credential_id**。
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
    記錄新建配置的所傳回 **configuration_id**。
3.  使用[集合 API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/discovery#create-a-collection){: new_window} 來建立新的集合。定義集合的物件必須包含您先前記錄的 **configuration_id**。

建立集合之後，來源搜索會立即開始，然後再次依照您指定的頻率進行。**附註：**如果您在配置的 **source** 物件中修改任何項目，則會在該時間啟動新搜索（如果已經在執行中，則重新啟動）。

### 指定 `customer_id`
{: #source_customer_id}

可使用所汲取之 {{site.data.keyword.discoveryshort}} 文件的 `customer_id` 欄位，並利用 API 中的 **user-data** 方法，根據 `customer_id` 來刪除內容。汲取時，不會為資料來源中的送入文件自動指派 `customer_id`。如果您的應用程式需要定義 `customer_id`，您可以從要複製的來源系統中，指定一個（或多個）送入欄位作為 `customer_id`。若要這麼做，您必須修改用來連接至來源的配置。

1.  執行範例查詢，並識別您要用來作為 `customer_id` 的欄位。
2.  修改配置。您需要新增**正規化**區段，才能建立 `customer_id` 欄位。
    -  在此工具中，導覽至集合，然後按一下配置區段中的**編輯**鏈結。接下來，按一下**正規化**標籤，然後加入一個**複製**正規化，以建立 `customer_id` 欄位。然後按一下**套用並儲存**。
    ![複製正規化](images/norm_copy.png)
    -  使用 API 時，請將下列物件新增至 **normalizations** 陣列：
       ```json
       {
         "operation" : "copy",
         "source_field" : "{original_field_name}",
         "destination_field" : "customer_id"
       }
       ```
       {: codeblock}
3.  下一個排定的搜索會將 `customer_id` 欄位新增至所有文件。如果您要立即啟動搜索，請修改來源配置（工具中的**同步設定**）。

如需詳細資訊，以及根據 `customer_id` 進行刪除的相關資訊，請參閱[資訊安全](/docs/services/discovery?topic=discovery-information-security#information-security)。

## 為內部部署資料安裝 IBM Secure Gateway 
{: #gateway}

若要連接內部部署資料來源，您需要先下載、安裝並配置 IBM Secure Gateway。為您的第一個內部部署資料來源安裝 IBM Secure Gateway 之後，就不需要再重複此程序。

1.  從 {{site.data.keyword.discoveryshort}} 工具的**管理資料**頁面中，選取**連接資料來源**。
1.  選取您要連接的資料來源。當您選取內部部署資料來源時，請移至**連接至您的內部部署網路**區段，然後按一下**建立連線**按鈕。
1.  在**下載並安裝 Secure Gateway Client** 畫面上，下載適當版本的 IBM Secure Gateway。
1.  完成下載之後，按一下**下載 Secure Gateway 並繼續**按鈕。在安裝期間，您會需要依 Secure Gateway Client 的提示，在在畫面上提供**閘道 ID** 和**記號**。如需安裝指示，請參閱 Secure Gateway 文件中的[安裝用戶端 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/docs/services/SecureGateway/securegateway_install.html#installing-the-client){: new_window}。
1.  在執行 Secure Gateway Client 的機器上，開啟 Secure Gateway 儀表板 (http://localhost:9003)。
1.  按一下儀表板上的**新增 ACL**。將每個 SharePoint 集合的端點 URL 新增至**容許存取**清單。例如，主機名稱：`mycompany.sharepoint.com`，埠：`80`。
1.  回到 {{site.data.keyword.discoveryshort}} 工具，然後按一下**繼續**。如果連線成功，您會看到 `Connection successful`（連線成功）訊息。如果連線失敗，請開啟 Secure Gateway 儀表板，確認**容許存取**清單上的端點正確。

連線成功之後，即可開始輸入內部部署資料來源的認證。

## 資料來源連線和資料隔離
{: #source_isolation}

[連接至外部資料來源](/docs/services/discovery?topic=discovery-sources#sources)會減少服務實例的資料隔離，因為在來源與服務之間轉移的資料無法隔離。所有其他隔離（靜止、管理、查詢）則維持原狀。所有在服務與資料來源之間和之中進行的通訊，都會使用傳輸層安全 (TLS) 1.2 版加密。傳輸層安全 (TLS) 憑證的私密金鑰會使用 AES-256-GCM 進行靜止加密，服務憑證每三年到期，而憑證撤銷清冊為每月更新。所有認證都是透過使用傳輸層安全 (TLS) 1.2 版的加密連線來傳送，並使用 AES-256 進行靜止加密。連接至那些資料來源的連線會使用那些資料來源支援的任何安全通訊協定。
