---

copyright:
  years: 2019
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

# Alta disponibilidad y recuperación tras desastre
{: #recovery}

{{site.data.keyword.discoveryfull}} da soporte a la alta disponibilidad sin ningún punto único de anomalía. Además, es responsabilidad del cliente realizar una copia de seguridad de los datos de {{site.data.keyword.discoveryshort}} como parte de su propio plan de recuperación tras desastre, de forma que pueda volver a crear el servicio.
{: shortdesc}

La carga del tráfico de {{site.data.keyword.discoveryshort}} está equilibrada en varias zonas de una región. Cada zona es un centro de datos en la misma región. Consulte [¿Cómo puedo asegurar un tiempo de inactividad cero? ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/docs/overview?topic=overview-zero-downtime#zero-downtime){: new_window} para obtener más información.

## Copia de seguridad de los datos en Watson Discovery
{: #backup}

Hay varios métodos para realizar una copia de seguridad de los datos almacenados en {{site.data.keyword.discoveryfull}}. Estos métodos se deben incluir en el plan de recuperación tras desastre. 

-  Datos de los que debería guardar una copia, como por ejemplo documentos de origen
-  Datos que almacena {{site.data.keyword.discoveryshort}}, que debe extraer y de los que debe realizar una copia de seguridad
  
Habrá datos que será necesario volver a crear a partir de cero (por ejemplo, datos de los que no puede realizar una copia de seguridad como, por ejemplo, sucesos de comentarios). 

### Documentos ingeridos
{: #backupdocs}

Los documentos cargados se convierten y se enriquecen y, a continuación, se almacenan en el índice de búsqueda. El índice de búsqueda no es recuperable en caso de desastre y, por lo tanto, debería almacenar una copia de seguridad de todos los documentos de origen en un lugar seguro.

Si también importa documentos realizando rastreos planificados de orígenes de datos externos, debería conservar sus credenciales de origen de datos externamente, de forma que pueda volver a establecer los orígenes de datos rápidamente. Consulte [Conexión a orígenes de datos](/docs/services/discovery?topic=discovery-sources#sources) para ver la lista de orígenes disponibles y las credenciales necesarias para cada uno de ellos.

### Configuraciones
{: #backupconfigs}

Debe realizar una copia de seguridad de las configuraciones de instancia y almacenarla localmente en caso de desastre. 

Para realizar una copia de seguridad de estas configuraciones, en primer lugar [liste las configuraciones](https://cloud.ibm.com/apidocs/discovery#list-configurations) para cada instancia. 

Después de obtener la lista de configuraciones, [obtenga los detalles](https://cloud.ibm.com/apidocs/discovery#get-configuration-details) para cada configuración.

### Datos de entrenamiento
{: #backuptraining}

Debe realizar una copia de seguridad de los datos de entrenamiento para cada recopilación entrenada y almacenarla localmente en caso de desastre.  

Los datos de entrenamiento se utilizan para el entrenamiento explícito de las recopilaciones y se almacenan por cada recopilación. 

Para extraer los datos de entrenamiento, utilice la API para descargar las consultas y las valoraciones de {{site.data.keyword.discoveryshort}}. 

1.  [Liste los datos de entrenamiento](https://cloud.ibm.com/apidocs/discovery#list-training-data)
1.  [Liste los ejemplos](https://cloud.ibm.com/apidocs/discovery#list-examples-for-a-training-data-query) para cada consulta.
1.  [Obtenga los detalles](https://cloud.ibm.com/apidocs/discovery#get-details-for-training-data-example) para ver los ejemplos de datos de entrenamiento. 

Los `id de documento` que utiliza en los datos de entrenamiento apuntan a los documentos de la recopilación actual. DEBE utilizar los mismos `id de documento` en las nuevas recopilaciones para asegurarse de que se haga referencia a los id correctos. Si no lo hace, el entrenamiento de relevancia restaurado NO FUNCIONARÁ.
{: important} 

### Consultas
{: #backupqueries}

De forma predeterminada (a no ser que desactive la opción), {{site.data.keyword.discoveryshort}} almacenará las consultas que le envíe. 

Si desea poder restaurarlas [con fines estadísticos](https://cloud.ibm.com/apidocs/discovery#number-of-queries-over-time), debe almacenar estas consultas por separado. 

Puede [extraer consultas](https://cloud.ibm.com/apidocs/discovery#search-the-query-and-event-log) de {{site.data.keyword.discoveryshort}}, aunque se almacenan un máximo de 10.000 consultas. No hay API de paginación. No se recomienda la restauración de consultas; recomendamos empezar desde cero. 

### Comentarios/pulsaciones
{: #clicks}

Si almacena clics en forma de sucesos de comentarios, actualmente no existe ninguna forma sencilla de realizar una copia de seguridad y restaurar esta información. La recomendación es empezar de cero con la API de [datos de clics/comentarios](https://cloud.ibm.com/apidocs/discovery#create-event). 

### Listas de expansión
{: #backupexpansions}

Si utiliza expansiones para la modificación de consultas, debe realizar una copia de seguridad de la lista de expansión y almacenarla localmente. Para ello, solicite la lista de expansión utilizando el mandato de la API [get expansion list](https://cloud.ibm.com/apidocs/discovery#get-the-expansion-list) y almacénela localmente.

### Diccionarios de señalización o palabras vacías
{: #backupstopwords}

Si utiliza estas funciones, tendrá que realizar una copia de seguridad de estos archivos y almacenarlos localmente. En el caso de las palabras vacías, realice una copia de seguridad del archivo de texto, y en el caso de las señalizaciones, debe realizar una copia de seguridad del archivo JSON. Consulte [Creación de diccionarios de señalización personalizados](/docs/services/discovery?topic=discovery-query-concepts#tokenization) y [Definición de palabras vacías](/docs/services/discovery?topic=discovery-query-concepts#stopwords) para obtener más información acerca de cada tipo de archivo.

### Información de la recopilación
{: #collectioninfo}

No es necesario, pero es una buena práctica recomendada [recuperar el estado](https://cloud.ibm.com/apidocs/discovery#get-collection-details) de cada recopilación de forma regular y almacenar la información localmente. Al retener estas estadísticas, puede verificar posteriormente si los procesos de restauración se han realizado correctamente, si es necesario.
{: tip} 


### Modelos de comprensión de documentos inteligentes
{: #backupsdu}

Si utiliza la función Comprensión de documentos inteligentes (SDU), tendrá modelos asociados a la configuración. Para evitar la pérdida de esta información, debe [exportar los modelos](/docs/services/discovery?topic=discovery-sdu#import), realizar una copia de seguridad de ellos y almacenarlos localmente. Los modelos de SDU tienen la extensión de archivo `.sdumodel`.


## Restauración de los datos en una nueva instancia de Watson Discovery
{: #restore}

Considere la posibilidad de utilizar las copias de seguridad para restaurar a una nueva instancia de {{site.data.keyword.discoveryshort}} en un centro de datos diferente (también conocido como región/ubicación; por ejemplo, Dallas, Houston, Washington, DC, Londres). 
{: note}

Para empezar la restauración, primero debe revisar la lista de recopilaciones y los orígenes de datos asociados, así como las copias de seguridad de los archivos.

-  Cree el [entorno](https://cloud.ibm.com/apidocs/discovery#create-an-environment) y las [recopilaciones](https://cloud.ibm.com/apidocs/discovery#create-a-collection) utilizando la información de configuración guardada. Asegúrese de que la configuración adecuada se haya definido de forma apropiada y de que el idioma de la recopilación se haya establecido correctamente. Si no lo hace, tardará más en poder volver a poner en marcha el sistema.
-  Si tiene alguna configuración personalizada establecida en {{site.data.keyword.discoveryshort}}, tendrá que [volver a crear estas configuraciones personalizadas](/docs/services/discovery?topic=discovery-configservice#when-you-need-a-custom-configuration). 
-  Vuelva a añadir diccionarios de señalización o palabras vacías a las recopilaciones. Consulte [Creación de diccionarios de señalización personalizados](/docs/services/discovery?topic=discovery-query-concepts#tokenization) y [Definición de palabras vacías](/docs/services/discovery?topic=discovery-query-concepts#stopwords).  
-  Si ha utilizado la expansión de consulta personalizada, tendrá que [añadir las expansiones de consulta](https://cloud.ibm.com/apidocs/discovery#create-or-update-expansion-list) para cada colección. 
-  Si ha utilizado modelos de entidad personalizados de Watson Knowledge Studio (WKS) para el enriquecimiento, tendrá que [volver a importar esos modelos](/docs/services/discovery?topic=discovery-configservice#custom-entity-model) en la instancia de {{site.data.keyword.discoveryshort}}. 

Una vez que tenga las recopilaciones configuradas como antes, tendrá que empezar a ingerir los documentos de origen. Dependiendo de cómo haya ingerido los documentos previamente, puede hacerlo mediante:
-  La [API](https://cloud.ibm.com/apidocs/discovery#add-a-document)
-  Un [conector](/docs/services/discovery?topic=discovery-sources#sources) 
-  [Data Crawler](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler)
-  u otro método

### Restauración de datos de entrenamiento
{: #restoretraining}

Una vez que se hayan restaurado las recopilaciones, puede empezar el proceso de [volver a crear los modelos de entrenamiento de relevancia](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api). 

Recupere los datos de entrenamiento de los que ha realizado la copia de seguridad y, a continuación:

1. [Cargue las consultas](https://cloud.ibm.com/apidocs/discovery#add-query-to-training-data)
1. [Cargue los documentos de ejemplo](https://cloud.ibm.com/apidocs/discovery#add-example-to-training-data-query) para cada consulta.
1.  Después de cargar los datos de entrenamiento, revise esta [publicación de blog](https://developer.ibm.com/dwblog/2017/get-relevancy-training/) para asegurarse de que cumple con las cifras de precisión anteriores. Tenga en cuenta que debe transferir los `id de documento` a los nuevos datos de entrenamiento, o actualizarlos para reflejar los nuevos id de documento en la nueva recopilación.


### Restauración de conexiones a orígenes de datos externos
{: #restoreconnections}

Si se produce una pérdida imprevista de datos, puede perder los rastreos planificados de los orígenes de datos externos. Consulte [Conexión a orígenes de datos](/docs/services/discovery?topic=discovery-sources#sources) para ver la lista de orígenes disponibles.

Para restaurar los datos externos, tendrá que volver a establecer las conexiones con estos orígenes de datos y, a continuación, volver a rastrearlos.

Busque las credenciales de origen de datos que ha almacenado anteriormente y siga las instrucciones indicadas [aquí](/docs/services/discovery?topic=discovery-sources#sources). De este modo, podrá volver a conectarse a sus orígenes de datos e importar los datos en {{site.data.keyword.discoveryshort}}.


### Restauración de modelos de comprensión de documentos inteligentes
{: #restoresdu}

Para importar un modelo de comprensión de documentos inteligentes (SDU) exportado previamente, siga las instrucciones indicadas [aquí](/docs/services/discovery?topic=discovery-sdu#import). Los modelos de SDU tienen la extensión de archivo `.sdumodel`.

Al importar un modelo de SDU existente en una nueva recopilación, es una buena práctica recomendada crear la nueva colección y añadir un documento y, a continuación, importar el modelo y cargar el resto de los documentos.
