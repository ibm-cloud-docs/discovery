---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-25"

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

# Visualización de métricas y mejora de los resultados de consulta con el panel de control de rendimiento
{: #performance-dashboard}

El panel de control de rendimiento del conjunto de herramientas de {{site.data.keyword.discoveryshort}} puede utilizarse para visualizar métricas de consulta y para mejorar resultados de consulta, incluida la relevancia de consultas.

Puede acceder al panel de control de rendimiento pulsando en el icono **Visualizar métricas de datos** de la izquierda. El panel de control no está disponible en los entornos Premium o Dedicado.

Hay dos formas de mejorar los resultados de consulta del lenguaje natural:
- [Arreglar las consultas sin resultados añadiendo más datos](/docs/services/discovery?topic=discovery-performance-dashboard#addmore)
- [Otorgar prioridad a los resultados relevantes entrenando los datos](/docs/services/discovery?topic=discovery-performance-dashboard#traindata)

Puede visualizar las métricas de datos en la [visión general de consulta](/docs/services/discovery?topic=discovery-performance-dashboard#overview). 

## Arreglar las consultas sin resultados añadiendo más datos
{: #addmore}

En esta sección del panel de control, puede revisar las consultas que no han devuelto resultados y añadir más datos para que devuelvan resultados en el futuro. Pulse el botón **Visualizar todo y añadir datos** para empezar. 

## Otorgar prioridad a los resultados relevantes entrenando los datos
{: #traindata}

En esta sección, puede entrenar sus recopilaciones para mejorar la relevancia de los resultados de consulta del lenguaje natural. Pulse el botón **Visualizar todo y realizar un entrenamiento de relevancia** para empezar. A continuación, consulte [Adición de consultas y calificación de la relevancia de resultados](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#results) para obtener instrucciones.

Para obtener más información sobre los requisitos y opciones de entrenamiento, consulte [Mejora de la relevancia de resultados con el conjunto de herramientas](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling).

## Descripción general de las consultas
{: #overview}

La sección Descripción general de las consultas muestra:
- El número total de consultas realizadas por los usuarios
- El porcentaje de consultas con uno o varios resultados seleccionados
- El porcentaje de consultas sin resultados seleccionados
- El porcentaje de consultas sin resultados devueltos
- Un gráfico que muestra los resultados a lo largo del tiempo, para que pueda realizar un seguimiento sobre cómo mejoran el rendimiento la adición de más datos y el entrenamiento de relevancia

Estos resultados se recopilan utilizando la API Sucesos y comentarios. Consulte la [referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery#create-event) para obtener más información.
