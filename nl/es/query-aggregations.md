---

copyright:
  years: 2015, 2018
lastupdated: "2018-05-09"

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

# Agregaciones de consulta
{: #query-aggregations}

Las agregaciones devuelven un conjunto de valores de datos. Si desea ver una lista completa de las agregaciones disponibles, consulte la [Referencia de consultas](/docs/services/discovery?topic=discovery-query-reference#aggregations).

## term
{: #term}

Devuelve los valores superiores (por puntuación y por frecuencia) de los enriquecimientos seleccionados. Todos los enriquecimientos son valores válidos. De forma opcional también puede utilizar `count` para especificar el número de términos a devolver. El parámetro `count` tiene un valor por defecto de 10. Este ejemplo devuelve el texto completo y los enriquecimientos de los valores superiores con el enriquecimiento concepts, y especifica devolver 10 términos.

Por ejemplo:
```bash
term(enriched_text.concepts.text,count:10)
```
{: codeblock}

## filter
{: #aggfilter}

Un modificador que reducirá el conjunto de documentos de la consulta de agregación que le precede. Este ejemplo filtra al conjunto de documentos que incluye el concepto "cloud computing".

Por ejemplo:
```bash
filter(enriched_text.concepts.text:"cloud computing")
```
{: codeblock}

## nested
{: #nested}

La aplicación de la anidación antes de una consulta de agregación restringe la agregación al área de los resultados especificados. Por ejemplo: `nested(enriched_text.entities)` significa que solo los componentes `enriched_text.entities` de cualquier resultado se utilizan para agregar.

Por ejemplo:
```bash
nested(enriched_text.entities)
```
{: codeblock}

## histogram
{: #histogram}

Crea segmentos de intervalos numéricos para clasificar documentos. Utiliza valores de un campo numérico individual para describir la categoría. El campo utilizado para crear el histograma debe ser de tipo numérico (`integer`, `float`, `double` o `date`). No se da soporte a tipos no numéricos como, por ejemplo, `string`. Por ejemplo, "price": 1.30 es un valor numérico que sirve, y "price": "1.30" es una serie, por lo que no sirve. Utilice el argumento `interval` para definir el tamaño de las secciones en las que se dividirán los datos. Los valores del intervalo deben ser números enteros no negativos, que se establecen para que la segmentación de sus valores de campo tenga sentido. Por ejemplo, si su conjunto de datos incluye el precio de varios artículos, como: “price”: 1.30, “price”: 1.99 y “price”: 2.99, podría utilizar intervalos de 1 unidad, de forma que la información la vería agrupada entre 1 y 2 y entre 2 y 3. Con toda probabilidad no utilizaría un intervalo de 100 unidades porque todos los datos acabarían en el mismo segmento. Los histogramas pueden procesar valores decimales, pero los intervalos tienen que ser números enteros. La sintaxis es `histogram(<field>,<interval>)`, tal como se muestra en el siguiente ejemplo.

Por ejemplo:
```bash
histogram(product.price,interval:1)
```
{: codeblock}

## timeslice
{: #timeslice}

Se trata de un histograma especializado que utiliza fechas para crear segmentos de intervalo. Valores válidos para el intervalo de fechas son `second/seconds` `minute/minutes`, `hour/hours`, `day/days`, `week/weeks`, `month/months` y `year/years`. La sintaxis es `timeslice(<field>,<interval>,<time_zone>)`. Para utilizar `timeslice`, los campos temporales en su documento deben ser del tipo de datos `date` con un formato de [tiempo UNIX ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://en.wikipedia.org/wiki/Unix_time){: new_window}. A no ser que se satisfagan estos requisitos, el parámetro `timeslice` no funcionará correctamente. Se puede crear este histograma temporal si sus documentos contienen campos `date` con valores como, por ejemplo, `1496228512`. El valor debe estar en un formato numérico (por ejemplo, `float` o `double`) sin que esté delimitado entre comillas. El servicio trata las fechas en texto y fecha en formato ISO 8601 como tipo de datos `string`, no como tipo de datos `date`. Puede detectar puntos anómalos en agregaciones de timeslice. Consulte [Detección de anomalías con timeslice](#anomaly-detection) para obtener más información. Este ejemplo devuelve valores para "sales" ("product.sales") en intervalos de 2 días en el huso horario de la ciudad de Nueva York.

Por ejemplo:
```bash
timeslice(product.sales,2day,America/New York)
```
{: codeblock}

### Detección de anomalías en timeslice
{: #anomaly-detection}

De forma opcional puede aplicar la detección de anomalías para los resultados de una agregación de `timeslice`. La detección de anomalías se utiliza para localizar puntos de datos inusuales dentro de una serie temporal y para señalarlos para revisarlos más tarde. Como ejemplo de detección de anomalías podríamos incluir la detección de un uso elevado anómalo de tarjetas de crédito o la búsqueda en Watson Discovery News de grupos de artículos con relación a un tema concreto.

Para aplicar la detección de anomalías, utilice la sintaxis siguiente en la agregación:

```bash
timeslice(field:<date>,interval:<interval>,anomaly:true)`
```
{: codeblock}

Si especifica `anomaly:true` con la agregación `timeslice`, la salida incluye los siguientes dos campos adicionales que se muestran en el ejemplo.

  - `"anomaly": true` para indicar que se realizó la detección de anomalías.
  - Un campo `anomaly` en los puntos que son anómalos en la matriz de resultados de la salida. El campo anomaly tiene un valor de tipo de datos `float` indicando la magnitud del comportamiento anómalo. Cuanto más cerca esté el valor del campo anomaly a `1`, más probable será que el resultado sea anómalo.

  - `key` y `key_as_string` en cada uno de los objetos en la matriz `results` corresponde a una indicación de fecha y hora UNIX en segundos.
  - La puntuación de la anomalía es relativa solo a la consulta original.

```json
"type": "timeslice",
"field": "blekko.chrondate",
"interval": "1d",
"anomaly": true,
"results": [
  {
    "matching_results": 2933,
    "anomaly": 1,
    "key_as_string": "1496880000",
    "key": 1496880000000
  },
  {
    "matching_results": 3435,
    "anomaly": 1,
    "key_as_string": "1496966400",
    "key": 1496966400000
  },
  {
    "matching_results": 3692,
    "anomaly": 0.598226,
    "key_as_string": "1496016000",
    "key": 1496016000000
  },
  {
    "matching_results": 4551,
    "anomaly": 0.828498,
    "key_as_string": "1495411200",
    "key": 1495411200000
  },
  {
    "matching_results": 947,
    "key_as_string": "1489968000",
    "key": 1489968000000
  },
 ...
]
...
```
{: codeblock}

#### Limitaciones en la detección de anomalías
{: #anomaly-limitations}

- La detección de anomalías actualmente solo está disponible en agregaciones `timeslice` de nivel superior. No está disponible en agregaciones (anidadas) de nivel inferior.
- El número máximo de puntos que se pueden procesar por la detección de anomalías en una agregación `timeslice` es de `1500`.
- El número máximo de agregaciones timeslice de nivel superior que la detección de anomalías puede procesar es de `20`.

<!--
#### Anomaly detection workflow

The following example workflow detects an anomaly for the text entity `London` and retrieves additional information about the anomalous datapoint.

  1. Timeslice aggregation: `query=entities.text:London&count=0&aggregation=timeslice(blekko.last_crawled,1day,anomaly:true)`
  1. Term aggregation to retrieve top keywords: `query=entities.text:London&count=0&aggregation=term(keywords.text,count:5)&filter=blekko.last_crawled>=1490140800,<=1490227200`
  1. Query to retrieve top enriched title: `query=entities.text:London,keywords.text:Westminster Bridge|police officer|people|Prime Minister Theresa|parliament&count=1&filter=blekko.last_crawled>=1490140800,<=1490227200&return=enrichedTitle.text`
  -->

## top_hits
{: #top_hits}

Devuelve los documentos clasificados por la puntuación de la consulta o el enriquecimiento. Se puede utilizar con cualquier parámetro o agregación. Este ejemplo devuelve los 10 aciertos superiores para una agregación de términos.

Por ejemplo:
```bash
term(enriched_text.concepts.text).top_hits(10)
```
{: codeblock}

## unique_count
{: #unique_count}

Devuelve un recuento de las instancias exclusivas del campo especificado en la recopilación.

Ejemplos:
```bash
unique_count(enriched_text.keyword.text)
```
{: codeblock}

```bash
nested(enriched_text.entities).term(enriched_text.entities.text,count:3).unique_count(enriched_text.entities.type)
```
{: codeblock}

## max
{: #max}

Devuelve el valor más alto en el campo especificado en todos los documentos coincidentes.

Por ejemplo:
```bash
max(product.price)
```
{: codeblock}

## min
{: #min}

Devuelve el valor más bajo en el campo especificado en todos los documentos coincidentes.

Por ejemplo:
```bash
min(product.price)
```
{: codeblock}

## average
{: #average}

Devuelve el valor medio de los valores en el campo especificado en todos los documentos coincidentes.

Por ejemplo:
```bash
average(product.price)
```
{: codeblock}

## sum
{: #sum}

Agrega los valores del campo especificado en todos los documentos coincidentes.

Por ejemplo:
```bash
sum(product.price)
```
{: codeblock}
