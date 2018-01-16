---

copyright:
  years: 2015, 2018
lastupdated: "2018-01-16"

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

# Creating a custom configuration to add canonical names
{: #normalizing-entities}

You can configure {{site.data.keyword.discoveryshort}} service to include *normalized entities*, also known as *canonical names*, in the output of your queries.
{: shortdesc}

**Note:** This feature is not currently supported with {{site.data.keyword.nlushort}} enrichments. It is supported if you are using {{site.data.keyword.alchemylanguageshort}} enrichments. ({{site.data.keyword.alchemylanguageshort}} enrichment support is scheduled to end on **15 January, 2018**.) Details on configuring this feature with {{site.data.keyword.alchemylanguageshort}} enrichments can be found in [Creating a custom configuration to normalize {{site.data.keyword.alchemylanguageshort}} entities](/docs/services/discovery/discovery-auxiliary.html#normalizing-entities).
