---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-07"

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

# Acerca de este servicio
{: #about}

{{site.data.keyword.discoveryfull}} permite crear con rapidez aplicaciones cognitivas de exploración basadas en la nube, que son capaces de desvelar conocimiento útil oculto en datos no estructurados - incluido en sus propios datos, así como en datos públicos de terceros.
{: shortdesc}

Esta es la arquitectura de toda la solución del servicio {{site.data.keyword.discoveryshort}}:

![Diagrama de la arquitectura de Discovery](images/discovery-flow.png)

Con {{site.data.keyword.discoveryshort}}, solo se necesitan unos pocos pasos para preparar sus datos no estructurados, crear una consulta que señalará la información que necesita y, a continuación, integrar estos conocimientos en nuevas aplicaciones o en soluciones existentes.

¿Cómo lo hace {{site.data.keyword.discoveryshort}}? Combinando el análisis de datos con la intuición cognitiva para tomar sus datos no estructurados y enriquecerlos de forma que descubra la información que necesita.

{{site.data.keyword.discoveryfull}} reúne un conjunto funcionalmente completo de API integradas y automatizadas de {{site.data.keyword.watson}} para:

- Rastrear, convertir, enriquecer y normalizar datos.
- Explorar el contenido propio de forma segura, así como contenido público gratuito y con licencia.
- Aplicar enriquecimientos adicionales como conceptos, relaciones y sentimientos a través del NLU ({{site.data.keyword.nlushort}}).
- Simplificar el desarrollo a la vez que proporcionar un acceso directo a las API.

Para obtener información sobre el soporte de idiomas, consulte [Soporte de idiomas de {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-language-support#language-support).

Para obtener información sobre la seguridad de {{site.data.keyword.Bluemix_notm}}, consulte la [Descripción del servicio de {{site.data.keyword.Bluemix_notm}}![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=%28IBM+Cloud+Service+description%29){: new_window}

{{site.data.keyword.discoveryfull}} Knowledge Graph es una característica en fase Beta que proporciona nuevos puntos finales para consultar entidades y relaciones entre documentos. Incluye búsquedas basadas en el contexto y clasificación según la relevancia. Consulte [{{site.data.keyword.discoveryfull}} Knowledge Graph](/docs/services/discovery?topic=discovery-kg#kg) para obtener más información.

## Soporte de navegador y requisitos previos
{: #browser-support-and-prerequisites}

Para obtener la lista de requisitos previos y navegadores soportados para {{site.data.keyword.Bluemix}}, consulte [Requisitos ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/docs/overview/prereqs.html#prereqs){: new_window}.

## Watson Discovery News
{: #wds}

{{site.data.keyword.discoverynewsshort}}, un conjunto de datos públicos que previamente se ha enriquecido con conocimientos cognitivos, también se incluye con {{site.data.keyword.discoveryshort}}. Puede utilizar este conjunto de datos no estructurados públicos para consultar información que se puede integrar en sus aplicaciones. Consulte [Watson Discovery News](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news) para obtener más información. Consulte una demostración que puede realizar con {{site.data.keyword.discoverynewsshort}} [aquí ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://discovery-news-demo.ng.bluemix.net/){: new_window}.

El servicio {{site.data.keyword.discoveryshort}} está disponible en [{{site.data.keyword.Bluemix_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/catalog/services/discovery){: new_window}

## Conjunto de herramientas de Discovery
{: #discovery-tooling}

El servicio {{site.data.keyword.discoveryshort}} incluye un conjunto completo de herramientas en línea, el conjunto de herramientas de {{site.data.keyword.discoveryshort}}, para ayudarle a configurar rápidamente una instancia del servicio y cumplimentarla con datos.

El conjunto de herramientas de servicio {{site.data.keyword.discoveryshort}} ha sido diseñada para que ahorre tiempo eliminando la necesidad de utilizar API para configurar y cumplimentar su servicio. Esto permite a los desarrolladores de aplicaciones centrarse en crear soluciones de alto valor para que los usuarios finales experimenten el servicio {{site.data.keyword.discoveryshort}}. Consulte [Iniciación al conjunto de herramientas](/docs/services/discovery?topic=discovery-getting-started#getting-started) para una introducción al conjunto de herramientas de {{site.data.keyword.discoveryshort}}.


## Pasos siguientes
{: #next-steps}

- Empiece con el conjunto de herramientas de {{site.data.keyword.discoveryshort}} o con la {{site.data.keyword.discoveryshort}} API:
    - [Iniciación al conjunto de herramientas de {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-getting-started#getting-started)
    - [Iniciación a la API de {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-gs-api#gs-api)
- El servicio de {{site.data.keyword.discoveryshort}} ofrece soporte a un número de SDK para simplificar el desarrollo de aplicaciones. Los SDK están disponibles para varios lenguajes de programación y plataformas ampliamente utilizados, que incluyen Node.js, Java y Python. Todos los SDK están disponibles en el [espacio de nombres watson-developer-cloud ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/watson-developer-cloud){: new_window} en GitHub.
    - Para ver una lista completa de los SDK e información sobre cómo utilizarlos, consulte [SDK de {{site.data.keyword.watson}}](https://cloud.ibm.com/docs/services/watson/getting-started-sdks.html#sdks).
    - Para obtener información detallada sobre todos los métodos de SDK Node, Java y Python, consulte la [referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery){: new_window}.
