---

copyright:
  years: 2015, 2018
lastupdated: "2018-05-21"

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

# Iniciación a la creación de consultas

En esta guía de aprendizaje, vamos a aprender a escribir algunos tipos de consultas en {{site.data.keyword.discoveryshort}}.
{: shortdesc}

Para obtener más información sobre cómo escribir consultas, consulte:
- [Conceptos de consultas](/docs/services/discovery/using.html)
- [Referencia de consultas](/docs/services/discovery/query-reference.html) (incluye la lista de parámetros, operadores y agregaciones disponibles en {{site.data.keyword.discoveryshort}} Query Language)

Estas consultas de ejemplo se crean utilizando el conjunto de herramientas de {{site.data.keyword.discoveryshort}}. Si desea utilizar la API en su lugar, añada los parámetros de consulta a la llamada de la API. Para obtener más información y ejemplos, consulte la sección de Consultas de la [Referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection){: new_window}.

También puede escribir consultas de lenguaje natural (como "IBM Watson partnerships") utilizando el conjunto de herramientas de {{site.data.keyword.discoveryshort}}. Esta guía de aprendizaje se centra primordialmente en escribir consultas con {{site.data.keyword.discoveryshort}} Query Language puesto que sus requisitos podrían requerirle una consulta estructurada, y los filtros y las agregaciones se deben escribir en {{site.data.keyword.discoveryshort}} Query Language.
{: tip}

## Antes de empezar

**Complete los pasos de la [Iniciación al conjunto de herramientas](/docs/services/discovery/getting-started-tool.html). ** Si todavía no ha completado la **Iniciación**, vaya a la pantalla **Gestionar datos**, cree una nueva recopilación denominada {{site.data.keyword.IBM_notm}} Press Releases, y añada estos cuatro documentos a la misma (utilice la **Configuración predeterminada**): <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo" title="Icono de enlace externo" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo" title="Icono de enlace externo" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo" title="Icono de enlace externo" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo" title="Icono de enlace externo" class="style-scope doc-content"></a>

## Paso 1: Inicio rápido para el esquema de datos de Discovery

Primero nos familiarizaremos con el JSON de {{site.data.keyword.discoveryshort}}. Para entender cómo crear una consulta con {{site.data.keyword.discoveryshort}} Query Language, es importante familiarizarse con el JSON que {{site.data.keyword.discoveryshort}} genera después de enriquecer los documentos en su recopilación.

1.  [Inicie el conjunto de herramientas de {{site.data.keyword.discoveryshort}}](/docs/services/discovery/getting-started-tool.html#launch-the-tooling). En la pantalla **Gestionar datos**, elija la recopilación {{site.data.keyword.IBM_notm}} Press Releases.

1.  Revise los conocimientos descubiertos por Watson en sus documentos enriquecidos.

    -  **Sentimientos generales** visualiza un desglose porcentual de los documentos etiquetados como positivos, neutros o negativos según el enriquecimiento del Análisis de sentimiento.
    -  **Entidades principales** visualiza las personas, lugar y organizaciones que el enriquecimiento Extracción de entidades ha descubierto en sus documentos.
    -  **Jerarquía de contenido** visualiza las taxonomías jerárquicas que el enriquecimiento de Clasificación de categorías ha descubierto en sus documentos.
    -  **Conceptos relacionados** visualiza los conceptos que el enriquecimiento Etiquetado de conceptos ha descubierto en sus documentos.

         Pulse **Ver en esquema** en cualquier tarjeta para ver los enriquecimientos que comprenden dichos resultados.
         {: tip}

1.  Para familiarizarse con el esquema de datos de los documentos, consulte la pantalla **Ver esquema de datos**. Esta pantalla visualiza los campos y valores en sus documentos transformados de dos maneras: por documento (**Vista de documentos**) o por campo (**Vista de recopilación**). La **Vista de recopilación** visualizará todos los campos en la recopilación.

    Pulse el botón **Ver esquema de datos**. En la **Vista de recopilación**, bajo `enriched_text`, puede examinar los enriquecimientos aplicados con el archivo de la **Configuración predeterminada**. Pulse en `categories`, `concepts`, `entities` y `sentiment` para cómo la recopilación se enriquece con la información de Watson.

Si su consulta no devuelve ningún resultado coincidente, y piensa que debería hacerlo, intente cambiar el campo/valor que está utilizando la consulta por uno que pueda verificar en el esquema de datos.
{: tip}    

## Paso 2: Cree una consulta básica

Empezaremos escribiendo una consulta que encontrará el concepto `Cloud computing` en la recopilación:

1.  Pulse en el icono de crear consultas ![Icono de consultas](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> para abrir la página de consultas. Seleccione la recopilación que contiene {{site.data.keyword.IBM_notm}} Press Releases y pulse **Empezar**.
1.  En la pantalla **Crear consultas**, pulse **Buscar documentos**, a continuación **Utilizar {{site.data.keyword.discoveryshort}} Query Language** y luego:
    - Pulse el desplegable **Campo** y seleccione `enriched_text.concepts.text`, para **Operador** elija `contiene` y, a continuación, especifique el **Valor** de `Cloud computing`. Se visualizará la consulta `enriched_text.concepts.text:Cloud computing` bajo **Creador de consulta visual**.

    - Como alternativa, puede pulsar **Editar en lenguaje natural** y, a continuación, **Utilizar {{site.data.keyword.discoveryshort}} Query Language**. Especifique `enriched_text.concepts.text:"Cloud computing"` en el campo **Especifique aquí una consulta**.

1.  Pulse **Ejecutar consulta**. Debería haber una coincidencia (`"matching_results": 1`). Copie el **URL de consulta** en la parte superior del separador **Resumen** o **JSON** para utilizar en su aplicación.

**Adicional:** Bajo **Más opciones**, tendrá la opción de activar la recuperación de pasajes con el botón de selección **Incluir pasajes relevantes**. Los pasajes son fragmentos significativos breves que se extraen de los documentos completos que devuelve su consulta. Estos fragmentos específicos se extraen de los campos `text` de los documentos en su recopilación. Consulte [Pasajes](/docs/services/discovery/query-parameters.html#passages) para obtener más información. La recuperación de pasajes no está disponible en la recopilación {{site.data.keyword.discoveryshort}} News.

Si desea comprobar algunas consultas creadas de forma previa, pulse el botón **Utilizar una consulta de ejemplo**.
{: tip}

## Paso 3: Experimente con diferentes consultas

Pruebe estas consultas:

Para recuperar todos los documentos con un sentimiento `positivo`: Pulse **Buscar documentos**, **Utilizar {{site.data.keyword.discoveryshort}} Query Language** y, a continuación:
-  Pulse el desplegable **Campo** y seleccione `enriched_text.sentiment.document.label`, para **Operador** elija `contiene` y, a continuación, especifique el **Valor** de `positive`.  

   Se visualizará la consulta `enriched_text.sentiment.document.label:positive` bajo **Creador de consulta visual**.

Para recuperar todos los documentos en la categoría `health and fitness`: Pulse **Buscar documentos**, **Utilizar {{site.data.keyword.discoveryshort}} Query Language** y, a continuación:
-  Pulse el desplegable **Campo** y seleccione `enriched_text.categories.label`, para **Operador** elija `es` y, a continuación, especifique el **Valor** de `"health and fitness"`.

   Se visualizará la consulta `enriched_text.categories.label::"health and fitness"` bajo **Creador de consulta visual**. El operador `::` especifica una coincidencia exacta.

Para recuperar todos los documentos que contengan la entidad `IBM`, pero que no contengan la entidad `Watson`: Pulse **Buscar documentos**, **Utilizar {{site.data.keyword.discoveryshort}} Query Language** y, a continuación:
-  Pulse el desplegable **Campo** y elija `enriched_text.entities.text`, para el **Operador** elija `contiene` y, a continuación, especifique el **Valor** de `IBM`. Pulse **Añadir regla**, luego para el **Campo** elija `enriched_text.entities.text`, para el **Operador** elija `no contiene` y, a continuación, especifique el **Valor** de `Watson`.

   Se visualizará la consulta `enriched_text.entities.text:IBM,enriched_text.entities.text:!Watson` bajo **Creador de consulta visual**. El operador `:!` especifica "no contiene".

## Paso 4: Crear una consulta combinada

Los parámetros de las consultas se pueden combinar para crear consultas más específicas. Empezaremos utilizando conjuntamente los parámetros `filter` y `query` para recuperar documentos sobre las adquisiciones de {{site.data.keyword.IBM_notm}}. El parámetro de filtro reducirá los resultados a únicamente los documentos que mencionan `IBM` y después el parámetro de consulta query devolverá todos los resultados sobre `acquisitions` ordenados por relevancia.

1.  Pulse en el icono de crear consultas ![Icono de consultas](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> para abrir la página de consultas. Seleccione la recopilación que contiene {{site.data.keyword.IBM_notm}} Press Releases y pulse **Empezar**.

1.  Bajo **Filtrar los documentos que consultará**:
    -  Pulse el desplegable **Campo** y elija `enriched_text.entities.text`, para el **Operador** elija `contiene` y, a continuación, especifique el **Valor** de `IBM`.

       La consulta `enriched_text.entities.text:IBM` reducirá los documentos encontrados a aquellos donde se menciona la entidad `IBM`.

1.  En **Buscar documentos**, pulse **Utilizar {{site.data.keyword.discoveryshort}} Query Language** y, a continuación:
    -  Pulse el desplegable **Campo** y elija `enriched_text.concepts.text`, para el **Operador** elija `contiene` y, a continuación, especifique el **Valor** de `world wide web`.

       La consulta `enriched_text.concepts.text:"world wide web"` devolverá todos los documentos que incluyen el concepto `world wide web`, y dichos documentos se clasificarán por orden de relevancia.

1.  Pulse **Más opciones** y, a continuación, **Campos a devolver** y elija **Especificar**. Seleccione `text`. Esto limitará la respuesta al texto de los artículos relevantes y excluirá todo lo demás.

1.  Pulse **Ejecutar consulta**. Habrá un documento coincidente: `"matching_results": 1`

## Paso 5: Cree una agregación

Las agregaciones devuelven un conjunto de valores de datos, por ejemplo, palabras clave más destacadas, sentimiento general de las entidades, etc.

Intentaremos crear una agregación que devolverá los 10 conceptos más importantes en la recopilación de notas de prensa de {{site.data.keyword.IBM_notm}}.

1.  Pulse en el icono de crear consultas ![Icono de consultas](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> para abrir la página de consultas. Seleccione la recopilación que contiene {{site.data.keyword.IBM_notm}} Press Releases y pulse **Empezar**.

1.  Bajo **Incluir análisis de los resultados**:
    -  Pulse el desplegable **Salida** y elija `Valores superiores`, para el **Campo** elija `enriched_text.concepts.text` y, a continuación, especifique el **Recuento** de `10`.

       `term` devolverá los valores más habituales para el campo `concepts` `text`. **Recuento** especifica el número de resultados que desea obtener. La consulta `term(enriched_text.concepts.text,count:10)` se visualizará bajo **Visual Query Builder**.   

1.  Pulse **Más opciones** y, a continuación, especifique `0` en el campo **Número de documentos a devolver**.

1.  Pulse **Ejecutar consulta**. Se visualizarán los 10 conceptos principales en los separadores **Resumen** y **JSON**. A continuación hay un ejemplo de un resumen:

## Paso 6: Cree una consulta en Watson Discovery News

{{site.data.keyword.discoverynewsshort}}, es un conjunto de datos públicos que se ha enriquecido de forma previa con conocimientos cognitivos. Se incluye con {{site.data.keyword.discoveryshort}}. Consulte [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html#watson-discovery-news) para obtener más información sobre esta recopilación.

No es posible ajustar la configuración de {{site.data.keyword.discoverynewsshort}}, ni realizar tareas de entrenamiento ni tampoco añadir documentos la recopilación de {{site.data.keyword.discoverynewsshort}}. Consulte una demostración que puede realizar con {{site.data.keyword.discoverynewsshort}} [aquí ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://discovery-news-demo.ng.bluemix.net/){: new_window}.

La siguiente consulta de ejemplo devuelve los 10 artículos principales en {{site.data.keyword.discoverynewsfull}} sobre el equipo Pittsburgh Steelers que tienen un sentimiento positivo.

1.  Pulse en el icono de crear consultas ![Icono de consultas](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> para abrir la página de consultas. Seleccione la recopilación {{site.data.keyword.discoverynewsshort}} y pulse **Empezar**. (Para consultar las recopilaciones de {{site.data.keyword.discoverynewsshort}} en español, alemán o coreano, primero debe pulsar en el icono ![Gestionar datos](/images/icon_yourData.png) y seleccionar el idioma adecuado en el desplegable).

1.  En **Buscar documentos**, pulse **Utilizar {{site.data.keyword.discoveryshort}} Query Language** y, a continuación:
    -  Pulse el desplegable **Campo** y elija `text`, para el **Operador** elija `contiene` y, a continuación, especifique el **Valor** de `Pittsburgh Steelers`. Pulse **Añadir regla** y, a continuación el desplegable **Campo** y elija `enriched_text.sentiment.document.label`, para **Operador** elija `contiene` y, a continuación especifique el **Valor** de `positive`.

       La consulta `text:"Pittsburgh Steelers",enriched_text.sentiment.document.label:"positive"` se mostrará en **Creador de consultas visuales**.

1.  Pulse **Más opciones** y, a continuación, especifique `10` (se trata del valor predeterminado) en el campo **Número de documentos a devolver**.

1.  Pulse **Ejecutar consulta**. Se visualizarán los 10 artículos principales sobre el equipo Pittsburgh Steelers con un sentimiento positivo.

**Nota:** El número máximo de resultados devueltos a una consulta de Watson Discovery es de `50`.

Los artículos de noticias a veces se sindican a varios proveedores de noticias, por lo que {{site.data.keyword.discoverynewsfull}} recopilará todas ellas, dando lugar a artículos duplicados. Esto significa que una consulta a {{site.data.keyword.discoverynewsfull}} potencialmente podría dar lugar a varios artículos idénticos o casi idénticos en los resultados de las consultas. Para desactivar la desduplicación, bajo **Más opciones**, elija **Excluir resultados duplicados**. Para obtener más información sobre esta funcionalidad en fase beta, consulte [Exclusión de documentos duplicados en los resultados de las consultas](/docs/services/discovery/query-parameters.html#deduplication).
