---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-30"

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

# Watson Discovery News

O {{site.data.keyword.discoverynewsfull}} é incluído com
o {{site.data.keyword.discoveryshort}}. O {{site.data.keyword.watson}}
{{site.data.keyword.discoverynewsshort}} é um conjunto de dados indexado que é pré-enriquecido
com os seguintes insights cognitivos: **Extração de Palavra-Chave**,
**Extração de Entidade**, **Extração de Função de Semântica**,
**Análise de Sentimentos**, **Extração de Relação** e
**Classificação de Categoria**. (Para saber mais sobre enriquecimentos, consulte
[Incluindo enriquecimentos](building.html#adding-enrichments).) Os seguintes metadados adicionais também são incluídos: data de crawl e data de publicação. A procura histórica está disponível para os últimos 60 dias de dados de notícias. Veja uma demonstração do que você pode construir com o {{site.data.keyword.discoverynewsfull}} [aqui ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://discovery-news-demo.mybluemix.net/){: new_window}.

O {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} é atualizado
continuamente com novos artigos. O {{site.data.keyword.discoverynewsshort}} em inglês é atualizado com
aproximadamente 300.000 novos artigos diariamente. O {{site.data.keyword.discoverynewsshort}}
em espanhol é atualizado com aproximadamente 60.000 novos artigos diariamente e o
{{site.data.keyword.discoverynewsshort}} em coreano é atualizado com 10.000 novos artigos diariamente.

Casos de uso para o {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}}:

- Alerta de Notícias - crie alertas de notícias aproveitando o suporte para entidades,
palavras-chave, categorias e análise de sentimentos para observar as notícias e como elas são percebidas.

- Detecção de Evento - a extração de função de semântica de sujeito/ação/objeto verifica termos/ações, como
"aquisição", "resultados das eleições" ou "IPO".

- Tópicos de tendência nas notícias - identifique tópicos populares e monitore aumentos e
diminuições na frequência com que eles (ou os tópicos relacionados) são mencionados.

Para obter informações sobre como gravar consultas para o
{{site.data.keyword.discoverynewsfull}}, veja
[Conceitos de consulta](/docs/services/discovery/using.html) e
[Referência de consulta](/docs/services/discovery/query-reference.html).

Não é possível ajustar a configuração do {{site.data.keyword.discoverynewsfull}},
treinar ou incluir documentos na coleção do {{site.data.keyword.discoverynewsfull}}.

**Observação:** o número máximo de resultados retornados para uma consulta do Watson Discovery News é `50`. Use as consultas adicionais e o parâmetro `offset` para retornar mais do que `50` resultados.

**Nota:** esta versão do {{site.data.keyword.discoverynewsfull}} estreou em
**31 de julho de 2017**. A versão original foi renomeada {{site.data.keyword.discoverynewsfull}} Original e foi retirada com uma remoção da data de serviço de **15 de janeiro de 2018**. 
Para obter informações sobre migração, consulte
[Migrando do Watson Discovery News Original](/docs/services/discovery/migrate-bwdn.html).
