---

copyright:
years: 2018
lastupdated: "2018-10-23"

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

# Comprensión del esquema de salida
{: #output_schema}

Cuando un documento se haya ingerido mediante la Clasificación de elementos, el servicio proporcionará la salida JSON en el esquema siguiente para la fecha de versión `2018-10-15` o posterior. La salida se incluirá en el objeto `enriched_html_elements`. 

```
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
      "location" : {
        "begin" : int,
        "end" : int
      },
      "text": string,
      "section_title": {
        "text": string,
        "location": {
          "begin" : int,
          "end" : int
        }
      },
      "table_headers" : [
        {
          "cell_id" : string,
          "location" : {
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
    "column_headers": [ {
          "cell_id" : string,
          "location" : {
            "begin" : int,
            "end" : int
          },
          "text" : string,
          "text_normalized" : string,
          "row_index_begin" : int,
          "row_index_end" : int,
          "column_index_begin" : int,
          "column_index_end" : int
        },
        ...
      ],
      "row_headers": [
        {
          "cell_id" : string,
          "location" : {
            "begin" : int,
            "end" : int
          },
          "text" : string,
          "text_normalized" : string,
          "row_index_begin" : int,
          "row_index_end" : int,
          "column_index_begin" : int,
          "column_index_end" : int
        },
        ...
      ],
    "body_cells": [ {
          "cell_id" : string,
          "location" : {
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
          "column_header_texts_normalized": [ string ]
        },
        ...
      ]
    },
    ...
  ],
  "document_structure": {
    "section_titles": [
      {
        "text": string,
        "location": {
          "begin": int,
          "end": int
        },
        "level": int
        "element_locations": [
          {
            "begin": int,
            "end": int
          },
          ...
        ]
      },
      ...
    ],
    "leading_sentences": [
      {
        "text": string,
        "location": {
          "begin": int,
          "end": int
        },
        "element_locations": [
          {
            "begin": int,
            "end": int
          },
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
      "addresses": [
        {
          "text": string,
          "location": {
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
      "text": string,
      "location": { "begin": int, "end": int }
     },
     ...
  ],
  "contract_amounts": [
    {
      "text": string,
      "location": { "begin": int, "end": int }
    },
    ...
  ]
}
```

El esquema se organiza de la manera siguiente.

  - `document`: Un objeto que enumera información básica sobre el documento, incluidos:
    - `title`: El título del documento, si se detecta.
    - `html`: El texto completo del documento de entrada en formato HTML.
    - `hash`: El hash MD5 del documento de entrada.
  - `model_id`: El modelo de análisis que se va a utilizar para clasificar el documento. El valor predeterminado es `contracts`. 
  - `model_version`: La versión del modelo de análisis especificado por el valor del parámetro `model_id`.
  - `elements`: Una matriz de los elementos del documento detectados por el servicio.
    - `location`: La ubicación del elemento como la definen los índices `begin` y `end`.
    - `text`: El texto del elemento.
    - `types`: Una matriz que describe lo que es el elemento y a quién afecta.
      - `label`: Un objeto que define el tipo utilizando un par de los elementos siguientes:
        - `nature`: El tipo de acción que requiere la oración. Los valores actuales son `Definition`, `Disclaimer`, `Exclusion`, `Obligation` y `Right`.
        - `party`: Una cadena que identifica la parte a la que se aplica la oración.
      - `provenance_ids`: Una matriz de uno o varios valores hash que puede enviar a IBM para proporciona comentarios o recibir soporte.
    - `categories`: Una matriz que enumera las categorías funcionales en las que se encuentra el elemento; en otras palabras, el tema del elemento.
      - `label`: Una serie que enumera la categoría identificada. Encontrará una lista de [categorías](/docs/services/discovery/parsing.html#contract_categories) en [Comprensión del análisis del contrato](/docs/services/discovery/parsing.html#contract_parsing).
      - `provenance_ids`: Una matriz de uno o varios valores hash que puede enviar a IBM para proporciona comentarios o recibir soporte.
    - `attributes`: Una matriz que identifica los atributos de documento. Cada objeto de la matriz consiste en tres elementos:
      - `type`: El tipo de atributo. Los valores posibles son `Location` (Ubicación), `DateTime` (Fecha y hora) y `Currency` (Moneda).
      - `text`: El texto que está asociado con el atributo.
      - `location`: La ubicación del atributo como la definen los índices `begin` y `end`.
  - `tables`\*: Una matriz que define las tablas identificadas en el documento de entrada.
    - `location`: La ubicación de la tabla actual como la definen los desplazamientos `begin` (inicio) y `end` (fin) en el documento de entrada.
    - `text`: Los contenidos textuales de la tabla actual del documento de entrada sin contenido de marcación asociado.
    - `section_title`: Si se identifica, la ubicación de un título de sección que contiene la tabla actual. Aparece vacío si no se identifica ningún título de sección.
      - `text`: El texto del título de sección identificado.
      - `location`: La ubicación del título de sección en el documento de entrada como lo definen los índices `begin` y `end`.
    - `table_headers`: Una matriz de las celdas a nivel de tabla aplicables como cabeceras al resto de celdas de la tabla actual. Cada cabecera de tabla se define como una colección de los elementos siguientes:
      - `cell_id`: Valor de serie en el formato `tableHeader-x-y` donde `x` e `y` son los desplazamientos de inicio y fin del valor de celda en el documento de entrada.
      - `location`: La ubicación de la celda en el documento de entrada como lo definen los índices `begin` y `end`.
      - `text`: Los contenidos textuales de la celda del documento de entrada sin contenido de marcación asociado.
      - `row_index_begin`: El índice `begin` de la ubicación `row` de la celda en la tabla actual.
      - `row_index_end`: El índice `end` de la ubicación `row` de la celda en la tabla actual.
      - `column_index_begin`: El índice `begin` de la ubicación `column` de la celda en la tabla actual.
      - `column_index_end`: El índice `end` de la ubicación `column` de la celda en la tabla actual.
    - `column_headers`: Una matriz de las celdas a nivel de columna, cada una aplicable como cabecera a otras celdas en la misma columna de la tabla actual. Cada cabecera de columna se define como una colección de los valores siguientes:
      - `cell_id`: Una valor de serie en el formato `columnHeader-x-y` donde `x` e `y` son los desplazamientos de inicio y fin de la celda de cabecera de columna en el documento de entrada.
      - `location`: La ubicación de la celda en el documento de entrada como lo definen los índices `begin` y `end`.
      - `text`: Los contenidos textuales de la celda del documento de entrada sin contenido de marcación asociado.
      - `text_normalized`: Si proporciona la entrada de personalización, la versión normalizada del texto de la celda de acuerdo con la personalización; de lo contrario, el mismo valor que `text`. 
      - `row_index_begin`: El índice `begin` de la ubicación `row` de la celda en la tabla actual.
      - `row_index_end`: El índice `end` de la ubicación `row` de la celda en la tabla actual.
      - `column_index_begin`: El índice `begin` de la ubicación `column` de la celda en la tabla actual.
      - `column_index_end`: El índice `end` de la ubicación `column` de la celda en la tabla actual.
    - `row_headers`: Una matriz de las celdas a nivel de fila, cada una aplicable como cabecera a otras celdas de la misma fila de la tabla actual. Cada cabecera de fila se define como una colección de los valores siguientes:
      - `cell_id`: Una valor de serie en el formato `rowHeader-x-y` donde `x` e `y` son los desplazamientos de inicio y fin de la celda de cabecera de fila en el documento de entrada.
      - `location`: La ubicación de la celda en el documento de entrada como lo definen los índices `begin` y `end`.
      - `text`: Los contenidos textuales de la celda del documento de entrada sin contenido de marcación asociado.
      - `text_normalized`: Si proporciona la entrada de personalización, la versión normalizada del texto de la celda de acuerdo con la personalización; de lo contrario, el mismo valor que `text`. 
      - `row_index_begin`: El índice `begin` de la ubicación `row` de la celda en la tabla actual.
      - `row_index_end`: El índice `end` de la ubicación `row` de la celda en la tabla actual.
      - `column_index_begin`: El índice `begin` de la ubicación `column` de la celda en la tabla actual.
      - `column_index_end`: El índice `end` de la ubicación `column` de la celda en la tabla actual.
    - `body_cells`: Una matriz de las celdas que no son de cabecera de tabla, cabecera de columna ni cabecera de fila de la tabla actual con las asociaciones de cabecera de columna y fila correspondientes. Cada celda del cuerpo se define como una colección de los valores siguientes:
      - `cell_id`: Una valor de serie en el formato `bodyCell-x-y` donde `x` e `y` son los desplazamientos de inicio y fin de la celda del cuerpo en el documento de entrada.
      - `location`: La ubicación de la celda en el documento de entrada como lo definen los índices `begin` y `end`.
      - `text`: Los contenidos textuales de la celda del documento de entrada sin contenido de marcación asociado.
      - `row_index_begin`: El índice `begin` de la ubicación `row` de la celda en la tabla actual.
      - `row_index_end`: El índice `end` de la ubicación `row` de la celda en la tabla actual.
      - `column_index_begin`: El índice `begin` de la ubicación `column` de la celda en la tabla actual.
      - `column_index_end`: El índice `end` de la ubicación `column` de la celda en la tabla actual.
      - `row_header_ids`: Una matriz de valores, que son el valor `cell_id` de una cabecera de fila aplicable a la celda del cuerpo.
      - `row_header_texts`: Una matriz de valores, que son el valor `text` (texto_celda) de una cabecera de fila aplicable a la celda del cuerpo.
      - `row_header_texts_normalized`: Si proporciona la entrada de personalización, la versión normalizada de los textos de la cabecera de fila de la celda de acuerdo con la personalización; de lo contrario, el mismo valor que `row_header_texts`. 
      - `column_header_ids`: Una matriz de valores, que son el valor `cell_id` de una cabecera de columna aplicable a la celda del cuerpo.
      - `column_header_texts`: Una matriz de valores, que son el valor `text` (texto_celda) de una cabecera de columna aplicable a la celda del cuerpo.
      - `column_header_texts_normalized`: Si proporciona la entrada de personalización, la versión normalizada de los textos de la cabecera de fila de la celda de acuerdo con la personalización; de lo contrario, el mismo valor que `column_header_texts`.
  - `document_structure`: Un objeto que describe la estructura del documento de entrada.
    - `section_titles`: Una matriz que contiene un objeto por sección o subsección detectada en el documento de entrada. Las secciones y subsecciones no están anidadas; en su lugar, están planas y se pueden volver a colocar por orden utilizando los valores `begin` y `end` del elemento y el valor `level` de la sección.
      - `text`: Una serie que lista el título de sección, si se detecta.
      - `location`: La ubicación del título en el documento de entrada como lo definen los índices `begin` y `end`.
      - `level`: Un entero que indica el nivel en el que se encuentra la sección en el documento de entrada. Por ejemplo, `1` representa una sección de nivel superior, `2` representa una subsección del nivel `1` y así sucesivamente.
      - `element_locations`: Una matriz que contiene objetos que especifican los valores `begin` y `end` de las frases de la sección.
    - `leading_sentences`: Una matriz que contiene un objeto por sección o subsección, en paralelo con la matriz `section_titles` que detalla las frases principales de la sección o subsección coincidentes. Al igual que en la matriz `section_titles`, los objetos no están anidados; están planos y se pueden volver a colocar por orden mediante los valores `begin` y `end` del elemento o cualquier marcador de nivel del documento de entrada.
      - `text`: Una serie que enumera la frase principal, si se detecta.
      - `location`: La ubicación de la frase principal en el documento de entrada como lo definen los índices `begin` y `end`.
      - `element_locations`: Una matriz que contiene objetos que especifican los valores `begin` y `end` de las frases principales de la sección.
  - `parties`: Una matriz que define las partes identificadas por el servicio.
    - `party`: Un valor de serio que identifica la parte.
    - `role`: Un valor de serie que identifica el rol de la parte.
    - `addresses`: Una matriz de objetos que identifican direcciones.
      - `text`: Una serie que contiene la dirección.
      - `location`: La ubicación de la dirección como la definen los índices `begin` y `end`.
    - `contacts`: Una matriz que define el nombre y el rol de los contactos identificados en el documento de entrada.
      - `name`: Una serie que lista el nombre de un contacto identificado.
      - `role`: Una serie que lista el rol del contacto identificado.  
  - `effective_dates`: Una matriz que identifica las fechas efectivas del documento.
    - `text`: Las fechas efectivas, listadas como una serie.
    - `location`: La ubicación de la fecha o fechas como las definen los índices `begin` y `end`.
  - `contract_amounts`: Una matriz que identifica los importes monetarios identificados en el documento.
    - `text`: Los importes del contrato, listados como una serie.
    - `location`: La ubicación del importe o importes como las definen los índices `begin` y `end`.

**\*Notas sobre las tablas:**
  - Los valores de índice de columna y fila por celda están basados en cero y empiezan por `0`.
  - Los valores múltiples en las matrices de los elementos `row_header_ids` y `row_header_texts` indican una jerarquía de las cabeceras de fila.
  - Los valores múltiples en las matrices de los elementos `column_header_ids` y `column_header_texts` indican una jerarquía de cabeceras de columna.
