---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-30"

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

# Watson Discovery News

{{site.data.keyword.discoverynewsfull}} se incluye con {{site.data.keyword.discoveryshort}}. {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} es un conjunto indexado de datos que está enriquecido de forma previa con los siguientes conocimientos cognitivos: **Extracción de palabras clave**, **Extracción de entidades**, **Extracción de roles semánticos**, **Análisis de sentimientos**, **Extracción de relaciones** y **Clasificación de categorías**. (Para obtener más información sobre los enriquecimientos, consulte [Adición de enriquecimientos](building.html#adding-enrichments)). También se añaden los siguientes metadatos adicionales: fecha de rastreo y fecha de publicación. La búsqueda histórica está disponible para los últimos 60 días de datos de noticias. Consulte una demostración que puede realizar con {{site.data.keyword.discoverynewsfull}} [aquí ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://discovery-news-demo.mybluemix.net/){: new_window}.

{{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} se actualiza continuamente con nuevos artículos. {{site.data.keyword.discoverynewsshort}} English se actualiza con aproximadamente 300.000 artículos nuevos cada día. {{site.data.keyword.discoverynewsshort}} Spanish se actualiza con aproximadamente 60.000 artículos nuevos cada día, {{site.data.keyword.discoverynewsshort}} Korean con 10.000 artículos cada día. 

Utilice los casos de uso de {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}}:

- Creación de alertas de noticias: Cree nuevas alertas de noticias aprovechando el soporte a entidades, palabras clave, categorías y el análisis de sentimiento para observar tanto las noticias como la forma en la que son percibidas. 

- Detección de sucesos: La extracción de roles semánticos sujeto/acción/objeto comprueba términos/acciones como "adquisición", "resultados elección" o "IPO".

- Tendencias en las noticias: Identifica temas de interés y supervisa incrementos y disminuciones sobre la frecuencia en la que estos temas o temas relacionados son mencionados. 

Para obtener información sobre cómo escribir consultas para {{site.data.keyword.discoverynewsfull}}, consulte [Conceptos de consultas](/docs/services/discovery/using.html) y [Referencia de consultas](/docs/services/discovery/query-reference.html). 

No es posible modificar la configuración de {{site.data.keyword.discoverynewsfull}}, ni entrenar ni añadir documentos a la recopilación de {{site.data.keyword.discoverynewsfull}}. 

**Nota:** El número máximo de resultados devueltos a una consulta de Watson Discovery es de `50`. Utilice consultas adicionales y el parámetro `offset` para obtener más de `50` resultados.

**Nota:** Esta versión de {{site.data.keyword.discoverynewsfull}} comenzó el **31 de julio del 2017**. El nombre de la versión original se cambió a {{site.data.keyword.discoverynewsfull}} Original. Esta versión ha sido retirada con una eliminación desde la fecha de servicio del **15 de enero del 2018**. Para obtener información sobre la migración, consulte [Migración desde Watson Discovery News Original](/docs/services/discovery/migrate-bwdn.html).
