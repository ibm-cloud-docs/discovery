---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-18"

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

# Rendimiento de consultas
{: #qp}

El rendimiento de las consultas en {{site.data.keyword.discoveryshort}} depende de una serie de factores. 

## Evaluación del rendimiento 
{: #qp-evaluate}

Si espera una carga simultánea alta en la aplicación, es importante evaluar el rendimiento de la aplicación de {{site.data.keyword.discoveryshort}}. Hay varias dimensiones que se utilizan con frecuencia para medir el rendimiento:
1.  **Latencia de respuesta**: el tiempo que tarda {{site.data.keyword.discoveryshort}} en devolver los resultados de la consulta. 
    - La latencia puede variar en función de varios factores; consulte [Factores que afectan al rendimiento](/docs/services/discovery?topic=discovery-qp#perffactors) para obtener más información. 
    - Es importante ejecutar pruebas en el entorno de producción utilizando un conjunto representativo de consultas para determinar la latencia media. 
1.   **Tasa de consultas**: el número de solicitudes que se pueden procesar en un momento determinado, normalmente medido en consultas por segundo (QPS). Esta medida es más importante cuando se espera una carga simultánea alta en la aplicación.  
     - La tasa que se puede obtener varía en función de muchos de los mismos factores que la latencia. 
     - La tasa de consultas también se debe evaluar con consultas representativas y en las cargas que se espera tener. Durante las pruebas, recuerde tener en cuenta las cargas máximas.

## Factores que afectan al rendimiento
{: #perffactors}

El rendimiento de las consultas en {{site.data.keyword.discoveryshort}} variará en función de una serie de factores, incluidos el tamaño del plan, la complejidad de las consultas, las características utilizadas y el tamaño y la complejidad de la recopilación.

### Tamaño del plan
{: #qp-plansize}

Los planes de precios de {{site.data.keyword.discoveryshort}} limitan el número de documentos disponibles y también proporcionan una capacidad distinta para manejar la carga de consultas. Cuanto mayor sea el tamaño del plan, más recursos estarán disponibles para manejar las consultas. El promedio de límites de tasas también varía según el tamaño del plan. La actualización del plan puede mejorar el rendimiento. Consulte [Planes de precios de {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans) para ver los planes y los límites. 

### Complejidad de consulta
{: #qp-query}

Hay muchas maneras de ejecutar consultas en {{site.data.keyword.discoveryshort}} y las distintas operaciones utilizadas pueden afectar al rendimiento. Estas características de consulta pueden afectar al rendimiento:

1.   **Longitud**: es muy probable que las consultas más largas tengan un rendimiento más bajo. 
1.   **Agregaciones**: las agregaciones son un tipo de consulta más complejo, con agregaciones anidadas que tienen el mayor impacto en el rendimiento. 
1.   **Operadores**: los comodines y las coincidencias aproximadas pueden afectar al rendimiento.
1.   **Recuentos**: la reducción del recuento de documentos devueltos puede mejorar el rendimiento; si necesita navegar por los resultados, utilice el parámetro `offset`. 
1.   **Campos devueltos**: limitar los campos devueltos a solo los necesarios para la aplicación puede resultar útil (por ejemplo, no devuelva el texto completo del documento si solo se necesitan el título y el pasaje). 

Consulte [Referencia de consultas](/docs/services/discovery?topic=discovery-query-reference#query-reference) para obtener detalles.

### Características utilizadas
{: #qp-features}

Hay una serie de características que mejoran los resultados de la consulta. Las características siguientes pueden afectar al rendimiento:
 
1.   **Recuperación de pasajes**: búsquedas de recuperación de pasajes dentro de los documentos para encontrar fragmentos de texto relevantes para la consulta. Puede ajustar los campos en los documentos en los que se realiza la búsqueda de recuperación de pasajes con el parámetro `passages.fields`; si el contenido tiene muchos campos, esto ayudará a reducir la latencia de la recuperación de pasajes. Consulte [Pasajes](/docs/services/discovery?topic=discovery-query-parameters#passages) para obtener más información sobre la recuperación de pasajes.
1.   **Entrenamiento de relevancia**: el entrenamiento de relevancia calcula características para cada campo de texto de nivel superior (campos al mismo nivel que `document_id` en el JSON) de la recopilación. Si hay muchos campos de nivel superior, el rendimiento de `natural_language_query` se puede ver afectado al utilizar el entrenamiento. Reducir el número de campos de nivel superior puede mejorar el rendimiento. Esta acción se puede realizar a través de la normalización o editando manualmente el JSON para poner campos que no son útiles para buscar contenido relevante en una estructura anidada. Cambiar los campos utilizados para el entrenamiento también tiene afecta al modelo, por lo que tendrá que tener en cuenta el impacto en el rendimiento y la precisión de los resultados si se realiza este cambio. Consulte [Mejora de la relevancia de los resultados](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling) para obtener más información sobre el entrenamiento de relevancia.
1.  **Entrenamiento de relevancia continuo**: las búsquedas de entrenamiento de relevancia continuo buscan en todas las recopilaciones de un entorno. Cuantas más recopilaciones hay en un entorno, mayor es el impacto en el rendimiento.  Consulte [Entrenamiento de relevancia continuo](/docs/services/discovery?topic=discovery-crt#crt) para obtener más información.

### Tamaño y complejidad de la recopilación
{: #qp-collection} 

La composición de los documentos de una recopilación privada también puede afectar al rendimiento de las consultas:
1.  **Número total de documentos**: el rendimiento puede verse afectado cuando están a punto de alcanzarse los límites máximos de `Número de documentos` para los tamaños de plan Avanzado. 
1.  **Tamaño de documentos**: los documentos muy grandes (con un tamaño de varios MB) requieren mover una gran cantidad de datos por solicitud, lo que puede afectar negativamente al rendimiento, especialmente cuando se utiliza la recuperación de pasajes y el entrenamiento de relevancia. 
1.  **Número de enriquecimientos**: los enriquecimientos añaden complejidad a los documentos añadiendo un número significativo de campos anidados. Si un enriquecimiento no es necesario para el caso de uso, inhabilítelo en el momento de la ingestión. Los enriquecimientos no se utilizan directamente para la relevancia de búsqueda de `natural_language_query`. Consulte [Adición de enriquecimientos](/docs/services/discovery?topic=discovery-configservice#adding-enrichments) para obtener más información sobre los enriquecimientos.
