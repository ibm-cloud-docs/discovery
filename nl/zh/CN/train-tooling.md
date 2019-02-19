---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-06"

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

在 {{site.data.keyword.discoveryfull}} 服务中，自然语言查询结果的相关性可以通过训练来改进。您可以使用 {{site.data.keyword.discoveryshort}} 工具或 {{site.data.keyword.discoveryshort}} API 来训练专用集合。如果您希望使用 API，请参阅[使用 API 改进查询结果的相关性](/docs/services/discovery/train.html)。
{: shortdesc}

相关性训练是可选的；如果查询结果满足您的需求，那么没必要进一步训练。有关构建用例进行训练的概述，请参阅博客帖子 [How to get the most out of Relevancy Training ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/dwblog/2017/get-relevancy-training/){: new_window}。

为了训练 Watson，您需要：

  -   提供能代表您的用户所输入查询的示例查询；
  -   提供评级，以说明每个查询的哪些结果相关，哪些不相关

一旦 Watson 有足够的训练输入后，您提供的关于每个查询的哪些结果好以及哪些结果差的信息将用于了解有关集合的信息。Watson 不仅仅记住这些信息，还会从有关各个查询的特定信息进行学习，并将检测到的模式应用于所有新查询。它通过机器学习 Watson 方法在您的内容和问题中查找信号，从而实现这一点。应用训练后，{{site.data.keyword.discoveryshort}} 会对查询结果重新排序，使最相关的结果显示在最前。随着添加的训练数据越来越多，{{site.data.keyword.discoveryshort}} 的查询结果排序应该会更准确。

**注：**目前，相关性训练仅适用于专用集合中的自然语言查询。它不适用于结构化的 {{site.data.keyword.discoveryshort}} Query Language 查询。有关 {{site.data.keyword.discoveryshort}} Query Language 的更多信息，请参阅[查询概念](/docs/services/discovery/using.html)。

已训练的集合将在自然语言查询的结果中返回 `confidence` 分数。请参阅[置信度分数](/docs/services/discovery/train-tooling.html#confidence)以获取详细信息。

请参阅[训练数据需求](/docs/services/discovery/train.html#reqs)，以了解训练的最低需求以及训练限制。

请参阅[使用情况监视](/docs/services/discovery/feedback.html)，以获取有关跟踪使用情况以及使用这些数据帮助您了解和改进应用程序的详细信息。

## 添加查询并对结果相关性评级
{: #results}

训练由以下三部分组成：自然语言查询、查询结果以及应用于这些结果的评级。

1.  有两种方法可以访问 {{site.data.keyword.discoveryshort}} 工具中的训练页面：
    - 对于单个集合，在**构建查询**屏幕上，单击右上角的**训练 Watson 以改进结果**。无需在**构建查询**屏幕上输入查询来启动训练。 
    - 在性能仪表板中。单击左侧的**查看数据度量值**图标以打开该仪表板。系统将提示您选择要训练的集合。
1.  在**训练 Watson** 屏幕上，单击**添加自然语言查询**并添加查询，例如：“IBM Watson in healthcare”。请确保按照用户提问的方式编写查询。此外，还应使用查询与期望答案之间的某些项重叠来编写训练查询。这将在运行自然语言查询时改进初始结果。相关性训练仅使用自然语言查询，不要输入使用 {{site.data.keyword.discoveryshort}} Query Language 编写的查询。
1.  要查看查询的结果，请单击其旁边的**结果评级**按钮。如果您认为结果不够，可以尝试重写查询，或者通过**管理数据**屏幕将更多文档添加到此集合。
1.  开始将结果评级为`相关`或`不相关`。完成后，单击**返回到查询**。在 {{site.data.keyword.discoveryshort}} 工具中，`相关性`的分数为 `10`，`不相关`的分数为 `0`。如果已使用 API 开始对此集合的结果评级，但使用的评分量程不同，那么将显示警告，其中包含用于修正此问题的选项。在屏幕顶部，Watson 会跟踪训练状态，并提供有关可执行哪些操作来改进结果的技巧。“向评级添加更多变化”表示您应该同时使用`相关`和`不相关`评级。满足需求后，训练将定期启动更新。更新开始到完成需要的时间不超过 30 分钟；在 Watson 更新时，您可以继续工作。
1.  继续添加查询和对结果评级。

要随时返回到**构建查询**主屏幕，请单击左上角的**构建查询**。
{: tip}
要返回到**管理数据**屏幕，请单击右上角的集合名称。
{: tip}

如果您希望一次性删除集合中的所有训练数据，那么必须通过 API 来执行此操作。请参阅[删除集合的所有训练数据](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-all-training-data)，以获取更多信息。有关通过 API 进行训练的更多信息，请参阅[使用 API 改进查询结果的相关性](/docs/services/discovery/train.html)。

## 对结果相关性进行测试和迭代

完成对结果的评级并且 Watson 已应用训练后，您应该进行测试以查看查询结果是否已改进。要执行此操作，请运行与训练查询相关（但不完全相同）的测试查询。检查以确认测试查询的结果是否已改进。

如果您希望在测试后进一步改进结果，那么可以执行以下操作：
- 向集合添加更多文档。
- 添加更多训练查询。
- 对更多结果评级，并确保同时使用`相关`和`不相关`评级。

有关其他训练指导信息，请参阅[相关性训练技巧](/docs/services/discovery/train-tips.html#relevancy-tips)。

## 置信度分数
{: #confidence}

已训练的集合将在自然语言查询的结果中返回 `confidence` 分数。此 `confidence` 数字是根据结果相对于已训练模型的估计相关性来计算的。`confidence` 分数与 `score` **不同**。有关确定置信度分数阈值的更多信息，请参阅 [How to select a threshold for acting using confidence scores ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/watson/blog/2016/06/23/how-to-select-a-threshold-for-acting-using-confidence-scores/)。`score` 是相对计算，因此不应该用于设置绝对阈值。

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

**注：**只有成功完成相关性训练后，才会返回 `confidence` 字段。还可能存在已训练模型不可用，因而不返回 `confidence` 字段的情况。 

例如，如果引入新的顶级字段，或者由于摄取了具有不同模式的新文档而在其他方面更改了集合的模式，那么已训练的模型将暂时变为无效。在该场景中，返回的结果中不会包含 `confidence`，并且在模型自动进行重新训练并再次可用之前，结果将来自缺省的未训练搜索。在重新训练期间，不会返回 `confidence`。

对于使用 `confidence` 作为阈值的应用程序，应确保这些应用程序能够处理这些场景。由于 `score` 是相对于查询的，因此建议不要将其用作固定阈值。相反，我们建议应用程序始终对不包含 `confidence` 字段的所有结果执行相同的行为。例如，应用程序可显示不包含 `confidence` 字段的所有结果或隐藏不包含 `confidence` 字段的所有结果，但不应使用 `score` 值来显示一些结果而隐藏其他结果。
