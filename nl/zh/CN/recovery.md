---

copyright:
  years: 2019
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

# 高可用性和灾难恢复
{: #recovery}

{{site.data.keyword.discoveryfull}} 支持无单点故障的高可用性。此外，客户需要履行的职责是备份您的 {{site.data.keyword.discoveryshort}} 数据以支持您自己的灾难恢复计划，以便您可以重新创建服务。
{: shortdesc}

{{site.data.keyword.discoveryshort}} 流量在一个区域中的多个专区中进行负载均衡。每个专区都是同一区域中的一个数据中心。请参阅[如何确保停机时间为零？![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/docs/overview?topic=overview-zero-downtime#zero-downtime){: new_window} 以获取更多信息。

## 备份 Watson Discovery 中的数据
{: #backup}

有多种方法可用于备份 {{site.data.keyword.discoveryfull}} 中存储的数据。这些方法应包含在您的灾难恢复计划中。

-  您应保留副本的数据，如源文档
-  由 {{site.data.keyword.discoveryshort}} 存储并且您应抽取和备份的数据
  
有些数据将需要从头开始重新创建（例如，您无法备份的数据，如反馈事件）。 

### 摄入的文档
{: #backupdocs}

您上传的文档将进行转换和扩充，然后存储到搜索索引中。发生灾难时，搜索索引不可恢复，因此您应将所有源文档的备份存储到安全的位置。

如果还通过对外部数据源执行已安排的搜寻来导入文档，您应在外部保留您的数据源凭证，以便能够快速重新建立数据源。请参阅[连接到数据源](/docs/services/discovery?topic=discovery-sources#sources)，以获取可用源的列表以及每个‘源需要的凭证。

### 配置
{: #backupconfigs}

您应备份实例配置，并将其存储到本地位置，以防发生灾难事件。 

要备份这些配置，请首先针对每个实例[列出配置](https://cloud.ibm.com/apidocs/discovery#list-configurations)。 

获取配置列表后，针对每个配置[获取详细信息](https://cloud.ibm.com/apidocs/discovery#get-configuration-details)。

### 训练数据
{: #backuptraining}

您应为每个经过训练的集合备份训练数据，并将其存储到本地位置，以防发生灾难事件。 

训练数据用于对集合进行显式训练，并逐个集合进行存储。 

要抽取训练数据，请使用 API 从 {{site.data.keyword.discoveryshort}} 下载查询和评级。 

1.  [列出训练数据](https://cloud.ibm.com/apidocs/discovery#list-training-data)
1.  [列出示例](https://cloud.ibm.com/apidocs/discovery#list-examples-for-a-training-data-query)（针对每个查询）。
1.  [获取详细信息](https://cloud.ibm.com/apidocs/discovery#get-details-for-training-data-example)（针对训练数据示例）。 

您在训练数据点中使用的`文档标识`指向当前集合中的文档。您必须在新集合中使用相同的`文档标识`，以确保引用正确的标识。否则，复原的相关性训练将不起作用。
{: important} 

### 查询
{: #backupqueries}

缺省情况下（除非您选择性停用），{{site.data.keyword.discoveryshort}} 将存储您向其发送的查询。 

如果希望能够复原这些查询以[用于统计](https://cloud.ibm.com/apidocs/discovery#number-of-queries-over-time)，您应单独存储这些查询。 

您可以从 {{site.data.keyword.discoveryshort}} [抽取查询](https://cloud.ibm.com/apidocs/discovery#search-the-query-and-event-log)，但最多会存储 10,000 个查询。无分页 API。建议不要复原查询；建议从头开始。

### 反馈/点击数
{: #clicks}

如果将点击数存储为反馈事件形式，那么当前没有简单的方法来备份和复原此信息。建议您使用 [点击数/反馈数据](https://cloud.ibm.com/apidocs/discovery#create-event) API 从头开始。

### 扩展列表
{: #backupexpansions}

如果使用扩展进行查询修改，那么您应备份扩展列表，并在本地存储。为此，请使用 [get expansion list](https://cloud.ibm.com/apidocs/discovery#get-the-expansion-list) API 命令请求扩展列表，并在本地存储。

### 记号化字典或非索引字
{: #backupstopwords}

如果使用这些功能，您将需要备份这些文件并在本地存储。对于非索引字，请备份文本文件，而对于记号化，您应备份 JSON 文件。请参阅[创建定制记号化字典](/docs/services/discovery?topic=discovery-query-concepts#tokenization)和[定义非索引字](/docs/services/discovery?topic=discovery-query-concepts#stopwords)，以获取有关每个文件类型的更多信息。

### 集合信息
{: #collectioninfo}

此项并非必需，但最佳实践是定期对每个集合[检索状态](https://cloud.ibm.com/apidocs/discovery#get-collection-details)，并在本地存储这些信息。通过保留这些统计信息，您稍后可在需要时验证复原过程是否成功。
{: tip} 


### 智能文档理解模型
{: #backupsdu}

如果使用“智能文档理解”(SDU)，您的模型将与配置关联。要避免丢失此信息，您应[导出模型](/docs/services/discovery?topic=discovery-sdu#import)，进行备份，并在本地存储。SDU 模型的文件扩展名为 `.sdumodel`。


## 将数据复原到新的 Watson Discovery 实例
{: #restore}

考虑使用您的备份来复原到位于其他数据中心（也称为区域/位置 - 例如，达拉斯、休斯顿、华盛顿特区和伦敦）的新 {{site.data.keyword.discoveryshort}} 实例。
{: note}

要开始复原，首先请复查集合和关联的数据源的列表以及文件备份。

-  使用保存的配置信息来创建[环境](https://cloud.ibm.com/apidocs/discovery#create-an-environment)和[集合](https://cloud.ibm.com/apidocs/discovery#create-a-collection)。确保已适当定义相应的配置，并已正确设置集合的语言。否则，在使系统恢复启动并开始运行时会有所延迟。
-  如果在 {{site.data.keyword.discoveryshort}} 中设置了任何定制配置，您将需要[重新创建这些定制配置](/docs/services/discovery?topic=discovery-configservice#when-you-need-a-custom-configuration)。 
-  将记号化字典或非索引字添加回集合中。请参阅[创建定制记号化字典](/docs/services/discovery?topic=discovery-query-concepts#tokenization)和[定义非索引字](/docs/services/discovery?topic=discovery-query-concepts#stopwords)。 
-  如果具有定制查询扩展，您还将需要为每个集合[添加查询扩展](https://cloud.ibm.com/apidocs/discovery#create-or-update-expansion-list)。 
-  如果使用来自 Watson Knowledge Studio (WKS) 的任何定制实体模型进行扩充，您将需要[重新导入模型](/docs/services/discovery?topic=discovery-configservice#custom-entity-model)到您的 {{site.data.keyword.discoveryshort}} 实例中。

如先前一样设置集合后，您将需要开始摄入源文档。根据您先前摄入文档的方式，您可以使用如下方式来执行此操作：
-  [API](https://cloud.ibm.com/apidocs/discovery#add-a-document)
-  [连接器](/docs/services/discovery?topic=discovery-sources#sources) 
-  [Data Crawler](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler)
-  或其他方法

### 复原训练数据
{: #restoretraining}

复原集合之后，您可以开始[重新创建相关性训练模型](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api)。 

检索您备份的训练数据，然后：

1. [上传查询](https://cloud.ibm.com/apidocs/discovery#add-query-to-training-data)
1. [上传示例文档](https://cloud.ibm.com/apidocs/discovery#add-example-to-training-data-query)（针对每个查询）。
1.  上传训练数据后，请复查此[博客帖子](https://developer.ibm.com/dwblog/2017/get-relevancy-training/)以确保满足先前的准确性数目。请记住，旧的`文档标识`必须传输到新的训练数据中，或进行更新以在新集合中反映新的文档标识。


### 复原与外部数据源的连接
{: #restoreconnections}

在意外丢失数据的情况下，您可能会丢失外部数据源的已安排的搜寻。请参阅[连接到数据源](/docs/services/discovery?topic=discovery-sources#sources)，以获取可用源的列表。

要复原外部数据，您将需要重新建立与这些数据源的连接，然后重新搜寻。

查找您先前存储的数据源凭证，并遵循[此处](/docs/services/discovery?topic=discovery-sources#sources)的指示信息。您将能够重新连接到数据源，并将数据导入 {{site.data.keyword.discoveryshort}} 中。


### 复原智能文档理解模型
{: #restoresdu}

要导入先前导出的“智能文档理解”(SDU) 模型，请遵循[此处](/docs/services/discovery?topic=discovery-sdu#import)的指示信息。SDU 模型的文件扩展名为 `.sdumodel`。

将 SDU 现有模型导入新集合时，最佳实践是创建新的集合并添加一个文档，然后导入模型并上传其余文档。
