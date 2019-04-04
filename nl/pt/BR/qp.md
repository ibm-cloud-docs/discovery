---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-18"

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

# Desempenho da consulta
{: #qp}

O desempenho da consulta no {{site.data.keyword.discoveryshort}} é dependente de vários fatores. 

## Avaliando o desempenho 
{: #qp-evaluate}

Se você espera um alto carregamento simultâneo no aplicativo, é importante avaliar o desempenho de seu aplicativo {{site.data.keyword.discoveryshort}}. Há várias dimensões comumente usadas para medir o desempenho:
1.  **Latência de resposta** - O tempo que leva para o {{site.data.keyword.discoveryshort}} retornar os resultados de sua consulta. 
    - A latência pode variar dependendo de uma série de fatores. Consulte [Fatores que afetam o desempenho](/docs/services/discovery?topic=discovery-qp#perffactors) para obter mais informações. 
    - É importante executar testes em seu ambiente de produção usando um conjunto representativo de consultas para determinar a latência média. 
1.   **Taxa de consulta** - O número de solicitações que podem ser processadas em um determinado horário, geralmente medidas em consultas por segundo (QPS). Essa medida é mais importante quando você espera alta carga simultânea em seu aplicativo.  
     - A taxa que pode ser alcançada varia com base em muitos dos mesmos fatores que a latência. 
     - Também é necessário que a taxa de consulta seja avaliada com consultas representativas e com as cargas que você espera ver. Lembre-se de considerar as cargas de pico durante o teste.

## Fatores que impactam o desempenho
{: #perffactors}

O desempenho da consulta no {{site.data.keyword.discoveryshort}} variará com base em vários fatores, incluindo o tamanho do plano, a complexidade da consulta, os recursos usados e o tamanho e a complexidade da coleção.

### Tamanho do plano
{: #qp-plansize}

Os planos de precificação do {{site.data.keyword.discoveryshort}} limitam o número de documentos disponíveis e também fornecem a capacidade diferenciada de manipular a carga de consulta. Quanto maior o tamanho do plano, mais recursos estarão disponíveis para manipular consultas. Os limites de taxa médios também variam de acordo com o tamanho do plano. Fazer upgrade de seu plano pode melhorar o desempenho. Consulte [Planos de precificação do {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans) para planos e limites. 

### Complexidade de
{: #qp-query}

Há muitas maneiras de executar consultas com relação ao {{site.data.keyword.discoveryshort}} e as diferentes operações usadas podem afetar o desempenho. Essas características de consulta podem afetar o desempenho:

1.   **Comprimento** - As consultas mais longas provavelmente terão desempenho mais fraco. 
1.   **Agregações** - Agregações são um tipo de consulta mais complexo, com agregações aninhadas que têm o maior impacto no desempenho. 
1.   **Operadores** - A correspondência difusa e de curinga pode afetar o desempenho.
1.   **Contagens** - Reduzir a contagem de documentos retornados pode melhorar o desempenho. Se precisar paginar os resultados, use o parâmetro `offset`. 
1.   **Campos de retorno** - Limitar os campos retornados para apenas aqueles necessários para o seu aplicativo pode ajudar. (Por exemplo, não retorne o texto total do documento se apenas o título ou a passagem forem necessários.) 

Consulte  [ Referência de consulta ](/docs/services/discovery?topic=discovery-query-reference#query-reference)  para obter detalhes.

### Recursos usados
{: #qp-features}

Há vários recursos que aprimoram os resultados da consulta. Os recursos a seguir podem afetar o desempenho:
 
1.   **Recuperação de passagem** - A recuperação de passagem procura em documentos para localizar fragmentos relevantes de texto para a sua consulta. É possível ajustar os campos nos documentos sobre os quais a recuperação de passagem procura com o parâmetro `passages.fields`. Se o seu conteúdo tiver muitos campos, isso ajudará a reduzir a latência da recuperação de passagem. Consulte [Passagens](/docs/services/discovery?topic=discovery-query-parameters#passages) para obter mais informações sobre a recuperação de passagem.
1.   **Treinamento de relevância** - O treinamento de relevância calcula os recursos para cada campo de texto de nível superior (campos no mesmo nível que `document_id` no JSON) na coleção. Se houver muitos campos de nível superior, isso poderá causar um impacto de desempenho para uma `natural_language_query` ao usar o treinamento. Reduzir o número de campos de nível superior pode melhorar o desempenho. Isso pode ser feito por meio da normalização ou editando manualmente o JSON para colocar campos que não são úteis para localizar o conteúdo relevante em uma estrutura aninhada. Mudar os campos usados para treinamento também tem impacto no modelo. Assim, será necessário considerar tanto o impacto no desempenho quanto a precisão dos resultados se essa mudança for feita. Consulte [Melhorando a relevância do resultado](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling) para obter mais informações sobre o treinamento de relevância.
1.  **Treinamento contínuo de relevância** - Procuras de treinamento contínuo de relevância em todas as coleções em um ambiente. Quanto mais coleções em um ambiente, maior o impacto no desempenho.  Consulte [Treinamento contínuo de relevância](/docs/services/discovery?topic=discovery-crt#crt) para obter mais informações.

### Tamanho e complexidade de coleção
{: #qp-collection} 

A composição dos documentos em uma coleção privada também pode afetar o desempenho da consulta:
1.  **Número total de documentos** - O desempenho pode ser afetado ao se aproximar dos limites superiores de `Number of Documents` para tamanhos do plano Advanced. 
1.  **Tamanho de documentos** - Documentos muito grandes (aqueles com vários MB em tamanho) requerem a movimentação de uma grande quantia de dados por solicitação, o que pode afetar negativamente o desempenho, especialmente ao usar o treinamento de relevância e a recuperação de passagem. 
1.  **Número de enriquecimentos** - Enriquecimentos incluem complexidade nos documentos ao inserir um número significativo de campos aninhados. Se um enriquecimento não for necessário para o seu caso de uso, considere desativá-lo no momento da ingestão. Os enriquecimentos não são diretamente usados para relevância de procura `natural_language_query`. Consulte [Incluindo enriquecimentos](/docs/services/discovery?topic=discovery-configservice#adding-enrichments) para obter mais informações sobre enriquecimentos.
