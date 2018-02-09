---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-30"

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

# Watson Discovery Visual Insights
{: #visual-insights}

{{site.data.keyword.discoveryfull}} Visual Insights 是實驗性特性，您可以利用它來透過視覺化方式探索 {{site.data.keyword.discoveryshort}} 基於對語意元素、關係、概念等等的瞭解所識別的連接。

您可以使用 {{site.data.keyword.discoveryfull}} Visual Insights，先進一步瞭解集合，然後再使用 {{site.data.keyword.discoveryshort}} 來建立查詢，您可以將這些查詢整合到新的應用程式或現有的解決方案中，以便將使用者指向他們需要的資訊。

在實驗性版本期間，只有在公用環境中才能使用 Visual Insights。

**免責聲明：**Visual Insights 是實驗性特性（表示它可能不穩定），可能會經常變更，因此可能一經通知就停止使用。它是為了讓您評估其功能而提供。它可能未提供一般發行功能所提供的相同效能或相容性層次。它並非設計用於正式作業環境，如有這類使用需由您自行承擔風險。如需詳細資料，請參閱[測試版/實驗性特性](/docs/services/discovery/release-notes.html#beta-features)。

## Visual Insights 快速導覽
{: #quick-tour-visual-insights}

![Discovery Visual Insights 快速導覽](images/discovery-visualinsights-quicktour.png)

Visual Insights 畫面分為 4 個主要區域。

### 搜尋列
{: #search-bar}

您可以使用頂端的**搜尋列**來查詢 {{site.data.keyword.discoveryshort}} 集合。

- 如果您已使用 {{site.data.keyword.Bluemix_notm}} 認證登入，即可使用集合下拉清單（依預設為 {{site.data.keyword.discoverynewsfull}}）中與您帳戶相關聯的 {{site.data.keyword.discoveryshort}} 實例的所有集合。如果您未登入，則只能使用 {{site.data.keyword.discoverynewsfull}} 集合。
- 選擇您的集合，在搜尋方框中輸入您的查詢（例如，`What is net neutrality`），然後按一下**搜尋**按鈕來進行搜尋。如果是大型集合，則可能需要一點時間才能顯示結果。您可以按一下 `documents`、`concepts`、`people`、`locations`、`organizations` 或 `companies` 按鈕來過濾搜尋。
- 您可以按一下標頭中的 ![「查詢」圖示](images/discovery-query-icon.png) 圖示，選擇性地選取所顯示結果中的任何項目（實體、概念或文件）。
- 如果已選取專用集合，但尚未輸入任何查詢，則[詳細資料窗格](/docs/services/discovery/visual-insights.html#details-pane)中最多顯示集合中的 1000 份文件。如果已選擇 {{site.data.keyword.discoverynewsshort}} 集合，但未輸入任何查詢，則會顯示 100 篇最近的精選文章。

### 網路顯示畫面
{: #network-display}

搜尋列下方的中央畫面是**「網路」顯示畫面**。這是查詢結果的互動式視覺效果。

- **「網路」顯示畫面**是從查詢結果中擷取的文件、實體及概念的圖形表示法。粉紅色節點代表文件；藍色節點代表實體或概念。每一個文件節點會鏈結到 {{site.data.keyword.discoveryshort}} 在該文件中偵測到的所有實體和概念節點。越類似的文件，在視覺效果上彼此的位置越接近。
- 移至**「網路」顯示畫面**中的任何節點上方，即會顯示其相關聯標題並強調顯示它與其他節點的鏈結。
- 按一下任何節點，會在[詳細資料窗格](/docs/services/discovery/visual-insights.html#details-pane)中顯示該節點的相關資訊。

### 詳細資料窗格
{: #details-pane}

「網路」顯示畫面的右邊是**「詳細資料」窗格**。

- 「詳細資料」窗格提供每一個文件的更多詳細資料，包括其分類及日期（可用的話）、簡短摘錄（含有開啟完整文件的選項），以及其鏈結的實體和概念。
- 如果在「網路」顯示畫面中選取了非文件節點，該節點的相關資訊會顯示在「詳細資料」窗格頂端。
- 按一下「詳細資料」窗格中的任何鏈結的實體或概念，會在「網路」顯示畫面中選取對應的節點。

### 導覽窗格
{: #navigation-pane}

「網路」顯示畫面的左邊是**「導覽」窗格**。此窗格提供從所選擇集合之查詢結果中擷取的最常用詞彙的標籤雲概觀。詞彙越長，它在查詢結果中越常見。

- 在標籤雲中選取任何詞彙會使它變成粉紅色，而且會在「網路」顯示畫面中強調顯示與它相關聯的任何文件。「詳細資料」窗格將顯示所強調顯示的文件清單。標籤雲中的其他詞彙現在指出其與所選取詞彙之間的關係：
  - 變成灰色的詞彙與任何強調顯示的文件均無關聯。
  - 如果某個詞彙變成紫色，則它與所有強調顯示的文件都有關聯，對於嘗試區分文件沒有幫助。
  - 剩餘的藍色詞彙與部分（但非全部）強調顯示的文件相關聯，因此可用來進一步精簡強調顯示的文件集。選取其中一個詞彙，會使強調顯示的文件集縮減為只與這兩個標籤相關聯的文件，並將網路顯示畫面縮小成那些文件所在的區域。此方法可以用來將大型文件集精簡成小型文件集，您只要按幾下滑鼠即可。
- 若要取消選取已選取的詞彙，請再次按一下該詞彙。若要清除所有已選取的詞彙，請按一下標籤雲中這兩個單字之間的空白點。按一下灰色標籤將會清除現有的選擇，並選取該詞彙。
- 文件、人員、概念、組織、位置及公司的類型及計數會顯示在標籤雲上方。按一下其中任何一個可過濾標籤雲和「網路」顯示畫面視覺效果。

## 使用 Visual Insights
{: #using-visual-insights}

您可以使用 Visual Insights 來查詢 {{site.data.keyword.discoverynewsfull}}，而不需要登入。若要將 Visual Insights 與您的專屬集合搭配使用，您將需要：

- 包含 {{site.data.keyword.discoveryshort}} 實例的 {{site.data.keyword.Bluemix_notm}} 帳戶。
- 該 {{site.data.keyword.discoveryshort}} 實例中已使用[實體擷取](/docs/services/discovery/building.html#entity-extraction)強化，以及選擇性地加上任何[概念標記](/docs/services/discovery/building.html#concept-tagging)、[關鍵字擷取](/docs/services/discovery/building.html#keyword-extraction)、[關係擷取](/docs/services/discovery/building.html#relation-extraction)及[種類分類](/docs/services/discovery/building.html#category-classification)強化來強化的一個以上集合。還可包含其他強化，但不會由 Visual Insights 表示。

如需 {{site.data.keyword.discoveryshort}} 以及如何免費開始使用它的相關資訊，請參閱 [Watson {{site.data.keyword.discoveryshort}} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/watson/services/discovery/){: new_window}。

有了 {{site.data.keyword.Bluemix_notm}} 帳戶、{{site.data.keyword.discoveryshort}} 實例及移入一個以上的集合之後，當您登入時就會在 Visual Insights 中看到集合。

登入 Visual Insights

1. 開啟 [{{site.data.keyword.discoveryshort}} Visual Insights ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://visual-insights.bluemix.net){: new_window}。
1. 按一下「搜尋」列中的 ![「設定檔」圖示](images/discovery-profile-icon.png) 圖示。
1. 輸入您的 {{site.data.keyword.Bluemix_notm}} ID 和密碼。稍後，您的集合將出現在「搜尋」列中供您選取。

## 提供意見
{: #providing-feedback}

我們想知道您對 {{site.data.keyword.discoveryshort}} Visual Insights 的意見。若要存取意見鏈結，請按一下標頭中的 ![「資訊」圖示](images/discovery-info-icon.png) 圖示。
