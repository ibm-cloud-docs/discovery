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
{:gif: data-image-type='gif'}

# Comprensión de documentos inteligentes
{: #sdu}

La comprensión de documentos inteligentes (SDU) es una nueva forma de entrenar a {{site.data.keyword.discoveryfull}} para extraer campos personalizados en los documentos. Personalizar cómo se indexan los documentos en {{site.data.keyword.discoveryshort}} mejorará las respuestas devueltas por su aplicación.

SDU permite anotar campos dentro de los documentos para entrenar modelos de conversión personalizados. A medida que realiza anotaciones, Watson aprende y empieza a predecir anotaciones. Los modelos de SDU se pueden exportar y utilizar en otras recopilaciones. 

## Navegadores y tipos de documentos soportados
{: #doctypes}

Tipos de documentos soportados para la comprensión de documentos inteligentes: 
-  Planes Lite: PDF, Word, PowerPoint, Excel, JSON\*, HTML\*
-  Planes avanzados: PDF, Word, PowerPoint, Excel, PNG\*\*, TIFF\*\*, JPG\*\*, JSON\*, HTML\* 

\* {{site.data.keyword.discoveryfull}} soporta documentos JSON y HTML, pero estos no se pueden editar con el editor de SDU. Para cambiar la configuración de los documentos HTML y JSON, debe utilizar la API. Para obtener más información, consulte la [Referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery/){: new_window}.

\*\* Se exploran los archivos de imagen individuales (PNG, TIFF, JPG) y se extrae el texto (si lo hay). También se explorarán las imágenes PNG, TIFF y JPEG incluidas en archivos PDF, Word, PowerPoint y Excel, y se extraerá el texto (si lo hay).

Navegadores soportados: Chrome y Firefox.

## Utilización del editor de comprensión de documentos inteligentes
{: #annotate}

El editor de SDU solo está disponible para las nuevas recopilaciones que contienen tipos de documento soportados y no tienen aplicado el enriquecimiento de Clasificación de elementos. Las recopilaciones privadas existentes utilizarán el método de configuración original. Si desea utilizar el editor de SDU en una recopilación existente, deberá crear una nueva recopilación y cargar los documentos en ella. Si no desea utilizar el editor de SDU, puede definir la configuración mediante la API; consulte la [Referencia de la API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery/){: new_window}.
{: important}

Las funciones del editor de SDU sólo están disponibles en el conjunto de herramientas de {{site.data.keyword.discoveryshort}}, no están disponibles en la API.
{: note}

Navegación por el editor de comprensión de documentos inteligentes:

Si todavía no ha creado una instancia de {{site.data.keyword.discoveryshort}} y un entorno, consulte [Iniciación](/docs/services/discovery?topic=discovery-getting-started#getting-started) para obtener instrucciones.
{: tip}

1. En la pantalla **Gestionar datos**, pulse el botón **Cargar sus datos** y cree una nueva recopilación privada en {{site.data.keyword.discoveryshort}}.
1. Si lo desea, arrastre y suelte los documentos en la recopilación, o bien pulse **examinar desde el sistema** para cargar documentos. Después de completar la carga, se visualiza esta información:
   -  Los campos identificados en los documentos.
   -  Enriquecimientos aplicados a los documentos. {{site.data.keyword.discoveryshort}} aplica automáticamente al campo `texto` los enriquecimientos de Extracción de entidades, Análisis de sentimiento, Clasificación de categorías y Etiquetado de conceptos (a no ser que importe documentos mediante un conector). Puede añadir (o eliminar) enriquecimientos adicionales en el campo `texto`.
   -  Consultas creadas previamente que se pueden ejecutar de forma inmediata.
1. Pulse **Configurar datos** en la parte superior derecha. 
1. En la pantalla **Configurar datos**, habrá tres separadores: **Identificar campos**, **Gestionar campos** y **Enriquecer campos**.

   - **Identificar campos** contiene el editor de comprensión de documentos inteligentes. Este separador sustituye los separadores **Convertir** y **Normalizar** de la pantalla de {{site.data.keyword.discoveryshort}} original. 
   - **Gestionar campos** enumera todos los campos indexados (todos los campos se indexan de forma predeterminada). Desactive los campos que no desee indexar. Por ejemplo, los PDF pueden contener un pie de página o una cabecera repetitiva que no contenga información útil, por lo que puede excluir dichos campos del índice. Aquí también puede dividir documentos, en función de los campos; consulte [División de documentos](/docs/services/discovery?topic=discovery-sdu#splitting).
   - El separador **Enriquecer campos** es idéntico a **Enriquecer** en la pantalla original. Para obtener más información sobre los enriquecimientos, consulte [Adición de enriquecimientos](/docs/services/discovery?topic=discovery-configservice#adding-enrichments). La opción **Cargar documentos de ejemplo** no está disponible con recopilaciones de SDU.

   Si no ha cargado ningún documento antes, vuelva a la pantalla **Visión general** pulsando el nombre de la recopilación en la parte superior izquierda, o pulse el icono ![Gestionar datos](/images/icon_yourData.png) y elija la recopilación. Arrastre y suelte los documentos en la recopilación, o bien pulse **examinar desde el sistema**. Una vez que haya realizado una carga inicial, aparecerá el botón **Cargar documentos** en la parte superior derecha.
   {: important}

   Al utilizar la comprensión de documentos inteligentes, sólo se puede enriquecer el campo `texto`. No intente enriquecer ningún otro campo.
   {: important}

1. Abra el separador **Identificar campos**. Se cargarán como máximo veinte (20) documentos de la recopilación automáticamente en el editor de comprensión de documentos inteligentes.

La barra de herramientas de la parte superior le permitirá:
- Seleccionar un documento para anotar
- Navegar por el documento mostrado
- Ajustar la vista de página (`vista de página única`, `acercar`, `alejar`), `borrar cambios` y `exportar/importar modelos`. Pulse en `vista de página única` para cambiar la visualización; puede ver las anotaciones y el documento por separado o de forma conjunta.

También puede rastrear los orígenes de datos de Box, Salesforce, Microsoft SharePoint Online, IBM Cloud Object Storage y Microsoft SharePoint 2016, o efectuar un rastreo web con el conjunto de herramientas de {{site.data.keyword.discoveryshort}}. Pulse el botón **Conectar un origen de datos** y consulte [Conexión a orígenes de datos](/docs/services/discovery?topic=discovery-sources#sources) para obtener más información. Si crea una recopilación utilizando este método, no se aplicarán automáticamente los enriquecimientos.
{: tip}

## Cómo anotar un documento
{: #documents}

**Nota:** Las tablas se anotan en un paso aparte.

Consulte [Prácticas recomendadas para anotar documentos y tablas](/docs/services/discovery?topic=discovery-sdu#bestpractices) antes de empezar a realizar anotaciones.

1. Aparecerá un grupo de campos predeterminado en la parte derecha del documento. Los campos disponibles son `respuesta`, `autor`, `pie-de-página`, `cabecera`, `pregunta`, `subtítulo`, `tabla-de-contenidos`, `texto` y `título`. Si desea crear una o varias etiquetas de campo personalizadas nuevas, pulse **Crear nuevo**. Estos son los límites de número de etiquetas personalizadas: planes Lite - `0`, planes Avanzados - `5`, planes Premium - `20`.
1. Pulse en una etiqueta de campo a la derecha para activarla.
1. Haga clic en el contenido que representa este campo en el editor de Comprensión de documentos inteligentes. Aparecerá resaltado. 
   - De forma alternativa, puede seleccionar una etiqueta de campo a la derecha y arrastrarla al contenido en el editor de SDU. 
   - Para borrar un cambio, pulse en el botón **Borrar cambio** en la barra de herramientas.
1. Pulse **Enviar**.
   **Nota:** A medida que realiza anotaciones, Watson aprende y empieza a predecir anotaciones. Siga realizando anotaciones hasta que Watson identifique los campos de forma correcta y coherente.
1. Cuando haya terminado de realizar anotaciones, pulse en **Aplicar cambios a la recopilación**. Se abrirá la pantalla **Cargar los documentos**. Vuelva a cargar los documentos en la recopilación. Cuando se haya completado la carga, se le redirigirá a la pantalla **Gestionar datos**.

Campo | Definición  
------ | ------ 
respuesta | En un par de pregunta/respuesta (normalmente en las preguntas más frecuentes), la respuesta a la pregunta.
autor | Nombre del autor (o autores).
pie-de-página | Utilice este separador para denotar metainformación sobre el documento (como el número de página o referencia) que aparecen en la parte inferior de la página.
cabecera | Utilice esta etiqueta para indicar metainformación sobre el documento que aparece en la parte superior de la página.
pregunta | En el par de preguntas/respuestas (normalmente en las preguntas más frecuentes), la pregunta.
subtítulo | El título secundario del documento que se está anotando. 
tabla-de-contenidos | Utilice esta etiqueta en las listas de la tabla de contenido del documento.
texto | Utilice esta etiqueta en el texto de copia estándar, incluidos parágrafos, definiciones o cualquier grupo de palabras que no sean un título, parte de una tabla, una respuesta, un autor, un subtítulo o un pie de página. 
título | El título principal del documento que se está anotando.

## Cómo anotar una tabla
{: #tables}

La anotación de tablas está en release beta. Encontrará una explicación de las características beta que puede encontrar [aquí](/docs/services/discovery?topic=discovery-release-notes#beta-features).
{: important}

Consulte [Prácticas recomendadas para anotar documentos y tablas](/docs/services/discovery?topic=discovery-sdu#bestpractices) antes de empezar a realizar anotaciones.

1. Seleccione el campo `tabla` en la parte derecha del editor de SDU y, a continuación, seleccione la tabla en el documento. 
1. Mueva el puntero del ratón sobre la tabla para visualizar el botón **Anotar tabla**. Pulse en el botón para abrir el editor de tablas.
1. Primero, realice un esquema de la tabla:
   - Seleccione el campo `columna`.
   - Pulse en una columna de la tabla para activarla.
   - Seleccione el campo `fila`.
   - Pulse en una fila de la tabla para activarla.

   El esquema de la tabla aparecerá en la vista previa de la tabla en la parte izquierda.

   **Nota:** A medida que realiza anotaciones en tablas, Watson aprende y empieza a predecir anotaciones.
1. En segundo lugar, etiquete el contenido de la tabla.
1. Cuando haya terminado de realizar anotaciones en la tabla, pulse en **Anotaciones terminadas**.
1. Pulse en **Aplicar cambios a la recopilación**. Se abrirá la pantalla **Cargar los documentos**. Vuelva a cargar los documentos en la recopilación. Cuando se haya completado la carga, se le redirigirá a la pantalla **Gestionar datos**.

Utilice este vídeo como guía ![vídeo de anotaciones en tablas](images/SDU_table_demo.gif){: gif}

Campo | Definición  
------ | ------ 
cuerpo | Cualquier celda sin cabecera que contenga información
cabecera de columna | La celda de cabecera (si está presente) de cada columna de la tabla 
cabecera de varias columnas | Cualquier celda de cabecera que abarque más de una columna
título de fila | La cabecera de columna para la columna de las cabeceras de fila (si están presentes)
cabecera de filas | La etiqueta de fila (si está presente) de cada fila de la tabla
cabecera de varias filas | Cualquier etiqueta de fila que abarque más de una fila

## División de documentos
{: #splitting}

El separador **Gestionar campos** contiene la opción de **Mejorar los resultados de la consulta dividiendo los documentos**. Esta opción permite dividir los documentos en segmentos en función de un nombre de campo. Una vez divididos, cada segmento es un documento individual que se enriquecerá, indexará y devolverá como un resultado de consulta individual. 

Los documentos se dividen en función de un solo nombre de campo, por ejemplo: `título`, `autor`, `pregunta`. 

Consideraciones:

  - El número de segmentos por documento se limita a `250`. Cualquier contenido de documento que quede después de los `249` segmentos se almacenará en el segmento `250`.

  - Cada segmento se tendrá en cuenta con relación al límite de documentos de su plan. {{site.data.keyword.discoveryshort}} indexará segmentos hasta que se alcance el límite del plan. Consulte [Planes de precios de Discovery](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans) para ver los límites de documentos.

  - Los metadatos PDF y Word, así como los metadatos personalizados, se extraen y se incluyen en el índice con cada segmento. Cada segmento de un documento incluirá metadatos idénticos.

  - Si se ha actualizado un documento dividido y es necesario volver a cargarlo, el documento se debe sustituir utilizando el método [Actualizar documento ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery#update-a-document){: new_window}. El documento debe descargarse utilizando el método POST de la API `/environments/{environment_id}/collections/{collection_id}/documents/{document_id}`, que especifica el contenido del campo `parent_id` de uno de los segmentos actuales como la variable de vía de acceso `{document_id}`. Todos los segmentos se sobrescriben, a menos que la versión actualizada del documento tenga menos secciones que la original. Los segmentos más antiguos permanecerán en el índice y es posible suprimirlos de forma individual mediante la API. Consulte la [Referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery#delete-a-document){: new_window} para obtener más detalles. 

## Importación y exportación de modelos
{: #import}

Una vez que haya definido un modelo con el editor de SDU, puede guardarlo y reutilizarlo en otras recopilaciones.

Puede importar o exportar el modelo de SDU completado utilizando la barra de herramientas en la parte superior del editor. Pulse en el último icono y elija `Importar modelo` o `Exportar modelo`.

Los modelos exportados tienen la extensión de archivo `.sdumodel`. 

Los modelos importados están pensados para ser utilizados sin anotaciones adicionales. El modelo se sobrescribe completamente si continúa anotando después de importarlo. Si tiene previsto importar un modelo en una nueva recopilación, es una buena práctica recomendada crear una nueva recopilación que contenga sólo 1 documento, importar el modelo y, a continuación, cargar el resto de los documentos.

## Prácticas recomendadas para anotar documentos y tablas
{: #bestpractices}

La anotación de tablas está en release beta. Encontrará una explicación de las características beta que puede encontrar [aquí](/docs/services/discovery?topic=discovery-release-notes#beta-features).
{: important}

- Siga todas las directrices y cree etiquetas de forma coherente en todos los documentos
- No etiquete espacios en blanco
- Utilice las etiquetas de `imagen` en las imágenes y diagramas
- No trate el texto en **negrita**, _cursiva_ ni subrayado de forma distinta. Etiquete en función del contexto, no del estilo. 
- Al etiquetar un documento, hágalo de la primera página a la última.
- Si etiqueta un elemento de manera incorrecta, seleccione primero otra etiqueta para que el elemento se sobrescriba.
- Se pueden enviar las páginas en cualquier momento. Asegúrese de haber completado todo el proceso de etiquetado antes de enviarlas.
- Los documentos y tablas que parecen tener texto superpuesto a otro texto se conocen como documentos y tablas con "superposición doble" y no se pueden anotar. Notifique a su administrador acerca de estos documentos.
- Los documentos y tablas que contienen varias columnas de texto en una sola página no se pueden anotar. Notifique a su administrador acerca de estos documentos.
- Las notas a pie de página deben etiquetarse solo cuando aparezcan en la parte inferior de la página y estén referenciadas en el cuerpo de texto principal del documento.
- Las notas que aparezcan en las secciones o listas (por ejemplo, las llamadas de forma explícita "Notas") deben etiquetarse como `texto`.
- Si no está seguro de que la tabla se haya etiquetado correctamente y el panel de vista previa no responde, será necesario volver a cargar la página en el navegador y etiquetar la tabla para garantizar que se haya corregido la etiqueta.

