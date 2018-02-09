---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-08"

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

# Migrando do Watson Discovery News Original

Uma nova versão do {{site.data.keyword.discoverynewsshort}} lançada em **31 de julho de 2017**. A versão original foi renomeada {{site.data.keyword.discoverynewsshort}} Original e foi retirada com uma remoção da data de serviço de **15 de janeiro de 2018**.  
{: shortdesc}

Para migrar do {{site.data.keyword.discoverynewsshort}} Original para a nova versão, é necessário
fazer várias mudanças, incluindo atualizar quaisquer consultas criadas para o
{{site.data.keyword.discoverynewsshort}} Original.

  **Nota:** se você tiver criado uma nova instância do
{{site.data.keyword.discoveryshort}}, você terá acesso somente à nova versão do
{{site.data.keyword.discoverynewsshort}}. O acesso aos novos
{{site.data.keyword.discoverynewsshort}} e {{site.data.keyword.discoverynewsshort}} Original
está disponível apenas em instâncias do {{site.data.keyword.discoveryshort}} criadas antes de
**31 de julho de 2017**.

Consulte [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html) para obter uma descrição desta coleção.

Para obter uma descrição e informações sobre a consulta do {{site.data.keyword.discoverynewsshort}}
Original, consulte
[Watson Discovery
News Original](/docs/services/discovery/discovery-auxiliary.html#watson-discovery-news-original).

## Comparação de serviço

| {{site.data.keyword.discoverynewsshort}} Original         | {{site.data.keyword.discoverynewsshort}}           |
|----------------------------------------|---------------------------------|
| O **{{site.data.keyword.discoverynewsshort}} Original** é pré-aprimorado
com os enriquecimentos do Alchemy Language a seguir: Extração de Palavra-Chave, Extração de
Entidade, Identificação de Conceito, Extração de Relação, Análise de Sentimentos e Classificação de Taxonomia. Os seguintes metadados adicionais também são incluídos: data de crawl, data de publicação, classificação de URL, classificação de host e texto âncora.     | 
O **{{site.data.keyword.discoverynewsshort}}** é pré-aprimorado com os
enriquecimentos do {{site.data.keyword.nlushort}} (NLU) a seguir: Extração de
Palavra-Chave, Extração de Entidade, Extração de Função Semântica, Análise de Sentimentos,
Relações e Classificação de Categoria. Os seguintes metadados adicionais também são incluídos: data de crawl e data de publicação. 
Para saber mais sobre os enriquecimentos do NLU, consulte
[Incluindo enriquecimentos](/docs/services/discovery/building.html#adding-enrichments).
|
| O **{{site.data.keyword.discoverynewsshort}} Original** era acessível por meio de
um ambiente que era exclusivo na instância de serviço.                       | Ao usar o
**{{site.data.keyword.discoverynewsshort}}**, todos os usuários consultam o mesmo
ambiente e coleção. Isso significa que todas as referências ao seu ambiente e coleção precisam ser mudadas.
|
| No **{{site.data.keyword.discoverynewsshort}} Original**, você recebe informações
como o tamanho da coleção, o número de documentos, etc., ao recuperar o ambiente por meio da API.  | 
A API do **{{site.data.keyword.discoverynewsshort}}** não retorna essas
informações.
|

Os novos campos a seguir estão disponíveis no
**{{site.data.keyword.discoverynewsshort}}**:

`enriched_text.relations.arguments.text`  
`enriched_text.relations.score`  
`enriched_text.relations.sentence`  
`enriched_text.relations.type`  
`enriched_title.relations`  
`enriched_title.relations.arguments`  
`enriched_title.relations.arguments.entities`<br/>
`enriched_title.relations.arguments.entities.text`  
`enriched_title.relations.arguments.entities.type`  
`enriched_title.relations.arguments.text`  
`enriched_title.relations.score`  
`enriched_title.relations.sentence`  
`enriched_title.relations.type`  
`external_links`  
`extracted_metadata`  
`extracted_metadata.file_type`  
`extracted_metadata.filename`  
`extracted_metadata.sha1`  
`forum_title`  
`main_image_url`

Muitos campos também foram removidos, por exemplo, `blekko.hostrank`,
`duplicate_url`, `domain`, etc. Consulte <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/News_migration_v_1.01.xlsx" download>AQUI <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo" class="style-scope doc-content"></a> para obter uma lista completa.

## Movendo Consultas para o novo Watson Discovery News

Para mover suas consultas do {{site.data.keyword.discoverynewsshort}} Original para o novo {{site.data.keyword.discoverynewsshort}}, é necessário modificar todas as consultas existentes das maneiras a seguir:  

- Mude o ID do ambiente que a consulta está chamando. O nome do ambiente de notícias foi padronizado em todas as instâncias de serviço do {{site.data.keyword.discoveryshort}} para:

  `sistema`  

- Mude o ID da coleção chamado pela consulta. O nome da coleção de notícias foi padronizado em todas as instâncias de serviço do {{site.data.keyword.discoveryshort}} para:

  `news`

- Modifique a consulta para usar a nova estrutura de caminho JSON para o novo {{site.data.keyword.discoverynewsshort}}. A maioria dos campos mudou os caminhos, múltiplos campos foram incluídos e um grupo selecionado de campos de baixo valor foi removido. Consulte a planilha de migração de campo para obter detalhes completos <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/News_migration_v_1.01.xlsx" download>aqui <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo" class="style-scope doc-content"></a>).
Por exemplo, a consulta a seguir:

  `discovery/api/v1/environments/ae5790c2-592f-432a-804a-ee16de7154d7/collections/3edcd8f1-e25a-4f44-a069-58332ad17651/query?version=2017-11-07&query=entities.type:"Company"`

  Deve ser mudada para:

  `discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.type:"Company"`  

## Consultando o Watson Discovery News

É possível consultar o {{site.data.keyword.discoverynewsshort}} usando a API ou um dos SDKs do {{site.data.keyword.watson}}. Além disso, é possível usar o conjunto de ferramentas de construção de consulta para construir consultas de forma interativa.

**Para ativar o conjunto de ferramentas do {{site.data.keyword.discoveryshort}} e a consulta do {{site.data.keyword.discoverynewsshort}}:**

1. Clique em **ferramenta Ativar** para {{site.data.keyword.discoveryshort}} em **Serviços**.
1. Clique no quadrado {{site.data.keyword.discoverynewsshort}} para abrir a tela **Gerenciar dados**.
1. Clique em **Visualizar esquema de dados**, em seguida, clique em **Construir consultas** para abrir o gerador de consultas.

  As consultas no {{site.data.keyword.discoverynewsshort}} são estruturadas da mesma forma que as consultas gravadas para coleções de dados privados. Consulte [Conceitos de Consulta](/docs/services/discovery/using.html) e [Referência de consulta](/docs/services/discovery/query-reference.html).
  {: tip}

**Nota:** não espere que resultados idênticos serão retornados para consultas semelhantes no {{site.data.keyword.discoverynewsshort}} Original e no {{site.data.keyword.discoverynewsshort}}. Tempo de crawl, fontes e enriquecimentos combinam-se para retornar resultados diferentes.

## Incluindo as consultas do Watson Discovery News em seu aplicativo

Use um dos seguintes métodos para incluir consultas em seu aplicativo. Todos esses exemplos de consulta para `enriched_text.entities` com um valor de `text` de `IBM` (`enriched_text.entities.text:IBM`).

Em todos os exemplos a seguir, substitua `{username}` e `{password}` pelo nome do usuário e senha que estão listados na página **Credenciais de serviço** de sua instância de serviço.

### Usando chamadas diretas para a API

```bash
curl -u "{username}":"{password}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

### Usando o SDK Java do Watson

```java
Discovery discovery = new Discovery("2017-11-07"); discovery.setEndPoint("https://gateway.watsonplatform.net/discovery/api/v1"); discovery.setUsernameAndPassword("{username}", "{password}"); String environmentId = "system"; String collectionId = "news";

QueryRequest.Builder queryBuilder = new QueryRequest.Builder(environmentId, collectionId);  
queryBuilder.query("enriched_text.entities.text:IBM");  
QueryResponse queryResponse = discovery.query(queryBuilder.build()).execute();
```
{: codeblock}

### Usando o SDK Watson Node.js

```javascript
var watson = require('watson-developer-cloud');  

var discovery = new DiscoveryV1({  
  username: '{username}', password: '{password}', version_date: '2017-11-07' });  

discovery.query(('system', 'news', 'enriched_text.entities.text:IBM'), function(error, data) {  
    console.log(JSON.stringify(data, null, 2)); }
);
```
{: codeblock}

### Usando o SDK Watson Python

```python
import sys import os import json from watson_developer_cloud import DiscoveryV1  

discovery = DiscoveryV1( username="{username}", password="{password}", version="2017-11-07" )  

qopts = {'query': 'enriched_text.entities.text:IBM'}  
my_query = discovery.query('system', 'news', qopts)  
print(json.dumps(my_query, indent=2))  
```
{: codeblock}
