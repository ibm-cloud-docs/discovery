---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-15"

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

# Adición de contenido

¿Cómo decido el método que tengo que utilizar para cargar documentos?
{: shortdesc}

-   Utilice la [API](/docs/services/discovery/getting-started.html) si está integrando la carga de contenido con una aplicación existente o si desea crear su propio mecanismo de carga personalizada.
-   Utilice el [conjunto de herramientas de {{site.data.keyword.discoveryshort}}](/docs/services/discovery/getting-started-tool.html) si desea cargar con rapidez archivos que son localmente accesibles.
    Al cargar documentos utilizando el conjunto de herramientas de {{site.data.keyword.discoveryshort}}, todos los documentos deben tener un nombre de archivo exclusivo. Si dos archivos tienen el mismo nombre, el original se sobrescribe al cargar la versión más reciente. Si prefiere que documentos con el mismo nombre de archivo coexistan en la recopilación, se debe especificar el ID de documento. El ID de documento se puede especificar si carga documentos con la API o con Data Crawler.
-   Utilice el conjunto de herramientas de {{site.data.keyword.discoveryshort}} o la API para conectarse a los orígenes de datos de Box, Salesforce y Microsoft SharePoint Online. Consulte [Conexión a orígenes de datos](/docs/services/discovery/connect.html) para obtener más información.
-   [Data Crawler](/docs/services/discovery/data-crawler.html) permite una carga gestionada de un número significativo de archivos, o si desea extraer contenido de un repositorio soportado (como, por ejemplo, una base de datos DB2).

## Adición de contenido con el conjunto de herramientas o la API

Tenga en cuenta lo siguiente cuando esté listo para añadir documentos a su recopilación:

-   El tamaño máximo del archivo que se puede cargar al servicio {{site.data.keyword.discoveryshort}} es de 50MB.
-   Los documentos de ejemplo no se añade automáticamente a la recopilación. Debe añadirlos si desea que sean parte de la recopilación.
-   Únicamente se enriquecerán los primeros 50.000 caracteres de cada campo JSON seleccionado para ser enriquecido.
-   Al crear una recopilación, se selecciona el idioma de los documentos (el inglés es el idioma predeterminado). Consulte [Soporte de idiomas](/docs/services/discovery/language-support.html) para obtener la lista de idiomas. Los documentos serán enriquecidos en el idioma seleccionado. No mezcle idiomas dentro de la misma recopilación.
-   Se pueden añadir documentos Microsoft Word, PDF, HTML y JSON a su recopilación. **Nota:** Los archivos PDF que corresponden a archivos de imágenes escaneadas no se pueden convertir ni enriquecer.
-   Los documentos de la recopilación se convertirán utilizando el archivo de configuración que proporcione, la Configuración predeterminada, a no ser que elija un archivo de configuración diferente. Para obtener información sobre cómo crear un archivo de configuración, consulte [Configuración personalizada](/docs/services/discovery/building.html#custom-configuration).
-   Cuando se cargan documentos en una recopilación de datos, se convierten y enriquecen utilizando el archivo de configuración elegido para dicha recopilación. Si decide posteriormente que desea cambiar una recopilación con un archivo de configuración diferente, puede hacerlo, sin embargo, los documentos que ya se han cargado seguirán convertidos según al archivo de configuración original. Todos los documentos cargados después de cambiar el archivo de configuración utilizarán el nuevo archivo de configuración. Si desea que **toda** la recopilación utilice la nueva configuración, necesitará crear una nueva recopilación, elegir el nuevo archivo de configuración y volver a cargar todos los documentos.
-   No puede especificar el valor `data type` (Por ejemplo: `text` o `date`) de los campos. Durante la ingestión de documentos, si se detecta que un campo no existe en el índice, {{site.data.keyword.discoveryshort}} detectará automáticamente el valor `data type` del campo en función del valor del campo del primer documento indexado.
-   Un documento podría no ingerirse debido a una discrepancia entre el tipo de los datos en el documento actual y datos parecidos en un documento ingerido con anterioridad. Por ejemplo, un campo podría definirse como `date` en un documento y como `string` en un documento posterior, impidiendo que éste último se indexase de forma correcta.
-   Si tiene previsto utilizar la tokenización personalizada (actualmente solo disponible en las recopilaciones japonesas al utilizar la API de {{site.data.keyword.discoveryshort}}), el diccionario de tokenización de la colección debe añadirse antes de cargar documentos.

Se aplican los siguientes límites al cargar documentos:

-   Planes **Lite**: 21 documentos en curso
-   Planes **Avanzados**: 105 documentos en curso (excepto en los planes Avanzados extra pequeños, que disponen de un límite de 50 documentos en curso)
-   Planes **Premium**: 210 documentos en curso

Estos límites están sujetos a cambios. 

Al utilizar el servicio Discovery, la carga en curso representa el documento que se está cargando y procesando antes de que se añada a la recopilación. Si alcanza el límite en curso, debe reducir la velocidad de la ingestión. Una opción es añadir un mecanismo automatizado de interrupción con reintentos.

## Carga de documentos con el conjunto de herramientas de Discovery

1.  Cree una recopilación. Consulte [Preparación del servicio para los documentos](/docs/services/discovery/building.html#preparing-the-service-for-your-documents).
1.  Pulse en la recopilación para abrirla.
1.  Pulse el botón **Cargar documentos** y empiece a cargar los documentos mediante el mecanismo de arrastrar y soltar o examinando a través del sistema de archivos.

Los documentos se colocarán en la cola para ser convertidos y enriquecidos. El tiempo necesario dependerá del tamaño de la recopilación. Después de indexar y enriquecer, se visualizarán los detalles de la recopilación en la sección **Visión general**.

-   Fechas de **Creación** y **Última actualización** (pulse en **Utilizar esta recopilación en una API** para ver los valores de `collection_id`, `configuration_id` y `environment_id`).
-   **Número de documentos** en su recopilación
-   **Configuración** - El nombre del archivo de configuración utilizado para convertir esta recopilación
-   **Errores y avisos **

Para obtener información sobre cómo conectarse a los orígenes de datos de Box, Salesforce y Microsoft SharePoint Online con el conjunto de herramientas de {{site.data.keyword.discoveryshort}}, consulte [Conexión a orígenes de datos](/docs/services/discovery/connect.html).


## Carga de documentos con la API

Consulte [Iniciación a la {{site.data.keyword.discoveryshort}} API](/docs/services/discovery/getting-started.html) para una guía de aprendizaje paso a paso.

Para obtener más información sobre la API, consulte la [Referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}.

1.  Utilice el método `POST /v1/environments/{environment_id}/collections` para crear una recopilación.
1.  A continuación, utilice el método `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` para añadir documentos a su recopilación.

## Rastreo de URL

Rastree URL e indéxelas con el [Plugin de indexación para Apache Nutch ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/IBM-Watson/nutch-indexer-discovery) de {{site.data.keyword.IBM_notm}} {{site.data.keyword.watson}} {{site.data.keyword.discoveryshort}} Service. El rastreo no actualiza de forma automática, de modo que será necesario repetir el procedimiento periódicamente para mantener el índice actualizado.
