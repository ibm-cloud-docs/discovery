---

copyright:
years: 2018, 2019
lastupdated: "2019-01-15"

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

# Entendendo o esquema de saída
{: #output_schema}

Após um documento ter sido alimentado usando a Classificação de elementos, o serviço fornece saída JSON no esquema a seguir para a data da versão `2018-10-15` ou mais recente. A saída será incluída dentro do objeto `enriched_html_elements`. 

```json
{
  "document": {
    "title": string,
    "html": string,
    "hash": string
  },
  "model_id" : string,
  "model_version" : string,  
  "elements": [
    {
      "location": { 
        "begin": int,
        "end": int
      },
      "text": string,
      "types": [
        {
          "label": { "nature": string, "party": string },
          "provenance_ids": [string, string, ...]
            ...
          ]
        }
        ...
      ],
      "categories": [
        {
          "label": string,
          "provenance_ids": [string, string, ...]
        }
        ...
      ],
      "attributes": [
        {
      	  "type": string,
          "text": string,
          "location": { "begin": int, "end": int }
         }
      ]
    }
    ...
  ],
  "tables": [
    {
      "location": {
        "begin" : int,
        "end" : int
      },
      "text": string,
      "section_title": {
        "text": string, "location": {
          "begin" : int,
          "end" : int
        }
      },
      "table_headers" : [
        {
          "cell_id" : string, "location" : {
            "begin" : int,
            "end" : int
          },
          "text" : string,
          "row_index_begin" : int,
          "row_index_end" : int,
          "column_index_begin" : int,
          "column_index_end" : int
        },
        ...
      ],
      "column_headers" : [
        {
          "cell_id" : string, "location" : {
            "begin" : int, "end" : int }, "text" : string, "text_normalized" : string, "row_index_begin" : int, "row_index_end" : int, "column_index_begin" : int, "column_index_end" : int },
        ...
      ],
      "row_headers" : [
        {
          "cell_id" : string, "location" : {
            "begin" : int, "end" : int }, "text" : string, "text_normalized" : string, "row_index_begin" : int, "row_index_end" : int, "column_index_begin" : int, "column_index_end" : int },
        ...
      ],
      "body_cells" : [
        {
          "cell_id" : string, "location" : {
            "begin" : int,
            "end" : int
          },
          "text" : string,
          "row_index_begin" : int,
          "row_index_end" : int,
          "column_index_begin" : int,
          "column_index_end" : int,
          "row_header_ids": [ string ],
          "row_header_texts": [ string ],
          "row_header_texts_normalized": [ string ],
          "column_header_ids": [ string ],
          "column_header_texts": [ string ],
          "column_header_texts_normalized": [ string ],
          "attributes" : [
             {
               "type" : string,
               "text" : string,
               "location" : {
                 "begin" : int,
          "end" : int
        }
             },
             ...
           ]
        },
        ...
      ]
    },
    ...
  ], "document_structure": {
    "section_titles": [
      {
        "text": string, "location": {
          "begin": int,
          "end": int
        },
        "level": int,
        "element_locations": [
          {
            "begin": int, "end": int },
          ...
        ]
      },
      ...
    ],
    "leading_sentences": [
      {
        "text": string, "location": {
          "begin": int,
          "end": int
        },
        "element_locations": [
          {
            "begin": int, "end": int },
          ...
        ]
      },
      ...
    ]
  },
  "parties": [
    {
      "party": string,
      "role": string,
      "importance": string,
      "addresses": [
        {
          "text": string, "location": {
            "begin": int,
            "end": int
          }
        },
        ...
      ],
      "contacts": [
        {
          "name": string,
          "role": string 
        },
        ...
      ]
    },
    ...
  ],
  "effective_dates": [
    {
      "text": string, "confidence_level": string, "location": { "begin": int, "end": int }
     },
     ...
  ],
  "contract_amounts": [
    {
      "text": string, "confidence_level": string, "location": { "begin": int, "end": int }
    },
    ...
  ],
  "termination_dates": [
    {
      "text": string, "confidence_level": string, "location": { "begin": int, "end": int }
    },
    ...
  ]
}
```
{: codeblock}

O esquema é organizado conforme a seguir.

  - `document`: um objeto que lista informações básicas sobre o documento, incluindo:
    - ` title `: O título do documento, se detectado.
    - `html`: o texto integral do documento de entrada no formato HTML.
    - `hash`: o hash MD5 do documento de entrada.
  - `model_id`: o modelo de análise a ser usado pelo serviço. Para os métodos `/v1/element_classification` e `/v1/comparison`, o padrão é `contracts`. Para o método `/v1/tables`, o padrão é `tables`. Esses padrões se aplicam aos métodos independentes e ao uso dos métodos em solicitações de processamento em lote.
  - `model_version`: a versão do modelo de análise especificado pelo valor do parâmetro `model_id`.
  - `elements`: uma matriz dos elementos de documento detectados pelo serviço.
    - `location`: o local do elemento conforme definido por seus índices `begin` e `end`.
    - ` text `: o texto do elemento.
    - `types`: uma matriz que descreve qual é o elemento e quem ele afeta.
      - `label`: um objeto que define o tipo usando um par dos elementos a seguir:
        - `nature`: o tipo de ação que a sentença requer. Os valores atuais são `Definition`, `Disclaimer`, `Exclusion`, `Obligation` e `Right`.
        - `party`: uma sequência que identifica a parte para a qual a sentença se aplica.
      - `provenance_ids`: uma matriz de um ou mais valores com hash que podem ser enviados para a IBM para fornecer feedback ou receber suporte.
    - `categories`: uma matriz que lista as categorias funcionais nas quais o elemento cai; em outras palavras, o assunto do elemento.
      - `label`: uma sequência que lista a categoria identificada. É possível localizar uma lista de [categorias](/docs/services/discovery?topic=discovery-contract_parsing#contract_categories) em [Entendendo a análise sintática do contrato](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing).
      - `provenance_ids`: uma matriz de um ou mais valores com hash que podem ser enviados para a IBM para fornecer feedback ou receber suporte.
    - `attributes`: uma matriz que identifica atributos de documento. Cada objeto na matriz consiste em três elementos:
      - ` type `: O tipo de atributo. Os valores possíveis são `Address`, `Currency`, `DateTime`, `Location`, `Organization` e `Person`.
      - `text`: o texto associado ao atributo.
      - `location`: o local do atributo conforme definido por seus índices `begin` e `end`.
  - `tables`\*: uma matriz que define as tabelas identificadas no documento de entrada.
    - `location`: o local da tabela atual conforme definido por seus índices `begin` e `end` no documento de entrada.
    - `text`: os conteúdos textuais da tabela atual do documento de entrada sem conteúdo de marcação associado.
    - `section_title`: se identificado, a localização de um título de seção contido na tabela atual. Vazio se nenhum título da seção for identificado.
      - `text`: o texto do título da seção identificado.
      - `location`: o local do título da seção no documento de entrada conforme definido por seus índices `begin` e `end`.
    - `table_headers`: uma matriz de células de nível de tabela aplicáveis como cabeçalhos para todas as
outras células da tabela atual. Cada cabeçalho da tabela é definido como uma coleção dos elementos a seguir:
      - `cell_id`: valor de sequência no formato `tableHeader-x-y`, em que `x` e `y` são os deslocamentos inicial e final do valor da célula no documento de entrada original.
      - `location`: o local da célula no documento de entrada conforme definido por seus índices `begin` e `end`.
      - `text`: os conteúdos textuais da célula por meio do documento de entrada sem conteúdo de marcação associado.
      - `row_index_begin`: o índice `begin` do local de `row` da célula na tabela atual.
      - `row_index_end`: o índice `end` do local de `row` da célula na tabela atual.
      - `column_index_begin`: o índice `begin` do local de `column` da célula na tabela atual.
      - `column_index_end`: o índice `end` do local de `column` da célula na tabela atual.
    - `column_headers`: uma matriz de células de nível de coluna da tabela atual, cada uma delas aplicável como
um cabeçalho para as outras células na própria coluna. Cada cabeçalho da coluna é definido como uma coleção dos itens a seguir:
      - `cell_id`: um valor de sequência no formato `columnHeader-x-y`, em que `x` e `y` são os deslocamentos inicial e final dessa célula do cabeçalho da coluna no documento de entrada.
      - `location`: o local da célula no documento de entrada conforme definido por seus índices `begin` e `end`.
      - `text`: os conteúdos textuais da célula por meio do documento de entrada sem conteúdo de marcação associado.
      - `text_normalized`: se você fornecer entrada de customização, a versão normalizada do texto da célula de acordo com a customização; caso contrário, o mesmo valor que `text`. 
      - `row_index_begin`: o índice `begin` do local de `row` da célula na tabela atual.
      - `row_index_end`: o índice `end` do local de `row` da célula na tabela atual.
      - `column_index_begin`: o índice `begin` do local de `column` da célula na tabela atual.
      - `column_index_end`: o índice `end` do local de `column` da célula na tabela atual.
    - `row_headers`: uma matriz de células de nível de linha da tabela atual, cada uma delas aplicável como
um cabeçalho para as outras células na própria linha. Cada cabeçalho de linha é definido como uma coleção dos itens a seguir:
      - `cell_id`: um valor de sequência no formato `rowHeader-x-y`, em que `x` e `y` são os deslocamentos inicial e final dessa célula do cabeçalho da linha no documento de entrada.
      - `location`: o local da célula no documento de entrada conforme definido por seus índices `begin` e `end`.
      - `text`: os conteúdos textuais da célula por meio do documento de entrada sem conteúdo de marcação associado.
      - `text_normalized`: se você fornecer entrada de customização, a versão normalizada do texto da célula de acordo com a customização; caso contrário, o mesmo valor que `text`. 
      - `row_index_begin`: o índice `begin` do local de `row` da célula na tabela atual.
      - `row_index_end`: o índice `end` do local de `row` da célula na tabela atual.
      - `column_index_begin`: o índice `begin` do local de `column` da célula na tabela atual.
      - `column_index_end`: o índice `end` do local de `column` da célula na tabela atual.
    - `body_cells`: uma matriz de células que não são de cabeçalho de tabela, de coluna ou de linha, da tabela atual com associações de cabeçalho de linha e coluna correspondentes. Cada célula do corpo é definida como uma coleção dos itens a seguir:
      - `cell_id`: um valor de sequência no formato `bodyCell-x-y`, em que `x` e `y` são os deslocamentos inicial e final dessa célula do corpo no documento de entrada.
      - `location`: o local da célula no documento de entrada conforme definido por seus índices `begin` e `end`.
      - `text`: os conteúdos textuais da célula por meio do documento de entrada sem conteúdo de marcação associado.
      - `row_index_begin`: o índice `begin` do local `row` dessa célula na tabela atual.
      - `row_index_end`: o índice `end` do local `row` dessa célula na tabela atual.
      - `column_index_begin`: o índice `begin` do local `column` dessa célula na tabela atual.
      - `column_index_end`: o índice `end` do local `column` dessa célula na tabela atual.
      - `row_header_ids`: uma matriz de valores, cada um sendo o valor `cell_id` de um cabeçalho de linha que é aplicável a essa célula do corpo.
      - `row_header_texts`: uma matriz de valores, cada um sendo o valor de `text` de um cabeçalho de linha que é aplicável a essa célula do corpo.
      - `row_header_texts_normalized`: se você fornecer entrada de customização, a versão normalizada dos textos de cabeçalho da linha de acordo com a customização; caso contrário, o mesmo valor que `row_header_texts`. 
      - `column_header_ids`: uma matriz de valores, cada um sendo o valor `cell_id` de um cabeçalho da coluna que é aplicável a essa célula do corpo.
      - `column_header_texts`: uma matriz de valores, cada um sendo o valor `text` de um cabeçalho da coluna que é aplicável a essa célula do corpo.
      - `column_header_texts_normalized`: se você fornecer entrada de customização, a versão normalizada dos textos de cabeçalho da coluna de acordo com a customização; caso contrário, o mesmo valor que `column_header_texts`.
      - `attributes`: uma matriz que identifica atributos de documento. Cada objeto na matriz consiste em três elementos:
        - ` type `: O tipo de atributo. Os valores possíveis são `Address`, `Currency`, `DateTime`, `Location`, `Organization` e `Person`.
        - `text`: o texto associado ao atributo.
        - `location`: o local do atributo conforme definido por seus índices `begin` e `end`.
  - `document_structure`: um objeto que descreve a estrutura do documento de entrada.
    - `section_titles`: uma matriz que contém um objeto por seção ou subseção que é detectado no documento de entrada. Seções e subseções não são aninhadas. Em vez disso, eles são esvaziados e podem ser colocados de volta em ordem usando os valores `begin` e `end` do elemento e o valor `level` da seção.
      - `text`: uma sequência que lista o título da seção, se detectado.
      - `location`: o local do título no documento de entrada conforme definido por seus índices `begin` e `end`.
      - `level`: um número inteiro que indica o nível no qual a seção está localizada no documento de entrada. Por exemplo, representa uma seção de nível superior, representa uma subseção dentro da seção de nível.
      - `element_locations`: uma matriz que especifica os valores `begin` e `end` das sentenças na seção.
    - `leading_sentences`: uma matriz que contém um objeto por seção ou subseção, em paralelo com a matriz `section_titles`, que detalha as sentenças iniciais na seção ou subseção correspondente. Como na matriz `section_titles`, os objetos não são aninhados; em vez disso, eles são comprimidos e podem ser colocados de volta em ordem usando os valores `begin` e `end` do elemento ou quaisquer marcadores de nível no documento de entrada.
      - `text`: uma sequência que lista a sentença inicial, se detectada.
      - `location`: o local da sentença inicial no documento de entrada, conforme definido por seus índices `begin` e `end`.
      - `element_locations`: uma matriz que especifica os valores `begin` e `end` das sentenças iniciais na seção.
  - `parties`: uma matriz que define as partes que são identificadas pelo serviço.
    - `party`: um valor de sequência que identifica a parte.
    - `role`: um valor de sequência que identifica a função da parte.
    - `importance`: um valor de sequência que identifica a importância da parte. Os valores possíveis incluem `Primary` para uma parte primária e `Unknown` para uma parte não primária.
    - `addresses`: uma matriz de objetos que identificam endereços.
      - `text`: uma sequência que contém o endereço.
      - `location`: o local do endereço conforme definido por seus índices `begin` e `end`.
    - `contacts`: uma matriz que define o nome e a função de contatos que são identificados no documento de entrada.
      - `name`: uma sequência que lista o nome de um contato identificado.
      - `role`: uma sequência que lista a função do contato identificado.  
  - `effective_dates`: uma matriz que identifica as datas de vigência do documento.
    - `text`: uma data de vigência, que é listada como uma sequência.
    - `confidence_level`: o nível de confiança da identificação da data de vigência. Os valores possíveis incluem `High`, `Medium` e `Low`.
    - `location`: o local da data, conforme definido por seus índices `begin` e `end`.
  - `contract_amounts`: uma matriz que identifica as quantias monetárias que são identificadas no documento.
    - `text`: uma quantia de contrato, que é listada como uma sequência.
    - `confidence_level`: o nível de confiança da identificação da quantia do contrato. Os valores possíveis incluem `High`, `Medium` e `Low`.    
    - `location`: o local da quantia ou quantias conforme definido por seus índices `begin` e `end`.
  - `termination_dates`: uma matriz que identifica as datas de rescisão do documento.
    - `text`: uma data de rescisão, que é listada como uma sequência.
    - `confidence_level`: o nível de confiança da identificação da data de rescisão. Os valores possíveis incluem `High`, `Medium` e `Low`.    
    - `location`: o local da data, conforme definido por seus índices `begin` e `end`.

** \ *Notas sobre tabelas: **
  - Os valores de índice da linha e da coluna por célula são baseados em zero e, portanto, iniciam com `0`.
  - Múltiplos valores em matrizes de elementos `row_header_ids` e `row_header_texts` indicam uma possível hierarquia de cabeçalhos de linha.
  - Múltiplos valores em matrizes de elementos `column_header_ids` e `column_header_texts` indicam uma possível hierarquia de cabeçalhos de coluna.
