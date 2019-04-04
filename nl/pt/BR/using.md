---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-01-22"

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

# Conceitos de consulta
{: #query-concepts}

O serviço do {{site.data.keyword.discoveryfull}} oferece recursos poderosos de procura de
conteúdo. Depois que seu conteúdo é transferido por upload e enriquecido pelo serviço do
{{site.data.keyword.discoveryshort}}, é possível construir consultas e, em seguida, integrar o
{{site.data.keyword.discoveryshort}} em seus próprios projetos ou criar um aplicativo customizado
usando o {{site.data.keyword.watson}} Explorer Application Builder.
{: shortdesc}

  As consultas que você grava variam de acordo com a coleção, já que todas as coleções possuem conteúdo
exclusivo.
  {: tip}

Ao criar uma consulta ou um filtro, o {{site.data.keyword.discoveryshort}} examina cada
resultado e tenta corresponder os caminhos que você definiu. Quando correspondências ocorrem, elas são incluídas no
conjunto de resultados. Ao criar uma consulta, é possível ser tão vago ou tão específico quanto quiser. Quanto
mais específica for a consulta, mais direcionados serão os resultados.

Também há a opção para ativar a recuperação de passagem. As passagens são curtas, excertos relevantes extraídos dos documentos completos retornados pela sua consulta. Essas passagens direcionadas são extraídas dos campos `text` dos documentos em sua coleção. Por padrão, até 10 passagens de cerca de 400 caracteres cada serão retornadas para uma consulta. No máximo
três passagens são extraídas de um único resultado. O parâmetro `passages` está
disponível somente para coleções privadas; ele não está disponível na
coleção do {{site.data.keyword.discoverynewsshort}}. Consulte [Passages](//docs/services/discovery?topic=discovery-query-parameters#passages) para obter mais
informações sobre como as passagens são identificadas.

  É possível gravar consultas de linguagem natural (como "Parcerias do IBM Watson") usando
o conjunto de ferramentas do {{site.data.keyword.discoveryshort}} ou a API.
  {: tip}

Todas as coleções privadas retornarão uma pontuação de `confidence` nos resultados da consulta na maioria dos casos. Consulte [Pontuações de confiança](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence) para obter detalhes.

O {{site.data.keyword.discoveryshort}} retorna os resultados da consulta que incluem caracteres especiais para os idiomas a seguir: inglês, alemão, francês, holandês, italiano e português. Por exemplo, se você consultar `aqui`, agora receberá os resultados para `aqui` e <code>aqu&iacute;</code>.

É possível criar consultas mais longas e mais complexas que incluem múltiplos filtros e agregações complexas. Essa opção está disponível somente na API e aumentará o limite de caractere de uma consulta para 10.000 caracteres. Veja [Consultas longas de coleção ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#long-collection-queries){: new_window} e [Consultas longas do ambiente ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#long-environment-queries){: new_window} para obter detalhes.

{{site.data.keyword.discoveryfull}} Knowledge Graph é um recurso beta que fornece novos terminais para consultas de entidades e de relações entre documentos. Isso inclui buscas baseadas em contexto e classificação de relevância. Consulte [{{site.data.keyword.discoveryfull}} Gráfico de conhecimento](/docs/services/discovery?topic=discovery-kg#kg) para obter mais informações.

Para obter informações sobre como criar consultas, consulte:
- [Introdução ao tutorial de
consultas](/docs/services/discovery?topic=discovery-getting-started-with-querying#getting-started-with-querying)
- [Referência de consulta](/docs/services/discovery?topic=discovery-query-reference#query-reference) (inclui a lista de parâmetros, de operadores e de agregados disponíveis na linguagem de consulta do {{site.data.keyword.discoveryshort}})

## O esquema de dados do Discovery
{: #discovery-schema}

Comece conhecendo o {{site.data.keyword.discoveryshort}} JSON. Para entender como construir uma
consulta usando o {{site.data.keyword.discoveryshort}} Query Language, é necessário estar
familiarizado com o JSON produzido pelo {{site.data.keyword.discoveryshort}} depois que enriquece os
documentos em sua coleção. Quando você estiver familiarizado com o esquema de dados de seus documentos, será
mais fácil gravar consultas no {{site.data.keyword.discoveryshort}} Query Language. Há três maneiras
de fazer isso.

  1. No {{site.data.keyword.discoveryshort}} Tooling, abra a tela **Gerenciar
dados** e escolha a coleção que contém as Press Releases da {{site.data.keyword.IBM_notm}}. Clique no botão **Visualizar esquema de dados**. A tela **Visualizar esquema
de dados** exibe os campos e valores em seus documentos transformados duas maneiras: pelo
documento (**Visualização de documento**) ou pelo campo (**Visualização
de coleção**). No máximo 50 documentos são exibidos na **Visualização de
documentos**. A **Visualização de coleção** exibe os campos na
coleção inteira.

    Na **Visualização de coleção**, em `enriched_text`, é possível examinar os enriquecimentos aplicados à sua coleção. Clique em `categories`, `concepts`, `entities` e `sentiment` para ver como sua coleção foi enriquecida com o Watson Insights.

  1. Execute uma consulta "vazia" para visualizar o JSON. Na tela **Visualizar esquema de
dados**, clique no botão **Construir consultas** e, em seguida, clique em
**Executar consulta**. Os resultados são exibidos à direita, em duas guias:
**Resumo** (uma visão geral dos resultados da consulta) e **JSON**. Comece abrindo a guia **JSON**.

     -  Cada um dos quatro documentos será precedido por um número de `id`,
     -  Role até o campo `enriched_text`. Examine cada enriquecimento para aprender
sobre os campos JSON que podem ser consultados.

        ![Campos de configuração padrão](images/JSON.png)

     -  **entidades** - comece localizando o campo `text` e
examine as outras informações de enriquecimento.
     -  **impressão** - comece localizando o campo `label` e
examine as outras informações de enriquecimento.
     -  **conceitos** - comece localizando o campo `text` e
examine as outras informações de enriquecimento.
     -  **categorias** - comece localizando o campo `document`
e examine as outras informações de enriquecimento.

     Depois de ter examinado os insights no primeiro documento, será possível observar outros três
documentos, se desejar.

  1. Visualize os campos disponíveis no **Visual Query Builder**. Na
tela **Construir consultas**, clique em **Procurar por documentos** e
depois em **Usar o {{site.data.keyword.discoveryshort}} Query Language**. Clique no
menu suspenso **Campo** para visualizar os campos disponíveis em seus dados. Clique em
**Editar na linguagem de consulta** para construir as consultas manualmente usando o
{{site.data.keyword.discoveryshort}} Query Language.      

### Como estruturar uma consulta básica
{: #structure-basic-query}

Como você observou, o JSON é hierárquico, portanto, as consultas precisam ser gravadas usando essa mesma
hierarquia. Assim, seu JSON será semelhante a este:

```json
"enriched_text": {
  "concepts": [ {
    "text": "Cloud computing",
    "relevance": 0.610029}
    ]
  }
```
{: codeblock}

Sua consulta seria estruturada como esta:

![Exemplo de estrutura de consulta](images/query_structure2.png)

  Operadores que avaliam um campo (`<=` , `>=`, `<`, `>`) requerem um `number` ou `date` como o valor. O uso de cotações em torno de um valor sempre o torna uma `string`. Portanto, `score>=0.5` é uma consulta válida e `score>="0.5"` não é. Veja [Operadores de consulta](/docs/services/discovery?topic=discovery-query-operators#query-operators) para obter uma lista completa de operadores.
  {: tip}

Considerações:

- Não sabe quando consultar em uma entidade, conceito ou palavra-chave? Consulte
[Entendendo a diferença entre Entidades, Conceitos e
Palavras-chave](/docs/services/discovery?topic=discovery-configservice#udbeck).

- **Nota:** depois de clicar em **Executar consulta** e abrir a
guia **JSON**, você observará que o destaque da consulta é ativado por padrão. Isso
incluirá um campo `highlight` nos seus resultados da consulta. No campo `highlight`, as palavras que corresponderem à sua consulta serão agrupadas nas tags `<em>` (ênfase) HTML. Consulte os [Parâmetros de consulta](/docs/services/discovery?topic=discovery-query-parameters#highlight) para obter detalhes.

## Construir consultas combinadas
{: #building-combined-queries}

É possível combinar parâmetros de consulta para construir mais consultas direcionadas. Por exemplo, é possível usar os parâmetros `filter` e `query` juntos. Para obter mais informações sobre filtragem e consulta, veja [Diferenças entre os parâmetros de filtro e de consulta](/docs/services/discovery?topic=discovery-query-parameters#filtervquery).

## Como estruturar uma agregação
{: #structure-aggregation}

As agregações retornam um conjunto de valores de dados; por exemplo, palavra-chaves principais, impressão geral de entidades e mais. Para obter a lista completa de opções de agregação, consulte [Agregações](/docs/services/discovery?topic=discovery-query-reference#aggregations).

![Exemplo de estrutura de consulta de agregação](images/aggregation_structure.png)

Essa agregação de exemplo localizará todos os `Conceitos` em sua coleção.
O delimitador nesta consulta é `.` e o operador é `()`, veja [Operadores de consulta](/docs/services/discovery?topic=discovery-query-operators#query-operators) para aprender sobre outros operadores disponíveis no {{site.data.keyword.discoveryshort}} Query Language.

### Exemplo de consultas de agregação
{: #example-aggregations}

Há várias maneiras de agregar resultados com o {{site.data.keyword.discoverynewsshort}}, incluindo valores principais, soma, mínima, máxima, média, fatia de tempo e histograma. Também é possível incluir filtros e agregações aninhadas.

#### Filtrar agregações
{: #filter-aggregations}

Essa agregação de exemplo retorna o número de artigos localizados no {{site.data.keyword.discoverynewsshort}} sobre o Pittsburgh Steelers e quantos desses resultados possuem um sentimento `positive`, `negative` ou `neutral`.

- `filter(enriched_text.entities.text:"Pittsburgh Steelers").term(enriched_text.sentiment.document.label,count:3)`


Essa agregação de exemplo primeiro limitará (filtrará) um conjunto de artigos no {{site.data.keyword.discoverynewsshort}} a somente aqueles que incluem o texto de entidades de `twitter` e, em seguida, dividirá esses artigos pelos tipos de sentimento do documento. Apenas os 3 principais tipos de impressão do documento (`positive`, `negative` e
`neutral`) serão retornados.

- `filter(enriched_text.entities.text:twitter).term(enriched_text.sentiment.document.label,count:3)`

#### Agregações aninhadas
{: #nested-aggregations}

A inclusão de `nested` antes de uma agregação restringe a agregação para a área dos resultados especificados. Por exemplo: `nested(enriched_text.entities)` significa que somente os componentes `enriched_text.entities` de qualquer resultado são usados para agregação.

Isso pode ser visto facilmente observando as diferenças entre as duas consultas a seguir:
- `filter(enriched_text.entities.disambiguation.subtype::City)` - a agregação conta o número de *Resultados* que contêm uma `entity` ou mais com o tipo `City`
- `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City)` - a agregação conta o número de instâncias de uma `entity` com o tipo `City` nos resultados.  

Além disso, qualquer operação subsequente restringirá ainda mais o conjunto de resultados que pode ser agregado. Por exemplo:

- `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City)` significa que apenas as entidades de `subtype::City` serão agregadas.
- `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City).term(enriched_text.entities.text,count:3)` agregará as 3 principais entidades de subtipo `City`
- `filter(enriched_text.entities.disambiguation.subtype::City).term(enriched_text.entities.text,count:3)` retornará as 3 principais entidades em que o resultado contém pelo menos uma entidade de subtipo `City`.

## Consultando o Watson Discovery News
{: #querying-news}

{{site.data.keyword.discoverynewsshort}}, um conjunto de dados públicos que foi pré-enriquecido com insights cognitivos, também está incluído com o {{site.data.keyword.discoveryshort}}. Consulte [Watson Discovery News](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news) para obter mais informações sobre esta coleção.

É possível consultar esta coleção usando consultas de linguagem natural, por exemplo, "Parcerias do IBM Watson" ou o {{site.data.keyword.discoveryshort}} Query Language. Para saber mais sobre consultas de linguagem natural, veja a [Consulta de linguagem natural](/docs/services/discovery?topic=discovery-query-parameters#nlq).

Não é possível ajustar a configuração do {{site.data.keyword.discoverynewsshort}}, treinar ou incluir documentos na coleção do {{site.data.keyword.discoverynewsshort}}. Veja uma demonstração do que você pode construir com o {{site.data.keyword.discoverynewsshort}} [aqui ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://discovery-news-demo.ng.bluemix.net/){: new_window}.

As coleções do {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} nos idiomas inglês, coreano, alemão, espanhol e japonês estão disponíveis por meio do conjunto de ferramentas do {{site.data.keyword.discoveryshort}} e da API.

O idioma padrão do {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} no conjunto de ferramentas é inglês. Para alternar o idioma, deve-se primeiro clicar no ícone ![Gerenciar dados](/images/icon_yourData.png) e, em seguida, escolher o idioma apropriado na lista suspensa.

Para obter informações sobre como consultar uma coleção por meio da API, consulte [Referência da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#query-your-collection){: new_window}. O `collection_id` da versão em inglês do Watson {{site.data.keyword.discoverynewsshort}} é `news-en`. Anteriormente, o `collection_id` era `news` - se você estiver usando o `collection_id` anterior, ele continuará funcionando, no entanto, será possível mudar para o novo, `collection_id` para novos projetos. O `collection_id` da coleção em coreano é `news-ko`, o `collection_id` em espanhol é `news-es`, o `collection_id` em alemão é `news-de`, o `collection_id` em japonês é `news-ja`.

As consultas do {{site.data.keyword.discoverynewsfull}} exibem as primeiras 50 palavras de cada artigo no campo da JSON `text`.

O número máximo de resultados retornados para uma consulta do {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} é `50`. Use as consultas adicionais e o parâmetro `offset` para retornar mais do que `50` resultados.

Se estiver usando o {{site.data.keyword.discoveryshort}} Query Language, será possível incluir um intervalo de data relativo em suas consultas do {{site.data.keyword.discoverynewsshort}}, por exemplo: `crawl_date>=now-1month`. Os valores de intervalo de data válida são `second/seconds` `minute/minutes`, `hour/hours`, `day/days`, `week/weeks`, `month/months` e `year/years`. O parâmetro `now` não é afetado pelo parâmetro `time_zone` e o
fuso horário `UTC` é o padrão.

Este exemplo será consultado para uma palavra-chave dentro de um intervalo de data específico. As informações de fuso horário não são necessárias:
- ` enriched_text.keywords.text: "olympics ", publication_date<=2018-02-15T00:00:00Z, publication_date>= 2018-02-01T00:00:00Z `

Os artigos de notícias podem ser organizados em vários meios de comunicação e {{site.data.keyword.discoverynewsfull}} escolherá cada um deles, resultando em artigos duplicados. Isso significa que uma consulta ao {{site.data.keyword.discoverynewsfull}} pode retornar potencialmente vários artigos idênticos ou quase idênticos nos resultados da consulta. É possível gerenciar isso usando deduplicação. Para saber mais sobre o recurso beta, consulte [Excluindo documentos beta de resultados da consulta](/docs/services/discovery?topic=discovery-query-parameters#deduplication).

## Consultando múltiplas coleções
{: #multiple-collections}

Se você tiver múltiplas coleções em seu ambiente, talvez deseja visualizar os resultados nessas coleções. Os métodos de consulta (`query`, `files` e `notices`) no nível `environment` permitem consultar múltiplas coleções especificadas. A consulta entre as coleções não está disponível atualmente no
conjunto de ferramentas do {{site.data.keyword.discoveryshort}}.

É possível consultar múltiplas coleções no mesmo ambiente usando o método da API `environments/{environment_id}/query`. Ao consultar em múltiplas coleções, leve em consideração os seguintes itens.
-  O parâmetro `collection_ids` deve ser especificado ao usar esse método. `collection_ids` é uma lista de coleções separadas por vírgulas no ambiente a ser consultado.
-  `passages` são suportadas ao consultar múltiplas coleções.
-  `collection_id` é retornado como parte de cada objeto de resultado. Esse campo especifica a coleção na qual o resultado foi localizado.
-  O {{site.data.keyword.discoverynewsshort}} faz parte do ambiente `system` e não pode ser incluído em consultas de múltiplas coleções.
-  O treinamento de relevância de coleção individual não afeta a classificação de resultados ao consultar múltiplas coleções. Para reclassificar os resultados retornados ao consultar múltiplas coleções, implemente o [Continuous Relevancy Training](/docs/services/discovery?topic=discovery-crt#crt).
-  A reclassificação não é executada em nenhuma parte de uma consulta de múltiplas coleções, mesmo se todas as coleções na consulta tiverem sido treinadas.

Consulte a [Referência da API de consulta de múltiplas coleções ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#query-documents-in-multiple-collections){: new_window} para obter mais informações.

É possível visualizar avisos em múltiplas coleções no mesmo ambiente usando o método da API `environments/{environment_id}/notices`.
-  O parâmetro `collection_ids` deve ser especificado ao usar esse método. `collection_ids` é uma lista de coleções separadas por vírgulas no ambiente a ser consultado.
-  `passages` são suportadas ao consultar múltiplas coleções.

Veja [Referência da API de avisos de múltiplas coleções ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#get-collection-details){: new_window} para obter mais informações.

É possível visualizar os campos disponíveis nas coleções no mesmo ambiente usando o método da API `environments/{environment_id}/fields`. Veja [Referência da API de consulta de campo de múltiplas coleções ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#list-fields-across-collections){: new_window} para obter mais informações.

## Expansão de consulta
{: #query-expansion}

É possível expandir o escopo de uma consulta além de correspondências exatas. Por exemplo, é possível expandir uma consulta para "carro" para incluir "automóvel" e "veículo", fazendo upload de uma lista de termos de expansão de consulta usando a API do {{site.data.keyword.discoveryshort}}. Os termos de expansão de consulta são geralmente sinônimos, antônimos ou erros típicos de ortografia para termos comuns.

É possível definir dois tipos de expansões:
-  **bidirecional** - cada `expanded_term` será expandido para incluir todos os termos expandidos. Por exemplo, uma consulta para `car` se expandiria para `car OR automobile OR vehicle`).
-  **unidirecional** - os `input_terms` na consulta serão substituídos pelos `expanded_terms`. Por exemplo, uma consulta para `banana` pode se expandir para `plaintain` e `fruit`. Os `input_terms` não são usados como parte da consulta resultante. No exemplo de `banana` anterior, a consulta `banana` seria convertida para `plantain` OU `fruit` e não conteria o termo original.

Esse arquivo pode ser usado como um ponto de início ao construir uma lista de expansões de consulta:
<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/expansions.json" download>expansions.json <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo"></a>. É possível modificar esse arquivo para criar sua lista de expansões de consulta customizada.

Exemplo bidirecional:
```JSON
 {
   "expansions": [ {
       "expanded_terms": [
         "car",
         "automobile",
         "vehicle"
       ]
     }
   ]
 }
```
{: codeblock}

Exemplo unidirecional:
```JSON
 {
   "expansions": [ {
      "input_terms": [
        "Banana"
       ], "expanded_terms": [
        "banana",
         "plantain",
         "fruit"
       ]
     }
   ]
 }
```
{: codeblock}

Notas sobre expansão de consulta:

-  A expansão de consulta de vários tokens não é suportada.
-  A expansão de consulta está disponível somente para coleções privadas. O número de matrizes `expansions` disponíveis (total de matrizes bidirecionais e unidirecionais) e os termos (o total de `input_terms` mais `expanded_terms`) varia por plano. Consulte  [ Planos de precificação de descoberta ](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)  para obter detalhes. **Nota:** todos os termos de consulta (` input_terms ` e `expanded_terms`) contam, cada um, como um termo. Esse exemplo contém dois objetos na matriz `expansions` e sete sequências de termo.

```JSON
 {
   "expansions": [ {
      "input_terms": [
         "ibm"
       ], "expanded_terms": [
         "ibm",
         "watson"
       ]
     },
     {
      "input_terms": [
         "Banana"
       ], "expanded_terms": [
         "banana",
         "plantain",
         "fruit"
       ]
     }
   ]
 }
```
{: codeblock}

-  Somente uma lista de expansões de consulta pode ser transferida por upload por coleção; se uma segunda lista de expansões for transferida por upload, ela substituirá a primeira.
-  Todos os `input_terms` e `expanded_terms` devem estar em minúsculas. Termos de minúsculas serão expandidos para maiúscula.
-  A lista de expansões de consulta deve ser gravada em JSON.
-  Para desativar a expansão de consulta, exclua a lista de expansões de consulta.
-  Não é possível fazer upload ou excluir atualmente de uma lista de expansões de consulta usando o conjunto de ferramentas do {{site.data.keyword.discoveryshort}}; isso deve ser feito usando a API do {{site.data.keyword.discoveryshort}}.
-  A expansão de consulta é executada nos métodos `query` e `multiple collection query`. A expansão de consulta não é executada nas consultas do Knowledge Graph.
-  Cada conjunto de expansões está associado a uma coleção. Ao consultar em [múltiplas coleções](/docs/services/discovery?topic=discovery-query-concepts#multiple-collections), cada coleção é expandida individualmente.
-  As expansões de consulta são aplicadas no momento da consulta, não durante a indexação, de modo que a lista de expansões possa ser atualizada sem a necessidade de realimentar seus documentos.
-  Não faça upload ou exclua uma lista de expansões de consulta ao mesmo tempo em que os documentos estão sendo alimentados em sua coleção. Isso pode fazer com que o índice fique indisponível por esse breve período.

Veja a [Referência da API de expansão de consulta ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#get-the-expansion-list){: new_window} para os comandos da API para fazer upload e excluir arquivos de expansão de consulta.

## Definindo palavras-chave
{: #stopwords}

Palavras vazias são palavras filtradas de consultas porque acrescem pouco valor, por exemplo: `a, an, the`. A inclusão de palavras comuns em uma lista de palavras vazias também pode melhorar a relevância dos resultados para consultas de língua natural. 

O {{site.data.keyword.discoveryshort}} aplica uma lista padrão de palavras vazias para vários idiomas no tempo de consulta. No entanto, é possível definir e fazer upload de uma lista customizada de palavras vazias que substituirão a lista padrão. O {{site.data.keyword.discoveryshort}} aplicará a lista de palavras vazias padrão ou customizada apropriada para suas coleções privadas com base no idioma especificado para essa coleção. 

A sua lista de palavras vazias customizadas deve ser um arquivo `txt` separado por uma nova linha. Exemplo de lista de stopword customizada:

```
ibm
watson
a
an
the
what
how
when
can
should
```
Essa lista contém todas as palavras vazias padrão em inglês <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/custom_stopwords_en.txt" download>custom_stopwords_en.txt <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo"></a>. Ela pode ser usada como um ponto de início ao construir uma lista de palavras vazias customizadas em inglês. A criação de uma lista de palavras vazias customizadas que não inclui termos muito comuns, como `a` e `the`, pode levar a um desempenho de consulta reduzido, portanto, é recomendado que você mantenha essas palavras em sua lista de palavras vazias customizadas. A seguir estão as listas de palavras vazias para vários outros idiomas suportados. Todas elas incluem as palavras vazias padrão para esse idioma:

-  Holandês: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/custom_stopwords_nl.txt" download>custom_stopwords_nl.txt <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo"> </a>.
-  Francês: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/custom_stopwords_fr.txt" download>custom_stopwords_fr.txt <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo"> </a>.
-  Alemão: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/custom_stopwords_de.txt" download>custom_stopwords_de.txt <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo"> </a>. 
-  Italiano: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/custom_stopwords_it.txt" download>custom_stopwords_it.txt <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo"> </a>.
-  Japonês: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/custom_stopwords_ja.txt" download>custom_stopwords_ja.txt <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo"> </a>.
-  Espanhol: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/custom_stopwords_es.txt" download>custom_stopwords_es.txt <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo"> </a>. 

Veja [Suporte ao idioma](/docs/services/discovery?topic=discovery-language-support#supported-languages) para obter a lista de idiomas suportados pelo {{site.data.keyword.discoveryshort}}. Vários idiomas suportados não têm uma lista de palavras vazias padrão.

Consulte a [referência de API de palavras vazias ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#create-stopword-list){: new_window} para obter os comandos de API que serão transferidos por upload e excluir as listas de palavras vazias customizadas.

Notas sobre stopwords:

-  Atualmente, não é possível fazer upload ou excluir uma lista de palavras vazias customizadas usando o conjunto de ferramentas do {{site.data.keyword.discoveryshort}}. Essas ações devem ser feitas usando a API do {{site.data.keyword.discoveryshort}}. Consulte a [referência de API de palavras vazias ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#create-stopword-list){: new_window}.
-  Fazer upload de uma lista de palavras vazias customizadas está disponível somente para coleções privadas em planos `Advanced` e `Premium`.
-  O limite de tamanho para um arquivo `txt` de lista de palavras vazias customizadas é de um milhão de caracteres. No entanto, se você fizer upload de uma lista de palavras vazias customizadas com um grande número de termos, a precisão da procura poderá ser afetada negativamente. O número de palavras é dependente do idioma, dos conteúdos do documento e das palavras escolhidas. Uma boa prática seria manter sua lista de palavras vazias abaixo de `200` palavras no total. 
-  Somente uma lista de palavras vazias customizadas pode ser transferida por upload por coleção. Se uma segunda lista de palavras vazias customizadas for transferida por upload, ela substituirá a primeira.
-  Todas as interruphas devem estar em minúsculas. 
-  Para desativar a lista de palavras vazias customizadas, exclua-a.
-  Não faça upload ou exclua uma lista de palavras vazias customizadas ao mesmo tempo em que os documentos estão sendo alimentados em sua coleção. Isso pode fazer com que o índice fique indisponível por esse breve período.
-  As palavras vazias são removidas do índice e do tempo de consulta. Uma boa prática é fazer upload de sua lista de palavras vazias customizadas antes de fazer upload dos documentos.
   - Se seus documentos já tiverem sido indexados com as palavras vazias padrão e, em seguida, você incluir uma lista de palavras vazias customizadas, as novas palavras vazias ainda serão incluídas no índice. Nesse caso, as consultas que contiverem essas novas palavras vazias filtrarão essas palavras no tempo de consulta.
   - Se um usuário procurar uma palavra que foi uma palavra vazia em algum momento, mas desde então foi removida da lista de palavras vazias customizadas, ele não localizará documentos correspondentes à palavra vazia original porque o termo foi removido no tempo de índice. Para corrigir esse problema, exclua os documentos em sua coleção e refaça o upload de todos os documentos para que eles sejam indexados com a lista de palavras vazias customizadas atualizada.
-  Cada conjunto de palavras vazias está associado a uma coleção. Ao consultar em múltiplas coleções, cada coleção usará a lista de palavras vazias customizadas associada a essa coleção.
- Se você fizer mudanças significativas em sua lista de palavras vazias customizadas, será necessário excluir os documentos em sua coleção e refazer o upload de todos os documentos para que eles sejam indexados com a lista de palavras vazias customizadas atualizada.

## Criando dicionários de tokenização customizados
{: #tokenization}

A tokenização quebra o texto em unidades chamadas de tokens. Um dicionário de tokenização padrão é aplicado às suas coleções, mas é possível melhorar a precisão da procura para seu domínio ou idioma fazendo upload de um dicionário de tokenização customizado. Seu dicionário customizado substituirá o dicionário padrão. É possível fazer upload de seu dicionário usando a API do {{site.data.keyword.discoveryshort}}. 

Veja a [Referência da API de tokenização ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#create-tokenization-dictionary){: new_window} para os comandos da API para fazer upload e excluir arquivos de tokenização. 

**Nota:** esse recurso está disponível atualmente somente para coleções em japonês. 

No exemplo abaixo, **text** é a frase que será convertida em token quando encontrada e **tokens** são as palavras pelas quais o **texto** será dividido (elas devem ser definidas individualmente). **Leituras** lista a versão dos tokens representados por um conjunto de caracteres diferente e **part_of_speech** é a parte do discurso que os tokens representam.

Com esse dicionário customizado, se você procurar este texto: `??`, os resultados da procura incluirão o texto contendo `????`, bem como o texto contendo somente `??`.

```
{ "tokenization_rules":
  [
     {
      "text":"すし",
      "tokens":[
        "すし"
      ],
      "readings":[
        "寿司"
      ],
      "part_of_speech":"カスタム名詞"
    },
    {
      "text":"ネコ",
      "tokens":[
        "ネコ"
      ],
      "readings":[
        "ネコ"
      ],
      "part_of_speech":"カスタム名詞"
    }
```

Com esse dicionário customizado, é possível criar regras com um único token. Neste exemplo, o `ibm発見` será tokenizado como um único token, portanto, ele não será dividido em unidades menores.

```
{ "tokenization_rules":
  [
    {
      "text":"ibm発見",
      "tokens":[
      "ibm発見"
      ],
      "readings":[
      "ibm発見"
      ],
      "part_of_speech":"カスタム名 詞"
    },
    ...
  ]
}
```

-  A tokenização ocorre no tempo de índice e de consulta.
-  Tokens devem ser definidos individualmente.
-  Um dicionário de tokenização padrão é usado em todas as coleções. Se sua coleção já foi indexada a esse dicionário, deve-se realimentar os documentos nessa coleção depois de fazer upload de um dicionário de tokenização customizado.
-  O upload de um dicionário de tokenização está disponível somente para as coleções privadas nos planos `Advanced` e `Premium`. 
-  Somente um dicionário de tokenização pode ser transferido por upload por coleção; se um segundo dicionário de tokenização for transferido por upload, ele substituirá o primeiro. Se essa coleção já continha documentos, deve-se realimentá-los para que o novo dicionário de tokenização customizado seja aplicado.
-  O dicionário de tokenização customizado deve ser gravado em JSON; nome do arquivo de exemplo: `custom_tokenization_dictionary.json`.
-  Todos os termos do dicionário de tokenização customizado devem estar em minúsculas.
-  Para desativar a tokenização, exclua o dicionário de tokenização e realimente seus documentos.
-  Não é possível fazer upload ou excluir atualmente um dicionário de tokenização usando o conjunto de ferramentas do {{site.data.keyword.discoveryshort}}; isso deve ser feito usando a API do {{site.data.keyword.discoveryshort}}.
-  A tokenização é executada nos métodos `query` e `multiple collection query`. A tokenização não é executada nas consultas do Knowledge Graph.
-  Cada dicionário de tokenização está associado a uma coleção. Ao consultar em [múltiplas coleções](/docs/services/discovery?topic=discovery-query-concepts#multiple-collections), cada coleção é tokenizada individualmente.
-  Não faça upload ou exclua um dicionário de tokenização ao mesmo tempo em que os documentos estão sendo alimentados em sua coleção. 

## Similaridade do documento
{: #doc-similarity}

Uma consulta de similaridade de documento localizará outros documentos semelhantes ao documento atualmente visualizado, por exemplo, um operador de central de atendimento poderia estar visualizando os manuais para um produto e usar a similaridade de documentos para localizar outros documentos com características semelhantes. É possível consultar documentos semelhantes por `similar.document_ids` e, opcionalmente, refinar a similaridade especificando `similar.fields` adicionais.

A similaridade de documento é determinada extraindo os 25 termos mais relevantes do documento original e, em seguida, procurando documentos com termos relevantes semelhantes.

Exemplo de consulta por `similar.document_ids` (não deve haver espaço após a vírgula se especificar múltiplos `similar.document_ids`):

` curl -u "apikey }" "https: //gateway.watsonplatform.net/discovery/api/v1/environments/ {2}{0}{1}{7}-11-07&similar.document_ids=4107b6f1-5d3f-5d3f-5bea-fb05bbf960b1, 6057k6d1-7d7k-7d7k-7d7k-7d7k-cfbb-bbb-kj98ssf786c2" `

Consulta de exemplo com  ` similar.fields `  incluída:

`curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&similar.document_ids=4107b6f1-5d3f-4bea-bbcf-fb05bbf960b1&similar.fields=title&return=title&count=100"`

Veja a [Referência da API de similaridade de documento ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#query-your-collection){: new_window} e [parâmetros de consulta](/docs/services/discovery?topic=discovery-query-parameters#similar) para obter mais informações.
