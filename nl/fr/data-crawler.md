---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-03"

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

# Ajout de contenu à l'aide de Data Crawler

Data Crawler vous permet d'automatiser le téléchargement de contenu dans le service {{site.data.keyword.discoveryshort}}.
{: shortdesc}

## Exploration de données à l'aide de Data Crawler

Data Crawler est un outil de ligne de commande qui vous aide à extraire des documents dans les référentiels où ils résident (par exemple : partages de fichiers, bases de données, Microsoft SharePoint) et à les déposer dans le cloud, afin qu'ils soient utilisés par le service {{site.data.keyword.discoveryshort}}. 

Vous pouvez utiliser les outils ou l'API {{site.data.keyword.discoveryshort}} pour explorer des sources de données Box, Salesforce et Microsoft SharePoint Online. Voir [Connexion à des sources de données](/docs/services/discovery/connect.html) pour plus d'informations.
{: tip}

## Quand utiliser Data Crawler

Utilisez Data Crawler si vous souhaitez télécharger de manière gérée un nombre important de fichiers à partir d'un système distant ou si vous souhaitez extraire le contenu d'un référentiel pris en charge (par exemple, une base de données DB2).

Data Crawler n'est pas destiné à être une solution de téléchargement de fichiers à partir de votre unité locale. Le téléchargement de fichiers à partir d'une unité locale doit être effectué à l'aide des outils ou des appels API directs.
{: tip}

## Utilisation de Data Crawler

1. [Configurez le service {{site.data.keyword.discoveryshort}}](/docs/services/discovery/building.html#configuring-your-service)
1. [Téléchargez et installez Data Crawler](/docs/services/discovery/data-crawler-install.html) sur un système Linux pris en charge pouvant accéder au contenu que vous souhaitez explorer.
1. [Connectez Data Crawler](/docs/services/discovery/data-crawler-seeds.html) à votre contenu.
1. [Configurez Data Crawler](/docs/services/discovery/data-crawler-discovery.html) pour qu'il se connecte au service {{site.data.keyword.discoveryshort}}.
1. [Explorez votre contenu](/docs/services/discovery/data-crawler-run.html).

Vous pouvez vous initier rapidement à l'utilisation de Data Crawler en suivant l'exemple contenu dans la rubrique [Initiation à Data Crawler](/docs/services/discovery/data-crawler-qs.html).
