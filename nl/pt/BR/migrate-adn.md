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

# Migrando do AlchemyData News
{: #migrate-adn}

Uma nova versão do {{site.data.keyword.discoverynewsfull}} lançada em **31 de julho de 2017**. Consulte [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html) para obter uma descrição desta coleção.

O AlchemyData News se tornou obsoleto com uma remoção na data de serviço de **7 de março de 2018**

## Comparação de serviço
{: shortdesc}

As seguintes diferenças são observadas ao mover do AlchemyData News para o {{site.data.keyword.discoverynewsshort}} no serviço do {{site.data.keyword.discoveryshort}}.

- O {{site.data.keyword.discoveryshort}} cobra consultas de notícias somente pela consulta. Todos os campos estão disponíveis para retorno com cada resultado sem nenhum custo adicional.
- Cada consulta do {{site.data.keyword.discoveryshort}} pode retornar até um máximo de 50 resultados. Um parâmetro `offset` está disponível para que seja possível localizar consultas para qualquer número de resultados que precisar.
- O {{site.data.keyword.discoveryshort}} também suporta agregações. Consulte a seção [agregações](/docs/services/discovery/query-reference.html#aggregations) da documentação do {{site.data.keyword.discoveryshort}} para obter mais informações.
- O {{site.data.keyword.discoverynewsfull}} não classifica na mesma maneira que o AlchemyData News faz. Atualmente não há nenhum campo para classificação.
- A estrutura de consulta e a estrutura dos dados retornados são diferentes entre o {{site.data.keyword.discoverynewsshort}} e o AlchemyData News. Uma boa maneira de entender a estrutura JSON é consultar um único resultado no {{site.data.keyword.discoverynewsshort}} e inspecionar esse resultado.
- O {{site.data.keyword.discoverynewsshort}} não suporta saída XML.
- A deduplicação é um recurso beta no {{site.data.keyword.discoverynewsshort}}.

## Diferenças de autenticação

O serviço do {{site.data.keyword.discoveryshort}} usa as credenciais `username` e `password` padrão do {{site.data.keyword.Bluemix_notm}} para acessar consultas. Isso substitui o método de chave API existente que o AlchemyData News usou. Todas as consultas do {{site.data.keyword.discoveryshort}} devem ser feitas com uma combinação de nome de usuário e senha criada pela instância de serviço do {{site.data.keyword.discoveryshort}}.

As credenciais de serviço podem ser gerenciadas ao visualizar a guia **Credenciais de serviço** do seu serviço dentro do {{site.data.keyword.Bluemix_notm}}.

## Configurando uma instância do Discovery

Uma instância de serviço do {{site.data.keyword.discoveryshort}} é criada na mesma maneira que você criou sua instância do AlchemyData News.

1. Navegue para o [{{site.data.keyword.Bluemix_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window}, efetue login e selecione o {{site.data.keyword.discoveryshort}} no catálogo de serviços.
1. Selecione o plano apropriado para suas necessidades e clique em **Criar**.

  O serviço do {{site.data.keyword.discoveryshort}} oferece um plano Lite com 1.000 consultas de notícias disponíveis por mês. É possível usar uma instância desse plano para identificar consultas equivalentes sem ter que pagar por elas.
  {: tip}

1. Clique na guia **Credenciais de serviço** e selecione **Visualizar credenciais** para identificar a `url`, `username` e `password` para essa instância.

## Consultando o Watson Discovery News

É possível consultar o {{site.data.keyword.discoverynewsfull}} usando a API ou um dos SDKs do {{site.data.keyword.watson}}. Além disso, é possível usar o conjunto de ferramentas de construção de consulta para construir consultas interativamente.

Para ativar o conjunto de ferramentas do {{site.data.keyword.discoveryshort}} e consultar o {{site.data.keyword.discoverynewsshort}}:

1. Clique em **ferramenta Ativar** para {{site.data.keyword.discoveryshort}} em **Serviços**.
1. Clique no quadrado {{site.data.keyword.discoverynewsshort}} para abrir a tela **Gerenciar dados**.
1. Clique em **Visualizar esquema de dados**, em seguida, clique em **Construir consultas** para abrir o gerador de consultas.

  As consultas no {{site.data.keyword.discoverynewsfull}} são estruturadas da mesma forma que as consultas gravadas para coleções de dados privados. Consulte [Conceitos de consulta](/docs/services/discovery/using.html) e [Referência de consulta](/docs/services/discovery/query-reference.html).
  {: tip}

**Nota:** não espere que resultados idênticos serão retornados para consultas semelhantes no AlchemyData News e no {{site.data.keyword.discoverynewsfull}}. Tempo de crawl, fontes e enriquecimentos combinam-se para retornar resultados diferentes.

## Incluindo as consultas do Watson Discovery News em seu aplicativo

Use um dos seguintes métodos para incluir consultas em seu aplicativo. Todos esses exemplos de consulta para `enriched_text.entities` com um valor de `text` de `IBM` (`enriched_text.entities.text:IBM`).

Em todos os exemplos a seguir, substitua `{username}` e `{password}` pelo nome do usuário e senha que estão listados na página **Credenciais de serviço** de sua instância de serviço.

### Usando chamadas diretas para a API

```bash
curl -u "{username}":"{password}"  'https://gateway.watsonplatform.net/discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

### Usando o SDK Java

```java
Discovery discovery = new Discovery("2017-11-07");
discovery.setEndPoint("https://gateway.watsonplatform.net/discovery/api/v1");
discovery.setUsernameAndPassword("{username}", "{password}");
String environmentId = "system";
  String collectionId = "news";

QueryRequest.Builder queryBuilder = new QueryRequest.Builder(environmentId,collectionId);
queryBuilder.query("enriched_text.entities.text:IBM");
QueryResponse queryResponse =
discovery.query(queryBuilder.build()).execute();
```
{: codeblock}

### Usando o SDK Watson Node.js

```javascript
var watson = require('watson-developer-cloud');

var discovery = new DiscoveryV1({  
  username: '{username}', password: '{password}', version_date: '2017-11-07' });  

discovery.query(('system', 'news', 'enriched_text.entities.text:IBM'),
  function(error, data) {  
  console.log(JSON.stringify(data, null, 2));  
```
{: codeblock}

### Usando o SDK Watson Python

```python
import sys
import os
import json
from watson_developer_cloud import DiscoveryV1

discovery = DiscoveryV1(
  username="{username}",
  password="{password}",
  version="2017-11-07"
)

qopts = {'query': 'enriched_text.entities.text:IBM'}
my_query = discovery.query('{environment_id}', '{collection_id}', qopts)
print(json.dumps(my_query, indent=2))
```
{: codeblock}
