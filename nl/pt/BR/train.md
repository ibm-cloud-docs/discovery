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

# Melhorando a relevância dos resultados com a API

É possível treinar o serviço do {{site.data.keyword.discoveryshort}} para melhorar a relevância dos resultados da consulta para sua organização ou área de assunto específica. Ao fornecer uma instância do {{site.data.keyword.discoveryshort}} com *dados de treinamento*, o serviço usa técnicas Watson de aprendizado de máquina para encontrar sinais em seu conteúdo e nas perguntas. Em seguida, o serviço reordena os resultados da consulta para exibir os resultados mais relevantes na parte superior. À medida que você inclui mais dados de treinamento, a instância de serviço se torna mais precisa e sofisticada na ordenação dos resultados que ela retorna.
{: shortdesc}

O treinamento de relevância é opcional; se os resultados das suas consultas atendem às suas necessidades, não é necessário treinamento adicional. Para obter uma visão geral dos casos de uso de construção, consulte a postagem do blog[Como aproveitar ao máximo o treinamento de relevância ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.ibm.com/dwblog/2017/get-relevancy-training/){: new_window}.

Para obter informações abrangentes sobre as APIs de treinamento, consulte a [Referência da API![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}.

Se você preferir usar o conjunto de ferramentas do {{site.data.keyword.discoveryshort}} para treinar o {{site.data.keyword.discoveryshort}}, consulte [Melhorando a relevância do resultado com o conjunto de ferramentas](/docs/services/discovery/train-tooling.html).

**Observação:** o treinamento de relevância precisa de certos requisitos de dados de treinamento antes que ele entre em vigor. O serviço verifica os dados de treinamento periodicamente para determinar se esses requisitos são atendidos e se atualiza automaticamente com base em qualquer mudança.

**Observação:** o treinamento de relevância atualmente se aplica apenas a consultas de linguagem natural em coleções particulares. Ele não se destina a ser usado com consultas estruturadas da linguagem de consulta do {{site.data.keyword.discoveryshort}}.  Para saber mais sobre a linguagem de consulta do {{site.data.keyword.discoveryshort}}, consulte [Conceitos da consulta](/docs/services/discovery/using.html).

Coleções treinadas retornarão uma pontuação de `confidence` no resultado de uma consulta de linguagem natural. Consulte [Pontuações de confiança](/docs/services/discovery/train-tooling.html#confidence) para obter detalhes.

**Observação:** há um máximo de 4 coleções treinadas por ambiente.

<!-- A trained Discovery service instance is intended primarily for use with natural language queries, but it works equally well with queries that use structured syntax. -->  <!-- See [Query Concepts](/docs/services/discovery/using.html) and the [Query reference](/docs/services/discovery/query-reference.html) for information about structured queries and natural language queries. -->

Os componentes necessários para treinar uma instância do Discovery incluem o seguinte:

 - **Dados de treinamento**. Este é o conjunto de *consultas* e *exemplos* que o serviço usa para refinar os resultados da consulta.
 - **Consulta**. Uma consulta de linguagem natural que se aplica ao conjunto de dados de treinamento.
   Cada consulta possui um ou mais *exemplos* associados, conforme descrito no ponto marcador a seguir.
   Cada consulta deve ser exclusiva dentro do conjunto de dados de treinamento.
 - **Exemplo**. Este é um documento indexado em uma coleção do Discovery que age como um exemplar, **bom ou ruim**, para a consulta associada. Ao incluir um exemplo em uma consulta de dados de treinamento, você inclui um rótulo de relevância que indica a relevância (ou a "bondade" versus "ruindade") do documento conforme ele se aplica à consulta especificada.

   Os exemplos são identificados pelo ID do documento indexado. Conforme observado, cada exemplo deve incluir um rótulo que indique a "bondade" ou a "ruindade" do documento com relação à consulta.

   Os exemplos podem, opcionalmente, especificar uma consulta de referência cruzada. A consulta de referência cruzada precisa retornar apenas o documento de exemplo e deve ser independente do ID do documento exclusivo do Watson Discovery. No momento as consultas de referência cruzada não são usadas automaticamente, mas podem ser usadas para reparar dados de treinamento quando novos IDs são designados aos documentos durante um evento de ingestão.

## Requisitos de dados de treinamento

Os dados de treinamento devem atender aos seguintes critérios **mínimos** de qualidade para melhorar efetivamente a relevância das respostas que são retornadas pelo serviço do Discovery. Observe que **mínimo** não significa **ideal**.

- O conjunto de dados de treinamento da coleção deve conter pelo menos 49 consultas de treinamento exclusivas (ou seja, conjuntos de consultas e exemplos). Dependendo do tamanho e da complexidade de sua coleção, o número de consultas de treinamento em seu conjunto pode precisar ser superior a 49 para que o Watson seja capaz de aplicar treinamento de relevância à coleção.
- A pontuação de relevância para cada consulta de treinamento deve ser um número inteiro não negativo, por exemplo, `0` para representar *não relevante*, `1` para representar *algo relevante* e `2` para representar *altamente relevante*. No entanto, para flexibilidade máxima, o serviço aceita números inteiros não negativos entre `0` e `100` para usuários avançados que experimentam esquemas de pontuação diferentes. Independentemente do intervalo utilizado, o maior número inteiro no conjunto de consultas de treinamento indica relevância máxima. O conjunto de ferramentas do {{site.data.keyword.discoveryshort}} usa as pontuações de relevância de `0` para representar *não relevante* e `10` para representar *relevante*. Se você planeja pontuar seus documentos usando tanto o conjunto de ferramentas do {{site.data.keyword.discoveryshort}} quanto a API ou planeja iniciar a API e mudar para o conjunto de ferramentas, use as pontuações de relevância `0` e `10`.
- As consultas de treinamento devem incluir alguma sobreposição de termo entre a consulta e a resposta desejada para que ele possa ser recuperado pela procura inicial do serviço do Discovery, que possui um escopo amplo.

**Nota:** o Watson utiliza dados de treinamento para aprender padrões e para generalizar consultas de treinamento individuais, não para memorizá-las. O serviço, portanto, nem sempre pode reproduzir os resultados de relevância idênticos para qualquer consulta de treinamento fornecida.

## Incluindo uma consulta no conjunto de dados de treinamento

Use o método `POST /v1/environments/{environment_id}/collections/{collection_id}/training_data` para incluir uma consulta em conjunto de dados de treinamento de uma coleção. A consulta é especificada como um objeto JSON no formato a seguir:

```json
{
  "query_id": "string",
  "natural_language_query": "string",
  "filter": "string",
  "examples": [
    {
      "document_id": "string",
      "cross_reference": "string",
      "relevance": 0
    }
  ]
}
```
{: codeblock}

Os valores neste objeto são os seguintes:

- `query_id`: um ID exclusivo para a consulta. Se você não especificar esse campo, o serviço gerará automaticamente um ID.
- `natural_language_query`: uma consulta de linguagem natural do Discovery que se aplica ao conjunto de treinamento. <!-- The `natural_language_query` parameter is preferred. -->

- `filter`: um filtro opcional para a consulta, conforme descrito na [Referência de consulta](/docs/services/discovery/query-reference.html#parameter-descriptions).

    **Nota:** se você incluir filtros em suas consultas de dados de treinamento, certifique-se de usar os mesmos filtros ao usar consultas de linguagem natural em sua coleção treinada. Se você treinar a coleção com dados filtrados, mas não usar os mesmos tipos de filtros ao consultar a coleção, os resultados poderão ser imprevisíveis.

- `Exemplos`: uma matriz que contém os seguintes valores:

   - `document_id`: o ID exclusivo do documento que se aplica ao conjunto de treinamento. Esse é o *exemplo* descrito anteriormente.
   - `cross_reference`: um rótulo opcional, geralmente consistindo em um campo no documento referido, que "fixa" o documento e as informações do campo no local no evento em que o ID do documento muda, por exemplo, se um documento recém-alimentado recebe o mesmo ID. A especificação de um valor para `cross-reference` **não** vincula um documento a outro; em vez disso, ela assegura que o serviço retenha informações pertinentes do documento, caso o documento seja renomeado ou sobrescrito.
   - `relevante`: um número inteiro de `0` a `100`, inclusive, que indica a importância relativa da consulta para os dados de treinamento. Valores mais altos indicam maior relevância. Um valor de `0` indica nenhuma relevância para a consulta, enquanto que um valor de `100` indica relevância absoluta para a consulta.

   **Nota:** embora o intervalo do parâmetro `relevance` seja de `0` a `100` para flexibilidade máxima, é possível usar um intervalo menor para simplificar exemplos de pontuação. Um intervalo padrão pode ser de `0` a `4` ou pode usar o intervalo inteiro, mas sempre usando incrementos de 20 (`0`, `20`, `40`, `60`, `80` e `100`). O conjunto de ferramentas do {{site.data.keyword.discoveryshort}} usa as pontuações de relevância de `0` para representar *não relevante* e `10` para representar *relevante*. Se você planeja pontuar seus documentos usando tanto o conjunto de ferramentas do {{site.data.keyword.discoveryshort}} quanto a API ou planeja iniciar a API e mudar para o conjunto de ferramentas, use as pontuações de relevância `0` e `10`.

O objeto a seguir mostra uma consulta de dados de treinamento preenchida.

```json
{
  "natural_language_query": "why is the sky blue", "filter": "text:meteorology", "examples": [ {
      "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877", "relevance": 0
    },
    {
      "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81", "relevance": 1
    },
    {
      "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da", "cross_reference": "my_id_field:1463", "relevance": 4 }
  ]
}
```
{: codeblock}

O exemplo de comando a seguir inclui a consulta de dados de treinamento anterior em uma coleção chamada `99040100-fe6a-4782-a4f5-28f9eee30850` em um ambiente chamado `a56dd9b4-040b-4ea3-a736-c1e7a467e191`:

```bash
curl -X POST -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" -H "Content-Type: application/json" -d
'{
  "natural_language_query": "why is the sky blue", "filter": "text:meteorology", "examples": [ {
    "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877", "relevance": 0
    },
    {
      "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81", "relevance": 1
    },
    {
      "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da", "cross_reference": "my_id_field:1463", "relevance": 4 }
  ]
}'
"https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data?version=2016-12-01"
```
{: pre}

## Incluindo um exemplo em uma consulta de dados de treinamento

Depois de criar uma consulta de dados de treinamento, é possível continuar a incluir exemplos para melhorar a precisão do treinamento. Use o método `POST /v1/environments/{environment_id}/collections/{collection_id}/training_data/{query_id}` para incluir um exemplo em uma consulta de dados de treinamento existente.

Execute as etapas a seguir para incluir exemplo em uma consulta de dados de treinamento.

1. Obtenha o ID da consulta de dados de treinamento na qual deseja incluir um novo exemplo [listando as consultas de dados de treinamento da coleção ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#get-training-data){: new_window}:

   ```bash
    curl -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" "https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data?version=2016-12-01"
   ```
   {: pre}

   O JSON que é retornado será do seguinte formato:

   ```json
    {
      "query_id": "484baad4-d440-44b7-a0dd-70bb2ac77baa", "natural_language_query": "why is the sky blue", "filter": "text:meteorology", "examples": [ {
          "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877", "relevance": 0
        },
        {
          "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81", "relevance": 1
        },
        {
          "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da", "cross_reference": "my_id_field:1463", "relevance": 4 }
      ]
    }
   ```
   {: codeblock}

1. Inclua o novo exemplo usando a mesma sintaxe que você usa para definir exemplos ao criar uma nova consulta de dados de treinamento. O exemplo de comando a seguir não inclui uma referência cruzada.

   ```bash
    curl -u -X POST -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" -H "Content-Type: application/json" -d
    '{
      "document_id": "46b52fdc-3a72-4700-9849-ac217532b373",
      "relevance": 3
    }' "https://gateway.watsonplatform.net/discovery/api/v1/environments//a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data/484baad4-d440-44b7-a0dd-70bb2ac77baa?version=2016-12-01"
   ```
   {: pre}

1. Verifique se o novo exemplo foi incluído na consulta de dados de treinamento [listando novamente as consultas de dados de treinamento da coleção ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#get-training-data){: new_window}:

   ```bash
    curl -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" "https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data?version=2016-12-01"
   ```
   {: pre}

   O JSON que é retornado será do seguinte formato:

   ```json
    {
      "query_id": "484baad4-d440-44b7-a0dd-70bb2ac77baa", "natural_language_query": "why is the sky blue", "filter": "text:meteorology", "examples": [ {
          "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877", "relevance": 0
        },
        {
          "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81", "relevance": 1
        },
        {
          "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da",
          "cross_reference": "my_id_field:1463",
          "relevance": 4
        },
        {
          "document_id": "46b52fdc-3a72-4700-9849-ac217532b373",
          "relevance": 3
        }
      ]
    }
   ```
   {: codeblock}

1. Verifique o status do treinamento usando o método [Listar detalhes da coleção ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#list-collection-details){: new_window} e observando o valor do campo `"training"`/`"available"`. Quando você tiver incluído consultas e exemplos suficientes para atender aos requisitos de treinamento, o valor do campo retornará como `true` e o serviço começará a usar os dados de treinamento automaticamente.

   ```bash
    curl -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" "https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850?version=2016-12-01"
   ```
   {: pre}

   O JSON que é retornado será do seguinte formato:

   ```json
    {
      "collection_id": "99040100-fe6a-4782-a4f5-28f9eee30850",
      "name": "democollection",
      "description": "this is a demo collection",
      "created": "2015-08-24T18:42:25.324Z",
      "updated": "2015-08-24T18:42:25.324Z",
      "status": "available",
      "configuration_id": "def9bd08-8472-470f-ab5a-e377f77e9300",
      "language": "en_us",
      "document_counts": {
        "available": 1000, "processing": 20, "failed": 180
      }, "training": {
        "total_examples": 54,
        "available": true,
        "processing": false,
        "minimum_queries_added": true,
        "minimum_examples_added": true,
        "sufficient_label_diversity": false,
        "notices": 13,
        "successfully_trained": "2017-02-08T14:18:22.786Z",
        "data_updated": "2017-02-10T14:18:22.786Z"
      }
    }
   ```
   {: codeblock}

1. Quando todos os campos a seguir na etapa anterior retornam `true`, emita algumas consultas de amostra para ver se o serviço retorna resultados mais relevantes:

   - `minimum_queries_added`
   - `minimum_examples_added`
   - `sufficient_label_diversity`

   Se a relevância de seus resultados não melhorar, inclua mais consultas de treinamento até que os resultados atendam seus requisitos.

Para obter orientação de treinamento adicional, consulte [Dicas de treinamento de relevância](/docs/services/discovery/train-tips.html#relevancy-tips).   

## Executando outras operações de consulta de dados de treinamento
{: #training-data-operations}

É possível administrar e manter consultas de dados de treinamento usando outros métodos de API conforme descrito na [Referência da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}:

 - [Listar os dados de treinamento para uma coleção ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#get-training-data){: new_window}
 - [Excluir todos os dados de treinamento de uma coleção ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-all-training-data){: new_window}
 - [Exibir o conteúdo de uma consulta de dados de treinamento especificada ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#show-td-query){: new_window}
 - [Excluir uma consulta de dados de treinamento da coleção ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1#delete-td-query-example){: new_window}
 - [Mudar um rótulo relevância ou uma referência cruzada de um exemplo de consulta de dados de treinamento ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#update-example){: new_window}
 - [Excluir um documento de exemplo de uma consulta de dados de treinamento ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-example){: new_window}

 **Monitoramento de erro:** erros de dados de treinamento aparecem nos avisos, que podem ser monitorados usando a [API de avisos de consulta ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-notices){: new_window} (`GET /v1/environments/{environment_id}/collections/{collection_id}/notices`).
