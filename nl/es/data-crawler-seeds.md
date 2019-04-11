---

copyright:
  years: 2015, 2017, 2019
lastupdated: "2019-01-28"

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

# Configuración del conector y las opciones de semilla
{: #configuring-connector-and-seed-options}

Al rastrear datos, el rastreador primero identifica el tipo de repositorio de datos (conector) y la ubicación inicial especificada por el usuario (semilla) para empezar a descargar información.
{: shortdesc}

Data Crawler solo debe utilizarse para rastrear comparticiones de archivos o bases de datos, en todos los demás casos debe utilizar el conector adecuado de {{site.data.keyword.discoveryshort}}. Consulte [Conexión a orígenes de datos](/docs/services/discovery?topic=discovery-sources#sources) para obtener más información. Ya no se proporciona asistencia para Data Crawler si lo está utilizando con un origen de datos soportado por los conectores de {{site.data.keyword.discoveryshort}}.
{: important}

**Importante:** Cuando se utiliza Data Crawler, los valores de seguridad del repositorio de datos se ignoran.

Las semillas son los puntos de partida de un rastreo. Data Crawler utiliza las semillas para recuperar datos del recurso que el conector identifica. Habitualmente, las semillas configuran URL para acceder a recursos basados en protocolos como, por ejemplo, comparticiones de archivos, comparticiones SMB, bases de datos y otros repositorios de bases de datos accesibles a través de dichos protocolos. Además, distintos URL de semilla tienen prestaciones distintas. Una semilla también puede ser específica de repositorio a fin de habilitar el rastreo de aplicaciones de terceros concretas como, por ejemplo, sistemas de gestión de relaciones con los clientes (CRM), sistemas de ciclo de vida de producto (PLC), sistemas de gestión de contenidos (CMS), aplicaciones basadas en la nube y aplicaciones de base de datos web.

Para rastrear los datos correctamente, debe asegurarse de que el rastreador está configurado correctamente para leer el repositorio de datos. Data Crawler proporciona conectores para dar soporte a la recopilación de datos desde los repositorios siguientes:

-   [Sistema de archivos](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-filesystem-crawl-options)
-   [Bases de datos, a través de JDBC](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-database-crawl-options)
-   [CMIS (Content Management Interoperability Services)](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-cmis-crawl-options)
-   [Comparticiones de archivos SMB (Server Message Block), CIFS (Common Internet Filesystem) o Samba](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#smb-cifs-samba-crawl-options)

También se proporciona una plantilla de configuración de conector que permite personalizar un conector.

Siga estos pasos para configurar su conector:

1.  Abra el archivo en el directorio `connectors` que corresponde al repositorio al que se va a conectar, por ejemplo `filesystem.conf` es el archivo de configuración para el conector para un sistema de archivos en un editor de texto.

1.  Modifique los valores que sean apropiados para su repositorio:

    -   [Sistema de archivos](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#filesystem-crawl-options)
    -   [Bases de datos, a través de JDBC](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#database-crawl-seed)
    -   [CMIS (Content Management Interoperability Services)](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#cmis-crawl-options)
    -   [Comparticiones de archivos SMB (Server Message Block), CIFS (Common Internet Filesystem) o Samba](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#smb-cifs-samba-crawl-options)
1.  Guarde y cierre el archivo.
1.  Haga lo mismo para el archivo `-seed.conf` en el directorio `connectors/seeds` que corresponde al repositorio al que se está conectando (por ejemplo `filesystem-seed.conf` es el archivo de configuración de semilla (a dónde conectarse para el conector del sistema de archivos)) en un editor de texto.
1.  Vaya a [configuración de Data Crawler para conectarse a {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-the-data-crawler).

Para acceder al manual en el producto para los archivos de configuración de semilla y el conector, con la información más reciente, escriba los siguientes mandatos desde el directorio de instalación del rastreador:
-   Para las opciones de configuración del conector:
    ```bash
    man crawler-options.conf
    ```
    {: pre}
-   Para las opciones de configuración de la semilla de rastreo:
    ```bash
    man crawler-seed.conf
    ```
    {: pre}


## Configuración de las opciones de rastreo del sistema de archivos
{: #filesystem-crawl-options}

El conector del sistema de archivos permite rastrear archivos locales respecto a la instalación de Data Crawler.

Otra opción para cargar un gran número de archivos en {{site.data.keyword.discoveryshort}} es [discovery-files ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/IBM/discovery-files){: new_window} en GitHub.
{: note}

### Configuración del conector del sistema de archivos
{: #filesystem-connector}

A continuación se indican las opciones de configuración básicas necesarias para usar el conector del sistema archivos. Para establecer estos valores, abra el archivo `config/connectors/filesystem.conf` y modifique los siguientes valores específicos de acuerdo con su caso:

-   **`protocol`** - Nombre del protocolo de conector usado en el rastreo. Use `sdk-fs` para este conector.
-   **`collection`** – Este atributo se utiliza para desempaquetar los archivos temporales. El valor predeterminado es `crawler-fs`
-   **`logging-config`** - Especifica el archivo usado para configurar las opciones de registro; tiene que formatearse como una cadena XML de `log4j`.
-   **`classname`** - Nombre de la clase Java del conector. El valor que tiene que usar este conector es `plugin:filesystem.plugin@filesystem`.

### Configuración de la semilla de rastreo para el sistema de archivos
{: #filesystem-crawl-seed}

Configure los siguientes valores para el archivo de semilla de rastreo para el sistema de archivos. Para configurar estos valores, abra el archivo `config/seeds/filesystem-seed.conf` y especifique los siguientes valores conforme a cada caso de uso concreto:

-   **`url`** - Lista separada por saltos de línea de los archivos y carpetas por rastrear. Los usuarios de UNIX pueden usar una vía como, por ejemplo, `/usr/local/`.

    **Nota:** Los URL deben empezar por `sdk-fs://`. Por ejemplo, para rastrear `/home/watson/mydocs`, el valor de este URL sería `sdk-fs:///home/watson/mydocs` - la tercera `/` es necesaria.

    Los sistemas de archivos utilizados por Linux, UNIX y otros sistemas basados en UNIX pueden contener tipos especiales de archivos como, por ejemplo, archivos y nodos de dispositivo de caracteres y bloque que representan conductos con nombre, y que no es posible rastrear porque no contienen datos, sino que sirven como puntos de acceso de E/S o como dispositivos. Se generarán errores si se intenta rastrear estos archivos. Para evitar estos errores, debería excluir el directorio `/dev` en cualquier rastreo de nivel superior en sistemas de archivos Linux, UNIX o similares a UNIX. Si están presentes en el sistema que está rastreando, también debe excluir directorios del sistema temporal como `/proc`, `/sys` y `/tmp` que contienen archivos temporales e información del sistema.   **`hops`** - Para uso interno exclusivamente.   **`default-allow`** - Para uso interno exclusivamente.
    {: tip}

## Configuración de opciones de rastreo de base de datos
{: #database-crawl}

El conector de base de datos permite rastrear una base de datos ejecutando un mandato SQL personalizado y creando un documento por fila (registro) y un elemento de contenido por columna (campo). Se puede especificar una columna para que se use como clave exclusiva, así como una columna que contenga una indicación de fecha y hora que represente la fecha de última modificación de cada registro. El conector recupera todos los registros de la base de datos especificada y también puede limitarse a determinadas tablas, uniones, etc. en la sentencia SQL.

El conector de base de datos permite rastrear las bases de datos siguientes:

-   {{site.data.keyword.IBM}} DB2
-   MySQL
-   Oracle PostgreSQL
-   Microsoft SQL Server
-   Sybase
-   Otras bases de datos compatibles con SQL a través del controlador compatible JDBC 3.0

El conector recupera todos los registros de la base de datos y la tabla especificadas.

***Controladores JDBC*** - El conector de base de datos se proporciona con el controlador Oracle JDBC (Java Database Connectivity) versión 1.5. Todos los controladores JDBC de terceros que se entregan con Data Crawler se encuentran en el directorio `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` de la instalación de Data Crawler donde, si es necesario, los puede añadir, eliminar o modificar. También se puede utilizar el valor de `extra_jars_dir` en el archivo `crawler.conf` para especificar otra ubicación.

***Controladores DB2 JDBC*** - Data Crawler no proporciona controladores JDBC para DB2 debido a restricciones con la licencia. Sin embargo, todas las instalaciones de DB2 en el que haya instalado el soporte a JDBC incluyen los archivos JAR que Data Crawler necesita a fin de poder rastrear una instalación de DB2. Para rastrear una instancia de DB2, debe copiar estos archivos en el directorio adecuado en la instalación de Data Crawler para que el conector de base de datos pueda utilizarlos. Para que Data Crawler rastree una instalación de DB2, localice los archivos JAR `db2jcc.jar` y de licencia (habitualmente, `db2jcc_license_cu.jar`) en su instalación de DB2, y copie estos archivos al subdirectorio `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` de su instalación de Data Crawler, o utilice valor `extra_jars_dir` en el archivo `crawler.conf` para especificar otra ubicación.

***Controladores MySQL JDBC*** - Data Crawler no proporciona controladores JDBC para MySQL debido a posibles restricciones con la licencia si se entregasen como parte del producto. Sin embargo, descargar el archivo JAR que contiene los controladores JDBC de MySQL e integrar el archivo JAR en su instalación de Data Crawler es muy fácil:

1.  Use un navegador web para visitar el sitio de descargas de MySQL y localice el enlace de descarga de fuentes y binarios del formato de archivo que desee utilizar (normalmente zip en sistemas Microsoft Windows o un archivo tar comprimido con gzip en sistemas Linux). Pulse en ese enlace para iniciar el proceso de descarga. Es posible que se tenga que registrar.
1.  Use el correspondiente mandato unzip archive-file-name o tar zxf archive-file-name para extraer el contenido del archivado en función del tipo y del nombre del archivo de archivado descargado.
1.  Cambie al directorio que se extrajo a partir del archivo de archivado y copie el archivo JAR desde este directorio al subdirectorio `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` del directorio de instalación de Data Crawler, o utilice el valor `extra_jars_dir` en el archivo `crawler.conf` para especificar otra ubicación.

### Configuración del conector de base de datos
{: #database-connector}

A continuación se indican las opciones de configuración básicas necesarias para usar el conector de base de datos. Para configurar estos valores, abra el archivo config/connectors/database.conf y modifique los siguientes valores conforme a cada caso de uso concreto:

-   **`protocol`** - Nombre del protocolo de conector usado en el rastreo. El valor de este conector se basa en el sistema de base de datos al que se accede.
-   **`collection`** – Este atributo se utiliza para desempaquetar los archivos temporales.
-   **`classname`** - Nombre de la clase Java del conector. El valor que tiene que usar este conector es `plugin:database.plugin@database`.
-   **`logging-config`** - Especifica el archivo usado para configurar las opciones de registro; tiene que formatearse como una cadena XML de `log4j`.

### Configuración de la semilla de rastreo para una base de datos
{: #database-crawl-seed}

Pueden configurarse los valores siguientes para el archivo semilla de rastreo de base de datos. Para configurar estos valores, abra el archivo `config/seeds/database-seed.conf` y especifique los siguientes valores conforme a cada caso de uso concreto:

-   **`url`** - El URL de la tabla o vista que hay que recuperar. Define el URL de semilla de base de datos SQL personalizado. La estructura es:

    -   `database-system://host:port/database?[per=num]&[sql=SQL]`

    Al probar un URL de semilla se mostrarán todos los URL en cola. Por ejemplo, si se prueba el siguiente URL de una base de datos que contiene 200 registros:
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?per=100&sql=select%20*%20from%20vessel&`

    Se mostrarán los URL en cola siguientes:
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=0&`
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=100&`
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=200&`

    Mientras que si se prueba el URL siguiente se mostrarán los datos recuperados de la fila 43:
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?per-1&key-val=43`
-   **`hops`** - Para uso interno exclusivamente.
-   **`default-allow`** - Para uso interno exclusivamente.
-   **`user-password`** - Credenciales del sistema de base de datos. El nombre de usuario y la contraseña deben separarse con dos puntos (`:`) y la contraseña debe cifrarse de forma utilizando el programa vcrypt que se distribuye con Data Crawler. Por ejemplo: `username:[[vcrypt/3]]passwordstring`
-   **`max-data-size`** - Tamaño máximo de los datos de un documento. Es el mayor bloque de memoria que se carga a la vez. Suba este límite solo si dispone de suficiente memoria en el sistema.
-   **`filter-exact-duplicates`** - Para uso interno exclusivamente.
-   **`timeout`** - Para uso interno exclusivamente.
-   **`jdbc-class`** (opción de ampliación) - Cuando se especifica, esta cadena sustituye la clase JDBC usada por el conector cuando se seleccione `(other)` (otro) como sistema de base de datos.
-   **`connection-string`** (opción de ampliación) - Cuando se especifica, esta cadena sustituye la cadena de conexión JDBC generada de forma automática. Esto permite proporcionar una configuración más detallada de la conexión de base de datos como, por ejemplo, el equilibrio de carga o las conexiones SSL. Por ejemplo: `jdbc:netezza://127.0.0.1:5480/databasename`
-   **`save-frequency-for-resume`** (opción de ampliación) - Especifica el nombre de una etiqueta asociada o columna para poder reanudar un rastreo o realizar una renovación parcial. La semilla guarda el nombre de esta columna a intervalos regulares a medida que progresa el rastreo y lo guarda de nuevo una vez rastreada que la última fila de la base de datos. Al reanudar o renovar el rastreo, este comienza con la fila que se identifica en el valor guardado para este campo.

## Configuración de opciones de rastreo de CMIS
{: #cmis-crawl-options}

El conector de CMIS (Content Management Interoperability Services) permite rastrear repositorios CMS (Content Management System) para CMIS como, por ejemplo, Alfresco, Documentum o {{site.data.keyword.IBM}} Content Manager así como indexar los datos que contienen.

### Configuración del conector de CMIS
{: #cmis-connector}

A continuación se indican las opciones de configuración básicas necesarias para usar el conector CMIS. Para configurar estos valores, abra el archivo `config/connectors/cmis.conf` y especifique los siguientes valores conforme a cada caso de uso concreto:

-   **`protocol`** - Nombre del protocolo de conector usado en el rastreo. El valor que tiene que usar este conector es `cmis`.
-   **`collection`** – Este atributo se utiliza para desempaquetar los archivos temporales.
-   **`dns`** - Opción no usada.
-   **`classname`** - Nombre de la clase Java del conector. Utilice `plugin:cmis-v1.1.plugin@connector` para este conector.
-   **`logging-config`** - Especifica el archivo usado para configurar las opciones de registro; tiene que formatearse como una cadena XML de `log4j`.
-   **`endpoint`** - URL del punto final de servicio de un repositorio compatible con CMIS. 
-   **`username`** - Nombre de usuario del repositorio CMIS que se usa para acceder al contenido. Este usuario debe tener acceso a todos los documentos y carpetas de destino que se van a rastrear e indexar.
-   **`password`** - Contraseña del repositorio de CMIS que se usa para acceder al contenido. La contraseña NO puede estar cifrada; hay que proporcionarla en texto legible.
-   **`repositoryid`** – ID de repositorio CMIS que se utiliza para acceder al contenido de un repositorio concreto.
-   **`bindingtype`** - Identifica qué tipo de enlace hay que usar para conectarse a un repositorio CMIS. El valor es AtomPub o WebServices.
-   **`authentication`** - Identifica qué tipo de mecanismo de autenticación se usa al conectar con un repositorio compatible con CMIS: Basic HTTP Authentication, NTLM o WS-Security(señal nombre_usuario).
-   **`enable-acl`** - Habilita la recuperación de las ACL de los datos rastreados. Si no le importa la seguridad de los documentos de esta recopilación puede inhabilitar esta opción, ya que aumentará el rendimiento al no solicitar esta información en el documento y no tener que recuperarla ni decodificarla. El valor puede ser true o false.
-   **`user-agent`** - Cabecera que se envía al servidor cuando se rastrean documentos.
-   **`method`** - Método (GET o POST) por el que se pasan los parámetros.
-   **`url-logging`** - Nivel de registro de los URL rastreados. Los valores posibles son:

    -   `full-logging` - Registra toda la información sobre el URL.
    -   `refined-logging` - Solo se registra la información necesaria para examinar el registro del rastreador y para que el conector funcione de forma correcta. Se trata del valor predeterminado.
    -   `minimal-logging` - Se registra el mínimo de información necesaria para que el conector funcione correctamente.

    Si se configura esta opción a `minimal-logging` se reducirá el tamaño de los registros y se obtendrá una ligera mejora de rendimiento gracias a la reducción de E/S que conlleva la minimización de la cantidad de datos registrados.
-   **`ssl-version`** - Especifica una versión de SSL para utilizar para conexiones HTTPS. De forma predeterminada, se utiliza el protocolo más fuerte
disponible.

### Configuración de la semilla de rastreo para CMIS
{: #cmis-crawl-seed}

Pueden configurarse los valores siguientes para el archivo de semilla de rastreo de CMIS. Para configurar estos valores, abra el archivo `config/seeds/cmis-seed.conf` y modifique los siguientes valores conforme a cada caso de uso concreto:

-   **`url`** - URL de una carpeta del repositorio de CMIS que se utilizará como punto de partida para el rastreo, por ejemplo: `cmis://alfresco.test.com:8080/alfresco/cmisatom?folderToProcess-workspace://SpacesStore/guid`

    Para rastrear la carpeta raíz, necesitará proporcionar un URL como el siguiente: `cmis://alfresco.test.com:8080/alfresco/cmisatom?folderToProcess-`
-   **`at`** - Opción no usada.
-   **`default-allow`** - Para uso interno exclusivamente.

## Configuración de opciones de rastreo de SMB/CIFS/Samba
{: #smb-cifs-samba-crawl-options}

El conector Samba permite rastrear comparticiones de archivos SMB (Server Message Block) y CIFS (Common Internet File System). Este tipo de compartición de archivos es común en las redes Windows y también se proporciona en el proyecto de código abierto Samba.

### Configuración del conector de Samba
{: #smb-cifs-samba-crawl-connector}

A continuación se indican las opciones de configuración básicas necesarias para usar el conector Samba. Para configurar estos valores, abra el archivo `config/connectors/samba.conf` y especifique los siguientes valores conforme a cada caso de uso concreto:

-   **`protocol`** - Nombre del protocolo de conector usado en el rastreo. El valor para usar este conector es smb.
-   **`collection`** – Este atributo se utiliza para desempaquetar los archivos temporales.
-   **`classname`** - Nombre de la clase Java del conector. El valor que tiene que usar este conector es `plugin:smb.plugin@connector`.
-   **`logging-config`** - Especifica el archivo usado para configurar las opciones de registro; tiene que formatearse como una cadena XML de `log4j`.
-   **`username`** - Nombre de usuario Samba con el que autenticar. Si se proporciona, también hay que proporcionar el dominio y la contraseña. Si no se proporciona, se utiliza la cuenta de invitado.
-   **`password`** - Contraseña Samba con la que autenticar. Si se proporciona el nombre de usuario, este valor es obligatorio. La contraseña tiene que cifrarse utilizando el programa vcrypt que se distribuye con Data Crawler.
-   **`archive`** - Permite que el conector Samba rastree e indexe los archivos comprimidos dentro de los archivos de archivado. El valor puede ser true o false. El valor predeterminado es false.
-   **`max-policies-per-handle`** - Especifica el número máximo de políticas Local Security Authority (LSA) que pueden abrirse para un único manejador RPC. Estas políticas definen los permisos de acceso necesarios para consultar o modificar un determinado sistema en diversas condiciones. El valor predeterminado de esta opción es 255.
-   **`crawl-fs-metadata`** - Activar esta opción hará que Data Crawler añada un documento VXML con los metadatos de sistema de archivos disponibles sobre el archivo (fecha de creación, fecha de última modificación, atributos de archivo, etc.).
-   **`enable-arc-connector`** - Opción no usada.
-   **`disable-indexes`** - Lista separada por saltos de línea de los índices que hay que inhabilitar, lo que puede acelerar el rastreo; por ejemplo:

    -   `disable-url-index`
    -   `disable-error-state-index`
    -   `disable-crawl-time-index`
-   **`exact-duplicates-hash-size`** - Define el tamaño de la tabla hash usada para resolver duplicados exactos. Tenga cuidado al modificar este número. El valor que seleccione tiene que ser primo y cuanto mayor sea el tamaño más rápidas serán las búsquedas, aunque requerirán más memoria, mientras que tamaños más pequeños pueden ralentizar los rastreos aunque a la vez reducir considerablemente el consumo de memoria.
-   **`user-agent`** - Opción no usada.
-   **`timeout`** - Opción no usada.
-   **`n-concurrent-requests`** - Número de solicitudes que se envían en paralelo a una única dirección IP. El valor predeterminado es `1`.
-   **`enqueue-persistence`** - Opción no usada.

### Configuración de la semilla de rastreo para Samba
{: #smb-cifs-samba-crawl-seed}

Los valores siguientes pueden configurarse para el archivo semilla de rastreo de Samba. Para configurar estos valores, abra el archivo `config/seeds/samba-seed.conf` y especifique los siguientes valores conforme a cada caso de uso concreto:

-   **`url`** - Lista de separada por saltos de línea de las comparticiones que hay que rastrear, por ejemplo:

    ```
    smb://share.test.com/office
    smb://share.test.com/cash/money/change
    smb://share.test.com/C$/Program Files
    ```
    {: codeblock}

-   **`hops`** - Para uso interno exclusivamente.
-   **`default-allow`** - Para uso interno exclusivamente.
