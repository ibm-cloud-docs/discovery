---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-04"

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

# Parámetros de consulta
{: #query-parameters}

El servicio {{site.data.keyword.discoveryfull}} ofrece potentes funciones de búsqueda de contenido a través de las consultas. Después de que el contenido se haya cargado y el servicio {{site.data.keyword.discoveryshort}} lo haya enriquecido, puede crear consultas, integrar {{site.data.keyword.discoveryshort}} en sus propios proyectos o crear una aplicación personalizada utilizando {{site.data.keyword.watson}} Explorer Application Builder. Consulte [Conceptos de consultas](/docs/services/discovery?topic=discovery-query-concepts#query-concepts) para empezar a trabajar con las consultas. Si desea ver una lista completa de los parámetros, consulte la [Referencia de consultas](/docs/services/discovery?topic=discovery-query-reference#parameter-descriptions).
{: shortdesc}

**Parámetros de búsqueda**

Los parámetros de búsqueda permiten buscar en la recopilación, identificar un conjunto de resultados, y realizar análisis sobre dicho conjunto de resultados.

El **conjunto de resultados** es el grupo de documentos identificados por las búsquedas combinadas de los parámetros de búsqueda. El conjunto de resultados puede ser significativamente mayor que los resultados devueltos. Si se realiza una consulta vacía, el conjunto de resultados es igual a todos los documentos de la recopilación.

## query
{: #query}

Una búsqueda de query devuelve todos los documentos en su conjunto de datos con todos los enriquecimientos y todo el texto ordenados según su relevancia. Una consulta también excluye todos los documentos que no mencionan el contenido de la consulta. Estas consultas se escriben con el [{{site.data.keyword.discoveryshort}} Query Language](/docs/services/discovery?topic=discovery-query-operators#query-operators).

## filter
{: #filter}

Una consulta que se coloca en caché y que excluye los documentos que no mencionan el contenido de la consulta. Los resultados de la búsqueda de filtro **no** se devuelven ordenados según su relevancia. Estas consultas se escriben con el [{{site.data.keyword.discoveryshort}} Query Language](/docs/services/discovery?topic=discovery-query-operators#query-operators).

### Diferencias entre parámetros query y filter
{: #filtervquery}

Si prueba el mismo término de búsqueda en un pequeño conjunto de datos, puede encontrar que los parámetros `filter` y `query` devuelven resultados muy similares (si no idénticos). Sin embargo, hay una diferencia entre los dos parámetros.

- Utilizando únicamente un parámetro filter obtendrá los resultados de búsqueda sin orden específico.
- Utilizando únicamente un parámetro query obtendrá los resultados de búsqueda ordenados por su relevancia.

En grandes conjuntos de datos, si necesita resultados devueltos por orden de relevancia, debe combinar los parámetros `filter` y `query`, porque si los utiliza de forma conjunta mejorará el rendimiento. Esto se debe a que el parámetro `filter` se ejecutará y colocará los resultados en una caché primero y, a continuación, el parámetro `query` los clasificará. Para un ejemplo de la utilización de filtros y conjuntos de forma conjunta, consulte [Creación de consultas combinadas](/docs/services/discovery?topic=discovery-query-concepts#building-combined-queries). Los filtros también se pueden utilizar en agregaciones.

Cuando escriba una consulta que incluya `filter` y un parámetro `aggregation`, `query` o `natural_language_query`; en primer lugar se ejecutan los parámetros `filter` y después cualquier otro parámetro `aggregation`, `query` o `natural_language_query` se ejecuta en paralelo.

Con una consulta simple, especialmente con un pequeño conjunto de datos, `filter` y `query` a menudo devuelven los mismos resultados (o muy similares). Si una llamada `filter` y otra `query` devuelven resultados similares, y la obtención de una respuesta ordenada por relevancia no tiene importancia, es mejor usar filter porque las llamadas son más rápidas y se colocan en una caché. La colocación en la caché significa que la próxima vez que realice dicha llamada, obtendrá una respuesta mucho más rápida, especialmente con un conjunto de datos grande.

## aggregation
{: #aggregation}

Las consultas de agregación devuelven un recuento de documentos que coincide con un conjunto de valores de datos, por ejemplo, palabras clave más destacadas, sentimiento general de las entidades, etc. Para obtener una lista completa de opciones de agregación, consulte la [Tabla de agregaciones](/docs/services/discovery?topic=discovery-query-aggregations#query-aggregations). Estas agregaciones se escriben con el [{{site.data.keyword.discoveryshort}} Query Language](/docs/services/discovery?topic=discovery-query-operators#query-operators).

## natural_language_query
{: #nlq}

Una consulta de lenguaje natural permite realizar consultas expresadas en lenguaje natural, tal como lo hace un usuario final en una conversación o en una interfaz de texto sin formato como, por ejemplo "IBM Watson healthcare". El parámetro utiliza la entrada completa como texto de la consulta. **No** reconoce operadores. El parámetro `natural_language_query` habilita funcionalidades como la búsqueda de pasajes y entrenamiento de relevancia. Todas las recopilaciones privadas devolverán una puntuación de `confidence` en los resultados de consulta en la mayoría de los casos. Consulte [Puntuaciones de confianza](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence) para obtener más información. La longitud máxima de la serie de consulta para una consulta de lenguaje natural es `2048`.

**Parámetros de estructura**

Los parámetros de estructura definen el contenido y la organización de los documentos en el JSON que se devuelve. Esto incluye el número de resultados devueltos, dónde en el conjunto de resultados se empezarán a devolver documentos, cómo se ordenará el conjunto de resultados, qué campos se devolverán para cada uno de los documentos, si se deben eliminar documentos duplicados y si del conjunto de resultados se deben extraer pasajes significativos. La estructura de parámetros no afecta a los documentos que deben formar parte de todo el conjunto de resultados completo.

## count
{: #count}

El número de documentos que desea se devuelvan en la respuesta. El valor predeterminado es
`10`. El valor máximo para los valores `count` y `offset` de forma conjunta en una consulta cualquiera es `10000`.

## offset
{: #offset}

El número de resultados de la consulta para omitir al principio. Por ejemplo, si el número total de resultados que se devuelve es 10, y offset es 8, se devuelven los dos últimos resultados. El valor predeterminado es `0`. El valor máximo para los valores `count` y `offset` de forma conjunta en una consulta cualquiera es `10000`.

## return
{: #return}

Una lista separada por comas de la parte de la jerarquía del documento para devolver. Cualquier valor de la jerarquía del documento es válido.

## sort
{: #sort}

Una lista separada por comas de los campos en el documento para clasificarlos. De forma opcional se puede especificar una dirección de clasificación especificando el prefijo `-` en el campo para indicar una clasificación descendente o `+` para una clasificación ascendente. La dirección predeterminada de clasificación es la ascendente.

El parámetro `sort` actualmente únicamente está disponible para ser utilizado con la API, no está disponible en el conjunto de herramientas.

## bias
{: #bias}

Ajusta los resultados de búsqueda para que se inclinen hacia determinados resultados; por ejemplo, documentos que se han publicado más recientemente. Es necesario establecer `bias` en un campo de tipo `date` o un campo de tipo `number`, por ejemplo, `bias=publication_date` o `bias=field_1`.  Cuando se especifica un campo de tipo `date`, los resultados devueltos se inclinarán hacia los valores de campo más cercanos a la fecha actual. Cuando se especifica un campo de tipo `number`, los resultados devueltos se inclinarán hacia los valores de campo superiores. Este parámetro no se puede utilizar en la misma consulta que el parámetro `sort`.

El parámetro `bias` actualmente únicamente está disponible para ser utilizado con la API, no está disponible en el conjunto de herramientas.

## passages
{: #passages}

Un valor booleano que especifica si el servicio devolverá un conjunto con los pasajes más significativos de los documentos devueltos por una consulta que utiliza el parámetro `natural_language_query`. Los pasajes los generan algoritmos sofisticados de Watson que determinan los mejores pasajes del texto entre todos los documentos devueltos por la consulta. El valor predeterminado es `false`.

El parámetro `passages` sólo se puede utilizar en recopilaciones privadas. No se puede utilizar en la recopilación {{site.data.keyword.discoverynewsfull}}.
{: tip}

{{site.data.keyword.discoveryshort}} intenta devolver pasajes que empiezan al principio de una frase y que acaban al final utilizando una detección de límites de frases. Para ello, primero busca pasajes con una longitud aproximada a la especificada por el parámetro [`passages.characters`](/docs/services/discovery?topic=discovery-query-parameters#passages_characters) (el valor predeterminado es `400`). A continuación amplía cada pasaje hasta el límite del doble de la longitud especificada para poder devolver frases completas. Si el parámetro `passages.characters` corresponde a una longitud corta y/o sus frases en los documentos son muy largas es posible que no haya frases con los límites suficientemente cercanos para devolver una frase completa sin exceder dos veces la longitud solicitada. En este caso, {{site.data.keyword.discoveryshort}} permanece dentro del límite del doble del parámetro `passages.characters`, por lo que el pasaje devuelto no incluirá toda la frase y omitirá el principio, el final o ambos.

Puesto que los ajustes de los límites de las frases pueden ampliar el tamaño de los pasajes, verá un incremento sustancial en la longitud media de los pasajes. Si su aplicación tienen un espacio limitado de visualización en la pantalla, es posible que desee establecer un valor más pequeño para `passages.characters` y/o trunque los pasajes que {{site.data.keyword.discoveryshort}} devuelva. La detección de los límites de las frases funcionan bien en todos los lenguajes soportados y utiliza lógica específica de cada idioma.

El parámetro `passages` devuelve pasajes coincidentes (`passage_text`), así como el `score`, `document_id`, el nombre del campo del que se extrajo el pasaje (`field`) y los caracteres de inicio y fin del texto del pasaje dentro del campo (`start_offset` y `end_offset`), tal como se muestra en el siguiente ejemplo. La consulta se muestra en la parte superior del ejemplo.

```bash
 curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-06-25&natural_language_query='Hybrid%20cloud%20companies'&passages=true"
```
{: pre}

El JSON devuelto tendrá el siguiente formato:

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
       "passage_text":"Disaster Recovery Services for Hybrid Cloud</title></head>\n<body>\n\n\n<p>Published: Thu, 27 Oct 2016 07:01:21 GMT</p>\n"
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

Una lista separada por comas de campos en el índice a partir del que se crearán los pasajes. Si este parámetro no se especifica, se incluirán todos los campos de nivel superior.

### passages.count
{: #passages_count}

El número máximo de pasajes que se devolverán. La búsqueda devolverá menos pasajes si el número encontrado es inferior al máximo. El valor predeterminado es
`10`. El máximo es `100`.

### passages.characters
{: #passages_characters}

El número aproximado de caracteres que deberían tener los pasajes. El valor predeterminado es `400`. El mínimo es `50`. El máximo es `2000`. Los pasajes devueltos pueden tener una longitud hasta el doble de la solicitada (si es necesario).

## highlight
{: #highlight}

Un booleano que especifica si la salida devuelta incluye un objeto `highlight` en el que las claves son los nombres de campo y los valores son matrices que contienen segmentos de texto encontrado por la consulta que se resalta con la etiqueta HTML `*`.

En la salida se muestra el objeto `highlight` después del objeto `enriched_text`, tal como se muestra en el siguiente ejemplo.

```bash
curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-06-25&natural_language_query=Hybrid%20cloud%20companies&highlight=true"
```
{: pre}

El JSON devuelto tendrá el siguiente formato:

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

 Una funcionalidad en fase beta que excluye los documentos duplicados de los resultados de la consulta de recopilación de {{site.data.keyword.discoverynewsfull}} y que se basa en el campo `title`. Consulte [Exclusión de documentos duplicados en los resultados de las consultas](/docs/services/discovery?topic=discovery-query-parameters#deduplication).

### deduplicate.field
{: #deduplicate_field}

Una funcionalidad en fase beta que excluye documentos duplicados de los resultados de la consulta con base al `{field}` especificado. Consulte [Exclusión de documentos duplicados en los resultados de las consultas](/docs/services/discovery?topic=discovery-query-parameters#deduplication).

### Exclusión de documentos duplicados de los resultados de una consulta
{: #deduplication}

Si está realizando consultas en la recopilación {{site.data.keyword.discoverynewsfull}}, o si su recopilación de datos posee muchos documentos idénticos (o casi idénticos), puede excluir la mayoría de los resultados de la consulta utilizando la desduplicación.

**Nota:** Actualmente sólo se da soporte a la desduplicación de documentos como una funcionalidad beta. Consulte [Características en fase beta](/docs/services/discovery?topic=discovery-release-notes#beta-features) en las notas del release para obtener más información. Actualmente, esta característica beta solo está soportada en inglés, consulte [Soporte de idiomas](/docs/services/discovery?topic=discovery-language-support#feature-support) para obtener detalles.

**Nota:** Cada consulta se desduplica de forma independiente, no se da soporte a la desduplicación a través de varios offsets.

La desduplicación se realiza después de que se hayan extraído los `passages` y se hayan calculado las agregaciones, por lo que si incluye el parámetro `passages` en su consulta, se devolverán pasajes de todos los documentos en los resultados de la consulta, antes de la desduplicación. Si ejecuta una agregación y una consulta de forma conjunta, los resultados de agregación incluirán datos de todos los documentos devueltos, antes de la desduplicación.

La desduplicación solo se realiza en los campos devueltos. Si decide especificar `return=` en la consulta, incluya el campo de desduplicación.

Utilice la sintaxis siguiente en la consulta para aplicar la desduplicación.  Sustituya `{field}` con el nombre del campo por el que desea realizar la desduplicación. El `{field}` debe ser una serie como, por ejemplo, `title`.

```
&deduplicate.field={field}
```
{: codeblock}

Al realizar la desduplicación, la respuesta JSON incluye `"duplicates_removed": x`, donde `x` es el número de documentos eliminados de los resultados.

#### Desduplicación de documentos en Watson Discovery News
{: #deduplicatewds}

Los artículos de noticias a veces se sindican a varios proveedores de noticias, por lo que {{site.data.keyword.discoverynewsfull}} recopilará todas ellas, dando lugar a artículos duplicados. Esto significa que una consulta a {{site.data.keyword.discoverynewsfull}} potencialmente podría dar lugar a varios artículos idénticos o casi idénticos en los resultados de las consultas. Mediante la desduplicación eliminará la mayoría de los artículos de las consultas de búsqueda.

{{site.data.keyword.discoveryshort}} desduplica utilizando una coincidencia aproximada por el campo `title` por lo que no es necesario especificar este campo.

Para aplicar la desduplicación, utilice el siguiente parámetro en la consulta. Esta consulta desduplica automáticamente de acuerdo con el campo `title` en {{site.data.keyword.discoverynewsfull}}.

```bash
&deduplicate=true
```
{: codeblock}

Si prefiere desduplicar por un campo distinto a `title`, utilice la siguiente sintaxis en su consulta. Sustituya `{field}` con el nombre del campo por el que desea realizar la desduplicación. El `{field}` debe ser una serie como.

```bash
&deduplicate.field={field}
```
{: codeblock}

## collection_ids
{: #collection_ids}

Lista separada por comas de recopilaciones en el mismo entorno que serán consultadas. Este parámetro solo es válido cuando se utiliza `environments/{environment_id}/query?` . Consulte [Consulta a varias recopilaciones](/docs/services/discovery?topic=discovery-query-concepts#multiple-collections) para obtener más información.

```bash
&collection_ids={id1},{id2}
```
{: codeblock}

## similar
{: #similar}

La similaridad del documento identifica los documentos similares a aquellos listados en los parámetros `similar.document_ids`. Esto se puede detallar todavía más especificando los campos que se tendrán en cuenta en la comparación utilizando los parámetros `similar.fields`. El valor predeterminado es `false`. Consulte [Similitud de documento](/docs/services/discovery?topic=discovery-query-concepts#doc-similarity) para obtener más información.

```bash
&similar=true
```
{: codeblock}

### similar.document_ids
{: #similar_document_ids}

Una lista separada por comas de los ID de documento que se utilizarán como base para buscar documentos similares como resultados. Este parámetro es necesario si el parámetro `similar` se establece en `true`.

```bash
&similar.document_ids={id1},{id2}
```
{: codeblock}

### similar.fields
{: #similar_fields}

Una lista separada por comas opcional de los campos que se utilizarán para comparar documentos y encontrar otros similares. Este parámetro solo se puede utilizar junto con el parámetro `similar.document_ids`.

```bash
&similar.fields={field1},{field2}
```
{: codeblock}
