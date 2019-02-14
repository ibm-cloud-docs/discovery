---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-25"

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

# Dicas de treinamento de relevância
{: #relevancy-tips}

 Respostas para perguntas comuns sobre treinamento de uma coleção e explicações de mensagens de erro e de aviso comuns. Para obter mais informações sobre como melhorar a relevância das consultas de linguagem natural, consulte [Melhorando a relevância de resultados com o conjunto de ferramentas](/docs/services/discovery/train-tooling.html) e [Melhorando a relevância de resultados com a API](/docs/services/discovery/train.html).
{: shortdesc}

## Entendendo o treinamento

Respostas para perguntas comuns sobre treinamento de uma coleção.

### Como eu sei se meu sistema foi treinado?

Use o comando da API [Detalhes de coleção de lista ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/?curl#list-collection-details){: new_window} para verificar se seu sistema foi treinado.  

```bash
curl -u "apikey":"{apikey_value}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07"
```
{: pre}

Resposta de exemplo:

```json
{
  "training_status": {
    "data_updated": "2017-02-10T14:18:22.786Z", "total_examples": 54, "sufficient_label_diversity": false, "processing": false, "minimum_examples_added": true, "successfully_trained": "2017-02-08T14:18:22.786Z", "available": true, "notices": 13, "minimum_queries_added": true }
}
```

Para satisfazer os requisitos para treinamento, todos os itens a seguir devem ser `true`:
- `minimum_queries_added`
- `minimum_examples_added`
- `sufficient_label_diversity`   

Na resposta:
- `successfully_trained` é a última vez em que o treinamento foi concluído com sucesso.
- `available: true` indica que o treinamento ocorreu e que um modelo está disponível.
- `processing: true` indica que o treinamento está em andamento.
-  Se a data `data_updated` for posterior à data `successfully_trained`, um novo modelo não foi treinado desde o upload de dados recente.  

### Como verificar erros e avisos?

É possível usar a [API de avisos de consulta ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-notices){: new_window} para visualizar erros ou avisos.  

```bash
curl -u "apikey": "{1}/environments/{2}{0}{1}{7}-11-07"
```
{: pre}

Outras operações da API são listadas em [Executando outras operações de consulta de dados de treinamento](/docs/services/discovery/train.html#training-data-operations).

### Como eu interpreto a pontuação de `confidence` que aparece nos resultados da consulta de linguagem natural após o treinamento?

Coleções treinadas retornarão uma pontuação de `confidence` no resultado de uma consulta de linguagem natural. Este número de `confidence` é calculado com base no grau de relevância do resultado em comparação com o modelo treinado. A pontuação de `confidence` **não** é a mesma que a `score`. Consulte [Pontuações de confiança](/docs/services/discovery/train-tooling.html#confidence) para obter mais informações.  

## Interpretando erros e avisos

Explicações de mensagens de erro e de aviso comuns.

### Aviso: `Invalid training data found: The document was not returned in the top 100 search results for the given query, and will not be used for training`

Este aviso é causado porque os `document_ids` em seus dados de treinamento dados não correspondem aos `document_ids` em uma procura executada com relação à coleção. É necessário verificar suas consultas e certificar-se de que o `document_id` do documento que você está classificando é retornado nos 100 principais resultados para essa consulta. Caso contrário, talvez você queira verificar duas coisas:  

- Se o documento não é retornado entre os 100 principais, possivelmente ele não é um bom exemplo de um resultado de alta qualidade e talvez você queira rever por que este documento foi escolhido.  

- Se o documento não é retornado, é necessário revisar por que isso acontece e ver se há algum texto no documento que corresponde às partes da consulta.  

**Nota:** esse aviso indica que pode haver uma ou mais consultas inválidas, mas isso não indica que o treinamento não acontecerá.  

### Erro: `Invalid training data found: Syntax error when parsing query`

- Isso significa que há um problema com a sintaxe de consulta real. Valide que as consultas retornam resultados e que não emitem um erro de sintaxe. Isso poderá ocorrer apenas se você incluir um filtro na sua consulta de linguagem natural.

### Erro: `Invalid training data found: The query string provided exceeds the maximum length, please provide a shorter one`

- O comprimento máximo da sequência de consultas é `2048`. Será necessário encurtar a consulta específica. A inclusão de um filtro em sua consulta é uma maneira de solução alternativa.  

### Erro: `This collection cannot be trained: your plan does not support training on this many top-level text fields.`

- Esse erro ocorre apenas com os planos `Lite`. Os campos de nível superior são campos que não estão aninhados sob outro campo. O treinamento ocorre apenas nos campos de nível superior e há limites para quantos campos podem ser usados no processo de treinamento. Quanto mais campos de nível superior em uma coleção, mais dados de treinamento são necessários. Além disso, nos casos em que há mais de `10` campos de nível superior, o treinamento é mais provável de encontrar erros. 

### Erro: `Training data quality standards not met: You will need additional training queries with labeled examples. (To be considered for training, each example must appear in the top 100 search results for its query.)`

- Isso significa que é necessário incluir mais dados de treinamento para treinar com sucesso. São necessárias pelo menos 49 consultas de treinamento exclusivas e cada uma precisa de pelo menos um documento classificado. O mínimo não equivale ao ideal; o tamanho da coleção e outros fatores podem aumentar o número de exemplos de treinamento necessários para atender ao mínimo.  

### Erro: `Training data quality standards not met: Insufficient number of unique training queries. Expected at least n, but found m.`

- Para atender os requisitos mínimos de treinamento, são necessárias pelo menos 49 consultas de treinamento exclusivas e cada uma precisa de pelo menos um documento classificado. Se você tiver mais do que isso e ainda estiver recebendo essa mensagem de erro, será necessário verificar os avisos para erros adicionais.  

### Erro: `Training data quality standards not met: No documents found with non-zero relevance labels.`

- Os dados de treinamento precisam de dados rotulados suficientes que especifiquem quais documentos são de valor alto. Isso significa que é necessário classificar alguns documentos com valores diferentes de zero. Se estiver usando o Discovery Tooling, será necessário classificar alguns documentos como Relevantes (`10`); se estiver usando a API, será necessário rotular algum documento como `1` ou superior.   

### Erro: `Training data quality standards not met: Training examples have no relevance label variety for X queries.`

- Um dos requisitos para treinamento é ter uma diversidade de rótulo suficiente. Isso significa que, se você deseja obter um sistema bem treinado, deve incluir não somente documentos que sejam a melhor correspondência de relevância, mas também outros que sejam “bons” documentos relevantes. Em outras palavras, se você tiver uma escala de 0 a 4, ela ajudará a classificar documentos como 2 e 3, além dos classificados como 4. (Se você estiver usando o Discovery Tooling, os documentos serão classificados como Relevantes (`10`) ou Não relevantes (`0`)). Pelo menos 25% das questões devem ter alguma variedade de rótulo.   
