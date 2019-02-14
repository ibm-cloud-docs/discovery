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

# Incluindo conteúdo com o Data Crawler

O Data Crawler permite automatizar o upload de conteúdo para o
{{site.data.keyword.discoveryshort}} Service.
{: shortdesc}

## Efetuando crawling de dados com o Data Crawler

O Data Crawler é uma ferramenta de linha de comandos que ajudará você a tomar seus documentos dos repositórios em que eles residem (por exemplo: compartilhamentos de arquivo, bancos de dados, Microsoft SharePoint) e enviá-los por push para a nuvem, para serem usados pelo serviço {{site.data.keyword.discoveryshort}}.

É possível usar o conjunto de ferramentas do {{site.data.keyword.discoveryshort}} ou a API para efetuar crawl em origens de dados do Box, Salesforce e Microsoft SharePoint Online. Consulte [Conectando-se a origens de dados](/docs/services/discovery/connect.html) para obter mais informações.
{: tip}

## Quando usar o Data Crawler

O Data Crawler deve ser usado se você deseja ter um upload gerenciado de um número significativo de
arquivos de um sistema remoto ou se deseja extrair o conteúdo de um repositório suportado (como um banco
de dados DB2).

O Data Crawler não é destinado a ser uma solução para fazer upload de arquivos de sua unidade local. O upload de arquivos por meio de uma unidade local deve ser feito usando o conjunto de ferramentas ou
usando chamadas de API diretas.
{: tip}

## Usando o Data Crawler

1. [Configure o
serviço do {{site.data.keyword.discoveryshort}}](/docs/services/discovery/building.html#configuring-your-service)
1. [Faça download e instale o Data
Crawler](/docs/services/discovery/data-crawler-install.html) em um sistema Linux suportado que tenha acesso ao conteúdo que você deseja efetuar crawl.
1. [Conecte o Data Crawler](/docs/services/discovery/data-crawler-seeds.html) ao seu
conteúdo.
1. [Configure o Data Crawler](/docs/services/discovery/data-crawler-discovery.html)
para conectar-se ao {{site.data.keyword.discoveryshort}} Service.
1. [Efetue crawl de seu conteúdo](/docs/services/discovery/data-crawler-run.html).

É possível iniciar rapidamente com o Data Crawler seguindo o exemplo em:
[Introdução ao Data Crawler](/docs/services/discovery/data-crawler-qs.html)
