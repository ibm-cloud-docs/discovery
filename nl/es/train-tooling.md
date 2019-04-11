---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-11"

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

# Mejora de la relevancia de los resultados con el conjunto de herramientas
{: #improving-result-relevance-with-the-tooling}

Las consultas de lenguaje natural se pueden mejorar en el servicio {{site.data.keyword.discoveryfull}} con el entrenamiento. Puede entrenar sus recopilaciones privadas con el conjunto de herramientas de {{site.data.keyword.discoveryshort}} o con las API de {{site.data.keyword.discoveryshort}}. Consulte [Mejora de la relevancia de los resultados de las consultas con la API](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api) si prefiere utilizar las API.
{: shortdesc}

El entrenamiento de relevancia es opcional; si los resultados de sus consultas satisfacen sus necesidades, no es necesario un entrenamiento adicional. Para obtener una visión general de situaciones adecuadas para el entrenamiento, consulte el artículo de blog [Cómo sacar el mayor partido al entrenamiento de relevancia ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/dwblog/2017/get-relevancy-training/){: new_window}.

Para entrenar Watson, necesitará:

  -   Proporcionar consultas de ejemplo que sean representativas de las consultas de los usuarios y
  -   Proporcionar valoraciones para indicar la relevancia de los resultados de cada consulta

Una vez Watson tenga suficientes datos de entrenamiento, la información que haya proporcionado sobre qué resultados son buenos y qué resultados son malos para cada consulta se utilizará para aprender sobre su recopilación. Watson no tan solo memoriza, aprende sobre la información específica de consultas individuales y aplica los patrones que detecta a todas las nuevas consultas. Este mecanismo se basa en las técnicas de Watson de aprendizaje máquina que encuentran señales en sus preguntas y el contenido. Una vez aplicado el entrenamiento, {{site.data.keyword.discoveryshort}} reordena los resultados de las consultas para visualizar en primer lugar los resultados más relevantes. A medida que se añaden más datos de entrenamiento, {{site.data.keyword.discoveryshort}} debería ser más preciso a la hora de ordenar los resultados de las consultas.

**Nota:** El entrenamiento de relevancia solo se aplica a las consultas de lenguaje natural en recopilaciones privadas. No está pensado para ser utilizado con consultas estructuradas de {{site.data.keyword.discoveryshort}} Query Language. Para obtener más información sobre {{site.data.keyword.discoveryshort}} Query Language, consulte [Conceptos de consultas](/docs/services/discovery?topic=discovery-query-concepts#query-concepts).

Todas las recopilaciones privadas devolverán una puntuación de `confidence` en los resultados de consulta en la mayoría de los casos. Consulte [Puntuaciones de confianza](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence) para obtener más información.

La adición de una lista de palabras vacías personalizadas puede mejorar la relevancia de los resultados para las consultas de lenguaje natural. Consulte [Definición de palabras vacías](/docs/services/discovery?topic=discovery-query-concepts#stopwords) para obtener más información.

Consulte [Requisitos de datos de entrenamiento](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#reqs) para ver los requisitos mínimos del entrenamiento, además de los límites de entrenamiento.

Consulte [Supervisión de uso](/docs/services/discovery?topic=discovery-usage#usage) para obtener detalles sobre el seguimiento del uso y la utilización de los datos para ayudarle a comprender y mejorar sus aplicaciones.

## Adición de consultas y valoración de la relevancia de los resultados
{: #results}

El entrenamiento consta de tres partes: una consulta de lenguaje natural, los resultados de la consulta y la valoración que asignará a dichos resultados.

1.  Hay dos maneras de acceder a la página de entrenamiento en el conjunto de herramientas de {{site.data.keyword.discoveryshort}}:
    - Para realizar una recopilación individual, en la pantalla **Crear consultas**, pulse **Entrenar Watson para mejorar los resultados** en la parte superior derecha. No es necesario especificar una consulta en la pantalla **Crear consulta** para iniciar el entrenamiento. 
    - En el panel de control Rendimiento, pulse en el icono **Ver métricas de datos** en la izquierda para abrir el panel de control. Se le solicitará que elija una recopilación para entrenarla.
1.  En la pantalla **Entrenar Watson**, pulse **Añadir una consulta de lenguaje natural** como, por ejemplo: "IBM Watson in healthcare" y, a continuación, añádala. Asegúrese de escribir la consulta tal como lo harían sus usuarios. Además, las consultas de entrenamiento se deberían escribir con alguna superposición de términos entre la consulta y la respuesta deseada. Esto mejorará los resultados iniciales al ejecutar la consulta de lenguaje natural. El entrenamiento de relevancia solo utiliza consultas de lenguaje natural, no especifique consultas escritas en {{site.data.keyword.discoveryshort}} Query Language.
1.  Para ver los resultados de la consulta, pulse el botón **Valorar resultados** junto a los resultados. Si piensa que no hay suficientes resultados, podría intentar rescribir la consulta, o añadir más documentos a esta recopilación a través de la pantalla **Gestionar datos**.
1.  Empiece a valorar sus resultados como `relevantes` o `no relevantes`. Cuando haya terminado, pulse **Volver a las consultas**. En el conjunto de herramientas de {{site.data.keyword.discoveryshort}}, `Relevante` tiene una puntuación de `10` y `No relevante` tiene una puntuación de `0`. Si ya ha empezado a valorar resultados para esta recopilación utilizando la API y utilizó una escala de puntuación diferente, se visualizará un mensaje de aviso, con opciones para corregir el problema.
    En la parte superior de la ventana, Watson realiza un seguimiento del estado del entrenamiento, y proporcionar consejos sobre lo que puede hacer para mejorar los resultados. "Añadir más variedad a sus valoraciones" significa que debería utilizar tanto valoraciones `relevantes` como `no relevantes`. Una vez que haya satisfecho los requisitos, el entrenamiento empezará a actualizarse de forma periódica. Le tomará menos de 30 minutos completarlo una vez haya empezado, luego podrá continuar trabajando a medida que Watson actualiza.
1.  Continúe añadiendo consultas y valorando resultados.

Para volver a la pantalla principal de **Crear consultas**, pulse **Crear consultas** en la parte superior derecha.
{: tip}
Para volver a la pantalla **Gestionar datos**, pulse sobre el nombre de la recopilación en la parte superior derecha.
{: tip}

Si desea suprimir todos los datos de entrenamiento en su recopilación al mismo tiempo, debe hacerlo a través de la API. Consulte [Supresión de todos los datos de entrenamiento de una recopilación](https://{DomainName}/apidocs/discovery#delete-all-training-data) para obtener más información. Para obtener más información sobre el entrenamiento a través de la API, consulte [Mejora de la relevancia de los resultados de las consultas con la API](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api).

## Realización de pruebas e iteración para la relevancia de resultados
{: #testing-results}

Después de haber completado los resultados de valoración y de que Watson haya aplicado el entrenamiento, debe comprobar si los resultados de las consultas han mejorado. Para ello, ejecute consultas de prueba relacionadas (pero no idénticas) con las consultas de entrenamiento. Compruebe si los resultados de las consultas de prueba han mejorado.

Si desea mejorar aún más los resultados después de las pruebas, puede:
- Añadir más documentos a la recopilación.
- Añadir más consultas de entrenamiento.
- Valorar más resultados, asegurándose de utilizar tanto las valoraciones `relevante` como `no relevante`.

Consulte [Sugerencias de entrenamiento de relevancia](/docs/services/discovery?topic=discovery-relevancy-tips#relevancy-tips) para obtener más ayuda con relación al entrenamiento.

## Puntuaciones de confianza
{: #confidence}

{{site.data.keyword.discoveryshort}} devuelve una puntuación de `confidence` para las consultas de lenguaje natural y las escritas en {{site.data.keyword.discoveryshort}} Query Language.

Se devolverá la puntuación de `confidence` para las recopilaciones privadas entrenadas y no entrenadas (a excepción de las consultas de sólo filtro de recopilaciones no entrenadas). Además, {{site.data.keyword.discoveryshort}} devuelve un campo `document_retrieval_strategy` que indica el origen de la puntuación de `confidence`: 
-  `untrained`
-  `relevancy_training` o
-  `continuous_relevancy_training`

Se puede utilizar `document_retrieval_strategy` junto con la puntuación de `confidence` para determinar cómo se deben utilizar los resultados proporcionados. En los casos en los que la carga es alta, el valor devuelto de `document_retrieval_strategy` puede ser `untrained`, incluso si la recopilación se ha entrenado.

El valor de `confidence` varía entre 0.0 y 1.0. Cuanto mayor es el número, mayor es la relevancia del documento.

La puntuación de `confidence` se puede encontrar en los resultados de la consulta, bajo `result_metadata` en cada documento. El valor de `document_retrieval_strategy` aparecerá bajo `retrieval_details`.

```json
{
  "matching_results": 4,
  "session_token": "1_2gYuWJyaWx792Ni4_DQ4C5cbnW",
  "retrieval_details" : {
    "document_retrieval_strategy" : "relevancy_training",
  },
  "results": [
    {
      "id": "eea16dfd5fe6139a25324e7481a32f89_13",
            "result_metadata": {
        "confidence": 0.5893963975910735,
        "score": 0.5006834
      }
    }
  ]
}
```
{: codeblock}

En el caso de las recopilaciones entrenadas, el valor de `confidence` se calcula con base a cómo se estima de relevante un resultado en comparación con el modelo entrenado. Las recopilaciones entrenadas calculan las puntuaciones de `confidence` únicamente para las consultas de lenguaje natural. Si consulta una recopilación entrenada mediante {{site.data.keyword.discoveryshort}} Query Language, o el modelo entrenado no está disponible temporalmente, el número devuelto de `confidence` tendrá el valor `untrained` en `document_retrieval_strategy`. La puntuación de `confidence` para un resultado con el valor `untrained` en `document_retrieval_strategy` es una estimación no supervisada de la relevancia de los resultados del documento en la consulta; no es intercambiable con la puntuación devuelta para las recopilaciones entrenadas. Las recopilaciones entrenadas pueden proporcionar respuestas mejores a las consultas de lenguaje natural que las recopilaciones no entrenadas.

Tenga en cuenta que la puntuación de `confidence` **no** es la misma que la de `score`. Para obtener más información sobre la determinación de puntuaciones de confianza, consulte [Cómo seleccionar un umbral para actuar utilizando puntuaciones de confianza ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/watson/blog/2016/06/23/how-to-select-a-threshold-for-acting-using-confidence-scores/). El valor de `score` no se debería utilizar para establecer umbrales absolutos puesto que es un cálculo relativo. En su lugar, recomendamos que las aplicaciones siempre realicen el mismo comportamiento en todos los resultados que no incluyan el campo `confidence`. Por ejemplo, una aplicación puede mostrar u ocultar todos los resultados sin el campo `confidence`, pero no debe utilizar el valor de `score` para mostrar algunos y ocultar otros. Puesto que la forma en la que se calcula el valor de `confidence` varía entre los distintos métodos de recuperación, debe tener en cuenta el valor de `document_retrieval_strategy` al establecer un umbral y revisar los valores antes y después de entrenar.

Para obtener más información sobre las consultas, consulte [Iniciación a la creación de consultas](/docs/services/discovery?topic=discovery-getting-started-with-querying#getting-started-with-querying).

Para obtener más información sobre los métodos de entrenamiento supervisado, consulte
-  [Entrenamiento de relevancia](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling) y
-  [Entrenamiento de relevancia continuo](/docs/services/discovery?topic=discovery-crt#crt)
