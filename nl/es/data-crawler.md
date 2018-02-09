---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-18"

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

# Adición de contenido con Data Crawler

El rastreador de datos permite automatizar la carga de contenido en el servicio {{site.data.keyword.discoveryshort}}.
{: shortdesc}

## Rastreo de datos con Data Crawler

Data Crawler es una herramienta de línea de mandatos que le ayudará a tomar documentos de los repositorios en donde residen (por ejemplo: comparticiones de archivos, bases de datos, Microsoft SharePoint) y enviarlos a la nube, para que el servicio {{site.data.keyword.discoveryshort}} los utilice. 

## Cuándo utilizar Data Crawler

Data Crawler se debería utilizar si desea un carga gestionada de un número significativo de archivos desde un sistema remoto, o si desea extraer contenido desde un repositorio soportado (como, por ejemplo, una base de datos de DB2). 

Data Crawler no está pensado como solución para cargar archivos desde su disco local. La carga de archivos desde una unidad local se debería realizar con el conjunto de herramientas o utilizando llamadas de API directas.
{: tip}

## Utilización de Data Crawler

1. [Configure el servicio {{site.data.keyword.discoveryshort}}](/docs/services/discovery/building.html#configuring-your-service)
1. [Descargue e instale Data Crawler](/docs/services/discovery/data-crawler-install.html) en un sistema Linux soportado que tenga acceso al contenido que desea rastrear.
1. [Conecte Data Crawler](/docs/services/discovery/data-crawler-seeds.html) a su contenido. 
1. [Configure Data Crawler](/docs/services/discovery/data-crawler-discovery.html) para conectarse al servicio {{site.data.keyword.discoveryshort}}. 
1. [Rastree su contenido](/docs/services/discovery/data-crawler-run.html).

Siga el siguiente ejemplo para empezar con rapidez con Data Crawler: [Iniciación a Data Crawler](/docs/services/discovery/data-crawler-qs.html). 
