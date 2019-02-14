---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-26"

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

# 資訊安全
{: #information-security}

IBM 致力於為我們的客戶及合作夥伴提供創新的資料隱私權、安全及控管解決方案。
{: shortdesc}

**注意事項：**客戶須負責確定本身遵循各種法令規章，包括歐盟的「一般資料保護規範」。有關任何可能影響「客戶」業務之相關法令規章之確認與解釋，以及任何「客戶」為遵循該等法令規章所需採取之行動，「客戶」應自行負責向法律顧問取得諮詢意見。

本文所述的產品、服務及其他功能並不適合所有客戶情況，並且可用性可能受到限制。IBM 不提供法律、會計或審核意見，亦不聲明或保證其服務或產品可確保「客戶」符合任何法令規章。

如果您需要針對建立的 {{site.data.keyword.cloud}} {{site.data.keyword.watson}} 資源要求 GDPR 支援

-   在歐盟 (EU)，請參閱[要求在歐盟建立之 IBM Cloud Watson 資源的支援](/docs/services/watson/getting-started-gdpr-sar.html#request-EU)。
-   在歐盟以外地區，請參閱[要求歐盟以外資源的支援](/docs/services/watson/getting-started-gdpr-sar.html#request-non-EU)。

## 歐盟一般資料保護規範 (GDPR)
{: #gdpr}

IBM 致力於為我們的客戶及合作夥伴提供創新的資料隱私權、安全及控管解決方案，以協助他們邁向 GDPR 法規遵循。

在[這裡 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/gdpr){: new_window} 可進一步瞭解 IBM 本身的 GDPR 準備過程，以及我們支援您邁向法規遵循的 GDPR 功能及供應項目。

## 在 {{site.data.keyword.discoveryshort}} 中標示及刪除資料
{: #gdpr-discovery}

{{site.data.keyword.discoveryshort}} 服務包含一個 API，以在每個呼叫中標示資料。

使用此 API，您可以：

- 利用客戶 ID 標示資料。
- 刪除特定客戶 ID 的所有資料，包括相關注意事項。

資料的標示方式是將您選擇的 `customer_id`（請參閱[如何標示資料](/docs/services/discovery/information-security.html#labeling)中的限制）新增至選用性的 `X-Watson-Metadata` 標頭。然後，{{site.data.keyword.discoveryshort}} 便可以依照 `customer_id` 來刪除它。

在任何 REST 呼叫上，可以使用分號區隔的 `field=value` 配對來傳送選用性標頭 `X-Watson-Metadata`，該處目前僅持續保存 `customer_id`。透過在 `X-Watson-Metadata` 標頭中新增該 `customer_id`，要求指出它包含屬於這個 `customer_id` 的資料。

在單一 {{site.data.keyword.discoveryshort}} 服務實例內，`customer_id` 是唯一的。它們在每個環境或集合中「不是」唯一的。它們不應包含個人資料。

**附註：**實驗性及測試版特性不適用於正式作業環境，因此，在標示及刪除資料時，不保證如預期般運作。在實作需要標示及刪除資料的解決方案時，不應使用實驗性及測試版特性。

## 支援標示資料的方法
{: #pi_methods}

如果在最初使用相關聯方法新增資訊時指定了 `customer_id`，則可以使用 `customer_id` 來刪除下列儲存的資訊：

- 查詢 (`/v1/environments/{environment_id}/collections/{collection_id}/query`) 僅與 `passages` 或 `natural_language_query` 參數一起使用
- 事件 (`/v1/events`)
- 文件 (`/v1/environments/{environment_id}/collections/{collection_id}/documents`)
- 注意事項 (`/v1/environments/{environment_id}/collections/{collection_id}/notices`) 僅標示汲取 `notices`。
- 「知識圖」實體 (`/v1/environments/{environment_id}/collections/{collection_id}/query_entities`)
- 「知識圖」關係 (`/v1/environments/{environment_id}/collections/{collection_id}/query_relations`)
- 訓練資料 (`/v1/environments/{environment_id}/collections/{collection_id}/training_data`)

下列儲存的資訊並未明確標示，因而無法透過指定 `customer_id` 加以刪除。在這些欄位中不支援個人資料。

下列已儲存項目的任何字串欄位（包括但不限於 `name` 和 `description`）：
- 配置
- 集合
- 環境

## 標示資料
{: #labeling}

在汲取文件時，請使用 `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` 或 `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/ID` 作業來包含 `X-Watson-Metadata` 標頭。`customer_id` 欄位會新增至文件的 `extracted_metadata`。執行任何作業時，您的應用程式應該配置為在 `X-Watson-Metadata` 標頭中提供 `customer_id`。

您可以選擇性地在 `customer_id` 欄位中包含 `metadata` 多組件表單組件，而不使用 `X-Watson-Metadata` 標頭。

**附註：**如果已汲取文件，您必須重新汲取它們，才能新增 `X-Watson-Metadata` 標頭和 `customer_id`。

**附註：**如果您在 `metadata` 多組件表單組件「以及」相同文件的 `X-Watson-Metadata` 標頭中指定 `customer_id`，則會使用 `X-Watson-Metadata` 標頭中的 `customer_id`。

限制：

- `X-Watson-Metadata` 標頭的值不能超過 4 KB 的文字。
- `X-Watson-Metadata` 標頭必須包含以分號區隔的 `field=value` 配對清單。`field` 和 `value` 不得包含分號 (`;`) 或等號 (`=`)。
- `customer_id` 在每個 {{site.data.keyword.discoveryshort}} 實例內是唯一的。它們在每個環境或集合中「不是」唯一的。
- `customer_id` 的長度不能超過 256 個字元。
- 如果 `customer_id` 只包含空格或完全是空的，則會視為完全沒有提供 `customer_id`，且不會傳回任何錯誤訊息。

### 使用 Discovery 工具標示資料
{: #labelingtooling}

使用 {{site.data.keyword.discoveryshort}} 工具時，可以使用 `customer_id` 欄位來標示資料。請按一下 ![齒輪](images/icon_settings.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->，並在 **GDPR 資料標籤**欄位中輸入 `customer_id`。設定此欄位之後，使用此瀏覽器階段作業上傳的所有資料，都將以指定的 `customer_id` 標示，若相關聯的客戶 ID 變更，則必須手動變更此欄位。

使用 **GDPR 資料標籤**欄位新增 `customer_id`，將會標示該 URL 網域內此後的文件、注意事項、「知識圖」實體、「知識圖」關係及訓練資料，包括該網域下的每個實例。新增 **GDPR 資料標籤**欄位之前，在 {{site.data.keyword.discoveryshort}} 工具中發生的任何動作（包括文件上傳）都不會予以標示。

**附註：**如果您在使用 {{site.data.keyword.discoveryshort}} 工具的 **GDPR 資料標籤**欄位指定 `customer_id` 之後，切換網域、瀏覽器、清空瀏覽器快取，或啟動匿名 (incognito) 階段作業，則不會保留 `customer_id`，且不會標示您的資料。如果您必須切換網域或瀏覽器，請在 **GDPR 資料標籤**欄位中重新輸入 `customer_id`。

### 使用資料搜索器標示文件
{: #labelingdc}

如果已使用「資料搜索器」來搜索任何文件，您需要重新搜索它們，才能新增 `X-Watson-Metadata` 標頭和 `customer_id`。

1. 更新 {{site.data.keyword.discoveryshort}} 資料搜索器輸出配接器配置，以包含 `customer_id`。請參閱[配置輸出配接器](/docs/services/discovery/data-crawler-discovery.html#output-adapter)。
1. 排定搜索。文件會使用 `X-Watson-Metadata` 標頭提交至 {{site.data.keyword.discoveryshort}}，且文件會以所配置的 `customer_id` 來標示。

## 刪除標示的資料
{: #deletingdata}

資料必須以 `customer_id` 進行標示，之後才能刪除它。

1. 使用 `DELETE /v1/user_data` 作業，並提供您要刪除之資料的 `customer_id`。`DELETE /v1/user_data` 會刪除與該服務實例內的特定 `customer_id` 相關聯的所有資料，如[支援標示資料的方法](/docs/services/discovery/information-security.html#pi_methods)中所指定。另請參閱 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html#delete-user-data){: new_window}

刪除以非同步的方式執行。您無法追蹤刪除的進度。

如果提供不存在的 `customer_id`，將不會刪除任何內容，但會傳回 `200 - OK` 回應。

環境和集合不會以 `customer_id` 進行標示，即使在建立環境或集合的要求中包含 `X-Watson-Metadata` 標頭也一樣。只會標示環境內或集合內的個別文件。因此，在刪除資料時，「不會」刪除個別環境和集合。

您無法使用 {{site.data.keyword.discoveryshort}} 工具來刪除已標示的資料。
