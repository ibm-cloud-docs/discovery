---

copyright:
  years: 2015, 2018
lastupdated: "2018-05-09"

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

# Agregações de consultas
{: #query-aggregations}

As agregações retornam um conjunto de valores de dados. Para obter a lista completa de agregações
disponíveis, consulte a [Referência de consulta](/docs/services/discovery/query-reference.html#aggregations).

## term
{: #term}

Retorna os valores superiores (por pontuação e por frequência) para os enriquecimentos selecionados. Todos os enriquecimentos são valores válidos. É possível, opcionalmente, usar `count` para
especificar o número de termos a serem retornados. O parâmetro `count` tem um valor padrão de 10. Este exemplo retorna o texto completo e os valores maiores
com o enriquecimento de conceito e especifica para retornar 10 termos.

Por exemplo:
```bash
term(enriched_text.concepts.text,count:10)
```
{: codeblock}

## filtro
{: #filter}

Um modificador que limita o conjunto de documentos da consulta de agregação que o precede. Este exemplo
filtra até o conjunto de documentos que incluem o conceito de computação em nuvem.

Por exemplo:
```bash
filter (enriched_text.concepts.text: "cloud computing ")
```
{: codeblock}

## nested
{: #nested}

A aplicação de aninhamento antes de uma consulta de agregação restringe a agregação para a área dos
resultados especificados. Por exemplo: `nested(enriched_text.entities)` significa que somente os componentes `enriched_text.entities` de qualquer resultado são usados para agregação.

Por exemplo:
```bash
nested(enriched_text.entities)
```
{: codeblock}

## histogram
{: #histogram}

Cria segmentos de intervalo numérico para categorizar documentos. Usa valores de campo de um campo
numérico único para descrever a categoria. O campo usado para criar o histograma deve ser um tipo numérico
(`integer`, `float`, `double` ou `date`). Tipos não numéricos, como `string`, não são suportados. Por exemplo, "price": 1,30 é um valor
numérico que funciona e "price": "1,30" é uma sequência, que não funciona. Use o
argumento `interval` para definir o tamanho das seções nas quais os resultados são divididos. Os valores do intervalo devem ser números inteiros não negativos configurados de maneira lógica
para segmentação de seus possíveis valores de campo. Por exemplo, se seu conjunto de dados incluir o preço de vários itens,
como: "price": 1,30, "price": 1,99 e "price": 2,99, será possível usar intervalos de 1, para que tudo
esteja agrupado entre 1 e 2 e entre 2 e 3. Provavelmente você não usaria um intervalo de 100, já que, desse modo,
todos os dados acabariam no mesmo segmento. Os histogramas podem processar valores decimais, mas os intervalos
devem ser números inteiros. A sintaxe é `histogram(<field>,<interval>)`, conforme mostrado no
exemplo a seguir.

Por exemplo:
```bash
histogram(product.price,interval:1)
```
{: codeblock}

## timeslice
{: #timeslice}

Um histograma especializado que usa datas para criar segmentos de intervalo. Os valores de intervalo de data válida são `second/seconds` `minute/minutes`, `hour/hours`, `day/days`, `week/weeks`, `month/months` e `year/years`. A
sintaxe é `timeslice(<field>,<interval>,<time_zone>)`. Para usar o
`timeslice`, os campos de tempo em seus documentos devem ser do tipo de
dados `date` e estar no formato [Horário do
UNIX![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://en.wikipedia.org/wiki/Unix_time){: new_window}. A menos que esses dois requisitos sejam atendidos, o parâmetro timeslice não funciona
corretamente. Será possível criar uma fatia de tempo se seus documentos contiverem os campos
`date` com valores como `1496228512`. O valor deve estar em um formato
numérico (por exemplo, `float` ou `double`) e não deve estar colocado entre
aspas. O serviço trata datas em texto e datas no formato ISO 8601 como o tipo de dados `string`, não
como o tipo de dados `data`. É possível detectar pontos irregulares nas agregações de
fatia de tempo. Consulte [Detecção de anomalias de fatia de tempo](#anomaly-detection)
para obter informações adicionais. Este exemplo retorna valores para "sales" ("product.sales") em
intervalos de 2 dias no fuso horário de Nova York.

Por exemplo:
```bash
timeslice(product.sales,2day,America/New York)
```
{: codeblock}

### Detecção de anomalias de fatia de tempo
{: #anomaly-detection}

Opcionalmente, é possível aplicar a detecção de anomalias aos resultados de uma agregação
`timeslice`. A detecção de anomalias é usada para localizar pontos de dados incomuns em uma
série temporal e sinalizá-los para revisão adicional. Exemplos de usos de detecção de anomalias incluem
identificação de picos no uso do cartão de crédito e procura do Watson Discovery News por clusters
de artigos sobre um tópico específico.

Para aplicar detecção de anomalias, use a seguinte sintaxe em sua agregação:

```bash
timeslice(field:<date>,interval:<interval>,anomaly:true)`
```
{: codeblock}

Se você especificar `anomaly:true` com a agregação `timeslice`,
a saída incluirá os dois campos adicionais a seguir, que são mostrados no exemplo.

  - `"anomaly": true` para indicar que a detecção de anomalias foi executada
  - Um campo `anomaly` nos pontos que estão irregulares na matriz de resultados
da saída. O campo de anomalia possui um valor do tipo de dados `float` indicando
a magnitude do comportamento anômalo. Quanto mais próximo o valor do campo de anomalia estiver de
`1`, mais provavelmente o resultado será anômalo.

  - O `key` e o `key_as_string` em cada um dos objetos na
matriz `results` correspondem a um registro de data e hora do UNIX em segundos.
  - A pontuação de anomalia é relativa a uma consulta, não a várias consultas.

```json
"type": "timeslice",
"field": "blekko.chrondate",
"interval": "1d",
"anomaly": true,
"results": [
  {
    "matching_results": 2933,
    "anomaly": 1,
    "key_as_string": "1496880000",
    "key": 1496880000000
  },
  {
    "matching_results": 3435,
    "anomaly": 1,
    "key_as_string": "1496966400",
    "key": 1496966400000
  },
  {
    "matching_results": 3692,
    "anomaly": 0.598226,
    "key_as_string": "1496016000",
    "key": 1496016000000
  },
  {
    "matching_results": 4551,
    "anomaly": 0.828498,
    "key_as_string": "1495411200",
    "key": 1495411200000
  },
  {
    "matching_results": 947,
    "key_as_string": "1489968000",
    "key": 1489968000000
  },
 ...
]
...
```
{: codeblock}

#### Limitações de detecção de anomalias

- A detecção de anomalias está disponível atualmente somente em agregações `timeslice`
de nível superior. Ela não está disponível em agregações de nível inferior (aninhadas).
- O número máximo de pontos que podem ser processados pela detecção de anomalias em qualquer
agregação `timeslice` especificada é `1500`.
- O número máximo de agregações de fatia de tempo de nível superior que podem ser processadas pela
detecção de anomalias é `20`.

<!--
#### Anomaly detection workflow

The following example workflow detects an anomaly for the text entity `London` and retrieves additional information about the anomalous datapoint.

  1. Timeslice aggregation: `query=entities.text:London&count=0&aggregation=timeslice(blekko.last_crawled,1day,anomaly:true)`
  1. Term aggregation to retrieve top keywords: `query=entities.text:London&count=0&aggregation=term(keywords.text,count:5)&filter=blekko.last_crawled>=1490140800,<=1490227200`
  1. Query to retrieve top enriched title: `query=entities.text:London,keywords.text:Westminster Bridge|police officer|people|Prime Minister Theresa|parliament&count=1&filter=blekko.last_crawled>=1490140800,<=1490227200&return=enrichedTitle.text`
  -->

## top_hits
{: #top_hits}

Retorna os documentos classificados pela pontuação da consulta ou do enriquecimento. Pode ser usado
com qualquer parâmetro de consulta ou agregação. Esse exemplo retorna as 10 principais ocorrências de uma
agregação de termo.

Por exemplo:
```bash
term(enriched_text.concepts.text).top_hits(10)
```
{: codeblock}

## unique_count
{: #unique_count}

Retorna uma contagem de instâncias exclusivas do campo especificado na coleção.

Exemplos:
```bash
unique_count(enriched_text.keyword.text)
```
{: codeblock}

```bash
nested(enriched_text.entities).term(enriched_text.entities.text,count:3).unique_count(enriched_text.entities.type)
```
{: codeblock}

## máx.
{: #max}

Retorna o valor mais alto no campo especificado em todos os documentos correspondentes.

Por exemplo:
```bash
max(product.price)
```
{: codeblock}

## min
{: #min}

Retorna o valor mais baixo no campo especificado em todos os documentos correspondentes.

Por exemplo:
```bash
min(product.price)
```
{: codeblock}

## average
{: #average}

Retorna a média de valores do campo especificado em todos os documentos correspondentes.

Por exemplo:
```bash
average(product.price)
```
{: codeblock}

## sum
{: #sum}

Soma os valores do campo especificado em todos os documentos correspondentes.

Por exemplo:
```bash
sum(product.price)
```
{: codeblock}
