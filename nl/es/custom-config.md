---

copyright:
  years: 2015, 2018
lastupdated: "2018-01-23"

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

# Referencia de configuración

Tiene la posibilidad de crear su propia configuración de ingestión de {{site.data.keyword.discoveryshort}} en formato JSON si sus datos tienen unas necesidades especiales de [conversión](#conversion), [enriquecimiento](#enrichment) o [normalización](#normalization).
{: shortdesc}

 Las siguientes secciones detallan la estructura de este JSON y los objetos que se pueden definir en el mismo.

## Estructura de configuración
{: #structure}

Una configuración de {{site.data.keyword.discoveryshort}} está estructurada de la siguiente manera:

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

El objeto JSON base contiene los siguientes elementos:

-  `"name": "Configuration Name"` - Nombre de la configuración
-  `"description": "Descriptive text about the configuration"` - Descripción de la configuración.

Los siguientes objetos y matrices se deben definir para convertir, enriquecer y normalizar documentos que se cargan en su recopilación.

- `"conversions": {}` - Indica cómo se pueden enriquecer los documentos que se transforman en JSON.
- `"enrichments": []` - Indica los enriquecimientos que se aplican y a qué partes del JSON.
- `"normalizations": []` - Ajustes posteriores al enriquecimiento necesarios antes de almacenar el documento.

Además, {{site.data.keyword.discoveryshort}} añade los elementos siguientes al objeto base al crear/actualizar la configuración:

```json
{
  "configuration_id": "4f5b7c7b-ebf4-4963-882e-27eff08f08e3",
  "created": "2017-09-13T14:45:03.575Z",
  "updated": "2017-09-13T14:45:03.575Z"
}
```
{: codeblock}

## Conversión
{: #conversion}

La conversión de documentos toma el formato origen original y utilizando uno o varios pasos lo transforma en un formato JSON que utiliza el resto del proceso de ingestión. Dependiendo del tipo de archivo cargado, el proceso es el siguiente:

- Los archivos **PDF** se convierten a HTML utilizando las opciones `pdf`, el **HTML** resultante se convierte entonces a JSON utilizando las opciones `html`, y por último, el **JSON** resultante se convierte con las opciones `json`.

- Los archivos **Microsoft Word** se convierten a HTML utilizando las opciones `word`, el **HTML** resultante se convierte entonces a JSON utilizando las opciones `html`, y por último, el **JSON** resultante se convierte con las opciones `json`.

- Los archivos **HTML** se convierten a JSON utilizando las opciones `html` y el **JSON** resultante se convierte con las opciones `json`.

- Los archivos **JSON** se convierten con las opciones `json`.

Estas opciones se describen en las secciones siguientes. Una vez se completa la conversión, se realiza el [enriquecimento](#enrichment) y la [normalización](#normalization) antes de almacenar el contenido.

### PDF
{: #pdf}

El objeto de conversión `pdf` define la forma en la que se convierten los documentos PDF en HTML. Este objeto tiene la siguiente estructura:

```json
"pdf": {
  "heading": {
    "fonts": [
      {
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

Al convertir archivos PDF, es posible identificar cabeceras en dichos archivos (y convertirlas en la etiqueta HTML "`h`" adecuada) mediante la identificación del tamaño, el font y el estilo de cada nivel de cabecera. Los niveles de cabecera se pueden especificar varias veces si es necesario con el propósito de identificar correctamente todas las secciones significativas. Los niveles de cabecera HTML son importantes para la identificación si tiene previsto extraer los contenidos con selectores CSS, o si pretende dividir el documento utilizando la división de documentos. El objeto `heading` contiene la matriz `fonts` donde cada elemento en la matriz especifica un nivel de cabecera con los siguientes parámetros:

- `"level": INT` - *necesario* - Nivel HTML de `h` en el que se convertirá el texto identificado por estos parámetros.
- `"min_size": INT` - _opcional_ - Tamaño de font más pequeño que se identificará como perteneciente a este nivel de cabecera.
- `"max_size": INT` - _opcional_ - Tamaño de font más grande que se identificará como perteneciente a este nivel de cabecera.
- `"bold": boolean` - _opcional_ - Cuando se establece en `true`, únicamente los fonts en negrita se identificarán como pertenecientes a este nivel de cabecera.
- `"italic": boolean` - _opcional_ - Cuando se establece en `true`, únicamente los fonts en cursiva se identificarán como pertenecientes a este nivel de cabecera.
- `"name": "string"` - _opcional_ - Nombre del font que se identificará como perteneciente a este nivel de cabecera.

Para un área de texto que se deba identificar como una cabecera se deberán satisfacer todos los parámetros definidos en el elemento de matriz específico. Si los parámetros definidos son demasiado flexibles, podría identificar más cabeceras de las anticipadas. Tendrá mejores resultados si se define estrictamente cada nivel de cabecera varias veces para asegurarse de que todas las variantes del nivel de cabecera se incluyen sin falsas coincidencias.


### Word
{: #word}

El objeto de conversión `word` define la forma en la que se convierten los documentos PDF en HTML. Este objeto tiene la siguiente estructura:

```json
"word": {
  "heading": {
    "fonts": [
      {
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

El objeto de conversión de Microsoft Word funciona de forma similar al objeto de conversión de PDF. Sin embargo, hay dos matrices diferentes que se pueden especificar dentro el objeto `heading` al extraer cabeceras de los documentos Microsoft Word. Puede utilizar una o ambas matrices de extracción de cabeceras para extraer elementos de nivel de cabecera de los documentos de Microsoft Word.

Cada elemento en la matriz `fonts` especifica un nivel de cabecera con los siguientes parámetros utilizando características de font:

- `"level": INT` - *necesario* - Nivel HTML de `h` en el que se convertirá el texto identificado por estos parámetros.
- `"min_size": INT` - _opcional_ - Tamaño de font más pequeño que se identificará como perteneciente a este nivel de cabecera.
- `"max_size": INT` - _opcional_ - Tamaño de font más grande que se identificará como perteneciente a este nivel de cabecera.
- `"bold": boolean` - _opcional_ - Cuando se establece en `true`, únicamente los fonts en negrita se identificarán como pertenecientes a este nivel de cabecera.
- `"italic": boolean` - _opcional_ - Cuando se establece en `true`, únicamente los fonts en cursiva se identificarán como pertenecientes a este nivel de cabecera.
- `"name": "string"` - _opcional_ - Nombre del font que se identificará como perteneciente a este nivel de cabecera.

Para un área de texto que se deba identificar como una cabecera en la matriz `font` se deberán satisfacer todos los parámetros definidos en el elemento de matriz específico. Si los parámetros definidos son demasiado flexibles, podría identificar más cabeceras de las anticipadas. Tendrá mejores resultados si se define estrictamente cada nivel de cabecera varias veces para asegurarse de que todas las variantes del nivel de cabecera se incluyen sin falsas coincidencias.

Cada elemento en la matriz `styles` define un nivel de cabecera a partir de los estilos de Microsoft Word que se aplican a los párrafos.

- `"level": INT` - *necesario* - Nivel HTML de `h` en el que se convertirá el texto identificado por estos parámetros.
- `"names": array` - *necesario* - Matriz separada por comas de nombres de estilo que se identificarán como este nivel de cabecera.

*Cuándo utilizar fonts y cuándo utilizar estilos* -
Si sus documentos de Microsoft Word se ajustan bien a la hoja de estilo y cada párrafo está correctamente etiquetado con el estilo apropiado, es más recomendable utilizar `estilos` para extraer las cabeceras. Sin embargo, podría encontrarse de que algunos documentos tienen estilos que el autor haya sobrescrito de forma manual. Es más probable proporcionar una buena conversión para estos documentos cuando se utiliza el método de extracción de `fonts`.
{: tip}


### HTML
{: #html}

```json
"html": {
  "exclude_tags_completely": [
    "script",
    "sup"
  ],
  "exclude_tags_keep_content": [
    "font",
    "em"
  ],
  "exclude_content": {
    "xpaths": [
      "//*[@id='list-old']",
      "//*[@id='unstable']"
    ]
  },
  "keep_content": {
    "xpaths": [
      "//*[@id='footer']",
      "//*[@id='header']"
    ]
  },
  "exclude_tag_attributes": [
    "EVENT_ACTIONS"
  ],
  "keep_tag_attributes": [
    "id"
  ],
  "extracted_fields": {
    "{field_name}": {
      "css_selector": "{CSS_selector_expression_1}",
      "type": "{field_type}"
    }
  }
},
```
{: codeblock}

#### exclude_tags_completely

`"exclude_tags_completely" : array` - Matriz de nombres de etiqueta HTML que se excluirán. Incluye la etiqueta, el contenido y los atributos de etiqueta definidos.

#### exclude_tags_keep_content

`"exclude_tags_keep_content" : array` - Matriz de nombres de etiqueta HTML donde la información de etiqueta es eliminada. Esto da lugar a la eliminación de todos los atributos en las etiquetas HTML. El contenido de la etiqueta no se elimina a no ser que así se especifique. Por ejemplo, si especifica `exclude_tags_keep_content` para la etiqueta HTML `span`, entonces `<span class="info">Some <strong>Information</strong></span>` quedará como: `Some <strong>Information</strong>`.

#### exclude_content

`"xpaths" : array` - Matriz de varios XPath que identifican el contenido que se elimina. Si se establece este valor, todo lo que coincida con uno de los XPath se eliminará de la salida.

#### keep_content

`"xpaths" : array` - Matriz de varios XPath que identifican el contenido que se convierte. Si se establece este valor, todo lo que coincida con uno de los XPath se incluirá en la salida. Las inclusiones que especifica este parámetro se procesan después de cualquier otro proceso que `exclude_content` haya especificado.

#### exclude_tag_attributes

`"exclude_tag_attributes" : array` - Matriz de nombres de atributo HTML que la conversión elimina independientemente de la etiqueta HTML en la que se presentan. **Nota:** Recibirá un mensaje de error si especifica `exclude_tag_attributes` y `keep_tag_attributes` en la misma configuración; solo se puede especificar uno por configuración. Si está presente, `keep_tag_attributes` debe eliminarse por completo de la configuración; no puede estar presente como matriz vacía.

#### keep_tag_attributes

`"keep_tag_attributes" : array` - Matriz de nombres de atributo HTML que la conversión retiene. **Nota:** Recibirá un mensaje de error si especifica `keep_tag_attributes` y `exclude_tag_attributes` en la misma configuración; solo se puede especificar uno por configuración. Si está presente, `exclude_tag_attributes` debe eliminarse por completo de la configuración; no puede estar presente como matriz vacía.

#### extracted_fields

Este objeto define cualquier contenido del origen HTML que se extrae en un campo JSON separados como parte de la conversión. El contenido se identifica mediante selectores CSS.

Cada campo que desea crear se define mediante un objeto tal como se indica a continuación:

```json
"{field_name}": {
  "css_selector": "{CSS_selector_expression_1}",
  "type": "{field_type}"
}
```
{: codeblock}

- `"{field_name}"` - Nombre del campo a crear.

**Nota:** Los nombres de campo definidos en su configuración deben satisfacer las restricciones que se definen en los [Requisitos de nombre de campo](#field_reqs).

- `"css_selector" : string` *necesario* - Expresión de selector CSS que define el área de contenido a almacenar en un campo.
- `"type" : string` *necesario* - Tipo de campo a crear, puede ser `string`, `date`. Para obtener información detallada, consulte [Utilización de selectores CSS para extraer campos](/docs/services/discovery/building.md#using-css).

### Segmento
{: #segment}

El objeto `segment` es un conjunto de opciones de configuración que dividen documentos ingeridos en uno o varios segmentos que se basan en las cabeceras HTML identificadas (`h1`, `h2`).

```json
"segment": {
  "enabled": true,
  "selector_tags": ["h1", "h2", "h3", "h4", "h5", "h6"]
}
```
{: codeblock}

- `"enabled": boolean` - *necesario* - Debe ser `true` para habilitar la segmentación de documentos.
- `"selector_tags": array` - *necesario* - Matriz separada por comas de etiquetas HTML `h` por las que dividir documentos.

En términos generales, cuando se habilita la segmentación de documentos no es posible especificar lo siguiente:

-  `json_normalizations` no se puede especificar como parte de la configuración.
-  `normalizations` no se puede especificar como parte de la configuración.
-  La opción `extracted_fields` de la conversión `html` no se puede especificar como parte de la configuración.

Para obtener información detallada, consulte [Cómo realizar una segmentación](/docs/services/discovery/building.html#performing-segmentation).


### JSON
{: #json}

Puede realizar la normalización con anterioridad al enriquecimiento del JSON ingerido definiendo objetos `operation` en la matriz `json_normalizations`.

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

#### Objetos de operaciones
{: #operations}

- `"operation": string` - *necesario* - Operación que se realizará en el JSON. Debe ser una de las siguientes:
  - `remove` - Se eliminará del JSON el `source_field` especificado.
  - `copy` - Se copiará en la nueva instancia el contenido `source_field` especificado en una nueva instancia de `destination_field`.
  - `move` - El `source_field` especificado se renombrará como `destination_field`. Si `destination_field` ya existe, se creará una nueva instancia de `destination_field`.
  - `merge` - El contenido de `source_field` y `destination_field` se fusionará en `destination_field`.
  - `remove_nulls` - Se eliminan los campos con contenido `null`.
- `"source_field": string` - _opcional_ - Campo en el que se realizará la operación.
- `"destination_field": string` - _opcional_ - El campo de destino para la salida de la operación.  

  **Nota:** Los nombres de campo definidos en su configuración deben satisfacer las restricciones que se definen en los [Requisitos de nombre de campo](#field_reqs).


## Enriquecimientos
{: #enrichments}

```json
"enrichments": [
   {
    "enrichment": "elements",
    "source_field": "html",
    "destination_field": "enriched_html",
    "options": {
      "model": "contract"
    }
  },
  {
    "enrichment": "natural_language_understanding",
    "source_field": "title",
    "destination_field": "enriched_title",
    "options": {
      "features": {
        "keywords": {
          "sentiment": true,
          "emotion": false,
          "limit": 50
        },
        "entities": {
          "sentiment": true,
          "emotion": false,
          "limit": 50,
          "mentions": true,
          "mention_types": true,
          "sentence_locations": true,        
          "model": "WKS-model-id"
        },
        "sentiment": {
          "document": true,
          "targets": [
            "IBM",
            "Watson"
          ]

        },
        "emotion": {
          "document": true,
          "targets": [
            "IBM",
            "Watson"
          ]
        },
        "categories": {},
        "concepts": {
          "limit": 8
        },
        "semantic_roles": {
          "entities": true,
          "keywords": true,
          "limit": 50
        },
            "relations": {
          "model": "WKS-model-id"
        }
      }
    }
  }
]
```
{: codeblock}

{{site.data.keyword.discoveryshort}} da soporte a la adición de enriquecimientos de Clasificación de elementos y {{site.data.keyword.nlushort}}. Cada campo que desee enriquecer se define mediante un objeto en la matriz `enrichments`. Cada objeto de enriquecimiento precisa especificar un `source_field`, un `destination_field` y los enriquecimientos.

- `"enrichment" : string` - *necesario* - Tipo de enriquecimiento que utilizará este campo. Para extraer enriquecimientos de {{site.data.keyword.nlushort}} utilice `natural_language_understanding`, para realizar la Clasificación de elementos utilice `elements`.

  **Nota:** Al utilizar el enriquecimiento `elements`, es importante seguir las directrices que se especifican en la documentación de [Clasificación de elementos](/docs/services/discovery/element-classification.html). En concreto, sólo se pueden ingerir archivos PDF cuando se especifica este enriquecimiento.

- `"source_field" : string` - *necesario* - Campo origen que se enriquecerá. Este campo debe existir en su origen después de que se haya completado la operación `json_normalizations`.
- `"destination_field" : string` - *necesario* - Nombre del objeto contenedor donde se crearán los enriquecimientos.

  **Nota:** Los nombres de campo definidos en su configuración deben satisfacer las restricciones que se definen en los [Requisitos de nombre de campo](#field_reqs).

### Enriquecimientos de Clasificación de elementos

Al utilizar la Clasificación de elementos, cada objeto de enriquecimiento `elements` debe contener un objeto `"options": {}` especificando los siguientes parámetros:

- `"model" : string` - *necesario* - Modelo de extracción que se utilizará en este documento. Actualmente los modelos soportados son: `contract`

**Nota:** Al utilizar el enriquecimiento `elements`, es importante seguir las directrices que se especifican en la documentación de [Clasificación de elementos](/docs/services/discovery/element-classification.html). En concreto, sólo se pueden ingerir archivos PDF cuando se especifica este enriquecimiento.

### Enriquecimientos de NLU (Natural Language Understanding)

Al utilizar {{site.data.keyword.nlushort}}, cada objeto dentro de una matriz `enrichments` también debe contener un objeto `"options": { "features": { } }` que contiene uno o varios de los siguientes enriquecimientos:

### categories

El enriquecimiento `categories` identifica todas las categorías generales en el documento ingerido. Este enriquecimiento no tiene opciones y se debe especificar como un objeto vacío `"categories" : {}`

### concepts

El enriquecimiento `concepts` encuentra conceptos a los que está asociado el documento de entrada, basándose en otros conceptos y entidades presentes en dicho texto.

- `"limit" : INT` - *necesario* - Número máximo de conceptos a extraer del documento ingerido.

### emotion

El enriquecimiento `emotion` evalúa el tono emocional general (por ejemplo enfado (`anger`)) de todo el documento o de series específicas en el documento. Este enriquecimiento sólo se puede utilizar con contenido en el idioma inglés.

- `"document" : boolean ` _opcional_ - Cuando se establece en `true`, se evalúa el tono emocional de todo el documento.
- `"targets" : array ` _opcional_ - Matriz separada por comas de series de destino para evaluar su estado emocional dentro del documento.

### entidades

El enriquecimiento `entities` extrae instancias de entidades conocidas como, por ejemplo, personas, lugares y organizaciones. De forma opcional, se puede especificar un modelo personalizado de {{site.data.keyword.knowledgestudioshort}} para extraer entidades personalizadas.

- `"sentiment" : boolean` - _opcional_ - Cuando se establece en `true`, se realiza el análisis del sentimiento en las entidades extraídas en el contexto del contenido que lo rodea.
- `"emotion" : boolean` - _opcional_ - Cuando se establece en `true`, se realiza el análisis del tono emocional en las entidades extraídas en el contexto del contenido que lo rodea.
- `"limit" : INT` - _opcional_ - Número máximo de entidades a extraer del documento ingerido. El valor predeterminado es `50`.
- `"mentions": boolean` - _opcional_ - Cuando se establece en `true`, se registra el número de veces que se menciona esta entidad. El valor predeterminado es `false`.
- `"mention_types": boolean` - _opcional_ - Cuando se establece en `true`, se almacena el tipo de mención de cada mención de esta entidad. El valor predeterminado es `false`.
- `"sentence_location": boolean` - _opcional_ - Cuando se establece en `true`, se almacena la ubicación de la frase de cada mención de la entidad. El valor predeterminado es `false`.
- `"model" : string` - _opcional_ - Cuando se especifica, se utiliza el modelo personalizado para extraer entidades en lugar del modelo público. Esta opción precisa un modelo personalizado de {{site.data.keyword.knowledgestudioshort}} para asociarlo con su instancia de {{site.data.keyword.discoveryshort}}. Consulte [Integración con Watson Knowledge Studio](/docs/services/discovery/integrate-wks.html) para obtener más información.

### keywords

El enriquecimiento `keywords` extrae instancias de palabras significativas dentro del texto. Para entender la diferencia entre palabras claves, conceptos y entidades, consulte: [Diferencias entre entidades, conceptos y palabras clave](/docs/services/discovery/building.html#udbeck).

- `"sentiment" : boolean` - _opcional_ - Cuando se establece en `true`, se realiza el análisis del sentimiento en la palabra clave extraída en el contexto del contenido que lo rodea.
- `"emotion" : boolean` - _opcional_ - Cuando se establece en `true`, se realiza el análisis del tono emocional en la palabra clave extraída en el contexto del contenido que lo rodea.
- `"limit" : INT` - _opcional_ - Número máximo de palabras clave a extraer del documento ingerido. El valor predeterminado es `50`.

### semantic_roles

El enriquecimiento `semantic_roles` identifica componentes de frases como sujeto, acción y objeto dentro del texto ingerido.

- `"entities" : boolean` - _opcional_ Cuando se establece en `true`, las entidades se extraen de los componentes de las frases.
- `"keywords" : boolean` - _opcional_ Cuando se establece en `true`, las palabras clave se extraen de los componentes de las frases.
- `"limit" : INT` - _opcional_ - Número máximo de objetos `semantic_roles` para extraer (frases a analizar) del documento ingerido. El valor predeterminado es `50`.

### sentiment

El enriquecimiento `sentiment` evalúa el nivel del sentimiento general de series de destino especificadas en el documento.

- `"document" : boolean ` _opcional_ - Cuando se establece en `true`, se evalúa el sentimiento de todo el documento.
- `"targets" : array ` _opcional_ - Matriz separada por comas de series de destino para evaluar el sentimiento dentro del documento.

### relations

El enriquecimiento `relations` extrae relaciones conocidas entre entidades identificadas dentro del documento. De forma opcional, se puede especificar un modelo personalizado de {{site.data.keyword.knowledgestudioshort}} para extraer relaciones personalizadas.

- `"model" : string` - _opcional_ - Cuando se especifica, se utiliza el modelo personalizado para extraer relaciones en lugar del modelo público. Esta opción precisa un modelo personalizado de {{site.data.keyword.knowledgestudioshort}} para asociarlo con su instancia de {{site.data.keyword.discoveryshort}}. Consulte [Integración con Watson Knowledge Studio](/docs/services/discovery/integrate-wks.html) para obtener más información.

## Normalización
{: #normalization}

`normalizations` es una matriz de objetos JSON `operation` que se utilizan para limpiar el JSON ingerido después de que se hayan aplicado los `enrichments` y antes de almacenarlo.

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

Las opciones del objeto `operation` se listan [aquí](#operations).

## Requisitos de nombre de campo
{: #field_reqs}

Los nombres de los campos no pueden contener espacios. Los siguientes caracteres y series están reservados y no se pueden utilizar en nombres de campo:


```
  .  ,  # ? :
  id
  score
  highlight
  result_metadata
```
{: pre}

Los caracteres `_`, `+` y `-` no se pueden utilizar como prefijo de un `field_name`

Los caracteres numéricos `0 - 9` no se deberían utilizar como sufijo de un nombre de campo (por ejemplo, `extracted-content2`). Estos nombres de campos se indexarán, pero no se podrán utilizar en consultas.
