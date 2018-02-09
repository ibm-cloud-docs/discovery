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

# Mejora de la relevancia de los resultados con la API

El servicio {{site.data.keyword.discoveryshort}} se puede entrenar para mejorar la relevancia de los resultados de las consultas para su área de interés u organización concreta. Cuando se proporciona una instancia de {{site.data.keyword.discoveryshort}} con el *
entrenamiento de datos*, el servicio utiliza técnicas de entrenamiento máquina de Watson para encontrar señales en el contenido y en las preguntas. A continuación, el servicio reordena los resultados de la consulta para mostrar en primer lugar los resultados más relevantes. A medida que se añaden datos de entrenamiento, la instancia del servicio cada vez es más precisa y sofisticada en la ordenación de los resultados que devuelve.
{: shortdesc}

El entrenamiento de relevancia es opcional; si los resultados de sus consultas satisfacen sus necesidades, no es necesario un entrenamiento adicional. Para obtener una visión general de situaciones adecuadas para el entrenamiento, consulte el artículo de blog [Cómo sacar el mayor partido al entrenamiento de relevancia ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/dwblog/2017/get-relevancy-training/){: new_window}. 

Para obtener una amplia información sobre las API de entrenamiento, consulte la [Referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}. 

Si prefiere utilizar el conjunto de herramientas de {{site.data.keyword.discoveryshort}} para realizar el entrenamiento de {{site.data.keyword.discoveryshort}}, consulte [Mejora de la relevancia de los resultados con el conjunto de herramientas](/docs/services/discovery/train-tooling.html). 

**Nota:** El entrenamiento de relevancia necesita determinados requisitos de datos de entrenamiento antes de ser efectivo. El servicio comprueba los datos de entrenamiento de forma periódica para determinar si se satisfacen estos requisitos, y se actualiza a sí mismo de forma automática con base a los cambios. 

**Nota:** El entrenamiento de relevancia solo se aplica a las consultas de lenguaje natural en recopilaciones privadas. No está pensado para ser utilizado con consultas estructuradas de {{site.data.keyword.discoveryshort}} Query Language. Para obtener más información sobre {{site.data.keyword.discoveryshort}} Query Language, consulte [Conceptos de consultas](/docs/services/discovery/using.html). 

Las recopilaciones entrenadas devolverán una puntuación de `confidence` en el resultado de una consulta de lenguaje natural. Consulte [Puntuaciones de confianza](/docs/services/discovery/train-tooling.html#confidence) para obtener más información. 

**Nota:** Hay un máximo de 4 recopilaciones entrenadas por entorno.

<!-- A trained Discovery service instance is intended primarily for use with natural language queries, but it works equally well with queries that use structured syntax. -->  <!-- See [Query Concepts](/docs/services/discovery/using.html) and the [Query reference](/docs/services/discovery/query-reference.html) for information about structured queries and natural language queries. -->

Los componentes necesarios para entrenar una instancia de Discovery incluyen lo siguiente: 

 - **Datos de entrenamiento**. Es un conjunto de *consultas* y *ejemplo* que el servicio utiliza para refinar resultados de consultas. 
 - **Consulta**. Una consulta de lenguaje natural que se aplica al conjunto de datos de entrenamiento. Cada consulta tiene uno o varios *ejemplos* asociados, tal como se describe en el siguiente punto de la lista. Cada consulta debe ser exclusiva dentro del conjunto de datos de entrenamiento. 
 - **Ejemplo**. Es un documento indexado en una recopilación de Discovery que actúa como ejemplar, con **exactitud o inexactitud**, para la consulta asociada. Cuando se añade un ejemplo a una consulta de datos de entrenamiento, se incluye una etiqueta de relevancia que indica la relevancia (o "exactitud" con relación a su "inexactitud") del documento en la medida que se aplica a la consulta especificada. 

   Los ejemplos se identifican mediante el ID de documento indexado. Como se ha dicho, cada documento debe incluir una etiqueta que indique su "exactitud" o "inexactitud" de pertenencia a la consulta. 

   Los ejemplos opcionalmente pueden especificar una consulta de referencias cruzadas. La consulta de referencia cruzada solo necesita devolver el documento de ejemplo y debe ser independiente del ID de documento de Watson Discovery exclusivo. Las consultas de referencia cruzada actualmente no se utilizan automáticamente pero se pueden utilizar para reparar datos de entrenamiento en el caso de que se asignen nuevos ID a documentos durante un suceso de ingestión. 

## Requisitos de datos de entrenamiento

Los datos de entrenamiento deben satisfacer los siguientes criterios de calidad **mínimos** para mejorar de forma efectiva la relevancia de las respuestas que el servicio Discovery devuelve. Tenga presente que **mínimos** no significa **óptimos**.

- El conjunto de datos de entrenamiento de la recopilación debe contener un mínimo de 49 consultas de entrenamiento exclusivas (esto es, conjuntos de consultas y ejemplos). Dependiendo del tamaño y la complejidad de su recopilación, el número de consultas de entrenamiento en su conjunto podría precisar de más de 49 antes que de Watson puede aplicar el entrenamiento de relevancia a la recopilación. 
- La puntuación de relevancia para cada consulta de entrenamiento debe ser un entero no negativo, por ejemplo, `0` para representar *no relevante*, `1` para representar *parcialmente relevante* y `2` para representar *altamente relevante*. Sin embargo, para ofrecer la mayor flexibilidad posible, el servicio acepta enteros no negativos entre `0` y `100` para que usuarios avanzados experimenten con distintos esquemas de puntuación. Independientemente del rango que utilice, el mayor entero en el conjunto de consultas de entrenamiento indica la máxima relevancia. El conjunto de herramientas de {{site.data.keyword.discoveryshort}} utiliza las puntuaciones de relevancia de `0` para representar *no relevante* y `10` para representar *relevante*. Si tiene previsto puntuar sus documentos tanto con el conjunto de herramientas de {{site.data.keyword.discoveryshort}} como con la API, o si tiene previsto empezar con la API para pasar al conjunto de herramientas, utilice las puntuaciones de relevancia entre `0` y `10`. 
- Las consultas de entrenamiento deben incluir alguna superposición de términos entre la consulta y la respuesta deseada de forma que pueda ser recuperada por la búsqueda inicial del servicio Discovery, que tiene un ámbito más amplio. 

**Nota:** Watson utiliza datos de entrenamiento para entrenar patrones y generalizar, no memoriza consultas de entrenamiento concretas. Por lo tanto el servicio no siempre reproduce resultados de relevancia idénticos para una consulta de entrenamiento dada. 

## Adición de una consulta al conjunto de datos de entrenamiento

Utilice el método `POST /v1/environments/{environment_id}/collections/{collection_id}/training_data` para añadir un conjunto de datos de entrenamiento de una recopilación. La consulta se especifica como un objeto JSON con el formato siguiente: 

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

Los valores en este objeto son los siguientes:

- `query_id`: ID exclusivo para la consulta. Si no especifica este campo, el servicio genera automáticamente un ID.
- `natural_language_query`: Consulta de lenguaje natural de Discovery que se aplica al conjunto de entrenamiento. <!-- The `natural_language_query` parameter is preferred. -->
- `filter`: Parámetro opcional para la consulta, tal como se describe en la [Referencia de consultas](/docs/services/discovery/query-reference.html#parameter-descriptions).

    **Nota:** Si incluye filtros en sus consultas de datos de entrenamiento, asegúrese de utilizar los mismos filtros al utilizar consultas de lenguaje natural en la recopilación entrenada. Si entrena la recopilación con datos filtrados y no utiliza los mismos tipos de filtros al consultar la recopilación, los resultados podrían ser impredecibles. 

- `examples`: Matriz que contiene los valores siguientes:

   - `document_id`: ID exclusivo del documento que se aplica al conjunto de entrenamiento. Se trata del *example* descrito con anterioridad.  
   - `cross_reference`: Etiqueta opcional, habitualmente formada por un campo en el documento referenciado, que "fija" el documento y la información del campo en el caso de que el ID del documento cambie, por ejemplo, si un nuevo documento ingestado se asigna al mismo ID. Especificar un valor para `cross-reference` **no** enlaza un documento con otro, sino que asegura que el servicio conservará la pertinente información del documento en caso de que se cambie su nombre o sea sobrescrito. 
   - `relevance`: Entero entre `0` y `100`, ambos incluidos, que indican la relevancia relativa de la consulta para los datos de entrenamiento. Valores elevados indican una mayor relevancia. Un valor de `0` indica que no hay relevancia para la consulta, mientras que un valor de `100` indica una relevancia absoluta para la consulta. 

   **Nota:** Aunque el rango del parámetro `relevance` está entre `0` y `100`, para una mayor flexibilidad, es posible utilizar un rango más reducido para simplificar la puntuación de los ejemplos.  Un rango estándar podría estar entre `0` y `4`, o se podría utilizar todo el rango a base de incrementos de 20 unidades (`0`,`20`,`40`,`60`,`80` y `100`). El conjunto de herramientas de {{site.data.keyword.discoveryshort}} utiliza las puntuaciones de relevancia de `0` para representar *no relevante* y `10` para representar *relevante*. Si tiene previsto puntuar sus documentos tanto con el conjunto de herramientas de {{site.data.keyword.discoveryshort}} como con la API, o si tiene previsto empezar con la API para pasar al conjunto de herramientas, utilice las puntuaciones de relevancia entre `0` y `10`. 

El objeto siguiente muestra una consulta de datos de entrenamiento cumplimentada. 

```json
{
  "natural_language_query": "why is the sky blue",
  "filter": "text:meteorology",
  "examples": [
    {
      "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877",
      "relevance": 0
    },
    {
      "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81",
      "relevance": 1
    },
    {
      "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da",
      "cross_reference": "my_id_field:1463",
      "relevance": 4
    }
  ]
}
```
{: codeblock}

A continuación se muestra un ejemplo de mandato que añade una consulta de datos de entrenamiento anterior a la recopilación denominada `99040100-fe6a-4782-a4f5-28f9eee30850` en el entorno denominado `a56dd9b4-040b-4ea3-a736-c1e7a467e191`:

```bash
curl -X POST -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" -H "Content-Type: application/json" -d
'{
  "natural_language_query": "why is the sky blue",
  "filter": "text:meteorology",
  "examples": [
    {
    "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877",
    "relevance": 0
    },
    {
      "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81",
      "relevance": 1
    },
    {
      "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da",
      "cross_reference": "my_id_field:1463",
      "relevance": 4
    }
  ]
}'
"https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data?version=2016-12-01"
```
{: pre}

## Adición de un ejemplo a una consulta de datos de entrenamiento

Después de crear una consulta de datos de entrenamiento, puede continuar añadiendo ejemplos a la misma para mejorar la precisión del entrenamiento. Utilice `POST /v1/environments/{environment_id}/collections/{collection_id}/training_data/{query_id}` para añadir un ejemplo a una consulta de datos de entrenamiento existente. 

Siga los siguientes pasos para añadir un ejemplo a una consulta de datos de entrenamiento. 

1. Obtenga el ID de la consulta de la consulta de datos de entrenamiento que desea añadir al nuevo ejemplo [listando las consultas de datos de entrenamiento de la recopilación ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#get-training-data){: new_window}:

   ```bash
    curl -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" "https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data?version=2016-12-01"
   ```
   {: pre}

   El JSON devuelto tendrá el siguiente formato: 

   ```json
    {
      "query_id": "484baad4-d440-44b7-a0dd-70bb2ac77baa",
      "natural_language_query": "why is the sky blue",
      "filter": "text:meteorology",
      "examples": [
        {
          "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877",
          "relevance": 0
        },
        {
          "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81",
          "relevance": 1
        },
        {
          "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da",
          "cross_reference": "my_id_field:1463",
          "relevance": 4
        }
      ]
    }
   ```
   {: codeblock}

1. Añada el nuevo ejemplo mediante la misma sintaxis se utiliza para definir los ejemplos al crear una nueva consulta de datos de entrenamiento. El siguiente mandato de ejemplo no incluye una referencia cruzada. 

   ```bash
    curl -u -X POST -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" -H "Content-Type: application/json" -d
    '{
      "document_id": "46b52fdc-3a72-4700-9849-ac217532b373",
      "relevance": 3
    }' "https://gateway.watsonplatform.net/discovery/api/v1/environments//a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data/484baad4-d440-44b7-a0dd-70bb2ac77baa?version=2016-12-01"
   ```
   {: pre}

1. Verifique que el nuevo ejemplo se haya añadido a la consulta de datos de entrenamiento [listando de nuevo las consultas de datos de entrenamiento de la recopilación ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#get-training-data){: new_window}:

   ```bash
    curl -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" "https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data?version=2016-12-01"
   ```
   {: pre}

   El JSON devuelto tendrá el siguiente formato: 

   ```json
    {
      "query_id": "484baad4-d440-44b7-a0dd-70bb2ac77baa",
      "natural_language_query": "why is the sky blue",
      "filter": "text:meteorology",
      "examples": [
        {
          "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877",
          "relevance": 0
        },
        {
          "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81",
          "relevance": 1
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

1. Compruebe el estado del entrenamiento utilizando el método para [listar los detalles de la recopilación ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#list-collection-details){: new_window} y busque la información del campo `"training"`/`"available"`. Cuando se hayan añadido suficientes consultas y ejemplos para satisfacer sus requisitos, el valor del campo devuelve `true` y el servicio de forma automática empieza a utilizar los datos de entrenamiento. 

   ```bash
    curl -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" "https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850?version=2016-12-01"
   ```
   {: pre}

   El JSON devuelto tendrá el siguiente formato: 

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
        "available": 1000,
        "processing": 20,
        "failed": 180
      },
      "training": {
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

1. Cuando los campos siguientes en el paso anterior devuelvan todos ellos `true`, emita algunas consultas de ejemplo para ver si el servicio devuelve los resultados más relevantes:

   - `minimum_queries_added`
   - `minimum_examples_added`
   - `sufficient_label_diversity`

   Si la relevancia de sus resultados no mejora, añada más consultas de entrenamiento hasta que los resultados satisfagan sus necesidades. 

Consulte [Sugerencias de entrenamiento de relevancia](/docs/services/discovery/train-tips.html#relevancy-tips) para obtener más ayuda con relación al entrenamiento.    

## Realización de otras operaciones de consultas de datos de entrenamiento
{: #training-data-operations}

Las consultas de datos de entrenamiento se pueden administrar y mantener con otros métodos de API que se describen en la [Referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}: 

 - [Listado de datos de entrenamiento de una recopilación ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#get-training-data){: new_window}
 - [Supresión de todos los datos de entrenamiento de una recopilación ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-all-training-data){: new_window}
 - [Visualización del contenido de una consulta de datos de entrenamiento especificada ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#show-td-query){: new_window}
 - [Supresión de una consulta de datos de entrenamiento de la recopilación ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1#delete-td-query-example){: new_window}
 - [Cómo cambiar la referencia cruzada o la etiqueta de relevancia de un ejemplo de consulta de datos de entrenamiento ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#update-example){: new_window}
 - [Supresión de un documento de ejemplo de una consulta de datos de entrenamiento ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-example){: new_window}

 **Supervisión de errores:**
Los errores de los datos de entrenamiento aparecen en los avisos, que se pueden supervisar con la [
API de consulta de avisos ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-notices){: new_window}
 (`GET /v1/environments/{environment_id}/collections/{collection_id}/notices`).
