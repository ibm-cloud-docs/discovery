---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-02-28"

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

# Configuración de Data Crawler
{: #configuring-the-data-crawler}

Para configurar Data Crawler para que rastree su repositorio, debe especificar el adaptador de entrada adecuado en el archivo `crawler.conf` y después configurar la información específica del repositorio en los archivos de configuración del adaptador de entrada.
{: shortdesc}

Data Crawler solo debe utilizarse para rastrear comparticiones de archivos o bases de datos, en todos los demás casos debe utilizar el conector adecuado de {{site.data.keyword.discoveryshort}}. Consulte [Conexión a orígenes de datos](/docs/services/discovery?topic=discovery-sources#sources) para obtener más información. Ya no se proporciona asistencia para Data Crawler si lo está utilizando con un origen de datos soportado por los conectores de {{site.data.keyword.discoveryshort}}.
{: important}

Antes de realizar los cambios que se indican en estos pasos, asegúrese de que ha creado su directorio de trabajo copiando el contenido del directorio `{installation_directory}/share/examples/config` a un directorio de trabajo en su sistema, por ejemplo, `/home/config`.

**Importante:** No modifique directamente los archivos de ejemplo de configuración. Cópielos y luego edítelos. Si edita los archivos de ejemplo en la ubicación original, su configuración podría ser sobrescrita al actualizar Data Crawler, o ser eliminados al desinstalarlo.

**Nota:** Las referencias en esta guía a archivos en el directorio `config`, como por ejemplo `config/crawler.conf`, hacen referencia a dicho archivo en su directorio de trabajo y NO al directorio de `{installation_directory}/share/examples/config` instalado.

Los valores especificados son los predeterminados en `config/crawler.conf` y configuran el conector para el sistema de archivos:

1.  Abra el archivo `config/crawler.conf` en un editor de texto.

    -   Establezca la opción `crawl_config_file` en el `.conf` que modificó con anterioridad, por ejemplo: `connectors/filesystem.conf`.
    -   Establezca la opción `crawl_seed_file` en el `-seed.conf` que modificó con anterioridad, por ejemplo: `seeds/filesystem-seed.conf`.
    -   Configure la `class` `output_adapter` y las opciones de `config` para el servicio {{site.data.keyword.discoveryshort}} tal como se indica a continuación:

        ```
        class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

        config - "discovery_service"

        discovery_service {
          include "discovery/discovery_service.conf"
        }
        ```
        {: codeblock}

    Hay otros valores opcionales en este archivo que se podrían configurar según sea lo apropiado para su entorno, consulte: [Configuración de opciones de rastreo](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-crawl-options), [Configuración del adaptador de entrada](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#input-adapter), [Configuración del adaptador de salida](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#output-adapter) y [Opciones de gestión de rastreo adicionales](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#additional-crawl-management-options) para obtener información detallada sobre cómo establecer estos valores.

1.  Abra el archivo `discovery/discovery_service.conf` en un editor de texto. Modifique los siguientes valores específicos del servicio {{site.data.keyword.discoveryshort}} que ha creado anteriormente en {{site.data.keyword.Bluemix}}:

    -   `environment_id` - ID de entorno de servicio {{site.data.keyword.discoveryshort}}.
    -   `collection_id` - ID de recopilación de servicio {{site.data.keyword.discoveryshort}}.
    -   `configuration_id` - ID de configuración de servicio {{site.data.keyword.discoveryshort}}.
    -   `configuration` - Ubicación de vía de acceso completa del archivo `discovery_service.conf`, por ejemplo, `/home/config/discovery/discovery_service.conf`.
    -   `username` - Credencial de nombre de usuario para el servicio {{site.data.keyword.discoveryshort}}.
    -   `apikey` - Credencial para el servicio {{site.data.keyword.discoveryshort}}.

    Hay otros valores opcionales en este archivo que se pueden establecer según corresponda a su entorno. Consulte [Configuración de opciones de servicio](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-service-options) para obtener información sobre cómo establecer estos valores.

1.  Después de modificar estos archivos, estará listo para rastrear los datos. Vaya a [Rastreo de su repositorio de datos](/docs/services/discovery?topic=discovery-crawling-your-data-repository#crawling-your-data-repository) para continuar.

## Configuración de opciones de rastreo
{: #configuring-crawl-options}

El archivo `config/crawler.conf` contiene información que indica a Data Crawler qué archivos utilizar en su rastreo (adaptador de entrada), dónde enviar la recopilación de los archivos rastreados una vez éste se haya completado (adaptador de salida) así como otras opciones de gestión del rastreo.

**Nota:** Todas las vías de acceso son relativas al directorio `config` salvo que se indique lo contrario.

Para acceder al manual en el producto para el archivo `crawler.conf` con la información más reciente, escriba el siguiente mandato desde el directorio de instalación del rastreador:
`man crawler.conf`
{: tip}

Las opciones que se pueden establecer en este archivo son:

### Adaptador de entrada
{: #input-adapter}

-   **`class`** - Para uso interno exclusivamente. Define la clase del adaptador de entrada de Data Crawler. El valor predeterminado es: `com.ibm.watson.crawler.connectorframeworkinputadapter.Crawl`
-   **`config`** - Para uso interno exclusivamente. Define la configuración de la infraestructura del conector. La clave de configuración predeterminada dentro de este bloque para pasar al adaptador de entrada elegido es: `connector_framework`

    La infraestructura de conector es la entidad que permite interactuar con sus datos. Estos pueden ser datos internos dentro de la empresa o datos externos en la web o en la nube. Los siguientes conectores permiten acceder a diversos orígenes de datos, mientras la conexión propiamente dicha está controlada por el proceso de rastreo.

    **Importante:** Los datos recuperados por el adaptador de entrada de la infraestructura del conector se colocan en una caché local. No se guardan cifrados. De forma predeterminada, los datos se guardan en caché en un directorio temporal que debe limpiarse al rearrancar y que solo pueda ser leído por el usuario que ejecuta el mandato crawler.

    Existe una probabilidad de que este directorio sobreviva al rastreador si la infraestructura de conector se cae antes de poder realizar la limpieza. Tenga cuidado al elegir la ubicación de los datos guardados en caché; puede colocarlos en un sistema de archivos cifrado, pero tenga presente el impacto que ello tiene en el rendimiento. Es el usuario quien debe encontrar un equilibrio entre la seguridad y la velocidad para los rastreos.
-   **`crawl_config_file`** - Archivo de configuración que se usa en el rastreo. El valor predeterminado es: `connectors/filesystem.conf`.
-   **`crawl_seed_file`** - Archivo de semilla de rastreo que se usa en el rastreo. El valor predeterminado es: `seeds/filesystem-seed.conf`.
-   **`id_vcrypt_file`** - Archivo de claves utilizado por el rastreador para el cifrado de datos. La clave predeterminada incluida en el rastreador es `id_vcrypt`. Utilice el script vcrypt en la carpeta `bin` si necesita generar un nuevo archivo `id_vcrypt`.
-   **`crawler_temp_dir`** - Carpeta temporal del rastreador para guardar los registros de conector. Se proporciona el valor predeterminado, `tmp`. En caso de no existir, la carpeta `tmp` se creará en el directorio de trabajo actual.
-   **`extra_jars_dir`** - Añade un directorio de JAR adicionales a la vía de acceso de clases de la infraestructura de conector.

    **Nota:** Es relativa al directorio `lib/java` de la infraestructura de conector.

    -   Este valor debe ser `database` cuando se utiliza el conector de base de datos.

    Puede dejar este valor vacío (es decir, serie vacía "") cuando se utilicen otros conectores.

-   **`urls_to_filter`** - Lista negra de URL que no deberían rastrearse, con formato de expresión regular. Data Crawler no rastreará URL que coincidan con alguna de las expresiones regulares proporcionadas.

    `domain list` contiene los dominios que no se pueden rastrear. Añádalos si es necesario.

    `filetype list` contiene extensiones de archivo que el servicio de orquestación no admite.

    Elimine los tipos de archivo soportados de las expresiones regulares.

    Asegúrese de que el filtro permite su dominio de URL de semilla. Utilice un filtro vacío para el comportamiento `permitir todo`.

    Asegúrese de que no haya ningún filtro que excluya el URL de semilla, pues, de lo contrario, el rastreador podría colgarse.

-   **`max_text_size`** - Tamaño máximo, en bytes, que puede tener un documento antes de que la infraestructura de conector lo escriba en disco. Cuanto mayor es esta valor, menor es el número de documentos escritos en el disco, pero se incrementa el uso de la memoria. El valor predeterminado es `1048576`
-   **`extra_vm_params`** - Permite añadir parámetros Java al mandato utilizado para lanzar la infraestructura de conector.

-   **`bootstrap_logging`** - Registra el arranque de la infraestructura de conector; solo es útil en depuraciones avanzadas. Los valores posibles son `true` o `false`. El archivo de registro se escribirá en `crawler_temp_dir`.

-   **`read-timeout`** - Establece el tiempo (en segundos) que el rastreador esperará una respuesta de la infraestructura de conector. El valor predeterminado es 5 segundos.

### Adaptador de salida
{: #output-adapter}

-   **`class`** - Define la clase del adaptador de salida de Data Crawler.
-   **`config`** - Define qué clave de configuración se pasa al adaptador de salida. La serie debe corresponderse con una clave dentro de este objeto de configuración. En el ejemplo de código siguiente:

    ```
    class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

    config - "discovery_service"

    discovery_service {
        include "discovery/discovery_service.conf"
      }
    ```
    {: codeblock}

    La clave de configuración es `discovery_service`.

Hay que seleccionar un adaptador de salida especificando el parámetro `class` y la clave `config`.

-   Adaptador de salida de servicio **{{site.data.keyword.discoveryshort}}** - Carga los documentos explorados en el servicio {{site.data.keyword.discoveryfull}}. Seleccione este adaptador estableciendo el parámetro `class` y la clave `config` tal como se indica a continuación.

```
class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

config - "discovery_service"

discovery_service {
            include "discovery/discovery_service.conf"
          }
```
{: codeblock}

-   **Adaptador de salida de prueba** - El Adaptador de salida de prueba escribe una representación de los archivos rastreados en disco en una ubicación específica. Seleccione este adaptador estableciendo el parámetro `class` y la clave `config` tal como se indica a continuación.

    Un parámetro adicional, `output_directory`, selecciona el directorio en el que la representación de los datos rastreados deben escribirse.

```
class - "com.ibm.watson.crawler.testoutputadapter.TestOutputAdapter"

config - "test"

output_directory - "/tmp/crawler-test-output"`
```
{: codeblock}

-   **`retry`** - Especifica las opciones de reintento en caso de intentos fallidos de inyectar en el adaptador de salida.

    -   `max_attempts` - Número máximo de reintentos. El valor predeterminado es `10`
    -   `delay` - Retardo mínimo entre intentos, en segundos. El valor predeterminado es `2`
    -   `exponent_base` - Factor que determina el crecimiento del tiempo de retardo con cada intento fallido. El valor predeterminado es `2`

    La fórmula es:

        **`d(reinento_n) - retardo * (base_exponente ^ reintento_n)`**

    Por ejemplo, los valores predeterminados con un retardo de 1 segundo y una base de exponente 2, originará el segundo reintento, el tercer intento, retardarse 2 segundos en lugar de 1, y el siguiente retardo 4 segundos.

        `d(0) - 1 * (2 ^ 0)` - 1 segundo
        `d(1) - 1 * (2 ^ 1)` - 2 segundos
        `d(2) - 1 * (2 ^ 2)` - 4 segundos

    Por lo tanto, con los valores predeterminados, un envío se intentará hasta 10 veces, esperando aproximadamente 1022 segundos - un poco más de 17 minutos. Este tiempo es aproximado porque se añade tiempo para evitar la ejecución simultánea de varios reenvíos. Este tiempo aproximado puede variar hasta un 10%, de forma que el último reintento podría retrasarse hasta 7.7 segundos. El tiempo de espera no incluye el tiempo invertido en conectar con el servicio, en cargar los datos o en esperar una respuesta.

    El valor de `output_timeout` prevalece sobre el tiempo de espera aquí: si el tiempo total de espera de reintentos supera esta valor, el envío fallará incluso si se debería haber reintentado.
    {: tip}

### Opciones de gestión de rastreo adicionales
{: #additional-crawl-management-options}

-   **`full_node_debugging`** - Activa el modo de depuración. Los valores posibles son `true` y `false`.

    **Importante:** Esto colocará todos los datos de cada documento rastreado en los registros.   

-   **`logging.log4j.configuration_file`*** - Archivo de configuración utilizado para crear el registro. En el archivo de ejemplo `crawler.conf`, esta opción está definida en `logging.log4j` y su valor predeterminado es `log4j_custom.properties`. Esta opción debe definirse de manera similar cuando se usen archivos `.properties` o `.conf`.   
-   **`shutdown_timeout`** – Especifica el valor del tiempo de espera, en minutos, antes de que se concluya la aplicación. El valor predeterminado es `10`.   
-   **`output_limit`** - Número máximo de elementos indexables que el rastreador intenta enviar de forma simultánea al adaptador de salida. Puede limitarse adicionalmente con el número de núcleos disponibles para realizar el trabajo. Indica que, en cualquier momento dado, no habrá más de "x" elementos indexables enviados al adaptador en espera de devolución. El valor predeterminado es `10`.   
-   **`input_limit`** - Limita el número de URL que se pueden solicitar al mismo tiempo desde el adaptador de entrada. El valor predeterminado es `30`.   
-   **`output_timeout`** - Cantidad de tiempo, en segundos, antes de que Data Crawler renuncie a una solicitud para adaptador de salida y, a continuación, elimina el elemento de la cola del adaptador de salida para permitir continuar el proceso. El valor predeterminado es `1200`.

    Se deberían considerar las restricciones impuestas por el adaptador de salida, puesto que estas restricciones podrían estar relacionadas con los límites que aquí se definen. El valor de `output_limit` definido solo relaciona el número de objetos indexables que se pueden enviar al adaptador de salida al mismo tiempo. Una vez que un objeto indexable se envía al adaptador de salida, empieza a "contar el reloj" definido en la variable `output_timeout`. Puede que el propio adaptador de salida tenga un regulador que impida que pueda procesar todas las entradas que reciba. Por ejemplo, puede que el adaptador de salida de Orchestration tenga una agrupación de conexiones configurable para las conexiones HTTP del servicio. Si, por ejemplo, su valor predeterminado es 8 y se configura `output_limit` a un número mayor que 8, habrá procesos que estén esperando su turno para ejecutar y para los que esté contando el reloj. Puede que en tal caso se produzcan agotamientos del tiempo de espera.   
-   **`num_threads`** - Número de hebras que se pueden ejecutar a la vez. Este valor puede ser un entero, que especifica directamente el número de hebras, o puede ser una cadena con el formato `"xNUM"` que especifica el factor de multiplicación del número de procesadores disponibles, por ejemplo, `"x1.5"`. El valor predeterminado es `"30"`

## Configuración de opciones de servicio
{: #configuring-service-options}

El servicio {{site.data.keyword.discoveryshort}} indica al rastreador cómo gestionar archivos rastreados cuando se utiliza el servicio {{site.data.keyword.discoveryfull}}.

Para acceder al manual en el producto para el archivo `discovery-service.conf` con la información más reciente, escriba el siguiente mandato desde el directorio de instalación del rastreador:

  ```bash
  man discovery_service.conf
  ```
  {: pre}
{: tip}

Las opciones predeterminadas se pueden cambiar directamente abriendo el archivo `config/discovery/discovery_service.conf` y especificando los siguientes valores específicos para su caso concreto:

-   **`http_timeout`** – Tiempo de espera, en segundos, de la operación de lectura/indexación de documentos; el valor predeterminado es `125`.
-   **`proxy_host_port`** - (opcional) Cuando el rastreador se ejecuta detrás de un cortafuegos, podría necesitar establecer el nombre de host de proxy y el número de puerto de proxy para que el rastreador de datos se comunicase con el servicio {{site.data.keyword.discoveryshort}}. El valor predeterminado de esta opción es una serie vacía que deberá cambiar con un valor en el formato `"<host>:<port>"`.
-   **`concurrent_upload_connection_limit`** - Número de conexiones simultáneas permitidas para cargar documentos. El valor predeterminado es `2`.

    **Nota:** Cuando se utiliza el Adaptador de salida del servicio de orquestación, este valor debería ser mayor que, o igual a, el `output_limit` establecido al configurar las opciones de rastreo.   

-   **`base_url`** - URL al que se enviarán los documentos rastreados. Para el release actual del servicio {{site.data.keyword.discoveryshort}}, el valor es `https://gateway.watsonplatform.net/discovery/api`.   
-   **`environment_id`** - Ubicación de su recopilación de documentos rastreados en el URL base.   
-   **`collection_id`** - Nombre de la recopilación de documentos que configuró en el servicio {{site.data.keyword.discoveryshort}}.
-   **`api_version`** - Para uso interno exclusivamente. Fecha del último cambio de versión de la API.   
-   **`configuration_id`** - Nombre de archivo del archivo de configuración que utiliza el servicio {{site.data.keyword.discoveryshort}}.
-   **`apikey`** - Credencial para autenticar para la ubicación de su recopilación de documentos rastreados.

El Adaptador de salida del servicio {{site.data.keyword.discoveryshort}} puede enviar estadísticas con el propósito de que {{site.data.keyword.IBM}} entienda mejor a los usuarios y les pueda ofrecer un mejor servicio. Pueden configurarse las opciones siguientes para la variable `send_stats`:

-   **`jvm`** – Las estadísticas de la máquina virtual Java (JVM) enviadas incluyen el proveedor y la versión Java tal cual los notifica la propia JVM que se usa para ejecutar el rastreador de datos. El valor es `true` o `false`. El valor predeterminado es `true`.
-   **`os`** - Las estadísticas de sistema operativo (SO) enviadas incluyen el nombre, la versión y la arquitectura del SO tal y como los notifica la JVM usada para ejecutar el rastreador de datos. El valor es `true` o `false`. El valor predeterminado es `true`.
