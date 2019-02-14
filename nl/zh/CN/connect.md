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

# 连接到数据源
{: #sources}

通过 {{site.data.keyword.discoveryshort}} 服务，您可以连接到远程源并在其中搜寻文档。
{: shortdesc}

您可以连接到数据源，并通过配置要与该源关联的集合，定期（如果需要）将文档拉取到 {{site.data.keyword.discoveryshort}} 服务中。每个集合可以配置有一个数据源。{{site.data.keyword.discoveryshort}} 服务使用名为搜寻的过程从数据源拉取文档。搜寻是指从指定的起始位置系统地浏览和检索文档的过程。{{site.data.keyword.discoveryshort}} 服务仅对您显式指定的项进行搜寻。可以搜寻以下类型的数据源：

-  [Box](/docs/services/discovery/connect.html#connectbox)
-  [Salesforce](/docs/services/discovery/connect.html#connectsf)
-  [Microsoft SharePoint Online](/docs/services/discovery/connect.html#connectsp)

连接到数据源的操作可以使用 {{site.data.keyword.discoveryshort}} 工具或 API 来执行。{{site.data.keyword.discoveryshort}} 工具提供了一种简化的连接方法，该方法不需要对源系统了解很多，而 API 则提供了更细粒度的高度可配置界面，该界面要求更好地了解您要连接的源。通过以下过程概述，您可了解接下来要阅读本文档的哪些部分：

1.  请阅读[一般源需求](/docs/services/discovery/connect.html#gen_req)，以便大致了解需要哪些内容。
2.  请阅读特定于源系统的需求：
    -  [Box](/docs/services/discovery/connect.html#connectbox)
    -  [Salesforce](/docs/services/discovery/connect.html#connectsf)
    -  [Microsoft SharePoint Online](/docs/services/discovery/connect.html#connectsp)
3.  请根据您的配置选择来阅读源配置指示信息：
    -  [使用工具](/docs/services/discovery/connect.html#source_tooling)
    -  [使用 API](/docs/services/discovery/connect.html#source_api)

## 一般源需求
{: #gen_req}

以下一般需求适用于所有数据源：

-  Box、Salesforce 和 SharePoint Online 的单个文档文件大小限制为 10 MB。
-  您需要每个数据源的凭证和文件位置（或 URL）- 这些信息通常由数据源的开发者/系统管理员提供。
-  您需要知道要搜寻哪些数据源资源。这可以由源管理员提供。搜寻 Box 或 Salesforce 时，如果使用 {{site.data.keyword.discoveryshort}} 工具来配置源，那么会显示可用资源的列表。
-  搜寻数据源将使用数据源的资源（API 调用）。调用数取决于搜寻的文档数。必须针对数据源获取相应级别的服务（例如，企业），并咨询源系统管理员。
-  {{site.data.keyword.discoveryshort}} 可以摄入以下文件类型，其他所有类型的文档都会忽略：
   -  Microsoft Word
   -  PDF
   -  HTML
   -  JSON
-  {{site.data.keyword.discoveryshort}} 源搜寻不会删除集合中存储的文档。重新搜寻源时，会添加新文档，将更新的文档修改为当前版本，而删除的文档仍保留为上次存储的版本。

## Box
{: #connectbox}

连接到 Box 源时，请确保计划连接到的实例是企业套餐或更高级别的套餐。

设置 Box 帐户以使用 {{site.data.keyword.discoveryshort}}：

1.  在 `https://app.box.com/developers/console` 上创建新的 Box 定制应用程序（使用您公司的 Box URL）。
1.  然后执行下列其中一个操作：
    - 对于**应用程序访问权**，选择`企业`，然后使用现有受管用户继续执行操作。
      或
    - 对于**应用程序访问权**，选择`应用程序`，然后使用 [Box API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.box.com/reference#create-app-user){: new_window} 为新创建的应用程序创建`应用程序用户`。
1.  启用以下**应用程序作用域**：
    - `读写存储在 Box 中的所有文件夹`
    - `管理用户`
1.  启用以下**高级功能**：
    - `以用户身份执行操作`
    - `生成用户访问令牌`
1.  通过将 `https://app.box.com/developers/console` 中的`客户机标识`输入到 `API 密钥`字段中，使管理员对您的应用程序客户机标识授权 `https://app.box.com/master/settings/openbox`。
1.  生成`公用/专用密钥对`（将下载到您的计算机）。
1.  打开下载的文件，然后将这些字段复制/粘贴到 {{site.data.keyword.discoveryshort}}。复制到 {{site.data.keyword.discoveryshort}} 中时，请除去 `privateKey` 末尾的尾部换行符 `\n`。

**注：**{{site.data.keyword.discoveryshort}} 不支持定制应用程序搜寻本身（您无法模拟自身）。 

下面是连接到 Box 源所需的凭证；这些凭证应该从 Box 管理员获取（除非您通过使用先前步骤设置 Box 定制应用程序来获取这些凭证）：

-  `client_id` - 这些凭证连接到的源的 `client_id`。    
-  `enterprise_id` - 这些凭证连接到的 Box 站点的 `enterprise_id`。
-  `client_secret` - 这些凭证连接到的源的 `client_secret`。此值从不会返回，而只在创建或修改凭证时使用。
-  `public_key_id` - 这些凭证连接到的源的 `public_key_id`。此值从不会返回，而只在创建或修改凭证时使用。
-  `private_key` - 这些凭证连接到的源的 `private_key`。此值从不会返回，而只在创建或修改凭证时使用。
-  `passphrase` - 这些凭证连接到的源的 `passphrase`。此值从不会返回，而只在创建或修改凭证时使用。

确定凭证时，查阅 [Box 开发者文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.box.com/){: new_window} 可能非常有用。

搜寻 Box 时要考虑的其他事项：

-  Box 注释以 JSON 格式存储，以便 {{site.data.keyword.discoveryshort}} 摄入指定文件夹中的任何 Box 注释。
-  使用 API 时，您需要有“文件夹标识”列表以及要搜寻的每个文件夹的关联“所有者标识”。通过 {{site.data.keyword.discoveryshort}} 工具，您可以浏览并选择要搜寻的内容。

## Salesforce
{: #connectsf}

连接到 Salesforce 源时，请确保计划连接到的实例是企业套餐或更高级别的套餐。

下面是连接到 Salesforce 源所需的凭证；这些凭证应该从 Salesforce 管理员获取：
-  `url` - 这些凭证连接到的源的 `url`。
-  `username` - 这些凭证连接到的源的 `username`。
-  `password` - `password` 由 Salesforce 密码和有效的 Salesforce 安全性令牌并置而成。此值从不会返回，而只在创建或修改凭证时使用。

确定凭证时，查阅 [Salesforce 开发者文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.salesforce.com/docs/){: new_window} 可能非常有用。

搜寻 Salesforce 时要考虑的其他事项：

-  仅当知识库文章的**版本**为`已发布`且其语言为 `en-us` 时，才会搜寻这些文章。
-  使用 API 时，您需要有要搜寻的 Salesforce 对象的列表。通过 {{site.data.keyword.discoveryshort}} 工具，您可以浏览并选择要搜寻的内容。


## SharePoint Online
{: #connectsp}

连接到 Microsoft SharePoint Online 源时，请确保计划连接到的实例是企业 (E1) 套餐或更高级别的套餐。

下面是连接到 SharePoint Online 源所需的凭证；这些凭证应该从 SharePoint 管理员获取：

-  `organization_url` - 这些凭证连接到的源的 `organization_url`。
-  `site_collection.path` - 这些凭证连接到的源的 `site_collection.path`。
-  `username` - 这些凭证连接到的源的 `client_id`。
-  `password` - 这些凭证连接到的源的 `password`。此值从不会返回，而只在创建或修改凭证时使用。

确定凭证时，查阅 [Microsoft SharePoint 开发者文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://docs.microsoft.com/en-us/sharepoint/dev/){: new_window} 可能非常有用。

搜寻 Microsoft SharePoint Online 时要考虑的其他事项：

-  搜寻 SharePoint 时，您需要有要搜寻的 SharePoint 站点集合路径的列表。通过 {{site.data.keyword.discoveryshort}} 工具，您可以浏览并选择要搜寻的内容。要搜寻整个 SharePoint Online 站点，请勿在此字段中选择多个路径 (URL)。在该场景中，请在 `site_collection.path` 字段中输入 `/`。

## 使用工具
{: #source_tooling}

使用 {{site.data.keyword.discoveryshort}} 工具连接到数据源的操作可通过专门为源创建集合来执行。执行以下步骤来创建源集合并对其进行搜寻：

1.  在 {{site.data.keyword.discoveryshort}} 工具的**管理数据**页面中，选择**连接数据源**。
2.  选择要连接到的数据源。
3.  输入源凭证，然后单击“连接”。源凭证必须从源系统管理员获取。
4.  选择要搜寻的数据以及要对其进行同步的频率。
5.  单击**保存并同步对象**以开始搜寻数据源。然后，会将您重定向到“集合状态”屏幕，在文档添加到集合后，此屏幕会更新。

搜寻初始将同步数据，然后会按指定的频率进行同步。**注：**如果在**同步设置**屏幕中修改了任何内容，然后单击**保存并同步对象**，那么此时将启动搜寻（或者，如果已经有搜寻在运行，那么将重新启动搜寻）。

## 使用 API
{: #source_api}

使用以下过程来创建使用 API 连接到数据源的集合。
1.  使用[源凭证 API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#credentials-api){: new_window} 为要连接到的源创建凭证。记录新创建凭证的返回的 **credential_id**。
2.  使用[配置 API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#configurations-api){: new_window} 创建新配置。此配置必须包含用于定义应该搜寻的内容的 **source** 对象。**source** 对象必须包含您先前记录的 **credential_id**。
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
    记录新创建配置的返回的 **configuration_id**。
3.  使用[集合 API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#configurations-api){: new_window} 创建新集合。定义集合的对象必须包含先前记录的 **configuration_id**。

源搜寻将在创建集合后立即启动，随后会根据您指定的频率再次启动。
**注：**如果在配置的 **source** 对象中修改了任何内容，那么此时将启动新的搜寻（或者，如果已经有搜寻在运行，那么将重新启动搜寻）。

## 指定 `customer_id`
{:# source_customer_id}

摄入的 {{site.data.keyword.discoveryshort}} 文档中的 `customer_id` 字段可用于通过 API 中的 **user-data** 方法基于 `customer_id` 来删除内容。从数据源摄入传入文档时，不会自动为其指定 `customer_id`。如果应用程序需要定义 `customer_id`，那么可以指定要从源系统复制并用作 `customer_id` 的一个或多个传入字段。为此，您必须修改要用于连接到源的配置。

1.  执行样本查询并确定要用作 `customer_id` 的字段。
2.  修改配置。您需要添加**规范化**部分，以创建 `customer_id` 字段。
    -  在工具中，浏览至您的集合，然后单击“配置”部分中的**编辑**链接。接着，单击**规范化**选项卡并添加**复制**规范化，以创建 `customer_id` 字段。然后，单击**应用并保存**。
    ![复制规范化](images/norm_copy.png)
    -  使用 API 时，请将以下对象添加到 **noramizations** 数组：
       ```json
       {
         "operation" : "copy",
         "source_field" : "{original_field_name}",
         "destination_field" : "customer_id"
       }
       ```
       {: codeblock}
3.  下一个安排的搜寻会将 `customer_id` 字段添加到所有文档。如果要立即开始搜寻，请修改源配置（工具中的**同步设置**）。

请参阅[信息安全 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.bluemix.net/docs/services/discovery/information-security.html){: new_window} 以获取更多相关信息以及有关基于 `customer_id` 进行删除的信息。
