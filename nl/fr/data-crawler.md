---

copyright:
  years: 2015, 2017, 2019
lastupdated: "2019-02-08"

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

# Ajout de contenu à l'aide de Data Crawler
{: #adding-content-with-data-crawler}

Data Crawler vous permet d'automatiser le téléchargement de contenu dans le service {{site.data.keyword.discoveryshort}}.
{: shortdesc}

Utilisez Data Crawler uniquement pour explorer les bases de données ou les partages de fichier. Dans tous les autres cas, vous devez utiliser le connecteur {{site.data.keyword.discoveryshort}} approprié. Pour plus de détails, voir [Connexion à des sources de données](/docs/services/discovery?topic=discovery-sources#sources). Plus aucune assistance n'est disponible pour Data Crawler si vous utilisez ce composant avec une source de données prise en charge par les connecteurs {{site.data.keyword.discoveryshort}}.
{: important}

## Exploration de données à l'aide de Data Crawler
{: #dc-crawling}

Data Crawler est un outil de ligne de commande qui vous aide à extraire des documents des référentiels où ils résident (par exemple : partages de fichiers, bases de données) et à les déposer dans le cloud, afin qu'ils soient utilisés par le service {{site.data.keyword.discoveryshort}}.

Utilisez Data Crawler uniquement pour explorer les bases de données ou les partages de fichier. Dans tous les autres cas, vous devez utiliser le connecteur {{site.data.keyword.discoveryshort}} approprié pour Box, SharePoint, Salesforce, IBM Cloud Object Storage ou l'exploration Web. Pour plus de détails, voir [Connexion à des sources de données](/docs/services/discovery?topic=discovery-sources#sources). Plus aucune assistance n'est disponible pour Data Crawler si vous utilisez ce composant avec une source de données prise en charge par les connecteurs {{site.data.keyword.discoveryshort}}.
{: important}

## Quand utiliser Data Crawler
{: #dc-use}

Utilisez Data Crawler si vous souhaitez télécharger de manière gérée un nombre important de fichiers à partir d'un système distant ou si vous souhaitez extraire le contenu d'un référentiel pris en charge (par exemple, une base de données DB2).

Data Crawler n'est pas destiné à être une solution de téléchargement de fichiers à partir de votre unité locale. Le téléchargement de fichiers à partir d'une unité locale doit être effectué à l'aide des outils ou des appels API directs. Pour télécharger un grand nombre de fichiers dans {{site.data.keyword.discoveryshort}}, vous pouvez utiliser [discovery-files ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/IBM/discovery-files){: new_window} sur GitHub.
{: note}

## Utilisation de Data Crawler
{: #dc-using}

1. [Configurez le service {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-configservice#configservice)
1. [Téléchargez et installez Data Crawler](/docs/services/discovery?topic=discovery-downloading-and-installing-the-data-crawler#downloading-and-installing-the-data-crawler) sur un système Linux pris en charge pouvant accéder au contenu que vous souhaitez explorer.
1. [Connectez Data Crawler](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-connector-and-seed-options) à votre contenu.
1. [Configurez Data Crawler](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-the-data-crawler) pour qu'il se connecte au service {{site.data.keyword.discoveryshort}}.
1. [Explorez votre contenu](/docs/services/discovery?topic=discovery-crawling-your-data-repository#crawling-your-data-repository).

Vous pouvez vous initier rapidement à l'utilisation de Data Crawler en suivant l'exemple contenu dans la rubrique [Initiation à Data Crawler](/docs/services/discovery?topic=discovery-getting-started-with-the-data-crawler#getting-started-with-the-data-crawler).
