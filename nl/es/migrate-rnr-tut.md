---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-09"

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


# Guía de aprendizaje: Migración desde Retrieve and Rank
{: #migrate-rnr}

Migración desde {{site.data.keyword.retrieveandrankshort}} al servicio {{site.data.keyword.discoveryfull}}. Es una continuación de la guía de aprendizaje de iniciación de Cranfield.

## Visión general
{: #overview-rnr}

Esta guía le guía a través del proceso de creación y entrenamiento de un servicio {{site.data.keyword.discoveryfull}} con datos de ejemplo. Esta guía de aprendizaje utiliza el mismo conjunto de datos que el utilizado en la [Guía de aprendizaje de iniciación de {{site.data.keyword.retrieveandrankshort}}](/docs/services/retrieve-and-rank/getting-started.html), pero puede utilizar la misma aproximación para crear una instancia de servicio que utilice sus propios datos.

El proceso para los usuarios de migración de datos desde {{site.data.keyword.retrieveandrankshort}} a {{site.data.keyword.discoveryshort}} está formado por dos pasos principales.

1. Migrar los datos de recopilación.
2. Migrar los datos de entrenamiento.

Cuando se migran los datos de recopilación entrenados, lo que es **más** importante es _mantener los mismos id de documento_. Esto se debe a que los datos de entrenamiento utilizan estos id para hacer referencia a los datos objetivos ("ground truth"), y si los id se cambian en el traspaso desde {{site.data.keyword.retrieveandrankshort}} a {{site.data.keyword.discoveryshort}}, entonces la reclasificación será totalmente errónea (o incluso podría no iniciarse). {{site.data.keyword.discoveryshort}} permite especificar el ID de documento en el proceso de carga de API, de forma que se pueda evitar este problema si se siguen las directrices en este documento.  Los datos de entrenamiento de {{site.data.keyword.retrieveandrankshort}} habitualmente se almacenan en un archivo `csv`. En esta guía de aprendizaje, este archivo `csv` se utilizará para cargar los datos de entrenamiento de ejemplo en {{site.data.keyword.discoveryshort}}.  La migración de datos de entrenamiento exportados desde el conjunto de herramientas de {{site.data.keyword.retrieveandrankshort}} se explica en detalle en la [migración de datos de entrenamiento desde el servicio](/docs/services/discovery?topic=discovery-migrate-dcs-rr#extract-train).

Esta guía de aprendizaje presupone que {{site.data.keyword.retrieveandrankshort}} se configuró de forma parecida a la indicada en la [Guía de aprendizaje de iniciación de {{site.data.keyword.retrieveandrankshort}}](/docs/services/retrieve-and-rank/getting-started.html) y se sigue el camino de migración desde los datos de origen tal como se describe [aquí](/docs/services/discovery?topic=discovery-migrate-dcs-rr#source). Consulte [Evaluación de los caminos de migración para el servicio Watson Discovery](/docs/services/discovery?topic=discovery-migrate-dcs-rr#evaluate) para conocer otras opciones de migración.

Necesitará lo siguiente para completar la guía de aprendizaje:

-  **cURL.**  Puede instalar la versión de cURL para su sistema operativo desde [haxx.se ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://curl.haxx.se/){: new_window}. Debe instalar la versión que dé soporte al protocolo SSL (Secure Sockets Layer). Asegúrese de incluir el archivo binario instalado en la variable de entorno PATH.
-  Datos de ejemplo de Cranfield. Esta guía de aprendizaje utiliza los datos de la recopilación de ejemplo de la Guía de aprendizaje de iniciación de {{site.data.keyword.retrieveandrankshort}}. [Datos json de cranfield ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-data.json){: new_window}
-  **Datos de ejemplo objetivos ("ground truth")** Esta guía de aprendizaje utiliza los datos objetivos de ejemplo de Cranfield de la Guía de aprendizaje de iniciación de {{site.data.keyword.retrieveandrankshort}}. [CSV de datos objetivos de Cranfield![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-gt.csv){: new_window}
-  **Python versión 2.**  Para comprobar si Python está instalado, especifique `python --version` en un indicador de línea de mandatos y asegúrese de que el número de versión empieza por 2. Si necesita instalar Python, consulte [Descargar Python ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://wiki.python.org/moin/BeginnersGuide/Download){: new_window}.
-  Script de carga de datos: [Cargador de documentos de Discovery ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-upload.py){: new_window}
-  Script de carga de datos de entrenamiento: [Cargador de entrenamiento de Discovery ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-train.py){: new_window}

Son necesarios los siguientes requisitos previos antes de empezar esta guía de aprendizaje:

-  Esta guía de aprendizaje presupone que ya ha creado una instancia de {{site.data.keyword.discoveryshort}}. Si necesita instrucciones sobre cómo crear una instancia de {{site.data.keyword.discoveryshort}}, consulte la [siguiente guía de aprendizaje](/docs/services/discovery?topic=discovery-gs-api#gs-api).

-  Esta guía de aprendizaje presupone que tiene sus credenciales de servicio.
   -  En el servicio de Watson {{site.data.keyword.discoveryshort}} en {{site.data.keyword.Bluemix_notm}}, pulse **Credenciales de servicio**.
   -  Pulse **Ver credenciales** bajo Acciones.
   -  Copie el valor `apikey` y asegúrese de que el valor `url` coincide con el de los ejemplos que hay a continuación; si no es así, sustitúyalo también.

## Adición de datos de Cranfield a Discovery
{: #cranfield-rnr}

1.  Cree un entorno.

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d '{ "name": "my_environment", "description": "My environment" }' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    Copie el `environment-id` que aparece listado en el JSON devuelto.

1. Cree una recopilación.

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d '{ "name": "test_collection", "description": "My test collection", "configuration_id": "{configuration_id}", "language_code": "en" }' "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07"
    ```
    {: pre}

    Copie el `collection-id` que aparece listado en el JSON devuelto.

1.  Añada los documentos que se buscarán.
    1.  Descargue el archivo [cranfield-data.json ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-data.json){: new_window} si todavía no lo ha hecho. Se trata del origen de los documentos que se utilizan en {{site.data.keyword.retrieveandrankshort}}. Los documentos de la recopilación de Cranfield están en formato JSON, que es el formato que {{site.data.keyword.retrieveandrankshort}} acepta y que también funciona bien con Watson {{site.data.keyword.discoveryshort}}.
        **Nota:** {{site.data.keyword.discoveryshort}} no precisa cargar el esquema de Solr. Esto se debe a que {{site.data.keyword.discoveryshort}} infiere de forma automática el esquema de la estructura JSON.
    1.  Descargue el script de carga de datos [aquí ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-upload.py){: new_window}. El script cargará el json de Cranfield json en {{site.data.keyword.discoveryshort}}.
        El script lee a través del archivo JSON y envía cada documento JSON individual al servicio {{site.data.keyword.discoveryshort}} utilizando una configuración predeterminada en {{site.data.keyword.discoveryshort}}.
        **Nota:** La configuración predeterminada en {{site.data.keyword.discoveryshort}} proporciona valores similares a los de la configuración de Solr predeterminada en {{site.data.keyword.retrieveandrankshort}}.
    1.  Especifique el siguiente mandato para cargar los datos de `cranfield-data-json` en la recopilación `cranfield_collection`. sustituya `{apikey_value}`, `{path_to_file}`,  `{environment_id}`, `{collection_id}` con su información.  Observe que hay opciones adicionales: -d para depurar y –v para una salida detallada desde curl.

        ```bash
        python ./disco-upload.py -u apikey:{apikey_value} -i {path_to_file}/cranfield-data.json -e {environment_id} -c {collection_id}
        ```
        {: pre}

1.  Una vez que el proceso de carga haya finalizado, puede comprobar que los documentos se han cargado especificando el siguiente mandato para ver los detalles de la recopilación:

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07"
    ```
    {: pre}

    La salida debería ser similar a la siguiente:

    ```json
    {
      "collection_id": "f1360220-ea2d-4271-9d62-89a910b13c37",
      "name": "democollection",
      "configuration_id": "6963be41-2dea-4f79-8f52-127c63c479b0",
      "language": "en",
      "status": "available",
      "description": "this is a demo collection",
      "created": "2015-08-24T18:42:25.324Z",
      "updated": "2015-08-24T18:42:25.324Z",      
      "document_counts": {
        "available": 1000,
        "processing": 20,
        "failed": 180
      },
      "disk_usage": {
        "used_bytes": 260
      },
      "training_status": {
        "data_updated": null,
        "total_examples": 0,
        "sufficient_label_diversity": false,
        "processing": false,
        "minimum_examples_added": true,
        "successfully_trained": null,
        "available": false,
        "notices": 0,
        "minimum_queries_added": false        
      }
    }
    ```
    {: codeblock}

Busque en la sección `document_counts` para ver cuántos documentos se han cargado correctamente. No deberían haber errores de documento con este conjunto de datos de ejemplo. Sin embargo, con otros conjuntos de datos, podría haber un recuento con documentos anómalos. Si tiene algún documento anómalo, consulte la API de avisos para ver los mensajes de error. Busque en la sección [aquí ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery#query-system-notices){: new_window} para revisar el mandato de la API de avisos.

La sección `training` de la información devuelta proporciona información sobre el entrenamiento. Revisaremos esta sección después de haber cargado los datos de entrenamiento.

## Adición de datos de entrenamiento en Discovery
{: #trainingdata-rnr}

El servicio Watson {{site.data.keyword.discoveryshort}} utiliza un modelo de aprendizaje máquina para reclasificar documentos. Para ello es necesario entrenar un modelo. El entrenamiento se realiza después de haber cargado suficientes consultas junto con los documentos valorados apropiados. Si carga suficientes documentos con la suficiente variedad en {{site.data.keyword.discoveryshort}}, le estará indicando lo "bueno" que es un documento. En este paso, utilizaremos los datos objetivos ("ground truth") de Cranfield que se utilizan en {{site.data.keyword.retrieveandrankshort}} para entrenar a Watson {{site.data.keyword.discoveryshort}}.

1.  Descargue el ejemplo del [archivo csv de datos objetivos ("ground truth") de Cranfield ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-gt.csv){: new_window} desde la guía de aprendizaje de {{site.data.keyword.retrieveandrankshort}} si todavía no lo ha hecho.

   El archivo es un conjunto de preguntas que un usuario podría preguntar sobre los documentos. El archivo proporciona información de ejemplo para entrenar el clasificador en {{site.data.keyword.retrieveandrankshort}} y el entrenamiento de relevancia en {{site.data.keyword.discoveryshort}} sobre preguntas y respuestas relevantes.

   Para cada pregunta, hay al menos un identificador para una respuesta (el ID de documento). Cada ID de documento incluye un número para indicar la relevancia de la respuesta a la pregunta. El ID de documento apunta a la respuesta en el archivo `cranfield-data.json` que ha cargado en {{site.data.keyword.discoveryshort}} en el paso anterior.

1.  Descargue el script de carga de datos de entrenamiento. Utilizará este script para cargar los datos de entrenamiento en {{site.data.keyword.discoveryshort}}. El script transforma el archivo `csv` en un conjunto de ejemplos y los envía al servicio {{site.data.keyword.discoveryshort}} utilizando las [API de datos de entrenamiento ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery#list-training-data){: new_window}
    **Nota:** {{site.data.keyword.discoveryshort}}gestiona datos de entrenamiento dentro del servicio, por lo que al generar nuevos ejemplos y consultas de entrenamiento se pueden almacenar en el propio {{site.data.keyword.discoveryshort}} en vez de un archivo CSV aparte que es necesario mantener.
1.  Ejecute el script de carga de entrenamiento para cargar los datos de entrenamiento en {{site.data.keyword.discoveryshort}}. Sustituya `{apikey_value}`, `{path_to_file}`, `{environment_id}`, `{collection_id}` con su información. Observe que hay opciones adicionales: `-d` para depurar y `–v` para una salida detallada desde curl.

    ```bash
    python ./disco-train.py -u apikey:{apikey_value} -i {path_to_file}/cranfield-gt.csv –e {environment_id} -c {collection_id}
    ```
    {: pre}

1.  Una vez se hayan cargado los datos, puede comprobar el estado del entrenamiento utilizando el mandato de detalles de recopilación que vimos en la sección anterior. {{site.data.keyword.discoveryshort}} comprobará aproximadamente cada hora si hay nuevos datos, y si lo hay empezará a procesarlos y convertirlos en un modelo de aprendizaje máquina. Cuando el modelo se esté entrenando, verá que el estado de la sección de aprendizaje cambia de `"processing": false` a `"processing": true`. Una vez que el modelo esté entrenado, verá que el estado en la sección de aprendizaje cambia de `"available": false` a `"available": true`. También verá el cambio de fecha para el valor `"successfully_trained"`.  Si hay errores, los verá consultando la **API de avisos** tal como se ha descrito en la sección anterior.

## Búsqueda de documentos
{: #search-rnr}

El servicio {{site.data.keyword.discoveryshort}} automáticamente utilizará un modelo entrenado para reclasificar los resultados de búsqueda de rango si están disponibles. Cuando se realiza [una llamada de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery#query-your-collection){: new_window} con `natural_language_query` en lugar de `query`, se realiza una comprobación para ver si hay disponible un modelo. Si hay disponible un modelo, {{site.data.keyword.discoveryshort}} utiliza el modelo para reclasificar los resultados. En primer lugar, haremos una búsqueda en los documentos no clasificados, y luego haremos una búsqueda utilizando el modelo de clasificación.

1.  Puede buscar documentos en su recopilación mediante un mandato cURL. Realice una consulta utilizando la llamada de API de query para ver los resultados sin clasificar. Sustituya `{apikey_value}`, `{environment_id}`, `{collection_id}` por sus propios valores.  Los resultados devueltos serán resultados sin clasificar, y utilizarán las fórmulas de clasificación de {{site.data.keyword.discoveryshort}} predeterminadas. Puede intentar otras consultas abriendo el archivo de datos de entrenamiento `csv` y copiando el valor de la primera columna en el parámetro de consulta.

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&query=what is the basic mechanism of the transonic aileron buzz"
    ```
    {: pre}

1.  Realice ahora una búsqueda con el modelo estableciendo el parámetro `natural_language_query`. Antes de hacerlo, asegúrese de comprobar que tiene un modelo entrenado tal como se describe en la sección anterior.  Pegue el siguiente código en su consola, sustituyendo `{apikey_value}`, `{environment_id}` y `{collection_id}` por sus valores.

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&natural_language_query=what is the basic mechanism of the transonic aileron buzz"
    ```
    {: pre}

    Este mandato devolverá resultados reclasificados utilizando el modelo que entrenó con anterioridad. Compare los resultados de esta búsqueda así como los resultados de algunas otras búsquedas que ha intentado con anterioridad. Puede ver algunas diferencias en los resultados si los compara con los que ve en {{site.data.keyword.retrieveandrankshort}}. Esto se debe a que algunas de las técnicas utilizadas para la búsqueda han cambiado para simplificar la experiencia y mejorar los resultados, sin embargo, globalmente la calidad de los resultados será similar.

Después de evaluar los resultados de búsqueda reclasificados, puede refinarlos en {{site.data.keyword.discoveryshort}} repitiendo el paso de cargar datos de entrenamiento adicionales con ejemplos y consultas de entrenamiento adicionales, y visualizando los resultados de las búsquedas.  También puede añadir documentos nuevos, tal como se describe en el primer paso, para ampliar el ámbito de la búsqueda. Del mismo modo que con {{site.data.keyword.retrieveandrankshort}}, la mejora en los resultados con el entrenamiento es un proceso iterativo.
