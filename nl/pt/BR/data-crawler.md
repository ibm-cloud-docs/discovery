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

# Incluindo conteúdo com o Data Crawler
{: #adding-content-with-data-crawler}

O Data Crawler permite automatizar o upload de conteúdo para o
{{site.data.keyword.discoveryshort}} Service.
{: shortdesc}

O Data Crawler deve ser usado apenas para efetuar crawl de compartilhamentos de arquivo ou bancos de dados; em todos os outros casos, é necessário usar o conector apropriado do {{site.data.keyword.discoveryshort}}. Veja [Conectando a origens de dados](/docs/services/discovery?topic=discovery-sources#sources) para obter detalhes. A assistência não será mais fornecida para o Data Crawler se você estiver usando-o com uma origem de dados suportada pelos conectores do {{site.data.keyword.discoveryshort}}.
{: important}

## Efetuando crawling de dados com o Data Crawler
{: #dc-crawling}

O Data Crawler é uma ferramenta de linha de comandos que ajudará a tirar seus documentos dos repositórios em que eles residem (por exemplo: compartilhamentos de arquivo, bancos de dados) e enviá-los por push para a nuvem, para serem usados pelo serviço do {{site.data.keyword.discoveryshort}}.

O Data Crawler deve ser usado apenas para executar crawl de compartilhamentos de arquivo ou bancos de dados. Em todos os outros casos, é necessário usar o conector do {{site.data.keyword.discoveryshort}} apropriado para Box, SharePoint, Salesforce, IBM Cloud Object Storage ou Web Crawl. Veja [Conectando a origens de dados](/docs/services/discovery?topic=discovery-sources#sources) para obter detalhes. A assistência não será mais fornecida para o Data Crawler se você estiver usando-o com uma origem de dados suportada pelos conectores do {{site.data.keyword.discoveryshort}}.
{: important}

## Quando usar o Data Crawler
{: #dc-use}

O Data Crawler deve ser usado se você deseja ter um upload gerenciado de um número significativo de
arquivos de um sistema remoto ou se deseja extrair o conteúdo de um repositório suportado (como um banco
de dados DB2).

O Data Crawler não é destinado a ser uma solução para fazer upload de arquivos de sua unidade local. O upload de arquivos por meio de uma unidade local deve ser feito usando o conjunto de ferramentas ou
usando chamadas de API diretas. Outra opção para fazer upload de grandes números de arquivos no {{site.data.keyword.discoveryshort}} é [discovery-files ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/IBM/discovery-files){: new_window} no GitHub.
{: note}

## Usando o Data Crawler
{: #dc-using}

1. [ Configure o serviço  {{site.data.keyword.discoveryshort}}  ](/docs/services/discovery?topic=discovery-configservice#configservice)
1. [Faça download e instale o Data
Crawler](/docs/services/discovery?topic=discovery-downloading-and-installing-the-data-crawler#downloading-and-installing-the-data-crawler) em um sistema Linux suportado que tenha acesso ao conteúdo que você deseja efetuar crawl.
1. [Conecte o Data Crawler](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-connector-and-seed-options) ao seu
conteúdo.
1. [Configure o Data Crawler](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-the-data-crawler)
para conectar-se ao {{site.data.keyword.discoveryshort}} Service.
1. [Efetue crawl de seu conteúdo](/docs/services/discovery?topic=discovery-crawling-your-data-repository#crawling-your-data-repository).

É possível iniciar rapidamente com o Data Crawler seguindo o exemplo em:
[Introdução ao Data Crawler](/docs/services/discovery?topic=discovery-getting-started-with-the-data-crawler#getting-started-with-the-data-crawler)
