---

copyright:
  years: 2015, 2017
lastupdated: "2017-12-05"

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

# 使用工具改进结果相关性

在 {{site.data.keyword.discoveryfull}} 服务中，自然语言查询结果的相关性可以通过培训来改进。您可以使用 {{site.data.keyword.discoveryshort}} 工具或 {{site.data.keyword.discoveryshort}} API 来培训专用集合。如果您希望使用 API，请参阅[使用 API 改进查询结果的相关性](/docs/services/discovery/train.html)。
{: shortdesc}

相关性培训是可选的；如果查询结果满足您的需求，那么没必要进一步培训。有关构建用例进行培训的概述，请参阅博客帖子 [How to get the bost out of Relevance Training ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/dwblog/2017/get-relevancy-training/){: new_window}。

为了培训 Watson，您需要：

  -   提供能代表您的用户所输入查询的示例查询；
  -   提供评级，以说明每个查询的哪些结果相关，哪些不相关

一旦 Watson 有足够的培训输入后，您提供的关于每个查询的哪些结果好以及哪些结果差的信息将用于了解有关集合的信息。Watson 不仅仅记住这些信息，还会从有关各个查询的特定信息进行学习，并将检测到的模式应用于所有新查询。它通过机器学习 Watson 方法在您的内容和问题中查找信号，从而实现这一点。应用培训后，{{site.data.keyword.discoveryshort}} 会对查询结果重新排序，使最相关的结果显示在最前。随着添加的培训数据越来越多，{{site.data.keyword.discoveryshort}} 的查询结果排序应该会更准确。

培训必须满足 {{site.data.keyword.discoveryshort}} 的以下**最低**需求才可开始应用您的评级：

  - 必须至少培训 49 个查询，甚至可能更多。如果 Watson 需要更多查询才能执行培训，它会提供相应反馈。
  - 应该将两个可用的评级都应用于结果：`相关`和`不相关`。仅对`相关`文档进行评级不会提供所需的数据。

**注：**相关性培训需要满足特定培训数据需求才能生效。服务会定期检查培训数据以确定是否满足这些需求，并自动根据任何更改来更新自身。

**注：**目前，相关性培训仅适用于专用集合中的自然语言查询。它不适用于结构化的 {{site.data.keyword.discoveryshort}} Query Language 查询。有关 {{site.data.keyword.discoveryshort}} Query Language 的更多信息，请参阅[查询概念](/docs/services/discovery/using.html)。

**注：**每个环境最多可有 4 个经过培训的集合。  

## 添加查询并对结果相关性评级

培训由以下三部分组成：自然语言查询、查询结果以及应用于这些结果的评级。

1.  在 {{site.data.keyword.discoveryshort}} 工具中，可以在**构建查询**屏幕中访问集合的培训页面。单击右上角的**培训 Watson 以改进结果**。无需在**构建查询**屏幕上输入查询来启动培训。
1.  在**培训 Watson** 屏幕上，单击**添加自然语言查询**并添加查询，例如：“IBM Watson in healthcare”。请确保按照用户提问的方式编写查询。此外，还应使用查询与期望答案之间的某些项重叠来编写培训查询。这将在运行自然语言查询时改进初始结果。相关性培训仅使用自然语言查询，不要输入使用 {{site.data.keyword.discoveryshort}} Query Language 编写的查询。
1.  要查看查询的结果，请单击其旁边的**结果评级**按钮。如果您认为结果不够，可以尝试重写查询，或者通过**管理数据**屏幕将更多文档添加到此集合。
1.  开始将结果评级为`相关`或`不相关`。完成后，单击**返回到查询**。在 {{site.data.keyword.discoveryshort}} 工具中，`相关性`的分数为 `10`，`不相关`的分数为 `0`。如果已使用 API 开始对此集合的结果评级，但使用的评分量程不同，那么将显示警告，其中包含用于修正此问题的选项。在屏幕顶部，Watson 会跟踪培训状态，并提供有关可执行哪些操作来改进结果的技巧。“向评级添加更多变化”表示您应该同时使用`相关`和`不相关`评级。满足需求后，培训将定期启动更新。更新开始到完成需要的时间不超过 30 分钟；在 Watson 更新时，您可以继续工作。
1.  继续添加查询和对结果评级。

要随时返回到**构建查询**主屏幕，请单击左上角的**构建查询**。
{: tip}
要返回到**管理数据**屏幕，请单击右上角的集合名称。
{: tip}

如果您希望一次性删除集合中的所有培训数据，那么必须通过 API 来执行此操作。请参阅[删除集合的所有培训数据](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-all-training-data)，以获取更多信息。有关通过 API 进行培训的更多信息，请参阅[使用 API 改进查询结果的相关性](/docs/services/discovery/train.html)。

## 对结果相关性进行测试和迭代

完成对结果的评级并且 Watson 已应用培训后，您应该进行测试以查看查询结果是否已改进。要执行此操作，请运行与培训查询相关（但不完全相同）的测试查询。检查以确认测试查询的结果是否已改进。

如果您希望在测试后进一步改进结果，那么可以执行以下操作：
- 向集合添加更多文档。
- 添加更多培训查询。
- 对更多结果评级，并确保同时使用`相关`和`不相关`评级。

有关其他培训指导信息，请参阅[相关性培训技巧](/docs/services/discovery/train-tips.html#relevancy-tips)。

## 置信度分数
{: #confidence}

已培训的集合将在自然语言查询的结果中返回 `confidence` 分数。此 `confidence` 数字是根据结果相对于已培训模型的估计相关性来计算的。`confidence` 分数与 `score` **不同**。有关确定置信度分数阈值的更多信息，请参阅 [How to select a threshold for acting using confidence scores ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/watson/blog/2016/06/23/how-to-select-a-threshold-for-acting-using-confidence-scores/)。`score` 是相对计算，因此不应该用于设置绝对阈值。

`confidence` 的范围可以从 0.0 到 1.0。数字越大，文档相关性越高。

`confidence` 分数可以在查询结果中每个文档的 `result_metadata` 下找到，例如：

```json
    "results": [
        {
            "id": "eea16dfd5fe6139a25324e7481a32f89_13",
            "result_metadata": {
                "confidence": 0.5893963975910735,
                "score": 0.5006834
            },
```
