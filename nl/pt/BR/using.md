---

copyright:
  years: 2015, 2017
lastupdated: "2017-12-15"

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

# Conceitos de consulta

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

Também há a opção para ativar a recuperação de passagem. As passagens são curtas, excertos relevantes extraídos dos documentos completos retornados pela sua consulta. Essas passagens direcionadas são extraídas dos campos `text` dos documentos em sua coleção. 
Por padrão, até 10 passagens de cerca de 400 caracteres cada serão retornadas para uma consulta. No máximo
três passagens são extraídas de um único resultado. O parâmetro `passages` está
disponível somente para coleções privadas; ele não está disponível na
coleção do {{site.data.keyword.discoverynewsshort}}.
Consulte [Passages](/docs/services/discovery/query-parameters.html#passages) para obter mais
informações sobre como as passagens são identificadas.

  É possível gravar consultas de linguagem natural (como "Parcerias do IBM Watson") usando
o conjunto de ferramentas do {{site.data.keyword.discoveryshort}} ou a API.
  {: tip}

Coleções treinadas retornarão uma pontuação de `confidence` no resultado de uma consulta de linguagem natural. Consulte [Pontuações de confiança](/docs/services/discovery/train-tooling.html#confidence) para obter detalhes.

{{site.data.keyword.discoveryfull}} Visual Insights é um recurso experimental que pode ser usado para explorar visualmente as conexões identificadas pelo entendimento do {{site.data.keyword.discoveryshort}} de elementos de semântica, relações, conceitos e mais. Para obter mais informações, consulte [{{site.data.keyword.discoveryfull}} Visual Insights](/docs/services/discovery/visual-insights.html).

{{site.data.keyword.discoveryfull}} Knowledge Graph é um recurso beta que fornece novos terminais para consultas de entidades e de relações entre documentos. Isso inclui buscas baseadas em contexto e classificação de relevância. Consulte [{{site.data.keyword.discoveryfull}} Gráfico de conhecimento](/docs/services/discovery/building-kg.html) para obter mais informações.

Para obter informações sobre como criar consultas, consulte:
- [Introdução ao tutorial de
consultas](/docs/services/discovery/getting-started-query.html)
- [Referência de consulta](/docs/services/discovery/query-reference.html) (inclui a lista de parâmetros, de operadores e de agregados disponíveis na linguagem de consulta do {{site.data.keyword.discoveryshort}})

## O esquema de dados do Discovery
{: #discovery-schema}

Comece conhecendo o {{site.data.keyword.discoveryshort}} JSON. Para entender como construir uma
consulta usando o {{site.data.keyword.discoveryshort}} Query Language, é necessário estar
familiarizado com o JSON produzido pelo {{site.data.keyword.discoveryshort}} depois que enriquece os
documentos em sua coleção. Quando você estiver familiarizado com o esquema de dados de seus documentos, será
mais fácil gravar consultas no {{site.data.keyword.discoveryshort}} Query Language. Há três maneiras
de fazer isso.

  1. No {{site.data.keyword.discoveryshort}} Tooling, abra a tela **Gerenciar
dados** e escolha a coleção que contém as Press Releases da {{site.data.keyword.IBM_notm}}.
Clique no botão **Visualizar esquema de dados**. A tela **Visualizar esquema
de dados** exibe os campos e valores em seus documentos transformados duas maneiras: pelo
documento (**Visualização de documento**) ou pelo campo (**Visualização
de coleção**). No máximo 50 documentos são exibidos na **Visualização de
documentos**. A **Visualização de coleção** exibe os campos na
coleção inteira.

    Na **visualização de Coleção**, em `enriched_text`, é possível examinar os enriquecimentos que você aplicou com o arquivo de **Configuração padrão**. Clique em `categories`, `concepts`, `entities` e `sentiment` para ver como sua coleção foi enriquecida com o Watson Insights.

  1. Execute uma consulta "vazia" para visualizar o JSON. Na tela **Visualizar esquema de
dados**, clique no botão **Construir consultas** e, em seguida, clique em
**Executar consulta**. Os resultados são exibidos à direita, em duas guias:
**Resumo** (uma visão geral dos resultados da consulta) e **JSON**. 
Comece abrindo a guia **JSON**.

     -  Cada um dos quatro documentos será precedido por um número `id`.
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


Considerações:

- Não sabe quando consultar em uma entidade, conceito ou palavra-chave? Consulte
[Entendendo a diferença entre Entidades, Conceitos e
Palavras-chave](/docs/services/discovery/building.html#udbeck).

- **Nota:** depois de clicar em **Executar consulta** e abrir a
guia **JSON**, você observará que o destaque da consulta é ativado por padrão. Isso
incluirá um campo `highlight` nos seus resultados da consulta. No campo `highlight`, as palavras que corresponderem à sua consulta serão agrupadas nas tags `<em>` (ênfase) HTML. Consulte os [Parâmetros de consulta](/docs/services/discovery/query-parameters.html#highlight) para obter detalhes.

## Construir consultas combinadas
{: #building-combined-queries}

É possível combinar parâmetros de consulta para construir mais consultas direcionadas. Por exemplo, é possível usar os parâmetros `filter` e `query` juntos. Para obter mais informações sobre filtragem e consulta, veja [Diferenças entre os parâmetros de filtro e de consulta](/docs/services/discovery/query-parameters.html#filtervquery).

## Como estruturar uma agregação
{: #structure-aggregation}

As agregações retornam um conjunto de valores de dados; por exemplo, palavra-chaves principais, impressão geral de entidades e mais. Para obter a lista completa de opções de agregação, consulte [Agregações](/docs/services/discovery/query-reference.html#aggregations).

![Exemplo de estrutura de consulta de agregação](images/aggregation_structure.png)

Essa agregação de exemplo localizará todos os `Conceitos` em sua coleção.
O delimitador nesta consulta é `.` e o operador é `()`, veja [Operadores de consulta](/docs/services/discovery/query-operators.html) para aprender sobre outros operadores disponíveis no {{site.data.keyword.discoveryshort}} Query Language.

### Exemplo de consultas de agregação
{: #example-aggregations}

Há várias maneiras de agregar resultados com o {{site.data.keyword.discoverynewsshort}}, incluindo valores principais, soma, mínima, máxima, média, fatia de tempo e histograma. Também é possível incluir filtros e agregações aninhadas.

#### Filtrar agregações
{: #filter-aggregations}

Essa agregação de exemplo retorna o número de artigos localizados no {{site.data.keyword.discoverynewsshort}} sobre o Pittsburgh Steelers e quantos desses resultados possuem um sentimento `positive`, `negative` ou `neutral`.

- `filter(enriched_text.entities.text:"Pittsburgh Steelers").term(enriched_text.sentiment.document.label,count:3)`


Essa agregação de exemplo primeiramente limitará (filtrará) um conjunto de artigos no {{site.data.keyword.discoverynewsshort}} para somente aqueles que incluírem o texto de entidades do Twitter e, em seguida, dividirá esses artigos pelos tipos de impressão do documento. Apenas os 3 principais tipos de impressão do documento (`positive`, `negative` e
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

{{site.data.keyword.discoverynewsshort}}, um conjunto de dados públicos que foi pré-enriquecido com insights cognitivos, também está incluído com o {{site.data.keyword.discoveryshort}}. Consulte [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html#watson-discovery-news) para obter mais informações sobre esta coleção.

É possível consultar esta coleção usando consultas de linguagem natural, por exemplo, "Parcerias do IBM Watson" ou o {{site.data.keyword.discoveryshort}} Query Language. Para saber mais sobre consultas de linguagem natural, veja a [Consulta de linguagem natural](/docs/services/discovery/query-parameters.html#nlq).

Não é possível ajustar a configuração do {{site.data.keyword.discoverynewsshort}}, treinar ou incluir documentos na coleção do {{site.data.keyword.discoverynewsshort}}. Veja uma demonstração do que você pode construir com o {{site.data.keyword.discoverynewsshort}} [aqui ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://discovery-news-demo.mybluemix.net/){: new_window}.

A versão em inglês do Watson {{site.data.keyword.discoverynewsshort}} está disponível por meio do conjunto de ferramentas do {{site.data.keyword.discoveryshort}} e pela API. As versões nos idiomas coreano (`collection_id`: `news-ko`) e espanhol (`collection_id`: `news-es`) estão disponíveis para uso somente por meio da API. Para obter informações sobre como consultar uma coleção por meio da API, consulte [Referência da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection){: new_window}. 
O `collection_id` da versão em inglês do Watson {{site.data.keyword.discoverynewsshort}} é `news-en`. Anteriormente, o `collection_id` era `news` - se você estiver usando o `collection_id` anterior, ele continuará funcionando, no entanto, será possível mudar para o novo, `collection_id` para novos projetos.

**Observação:** o número máximo de resultados retornados para uma consulta do Watson Discovery News é `50`. Use as consultas adicionais e o parâmetro `offset` para retornar mais do que `50` resultados.

Se estiver usando o {{site.data.keyword.discoveryshort}} Query Language, será possível incluir um intervalo de data relativo em suas consultas do {{site.data.keyword.discoverynewsshort}}, por exemplo: `crawl_date>=now-1month`. Os valores de intervalo de data válida são `second/seconds` `minute/minutes`, `hour/hours`, `day/days`, `week/weeks`, `month/months` e `year/years`. O parâmetro `now` não é afetado pelo parâmetro `time_zone` e o
fuso horário `UTC` é o padrão.

Os artigos de notícias podem ser organizados em vários meios de comunicação e {{site.data.keyword.discoverynewsfull}} escolherá cada um deles, resultando em artigos duplicados. Isso significa que uma consulta ao {{site.data.keyword.discoverynewsfull}} pode retornar potencialmente vários artigos idênticos ou quase idênticos nos resultados da consulta. 
É possível gerenciar isso usando deduplicação. Para saber mais sobre o recurso beta, consulte [Excluindo documentos beta de resultados da consulta](/docs/services/discovery/query-parameters.html#deduplication).

## Consultando múltiplas coleções
{: #multiple-collections}

Se você tiver múltiplas coleções em seu ambiente, talvez deseja visualizar os resultados nessas coleções. Os métodos de consulta (`query`, `files` e `notices`) no nível `environment` permitem consultar múltiplas coleções especificadas. A consulta entre as coleções não está disponível atualmente no
conjunto de ferramentas do {{site.data.keyword.discoveryshort}}.

É possível consultar múltiplas coleções no mesmo ambiente usando o método da API `environments/{environment_id}/query`.
Ao consultar em múltiplas coleções, leve em consideração os seguintes itens.
-  O parâmetro `collection_ids` deve ser especificado ao usar esse método. `collection_ids` é uma lista de coleções separadas por vírgulas no ambiente a ser consultado.
-  `passages` e todos os subparâmetros não são suportados ao consultar várias coleções.
-  Um novo campo, `collection_id`, é retornado como parte de cada objeto de resultado. Esse campo especifica a coleção na qual o resultado foi localizado.
-  O {{site.data.keyword.discoverynewsshort}} faz parte do ambiente `system` e não pode ser incluído em consultas de múltiplas coleções.
-  A reclassificação não é executada em nenhuma parte de uma consulta de múltiplas coleções, mesmo se todas as coleções na consulta tiverem sido treinadas.

Consulte a [Referência da API de consulta de múltiplas coleções ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-multi-collections){: new_window} para obter mais informações.

É possível visualizar avisos em múltiplas coleções no mesmo ambiente usando o método da API `environments/{environment_id}/notices`.
-  O parâmetro `collection_ids` deve ser especificado ao usar esse método. `collection_ids` é uma lista de coleções separadas por vírgulas no ambiente a ser consultado.
-  `passages` e todos os subparâmetros não são suportados ao consultar várias coleções.

Veja [Referência da API de avisos de múltiplas coleções ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#collections-notices){: new_window} para obter mais informações.

É possível visualizar os campos disponíveis nas coleções no mesmo ambiente usando o método da API `environments/{environment_id}/fields`.
Veja [Referência da API de consulta de campo de múltiplas coleções ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#multi-list-fields){: new_window} para obter mais informações. 
