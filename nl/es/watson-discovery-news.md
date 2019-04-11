---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-02-05"

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

# Watson Discovery News
{: #watson-discovery-news}

{{site.data.keyword.discoverynewsfull}} se incluye con {{site.data.keyword.discoveryshort}}. {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} es un conjunto indexado de datos que está enriquecido de forma previa con los siguientes conocimientos cognitivos: **Extracción de palabras clave**, **Extracción de entidades**, **Extracción de roles semánticos**, **Análisis de sentimientos**, **Extracción de relaciones** y **Clasificación de categorías**. (Para obtener más información sobre los enriquecimientos, consulte [Adición de enriquecimientos](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)). También se añaden los siguientes metadatos adicionales: fecha de rastreo y fecha de publicación. La búsqueda histórica está disponible para los últimos 60 días de datos de noticias. Consulte una demostración que puede realizar con {{site.data.keyword.discoverynewsfull}} [aquí ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://discovery-news-demo.ng.bluemix.net/){: new_window}.

{{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} se actualiza continuamente con nuevos artículos y está disponible en inglés, español, alemán, coreano y japonés. {{site.data.keyword.discoverynewsshort}} en inglés se actualiza con aproximadamente 300.000 artículos nuevos cada día. {{site.data.keyword.discoverynewsshort}} en español se actualiza diariamente con aproximadamente 60.000 nuevos artículos; {{site.data.keyword.discoverynewsshort}} en alemán se actualiza diariamente con aproximadamente 15.000 nuevos artículos; {{site.data.keyword.discoverynewsshort}} en coreano se actualiza diariamente con 10.000 artículos. {{site.data.keyword.discoverynewsshort}} en japonés se actualiza diariamente con 17.000 artículos nuevos aproximadamente. Las fuentes de noticias varían según el idioma, por lo que los resultados de la consulta de cada colección no serán idénticos.

Utilice los casos de uso de {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}}:

- Creación de alertas de noticias: Cree nuevas alertas de noticias aprovechando el soporte a entidades, palabras clave, categorías y el análisis de sentimiento para observar tanto las noticias como la forma en la que son percibidas.

- Detección de sucesos: La extracción de roles semánticos sujeto/acción/objeto comprueba términos/acciones como "adquisición", "resultados elección" o "IPO".

- Tendencias en las noticias: Identifica temas de interés y supervisa incrementos y disminuciones sobre la frecuencia en la que estos temas o temas relacionados son mencionados.

Para obtener información sobre cómo escribir consultas para {{site.data.keyword.discoverynewsfull}}, consulte:
- [Consultas para Watson Discovery News](/docs/services/discovery?topic=discovery-query-concepts#querying-news)
- [Conceptos de consultas](/docs/services/discovery?topic=discovery-query-concepts)
- [Referencia de consulta](/docs/services/discovery?topic=discovery-query-reference#query-reference).

No es posible modificar la configuración de {{site.data.keyword.discoverynewsfull}}, ni entrenar ni añadir documentos a la recopilación de {{site.data.keyword.discoverynewsfull}}.

Las consultas de {{site.data.keyword.discoverynewsfull}} muestran aproximadamente 50 palabras de cada artículo en el campo JSON `text`. Estas palabras se extraen de los aspectos más destacados. Consulte [aspectos destacados](/docs/services/discovery?topic=discovery-query-parameters#highlight) para obtener una explicación de los aspectos destacados. Para habilitar este comportamiento, no es necesario incluir de forma explícita los aspectos destacados en la consulta.

El número máximo de resultados devueltos para una consulta de {{site.data.keyword.discoverynewsfull}} es `50`. Utilice consultas adicionales y el parámetro `offset` para obtener más de `50` resultados.

**Nota:** Esta versión de {{site.data.keyword.discoverynewsfull}} comenzó el **31 de julio del 2017**. {{site.data.keyword.discoverynewsfull}} Original se retiró del servicio el **15 de enero de 2018**. Para obtener información sobre la migración, consulte [Migración desde Watson Discovery News Original](/docs/services/discovery?topic=discovery-migrate-bwdn#migrate-bwdn).
