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

# Incluindo conteúdo com o Data Crawler

O Data Crawler permite automatizar o upload de conteúdo para o
{{site.data.keyword.discoveryshort}} Service.
{: shortdesc}

## Efetuando crawling de dados com o Data Crawler

O Data Crawler é uma ferramenta de linha de comandos que o ajuda a obter seus documentos dos
repositórios nos quais eles residem (por exemplo: compartilhamentos de arquivos, bancos de dados, Microsoft
SharePoint&reg;) e enviá-los por push para a nuvem, para que sejam usados pelo
{{site.data.keyword.discoveryshort}} Service.

## Quando usar o Data Crawler

O Data Crawler deve ser usado se você deseja ter um upload gerenciado de um número significativo de
arquivos de um sistema remoto ou se deseja extrair o conteúdo de um repositório suportado (como um banco
de dados DB2).

O Data Crawler não é destinado a ser uma solução para fazer upload de arquivos de sua unidade local. 
O upload de arquivos por meio de uma unidade local deve ser feito usando o conjunto de ferramentas ou
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
