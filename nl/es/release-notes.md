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

# Notas del release
{: #release-notes}

Las notas del release proporcionan información sobre los cambios en el servicio {{site.data.keyword.discoveryfull}} desde el release anterior.
{: shortdesc}

## Versiones de la API del servicio
{: #apiversioning}

Las solicitudes de API requieren un parámetro de versión que toma una fecha en el formato `version=AAAA-MM-DD`. Siempre que cambiamos la API de forma que sea incompatible con versiones anteriores, ponemos a su disposición una versión inferior de la API.

Envíe el parámetro version con cada solicitud de API. El servicio utiliza la versión de la API correspondiente a la fecha que especifique, o la versión más reciente anterior a dicha fecha. No especifique como valor predeterminado la fecha actual. En su lugar, especifique una fecha que coincida con una versión que sea compatible con su app y no la modifique hasta que la app esté lista para una versión posterior.

La versión actual es `01-01-2019`.

## Características beta
{: #beta-features}

IBM lanzará servicios, características y soporte de idiomas que se clasifican como beta o experimental. Estas funcionalidades pueden ser inestables, pueden cambiar frecuentemente, y pueden ser suspendidas con poca antelación. Se proporcionan para que los usuarios puedan evaluar su funcionalidad. Una funcionalidad beta o experimental podría no proporcionar el mismo nivel de rendimiento o compatibilidad que el que proporcionan las funcionalidades disponibles de forma general. Estas funcionalidades no están diseñadas para su uso en un entorno de producción, y si lo hace es bajo su cuenta y riesgo.


## Cambios
{: #change-log}

Están disponibles los siguientes cambios y características nuevas del servicio.

## 10 de febrero de 2019
{: #10feb19}

- Se ha añadido la opción de conectarse y sincronizarse con IBM Cloud Object Storage. Este origen de datos no está disponible en entornos Dedicados. Consulte [IBM Cloud Object Storage](/docs/services/discovery?topic=discovery-sources#connectcos) para obtener más información.

## 4 de febrero de 2019
{: #4feb19}

Actualizado a la disponibilidad general:

-  La [comprensión de documentos inteligentes (SDU)](/docs/services/discovery?topic=discovery-sdu#sdu) se ha movido del estado beta al estado de disponibilidad general (GA).
   -  La anotación de tabla permanece en estado beta. Encontrará una explicación de las características beta que puede encontrar [aquí](/docs/services/discovery?topic=discovery-release-notes#beta-features).
   -  El botón `Valores de datos` de la parte superior derecha se ha renombrado a `Configurar datos`.
   -  La carga de un documento ya no es necesaria para acceder al botón `Configurar datos` (antes `Valores de datos`).

La versión beta de SDU se anunció el [22 de enero de 2019](/docs/services/discovery?topic=discovery-release-notes#22jan19).   
    
## 28 de enero de 2019
{: #28jan19}

Ya no se proporciona asistencia para Data Crawler si lo está utilizando con un origen de datos soportado por los conectores de {{site.data.keyword.discoveryshort}}. Los conectores de {{site.data.keyword.discoveryshort}} soportan el rastreo de Box, SharePoint y Salesforce, entre otros. Consulte [Conexión a orígenes de datos](/docs/services/discovery?topic=discovery-sources#sources) para obtener más información. Data Crawler solo debe utilizarse para rastrear comparticiones de archivos o bases de datos, en todos los demás casos, utilice el conector de {{site.data.keyword.discoveryshort}}. Otra opción para cargar un gran número de archivos en {{site.data.keyword.discoveryshort}} es [discovery-files ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/IBM/discovery-files){: new_window} en GitHub.

## 22 de enero de 2019
{: #22jan19}

- Se ha publicado la versión beta de la función de [comprensión de documentos inteligentes (SDU)](/docs/services/discovery?topic=discovery-sdu#sdu), una nueva forma de entrenar {{site.data.keyword.discoveryfull}} para extraer campos personalizados en los documentos. La comprensión de documentos inteligentes permite anotar campos dentro de los documentos para entrenar modelos de conversión personalizados. Encontrará una explicación de las características beta que puede encontrar [aquí](/docs/services/discovery?topic=discovery-release-notes#beta-features).

El editor de la versión beta de SDU solo está disponible para las nuevas recopilaciones que contienen tipos de documento soportados y no tienen aplicado el enriquecimiento de Clasificación de elementos. Las recopilaciones privadas existentes utilizarán el método de configuración original.

Si ha participado en la fase beta cerrada de la función de comprensión de documentos inteligentes, no importe en esta versión los modelos creados en dicha versión beta. Actualmente, la comprensión de documentos inteligentes no está disponible en entornos Dedicados.

Las funciones del editor de SDU sólo están disponibles en el conjunto de herramientas de {{site.data.keyword.discoveryshort}}, no están disponibles en la API.

## 15 de enero de 2019
{: #15jan19}

Actualizaciones de Clasificación de elementos:
-  En el enriquecimiento de Clasificación de elementos, se han actualizado las partes, las categorías y los atributos en la versión de API `2018-10-15` o posterior. Consulte las actualizaciones en [Análisis de contratos](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing).

- La salida del método `/v1/element_classification` ahora incluye lo siguiente:
    - La matriz `parties` incluye un campo `importance` que indica si una parte es `Primary` o `Unknown` (no primaria).
    - Las matrices `effective_dates`, `contract_amounts` y `termination_dates` incluyen un campo `confidence_level` que indica un valor `High`, `Medium` o `Low`.
    Para obtener más información, consulte [Clasificación de elementos](/docs/services/discovery?topic=discovery-output_schema#output_schema) y [Análisis de contratos](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing).

    El conjunto de herramientas de {{site.data.keyword.discoveryshort}} todavía no utiliza la versión actual de la API: `2019-01-01` (actualmente utiliza `2018-08-01`), de modo que no verá estos nuevos campos en la salida de Clasificación de elementos en el conjunto de herramientas de {{site.data.keyword.discoveryshort}}.

## 10 de enero de 2019
{: #10jan19}

Problema conocido:

-  Si especifica un `customer-id` mediante el método de normalización descrito en [Especificación de `customer_id`](/docs/services/discovery?topic=discovery-sources#source_customer_id) y luego intenta suprimir documentos que contienen ese `customer_id` mediante el método descrito aquí: [Supresión de datos etiquetados](/docs/services/discovery?topic=discovery-information-security#deletingdata), el documento de origen asociado no se suprime.

## 1 de enero de 2019
{: #1jan19}

- La serie de versión de todas las llamadas de API ha cambiado de `2018-12-03` a `2019-01-01`. Esta versión introduce un nuevo estado de ingestión de documento: `pending`. Se devolverá el estado `pending` para los documentos que se han aceptado, pero aún no se han empezado a procesar. Anteriormente, estos documentos tenían el estado `processing`. El conjunto de herramientas de {{site.data.keyword.discoveryshort}} todavía no utiliza esta versión de la API (actualmente utiliza `2018-08-01`), de modo que no se devolverá el estado `pending` cuando compruebe el estado del documento en el conjunto de herramientas de {{site.data.keyword.discoveryshort}}.

## 21 de diciembre de 2018
{: #21dec18}

- Se ha añadido la opción de conectarse y sincronizarse con Microsoft SharePoint 2016 On-Premise. Este origen de datos no está disponible en entornos Dedicados. Consulte [SharePoint 2016 On-Premise](/docs/services/discovery?topic=discovery-sources#connectsp_op) para obtener más información.

- Se ha añadido la versión beta del conector de rastreo web, que se puede utilizar para conectarse y sincronizarse con sitios web, y para rastrearlos. Este origen de datos no está disponible en entornos Dedicados. Consulte [Rastreo web](/docs/services/discovery?topic=discovery-sources#connectwebcrawl) para obtener más información. Encontrará una explicación de las características beta que puede encontrar [aquí](/docs/services/discovery?topic=discovery-release-notes#beta-features).

- Los orígenes de datos de Microsoft SharePoint Online, Salesforce y Box están ahora disponibles en entornos Premium. No están disponibles en entornos Dedicados.

## 17 de diciembre de 2018
{: #17dec18}

- Se ha añadido soporte completo para el italiano. Para obtener más información, consulte [Soporte de idiomas](/docs/services/discovery?topic=discovery-language-support#language-support).

## 14 de diciembre de 2018
{: #14dec18}

Ahora puede crear instancias de servicio de {{site.data.keyword.discoveryshort}} alojadas en el centro de datos de Londres sin sindicación. Al igual que todas las ubicaciones, la ubicación de Londres (eu-gb) de {{site.data.keyword.cloud}} utiliza la autenticación de IAM (Identity and Access Management) basada en señales. Todas las nuevas instancias de servicios que cree en esta ubicación utilizan la autenticación de IAM.

## 12 de diciembre de 2018
{: #12dec18}

- Se ha añadido la capacidad de definir y cargar una lista de palabras vacías personalizadas. Las palabras vacías personalizadas se implementan con la API de {{site.data.keyword.discoveryshort}}. Consulte [Definición de palabras vacías](/docs/services/discovery?topic=discovery-query-concepts#stopwords) para obtener más detalles. 

## 3 de diciembre de 2018
{: #3dec18}

- Para todas las consultas (con la excepción de las consultas de sólo filtro) escritas utilizando la versión de la API `2018-12-03` o superior, {{site.data.keyword.discoveryshort}} devolverá ahora una puntuación de `confidence` en el conjunto de resultados de la consulta, incluso si la recopilación no se ha entrenado mediante un método de entrenamiento supervisado como, por ejemplo, [Entrenamiento de relevancia](//docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling) o [Entrenamiento de relevancia continuo](/docs/services/discovery?topic=discovery-crt#crt). Además, {{site.data.keyword.discoveryshort}} devolverá un campo `document_retrieval_strategy` que indica el origen de la puntuación de `confidence`: `untrained`, `relevancy_training` o `continuous_relevancy_training`. Para obtener más información, consulte [Puntuaciones de confianza](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence).

- La serie de versión de todas las llamadas de API ha cambiado de `2018-10-15` a `2018-12-03`. El conjunto de herramientas de {{site.data.keyword.discoveryshort}} todavía no utiliza esta versión de la API (actualmente utiliza `2018-08-01`), por lo que las consultas escritas mediante el conjunto de herramientas de {{site.data.keyword.discoveryshort}} no devolverán una puntuación de `confidence` para las recopilaciones no entrenadas.

## 8 de noviembre de 2018
{: #8nov18}

- Se lanza {{site.data.keyword.discoveryshort}} en la región de `Tokio` el 8 de noviembre de 2018. Los entornos Premium y Dedicados actualmente no están disponibles en `Tokio`.

## 30 de octubre de 2018
{: #30oct18}

- El servicio {{site.data.keyword.discoveryshort}} ahora da soporte a la autenticación de IAM (Identity and Access Management) basada en señales en todas las regiones. IAM utiliza las señales de acceso en lugar de las credenciales de servicio en la autenticación con un servicio. Para obtener más información sobre cómo utilizar señales IAM con aplicaciones nuevas, consulte la actualización del release del [17 de mayo de 2018](#17May18).

## 25 de octubre de 2018
{: #25oct18}

El esquema del enriquecimiento de [Clasificación de elementos](/docs/services/discovery?topic=discovery-element-classification#element-classification) se ha modificado. Si desea utilizar el esquema actualizado, debe ingerir los documentos con la API utilizando la fecha de versión `2018-10-15` o posterior. El conjunto de herramientas de {{site.data.keyword.discoveryshort}} todavía no utiliza esta versión de la API (actualmente utiliza `2018-08-01`), por lo que los documentos ingeridos mediante el conjunto de herramientas de {{site.data.keyword.discoveryshort}} se enriquecerán con el esquema original.

## 24 de octubre de 2018
{: #24oct18}

- Las consultas de {{site.data.keyword.discoverynewsfull}} muestran aproximadamente 50 palabras de cada artículo en el campo JSON `text`. Estas palabras ahora se extraerán de los aspectos más destacados, en lugar de limitarse a mostrar las primeras 50 palabras del artículo. Consulte [aspectos destacados](/docs/services/discovery?topic=discovery-query-parameters#highlight) para obtener una explicación de los aspectos destacados. Para habilitar este comportamiento, no es necesario incluir de forma explícita los aspectos destacados en la consulta.

## 25 de septiembre de 2018
{: #25sept18}

- Se ha lanzado el entrenamiento de relevancia continuo, que utiliza interacciones de usuarios para aprender a emerger los resultados más relevantes. Puede aprender del comportamiento del usuario de forma automática, lo que reduce significativamente el esfuerzo necesario para mejorar la clasificación de resultados de relevancia.  Consulte [Entrenamiento de relevancia continuo](/docs/services/discovery?topic=discovery-crt#crt) para obtener detalles.

- Se ha añadido soporte de API para realizar consultas más largas. Esto aumenta el límite de caracteres a 10.000 y hace posible aumentar el número de filtros en las consultas y realizar agregaciones más complejas. Observe la consulta POST en [Referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery#long-collection-queries){: new_window} y [Referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery#long-environment-queries){: new_window} para obtener detalles.

- Ahora puede actualizar el plan Avanzado mediante la API. Consulte [Actualización del plan](/docs/services/discovery?topic=discovery-upgrading-your-plan#switchadvanced) para obtener detalles. 

- El enriquecimiento Clasificación de elementos ha actualizado los elementos clasificados, los elementos de contrato y las partes y tablas identificadas. Consulte [Clasificación de elementos](/docs/services/discovery?topic=discovery-element-classification#element-classification) para ver actualizaciones.

- Se ha añadido soporte completo para el portugués de Brasil. Para obtener más información, consulte [Soporte de idiomas](/docs/services/discovery?topic=discovery-language-support#language-support).

- La API de consulta (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`) ahora ofrece soporte al parámetro `bias`, que le permite inclinarse hacia determinados resultados; por ejemplo, documentos que se han publicado más recientemente. Consulte el método [Consultar su recopilación ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery#query-your-collection){: new_window} en la referencia de API para obtener más información.

- El archivo **Configuración de contrato predeterminada** que se proporciona para enriquecer recopilaciones para la [Clasificación de elementos](/docs/services/discovery?topic=discovery-element-classification#element-collection) parece tener un problema con las normalizaciones de HTML. Se ha incluido una **Configuración de contrato predeterminada** nueva con este release. Siga los pasos siguientes para aplicar la nueva **Configuración de contrato predeterminada** a sus recopilaciones.

     1. Determine cuáles de sus recopilaciones están utilizando el archivo de configuración **Configuración de contrato predeterminada** o una configuración personalizada basada en la **Configuración de contrato predeterminada**.
     1. Anote los cambios que ha realizado en cualquier configuración personalizada basada en la **Configuración de contrato predeterminada**.
     1. Puesto que el archivo de **Configuración de contrato predeterminada** debe suprimirse del entorno antes de poder usar uno nuevo, utilice la API [Suprimir configuración ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery#delete-a-configuration){: new_window} para suprimir la **Configuración de contrato predeterminada** asociada con cualquiera de sus recopilaciones. Suprima también las configuraciones basada en la **Configuración de contrato predeterminada** antigua.
     1. Ahora puede utilizar el nuevo archivo de **Configuración de contrato predeterminada**. Cree una nueva recopilación para cada recopilación que utilice alguna de estas configuraciones. Aplique la nueva **Configuración de contrato predeterminada** o cree una nueva configuración personalizada basada en la nueva **Configuración de contrato predeterminada** utilizando las notas que ha tomado en el paso 2.
     1. Cargue los archivos que ha ingerido previamente en las recopilaciones originales.
     1. Suprima las recopilaciones antiguas.

## 15 de agosto de 2018
{: #15aug18}

- Hay dos nuevos operadores de consulta disponibles. `Exists` (`:*`) se puede utilizar para devolver todos los resultados en los que existe el campo `field` especificado. `Does not exist` (`!*`) se puede utilizar para devolver todos los resultados que no incluyen el campo `field` especificado. Consulte [Operadores de consulta](/docs/services/discovery?topic=discovery-query-operators#query-operators) para obtener más información. 

## 2 de agosto de 2018
{: #2aug18}

- {{site.data.keyword.discoveryfull}} ahora ofrece soporte a las recopilaciones en inglés, español, alemán, italiano, portugués, francés, árabe, coreano y japonés al conectarlas y sincronizarlas con Box, Salesforce y SharePoint Online con el conjunto de herramientas de {{site.data.keyword.discoveryshort}}. 

## 31 de julio de 2018
{: #31jul18}
 
 - A partir del **1 de agosto de 2018**, {{site.data.keyword.discoveryfull}} tiene una nueva estructura de precios. Cuenta con un modelo de precios más sencillo (las horas de documento ya no forman parte del cálculo) y con precios por niveles en las consultas de {{site.data.keyword.discoverynewsfull}}. Además, el plan Estándar se ha retirado y el plan Lite ha reducido los límites de consulta de {{site.data.keyword.discoverynewsshort}} y documentos. Los cambios de precio no necesitarán que los usuarios de {{site.data.keyword.discoverynewsshort}} realicen ninguna acción. Consulte [Planes de precios de {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans) para obtener detalles.
 
**Nota:** La fecha de versión de la API se ha actualizado a `2018-08-01`. Para aprovechar las nuevas opciones de dimensionamiento del nuevo entorno (`LT`, `XS`, `S`, `MS`, `M`, `ML`, `L`, `XL`, `XXL`, `XXXL`), debe utilizar esta fecha de versión al crear entornos con la API. Los tamaños entorno ahora tienen el tipo `string` (anteriormente el tipo era `integer`).

## 27 de julio de 2018
{: #27jul18}

- Se ha publicado [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news) en un nuevo idioma: Japonés (`collection_id`: `news-ja`). {{site.data.keyword.discoverynewsfull}} también está disponible en inglés, español, alemán y coreano.

## 25 de junio de 2018
{: #25jun18}

- Se ha añadido la opción de conectarse y sincronizarse con los orígenes de datos de Salesforce, Microsoft SharePoint Online y Box. Estos orígenes de datos no están disponibles en entornos Premium. Se han liberado las API [Credencial de origen ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery#list-credentials){: new_window} y [Configuración ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery#add-configuration){: new_window} para los orígenes de datos. 
  - {{site.data.keyword.discoveryfull}} solo ofrece soporte a las recopilaciones en inglés al conectarse y sincronizarse a Box, Salesforce y SharePoint Online con el conjunto de herramientas de {{site.data.keyword.discoveryshort}}. [Resuelta](/docs/services/discovery?topic=discovery-release-notes#2aug18)
  - El límite de tamaño del archivo de documento individual para Box, Salesforce y SharePoint Online es 10MB.
- Se ha añadido un nuevo panel de control de rendimiento en el conjunto de herramientas de {{site.data.keyword.discoveryshort}}. Consulte [Visualización de métricas y mejora de los resultados de consulta con el panel de control de rendimiento](/docs/services/discovery?topic=discovery-performance-dashboard#performance-dashboard). El nuevo panel de control no está disponible en los entornos Premium o Dedicado.
- Se ha añadido soporte completo para el japonés. Para obtener más información, consulte [Soporte de idiomas](/docs/services/discovery?topic=discovery-language-support#language-support).

## 22 de junio de 2018
{: #22jun18}

- Se ha liberado la API Sucesos y comentarios. Consulte la [referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery#create-event){: new_window} para obtener más información.

## 11 de junio de 2018
{: #11jun18}

-  Para las aplicaciones alojadas en Washington, DC (EE.UU. este), el servicio ahora ofrece soporte a la autenticación de Gestión de acceso e identidades (IAM) basada en señales. IAM utiliza las señales de acceso en lugar de las credenciales de servicio en la autenticación con un servicio. Para obtener más información sobre cómo utilizar señales IAM con aplicaciones nuevas, consulte la actualización del release del [17 de mayo de 2018](#17May18).
-  Ahora se ofrece soporte a un elemento de contrato adicional en la Clasificación de elementos: `Protección y seguridad`. Consulte [Comprensión de los elementos de contrato](/docs/services/discovery?topic=discovery-element-classification#contract-elements) para obtener detalles.

## 6 de junio de 2018
{: #6jun18}

- Las consultas de {{site.data.keyword.discoverynewsfull}} ahora muestran las 50 primeras palabras de cada artículo en el campo JSON `text`. [Actualizar](#24oct18)

## 5 de junio de 2018
{: #5jun18}

- La Clasificación de elementos ahora está disponible para aquellos suscritos a los planes Premium.
- La calificación `assurance` de `Low` ya no está disponible en la clasificación de elementos.

## 31 de mayo de 2018
{: #31may18}

- Se ha añadido soporte completo para el francés. Para obtener más información, consulte [Soporte de idiomas](/docs/services/discovery?topic=discovery-language-support#language-support).

## 30 de mayo de 2018
{: #30may18}

- Se ha corregido un problema conocido en {{site.data.keyword.discoverynewsfull}}. Anteriormente, al consultar {{site.data.keyword.discoverynewsshort}} era posible recibir un recuento de documentos incorrecto, puesto que los documentos de otros idiomas se cuentan en función del idioma que ha solicitado. Esto ya no es así.
- A partir de recopilaciones creadas a partir del `22 de mayo de 2018`, {{site.data.keyword.discoveryshort}} devuelve resultados de consulta que incluyen caracteres especiales para los idiomas siguientes: inglés, alemán, francés, holandés, italiano y portugués. Por ejemplo, si consulta `aqui`, ahora recibirá resultados para `aqui` y <code>aqu&iacute;</code>.

## 21 de mayo de 2018
{: #21may18}

- Se ha liberado [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news) en un nuevo idioma: alemán (`collection_id`: `news-de`). {{site.data.keyword.discoverynewsfull}} también está disponible en inglés, español y coreano.

## 17 de mayo de 2018
{: #17May18}

- Las consultas de {{site.data.keyword.discoverynewsfull}} ahora muestran solo las 20 primeras palabras de cada artículo en el campo JSON `text`.

-   El servicio ahora ofrece soporte al nuevo proceso de autenticación de API para instancias de servicio de aplicaciones alojadas en Sídney (**au-syd**) a partir del 15 de mayo de 2018. Pronto se habilitarán en aplicaciones alojadas en otras regiones. {{site.data.keyword.Bluemix}} están en proceso de migración a la autenticación de Gestión de acceso e identidades (IAM) basada en señales. IAM utiliza las señales de acceso en lugar de las credenciales de servicio en la autenticación con un servicio.

   En la ubicación de Sídney, utilice las señales de acceso de IAM con el servicio de {{site.data.keyword.discoveryshort}} para

    -   *Nuevas instancias de servicio* que cree a partir del 15 de mayo. Para obtener más información, consulte [Autenticación con señales de IAM](/docs/services/watson/getting-started-iam.html).
    -   *Instancias de servicio existentes* que migra desde Cloud Foundry a un grupo de recursos gestionado por el controlador de recursos (RC). Las instancias de servicio creadas antes del 15 de mayo siguen utilizando credenciales de servicio para la autenticación hasta que las migre. Para obtener más información, consulte [Migración de instancias de servicio de Cloud Foundry a un grupo de recursos](/docs/resources/instance_migration.html).

    Todas las instancias de servicio nuevas y existentes en otras regiones siguen utilizando las credenciales de servicio (`apikey:{apikey_value}`) para la autenticación.

### Utilización de una señal de acceso de IAM para la autenticación
{: #iam-token}

Al utilizar señales de acceso de IAM realiza la autenticación antes de enviar una solicitud al servicio de {{site.data.keyword.discoveryshort}}.

1.  Obtenga una clave de API de IBM Cloud. Utilice esta clave para generar una señal de acceso de IAM. Para obtener más información, consulte [Cómo obtener una señal de IAM utilizando la clave de API de servicio de {{site.data.keyword.watson}}](/docs/services/watson/getting-started-iam.html#iamtoken).
1.  Pase la señal de acceso de IAM al servicio de {{site.data.keyword.discoveryshort}} mediante la cabecera `Autorización`. En la cabecera, indique que la señal de acceso es una señal `Bearer` especificando `Authorization: Bearer {access_token}`.

    El siguiente ejemplo de cURL simple utiliza una señal de acceso:

    ```bash
    curl -X GET
    --header "Authorization: Bearer eyJhbGciOiJIUz......sgrKIi8hdFs"
    "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    Para obtener más información, consulte [Utilización de una señal para la autenticación](/docs/services/watson/getting-started-iam.html#use_token).

### Actualización de una señal de acceso de IAM
{: #iam-refreshing}

Las señales de acceso de IAM que genera tienen la estructura siguiente. Utilice el valor del campo `access_token` para realizar una solicitud autenticada al servicio.

```javascript
{
  "access_token": "eyJhbGciOiJIUz......sgrKIi8hdFs",
  "refresh_token": "SPrXw5tBE3......KBQ+luWQVY=",
  "token_type": "Bearer",
  "expires_in": 3600,
  "expiration": 1473188353
}
```
{: codeblock}

Las señales de acceso tiene un tiempo de vida limitado. El campo `expires_in` indica cuánto tiempo durará la señal; en este caso una hora. El campo `expiration` muestra la fecha y hora de UNIX en que caduca la señal, que especifica el número de segundos a partir del 1 de enero de 1970 (medianoche UTC/GMT).

En la aplicación, compruebe la hora de caducidad de la señal de acceso antes de utilizara para realizar una solicitud autenticada. Si ha caducado, debe actualizar la señal de acceso antes de poder utilizarla. Utilice el valor del campo `refresh_token` para actualizar la señal de acceso. Para obtener más información, consulte [Actualización de una señal](/docs/services/watson/getting-started-iam.html#refresh_token).


## 11 de mayo de 2018
{: #11may18}

- Aquí encontrará detalles sobre la seguridad de la información [Seguridad de la información](/docs/services/discovery?topic=discovery-information-security#information-security).
- El siguiente problema conocido de `query_entities` de {{site.data.keyword.discoveryfull}} Knowledge Graph se ha arreglado con la actualización de la versión de la API del `2018-05-04`. Este arreglo solo se aplica a entidades ingeridas o sustituidas a partir del `04-05-2018`. Las entidades se pueden sustituir mediante la reingestión de documentos antiguos o la ingestión de nuevos documentos que contengan dichas entidades. Si las entidades antiguas no se han reemplazado, `query_entities` devolverá todo el caso en mayúsculas con la versión de la API `04-05-2018`.
  - Todos los nombres de entidades se han convertido previamente en bicapitalización en `query_entities`. Por ejemplo, el nombre de entidad "IBM Corporation" se ha convertido a "Ibm Corporation". Esto ya no es así.

## 9 de mayo de 2018
{: #9may18}

- Los documentos de muestra ahora se almacenan de forma local en la carpeta de datos roaming local de su navegador. Para obtener más información sobre los documentos de ejemplo, consulte [Carga de documentos de ejemplo](/docs/services/discovery?topic=discovery-configservice#uploading-sample-documents).

## 4 de mayo de 2018
{: #4may18}

- Ahora se ofrece soporte a dos elementos de contrato adicionales en Clasificación de elementos: Atributos y procedencia. Consulte [Comprensión de los elementos de contrato](/docs/services/discovery?topic=discovery-element-classification#contract-elements) para obtener detalles.

## 26 de abril de 2018
{: #26apr18}

- Se ha corregido el siguiente problema de ingestión; En algunos casos en los que se han especificado los valores `json_normalizations` y `normalizations` posteriores al enriquecimiento, es posible que las normalizaciones se hayan aplicado en el orden incorrecto. Esto puede dar como resultado que los documentos se indexen con valores de campo no esperado. Esto ya no es así.
- Ahora el tamaño de archivo máximo para un documento de ejemplo es 1MB. Anteriormente, el tamaño de archivo máximo era 5MB.

## 12 de abril de 2018
{: #12apr18}

- Knowledge Graph: [Pruebas](/docs/services/discovery?topic=discovery-kg#kg_evidence) y [Canonicalización y filtrado](/docs/services/discovery?topic=discovery-kg#kg_canonicalization) ahora están disponibles en todas las recopilaciones. En las recopilaciones creadas antes del `03-05-2018`, debe volver a ingerir los documentos para utilizar estas características. Anteriormente, era necesario crear una nueva recopilación y volver a ingerir los documentos.

## 11 de abril de 2018
{: #11apr18}

- Ahora se ofrece soporte a dos categorías adicionales en Clasificación de elementos: `Uso de activos` y `Comunicación`. Consulte [Comprensión de los elementos de contrato](/docs/services/discovery?topic=discovery-element-classification#contract-elements) para obtener detalles.

## 2 de abril de 2018
{: #2apr18}

- Los documentos de ejemplo ahora se suprimen automáticamente pasadas 24 horas, en lugar de 1 mes después.

## 16 de marzo de 2018
{: #16mar18}

- Se ha añadido soporte completo para el alemán. Para obtener más información, consulte [Soporte de idiomas](/docs/services/discovery?topic=discovery-language-support#language-support).

Conjunto de herramientas de {{site.data.keyword.discoveryshort}}:
- Se ha añadido una nueva configuración denominada **Configuración de contrato predeterminada** para ofrecer soporte a la Clasificación de elementos, que se puede utilizar para extraer en PDF la parte, la naturaleza y la categoría de elementos. Consulte [Clasificación de elementos](/docs/services/discovery?topic=discovery-element-classification#element-collection) para obtener más detalles.

Actualizado a la disponibilidad general:
- La segmentación de la documentación se ha movido del estado beta al estado de disponibilidad general (GA). El límite de segmentación ha aumentado a 250 segmentos. Ya no está limitado a 50 segmentos por documento. Consulte [Segmentación de la documentación](/docs/services/discovery?topic=discovery-configservice#doc-segmentation) para obtener detalles.

Problema conocido:
- Los comodines no funcionan con consultas que contienen letras mayúsculas. Por ejemplo, dado el par de clave/campo `{"borrower": "GOVERNMENT OF INDIA"}`, `query-borrower:*ndia` devolverá resultados, `query-borrower:*NDIA` no lo hará.

## 8 de marzo de 2018
{: #8mar18}

- La versión beta de {{site.data.keyword.discoveryfull}} Knowledge Graph ha añadido varias características. Durante el release beta, la funcionalidad [Knowledge Graph](/docs/services/discovery?topic=discovery-kg#kg) y los métodos asociados a la misma solo están disponibles para instancias de servicio suscritas a los planes **Avanzado**, **Premium** y todos los entornos **Dedicados**. Las nuevas características son:
  - [Similitud de entidades](/docs/services/discovery?topic=discovery-kg#kg_similarity)
  - [Pruebas](/docs/services/discovery?topic=discovery-kg#kg_evidence)
  - [Canonicalización y filtrado](/docs/services/discovery?topic=discovery-kg#kg_canonicalization)

## 7 de marzo de 2018
{: #7mar18}

- Se ha corregido el siguiente problema de ingestión conocido: Entre el 28 de febrero y el 6 de marzo, se indexó un pequeño porcentaje de documentos con los campos `id` y `extracted_metadata` (no se indexó ningún otro contenido de documento). El problema subyacente se ha solucionado, aunque deberá volver a enviar los documentos afectados para su ingestión. No hay una forma sencilla de identificar los documentos afectos.

## 5 de marzo de 2018
{: #5mar18}

- El siguiente problema conocido de {{site.data.keyword.discoveryfull}} Knowledge Graph se ha arreglado en la actualización de la versión de la API `05-03-2018`. Este arreglo solo se aplica a las recopilaciones recién creadas que utilizan la actualización de la versión `05-03-2018`.  
  - Todos los nombres de tipo de entidad y tipo de relación se han convertido previamente a mayúsculas durante la ingestión. Por ejemplo, la entidad "GeoPoliticalEntity" se ha convertido a "GEOPOLITICALENTITY," y la relación "partOf" se ha convertido a "PARTOF". Esto ya no es así.

## 1 de marzo de 2018
{: #1mar18}

- Los limites de la [expansión de consulta](/docs/services/discovery?topic=discovery-query-concepts#query-expansion) han aumentado en los planes Avanzado y Premium a 5.000 expansiones de consulta y 25.000 términos totales. Consulte [Planes de precios de Discovery](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans) para obtener detalles.

## 28 de febrero de 2018
{: #28feb18}

- Los enriquecimientos de {{site.data.keyword.alchemylanguageshort}} han pasado a estar en desuso el **1 de marzo de 2018**. Para obtener información sobre la migración de recopilaciones y de archivos de configuración que utilizan los enriquecimientos de {{site.data.keyword.alchemylanguageshort}}, consulte [Migración de enriquecimientos a {{site.data.keyword.nlushort}}](/docs/services/discovery?topic=discovery-migrate-nlu#migrate-nlu).

## 23 de febrero de 2018
{: #23feb18}

- Se ha añadido la capacidad de realizar consultas por similitud de documento. Puede consultar documentos similares por id de documento y, opcionalmente, detallar más la similitud especificando los campos. Consulte [Similitud de documento](/docs/services/discovery?topic=discovery-query-concepts#doc-similarity) para obtener más información.

- Se ha mejorado el [parámetro `highlight`](/docs/services/discovery?topic=discovery-query-parameters#highlight) en los resultados de consulta. Los resultados de consulta devolverán las frases completa ordenadas por su `puntuación`.

## 21 de febrero de 2018
{: #21feb18}

- Anteriormente, al ingerir documentos PDF, se devolvía `file_type` cuando se consultaban los avisos de ingestión en el objeto `extracted_metadata` y la API de los detalles de documento era `html`. Esto ya no es así. El `file_type` devuelto ahora será `pdf`. 

## 26 de enero de 2018
{: #26jan18}

Conjunto de herramientas de {{site.data.keyword.discoveryshort}}:

- Se ha añadido la capacidad de acceder a las recopilaciones en coreano y español en el mosaico de [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news) en el conjunto de herramientas. Anteriormente, estas recopilaciones solo se podían consultar a través de la API.

## 23 de enero de 2018
{: #23jan18}

- Se ha añadido la capacidad de ampliar el ámbito de una consulta; por ejemplo, puede expandir la consulta de "coche" para incluir "automóvil" y "vehículo de motor". Además, puede sustituir términos con errores ortográficos comunes, por ejemplo, puede sustituir consultas de "seabizcuit" con "seabiscuit". La expansión de consulta se ha implementado con la API de {{site.data.keyword.discoveryshort}}. Consulte [Expansión de consulta](/docs/services/discovery?topic=discovery-query-concepts#query-expansion) para obtener detalles.  

## 15 de enero de 2018
{: #15jan18}

- {{site.data.keyword.discoverynewsfull}} Original se ha retirado del servicio. Se sustituyó el 31 de julio de 2017 por una nueva versión denominada {{site.data.keyword.discoverynewsfull}}. Para obtener instrucciones sobre cómo migrar de {{site.data.keyword.discoverynewsfull}} Original a la nueva versión, consulte [Migración desde Watson Discovery News Original](/docs/services/discovery?topic=discovery-migrate-bwdn#migrate-bwdn).

## 11 de enero de 2018
{: #11jan18}

- Se ha añadido soporte completo para el coreano. Para obtener más información, consulte [Soporte de idiomas](/docs/services/discovery?topic=discovery-language-support#language-support).

## 15 de diciembre de 2017
{: #15dec17}

- Se lanza el enriquecimiento **Clasificación de elementos**, que analiza elementos (frases, listas, tablas) en documentos normativos para clasificar tipos y categorías. Consulte [Clasificación de elementos](/docs/services/discovery?topic=discovery-element-classification#element-classification) para obtener más información. La Clasificación de elementos no está disponible para instancias de servicio suscritas al plan **Premium**. [Resuelta](/docs/services/discovery?topic=discovery-release-notes#5jun18)
- Añadido el soporte de idioma básico para el holandés y el chino (simplificado). Consulte [Soporte de idiomas](/docs/services/discovery?topic=discovery-language-support#language-support) para obtener más información. Actualmente, las recopilaciones en holandés y chino (simplificado) se deben crear con la API.
- Se han añadido dos nuevos parámetros al Rastreador de datos: `proxy_host_port` y `read-timeout`. Consulte [Configuración de Data Crawler](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-the-data-crawler) para obtener detalles.
- Es posible encontrar los siguientes problemas al ingerir documentos PDF: [Resuelto](/docs/services/discovery?topic=discovery-release-notes#21feb18)
  - Cuando se consultan los avisos de ingestión, el campo `file_type` para documentos pdf se devuelve como `html`.
  - El campo `file_type` en el objeto `extracted_metadata` de resultados para los documentos pdf se establece en `html`.
  - La API de detalles de documento también devuelve el campo `file_type` para documentos pdf como `html`.
- Si ingiere JSON, las matrices de tipo mixto no se soporta.  

Conjunto de herramientas de {{site.data.keyword.discoveryshort}}:

- Se ha añadido un creador de consultas visual para la versión beta de {{site.data.keyword.discoveryfull}} Knowledge Graph. Consulte [Consultas de Knowledge Graph utilizando el conjunto de herramientas de {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-kg#querying-kg)

## 30 de noviembre de 2017
{: #30nov17}

- Se lanza la versión beta de {{site.data.keyword.discoveryfull}} Knowledge Graph, que proporciona nuevos puntos finales para consultar entidades y relaciones entre documentos. Incluye búsquedas basadas en el contexto y clasificación según la relevancia. Esta característica beta solo está disponible para los usuarios del plan **Advanced**. No está disponible en los entornos **Dedicados**. [Resuelto](/docs/services/discovery?topic=discovery-release-notes#8mar18) Consulte [{{site.data.keyword.discoveryfull}} Knowledge Graph](/docs/services/discovery?topic=discovery-kg#kg) para obtener más información.  Encontrará una explicación de las características beta que puede encontrar [aquí](/docs/services/discovery?topic=discovery-release-notes#beta-features).
  - Problema conocido en {{site.data.keyword.discoveryfull}} Knowledge Graph: Todos los nombres de tipo de entidad y nombres de tipo de relación se pasan a mayúsculas durante la ingestión. Por ejemplo, la entidad "GeoPoliticalEntity" se convierte en "GEOPOLITICALENTITY," y la relación "partOf" se convierte en "PARTOF." [Resuelta](/docs/services/discovery?topic=discovery-release-notes#5mar18)
- Se lanza [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news) en dos nuevos idiomas: coreano (`icollection_id`: `news-ko`) y español (`collection_id`: `news-es`). La recopilación {{site.data.keyword.discoverynewsfull}} en coreano y en español está disponible únicamente para ser utilizada a través de la API. Para obtener información sobre cómo consultar una recopilación a través de la API, consulte [Referencia de ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery#query-your-collection){: new_window} [Resuelta](/docs/services/discovery?topic=discovery-release-notes#26jan18). {{site.data.keyword.discoverynewsfull}} en inglés ahora tiene el `collection_id` `news-en`. Con anterioridad, el `collection_id` era `news`. Si ha estado utilizando el anterior `collection_id`, continuará funcionando, sin embargo, debería cambiar al nuevo `collection_id` para nuevos proyectos.
- Los resultados de las consultas devuelven un valor de `score`, que indica la relevancia relativa entre resultados de consulta. Desde el 30 de noviembre de 2017, se ha cambiado la forma en la que se calcula `score`. El valor de `score` únicamente se debería utilizar para clasificar documentos en una única búsqueda, no a través de búsquedas o sesiones. Si ha entrenado una recopilación, se devuelve un valor de `score` en los resultados de una consulta de lenguaje natural. Puesto que `score` indica una relevancia entre resultados de una consulta, no se debería utilizar como un umbral. En su lugar, utilice `confidence`, que indica la relevancia del resultado comparado respecto al modelo entrenado por lo que permite establecer umbrales. Consulte [Puntuaciones de confianza](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence) para obtener más información sobre cómo establecer umbrales.
- A partir de este release, la recuperación de pasajes detecta límites de frases, es decir, intenta recuperar pasajes que empiezan al principio de una frase y que acaban en la misma. Con anterioridad, muchos pasajes empezaban o finalizaban en medio de las frases. Consulte [Pasajes](/docs/services/discovery?topic=discovery-query-parameters#passages) para obtener más información sobre la recuperación de pasajes.

## 15 de noviembre de 2017
{: #15nov17}

Conjunto de herramientas de {{site.data.keyword.discoveryshort}}:

- Se ha añadido el enriquecimiento [Extracción de relaciones](/docs/services/discovery?topic=discovery-configservice#relation-extraction), que incluye la opción de incorporar un modelo de relaciones personalizado que se haya creado con {{site.data.keyword.knowledgestudiofull}}.
- El conjunto de herramientas de {{site.data.keyword.discoveryshort}} del enriquecimiento [Extracción de entidades](/docs/services/discovery?topic=discovery-configservice#entity-extraction) ahora incluye la opción de incorporar un modelo de entidades personalizado creado con {{site.data.keyword.knowledgestudiofull}}.
- Se ha eliminado la opción de crear una recopilación en japonés del conjunto de herramientas de {{site.data.keyword.discoveryshort}}, sin embargo permanece la opción para crearla en la API de {{site.data.keyword.discoveryshort}}.
- El conjunto de herramientas de {{site.data.keyword.discoveryshort}} ahora da soporte a entornos sindicados.

## 10 de noviembre de 2017
{: #10nov17}

Conjunto de herramientas de {{site.data.keyword.discoveryshort}}:

- Se han añadido opciones adicionales a la recuperación de pasajes en el conjunto de herramientas de {{site.data.keyword.discoveryshort}}. Al realizar consultas, ahora puede especificar los campos sobre los que extraer pasajes, el número de pasajes a devolver y el recuento máximo de caracteres de cada pasaje. Consulte [Pasajes](/docs/services/discovery?topic=discovery-query-parameters#passages) para conocer los límites, mínimos y máximos.

## 8 de noviembre de 2017
{: #8nov17}

La serie de versión de todas las llamadas de API se ha cambiado a `2017-11-07` (la anterior era `2017-10-16`). Esta versión:
- `score` en cada resultado de consulta se ha trasladado a un nuevo objeto denominado `result_metadata`.
- Si se entrenó la recopilación consultada, y la consulta es una consulta de lenguaje natural, `result_metadata` incluirá un campo `confidence` que visualizará la puntuación de confianza del resultado. Consulte [Puntuaciones de confianza](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence) para obtener más información.
- Los campos que se incluyan espacios en blanco (por ejemplo: `body.additional lectura`) serán ignorados durante la ingestión. La descripción `notices` indicará que `El campo 'additional reading' no es válido: espacios en blanco, '.', '#' y ',' no son válidos en un nombre de campo`.
- El campo `result_metadata` será ignorado durante la ingestión.

## 16 de octubre de 2017
{: #16oct17}

- La serie de versión de todas las llamadas de API se ha cambiado a `2017-10-16` (la anterior era `2017-09-01`). En esta versión pasa a estar en desuso el soporte para cargar nuevos documentos en recopilaciones existentes enriquecidas con los enriquecimientos de {{site.data.keyword.alchemylanguageshort}} y crear nuevas recopilaciones para enriquecerlas con nuevos enriquecimientos de {{site.data.keyword.alchemylanguageshort}}. Las recopilaciones enriquecidas existentes con {{site.data.keyword.alchemylanguageshort}} se deberían migrar a los enriquecimientos de {{site.data.keyword.nlushort}} lo antes posible. Consulte [Migración de enriquecimientos a {{site.data.keyword.nlushort}}](/docs/services/discovery?topic=discovery-migrate-nlu#migrate-nlu) para obtener más detalles. El conjunto de herramientas de {{site.data.keyword.discoveryshort}} también utiliza la versión `2017-10-16`, consulte más abajo para obtener más información.

Conjunto de herramientas de {{site.data.keyword.discoveryshort}}:

- El conjunto de herramientas de {{site.data.keyword.discoveryshort}} utiliza la serie de versión de API `2017-10-16`, por lo que si está utilizando el conjunto de herramientas, ya no podrá cargar documentos en recopilaciones de {{site.data.keyword.alchemylanguageshort}} existentes o crear nuevas recopilaciones enriquecidas con enriquecimientos de {{site.data.keyword.alchemylanguageshort}} después del `2017-10-16`.  Si desea continuar utilizando el conjunto de herramientas de {{site.data.keyword.discoveryshort}} para el enriquecimiento de recopilaciones, migre primero dichas recopilaciones a {{site.data.keyword.nlushort}}. Consulte [Migración de enriquecimientos a {{site.data.keyword.nlushort}}](/docs/services/discovery?topic=discovery-migrate-nlu#migrate-nlu) para obtener más detalles.
- El **Explorador de esquema de datos** visualiza consultas de ejemplo para varios enriquecimientos en la recopilación de {{site.data.keyword.discoverynewsfull}}. Ahora también tiene un enlace **Mostrar más valores** que visualizará valores de ejemplo adicionales para dicho enriquecimiento en {{site.data.keyword.discoverynewsfull}}.
- Se han introducido varias mejoras de productividad, entre otras, la combinación de estadísticas, errores y avisos y otros conocimientos sobre los datos de las recopilaciones en la pantalla **Gestionar datos**.
- Se ha añadido un mensaje que visualiza una alerta cuando ha finalizado el proceso de los documentos.

## 9 de octubre de 2017
{: #9oct17}

- En la API hay disponible una métrica de agregación: `unique_count`. Devolverá un recuento de las instancias exclusivas del campo especificado en una recopilación. Consulte [unique_count](/docs/services/discovery?topic=discovery-query-aggregations#unique_count) para obtener más información.

Conjunto de herramientas de {{site.data.keyword.discoveryshort}}:

- Ahora el **Creador de consulta visual** de soporte a las agregaciones de histogramas de valores (histogram) y de tiempo (timeslice). También existe la posibilidad de activar la detección de anomalías para las consultas de histogramas temporales (timeslice).
- El **Explorador de esquema de datos** visualiza consultas de ejemplo del enriquecimiento elegido. Ahora también tiene un enlace **Mostrar más valores" que visualizará valores de ejemplo adicionales para dicho enriquecimiento.
- Se ha añadido un menú hamburguesa para hacer más rápida la navegación a **Gestionar datos**, **Ver esquema de datos** y **Crear consultas**.

### 3 de octubre de 2017
{: #3oct17}

- Ahora está disponible la segmentación de documentos. Consulte [División de documentos con segmentación de documento](/docs/services/discovery?topic=discovery-configservice#doc-segmentation).

### 29 de septiembre de 2017
{: #29sept17}

- Se lanza {{site.data.keyword.discoveryshort}} en la ubicación `Alemania` el 29 de septiembre de 2017. Con el propósito de cumplir las regulaciones de datos de la Unión Europea, no se da soporte a los enriquecimientos de AlchemyLanguage en esta ubicación.
- Problema conocido: los campos de consulta no pueden contener espacios en blanco.  Al escribir una consulta en {{site.data.keyword.discoveryshort}}, si un campo de consulta contiene espacios en blanco (por ejemplo `body.additional reading`), recibirá un `400: Error de sintaxis de consulta no válida`. [Resuelta](/docs/services/discovery?topic=discovery-release-notes#8nov17)

### 25 de septiembre de 2017
{: #25sept17}

- Ahora hay disponible el plan de precios Premium. Para obtener más información, consulte [Planes de precios de {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans).
- Se ha añadido la posibilidad de consultar, listar campos y consultar avisos a través de recopilaciones dentro del mismo entorno. Consulte [Consulta a varias recopilaciones](/docs/services/discovery?topic=discovery-query-concepts#multiple-collections) para más detalles.
- La información de soporte de idiomas para {{site.data.keyword.discoveryshort}} está disponible en [Soporte de idiomas](/docs/services/discovery?topic=discovery-language-support#language-support)

Conjunto de herramientas de {{site.data.keyword.discoveryshort}}:
- El Creador de consulta visual ha pasado de un estado beta a un estado de disponibilidad general (GA). Actualmente no se da soporte a las agregaciones de filtro, histograma por tiempo (timeslice) e histograma de valores (histogram) con el Creador de consultas visuales. Pulse **Incluir análisis de los resultados** y, a continuación, **Editar en Query Language** en la pantalla **Crear consultas** para escribir estas agregaciones.
- Se ha añadido la funcionalidad beta para la desduplicación en las consultas de {{site.data.keyword.discoverynewsfull}}.
- Además de recopilaciones para el idioma inglés, alemán y español, ahora es posible crear recopilaciones para el árabe, francés, italiano, coreano, japonés y portugués (Brasil).
- Problema conocido: El conjunto de herramientas de {{site.data.keyword.discoveryshort}} no da soporte a los entornos sindicados. [Resuelta](/docs/services/discovery?topic=discovery-release-notes#15nov17)

### 14 de septiembre de 2017
{: #14sept17}

Conjunto de herramientas de {{site.data.keyword.discoveryshort}}:

- Se ha añadido el Explorador de esquema de datos, que muestra los campos y valores en los documentos transformados. Esta información puede utilizarse para comprender la estructura de datos de la recopilación antes de crear consultas utilizando Discovery Query Language. El esquema de datos pueden verse dos maneras: por documento (vista de documento) o por campo (vista de recopilación). Para acceder al Explorador de esquema de datos: en la pantalla **Mis conocimientos de datos**, pulse el botón **Ver esquema de datos** o pulse a la izquierda el icono **Ver esquema de datos**.

### 6 de septiembre de 2017
{: #6sept17}

- Se ha añadido la funcionalidad de desduplicación de documentos devueltos por las consultas. Esta característica beta funciona tanto para recopilaciones privadas como para recopilaciones de Watson Discovery News. Consulte [Exclusión de documentos duplicados en los resultados de las consultas](/docs/services/discovery?topic=discovery-query-parameters#deduplication) para más detalles.

Actualmente sólo se da soporte a la desduplicación de documentos como una funcionalidad beta. Consulte la declaración con relación a las funcionalidades beta en la parte superior del producto para más información.

### 31 de agosto de 2017
{: #31aug17}

- La serie de versión de todas las llamadas de API se ha cambiado a `2017-09-01` (la anterior era `2017-08-01`). Esta versión incluye actualizaciones que eliminarán los siguientes campos JSON no válidos durante la vista previa y la ingestión de forma que únicamente se ingerirán campos JSON válidos. Actualice su versión de serie a `2017-09-01` para evitar conflictos y posibles errores.

   - `id`, `score` y `highlight` a nivel superior (Puede continuar añadiendo documentos a su recopilación utilizando ID de documento con la función `add a document`. Consulte la [Referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery#add-a-document){: new_window} para obtener más detalles.
   - Nombres de campo con el prefijo `_` en el nivel superior (como consecuencia de esto, al consultar un documento por ID, puede consultar por `id` en lugar de `_id`).
   - `#` y `,` en el nombre de campo
   - Nombres de campo con prefijos `+` y `-`
   - Valores vacíos `"` `"` para un nombre de campo

**Nota:** Si sus documentos JSON incluyen estos caracteres en los nombres de campo, o `id`, `score` y `highlight` a nivel superior, necesitará eliminarlos antes de añadir los documentos a la recopilación, o dichos campos quedarán vacíos. Puede crear una configuración personalizada y normalizar el JSON antes de añadir documentos a su recopilación para evitar este problema. Consulte [Configuración personalizada](/docs/services/discovery?topic=discovery-configservice#custom-configuration).  Además, los documentos que incluyen los caracteres de puntuación `?`, `:` o `#` en el nombre del archivo originarán errores en al ser ingeridos. Renombre todos los documentos que incluyan estos caracteres antes de ingerirlos.

- Los métodos de recuperación para `natural_language_query` se han actualizado para mejorar la relevancia de los resultados para encontrar coincidencia de palabras con semánticas relacionadas. Esta actualización sólo afecta a recopilaciones en las que no se ha realizado entrenamiento de relevancia. Si está utilizando `natural_language_query` y no ha llevado a cabo un entrenamiento de relevancia, puede obtener una mejora en el orden de los resultados devueltos.

Conjunto de herramientas de {{site.data.keyword.discoveryshort}}:

- Se ha cambiado el creador de consultas para facilitar la conmutación entre las opciones de consulta de Discovery Query Language y de lenguaje natural, así como con las opciones de consultas, filtro y agregación.


### 25 de agosto de 2017
{: #25aug17}

- La matriz `passages` ahora incluye `field`, `start_offset` y `end _offset`. `field` corresponde al nombre del campo a partir del que se extrae el pasaje. `start_offset` es el carácter de inicio del texto del pasaje dentro del campo. `end_offset` es el carácter de fin del texto del pasaje dentro del campo.

Conjunto de herramientas de {{site.data.keyword.discoveryshort}}: Esta mejora para la creación de consultas se puede encontrar en la pantalla **Crear consultas**.

-  Se ha añadido la funcionalidad beta para escribir consultas en {{site.data.keyword.discoveryshort}} Query Language con un creador de consultas de tipo visual. Pulse **Crear en modalidad visual** en las secciones **Buscar documentos** y **Limitar los documentos a consultar** para probarlo.  A medida que crea su consulta de forma visual, se visualizará en **{{site.data.keyword.discoveryshort}} Query Language** por debajo.

   El creador de consultas visual está soportado únicamente como una funcionalidad beta. Consulte la declaración con relación a las funcionalidades beta en la parte superior del producto para más información.

### 18 de agosto de 2017
{: #18aug17}

Conjunto de herramientas de {{site.data.keyword.discoveryshort}}:

- Se ha añadido el soporte para condiciones y agregaciones anidadas para el creador de agregación visual beta que se introdujo el [11 de agosto de 2017](/docs/services/discovery?topic=discovery-release-notes#11aug17). Hay un límite de 3 condiciones por fila de agregación.

   El creador de agregación visual está soportado únicamente como una funcionalidad beta. Consulte la declaración con relación a las funcionalidades beta en la parte superior del producto para más información.

### 11 de agosto de 2017
{: #11aug17}

Conjunto de herramientas de {{site.data.keyword.discoveryshort}}:

Ambas características son mejoras en la creación de consultas y se pueden encontrar en la pantalla **Crear consultas**.

- Se ha añadido la opción para seleccionar una consulta de un conjunto de consultas y agregaciones de ejemplo creadas de forma previa. Pulse **Utilizar una consulta de ejemplo** en la parte superior derecha para acceder a la lista. Si está consultando una recopilación de datos privada, los ejemplos utilizan `top entities`, `categories`, etc. encontradas en la recopilación. Estas consultas se pueden utilizar como un punto de partida para escribir sus propias consultas. Las consultas de ejemplo están disponibles tanto para recopilaciones privadas como de {{site.data.keyword.discoverynewsfull}}.

-  Se ha añadido la funcionalidad beta para escribir agregaciones con un creador visual. Pulse **Crear en modalidad visual** por encima del campo **Escribir una consulta de agregación utilizando {{site.data.keyword.discoveryshort}} Query Language** para probar esta funcionalidad.  A medida que crea su agregación de forma visual, la consulta se visualizará en **{{site.data.keyword.discoveryshort}} Query Language** por debajo.  

   El creador de agregación visual está soportado únicamente como una funcionalidad beta. Consulte la declaración con relación a las funcionalidades beta en la parte superior del producto para más información.

### 31 de julio de 2017
{: #31jul17}

- Se lanzado una nueva versión de {{site.data.keyword.discoverynewsfull}}. El nombre de la versión original se cambió a {{site.data.keyword.discoverynewsfull}} Original. Esta versión ha sido retirada con una eliminación desde la fecha de servicio del **15 de enero del 2018**. Consulte [Migración desde Watson Discovery News Original](/docs/services/discovery?topic=discovery-migrate-bwdn#migrate-bwdn) para obtener las instrucciones de migración.
  **Nota:** Si ha creado una nueva instancia de {{site.data.keyword.discoveryshort}}, sólo tendrán acceso a la nueva versión de {{site.data.keyword.discoverynewsfull}}.

- Se ha lanzado un nuevo plan de precios para {{site.data.keyword.discoveryfull}}. Consulte [Planes de precios de {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans) para obtener detalles.

- La serie de versión de todas las llamadas de API se ha cambiado a `2017-08-01` (la anterior era `2017-07-19`). Esta versión incluye actualizaciones para el nuevo plan de precios y la nueva versión de Watson Discovery News. Actualice la serie de versión para evitar conflictos y posibles errores.

### 19 de julio de 2017
{: #19jul17}

 - Como parte del cambio en los precios que se anunció para el 1 de agosto de 2017, los usuarios que actualmente están en el plan en desuso de **30 días gratuitos de prueba** serán migrados de forma automática al plan **Lite**. Como resultado de esta transición, los usuarios existentes pueden haber alcanzado o superado el límite del plan con relación a los documentos _(2000)_, almacenamiento _(200Mb)_ o número de recopilaciones _(2)_. Si ha excedido el límite del plan **Lite**, no podrá añadir contenido adicional en el servicio, aún así, podrá seguir realizando consultas a las recopilaciones. Puede ver el estado actual de todos estos límites mediante el conjunto de herramientas de {{site.data.keyword.discoveryshort}} o la API. Para poder reanudar la adición de contenido a la instancia de {{site.data.keyword.discoveryshort}}, debe decidir entre:
   - eliminar recopilaciones y/o documentos de forma que no se superen los límites del plan **Lite**.
     Los documentos se pueden suprimir de forma individual a través de la API con el método [delete-doc](https://{DomainName}/apidocs/discovery#delete-a-document) o se pueden suprimir todas las recopilaciones con el conjunto de herramientas o la API utilizando el método [delete-collection](https://{DomainName}/apidocs/discovery#delete-a-collection)
   - actualice su plan a un nivel que satisfaga sus necesidades de almacenamiento.
 - Los clientes con entornos de tamaño **`1`** **`2`** o **`3`** serán migrados de forma automática al plan **Advanced**.

### 17 de julio de 2017
{: #17jul17}

 - Las siguientes funcionalidades han pasado de un estado beta a un estado de disponibilidad general (GA):

   - Entrenamiento de relevancia
   - Consulta de lenguaje natural
   - Resaltado

 - A partir de este release, {{site.data.keyword.discoveryfull}} está cambiando su mecanismo de enriquecimiento desde {{site.data.keyword.alchemylanguageshort}} a {{site.data.keyword.nlushort}}. {{site.data.keyword.alchemylanguageshort}} está en el proceso de caer en desuso, por lo que debería empezar a utilizar {{site.data.keyword.nlushort}} tan pronto como sea posible.  Consulte [Migración desde los enriquecimientos de {{site.data.keyword.alchemylanguageshort}} a {{site.data.keyword.nlushort}}](/docs/services/discovery?topic=discovery-migrate-nlu#migrate-nlu) para obtener más detalles.
   **Nota:** Al integrar con Watson Knowledge Studio, todavía se tiene que seguir utilizando la configuración de enriquecimiento de {{site.data.keyword.alchemylanguageshort}}. Consulte [Integración con {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-with-wks) para más detalles.

 - La serie de versión de todas las llamadas de API se ha cambiado a `2017-07-19` (la anterior era `2017-06-25`). Esta versión habilita la configuración predeterminada de NLU en la creación de recopilaciones. Todavía podrá enriquecer con {{site.data.keyword.alchemylanguageshort}} en versiones previas.

    La configuración predeterminada se ha actualizado para utilizar {{site.data.keyword.nlushort}}. Debería actualizar la serie de versión lo antes posible para evitar conflictos y posibles errores.

 - Conjunto de herramientas de Discovery:

    Las Tarjetas de conocimiento para las recopilaciones enriquecidas con enriquecimientos de {{site.data.keyword.alchemylanguageshort}} ya no se actualizarán de forma automática. Debe migrar su recopilación a los enriquecimientos de {{site.data.keyword.nlushort}} para que se actualicen las tarjetas de conocimiento.

    Si ha creado una recopilación con anterioridad al **18 de julio de 2017** y aplicó la **Configuración predeterminada**, dicha recopilación se enriqueció con los enriquecimientos de {{site.data.keyword.alchemylanguageshort}}. Si aplica la **Configuración predeterminada** a una recopilación después de esta fecha, se utilizarán los enriquecimientos de {{site.data.keyword.nlushort}} (el nombre de configuración cambiará a **Configuración predeterminada con NLU** en el conjunto de herramientas). Puesto que los enriquecimientos de {{site.data.keyword.alchemylanguageshort}} van a pasar a estar en desuso, no se deberían utilizar con nuevas recopilaciones.

### 30 de junio de 2017
{: #30jun17}

 -  La funcionalidad de normalización de entidades que se introdujo como una característica beta el 5 de mayo de 2017 pasa a estar disponible de forma general (GA). Consulte [Creación de una configuración personalizada para normalizar entidades](/docs/services/discovery?topic=discovery-normalizing-entities-cc#normalizing-entities-cc) para más detalles.

### 23 de junio de 2017
{: #23jun17}

 - La serie de versión de todas las llamadas de API se ha cambiado a `2017-06-25` (la anterior era `2016-12-01`). La nueva serie de versión habilita enriquecimientos en alemán (`de`) o español (`es`) si el idioma de una recopilación se establece en uno de dichos idiomas. Anteriormente, todos los enriquecimientos se realizaban en inglés independientemente del valor del idioma de la recopilación.

    Si solo utiliza enriquecimientos en inglés, puede continuar utilizando la serie de versión `2016-12-01`. Sin embargo, debería actualizar la serie de versión lo antes posible para evitar posibles conflictos.

 - La detección de anomalías ahora está disponible como parte de las agregaciones `timeslice` como una funcionalidad de disponibilidad general (GA). Consulte [Detección de anomalías en timeslice](/docs/services/discovery?topic=discovery-query-aggregations#anomaly-detection) para más detalles.

 - Conjunto de herramientas de Discovery:

   - Se ha añadido la funcionalidad beta para mejorar la relevancia de los resultados de las consultas utilizando el conjunto de herramientas de Discovery (conjunto de herramientas de relevancia). Consulte [Mejora de la relevancia de los resultados de las consultas con el conjunto de herramientas de Discovery](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling).

### 19 de junio de 2017
{: #19jun17}

  - Conjunto de herramientas de Discovery:

    - Se ha añadido la opción para especificar el idioma inglés, español o alemán de los documentos en una nueva recopilación. Para utilizarlo, elija **Seleccionar el idioma de los documentos** en el diálogo **Nombrar a su nueva recopilación**.

    - Se ha añadido el separador **Resumen** a la pantalla **Crear consultas**. El separador **Resumen** visualiza una visión general de los resultados de consulta completos que se proporcionan en el separador **JSON** existente. La pantalla **Resumen** variará con base a sus consultas y los enriquecimientos. La información que se puede visualizar incluye: ID o nombre de documento, estadísticas de agregación, pasajes de documento en orden de relevancia y resultados por enriquecimiento.

    - Se ha añadido la opción de Consulta de lenguaje natural en la pantalla **Crear consultas**. Para utilizarla, pulse **Realizar una pregunta en lenguaje simple** en la sección **Buscar documentos**. Aparecerá un campo donde podrá especificar su pregunta. Ahora podrá acceder al campo de la consulta original (con anterioridad denominada **Especificar una consulta o palabra clave**) pulsando el botón **Utilizar Discovery Query Language**.

    - Se ha rediseñado la pantalla **Crear consultas**, sin embargo, todos los campos y opciones permanecen. A continuación se indican los nombres anteriores y los nuevos nombres de los campos.

| **Nombre de campo anterior**                                           | **Nuevo nombre de campo o sección**                                                                                             |
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| Escribir y ejecutar una consulta                                    | Búsqueda de documentos                                                                                                  |
| Reducir los resultados de la consulta (Filtrar)                       | Limitar los documentos a consultar                                                                                       |
| Agrupar resultados de consulta (Agregación)                        | Incluir análisis de los resultados                                                                                      |
| Campos a visualizar                                        | El nombre no ha cambiado, pero se ha ubicado en la nueva sección de **Personalizar opciones de visualización**.                                      |
| Número de documentos a devolver (Recuento)                    | Número de documentos a devolver [Este campo se ha ubicado en la sección **Personalizar opciones de visualización**].                    |
| Incluir pasajes coincidentes                                | Incluir pasajes relevantes [Este campo se ha ubicado en la sección **Personalizar opciones de visualización**].                        |
| Número de campos de consulta para omitir al principio (Desplazamiento) | Número de resultados de consulta a omitir al principio [Este campo se ha ubicado en la sección **Personalizar opciones de visualización**]. |

### 5 de junio de 2017
{: #5jun17}

 - Las consultas de Watson Discovery News ahora solo visualizan las primeras 150 palabras de cada artículo en los campos JSON `text` y `alchemyapi_text`. El campo `blekko.snippet` únicamente visualizará la primera frase de la matriz de fragmentos.

### 30 de mayo de 2017
{: #30may17}

 - El parámetro `passages` en la API de consulta ha pasado de un estado beta a un estado de disponibilidad general (GA).

### 25 de mayo de 2017
{: #25may17}

 - Conjunto de herramientas de Discovery: En este release se ha añadido el resaltado de campos de consulta. Esta característica añade un resaltado amarillo a los nombres de campo en el JSON del panel Resultados. Todos los campos de consulta o filtro se resaltan en cada resultado incluso si el contenido del campo no coincide con el de la consulta. También se resaltan en los resultados de las consultas los campos utilizados en agregaciones, pero únicamente se resalta la primera operación de agregación.

### 10 de mayo de 2017
{: #10may17}

 - Ahora los métodos `query` y `notices` dan soporte al parámetro `highlight`. El parámetro es un booleano. Cuando se ejecuta una consulta y se especifica `highlight` con `true`, el servicio devuelve la salida que incluye un nuevo campo `highlight` en el que palabras que coinciden con la consultan se delimitan con etiquetas HTML `*` (énfasis). Consulte [Parámetros de consulta](/docs/services/discovery?topic=discovery-query-parameters#highlight) para obtener más información.

 - Es posible que la supresión de un entorno únicamente se complete de forma parcial, dando lugar a una situación en la que el nuevo entorno no se pueda crear debido a que sólo se permite un solo entorno por servicio. Si intenta suprimir y, a continuación, crear un entorno pero alguna de estas operaciones queda invariable en un estado `pendiente`, es probable que se haya encontrado con este problema. Como solución, vuelva a ejecutar la operación de supresión para completarla y, a continuación, cree el nuevo entorno.

### 8 de mayo de 2017
{: #8may17}

 - Se ha actualizado el modelo de puntuación del tono de emoción para mejorar la precisión en los enriquecimientos del análisis de emociones (`docEmotion`). El conjunto de datos de entrenamiento se ha ampliado, el diseño de la característica ha cambiado y como resultado, el modelo tiene una mayor precisión en el conjunto de datos de referencia.

### 5 de mayo de 2017
{: #5may17}

 - La normalización de entidades ahora está disponible para utilizarla con el servicio Discovery que utiliza un modelo personalizado que Watson Knowledge Studio genera. La normalización de entidades inserta nombres normalizados (canónicos) para las distintas referencias para la misma persona u objeto en el documento de origen. Consulte [Creación de una configuración personalizada para normalizar entidades](/docs/services/discovery?topic=discovery-normalizing-entities-cc#normalizing-entities-cc) para más detalles.

     **Nota:** Actualmente se da soporte a la normalización únicamente como una funcionalidad beta. Consulte la declaración con relación a las funcionalidades beta en la parte superior del producto para más información. [Resuelta](/docs/services/discovery?topic=discovery-release-notes#30jun17)

Conjunto de herramientas de {{site.data.keyword.discoveryshort}}:

 - El registro de errores del registro del conjunto de herramientas ya no está limitado a un máximo de ocho (8) páginas de resultados. El registro de errores seguirá visualizando el ID de documento si el nombre del documento no está disponible.

 - Los nombres de configuración están limitados a 50 caracteres y deben estar formados con los caracteres `[a-zA-Z0-9-_]`. 

 - El parámetro `passages` anteriormente únicamente estaba disponible a través de la API, ahora está disponible también en el conjunto de herramientas además de la API.

### 25 de abril de 2017
{: #25apr17}

  - El servicio ahora le permite proporcionar *datos de entrenamiento* para mejorar la precisión de los resultados de las consultas. Cuando proporciona una instancia de Discovery con datos de entrenamiento, el servicio utiliza los algoritmos de Watson para determinar los resultados más relevantes. A medida que se añaden datos de entrenamiento, la instancia del servicio cada vez es más precisa y sofisticada en los resultados que devuelve. Consulte [Mejora de la relevancia de los resultados de las consultas](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api) y la [Referencia de API](https://{DomainName}/apidocs/discovery#list-training-data) para obtener más información.

  - La API ahora da soporte al parámetro `natural_language_query` como una característica beta. Este parámetro permite especificar una consulta en lenguaje natural en lugar de hacerlo en el lenguaje de consultas del servicio Discovery. Consulte el método [Consultar su recopilación](https://{DomainName}/apidocs/discovery#query-your-collection) en la referencia de la API para obtener más información.

  - Correcciones de erratas y actualizaciones en la documentación.

### 14 de abril de 2017
{: #14apr17}

Se han añadido mejoras a la API de consultas (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`). Consulte el método [Consultar su recopilación](https://{DomainName}/apidocs/discovery#query-your-collection) en la referencia de la API para obtener más información.

  - La API de consulta ahora da soporte al parámetro `passages`. Si el parámetro se establece en `true`, la consulta devuelve un conjunto con los pasajes más relevantes de los documentos de su recopilación. Los pasajes los generan algoritmos sofisticados de Watson que determinan los mejores pasajes del texto entre todos los documentos devueltos por la consulta. Esto le permite encontrar información y contexto de forma más precisa. Consulte el método [Consultar su recopilación](https://{DomainName}/apidocs/discovery#query-your-collection) en la referencia de la API para obtener más información.

    - Si especifica `passages=true` se puede disminuir el rendimiento de la consulta como resultado de la necesidad de un mayor proceso para extraer los pasajes. En entornos grandes, el rendimiento podría verse afectado.

    - Solo se da soporte al parámetro `passages` en recopilaciones privadas. No está soportado en la recopilación Watson Discovery News.

    - Actualmente, el parámetro `passages` devuelve un máximo de 10 resultados. El número de resultados devueltos no se puede cambiar. [Actualizar](/docs/services/discovery?topic=discovery-query-parameters#passages_count)

    - El parámetro `passages` devuelve un máximo de tres (3) pasajes por documento en la recopilación. Si el documento contiene más de tres pasajes relevantes adicionales, el parámetro no los devuelve.

### 7 de abril de 2017
{: #7apr17}

- La API de consulta (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`) ahora da soporte al parámetro `sort`, que permite especificar una lista de campos separados por comas en el documento por los que clasificarlos. Consulte el método [Consultar su recopilación ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery#query-your-collection){: new_window} en la referencia de API para obtener más información.
- El parámetro `timeslice` para agregaciones de consulta ahora maneja de forma correcta las fechas en formato epoch de UNIX. Consulte [Referencia de consultas](/docs/services/discovery?topic=discovery-query-reference#aggregations) para obtener información sobre las agregaciones y el parámetro `timeslice`.
- Mejoras en los mensajes de error.
- Actualizaciones para el servicio de Java SDK. Consulte la [Referencia de API](https://{DomainName}/apidocs/discovery?language=java) para obtener más detalles.
- Se han corregido, y ahora funcionan correctamente, las siguientes limitaciones para utilizar comodines en las consultas:

  - Únicamente funcionaba un comodín en una consulta dada. Por ejemplo, `query-month:*ctober` daba resultados, pero `query-month:*ctobe*` generaba un error de análisis.
  - Los comodines no funcionaban con consultas con mayúsculas. Por ejemplo, dado el par de clave/campo `{"borrower": "GOVERNMENT OF INDIA"}`, `query-borrower:*ndia` devolvía resultados, en cambio `query-borrower:*NDIA` no lo hacía.

**Nota:** Los comodines no son necesarios dentro de las frases en las consultas. Por ejemplo, dado el par de clave/campo `{"borrower": "GOVERNMENT OF TIMOR"}`, `query-borrower:"GOVERNMENT OF TIMOR"` devuelve resultados pero `query-borrower:"GOVERNMENT OF TI*OR"` no lo haría. La utilización de comodines no es aplicable en las frases puesto que todos los caracteres dentro de las comillas (`"`) de una frase se codifican como de escape.

### 24 de marzo de 2017
{: #24mar17}

- Se ha añadido capacidad de filtrar a la pantalla "Mis conocimientos de datos" en el conjunto de herramientas de Discovery

### 15 de marzo de 2017
{: #15mar17}

Se han identificado los siguientes problemas conocidos.

-  Todos los campos que se ingieren a partir de documentos HTML, PDF y Word se convierten a **string**. Los campos calculados y los campos JSON como, por ejemplo, la puntuación de sentimiento, se convierten según a su definición. [Actualizar](/docs/services/discovery?topic=discovery-addcontent#adding-content-with-the-api-or-tooling)
- La operación `preview` actualmente no comprueba matrices JSON anidadas dentro de un documento JSON enviado. El servicio actualmente no da soporte a matrices JSON anidadas, por lo que un documento con matrices anidadas pasará de forma satisfactoria la operación `preview` pero el intento de ingestión fallará. Consulte [¿Puedo cargar matrices JSON?](/docs/services/discovery?topic=discovery-faqs#array)
- Si se le presentan errores de ingestión con el mensaje `idioma de texto no soportado`, actualice la configuración con la opción de enriquecimiento `"language": "english"` para forzar que todo el texto se interprete como inglés, tal como se muestra en el siguiente ejemplo. 
[Actualizar](/docs/services/discovery?topic=discovery-migrate-nlu#migrate-nlu)
```json
"enrichments": [
   {
     "enrichment": "alchemy_language",
     "source_field": "author.label",
     "options": {
       "extract": "taxonomy,entity,relation,doc-emotion,doc-sentiment,concept,keyword",
       "sentiment": true,
       "quotations": true,
       "language": "english"
     }
   }
 ]
```
{: codeblock}

Se han corregido los siguientes problemas.

- Se ha mejorado el rendimiento y la estabilidad del servicio.

### 8 de marzo de 2017
{: #8mar17}

 - Se ha optimizado el sistema de fondo y se han añadido nuevos tiempos de espera, para un mejor rendimiento global.
 - Se ha corregido un error que hacía que el estado de los entornos gratuitos (tamaño `0`) informasen de un estado de `pending` independientemente del estado real.
 - El único idioma nacional al que {{site.data.keyword.discoveryshort}} da soporte es el inglés de Estados Unidos (`en_US`). [Actualizar](/docs/services/discovery?topic=discovery-language-support#language-support)

### 3 de marzo de 2017
{: #3mar17}

- Se ha añadido la pantalla "Mis conocimientos de datos" al conjunto de herramientas de Discovery.

### 26 de febrero de 2017
{: #26feb17}

-     Se ha mejorado el rendimiento del entorno de {{site.data.keyword.discoverynewsshort}}.
-  El servicio de {{site.data.keyword.discoverynewsshort}} devuelve un máximo de 50 resultados al mismo tiempo. Como solución alternativa, utilice el parámetro `offset` en la consulta para paginar a través de los resultados.
-  Puede enviar una nueva configuración con un documento individual utilizando el siguiente mandato:

```bash
curl -X POST -u apikey:{apikey_value} -F "file=@wikipedia-sample.html" -F "configuration=$(cat config.json)" "https://gateway.watsonplatform.net/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2016-12-01"
```
{: pre}
-  Los convertidores de PDF y Word del servicio crean HTML como un paso intermedio. El servicio puede aplicar transformación y normalizaciones adicionales en el HTML intermedio antes de la transformación final a JSON normalizado.

Se han corregido los siguientes problemas.

-  Se han mejorado códigos de error.
-  Se han corregido varias erratas en la documentación.

### 16 de febrero de 2017
{: #16feb17}

-  Ahora se pueden utilizar selectores CSS para seleccionar campos JSON a los que después aplicar enriquecimientos. Consulte [Utilización de selectores CSS para extraer campos](/docs/services/discovery?topic=discovery-configservice#using-css) para obtener más información.
-  Ahora puede incrementar el tamaño de un entorno pasando un nuevo parámetro `size: X` al [método update-environment](https://{DomainName}/apidocs/discovery#update-an-environment), donde `X` es un entero entre 0 y 3. Consulte el [método create-environment](https://{DomainName}/apidocs/discovery#create-an-environment) para obtener información sobre los atributos y tamaños de entorno. [Actualizar](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)

    **Nota:** No es posible reducir el tamaño de un entorno existente. Si desea reducir el tamaño de su entorno, póngase en contacto con el soporte de {{site.data.keyword.IBM}} para que le ayuden.

-  Está disponible un nuevo operador de consulta. Se ha añadido el operador `::!` como operador unario no igual a. Por ejemplo, ahora puede ejecutar `query=field::!value` (no igual a). Con anterioridad, el único operador para las exclusiones era `:!` como operador de no contiene (por ejemplo, `query=field:!value`).

Se han corregido los siguientes problemas.

-  Se han aplicado actualizaciones de seguridad.
-  Se han mejorado mensajes de estado para las alertas de búsqueda.

### 1 de febrero de 2017
{: #1feb17}

Las notas siguientes se aplican específicamente a la versión 1.3.0. de Data Crawler.
[Actualizar](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler)

-   Data Crawler registra los valores de `document_id` utilizados para cargar documentos, y el estado de la carga. Los avisos de conversión ahora son persistentes fuera del registro. Actualmente no hay una herramienta para interactuar con los datos, pero se espera desarrollar herramientas de este tipo en la medida de lo posible. Los datos son accesibles a través de una base de datos H2, que se podría configurar para utilizar un sistema de gestión de bases datos (DBMS) remoto.

### 16 de enero de 2017
{: #16jan17}

Las notas siguientes se aplican específicamente a la versión 1.2.5 de Data Crawler.
[Actualizar](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler)

-  Data Crawler de forma opcional puede sondear el estado de un documento inmediatamente después de cargar un archivo. Esta comprobación es una parte del concepto del rastreador de "cargar un documento", de forma que cuando esta comprobación está habilitada, es virtualmente imposible que el rastreador cargue simultáneamente más documentos de los que el servicio {{site.data.keyword.discoveryshort}} puede procesar para el usuario de forma simultánea.

    Un efecto colateral de la característica `check_for_completion` es que el rastreador también puede exponer al usuario la razón del fallo del documento cuando esto ocurra. Todos los avisos adjuntados al documento que se cargó de forma satisfactoria, pero que tuvo errores al ser procesado, se visualizan en el registro del rastreador. Los avisos no se exportan a un archivo que se pueda procesar, sin embargo, IBM podría estar dispuesta a aceptar esta sugerencia como una posible característica.

### 5 de enero de 2017
{: #5jan17}

Las siguientes notas describen problemas identificados después de la disponibilidad general (GA) el 15 de diciembre de 2016.

[Actualización: Referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery){: new_window}

-   Si añade un documento utilizando la llamada `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` o `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]`, la llamada devuelve un ID de documento y el estado de **processing**. Si a continuación consulta el documento con la llamada `GET /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]`, el estado permanece en **processing** hasta que se completa la ingestión, en cuyo instante, el estado cambia a **available**.

    Si **actualiza** un documento existente utilizando la llamada `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]`, la correspondiente llamada **GET** devuelve el estado `available` incluso si el servicio todavía no ha acabado de procesar en su totalidad el documento cargado. El estado `available` puede hacer referencia al documento original o al documento actualizado. A no ser que la operación de actualización devuelva un error, actualmente no hay una forma de determinar el estado del documento actualizado.

    Como solución alternativa, puede esperar hasta 10 minutos después de haber enviado una actualización de documento antes de intentar consultar el contenido actualizado.

### Release de disponibilidad general (GA), 15 de diciembre de 2016
{: #15dec16}

Las siguientes notas se aplican al release de disponibilidad general (GA) del servicio {{site.data.keyword.discoveryfull}}.

#### Notas generales
{: #rn-general-notes}

[Actualización: Adición de contenido](/docs/services/discovery?topic=discovery-addcontent#addcontent)

Consulte [Referencia API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery){: new_window} para ver la versión de la API actual.

[Actualización: Integración con {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-with-wks).

-   Actualmente no se puede especificar el tipo de datos de los campos. Todos los campos se indexan como texto (tipo de datos **string**). 
-   Si utiliza la API para trabajar con el servicio, debe especificar la versión de la API con cada llamada. La versión de API actual es **2016-12-01**. 

    **Nota:** No se obliga a utilizar la versión específica en el release de disponibilidad general (GA), pero a pesar de esto se listará para habilitar la compatibilidad con futuros releases.

-   Puede utilizar el servicio con un modelo personalizado creado con {{site.data.keyword.knowledgestudiofull}}. El modelo personalizado se puede utilizar para enriquecer los documentos ingeridos. Debe utilizar la API para integrar el modelo personalizado con el servicio {{site.data.keyword.discoveryshort}} (no es posible realizar la integración con el conjunto de herramientas).

#### Gestión de datos
{: #rn-data}

[Actualizar](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)

-   Los índices de búsqueda no están cifrados.
-   Las funciones de copia de seguridad y restauración no las puede controlar el usuario.

#### Entornos
{: #rn-environments}

[Actualizar](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)

-   Únicamente se puede crear un entorno por instancia de servicio para cargar sus datos.
-   El servicio {{site.data.keyword.discoveryshort}} está ubicado en una única zona de disponibilidad (EE.UU. sur).
-   Actualmente los planes Dedicated y Premium no están disponibles.

#### Tamaño del entorno
{: #rn-sizing}

[Actualizar](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)

-   El tamaño de un entorno solo se puede elegir al crearlo. Actualmente no está disponible a los usuarios la posibilidad de redimensionar un entorno.
-   La elección de un tamaño de entorno con más RAM mejora el rendimiento.
-   Actualmente no hay recomendaciones de tamaño prescriptivas para casos de uso específicos.
-   El usuario no puede definir tamaños personalizados para los modelos de {{site.data.keyword.knowledgestudiofull}}. Póngase en contacto con el representante de {{site.data.keyword.IBM}} para obtener más información.

#### Limitaciones de ingestión
{: #rn-ingestion}

[Actualizar](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)

-   La ingestión actualmente está limitada a 100 operaciones simultáneas de ingestión de documentos. Una aplicación que envía documentos al servicio para su ingestión necesita respetar errores HTTP 429 y regular la ingestión de documentos de forma adecuada.
-   Los enriquecimientos de {{site.data.keyword.alchemylanguageshort}} están limitados a los primeros 50 KB por campo.
-   Los enriquecimientos de modelos personalizados de {{site.data.keyword.knowledgestudiofull}} no están limitados, pero divide documentos en fragmentos de 10 KB. No se anotan relaciones más allá de los límites de los fragmentos.

#### Limitaciones en las consultas
{: #rn-query}

[Actualizar](/docs/services/discovery?topic=discovery-query-concepts#query-concepts)

-   Una carga de consultas excesiva puede originar que el proceso de índice de búsqueda se reinicie de forma automática.
-   Las aplicaciones que emiten consultas deben respetar unos límites razonables de consultas simultáneas.

### Problemas conocidos
{: #rn-issues}

[Actualización: Referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery){: new_window}

[Actualización: herramientas](/docs/services/discovery?topic=discovery-getting-started#getting-started)

[Actualización: Data Crawler](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler)

[Actualización: Enriquecimientos](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)

[Actualización: Adición de contenido](/docs/services/discovery?topic=discovery-addcontent#addcontent)

-   No es posible suprimir un documento utilizando el conjunto de herramientas. Si necesita suprimir un documento, debe utilizar el método [Suprimir un documento](https://{DomainName}/apidocs/discovery#delete-a-document) de la API tal como se describe en la documentación de la referencia de API.

-   Actualmente la API no da soporte a la obtención de una lista de avisos y errores que se genera durante la ingestión de los documentos. Por lo tanto, el conjunto de herramientas no puede mostrar una lista de avisos de ingestión, y no hay una forma fácil de determinar, si hay, documentos que Data Crawler haya rastreado y que no se hayan podido ingerir. 
-   La información de estado del documento no siempre es precisa.
    -   Si una operación de ingestión excede el tiempo de espera configurado de 10 minutos, el servicio informa que lo desconoce hasta que la operación de ingestión acaba. Una vez se haya completado la operación, el estado del documento está disponible y es preciso.
    -   Documentos que se indexan de forma satisfactoria pero que generan errores pueden tener un estado **failed** durante un breve periodo de tiempo hasta que el documento se haya confirmado en su totalidad para el índice. Una vez el documento se haya confirmado para el índice, el estado que se muestra es el preciso.
-   No se puede utilizar el conjunto de herramientas para remplazar un documento específico. Si intenta hacerlo, el segundo documento se carga como un documento aparte. Si está utilizando la API sabe el ID del documento que desea remplazar, puede hacerlo; para ello, consulte [Actualizar un documento](https://{DomainName}/apidocs/discovery#update-a-document) en la Referencia de la API. Si está utilizando Data Crawler, si se carga un documento actualizado desde el mismo URL que un documento anterior remplazará el documento original.
-   Si está utilizando el conjunto de herramientas para editar los enriquecimientos en la configuración, puede editar únicamente aquellos enriquecimientos utilizados para la extracción. Si desea añadir o editar otros enriquecimientos (por ejemplo, enriquecimientos personalizados desde un modelo de {{site.data.keyword.knowledgestudiofull}}), debe utilizar la API. Consulte el método [Actualizar una configuración](https://{DomainName}/apidocs/discovery#update-a-configuration) en la referencia de la API para obtener más información.
-   Las notas siguientes se aplican específicamente a Data Crawler. 
    -   Data Crawler reintenta las cargas si se encuentra una anomalía en las mismas.
    -   Data Crawler no puede reintentar cargar documentos que se han cargado de forma satisfactoria pero que no se han podido convertir o indexar.
    -   Data Crawler no tiene una función para comprobar el estado en sentido descendente e intentar volver a cargar URL cuando producen anomalías en el flujo en sentido descendente.
    -   No hay una forma fácil de determinar qué documentos ha ingerido Data Crawler. Por ejemplo, si ejecuta Data Crawler con relación a un conjunto de 500 documentos, Data Crawler podría informar de anomalías al enviar 65 documentos de una recopilación de 212 documentos en total. El estado de los 223 restantes es indeterminado.

        Hay disponible un método alternativo, pero es complicado y suponer invocar a la API directamente. Póngase en contacto con el soporte de {{site.data.keyword.IBM}} para obtener ayuda.
-   Los SDK de Java, Python y Node.js SDK para {{site.data.keyword.discoveryshort}}
no proporcionan toda la funcionalidad que proporciona la API (cURL) REST predeterminada. No todos los métodos cURL tienen un método disponible en los SDK no-cURL, y no todos los métodos no-cURL proporcionan las mismas características que las que tienen los cURL equivalentes. En otras palabras, los SDK de Java, Python y Node.js actualmente únicamente proporcionan un subconjunto de las funcionalidades de la API de cURL.
-   Si utiliza un conversor de Word, la coincidencia de cabeceras utilizando la clave `style` es mucho más precisa y eficiente que la obtenida utilizando la clave `level`.
