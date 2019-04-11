---

copyright:
  years: 2015, 2018, 2019
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

# Iniciación
{: #getting-started}

En esta breve guía de aprendizaje, introduciremos el conjunto de herramientas de {{site.data.keyword.discoveryshort}} y recorreremos el proceso de creación de una recopilación de datos privados en los que buscar.
{: shortdesc}

Si prefiere trabajar en la API, consulte [Iniciación a la API](/docs/services/discovery?topic=discovery-gs-api#gs-api).
{: tip}

## Antes de empezar
{: #before-you-begin-tool}
{: hide-dashboard}

Para poder empezar, necesita una instancia de servicio.
{: hide-dashboard}

1.  {: hide-dashboard} Vaya a la página [{{site.data.keyword.discoveryshort}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/catalog/services/discovery) en el catálogo de {{site.data.keyword.cloud_notm}}.

    La instancia de servicio se crea en el grupo de recursos **predeterminado** si no elige uno diferente, y *no se puede* cambiar posteriormente. Este grupo es suficiente para probar el servicio.

    Si va a crear una instancia para un uso más potente, obtenga más información sobre los [grupos de recursos ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/docs/resources/bestpractice_rgs.html#bp_resourcegroups){: new_window}.
1.  {: hide-dashboard} Regístrese para obtener una cuenta de {{site.data.keyword.cloud_notm}} gratuita o inicie sesión.
1.  {: hide-dashboard} Pulse **Crear**.

## Paso 1: Iniciar el conjunto de herramientas
{: #launch-the-tooling}

Después de crear una instancia del servicio de {{site.data.keyword.discoveryshort}}, aparecerá su lista de servicios.
{: hide-dashboard}

1.  {: hide-dashboard} Pulse la instancia de servicio de {{site.data.keyword.discoveryshort}} que ha creado para ir al panel de control del servicio.
1.  En la página **Gestionar**, pulse **Iniciar herramienta**. Si se le solicita que inicie sesión en el conjunto de herramientas, proporcione las credenciales de {{site.data.keyword.cloud_notm}}.

<!-- To do: Add screenshot for developer console -->

## Paso 2: Crear una recopilación
{: #create-a-collection-tool}

El primer paso en el conjunto de herramientas de {{site.data.keyword.discoveryshort}} es crear una recopilación de datos.

Una recopilación es un conjunto de documentos. *¿Por qué querría más de una recopilación?* Hay varias razones:

- Puede que desee varias recopilaciones para separar los resultados para distintos públicos.
- Los datos podrían ser tan distintos que no tendría sentido realizar consultas al mismo tiempo.

También está disponible la recopilación pública de datos previamente enriquecidos {{site.data.keyword.discoverynewsshort}}. Está lista para realizar consultas, para que pueda empezar a crearlas de forma inmediata. No se puede ajustar la configuración ni añadir documentos a {{site.data.keyword.discoverynewsshort}}.

1.  Pulse ![Detalles del entorno](images/env_icon.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> y elija **Crear entorno**.
1.  Una vez que el entorno esté listo, pulse el botón **Cargar sus datos** y, a continuación, puede **Nombrar su nueva recopilación**. Asigne el nombre **InstallDocs** a la recopilación.

    Al crear una recopilación, bajo **Avanzado**, tiene la opción de elegir un archivo de configuración denominado **Configuración de contrato predeterminada**. Esta configuración sólo da soporte al enriquecimiento de Clasificación de elementos, que se puede utilizar para extraer la parte, la naturaleza y la categoría de los elementos en PDF. Consulte [Clasificación de elementos](/docs/services/discovery?topic=discovery-element-classification#element-collection) para obtener más detalles. No elija esta opción para esta guía de aprendizaje.

También puede rastrear los orígenes de datos de Box, Salesforce, Microsoft SharePoint Online, IBM Cloud Object Storage y Microsoft SharePoint 2016, o efectuar un rastreo web con el conjunto de herramientas de {{site.data.keyword.discoveryshort}}. Pulse el botón **Conectar un origen de datos** y consulte [Conexión a orígenes de datos](/docs/services/discovery?topic=discovery-sources#sources) para obtener más información.
{: tip}

## Paso 3: Descargar el documento de ejemplo y cargarlo en su recopilación
{: create-custom-configuration}

1.  Descargue este documento PDF de ejemplo: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/watsonexplorerinstall.pdf" download>Guía de instalación de Watson Explorer <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo" title="Icono de enlace externo"></a>. Consulte [Tipos de documentos soportados](/docs/services/discovery?topic=discovery-sdu#doctypes) para obtener la lista completa de tipos de documentos soportados en {{site.data.keyword.discoveryshort}}. 

    En algunos navegadores, los enlaces se abren en una nueva ventana en lugar de guardarse localmente. Si esto ocurre, seleccione `Guardar como` en el menú `Archivo` de su navegador para guardar una copia del archivo.
    {: tip}

1.  Cargue el documento en la recopilación. Arrástrelo y suéltelo en la recopilación, o bien pulse **examinar desde el sistema** para cargar documentos. Después de completar la carga, se visualiza la siguiente información:
    -  El número de documentos (1).
    -  Los campos identificados en el documento. Debería ver un campo identificado, `texto`. Luego identificaremos más campos.
    -  Enriquecimientos aplicados al documento. {{site.data.keyword.discoveryshort}} aplica automáticamente al campo `texto` los enriquecimientos de Extracción de entidades, Análisis de sentimiento, Clasificación de categorías y Etiquetado de conceptos. Obtenga más información sobre los enriquecimientos [aquí](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)). 
    -  Consultas creadas previamente que se pueden ejecutar de forma inmediata.
1.  Vamos a probar una consulta rápida de lenguaje natural en el nivel establecido. Pulse **Crear su propia consulta** en la parte inferior derecha.
1.  En la pantalla **Crear consultas**, pulse **Buscar documentos** y, a continuación, **Utilizar lenguaje natural**. Especifique `Cuáles son los requisitos mínimos de hardware` y pulse el botón **Ejecutar consulta**. Pulse el separador **JSON** de la derecha. El resultado no es tan preciso como podría ser, así que vamos a mejorarlo con la Comprensión de documentos inteligentes.
1.  Pulse en el nombre de la recopilación (**InstallDocs**) en la parte superior izquierda para volver a la pantalla **Visión general**.  
 
## Paso 4: Anotar el documento
{: #upload-your-documents}

Para obtener más información sobre los documentos anotados, consulte [Comprensión de documentos inteligentes](/docs/services/discovery?topic=discovery-sdu#sdu).
{: tip}

1.  Pulse **Configurar datos** en la parte superior derecha. 
1.  En la pantalla **Configurar datos**, habrá tres separadores: **Identificar campos**, **Gestionar campos** y **Enriquecer campos**.
1.  Se visualiza la `Guía de instalación de Watson Explorer` y está lista para la anotación en el separador **Identificar campos**. Todos los campos disponibles (`respuesta`, `autor`, `pie-de-página`, `cabecera`, `pregunta`, `subtítulo`, `tabla-de-contenidos`, `texto` y `título`) se visualizan en la lista de **etiquetas de campo** de la derecha. Si ha adquirido un plan Avanzado o Premium, puede crear sus propias etiquetas personalizadas.

    Puesto que el documento completo se identifica actualmente como `texto`, los marcadores de la parte derecha están totalmente en amarillo. A medida que se anota (y el sistema inicia la predicción), los colores se actualizan.
    {: tip}

1.  Pulse `título` y, a continuación, seleccione el marcador situado junto a `Guía de instalación e integración`. Pulse el botón **Enviar página**.
1.  En la vista previa de la página de la izquierda, pulse la página 3. Tenga en cuenta que el `título` ya se ha predicho para esta página. Pulse el botón **Enviar página**.
1.  En la página 4, seleccione la etiqueta `pie-de-página` y seleccione el marcador situado junto al pie de página. Pulse el botón **Enviar página**.
1.  En las páginas 5 y 6, anote los pies de página con la etiqueta `pie-de-página`. Envíe cada página. Pulse varias páginas más; observará que {{site.data.keyword.discoveryshort}} ha predicho correctamente el pie de página. Anote los `títulos` (alineados a la izquierda) y los `subtítulos` (con sangrado) en las páginas 7, 9 y 10 y envíe cada página por separado.
1.  Pulse varias páginas más y compruebe los títulos y los subtítulos predichos. Si necesita realizar algún cambio, anote las páginas y pulse el botón **Enviar página**.
1.  Luego pulse el separador **Gestionar campos** y, en **Mejorar los resultados de la consulta dividiendo los documentos**, divida el documento en función de los `subtítulos`. 
1.  Por ahora, esta anotación debería ser suficiente. Pulse el botón **Aplicar cambios a la recopilación** en la parte superior derecha. Aparecerá un recuadro de diálogo **Cargar los documentos**. Navegue hasta el archivo `watsonexplorerinstall.pdf` original y cárguelo. De este modo, se aplican todas las anotaciones al índice. Una vez finalizada la indexación, se abrirá la pantalla **Visión general**. Ahora debería ver más de 30 documentos y 4 campos identificados a partir de los datos: `pie-de-página`, `subtítulo`, `texto` y `título`. (Si los cambios no se visualizan pasados unos minutos, renueve la ventana del navegador).

    Puede excluir campos (como, por ejemplo, `pie-de-página`) de la indexación abriendo el separador **Gestionar campos** y `desactivando` esos campos.
    {: tip}

## Paso 5: Consultar
{: #build-a-query}

1.  Pulse **Crear su propia consulta** en la parte inferior derecha.
1.  En la pantalla **Crear consultas**, pulse **Buscar documentos** y, a continuación, **Utilizar lenguaje natural**. Especifique `Cuáles son los requisitos mínimos de hardware` y pulse el botón **Ejecutar consulta**. 
1.  Pulse el separador **JSON** de la derecha. Observe el campo de `texto` en los `resultados`. Las respuestas devueltas para la consulta son mucho más precisas.

Recursos adicionales:
-  Para obtener más información sobre el esquema de datos de los documentos, pulse el icono **Ver datos de esquema** en el extremo izquierdo o pulse el separador **JSON**. Consulte el [Esquema de datos de Discovery](/docs/services/discovery?topic=discovery-query-concepts#discovery-schema) para obtener más detalles.
-  Pulse el botón **Utilizar una consulta de ejemplo** para probar consultas de ejemplo escritas en {{site.data.keyword.discoveryshort}} Query Language.

## Pasos siguientes
{: #next-steps-tool}

Ahora tiene una instancia de servicio de {{site.data.keyword.discoveryshort}} cumplimentada y funcional. Ahora puede empezar a personalizar su recopilación añadiendo más documentos y enriquecimientos, y anotando más documentos. Consulte [Comprensión de documentos inteligentes](/docs/services/discovery?topic=discovery-sdu#sdu) para obtener más información.
