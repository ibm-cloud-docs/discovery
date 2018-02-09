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

# 疑難排解

使用 {{site.data.keyword.discoveryshort}} 服務的疑難排解提示。

如果您在使用 {{site.data.keyword.discoveryshort}} 服務時發生問題，請嘗試使用下列一個以上的疑難排解提示。

-   無法汲取文件，因為現行文件中的資料與先前所汲取文件中的類似資料之間有類型不符的情形。例如，在一份文件中的某個欄位可能輸入為**日期**，但在後續文件中卻輸入為**字串**，而導致後續文件無法正確進行檢索。

    預覽作業無法預測類型不符的情形，因為它只會測試單一文件，而且不會保留轉換結果的記錄。
-   快速或大規模的文件檢索有時候可能會導致後端搜尋服務重新啟動。如果發生此情況，請聯絡 {{site.data.keyword.IBM}} 支援人員以尋求協助。
