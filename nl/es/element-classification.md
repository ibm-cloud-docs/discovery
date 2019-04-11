---

copyright:
  years: 2015, 2018, 2019
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

# Clasificación de elementos
{: #element-classification}

La clasificación de elementos permite analizar rápidamente los documentos normativos para convertir, identificar y clasificar elementos de importancia. Con la ayuda de la última tecnología del NLP (Natural Language Processing), es posible extraer de elementos del documento la parte (a quién se refiere el documento), la naturaleza (el tipo del elemento) y la categoría (clase específica).

La clasificación de elementos está diseñada para proporcionar:

-  Entendimiento del lenguaje natural de contratos, con un interés especial en contratos de suministros de software
-  La posibilidad de convertir PDF programático en JSON anotado
-  Identificación de categorías y entidades legales que se alinean con el área de conocimiento del tema

La clasificación de elementos reúne también un amplio conjunto de funcionalidades de API integradas y automatizadas de Watson para especificar como entrada PDF programáticos para identificar: secciones, listas (numeradas o con viñetas), notas de pie de página y tablas; convirtiendo estos elementos en un formato HTML estructurado. Además, la clasificación de este formato estructurado se anota y explicita como JSON con categorías, tipos y elementos anotados.

La clasificación de elementos transmite los datos de forma segura al cifrarlos mientras se transiten o cuando están en reposo. Para obtener información sobre la seguridad de IBM Cloud, consulte la [Descripción del servicio {{site.data.keyword.Bluemix_notm}}![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=%28IBM+Cloud+Service+description%29){: new_window}

La clasificación de elementos devuelve un objeto JSON que contiene:

-  Un objeto `documents` que incluye el título del documento de entrada, una versión HTML del documento de entrada y el hash MD5 del documento de entrada.
-  Información sobre el modelo utilizado para clasificar el documento de entrada.  
-  Una matriz `elementos` que detalla los elementos identificados en el documento de entrada.
-  Una matriz `tablas` que divide las tablas identificadas en el documento de entrada.
-  Un objeto `document_structure` que enumera los títulos de sección y las frases principales identificadas en el documento de entrada.
-  Una matriz `partes` que enumera las partes, roles, direcciones y contactos de las partes identificados en el documento de entrada.
-  Matrices que definen `effective_dates`, `contract_amounts` y `termination_dates`.

Actualmente, esta característica solo está soportada en inglés, consulte [Soporte de idiomas](/docs/services/discovery?topic=discovery-language-support#feature-support) para obtener detalles.


## Requisitos de clasificación
{: #element-class}

Para clasificar documentos mediante la clasificación de elementos, la configuración y los documentos de origen deben cumplir los siguientes requisitos:

-  Los archivos a analizar deben estar en formato PDF.
-  El contenido de PDF está en formato de texto. Los documentos que se han escaneado no se pueden analizar aunque se hayan procesado mediante un lector de caracteres óptico (OCR).
   **Nota:** Puede identificar si un PDF posee texto abriendo el documento en un visor de PDF y utilizando la herramienta **Seleccionar texto** para seleccionar una única palabra. Si no puede seleccionar una única palabra en el documento, el archivo no se puede analizar.
-  Los archivos no pueden tener un tamaño superior a 50 Mb.
-  No es posible analizar PDF protegidos (con una contraseña para poder abrirlos) y cuya edición esté restringida (con una contraseña para poder editarlos).
-  El conjunto de herramientas de {{site.data.keyword.discoveryshort}} incluye una configuración denominada **Configuración de contrato predeterminada** que puede utilizarse para enriquecer su recopilación de documentos PDF. También puede crear una configuración personalizada que incluya el enriquecimiento `elements`. Consulte [Requisitos de recopilación](/docs/services/discovery?topic=discovery-element-classification#element-collection) para obtener detalles.
-  Los planes **Lite** pueden procesar un máximo de 500 páginas al mes.
-  No está disponible en los entornos **Dedicados**.
-  No es posible realizar la normalización posterior al enriquecimiento cuando se utiliza la Clasificación de elementos.

**Nota:** El archivo **Configuración de contrato predeterminada** se actualizó el 25 de septiembre de 2018. Si aplicó esta configuración a una recopilación anterior a esta fecha, consulte las [notas del release](/docs/services/discovery?topic=discovery-release-notes#25sept) para obtener información sobre cómo actualizar su recopilación.

## Requisitos de recopilación
{: #element-collection}

Para utilizar la clasificación de elementos, la configuración de su recopilación debe cumplir con requisitos específicos.

El conjunto de herramientas de {{site.data.keyword.discoveryshort}} incluye una configuración denominada **Configuración de contrato predeterminada** que se ha configurado previamente para enriquecer los documentos PDF con el enriquecimiento **Clasificación de elementos** y otras opciones necesarias. Podrá eligir esta configuración cuando cree su recopilación. El JSON para esta configuración es:

```json
 {
   "name": "Default Contract Configuration",
   "description": "Extract party, nature, and category from elements in PDFs.",
  "conversions": {
     "html": {
       "exclude_tags_completely": [],
       "exclude_tags_keep_content": []
     }
   },
   "enrichments": [
     {
       "source_field": "html",
       "destination_field": "enriched_html_elements",
       "enrichment": "elements",
       "options": {
         "model": "contract"
    }
     }
   ]
 }
```
{: codeblock}

Si desea crear un archivo de configuración personalizado, configure la recopilación para que cumpla con los requisitos siguientes:  

-  Los valores de conversión de `PDF` se ignoran si se especifican.
-  Los valores de conversión de `WORD` se pueden omitir puesto que los archivos de Microsoft Word no se pueden ingerir cuando se especifica la clasificación de elementos.
-  Los valores de normalización de `html` se ignoran si se especifican.
-  La segmentación de documentos no está soportada cuando se especifica el enriquecimiento `elements`.
-  En la configuración de {{site.data.keyword.discoveryshort}}, el campo `html` se debe enriquecer con el enriquecimiento `elements` y el `model` especificado como `contract`. En el siguiente ejemplo, `destination_field` es `enriched_html`, pero se puede utilizar cualquier otro valor válido:

```json
 "enrichments": [
   {
     "source_field": "html",
    "destination_field": "enriched_html",
    "enrichment": "elements",
    "options": {
       "model": "contract"
    }
   }
 ]
```
{: codeblock}

Podrá cargar los documentos después de seleccionar la `Configuración de contrato predeterminada` en el conjunto de herramientas. Si no está familiarizado con la creación de recopilaciones y la carga de documentos, consulte [Iniciación al conjunto de herramientas](/docs/services/discovery?topic=discovery-getting-started#getting-started).

## Elementos clasificados
{: #classified-elements}

Una vez que un documento se ha indexado con la clasificación de elementos, será devuelto con una matriz `elements` como parte del documento en el que se podrán realizar búsquedas.

Cada objeto de la matriz `elementos` describe un elemento del contrato que {{site.data.keyword.discoveryshort}} ha identificado. El código siguiente representa un elemento típico:

```json
 {
    "location" : {
     "begin" : 134323,
     "end" : 135109
    },
    "text" : "9. In the event that the Participant's total vested account balance is determined to be less than or equal to $2,000.00 as of the date that the Order is received, the parties will be informed in writing that the QDRO determination fee may potentially liquidate the account.",
   "types" : [ {
      "label" : {
        "nature": "Obligation",
			"party": "All Parties"
      },
      "provenance_ids" : ["Nlu0ogWAEGms4vjhhzpMv3iXhm8b8fBqMBNtT/bXH8JI=", "PlyERkjg5is36RpFjVUFXp69eDmGmCxLCXRs1sDMDUCo="
      ]
    } ],
   "categories" : [ {
      "label" : "Communication",
      "provenance_ids" : [ "Cs38YyU6VBFtJK1/bgtEJBlqqWmX5F6OYUciRxQXf7HrN5TOCPuI7QXbkbj4LRXoxVuB3/i9H15q5TU+vFxorhUBeWFfF998OYQiPYViD2yI="
      ]
    } ],
    "attributes" : [ {
      "type" : "Currency",
      "text" : "$2,000.00",
      "location" : {
        "begin" : 134780,
        "end" : 134789
      }
    } ]
 }
 ```
{: codeblock}

Cada elemento tiene cinco secciones importantes:
-  `location`: Los índices `begin` y `end` que indican la ubicación del elemento en el documento de entrada.
-  `text`: El texto del elemento clasificado.
-  `types`: Una matriz que incluye ninguno o varios objetos `label`. Cada objeto `label` incluye un campo `nature` que muestra el efecto del elemento en la parte identificada (por ejemplo, `Derecho` o `Exclusión`) y un campo `party` que identifica la parte o partes afectadas por el elemento. Consulte [Tipos](/docs/services/discovery?topic=discovery-contract_parsing#contract_types) en [Comprensión del análisis del contrato](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing) para obtener más información.
-  `categories`: Una matriz que contiene ninguno o varios objetos `label`. El valor de cada objeto `label` enumera una categoría funcional en la que se encuentra el elemento identificado. Consulte [Categorías](/docs/services/discovery?topic=discovery-contract_parsing#contract_categories) en [Comprensión del análisis del contrato](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing) para obtener más información.
-  `attributes`: Una matriz que enumera ninguno o varios objetos que definen atributos del elemento. Los objetos soportados actualmente incluyen `Location` (ubicación geográfica a la que hace referencia el elemento), `DateTime` (fecha, hora, rango de fechas o rango de hora especificados por el elemento) y `Currency` (valores y unidades monetarias). Cada objeto de la matriz `attributes` también incluye el texto y la ubicación del elemento identificado; la ubicación la definen los índices `begin` y `end` del texto en el documento de entrada. Consulte [Atributos](/docs/services/discovery?topic=discovery-contract_parsing#attributes) en [Análisis de contratos](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing) para obtener información adicional.

Además, cada objeto de las matrices `types` y `categories` incluye una matriz `provenance_ids`. Los valores enumerados en la matriz `provenance_ids` son valores hash que puede enviar a IBM para proporcionar comentarios o recibir soporte acerca de la parte del análisis asociado con el elemento. 

Algunas frases no están bajo ningún tipo o categoría, en cuyo caso el servicio devuelve las matrices `types` y `categories` como objetos vacíos.
{: note}

Algunas frases cubren varios temas, en cuyo caso el servicio devuelve varios conjuntos de objetos `types` y `categories`.
{: note}

Algunas frases no contienen ningún atributo identificable, en cuyo caso el servicio devuelve la matriz `attributes` como objetos vacíos.
{: note}
