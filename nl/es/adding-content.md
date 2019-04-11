---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-03-07"

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

# Adición de contenido
{: #addcontent}

¿Cómo decido el método que tengo que utilizar para cargar documentos?
{: shortdesc}

-   Utilice la [API](/docs/services/discovery?topic=discovery-gs-api#gs-api) si está integrando la carga de contenido con una aplicación existente o si desea crear su propio mecanismo de carga personalizada.
-   Utilice el [conjunto de herramientas de {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-getting-started#getting-started) si desea cargar con rapidez archivos que son localmente accesibles.
    Al cargar documentos utilizando el conjunto de herramientas de {{site.data.keyword.discoveryshort}}, todos los documentos deben tener un nombre de archivo exclusivo. Si dos archivos tienen el mismo nombre, el original se sobrescribe al cargar la versión más reciente. Si prefiere que documentos con el mismo nombre de archivo coexistan en la recopilación, se debe especificar el ID de documento. El ID de documento se puede especificar si carga documentos con la API o con Data Crawler.
-   Utilice el conjunto de herramientas de {{site.data.keyword.discoveryshort}} o la API para conectarse a los orígenes de datos de Box, Salesforce, Microsoft SharePoint Online, IBM Cloud Object Storage y Microsoft SharePoint 2016, o efectúe un rastreo web. Consulte [Conexión a orígenes de datos](/docs/services/discovery?topic=discovery-sources#sources) para obtener más información.
-   [Data Crawler](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler) permite una carga gestionada de un número significativo de archivos, o si desea extraer contenido de un repositorio soportado (como, por ejemplo, una base de datos DB2).

## Adición de contenido con el conjunto de herramientas o la API
{: #adding-content-with-the-api-or-tooling}

Tenga en cuenta lo siguiente cuando esté listo para añadir documentos a su recopilación:

-   El tamaño máximo del archivo que se puede cargar al servicio {{site.data.keyword.discoveryshort}} es de 50MB.
-   Los documentos de ejemplo no se añade automáticamente a la recopilación. Debe añadirlos si desea que sean parte de la recopilación. (Solo se aplica a las recopilaciones creadas antes de la publicación de la [Comprensión de documentos inteligentes](/docs/services/discovery?topic=discovery-sdu#sdu)).
-   Únicamente se enriquecerán los primeros 50.000 caracteres de cada campo JSON seleccionado para ser enriquecido.
-   Al crear una recopilación, se selecciona el idioma de los documentos (el inglés es el idioma predeterminado). Consulte [Soporte de idiomas](/docs/services/discovery?topic=discovery-language-support#language-support) para obtener la lista de idiomas. Los documentos serán enriquecidos en el idioma seleccionado. No mezcle idiomas dentro de la misma recopilación.
-   {{site.data.keyword.discoveryshort}} puede ingerir los tipos de archivos siguientes y los demás tipos de documento se ignoran:

Recopilación | Planes Lite | Planes Avanzados 
---------------- | ------------------------------ | ------------------------------------------- 
Recopilaciones existentes creadas específicamente para {{site.data.keyword.discoveryfull}} antes de la publicación de la [Comprensión de documentos inteligentes (SDU)](/docs/services/discovery?topic=discovery-release-notes#22jan19) | Microsoft Word, PDF, HTML, JSON | Microsoft Word, PDF, HTML, JSON     
Recopilaciones creadas tras el release de [SDU](/docs/services/discovery?topic=discovery-sdu#sdu) | PDF, Word, PowerPoint, Excel, JSON\*, HTML\* | PDF, Word, PowerPoint, Excel, PNG\*\*, TIFF\*\*, JPG\*\*, JSON\*, HTML\* 
    
\* {{site.data.keyword.discoveryfull}} soporta documentos JSON y HTML, pero estos no se pueden editar con el editor de SDU. Para cambiar la configuración de los documentos HTML y JSON, debe utilizar la API. Para obtener más información, consulte la [Referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery/){: new_window}.

\*\* Se exploran los archivos de imagen individuales (PNG, TIFF, JPG) y se extrae el texto (si lo hay). También se explorarán las imágenes PNG, TIFF y JPEG incluidas en archivos PDF, Word, PowerPoint y Excel, y se extraerá el texto (si lo hay).
-   Los documentos de la recopilación se convertirán utilizando la configuración actual, a no ser que elija un archivo de configuración diferente. Para obtener información sobre cómo crear un archivo de configuración, consulte [Configuración personalizada](/docs/services/discovery?topic=discovery-configservice#custom-configuration). (Solo se aplica a las recopilaciones creadas antes de la publicación de la [Comprensión de documentos inteligentes](/docs/services/discovery?topic=discovery-sdu#sdu)).
-   Cuando se cargan documentos en una recopilación de datos, se convierten y enriquecen utilizando el archivo de configuración elegido para dicha recopilación. Si decide posteriormente que desea cambiar una recopilación con un archivo de configuración diferente, puede hacerlo, sin embargo, los documentos que ya se han cargado seguirán convertidos según al archivo de configuración original. Todos los documentos cargados después de cambiar el archivo de configuración utilizarán el nuevo archivo de configuración. Si desea que **toda**
la recopilación utilice la nueva configuración, necesitará crear una nueva recopilación, elegir el nuevo archivo de configuración y volver a cargar todos los documentos. (Si se utiliza la [Comprensión de documentos inteligentes](/docs/services/discovery?topic=discovery-sdu#sdu), se le solicitará que vuelva a cargar los documentos después de pulsar el botón **Aplicar cambios a la recopilación**).
-   No puede especificar el valor `data type` (Por ejemplo: `text` o `date`) de los campos. Durante la ingestión de documentos, si se detecta que un campo no existe en el índice, {{site.data.keyword.discoveryshort}} detectará automáticamente el valor `data type` del campo en función del valor del campo del primer documento indexado.
-   Un documento podría no ingerirse debido a una discrepancia entre el tipo de los datos en el documento actual y datos parecidos en un documento ingerido con anterioridad. Por ejemplo, un campo podría definirse como `date` en un documento y como `string` en un documento posterior, impidiendo que éste último se indexase de forma correcta.
-   Si tiene previsto utilizar la señalización personalizada (actualmente solo disponible en las recopilaciones japonesas al utilizar la API de {{site.data.keyword.discoveryshort}}), el diccionario de señalización de la colección debe añadirse antes de cargar documentos.

## Carga de documentos con el conjunto de herramientas de Discovery
{: #upload_tooling}

1.  Cree una recopilación. Consulte [Preparación del servicio para los documentos](/docs/services/discovery?topic=discovery-configservice#preparing-the-service-for-your-documents).
1.  Pulse en la recopilación para abrirla.
1.  Pulse el botón **Cargar documentos** y empiece a cargar los documentos mediante el mecanismo de arrastrar y soltar o examinando a través del sistema de archivos.

Los documentos se colocarán en la cola para ser convertidos y enriquecidos. El tiempo necesario dependerá del tamaño de la recopilación. Después de indexar y enriquecer, se visualizarán los detalles de la recopilación en la sección **Visión general**.

-   Los **Campos identificados** en la recopilación (solo la Comprensión de documentos inteligentes).
-   Fechas de **Creación** y **Última actualización** (pulse en **Utilizar esta recopilación en una API** para ver los valores de `collection_id`, `configuration_id` y `environment_id`).
-   **Número de documentos** en su recopilación
-   **Configuración**: El nombre del archivo de configuración utilizado para convertir esta recopilación (solo para recopilaciones creadas antes de la publicación de la [Comprensión de documentos inteligentes](/docs/services/discovery?topic=discovery-sdu#sdu)).
-   **Errores y avisos**

Para obtener información sobre cómo conectarse a los orígenes de datos de Box, Salesforce, Microsoft SharePoint Online, IBM Cloud Object Storage y Microsoft SharePoint 2016, o efectuar un rastreo web con el conjunto de herramientas de {{site.data.keyword.discoveryshort}}, consulte [Conexión a orígenes de datos](/docs/services/discovery?topic=discovery-sources#sources).


## Carga de documentos con la API
{: #upload_api}

Consulte [Iniciación a la {{site.data.keyword.discoveryshort}} API](/docs/services/discovery?topic=discovery-gs-api#gs-api) para una guía de aprendizaje paso a paso.

Para obtener más información sobre la API, consulte la [Referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery/){: new_window}.

1.  Utilice el método `POST /v1/environments/{environment_id}/collections` para crear una recopilación.
1.  A continuación, utilice el método `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` para añadir documentos a su recopilación.

## Rastreo de URL
{: #crawl_urls}

Rastree URL e indéxelas con el [Plugin de indexación para Apache Nutch ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/IBM-Watson/nutch-indexer-discovery) de {{site.data.keyword.IBM_notm}} {{site.data.keyword.watson}} {{site.data.keyword.discoveryshort}} Service. El rastreo no actualiza de forma automática, de modo que será necesario repetir el procedimiento periódicamente para mantener el índice actualizado. 

También tiene la opción de utilizar la versión beta del conector de rastreo web. Consulte [Conexión a orígenes de datos](/docs/services/discovery?topic=discovery-sources#connectwebcrawl).
