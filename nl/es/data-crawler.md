---

copyright:
  years: 2015, 2017, 2019
lastupdated: "2019-02-08"

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

# Adición de contenido con Data Crawler
{: #adding-content-with-data-crawler}

El rastreador de datos permite automatizar la carga de contenido en el servicio {{site.data.keyword.discoveryshort}}.
{: shortdesc}

Data Crawler solo debe utilizarse para rastrear comparticiones de archivos o bases de datos, en todos los demás casos debe utilizar el conector adecuado de {{site.data.keyword.discoveryshort}}. Consulte [Conexión a orígenes de datos](/docs/services/discovery?topic=discovery-sources#sources) para obtener más información. Ya no se proporciona asistencia para Data Crawler si lo está utilizando con un origen de datos soportado por los conectores de {{site.data.keyword.discoveryshort}}.
{: important}

## Rastreo de datos con Data Crawler
{: #dc-crawling}

Data Crawler es una herramienta de línea de mandatos que le ayudará a tomar documentos de los repositorios en donde residen (por ejemplo: comparticiones de archivos, bases de datos) y enviarlos a la nube, para que el servicio {{site.data.keyword.discoveryshort}} los utilice.

Data Crawler solo debe utilizarse para rastrear comparticiones de archivos o bases de datos, en todos los demás casos debe utilizar el conector adecuado de {{site.data.keyword.discoveryshort}} para Box, SharePoint, Salesforce, IBM Cloud Object Storage o el rastreo web. Consulte [Conexión a orígenes de datos](/docs/services/discovery?topic=discovery-sources#sources) para obtener más información. Ya no se proporciona asistencia para Data Crawler si lo está utilizando con un origen de datos soportado por los conectores de {{site.data.keyword.discoveryshort}}.
{: important}

## Cuándo utilizar Data Crawler
{: #dc-use}

Data Crawler se debería utilizar si desea un carga gestionada de un número significativo de archivos desde un sistema remoto, o si desea extraer contenido desde un repositorio soportado (como, por ejemplo, una base de datos de DB2).

Data Crawler no está pensado como solución para cargar archivos desde su disco local. La carga de archivos desde una unidad local se debería realizar con el conjunto de herramientas o utilizando llamadas de API directas. Otra opción para cargar un gran número de archivos en {{site.data.keyword.discoveryshort}} es [discovery-files ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/IBM/discovery-files){: new_window} en GitHub.
{: note}

## Utilización de Data Crawler
{: #dc-using}

1. [Configure el servicio {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-configservice#configservice)
1. [Descargue e instale Data Crawler](/docs/services/discovery?topic=discovery-downloading-and-installing-the-data-crawler#downloading-and-installing-the-data-crawler) en un sistema Linux soportado que tenga acceso al contenido que desea rastrear.
1. [Conecte Data Crawler](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-connector-and-seed-options) a su contenido.
1. [Configure Data Crawler](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-the-data-crawler) para conectarse al servicio {{site.data.keyword.discoveryshort}}.
1. [Rastree su contenido](/docs/services/discovery?topic=discovery-crawling-your-data-repository#crawling-your-data-repository).

Siga el siguiente ejemplo para empezar con rapidez con Data Crawler: [Iniciación a Data Crawler](/docs/services/discovery?topic=discovery-getting-started-with-the-data-crawler#getting-started-with-the-data-crawler).
