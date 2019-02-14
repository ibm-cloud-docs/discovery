---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-04"

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

# Parâmetros de consulta
{: #query-parameters}

O serviço do {{site.data.keyword.discoveryfull}} oferece poderosos recursos de pesquisa de conteúdo por meio de consultas. Após seu conteúdo ser transferido por upload e enriquecido pelo serviço do {{site.data.keyword.discoveryshort}}, será possível construir consultas, integrar o{{site.data.keyword.discoveryshort}} em seus próprios projetos ou criar um aplicativo customizado usando o {{site.data.keyword.watson}} Explorer Application Builder. Para obter uma introdução das consultas, veja [Conceitos
de consulta](/docs/services/discovery/using.html). Para obter a lista completa de parâmetros, veja a
[Referência da
consulta](/docs/services/discovery/query-reference.html#parameter-descriptions).
{: shortdesc}

**Parâmetros de procura**

Os parâmetros de procura permitem procurar pela sua coleção, identificar um conjunto de resultados e
executar análise no conjunto de resultados.

O **conjunto de resultados** é o grupo de documentos identificados pelas procuras
combinadas dos parâmetros de procura. O conjunto de resultados pode ser significativamente maior que os
resultados retornados. Se uma consulta vazia for executada, o conjunto de resultados será igual a todos os
documentos na coleção.

## query
{: #query}

Uma consulta de procura retorna todos os documentos em seu conjunto de dados com enriquecimentos
completos e texto completo em ordem de relevância. Uma consulta também exclui quaisquer documentos que não
mencionem o conteúdo da consulta. Essas consultas são gravadas usando o
[{{site.data.keyword.discoveryshort}} Query
Language](/docs/services/discovery/query-operators.html).

## filtro
{: #filter}

Uma consulta armazenável em cache que exclui quaisquer documentos que não mencionem o conteúdo da consulta. Os resultados da procura de filtro **não** são retornados em ordem de relevância. Essas
consultas são gravadas usando o
[{{site.data.keyword.discoveryshort}} Query
Language](/docs/services/discovery/query-operators.html)

### Diferenças entre os parâmetros de filtro e de consulta
{: #filtervquery}

Se você testar o mesmo termo de procura em um conjunto de dados pequeno, talvez ache que os
parâmetros `filter` e `query` retornam resultados muito semelhantes
(se não idênticos). No entanto, há uma diferença entre os dois parâmetros.

- O uso de um parâmetro de filtro sozinho retorna resultados da procura em nenhuma ordem específica.
- O uso de um parâmetro de consulta sozinho retorna resultados da procura em ordem de relevância.

Em conjuntos de dados grandes, se você precisa que os resultados sejam retornados em ordem de relevância,
é necessário combinar os parâmetros `filter` e `query`, já que
usá-los juntos melhora o desempenho. Isso ocorre porque primeiramente o parâmetro `filter` é
executado armazenando os resultados em cache e, em seguida, o parâmetro `query`
os classifica. Para obter um exemplo de uso de filtros e de consultas juntos, consulte
[Construindo consultas
combinadas](/docs/services/discovery/using.html#building-combined-queries). Os filtros também podem ser usados em agregações.

Ao gravar uma consulta que inclua tanto um parâmetro `filter` quanto um
parâmetro `aggregation`, `query` ou
`natural_language_query`, os parâmetros `filter` são executados
primeiramente, após os quais quaisquer parâmetros
`aggregation`, `query` ou `natural_language_query`
são executados em paralelo.

Com uma consulta simples, especialmente em um conjunto de dados pequeno, `filter` e
`query` geralmente retornam os mesmos resultados exatos (ou semelhantes). Se uma chamada `filter` e `query` retornar resultados semelhantes e a
obtenção de uma resposta em ordem de relevância não for importante, será melhor usar o filtro, já que as
chamadas de filtro são mais rápidas e armazenadas em cache. O armazenamento em cache significa que, na próxima vez em que
essa chamada for feita, você obterá uma resposta muito mais rápida, especialmente em um conjunto de dados
grande.

## aggregation
{: #aggregation}

As consultas de agregação retornam uma contagem de documentos que correspondem um conjunto de valores de
dados; por exemplo, palavras-chave principais, a impressão geral de entidades, etc. Para obter a lista completa de opções de agregação, consulte a
[Tabela de agregações](/docs/services/discovery/query-aggregations.html). Essas agregações
são gravadas usando o
[{{site.data.keyword.discoveryshort}} Query
Language](/docs/services/discovery/query-operators.html)

## natural_language_query
{: #nlq}

Uma consulta de linguagem natural permite executar consultas expressas em linguagem natural, já que ela pode ser
recebida de um usuário final em uma interface de conversação ou de texto livre, por exemplo: "IBM
Watson em assistência médica". O parâmetro usa a entrada inteira como o texto da consulta. Ele
**não** reconhece operadores. O parâmetro `natural_language_query`
permite recursos, como procura de passagem e treinamento de relevância. Coleções treinadas retornarão uma pontuação de `confidence` no resultado de uma consulta de linguagem natural. Consulte [Pontuações de confiança](/docs/services/discovery/train-tooling.html#confidence) para obter detalhes. O comprimento máximo da sequência de consultas para uma consulta de língua natural é `2048`.

**Parâmetros de estrutura**

Os parâmetros de estrutura definem o conteúdo e a organização dos documentos no JSON retornado. Isso
inclui o número de resultados retornados, o ponto no conjunto de resultados para começar a retornar
documentos, como o conjunto de resultados é classificado, quais campos deverão ser retornados para cada
documento, se os documentos duplicados devem ser removidos e se passagens relevantes devem ser extraídas do
conjunto de resultados. Os parâmetros de estrutura não afetam quais documentos fazem parte do conjunto
de resultados inteiro.

## Nativa
{: #count}

O número de documentos que você deseja que sejam retornados na resposta. O padrão é `10`. O máximo para os valores `count` e `offset` juntos em qualquer consulta é
`10000`.

## Deslocamento
{: #offset}

O número de resultados da consulta para ignorar no início. Por exemplo, se o número total de resultados
que são retornados for 10 e o deslocamento for 8, ele retornará os dois últimos resultados. O padrão é
`0`. O máximo para os valores `count` e `offset`
juntos em qualquer consulta é `10000`.

## return
{: #return}

Uma lista separada por vírgula das parte da hierarquia de documentos a serem retornados. Qualquer
hierarquia de documentos representa valores válidos.

## ordenação
{: #sort}

Uma lista separada por vírgula de campos no documento para classificação. É possível, opcionalmente,
especificar uma direção de classificação prefixando o campo com `-` para ordem decrescente ou
`+` para ordem crescente. A ordem crescente é a direção de classificação padrão.

O parâmetro `sort` está atualmente disponível para uso apenas com a API; ele
não está disponível por meio do conjunto de ferramentas.

## Propensão
{: #bias}

Ajusta os resultados da procura com propensão a determinados resultados, por exemplo, documentos que foram publicados mais recentemente. O `bias` deve ser configurado para um campo de tipo `date` ou um campo de tipo `number`, por exemplo, `bias=publication_date` ou `bias=field_1`. Quando um campo de tipo `date` for especificado, os resultados retornados estarão propensos a valores de campo mais próximos da data atual. Quando um campo do tipo `number` for especificado, os resultados retornados estarão propensos a valores de campo mais altos. Esse parâmetro não pode ser usado na mesma consulta que o parâmetro `sort`.

O parâmetro `bias` está atualmente disponível para uso somente com a API; ele não está disponível por meio do conjunto de ferramentas.

## passages
{: #passages}

Um booleano que especifica se o serviço retorna um conjunto das passagens mais relevantes dos documentos
retornados por uma consulta que usa o parâmetro `natural_language_query`. As passagens são geradas por algoritmos Watson sofisticados para determinar as melhores passagens de texto de todos os documentos retornados pela consulta. O padrão
é `false`.

O parâmetro `passages` pode ser usado somente em coleções privadas. Ele não pode ser usado na coleção do {{site.data.keyword.discoverynewsfull}}.
{: tip}

O {{site.data.keyword.discoveryshort}} tenta retornar passagens que começam no início de uma
sentença e que param no término usando a detecção de limite de sentença. Para isso, primeiramente ele procura
por passagens com aproximadamente o comprimento especificado no
[parâmetro `passages.characters`](/docs/services/discovery/query-parameters.html#passages_characters)
(padrão `400`). Em seguida, ele expande cada passagem para o limite de duas vezes o
comprimento especificado para retornar sentenças completas. Se o seu
parâmetro `passages.characters` é curto e/ou as sentenças em seus documentos são muito
longas, talvez não haja limites de sentença próximas o
suficiente para retornar a sentença completa sem exceder duas vezes o comprimento solicitado. Nesse caso,
o {{site.data.keyword.discoveryshort}} permanece dentro do limite de duas vezes o
parâmetro `passages.characters`, de modo que a passagem retornada não incluirá a sentença
inteira e omitirá o início, o término ou ambos.

Como os ajustes de limite de sentença expandem o tamanho da passagem, você verá um
aumento substancial de comprimento médio de passagem. Se seu aplicativo possui um espaço de tela limitado,
talvez você deseja configurar um valor menor para `passages.characters` e/ou truncar as passagens
que são retornadas pelo {{site.data.keyword.discoveryshort}}. A detecção de limite de sentença
funciona para todos os idiomas suportados e usa a lógica específica do idioma.

O parâmetro `passages` retorna passagens correspondentes
(`passage_text`), bem como o `score`, o `document_id`, o nome
do campo do qual a passagem foi extraída (`field`) e os caracteres iniciais e finais do
texto da passagem dentro do campo (`start_offset` e `end_offset`), conforme mostrado no
exemplo a seguir. A consulta é mostrada na parte superior do exemplo.

```bash
 curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-06-25&natural_language_query='Hybrid%20cloud%20companies'&passages=true"
```
{: pre}

O JSON que é retornado será do seguinte formato:

```json
 {
   "matching_results":2,
   "passages":[
     {
       "document_id":"ab7be56bcc9476493516b511169739f0",
       "passage_score":15.230205287402338,
       "passage_text":"a privately held company that provides hybrid cloud recovery, cloud migration and business continuity software for enterprise data centers and cloud infrastructure."
       "start_offset":120
       "end_offset":300
       "field":"text"       
     },
     {
       "passage_text":"Disaster Recovery Services for Hybrid Cloud</title></head>\n<body>\n\n\n<p>Published:
Thu, 27 Oct 2016 07:01:21 GMT</p>\n"
       "passage_score":10.153470191601558,
       "document_id":"fbb5dcb4d8a6a29f572ebdeb6fbed20e",              
       "start_offset":70
       "end_offset":120
       "field":"html"
     },
  ...
```
{: codeblock}                        

### passages.fields
{: #passages_fields}

Uma lista separada por vírgula de campos no índice dos quais as passagens serão extraídas. Se este parâmetro não for especificado, então todos os campos de nível superior serão incluídos.

### passages.count
{: #passages_count}

O número máximo de passagens a serem retornadas. A procura retornará menos se esse for o número total
localizado. O padrão é `10`. O máximo é `100`.

### passages.characters
{: #passages_characters}

O número aproximado de caracteres que qualquer passagem deve ter. O padrão é `400`. O
mínimo é `50`. O máximo é `2000`. As passagens retornadas podem ter até duas
vezes o comprimento solicitado (se necessário) para que elas comecem e terminem nos limites da sentença.

## highlight
{: #highlight}

Um booleano que especifica se a saída retornada inclui um objeto `highlight` no
qual as chaves são nomes de campos e os valores são matrizes que contêm segmentos de texto de correspondência
de consulta destacados pela tag `*` HTML.

A saída lista o objeto `highlight` após o
objeto `enriched_text`, conforme mostrado no exemplo a seguir.

```bash
curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-06-25&natural_language_query=Hybrid%20cloud%20companies&highlight=true"
```
{: pre}

O JSON que é retornado será do seguinte formato:

```json
{
   "highlight": {
     "extracted_metadata.title": [
       "IBM to Acquire Sanovi Technologies to Expand Disaster Recovery Services for <em>Hybrid</em> <em>Cloud</em>"
       ],
     "enriched_text.concepts.text": [
       "Privately held <em>company</em>",
       "<em>Cloud</em> computing"
       ],
     "text": [
       " Sanovi Technologies, a privately held <em>company</em> that provides <em>hybrid</em> <em>cloud</em> recovery, <em>cloud</em> migration",
       "IBM to Acquire Sanovi Technologies to Expand Disaster Recovery Services for <em>Hybrid</em> <em>Cloud</em>\n\nPublished",
       " undergoing digital and <em>hybrid</em> <em>cloud</em> transformation.\n\nURL: http://www.ibm.com/press/us/en/pressrelease/50837.wss",
       " and business continuity software for enterprise data centers and <em>cloud</em> infrastructure. Adding"
       ],
     "enriched_text.categories.label": [
       "/business and industrial/<em>company</em>/bankruptcy"
       ],
     "enriched_text.entities.type": [
       "<em>Company</em>"
       ],
     "html": [
       " Technologies, a privately held <em>company</em> that provides <em>hybrid</em> <em>cloud</em>\n recovery, <em>cloud</em> migration and business",
       " Disaster Recovery Services for <em>Hybrid</em> <em>Cloud</em></title></head>\n<body>\n\n\n<p>Published: Thu, 27 Oct 2016 07:01",
       " digital and <em>hybrid</em> <em>cloud</em> transformation.</p>\n<p>URL: http://www.ibm.com/press/us/en/pressrelease/50837.wss</p>\n\n\n\n</body></html>",
       " continuity software for \nenterprise data centers and <em>cloud</em> infrastructure. Adding these \ncapabilities"
       ]
   }
}
```
{: codeblock}

## deduplicate
{: #deduplicate}

 Um recurso beta que exclui documentos duplicados dos resultados da consulta de coleção do
{{site.data.keyword.discoverynewsfull}}
com base no campo `title`. Consulte [Excluindo documentos duplicados de resultados da consulta](/docs/services/discovery/query-parameters.html#deduplication).

### deduplicate.field
{: #deduplicate_field}

Um recurso beta que exclui documentos duplicados dos resultados da consulta com base no
`{field}` especificado. Consulte [Excluindo documentos duplicados de resultados da consulta](/docs/services/discovery/query-parameters.html#deduplication).

### Excluindo documentos duplicados dos resultados da consulta
{: #deduplication}

Se você estiver consultando a coleção do {{site.data.keyword.discoverynewsfull}} ou se sua
coleção de dados privados contiver múltiplos documentos idênticos (ou quase idênticos), será possível
excluir a maioria deles dos seus resultados da consulta usando a deduplicação de documento.

**Nota:** a deduplicação de documentos é atualmente suportada apenas como um recurso
beta. Consulte [Recursos beta](/docs/services/discovery/release-notes.html#beta-features) nas
Notas sobre a liberação para obter mais informações. Esse recurso beta é atualmente suportado apenas em inglês. Consulte [Suporte ao idioma](/docs/services/discovery/language-support.html#feature-support) para obter detalhes.

**Nota:** cada consulta é deduplicada de forma independente, portanto, a
deduplicação nas compensações não é suportada.

A deduplicação é executada após as `passages` serem extraídas e as agregações serem
calculadas, portanto, se você incluir o parâmetro `passages` em sua consulta, as passagens
serão retornadas de todos os documentos nos resultados da consulta, antes da deduplicação. Se você executar
uma agregação e uma consulta juntas, os resultados da agregação incluirão dados de todos os documentos
retornados, antes da deduplicação.

A deduplicação é executada somente nos campos retornados. Se você optar por especificar o
`return=` em sua consulta, inclua o campo que você está deduplicando.

Para aplicar a deduplicação, use a seguinte sintaxe em sua consulta.  Substitua `{field}` pelo nome do campo em que você deseja deduplicar. O `{field}` especificado deve ser uma sequência, como um `title`.

```
&deduplicate.field={field}
```
{: codeblock}

Ao deduplicar, a resposta JSON inclui `"duplicates_removed": x`, em que
`x` é o número de documentos removidos dos resultados.

#### Deduplicando documentos no Watson Discovery News

Os artigos de notícias podem ser organizados em vários meios de comunicação e {{site.data.keyword.discoverynewsfull}} escolherá cada um deles, resultando em artigos duplicados. Isso significa que uma consulta ao {{site.data.keyword.discoverynewsfull}} pode retornar potencialmente vários artigos idênticos ou quase idênticos nos resultados da consulta. O uso da deduplicação remove a maioria dos artigos duplicados de suas consultas de procura.

O {{site.data.keyword.discoveryshort}} deduplica usando a correspondência aproximada no
campo `title` e, portanto, um campo não precisa ser especificado.

Para aplicar a deduplicação, use o parâmetro a seguir em sua consulta. Esta consulta
deduplica automaticamente o campo `title` no
{{site.data.keyword.discoverynewsfull}}.

```bash
&deduplicate=true
```
{: codeblock}

Se você preferir deduplicar em um campo diferente de `title`, use a seguinte sintaxe
em sua consulta. Substitua `{field}` pelo nome do campo em que você deseja deduplicar. O
`{field}` especificado deve ser uma sequência.

```bash
&deduplicate.field={field}
```
{: codeblock}

## collection_ids
{: #collection_ids}

Uma lista separada por vírgula de coleções no mesmo ambiente que será consultado. Esse parâmetro é
válido apenas ao usar o método `environments/{environment_id}/query?`. Veja [Consultando múltiplas coleções](/docs/services/discovery/using.html#multiple-collections) para obter mais informações.

```bash
&collection_ids={id1},{id2}
```
{: codeblock}

## semelhante
{: #similar}

A similaridade do documento identifica documentos que são semelhantes aos documentos listados nos parâmetros `similar.document_ids`. Isso pode ser refinado ainda mais, especificando quais campos serão considerados para comparação usando os parâmetros `similar.fields`. O padrão
é `false`. Consulte  [ Similaridade do documento ](/docs/services/discovery/using.html#doc-similarity)  para obter mais informações.

```bash
&similar=true
```
{: codeblock}

### similar.document_ids
{: #similar_document_ids}

Uma lista separada por vírgula de IDs de documentos que serão usados como uma base para localizar documentos semelhantes como resultados. Esse parâmetro será necessário se o parâmetro `similar` for configurado para `true`.

```bash
&similar.document_ids={id1},{id2}
```
{: codeblock}

### Similar.fields
{: #similar_fields}

Uma lista opcional separada por vírgulas de campos que serão usados para comparar documentos para localizar documentos semelhantes. Esse parâmetro pode ser usado somente em conjunto com o parâmetro `similar.document_ids`.

```bash
&similar.fields={field1},{field2}
```
{: codeblock}
