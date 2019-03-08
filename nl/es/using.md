---

copyright:
  years: 2015, 2018
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

# Conceptos de consultas
{: #query-concepts}

El servicio {{site.data.keyword.discoveryfull}} ofrece potentes funciones de búsqueda de contenido. Una vez el contenido se ha cargado y el servicio {{site.data.keyword.discoveryshort}} lo ha enriquecido, puede crear consultas, integrar {{site.data.keyword.discoveryshort}} en sus propios proyectos o crear una aplicación personalizada utilizando {{site.data.keyword.watson}} Explorer Application Builder.
{: shortdesc}

  Las consultas que escriba dependerán de la recopilación, puesto que cada recopilación posee contenido único.
  {: tip}

Cuando se crea una consulta o filtro, {{site.data.keyword.discoveryshort}} analiza cada resultado y busca coincidencias con las vías que haya definido. Cuando se producen coincidencias, se añaden al conjunto de resultados. Al crear una consulta, puede ser todo lo genérica o específica que desee. Cuando más específica sea una consulta, más acotados serán los resultados.

También tiene la opción de activar la recuperación de pasajes. Los pasajes son fragmentos significativos breves que se extraen de los documentos completos que devuelve su consulta. Estos fragmentos específicos se extraen de los campos `text` de los documentos en su recopilación. De forma predeterminada para una consulta, se devolverá un máximo de 10 pasajes de 400 caracteres. Se extrae un máximo de tres pasajes de un resultado individual. El parámetro `passages` solo está disponible en recopilaciones privadas, por lo tanto, no está disponible en la recopilación {{site.data.keyword.discoverynewsshort}}. Consulte [Pasajes](/docs/services/discovery/query-parameters.html#passages) para obtener más información sobre cómo se identifican los pasajes.

  Puede escribir consultas de lenguaje natural (como "IBM Watson partnerships") utilizando el conjunto de herramientas de {{site.data.keyword.discoveryshort}} o con la API.
  {: tip}

Las recopilaciones entrenadas devolverán una puntuación de `confidence` en el resultado de una consulta de lenguaje natural. Consulte [Puntuaciones de confianza](/docs/services/discovery/train-tooling.html#confidence) para obtener más información.

{{site.data.keyword.discoveryshort}} devuelve resultados de consulta que incluyen caracteres especiales para los idiomas siguientes: Inglés, alemán, francés, holandés, italiano y portugués. Por ejemplo, si consulta `aqui`, ahora recibirá resultados para `aqui` y <code>aqu&iacute;</code>.

Puede crear consultas más largas y complejas que incluyan varios filtros y agregaciones complejas. Esta opción está disponible solo en la API e incrementará el límite de caracteres de una consulta a 10.000 caracteres. Consulte [Consultas de recopilaciones largas![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#query){: new_window} y [Consultas de entorno largas ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#federated-query){: new_window} para obtener detalles.

{{site.data.keyword.discoveryfull}} Knowledge Graph es una característica en fase Beta que proporciona nuevos puntos finales para consultar entidades y relaciones entre documentos. Incluye búsquedas basadas en el contexto y clasificación según la relevancia. Consulte [{{site.data.keyword.discoveryfull}} Knowledge Graph](/docs/services/discovery/building-kg.html) para obtener más información.

Para obtener más información sobre cómo escribir consultas, consulte:
- [Iniciación a la guía de aprendizaje de creación de consultas](/docs/services/discovery/getting-started-query.html)
- [Referencia de consultas](/docs/services/discovery/query-reference.html) (incluye la lista de parámetros, operadores y agregaciones disponibles en {{site.data.keyword.discoveryshort}} Query Language)

## El esquema de datos de Discovery
{: #discovery-schema}

Familiarícese primero con el JSON de {{site.data.keyword.discoveryshort}}. Para entender cómo crear una consulta con {{site.data.keyword.discoveryshort}} Query Language, necesitará familiarizarse con el JSON que {{site.data.keyword.discoveryshort}} genera después de enriquecer los documentos en su recopilación. Una vez familiarizado con el esquema de datos de los documentos, será más fácil escribir consultas en {{site.data.keyword.discoveryshort}} Query Language. Hay tres maneras de hacerlo.

  1. En el conjunto de herramientas de {{site.data.keyword.discoveryshort}}, abra la pantalla **Gestionar datos**, elija la recopilación que contenga los {{site.data.keyword.IBM_notm}} Press Releases. Pulse el botón **Ver esquema de datos**. La pantalla **Ver esquema de datos** visualiza los campos y valores en sus documentos transformados de dos maneras: por documento (**Vista de documentos**) o por campo (**Vista de recopilación**). En la **Vista de documentos** se visualizará un máximo de 50 documentos. La **Vista de recopilación** visualizará los campos de toda la recopilación.

    En la **Vista de recopilación**, bajo `enriched_text`, puede examinar los enriquecimientos aplicados con el archivo de la **Configuración predeterminada**. Pulse en `categories`, `concepts`, `entities` y `sentiment` para cómo la recopilación se enriquece con la información de Watson.

  1. Ejecute una consulta "vacía" para ver el JSON. En la pantalla de **Ver esquema de datos**, pulse el botón **Crear consultas** y, a continuación, pulse **Ejecutar consulta**. Los resultados se visualizarán a la derecha, bajo dos separadores, **Resumen** (una visión general de los resultados de la consulta) y **JSON**. Empiece abriendo el separador **JSON**.

     -  Cada uno de los cuatro documentos estará precedido por un número de `id`.
     -  Desplácese hasta el campo `enriched_text`. Examine cada enriquecimiento para conocer los campos JSON que se utilizarán para realizar consultas.

        ![Campos de configuración predeterminados](images/JSON.png)

     -  **entities** - Encuentre el campo `text` y examine la información de enriquecimiento adicional.
     -  **sentiment** - Encuentre el campo `label` y examine la información de enriquecimiento adicional.
     -  **concepts** - Encuentre el campo `text` y examine la información de enriquecimiento adicional.
     -  **categories** - Encuentre el campo `document` y examine la información de enriquecimiento adicional.

     Después de haber examinado la información en el primer documento, puede consultar los otros tres documentos si así lo desea.

  1. Visualice los campos disponibles en el **Creador de consulta visual**. En la pantalla **Crear consultas**, pulse **Buscar documentos** y, a continuación, **Utilizar {{site.data.keyword.discoveryshort}} Query Language**. Pulse el desplegable **Campo** para ver los campos disponibles en sus datos. Pulse **Editar en lenguaje de consulta** para crear consultas de forma manual con {{site.data.keyword.discoveryshort}} Query Language.      

### Como estructurar una consulta básica
{: #structure-basic-query}

Como habrá observado, JSON es jerárquico, de forma que las consultas se deben escribir utilizando la misma jerarquía. Por ello, si su JSON es parecido a:

```json
"enriched_text": {
  "concepts": [
    {
    "text": "Cloud computing",
    "relevance": 0.610029}
    ]
  }
```
{: codeblock}

Su consulta se debería estructurar como:

![Ejemplo de estructura de consulta](images/query_structure2.png)

  Los operadores que evalúan un campo (`<=` , `>=`, `<`, `>`) requieren que un valor sea un `número` o `fecha`. Al utilizar comillas con un valor, este se transforma en `serie`. Por lo tanto, `score>=0.5` es una consulta válida y `score>="0.5"` no lo es. Consulte [Operadores de consulta](/docs/services/discovery/query-operators.html) para obtener una lista de operadores completa.
  {: tip}

Consideraciones:

- ¿No está seguro de cuándo realizar una consulta con relación a una entidad, concepto o palabra clave? Consulte [Diferencias entre entidades, conceptos y palabras clave](/docs/services/discovery/building.html#udbeck).

- **Nota:**  Después de pulsar **Ejecutar consulta** y abrir el separador **JSON**, observará que de forma predeterminada se activa el resaltado de la consulta. Esto añadirá un campo `highlight` a los resultados de la consulta. Dentro del campo `highlight`, las palabras que coinciden con su consulta serán delimitados en etiquetas `<em>` (emphasis) de HTML. Consulte [Parámetros de consulta](/docs/services/discovery/query-parameters.html#highlight) para obtener más información.

## Creación de consultas combinadas
{: #building-combined-queries}

Los parámetros de las consultas se pueden combinar para crear consultas más específicas. Por ejemplo, los parámetros `filter` y `query` se pueden utilizar de forma conjunta. Para obtener más información sobre el filtrado frente a la creación de consultas, consulte [Diferencias entre los parámetros query y filter](/docs/services/discovery/query-parameters.html#filtervquery).

## Cómo estructurar una agregación
{: #structure-aggregation}

Las agregaciones devuelven un conjunto de valores de datos, por ejemplo, palabras clave más destacadas, sentimiento general de las entidades, etc. Para obtener una lista completa de opciones de agregación, consulte [Agregaciones](/docs/services/discovery/query-reference.html#aggregations).

![Ejemplo de estructura de consulta de agregación](images/aggregation_structure.png)

Este ejemplo de agregación encontrará todos los `concepts` en su recopilación.
El delimitador en esta consulta es `.` y el operador es `()`. Consulte [Operadores de consulta](/docs/services/discovery/query-operators.html) para obtener más información sobre otros operadores disponibles en {{site.data.keyword.discoveryshort}} Query Language.

### Ejemplo de consultas de agregación
{: #example-aggregations}

Existen varias formas de agregar resultados con {{site.data.keyword.discoverynewsshort}} como, por ejemplo, con top values, sum, min, max, average, timeslice e histogram. También es posible añadir filtros y agregaciones anidadas.

#### Filtración de agregaciones
{: #filter-aggregations}

Este ejemplo de agregación devuelve el número de artículos encontrados en {{site.data.keyword.discoverynewsshort}} acerca del equipo Pittsburgh Steelers y cuántos resultados tienen un sentimiento `positive`, `negative` o `neutral`.

- `filter(enriched_text.entities.text:"Pittsburgh Steelers").term(enriched_text.sentiment.document.label,count:3)`


Este ejemplo de agregación primero delimitará (filtrará) un conjunto de artículos en {{site.data.keyword.discoverynewsshort}} a solo aquellos que incluyan el texto de entidades de twitter y, a continuación, dividirá estos artículos por tipos de sentimiento del documento. Solo se devolverán los primeros 3 documentos con tipos de sentimiento (`positive`, `negative`, `neutral`).

- `filter(enriched_text.entities.text:twitter).term(enriched_text.sentiment.document.label,count:3)`

#### Agregaciones anidadas
{: #nested-aggregations}

La adición de `nested` antes de una agregación restringe la agregación al área de los resultados especificados. Por ejemplo: `nested(enriched_text.entities)` significa que solo los componentes `enriched_text.entities` de cualquier resultado se utilizan para agregar.

Esto se muestra con facilidad consultando las diferencias entre las siguientes dos consultas:
- `filter(enriched_text.entities.disambiguation.subtype::City)` -
La agregación cuenta el número de *Resultados* que contienen una o varias `entity` con el tipo `City`
- `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City)` - La agregación cuenta el número de instancias de una `entity` con el tipo `City` en los resultados.  

Además, cualquier operación posterior restringirá aún más el conjunto de resultados por el que se puede agregar. Por ejemplo:

- `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City)` significa que solo se agregarán las entidades de `subtype::City`.
- `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City).term(enriched_text.entities.text,count:3)` agregará las 3 primeras entidades del subtipo `City`
- `filter(enriched_text.entities.disambiguation.subtype::City).term(enriched_text.entities.text,count:3)` devolverá las 3 primeras entidades donde el resultado contiene al menos una entidad del subtipo `City`.

## Consultas para Watson Discovery News
{: #querying-news}

{{site.data.keyword.discoverynewsshort}}, un conjunto de datos públicos que previamente se ha enriquecido con conocimientos cognitivos, también se incluye con {{site.data.keyword.discoveryshort}}. Consulte [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html#watson-discovery-news) para obtener más información sobre esta recopilación.

Esta recopilación se puede consultar utilizando consultas de lenguaje natural, por ejemplo "IBM Watson partnerships", o {{site.data.keyword.discoveryshort}} Query Language. Para obtener más información sobre las consultas en lenguaje natural, consulte [Consulta de lenguaje natural](/docs/services/discovery/query-parameters.html#nlq).

No es posible ajustar la configuración de {{site.data.keyword.discoverynewsshort}}, ni realizar tareas de entrenamiento ni tampoco añadir documentos la recopilación de {{site.data.keyword.discoverynewsshort}}. Consulte una demostración que puede realizar con {{site.data.keyword.discoverynewsshort}} [aquí ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://discovery-news-demo.ng.bluemix.net/){: new_window}.

Las recopilaciones de {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} en inglés, coreano, alemán, español y japonés están disponibles desde la API y el conjunto de herramientas de {{site.data.keyword.discoveryshort}}.

El idioma predeterminado de {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} en el conjunto de herramientas es el inglés. Para cambiar el idioma, primero debe pulsar en el icono ![Gestionar datos](/images/icon_yourData.png) y, a continuación, seleccionar el idioma adecuado en el desplegable.

Para obtener información sobre cómo consultar una recopilación a través de la API, consulte [Referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection){: new_window}. El `collection_id` de la versión en el idioma inglés de Watson {{site.data.keyword.discoverynewsshort}} es `news-en`. Con anterioridad, el `collection_id` era `news`. Si ha esta utilizando el anterior `collection_id`, continuará funcionando, sin embargo, debería cambiar al nuevo `collection_id` para nuevos proyectos. El `collection_id` de la recopilación en coreano es `news-ko`, el `collection_id` en español es `news-es`, el `collection_id` en alemán es `news-de` el `collection_id` en japonés es `news-ja`.

Las consultas de {{site.data.keyword.discoverynewsfull}} muestran las 50 primeras palabras de cada artículo en el campo JSON `text`.

El número máximo de resultados devueltos para una consulta de {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} es `50`. Utilice consultas adicionales y el parámetro `offset` para obtener más de `50` resultados.

Si está utilizando {{site.data.keyword.discoveryshort}} Query Language, puede incluir un rango de fechas relativo en sus consultas para {{site.data.keyword.discoverynewsshort}}, por ejemplo: `crawl_date>=now-1month`. Valores válidos para el intervalo de fechas son `second/seconds` `minute/minutes`, `hour/hours`, `day/days`, `week/weeks`, `month/months` y `year/years`. `now`
no se ve afectado por el parámetro `time_zone`, `UTC` es el huso horario predeterminado.

En este ejemplo se consultará una palabra clave en un rango de fechas específico. La información de huso horario no es necesaria:
- `enriched_text.keywords.text:"olympics", publication_date<=2018-02-15T00:00:00Z, publication_date>=2018-02-01T00:00:00Z`

Los artículos de noticias a veces se sindican a varios proveedores de noticias, por lo que {{site.data.keyword.discoverynewsfull}} recopilará todas ellas, dando lugar a artículos duplicados. Esto significa que una consulta a {{site.data.keyword.discoverynewsfull}} potencialmente podría dar lugar a varios artículos idénticos o casi idénticos en los resultados de las consultas. Esta situación se puede tratar con la desduplicación. Para obtener más información sobre esta funcionalidad en fase beta, consulte [Exclusión de documentos duplicados en los resultados de las consultas](/docs/services/discovery/query-parameters.html#deduplication).

## Consultas a varias recopilaciones
{: #multiple-collections}

Si tiene varias recopilaciones en su entorno, es posible que desee ver los resultados a través de varias de estas recopilaciones. Los métodos de consulta (`query`, `fields` y `notices`) al nivel de `environments` permiten consultar varias recopilaciones especificadas. Actualmente la consulta a través de varias recopilaciones no está disponible en el conjunto de herramientas de {{site.data.keyword.discoveryshort}}.

Puede consultar varias recopilaciones en el mismo entorno mediante el método de API `environments/{environment_id}/query`. Al realizar consultas a través de varias recopilaciones, tenga en cuenta los siguientes aspectos.
-  Al utilizar este método se debe especificar el parámetro `collection_ids`. El parámetro `collection_ids` es una lista separada por comas de recopilaciones en el entorno en el que realizar la consulta.
-  No se da soporte a `passages` al realizar consultas de varias recopilaciones.
-  Como parte del objeto de resultado, se devuelve el campo `collection_id`. Este campo especifica la recopilación donde se ha encontrado el resultado.
-  {{site.data.keyword.discoverynewsshort}} es parte del entorno `system` y no se puede incluir en consultas a varias recopilaciones.
-  El entrenamiento de relevancia de la recopilación individual no afecta a la clasificación de resultados al realizar consultas de varias recopilaciones. Para volver a reclasificar los resultados devueltos al consultar varias recopilaciones, implemente [Entrenamiento de relevancia continuo](/docs/services/discovery/continuous-training.html).
-  No se realiza una reclasificación en ninguna parte de una consulta de varias recopilaciones, incluso si se han entrenado todas las recopilaciones en la consulta.

Consulte [Referencia de API para consultas de varias recopilaciones ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-multi-collections){: new_window} para obtener más información.

Puede consultar varias noticias a través de varias recopilaciones en el mismo entorno mediante el método de API `environments/{environment_id}/notices`.
-  Al utilizar este método se debe especificar el parámetro `collection_ids`. El parámetro `collection_ids` es una lista separada por comas de recopilaciones en el entorno en el que realizar la consulta.
-  No se da soporte a `passages` al realizar consultas de varias recopilaciones.

Consulte [Referencia de API para noticias de varias recopilaciones ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#collections-notices){: new_window} para obtener más información.

Puede visualizar campos disponibles a través de recopilaciones en el mismo entorno mediante el método de API `environments/{environment_id}/fields`. Consulte [Referencia de API para consultas de campos de varias recopilaciones ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#multi-list-fields){: new_window} para obtener más información.

## Expansión de la consulta
{: #query-expansion}

Puede ampliar el ámbito de una consulta más allá de las coincidencias exactas, por ejemplo, puede expandir la consulta de "coche" para incluir "automóvil" y "vehículo de motor", cargando una lista de términos de expansión de consulta mediante la API de {{site.data.keyword.discoveryshort}}. Los términos de expansión de consulta normalmente son sinónimos, antónimos o errores ortográficos típicos de términos comunes.

Puede definir dos tipos de expansiones:
- **bidirectional**: cada `expanded_term` se expandirá para incluir todos los términos expandidos. Por ejemplo, una consulta de `coche` puede expandirse a `coche O automóvil O (motor Y vehículo`).
- **unidirectional**: el valor `input_terms` de la consulta se sustituirá por `expanded_terms`. Por ejemplo, la consulta `ibm` puede expandirse a `International Business Machines` y `Big Blue`. El valor `input_terms` no se utiliza como parte de la consulta resultante. En el ejemplo de `ibm` anterior, la consulta `IBM` se convierte a `international business machines` o `big blue` y no contiene el término original.

Este archivo puede utilizarse como punto de partida al crear una lista de expansión de la consulta:
<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/expansions.json" download>expansions.json <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo" title="Icono de enlace externo" class="style-scope doc-content"></a>. Puede modificar el archivo para crear una lista de expansión de la consulta personalizada.

Ejemplo bidirectional:
```JSON
 {
   "expansions": [
     {
       "expanded_terms": [
         "car",
         "automobile",
         "motor vehicle"
       ]
     }
   ]
 }
```
{: codeblock}

Ejemplo unidirectional:
```JSON
 {
   "expansions": [
     {
      "input_terms": [
        "ibm"
       ],
      "expanded_terms": [
        "ibm",
        "international business machines",
        "big blue"
       ]
     }
   ]
 }
```
{: codeblock}

Notas sobre la expansión de la consulta:

- La expansión de la consulta solo está disponible para recopilaciones privadas. El número de matrices `expansions` disponibles (matrices bidireccionales y unidireccionales totales) y los términos (`input_terms` y `expanded_terms` totales) varía según el plan. Consulte [Planes de precios de Discovery](/docs/services/discovery/pricing-details.html) para obtener detalles. **Nota:** Cada uno de los términos de consulta (`input_terms` y `expanded_terms`) cuentan como uno. Este ejemplo contiene dos objetos en la matriz `expansions` y ocho series de términos.

```JSON
 {
   "expansions": [
     {
      "input_terms": [
         "ibm"
       ],
      "expanded_terms": [
         "ibm",
         "international business machines",
         "big blue"
       ]
     },
     {
      "input_terms": [
         "banana"
       ],
      "expanded_terms": [
         "banana",
         "plantain",
         "fruit"
       ]
     }
   ]
 }
```
{: codeblock}

- Solo se puede cargar una lista de expansión de consulta por colección; si se carga una segunda lista de expansión, esta sustituirá a la primera.
- Todos los valores `input_terms` y `expanded_terms` deben estar en minúsculas. Los términos en minúsculas se expandirán a mayúsculas.
- La lista de expansión de la consulta se debe escribir en JSON.
- Para inhabilitar la expansión de la consulta, suprima la lista de expansión de la consulta.
- Actualmente, no puede cargar o suprimir una lista de expansión de la consulta mediante el conjunto de herramientas de {{site.data.keyword.discoveryshort}}; se debe realizar utilizando la API de {{site.data.keyword.discoveryshort}}.
- La expansión de la consulta se realiza en lo métodos `consulta` y `consulta de varias recopilaciones`. La expansión de la consulta no se realiza en las consultas de Knowledge Graph.
- Cada conjunto de expansiones está asociado a una recopilación. Al realizar consultas en [ varias recopilaciones](/docs/services/discovery/using.html#multiple-collections), cada colección se expande de manera individual.
- Las expansiones de la consulta se aplican cuando se realiza la consulta, no durante la indexación, por lo que la lista de expansión de consultas puede actualizarse sin la necesidad de volver a ingerir los documentos.
- No cargue o suprima una lista de expansión de la consulta al mismo tiempo que los documentos se ingieren en la recopilación. Esto puede provocar que el índice no esté disponible durante ese breve período.

Consulte la [referencia de API de la expansión de consultas![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-expansion){: new_window} para ver cómo los mandatos de API pueden cargar y suprimir los archivos de expansión de query.

## Diccionarios de señalización personalizados

La señalización divide el texto en unidades denominadas señales. Un diccionario de señalización estándar se aplica a su recopilación, pero puede mejorar la precisión de la búsqueda para el dominio y el idioma cargando un diccionario de señalización personalizado. El diccionario personalizado sustituirá al estándar. Puede cargar el diccionario mediante la API de {{site.data.keyword.discoveryshort}}. 

Consulte la [referencia de API de la señalización![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#create-tokenization-dictionary){: new_window} para ver los mandatos de API cargar y suprimir los archivos de señalización. 

**Nota:** Esta característica solo está disponible para las recopilaciones en japonés. 

En el ejemplo siguiente, **text** es la frase que se señalizará cuando se encuentre y **tokens** son las palabras en las que **text** se dividirá. **Readings** muestra la versión de las señales representadas por un conjunto de caracteres distintos y **part_of_speech** es la categoría léxica que representan las señales.

Con este diccionario personalizado, si busca el texto `ネコ`, los resultados de búsqueda incluirán texto que contenga `すしネコ` además de texto que solo contenga `ネコ`.

```
{ "tokenization_rules":
  [
    {
      "text":"すしネコ",
      "tokens":[
        "すし",
        "ネコ"
      ],
      "readings":[
        "寿司",
        "ネコ"
      ],
      "part_of_speech":"カスタム名詞"
    },
    ...
  ]
}
```

También puede crear reglas con una sola señal. En este ejemplo, `ibm発見` se señalizará como una sola señal, por lo que no se dividirá en unidades más pequeñas.

```
{ "tokenization_rules":
  [
    {
      "text":"ibm発見",
      "tokens":[  
      "ibm発見"
      ],
      "readings":[  
      "ibm発見"
      ],
      "part_of_speech":"カスタム名 詞"
    },
    ...
  ]
}
```

- La señalización se produce tanto en el índice como en el momento de la consulta. 
- En todas las colecciones se utiliza un diccionario de señalización estándar. Si la colección ya se ha indexado con el diccionario, deberá volver a ingerir los documentos de la colección después de cargar un diccionario de señalización personalizado.
- Solo es posible cargar un diccionario de señalización por recopilación; si se carga un segundo diccionario, este sustituirá al primero. Si dicha colección ya contenía documentos, deberá volver a ingerirlos para que se aplique el nuevo diccionario de señalización personalizado.
- El diccionario de señalización personalizado debe escribirse en JSON; ejemplo de un nombre de archivo: `custom_tokenization_dictionary.json`.
- Para inhabilitar la señalización, suprima el diccionario de señalización y vuelva a ingerir los documentos.
- Actualmente, no puede cargar o suprimir un diccionario de señalización mediante la herramienta de consultas de {{site.data.keyword.discoveryshort}}; se debe realizar mediante la API de {{site.data.keyword.discoveryshort}}.
- La señalización se realiza en los métodos `consulta` y `consulta de varias recopilaciones`. La señalización no se realiza en las consultas de Knowledge Graph.
- Cada diccionario de señalización está asociado con una recopilación. Al realizar consultas en [varias recopilaciones](/docs/services/discovery/using.html#multiple-collections), cada una de ellas se señaliza de manera individual.
- No cargue o suprima un diccionario de señalización al mismo tiempo que los documentos se ingieren en la recopilación. 

## Similitud de documentos
{: #doc-similarity}

Una consulta de similitud de documentos buscará otros documentos similares al documento que se está visualizando; por ejemplo, un operador de un centro de atención telefónica puede estar viendo manuales de un producto y utilizar la similitud de documentos para buscar otros documentos con características similares. Puede consultar documentos similares según el `similar.document_ids` y, opcionalmente, detallar la similitud especificando campos `similar.fields` adicionales.

La similitud de documentos se determina extrayendo los 25 términos más relevantes del documento original y buscando documentos con términos relevantes similares.

Ejemplo de consulta según `similar.document_ids` (no debería haber ningún espacio después de la coma si se están especificando varios valores `similar.document_ids`):

`curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&similar.document_ids=4107b6f1-5d3f-4bea-bbcf-fb05bbf960b1,6057k6d1-7d7k-6aeh-cfbb-kj98ssf786c2"`

Se ha añadido un ejemplo de consulta con el campo `similar.fields`:

`curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&similar.document_ids=4107b6f1-5d3f-4bea-bbcf-fb05bbf960b1&similar.fields=title&return=title&count=100"`

Consulte la [referencia de API sobre la similitud de documentos![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#query-using-get){: new_window} y los [parámetros de consulta](/docs/services/discovery/query-parameters.html#similar) para obtener más información.
