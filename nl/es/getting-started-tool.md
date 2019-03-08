---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-18"

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
{:download: .download}

# Iniciación
{: #getting-started}

En esta breve guía de aprendizaje, introduciremos el conjunto de herramientas de {{site.data.keyword.discoveryshort}} y recorreremos el proceso de creación de una recopilación de datos privados en los que buscar.
{: shortdesc}

Si prefiere trabajar en la API, consulte [Iniciación a la API](/docs/services/discovery/getting-started.html).
{: tip}

## Antes de empezar
{: #before-you-begin}

Para poder empezar necesitará una instancia de servicio.

<!-- Remove the text marked `download` after there's no g-s tab in the catalog dashboard -->


Ha creado la instancia de servicio. Pulse **Gestionar** y, a continuación, **Abrir herramienta**. Vaya al [Paso 2](/docs/services/discovery/getting-started-tooling.html#create-a-collection).
{: download tip}

Si ha creado una instancia de servicio de {{site.data.keyword.discoveryshort}}, habrá completado los requisitos previos. Vaya al [Paso 1](/docs/services/discovery/getting-started-tool.html#launch-the-tooling).

1.  Vaya a la página [{{site.data.keyword.discoveryshort}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.{DomainName}/catalog/services/discovery){: new_window} en el catálogo de {{site.data.keyword.Bluemix_notm}}.
1.  Regístrese para obtener una cuenta de {{site.data.keyword.Bluemix_notm}} gratuita o inicie sesión.
1.  Pulse **Crear**.


## Paso 1: Iniciar el conjunto de herramientas
{: #launch-the-tooling}

Después de crear una instancia del servicio de {{site.data.keyword.discoveryshort}}, llegará al panel de control de [{{site.data.keyword.Bluemix_notm}}](https://console.{DomainName}/dashboard). Pulse en la instancia de servicio de {{site.data.keyword.discoveryshort}} para ir al panel de control del servicio de {{site.data.keyword.discoveryshort}}.

En la página **Gestionar**, pulse **Abrir herramienta**.

<!-- To do: Add screenshot for developer console -->

Si se le solicita que inicie sesión en el conjunto de herramientas, proporcione las credenciales de {{site.data.keyword.Bluemix_notm}}.

Si no está en la página de detalles del proyecto para el servicio de {{site.data.keyword.discoveryshort}}, vaya a la página [Proyectos ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.{DomainName}/developer/watson/projects) de {{site.data.keyword.watson}} Developer Console y seleccione el proyecto.
{: tip}

<!-- Remove this text after dedicated instances have the Developer Console: begin -->

{{site.data.keyword.Bluemix_dedicated_notm}}: Seleccione la instancia de servicio en el panel de control para iniciar el conjunto de herramientas.

<!-- Remove this text after dedicated instances have the Developer Console: end -->

## Paso 2: Crear una recopilación
{: #create-a-collection}

El primer paso en el conjunto de herramientas de {{site.data.keyword.discoveryshort}} es crear una recopilación de datos.

Una recopilación es un conjunto de documentos. *¿Por qué querría más de una recopilación?* Hay varias razones:

- Puede que desee varias recopilaciones para separar los resultados para distintos públicos.
- Los datos podrían ser tan distintos que no tendría sentido realizar consultas al mismo tiempo.

También está disponible la recopilación pública de datos previamente enriquecidos {{site.data.keyword.discoverynewsshort}}. Está lista para realizar consultas para que de forma inmediata pueda empezar a crearlas. No se puede ajustar la configuración ni añadir documentos a {{site.data.keyword.discoverynewsshort}}.

1.  Pulse ![Rueda](images/icon_settings.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> y elija **Crear entorno**.
1.  Una vez que el entorno esté listo, pulse el botón **Cargar sus datos** y, a continuación, puede **Nombrar su nueva recopilación**. Dé un nombre a su recopilación y elija la **Configuración predeterminada** en **Seleccionar una configuración para aplicar** (la configuración la podrá cambiar más tarde).

Hay otra configuración disponible denominada **Configuración de contrato predeterminado** que da soporte a la Clasificación de elementos, que se puede utilizar para extraer en PDF la parte, la naturaleza y la categoría de los elementos. Consulte [Clasificación de elementos](/docs/services/discovery/element-classification.html#element-collection) para obtener más detalles.

También puede rastrear orígenes de datos de Box, Salesforce y Microsoft SharePoint Online con el conjunto de herramientas de {{site.data.keyword.discoveryshort}}. Pulse el botón **Conectar un origen de datos** y consulte [Conexión a orígenes de datos](/docs/services/discovery/connect.html) para obtener más información.
{: tip}

## Paso 3: Crear una configuración personalizada
{: create-custom-configuration}

Después de crear su recopilación, podría empezar a cargar contenido de forma inmediata con en el área para la carga de documentos, pero lo que haremos será crear y probar una configuración personalizada.

1.  Pulse **Conmutar** junto al nombre de la recopilación y seleccione **Crear una nueva configuración**. Dé un nombre a la configuración y pulse **Crear**.
1.  Después de crear su configuración, podrá personalizarla:
    1.  Descargue el documento de ejemplo <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo" title="Icono de enlace externo" class="style-scope doc-content"></a>.
    1.  Utilice el panel **Cargar documentos de ejemplo** para cargar el documento de ejemplo. Después de cargarlo, pulse en el enlace del nombre del documento para ver la transformación.
1.  Ahora es cuando ajustaremos la configuración. En esta tarea, cambiaremos los enriquecimientos que se aplican a cada documento:
    1.  Pulse la sección **Enriquecer** de la configuración. Inspeccione el JSON generado a la derecha de la pantalla. Desplácese hacia abajo en la sección *enriched_text* y observe como hay distintos *concepts*.
    1.  A continuación, elimine el enriquecimiento de texto denominado *concepts* pulsando la **X** junto al mismo y, a continuación, **Aplicar y guardar**.
    1.  Por último, consulte de nuevo el JSON. Observe como ha cambiado la salida y ya no incluye *concepts*.

## Paso 4: Cargar los documentos
{: #upload-your-documents}

Cuando esté satisfecho con la conversión personalizada de su documento de ejemplo será el momento de ingerir el contenido real en su recopilación.

1. Descargue estos tres documentos de ejemplo: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo" title="Icono de enlace externo" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo" title="Icono de enlace externo" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo" title="Icono de enlace externo" class="style-scope doc-content"></a>.
1.  Pulse ![Icono de archivo](images/icon_yourData.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> y seleccione su recopilación.
1.  Asegúrese de que la configuración personalizada que ha creado aparece listada bajo **Configuración**. Si no lo es, pulse **Conmutar** junto al nombre de la configuración para seleccionarla.
1.  Pulse el botón **Cargar documentos** y empiece a subir los cuatro documentos de ejemplo: test-doc1.html, test-doc2.html, test-doc3.html, test-doc4.html.
1.  Espere unos segundos para que se complete la carga. El estado de los documentos se visualiza en la sección **Visión general**.

## Paso 5: Crear una consulta
{: #build-a-query}

1.  Pulse ![Icono de consulta](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> para abrir la página de consultas. Seleccione su recopilación y pulse **Empezar**.
1.  En la pantalla **Crear consultas**, pulse **Buscar documentos** y, a continuación, **Utilizar {{site.data.keyword.discoveryshort}} Query Language**:
    - Para buscar resultados con entidades denominadas "IBM":
        1.  Pulse **Campo** y seleccione `enriched_text.entities.text`. Seleccione `contiene` para el **Operador** e `IBM` para el **Valor**. La consulta `enriched_text.entities.text:IBM` se visualiza en el **Creador de consulta visual**.
        1.  Pulse **Ejecutar consulta**. La consulta devuelve 4 resultados.
    - Para buscar resultados con las entidades denominadas "Watson":
        1.  Pulse **Campo** y seleccione `enriched_text.entities.text`. Seleccione `contiene` para el **Operador** y `watson` para el **Valor**. La consulta `enriched_text.entities.text:watson` se visualiza en el **Creador de consultas visuales**.
        1.  Pulse **Ejecutar consulta**. La consulta devuelve dos resultados.
    - Para buscar resultados con las entidades denominadas "Watson" y "Slack":
        1.  Pulse **Campo** y seleccione `enriched_text.entities.text`. Seleccione `contiene` para el **Operador** y `watson` para el **Valor**. Pulse **Añadir regla** y a continuación, repita las selecciones, pero elija el **Valor** de `Slack`. Se visualiza la consulta `enriched_text.entities.text:watson,enriched_text.entities.text:Slack` en el **Creador de consultas visuales**.
        1.  Pulse **Ejecutar consulta**. La consulta devuelve 1 resultado.

    Pulse **Editar en lenguaje de consulta** para crear consultas con {{site.data.keyword.discoveryshort}} Query Language. Para obtener más información sobre {{site.data.keyword.discoveryshort}} Query Language, consulte [Referencia de consultas](/docs/services/discovery/query-reference.html) y [Conceptos de consultas](/docs/services/discovery/using.html).
1.  Los resultados de la consulta se visualizan en la sección **Resultados**:
    - El separador **Resumen** proporciona una visión general de los resultados de la consulta.
    - El separador **JSON** muestra los resultados de JSON completos.

    Para las consultas listadas, **Resumen** visualiza en primer lugar los pasajes del documento (en orden de relevancia), seguidos por los nombres de los documentos encontrados y, a continuación, los resultados del enriquecimiento. Los **Pasajes** son fragmentos significativos breves que se extraen de los documentos completos que devuelve su consulta.

    En enlace **URL de consulta** que se proporciona bajo los separadores **JSON** y **Resumen** está listo para ser utilizado en su aplicación.

    También puede pulsar **Utilizar lenguaje natural** y escribir una consulta de lenguaje natural como, por ejemplo, "IBM Watson partnerships". Para obtener más información sobre las consultas en lenguaje natural, consulte [Consulta de lenguaje natural](/docs/services/discovery/query-parameters.html#nlq).

    Se puede entrenar a Watson para mejorar los resultados de las consultas de lenguaje natural. Consulte [Mejora de la relevancia de los resultados con el conjunto de herramientas](/docs/services/discovery/train-tooling.html).

    Recursos adicionales:
    - Para obtener más información sobre el esquema de datos de los documentos, pulse el icono **Ver datos de esquema** o pulse el separador **JSON**. Consulte [El esquema de datos de Discovery](/docs/services/discovery/using.html#discovery-schema) para obtener más detalles.
    - Si está editando en {{site.data.keyword.discoveryshort}} Query Language, pulse los iconos **?** junto a cualquiera de los campos **Especifique aquí una consulta** para ver más ejemplos.

## Pasos siguientes
{: #next-steps}

Ahora tiene una instancia de servicio de {{site.data.keyword.discoveryshort}} cumplimentada y funcional. Ahora puede empezar a personalizar su recopilación añadiendo más documentos y enriquecimientos, y personalizar los valores de conversión.
