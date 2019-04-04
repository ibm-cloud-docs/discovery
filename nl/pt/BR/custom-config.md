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

# Referência de configuração
{: #configref}

Será possível criar sua própria configuração de ingestão do {{site.data.keyword.discoveryshort}} no
JSON se seus dados tiverem necessidades especiais de [conversão](#conversion),
[enriquecimento](#enrichment) ou [normalização](#normalization).
{: shortdesc}

As seções a seguir detalham a estrutura deste JSON e o objeto que pode ser definido nele.

Se a sua coleção tiver sido criada usando o [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu), as configurações de conversão de PDF e Word listadas não serão usadas. Portanto, a mudança dessas configurações de conversão será ignorada.
{: note}

## Estrutura de configuração
{: #structure}

Uma configuração do {{site.data.keyword.discoveryshort}} é estruturada como segue:

```json
{
  "name": "Configuration Name",
  "description": "Descriptive text about the configuration",
  "conversions": {
    "word": {},
    "pdf": {},
    "html": {},
    "segment": {},
    "json_normalizations": []
  },
  "enrichments": [],
  "normalizations": []
}
```
{: codeblock}

O objeto JSON base contém os itens a seguir:

-  `"name": "Configuration Name"` - o nome de sua configuração
-  `"description": "Descriptive text about the configuration"` - uma descrição de sua
configuração

Os objetos e matrizes a seguir devem ser definidos para converter, enriquecer e normalizar documentos que
são transferidos por upload para sua coleção.

- `"conversions": {}` - como os documentos são transformados em JSON que podem ser
enriquecidos.
- `"enrichments": []` - quais enriquecimentos são aplicados a quais partes do JSON.
- `"normalizations": []` - quaisquer ajustes de pós-enriquecimento que são necessários
antes que o documento seja armazenado.

Além disso, os seguintes itens são incluídos no objeto base pelo
{{site.data.keyword.discoveryshort}} quando a configuração é criada/atualizada:

```json
{
  "configuration_id": "4f5b7c7b-ebf4-4963-882e-27eff08f08e3",
  "created": "2017-09-13T14:45:03.575Z",
  "updated": "2017-09-13T14:45:03.575Z"
}
```
{: codeblock}

## Conversão
{: #conversion}

A conversão de documentos usa o formato de origem original e o uso de uma ou mais etapas o transforma em
JSON, que poderá ser usado para o restante do processo de ingestão. Dependendo do tipo de arquivo transferido
por upload, o processo é o seguinte:

- Arquivos **PDF** são convertidos em HTML usando as opções `pdf`,
em seguida, o **HTML** resultante é convertido em JSON usando as opções
`html` e, finalmente, o **JSON** resultante é convertido usando as
opções `json`.

- Arquivos **Microsoft Word** são convertidos em HTML usando as opções
`word`, em seguida, o **HTML** resultante é convertido em JSON
usando as opções `html` e, finalmente, o **JSON** resultante é convertido
usando as opções `json`.

- Arquivos **HTML** são convertidos em JSON usando as opções `html`
e o **JSON** resultante é convertido usando as opções `json`.

- Arquivos **JSON** são convertidos usando as opções `json`.

Se a sua coleção tiver sido criada usando o [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu), as configurações de conversão de PDF e Word listadas não serão usadas. Portanto, a mudança dessas configurações de conversão será ignorada.
{: note}

Essas opções são descritas nas seções a seguir. Depois que a conversão é concluída,
o [enriquecimento](#enrichment) e a [normalização](#normalization) são
executados antes que o conteúdo seja armazenado.

### PDF
{: #pdf}

Se a sua coleção tiver sido criada usando o [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu), as configurações de conversão de PDF e Word listadas não serão usadas. Portanto, a mudança dessas configurações de conversão será ignorada.
{: note}

O objeto de conversão `pdf` define como os documentos PDF devem ser convertidos em HTML
e possui a estrutura a seguir:

```json
"pdf": {
  "heading": {
    "fonts": [ {
        "level": 1,
        "min_size": 24,
        "max_size": 80,
        "bold": false,
        "italic": true,
        "name": "arial"
      },
      {
        "level": 2,
        "min_size": 18,
        "max_size": 24,
        "bold": true,
        "italic": false,
        "name": "ariel"
      }
    ]
  }
},
```
{: codeblock}

Ao converter os arquivos PDF, os títulos nesses arquivos podem ser identificados (e
convertidos em uma tag "`h`" HTML apropriada) identificando o tamanho, a fonte e o estilo de
cada nível de título. Os níveis de título podem ser especificados várias vezes, se necessário, para
identificar corretamente todas as seções relevantes. É importante identificar os níveis de título HTML
se você planeja extrair o conteúdo usando seletores CSS ou se pretende dividir o documento usando divisão de
documento. O objeto `title` contém a matriz `fonts` e cada item
nessa matriz especifica um nível de título usando os parâmetros a seguir:

- `"level": INT` - *obrigatório* - o nível HTML `h` que o texto identificou com esses parâmetros será convertido.
- `"min_size": INT` - _opcional_ - o menor tamanho de letra que é identificado como este nível de título.
- `"max_size": INT` - _opcional_ - o maior tamanho da fonte que é identificado como este nível de título.
- `"bold": boolean` - _opcional_ - Quando `true` somente fontes em negrito são identificadas como este nível de título.
- `"italic": boolean` - _opcional_ - Quando `true` somente fontes em itálico são identificadas como este nível de título.
- `"name": "string"` - _opcional_ - o nome da fonte que é identificado como esse nível de título.

Para que uma área de texto seja identificada como um título, ela deve corresponder a todos os parâmetros
definidos no item de matriz específico. Se os parâmetros definidos forem muito flexíveis, será possível ter mais títulos identificados do que você previa. Você terá melhores resultados se você definir rigorosamente cada nível de cabeçalho várias vezes para garantir que todas as variações do nível de cabeçalho sejam incluídas sem combinações inválidas.


### Palavra
{: #word}

Se a sua coleção tiver sido criada usando o [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu), as configurações de conversão de PDF e Word listadas não serão usadas. Portanto, a mudança dessas configurações de conversão será ignorada.
{: note}

O objeto de conversão `word` define como os documentos PDF devem ser
convertidos em HTML e possui a seguinte estrutura:

```json
"word": {
  "heading": {
    "fonts": [ {
        "level": 1,
        "min_size": 24,
        "bold": true,
        "italic": false,
        "name": "arial"
      },
      {
        "level": 2,
        "min_size": 18,
        "max_size": 23,
        "bold": true,
        "italic": false
      }
    ],
    "styles": [
      {
        "level": 1,
        "names": [
          "pullout heading",
          "pulloutheading",
          "header"
        ]
      },
      {
        "level": 2,
        "names": [
          "subtitle"
        ]
      }
    ]
  }
},
```
{: codeblock}

O objeto de conversão do Microsoft Word funciona de maneira semelhante ao objeto de conversão PDF. No
entanto, há duas matrizes diferentes que podem ser especificadas dentro do objeto
`heading` ao extrair títulos de documentos do Microsoft Word. É possível usar uma ou ambas
as matrizes de extração de título para extrair os elementos de nível de título de seus documentos do Microsoft
Word.

Cada item na matriz `fonts` especifica um nível de título usando os parâmetros
a seguir com as características de fonte:

- `"level": INT` - *obrigatório* - o nível HTML `h` que o texto identificou com esses parâmetros será convertido.
- `"min_size": INT` - _opcional_ - o menor tamanho de letra que é identificado como este nível de título.
- `"max_size": INT` - _opcional_ - o maior tamanho da fonte que é identificado como este nível de título.
- `"bold": boolean` - _opcional_ - Quando `true` somente fontes em negrito são identificadas como este nível de título.
- `"italic": boolean` - _opcional_ - Quando `true` somente fontes em itálico são identificadas como este nível de título.
- `"name": "string"` - _opcional_ - o nome da fonte que é identificado como esse nível de título.

Para que uma área de texto seja identificada como um título na matriz `font`,
ela deve corresponder a todos os parâmetros definidos no item de matriz específico. Se os parâmetros definidos forem muito flexíveis, será possível ter mais títulos identificados do que você previa. Você terá melhores resultados se você definir rigorosamente cada nível de cabeçalho várias vezes para garantir que todas as variações do nível de cabeçalho sejam incluídas sem combinações inválidas.

Cada item na matriz `styles` especifica um nível de título dos estilos do Microsoft Word
que são aplicados a esse parágrafo.

- `"level": INT` - *obrigatório* - o nível HTML `h` que o texto identificou com esses parâmetros será convertido.
- `"names": array` - *obrigatório* - uma matriz separada por vírgula
de nomes de estilo que serão identificados como esse nível de título.

*Quando usar fontes e quando usar estilos* - se seus documentos do Microsoft Word
estão em boa conformidade com a folha de estilo com cada parágrafo identificado corretamente com o estilo apropriado, então
recomenda-se o uso de `styles` para extrair títulos. No entanto, talvez você ache que
alguns documentos têm estilos que foram substituídos manualmente pelo escritor. Esses documentos são mais
propensos a fornecer uma boa conversão quando o método de extração `fonts` é usado.
{: tip}


### HTML
{: #html}

```json
"html": {
  "exclude_tags_completely": [
    "script", "sup"
  ], "exclude_tags_keep_content": [
    "font",
    "em"
  ], "exclude_content": {
    "xpaths": [
      "//*[@id='list-old']",
      "//*[@id='unstable']"
    ]
  }, "keep_content": {
    "xpaths": [
      "//*[@id='footer']",
      "//*[@id='header']"
    ]
  }, "exclude_tag_attributes": [
    "EVENT_ACTIONS"
  ],
  "keep_tag_attributes": [
    "id"
  ], "extracted_fields": {
    "{field_name}": {
      "css_selector": "{CSS_selector_expression_1}",
      "type": "{field_type}"
    }
  }
},
```
{: codeblock}

#### exclude_tags_completely
{: #configref_exclude_completely}

`"exclude_tags_completely": array` - uma matriz de nomes de tag HTML que será
excluída. Isso inclui a tag, o conteúdo e quaisquer atributos de tag que estejam definidos.

#### exclude_tags_keep_content
{: #configref_exclude_tags_keep_content}

`"exclude_tags_keep_content": array` - uma matriz de nomes de tag HTML em que as
informações da tag são removidas. Isso resulta na remoção da tag HTML e de quaisquer atributos de tag. O conteúdo da tag não é removido adicionalmente, a menos que especificado. Por exemplo, se você especificar
`exclude_tags_keep_content` para a tag HTML `span`, então
`<span class="info">Some <strong>Information</strong></span>` será removido
para: `Some <strong>Information</strong>`

#### exclude_content
{: #configref_exclude_content}

`"xpaths": array` - uma matriz de XPaths que identificam o conteúdo que é removido. Se
esse valor for configurado, tudo o que corresponder a um dos XPaths será removido da saída.

#### keep_content
{: #configref_keep_content}

`"xpaths": array` - uma matriz de XPaths que identificam o conteúdo que é convertido. Se esse valor for configurado, tudo o que corresponder a um dos XPaths será incluído na saída. As inclusões especificadas por esse parâmetro são processadas após qualquer processamento especificado por `exclude_content`.

#### exclude_tag_attributes
{: #configref_exclude_tag_attributes}

`"exclude_tag_attributes": array` - uma matriz de nomes de atributos HTML que são
removidos pela conversão, independentemente da tag HTML na qual eles estiverem presentes. **Nota:** você receberá uma mensagem de erro se especificar `exclude_tag_attributes` e `keep_tag_attributes` na mesma configuração - somente um pode ser especificado por uma configuração. Se presente, `keep_tag_attributes` deve ser removido completamente da configuração; ele não pode estar presente como uma matriz vazia.

#### keep_tag_attributes
{: #configref_keep_tag_attributes}

`"keep_tag_attributes": array` - uma matriz de nomes de atributos HTML que são retidos
pela conversão. **Nota:** você receberá uma mensagem de erro se especificar `keep_tag_attributes` e `exclude_tag_attributes` na mesma configuração - somente um pode ser especificado por configuração. Se presente, `exclude_tag_attributes` deve ser removido completamente da configuração; ele não pode estar presente como uma matriz vazia.

#### extracted_fields
{: #configref_extracted}

Este objeto define qualquer conteúdo da origem HTML que deve ser extraído em um campo JSON separado como
parte da conversão. O conteúdo é identificado utilizando os seletores CSS.

Cada campo que você deseja criar é definido por um objeto como segue:

```json
"{field_name}": {
  "css_selector": "{CSS_selector_expression_1}", "type": "{field_type}"
}
```
{: codeblock}

- `"{field_name}"` - o nome do campo a ser criado.

**Observação:** os nomes de campos definidos na sua configuração devem atender às restrições definidas em [Requisitos de nome de campo](#field_reqs).

- `"css_selector": string` *obrigatório*, uma expressão do seletor CSS
que define a área de conteúdo a ser armazenada em um campo.
- `"type": string` *obrigatório* - o tipo de campo a ser criado, pode
ser `string` ou `date`. Para obter informações detalhadas, consulte
[Usando seletores CSS para extrair campos](/docs/services/discovery?topic=discovery-configservice#using-css).

### Segmento
{: #segment}

O objeto `segment` é um conjunto de opções de configuração que dividem os documentos
alimentados em um ou mais segmentos com base nos títulos HTML identificados (`h1`,
`h2`).

```json
"segment": {
  "enabled": true,
  "selector_tags": ["h1", "h2", "h3", "h4", "h5", "h6"]
}
```
{: codeblock}

- `"enabled": boolean` - *obrigatório* - deve ser configurado como
`true` para ativar a segmentação do documento.
- `"selector_tags": array` - *obrigatório* - uma matriz separada por vírgula
de tags `h` HTML nas quais os documentos são divididos.

Como uma visão geral, quando a segmentação de documento é ativada, o seguinte não pode ser especificado:

-  `json_normalizations` não pode ser especificado como parte da configuração.
-  `normalizations` não pode ser especificado como parte da configuração.
-  A opção `extracted_fields` da conversão `html` não pode
ser especificada como parte da configuração.

Para obter informações detalhadas, consulte
[Executando segmentação](/docs/services/discovery?topic=discovery-configservice#performing-segmentation).


### JSON
{: #json}

É possível executar a normalização de pré-enriquecimento do JSON alimentado definindo objetos
`operation` na matriz `json_normalizations`.

```json
"json_normalizations": [
  {
    "operation": "remove",
    "source_field": "header"
  },
  {
    "operation": "copy",
    "source_field": "title",
    "destination_field": "title_old"
  },
  {
    "operation": "move",
    "destination_field": "content",
    "source_field": "body"
  },
  {
    "operation": "merge",
    "source_field": "synopsis",
    "destination_field": "preamble"
  },
  {
    "operation": "remove_nulls"
  }
]
```
{: codeblock}

#### Objetos de operações
{: #operations}

- `"operation": string` - *obrigatório* - a operação que será
executada no JSON, deve ser uma das seguintes:
  - `remove` - o `source_field` especificado será removido do JSON.
  - `copy` - o conteúdo de `source_field` especificado será copiado
para uma nova instância do `destination_field`.
  - `mover` - o `source_field` especificado é renomeado para
`destination_field`. Se o `destination_field` já existir, uma nova instância
do `destination_field` será criada.
  - `merge` - os conteúdos do `source_field` e do
`destination_field` são mesclados no `destination_field`.
  - `remove_nulls` - campos com conteúdo `null` são
removidos.
- `"source_field": string` - _opcional_ - o campo no qual a operação será
executada.
- `"destination_field": string` - _opcional_ - o campo de destino no qual
a operação será gerada.  

  **Observação:** os nomes de campos definidos na sua configuração devem atender às restrições definidas em [Requisitos de nome de campo](#field_reqs).


## Enriquecimentos
{: #enrichments}

```json
"enrichments": [ {
    "enrichment": "elements",
    "source_field": "html",
    "destination_field": "enriched_html",
    "options": {
      "model": "contract" }
  },
  {
    "enrichment": "natural_language_understanding",
    "source_field": "title",
    "destination_field": "enriched_title",
    "options": {
      "features": {
        "keywords": {
          "sentiment": true, "emotion": false, "limit": 50
        },
        "entities": {
          "sentiment": true,
          "emotion": false,
          "limit": 50,
          "mentions": true,
          "mention_types": true,
          "sentence_locations": true,        
          "model": "WKS-model-id"
        }, "sentiment": {
          "document": true, "targets": [
            "IBM", "Watson" ]

        },
        "emotion": {
          "document": true, "targets": [
            "IBM", "Watson" ]
        },
        "categories": {},
        "concepts": {
          "limit": 8
        },
        "semantic_roles": {
          "entities": true,
          "keywords": true,
          "limit": 50
        }, "relations": {
          "model": "WKS-model-id"
        }
      }
    }
  }
]
```
{: codeblock}

O {{site.data.keyword.discoveryshort}} suporta a inclusão dos enriquecimentos
{{site.data.keyword.nlushort}} e Classificação de Elementos. Cada campo que você deseja enriquecer é
definido por um objeto na matriz `enrichments`. Cada objeto de enriquecimento requer que um
`source_field`, um `destination_field` e enriquecimentos sejam especificados.

- `"enrichment": string` - *obrigatório* - o tipo de enriquecimento a
ser usado neste campo. Para extrair enriquecimentos do {{site.data.keyword.nlushort}}, use
`natural_language_understanding` e para executar Classificação de Elementos, use
`elements`.

  **Observação:** ao usar o enriquecimento de `elements`, é importante seguir as diretrizes especificadas na documentação[Classificação de elemento](/docs/services/discovery?topic=discovery-element-classification#element-classification). Especificamente, apenas os arquivos PDF podem ser alimentados quando este enriquecimento é especificado.

- `"source_field": string` - *obrigatório* - o campo de origem que será
enriquecido. Este campo deverá existir em sua origem após a operação `json_normalizations`
ter sido concluída.
- `"destination_field": string` - *obrigatório* - o nome do objeto
contêiner no qual os enriquecimentos serão criados.

  **Observação:** os nomes de campos definidos na sua configuração devem atender às restrições definidas em [Requisitos de nome de campo](#field_reqs).

### Enriquecimentos Classificação de Elementos
{: #element_classification_enrichments}

Ao usar Classificação de Elementos, cada objeto de enriquecimento `elements`
deve conter um objeto `"options": {}` com os seguintes parâmetros especificados:

- `"model": string` - *obrigatório* - o modelo de extração elemento a ser
usado neste documento. Os modelos suportados atualmente são: `contract`

**Observação:** ao usar o enriquecimento de `elements`, é importante seguir as diretrizes especificadas na documentação[Classificação de elemento](/docs/services/discovery?topic=discovery-element-classification#element-classification). Especificamente, apenas os arquivos PDF podem ser alimentados quando este enriquecimento é especificado.

### Enriquecimentos do Natural Language Understanding
{: #nlu_enrichments}

Ao usar o {{site.data.keyword.nlushort}}, cada objeto na matriz `enrichments` também
deve conter um objeto `"options": { "features": { } }` que contenha um ou mais dos seguintes
enriquecimentos:

### Categorias
{: #nlu_categories}

O enriquecimento `categories` identifica quaisquer categorias gerais
no documento alimentado. Esse enriquecimento não tem opções e deve ser especificado como um objeto vazio
`"categories": {}`

### conceitos
{: #nlu_concepts}

O enriquecimento `concepts` localiza conceitos aos quais o texto de
entrada está associado, com base em outros conceitos e entidades que estão presentes nesse texto.

- `"limit": INT` - *obrigatório* - o número máximo de conceitos para
extrair do documento alimentado.

### Emoção
{: #nlu_emotion}

O enriquecimento `emotion` avalia o tom emocional geral (por exemplo,
`anger`) do documento inteiro ou das sequências de destino especificadas no documento inteiro. Este enriquecimento pode ser usado apenas com conteúdo em inglês.

- `"document": boolean` _opcional_ - quando `true`, o
tom emocional do documento inteiro é avaliado.
- `"targets": array` _opcional_ - Uma matriz separada por vírgula
de sequências de destino que avaliam o estado emocional dentro do documento.

### entidades
{: #nlu_entities}

O enriquecimento `entities` extrai instâncias de entidades
conhecidas, como pessoas, locais e organizações. Opcionalmente, um modelo customizado do
{{site.data.keyword.knowledgestudioshort}} pode ser especificado para extrair entidades customizadas.

- `"sentiment": boolean` - _opcional_ - quando `true`, a
análise de sentimentos é executada na entidade extraída no contexto do conteúdo circundante.
- `"emotion" : boolean` - _opcional_ - quando `true`,
a análise de tom emocional é executada na entidade extraída no contexto do conteúdo circundante.
- `"limit": INT` - _opcional_ - o número máximo de entidades a serem
extraídas do documento alimentado. O padrão é `50`.
- `"mentions": boolean` - _opcional_ - quando `true`, o
número de vezes que esta entidade é mencionada é registrado. O padrão
é `false`.
- `"mention_types": boolean` - _opcional_ - quando
`true`, o tipo de menção para cada menção dessa entidade é armazenado. O padrão
é `false`.
- `"sentence_location": boolean` - _opcional_ - quando
`true`, o local da sentença de cada menção de entidade é armazenado. O padrão
é `false`.
- `"model": string` - _opcional_ - quando especificado, o modelo
customizado é usado para extrair entidades em vez do modelo público. Essa opção requer que um modelo customizado do {{site.data.keyword.knowledgestudioshort}} seja associado à sua instância do {{site.data.keyword.discoveryshort}}. Consulte [Integrando com o Watson Knowledge Studio](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-with-wks) para obter mais informações.

### palavras-chave
{: #nlu_keywords}

O enriquecimento `keywords` extrai instâncias de palavras significativas
dentro do texto. Para entender a diferença entre palavras-chave, conceitos e entidades, consulte:
[Entendendo a diferença entre Entidades, Conceitos e
Palavras-chave](/docs/services/discovery?topic=discovery-configservice#udbeck).

- `"sentiment": boolean` - _opcional_ - quando `true`, a
análise de sentimentos é executada na palavra-chave extraída no contexto do conteúdo
circundante.
- `"emotion": boolean` - _opcional_ - quando `true`,
a análise de tom emocional é executada na palavra-chave extraída no contexto do conteúdo circundante.
- `"limit": INT` - _opcional_ - o número máximo de palavras-chave a
serem extraídas do documento alimentado. O padrão é `50`.

### semantic_roles
{: #nlu_semantic_roles}

O enriquecimento `semantic_roles` identifica componentes de sentença, como assunto,
ação e objeto dentro do texto alimentado.

- `"entities": boolean` - _opcional_ quando `true`,
as entidades são extraídas dos componentes de sentença.
- `"keywords": boolean` - _opcional_ - quando
`true`, palavras-chave são extraídas dos componentes de sentença.
- `"limit": INT` - _opcional_ - o número máximo de
objetos `semantic_roles` a serem extraídos (sentenças para analisar) do documento
alimentado. O padrão é `50`.

### Sentimento
{: #nlu_sentiment}

O enriquecimento `sentiment` avalia o nível geral de sentimento do documento inteiro ou
as sequências de destino especificadas no documento inteiro.

- `"document": boolean` _opcional_ - quando `true`, a
impressão do documento inteiro é avaliada.
- `"targets": array` _opcional_ - uma matriz separada por vírgula de
sequências de destino para avaliar o sentimento de dentro do documento.

### relações
{: #nlu_relations}

O enriquecimento `relations` extrai relacionamentos conhecidos
entre entidades identificadas no documento. Opcionalmente, um modelo customizado do
{{site.data.keyword.knowledgestudioshort}} pode ser especificado para extrair
relacionamentos customizados.

- `"model": string` - _opcional_ - quando especificado, o modelo
customizado é usado para extrair as relações em vez do modelo público. Essa opção requer que um modelo customizado do {{site.data.keyword.knowledgestudioshort}} seja associado à sua instância do {{site.data.keyword.discoveryshort}}. Consulte [Integrando com o Watson Knowledge Studio](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-with-wks) para obter mais informações.

## Normalização
{: #normalization}

`Normalizations` é uma matriz de objetos `operation` JSON que
são usados para limpar o JSON alimentado após os `enrichments` terem sido aplicados e antes de
ele ser armazenado.

```json
"normalizations": [
  {
    "operation": "remove",
    "source_field": "enriched_title.entities.text"
  },
  {
    "operation": "copy",
    "source_field": "enriched_title.sentiment.document.score",
    "destination_field": "titlescore"
  }
]
```
{:codeblock}

As opções do objeto `operation` estão listadas [aqui](#operations)

## Requisitos de nome do campo
{: #field_reqs}

Os nomes de campos não podem conter espaços. Os caracteres e sequências a seguir são reservados e não
podem ser usados em nomes de campo:


```
  .  ,  # ? :
  id
  score
  highlight
  result_metadata
```
{: pre}

Os caracteres `_`, `+` e `-` não podem ser usados
para o prefixo `field_name`

Caracteres numéricos `0-9` não devem ser usados como sufixo de um nome de campo (por
exemplo, `extracted-content2`). Esses nomes de campo serão indexados, mas não podem ser
consultados.
