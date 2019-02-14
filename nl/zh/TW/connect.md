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

# 連接至資料來源
{: #sources}

{{site.data.keyword.discoveryshort}} 服務可讓您從遠端來源連接至文件並搜索文件。
{: shortdesc}

您可以配置集合來建立與資料來源的關聯，藉以連接至該資料來源，並（視需要）依排程將文件取回到 {{site.data.keyword.discoveryshort}} 服務。每個集合都可以使用一個資料來源進行配置。{{site.data.keyword.discoveryshort}} 服務使用一個稱為「搜索」的處理程序，從資料來源取回文件。搜索是指系統性地從指定之開始位置瀏覽及擷取文件的處理程序。只有您明確指定的項目，{{site.data.keyword.discoveryshort}} 服務才會加以搜索。可以搜索的資料來源類型如下：

-  [Box](/docs/services/discovery/connect.html#connectbox)
-  [Salesforce](/docs/services/discovery/connect.html#connectsf)
-  [Microsoft SharePoint Online](/docs/services/discovery/connect.html#connectsp)

您可以使用 {{site.data.keyword.discoveryshort}} 工具或 API 來連接至資料來源。{{site.data.keyword.discoveryshort}} 工具提供的簡化連線方法不需要太瞭解來源系統，而 API 則提供更精細且可高度配置的介面，這需要對您所要連接的來源有較深入的瞭解。下列處理程序概觀可讓您知道接下來要閱讀本文件的哪幾節：

1.  閱讀[一般來源需求](/docs/services/discovery/connect.html#gen_req)，可大概瞭解您需要哪些項目。
2.  閱讀來源系統的特定需求：
    -  [Box](/docs/services/discovery/connect.html#connectbox)
    -  [Salesforce](/docs/services/discovery/connect.html#connectsf)
    -  [Microsoft SharePoint Online](/docs/services/discovery/connect.html#connectsp)
3.  根據您的配置選項，閱讀來源配置指示：
    -  [使用工具](/docs/services/discovery/connect.html#source_tooling)
    -  [使用 API](/docs/services/discovery/connect.html#source_api)

## 一般來源需求
{: #gen_req}

下列一般需求適用於所有資料來源：

-  Box、Salesforce 及 SharePoint Online 的個別文件檔案大小限制為 10MB。
-  您將需要每一個資料來源的認證和檔案位置（或 URL），這些通常是由資料來源的開發人員/系統管理者提供。
-  您需要知道要搜索資料來源的哪些資源。這可以由來源管理者提供。如果是搜索 Box 或 Salesforce，則在使用 {{site.data.keyword.discoveryshort}} 工具配置來源時會出現一份可用的資源清單。
-  搜索資料來源將使用資料來源的資源（API 呼叫）。呼叫次數取決於搜索的文件數目。必須取得資料來源的適當服務層級（例如「企業」），且必須諮詢來源系統管理者。
-  {{site.data.keyword.discoveryshort}} 可汲取下列檔案類型，並且會忽略所有其他類型的文件：
   -  Microsoft Word
   -  PDF
   -  HTML
   -  JSON
-  {{site.data.keyword.discoveryshort}} 來源搜索不會刪除已儲存在集合中的文件。重新搜索來源時，會新增新的文件、將已更新的文件修改為現行版本，而已刪除的文件則會保留為前次儲存的版本。

## Box
{: #connectbox}

連接至 Box 來源時，請確定您計劃要連接的實例是「企業」方案或更高版本。

設定 Box 帳戶以使用 {{site.data.keyword.discoveryshort}}：

1.  在 `https://app.box.com/developers/console`（請使用貴公司的 Box URL）中建立新的 Box 自訂應用程式。
1.  然後執行下列其中一項：
    - 選取 `Enterprise` 作為 **Application access**，然後使用現有的受管理使用者繼續進行。或者
    - 選取 `Application` 作為 **Application access**，然後使用 [Box API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.box.com/reference#create-app-user){: new_window}，以新建的應用程式建立 `Application User`。
1.  啟用下列 **Application Scopes**：
    - `Read and Write All Folders Stored In Box`
    - `Manage Users`
1.  啟用下列 **Advanced Features**
    - `Perform Actions as Users`
    - `Generate User Access Tokens`
1.  透過將來自 `https://app.box.com/developers/console` 的 `Client ID` 輸入到 `API Key` 欄位，讓管理者授權您的應用程式用戶端 ID `https://app.box.com/master/settings/openbox`。
1.  產生 `public/private keypair`（將下載到您的電腦）。
1.  開啟下載的檔案，然後將欄位複製/貼上至 {{site.data.keyword.discoveryshort}}。當複製到 {{site.data.keyword.discoveryshort}} 時，移除 `privateKey` 尾端的尾端換行字元 `\n`。

**附註：**{{site.data.keyword.discoveryshort}} 不支援自訂應用程式以自己的身分進行搜索（您不能假冒自己）。 

需要下列認證才能連接至 Box 來源，應該向您的 Box 管理者取得認證（除非您已使用先前的步驟設定 Box 自訂應用程式而取得它們）：

-  `client_id` - 這些認證所連接來源的 `client_id`。    
-  `enterprise_id` - 這些認證所連接 Box 網站的 `enterprise_id`。
-  `client_secret` - 這些認證所連接來源的 `client_secret`。絕不會傳回此值，而且只有在建立或修改認證時才會使用此值。
-  `public_key_id` - 這些認證所連接來源的 `public_key_id`。絕不會傳回此值，而且只有在建立或修改認證時才會使用此值。
-  `private_key` - 這些認證所連接來源的 `private_key`。絕不會傳回此值，而且只有在建立或修改認證時才會使用此值。
-  `passphrase` - 這些認證所連接來源的 `passphrase`。絕不會傳回此值，而且只有在建立或修改認證時才會使用此值。

識別認證時，參考 [Box 開發人員文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.box.com/){: new_window} 可能有幫助。

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
-  `site_collection.path` - 這些認證所連接來源的 `site_collection.path`。
-  `username` - 這些認證所連接來源的 `client_id`。
-  `password` - 這些認證所連接來源的 `password`。絕不會傳回此值，而且只有在建立或修改認證時才會使用此值。

識別認證時，參考 [Microsoft SharePoint 開發人員文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.microsoft.com/en-us/sharepoint/dev/){: new_window} 可能有幫助。

搜索 Microsoft SharePoint Online 時要注意的其他項目：

-  搜索 SharePoint 時，您需要有一份清單，列出您要搜索的 SharePoint 網站集合路徑。{{site.data.keyword.discoveryshort}} 工具可讓您瀏覽並選取要搜索的內容。若要搜索整個 SharePoint Online 網站，請勿在此欄位中選取多個路徑 (URL)。在該情境下，請於 `site_collection.path` 欄位中輸入 `/`。

## 使用工具
{: #source_tooling}

使用 {{site.data.keyword.discoveryshort}} 工具連接至資料來源時，需要特別為來源建立集合來執行。執行下列步驟以建立來源集合並對其進行搜索：

1.  從 {{site.data.keyword.discoveryshort}} 工具的**管理資料**頁面中，選取**連接資料來源**。
2.  選取您要連接的資料來源。
3.  輸入您的來源認證，然後按一下「連接」。必須向來源系統管理者取得您的來源認證。
4.  選擇您要搜索的資料及其同步頻率。
5.  按一下**儲存 & 同步物件**，開始搜索您的資料來源。然後，系統會將您重新導向至集合狀態畫面，當文件新增至集合時此畫面就會更新。

搜索一開始會使資料同步，然後依照您指定的頻率進行同步。**附註：**如果您在**同步設定**畫面中修改任何項目，然後按一下**儲存並同步物件**，則會在該時間啟動搜索（如果已經在執行，則重新啟動）。

## 使用 API
{: #source_api}

使用下列處理程序，可以使用 API 來建立連接至資料來源的集合。
1.  使用[來源認證 API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#credentials-api){: new_window} 來建立您要連接之來源的認證。記錄新建認證的所傳回 **credential_id**。
2.  使用[配置 API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#configurations-api){: new_window} 來建立新的配置。此配置必須包含一個 **source** 物件來定義要搜索的內容。**source** 物件必須包含您先前記錄的 **credential_id**。
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
3.  使用[集合 API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#configurations-api){: new_window} 來建立新的集合。定義集合的物件必須包含您先前記錄的 **configuration_id**。

建立集合之後，來源搜索會立即開始，然後再次依照您指定的頻率進行。**附註：**如果您在配置的 **source** 物件中修改任何項目，則會在該時間啟動新搜索（如果已經在執行中，則重新啟動）。

## 指定 `customer_id`
{:# source_customer_id}

可使用所汲取之 {{site.data.keyword.discoveryshort}} 文件的 `customer_id` 欄位，並利用 API 中的 **user-data** 方法，根據 `customer_id` 來刪除內容。汲取時，不會為資料來源中的送入文件自動指派 `customer_id`。如果您的應用程式需要定義 `customer_id`，您可以從要複製的來源系統中，指定一個（或多個）送入欄位作為 `customer_id`。若要這麼做，您必須修改用來連接至來源的配置。

1.  執行範例查詢，並識別您要用來作為 `customer_id` 的欄位。
2.  修改配置。您需要新增**正規化**區段，才能建立 `customer_id` 欄位。
    -  在此工具中，導覽至集合，然後按一下配置區段中的**編輯**鏈結。接下來，按一下**正規化**標籤，然後加入一個**複製**正規化，以建立 `customer_id` 欄位。然後按一下**套用並儲存**。
    ![複製正規化](images/norm_copy.png)
    -  使用 API 時，請將下列物件新增至 **noramizations** 陣列
       ```json
       {
         "operation" : "copy",
         "source_field" : "{original_field_name}",
         "destination_field" : "customer_id"
       }
       ```
       {: codeblock}
3.  下一個排定的搜索會將 `customer_id` 欄位新增至所有文件。如果您要立即啟動搜索，請修改來源配置（工具中的**同步設定**）。

如需相關資訊及根據 `customer_id` 進行刪除的相關資訊，請參閱[資訊安全 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.bluemix.net/docs/services/discovery/information-security.html){: new_window}。
