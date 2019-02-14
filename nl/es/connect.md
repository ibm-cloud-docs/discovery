---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-14"

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

# Conexión a orígenes de datos
{: #sources}

El servicio {{site.data.keyword.discoveryshort}} le permite conectarse y rastrear documentos desde orígenes remotos.
{: shortdesc}

Puede conectarse a un origen de datos y extraer documentos de una planificación (si lo desea) en el servicio {{site.data.keyword.discoveryshort}} configurando una recopilación para asociarla con dicho origen. Cada recopilación se puede configurar con un origen de datos. El servicio {{site.data.keyword.discoveryshort}} extrae documentos del origen de datos utilizando un proceso denominado rastreo. El rastreo es el proceso de examinar y recuperar sistemáticamente documentos desde la ubicación de inicio especificada. El servicio {{site.data.keyword.discoveryshort}} solo rastrea los elementos especificados explícitamente por el usuario. Se pueden rastrear los tipos de orígenes de datos siguientes:

-  [Box](/docs/services/discovery/connect.html#connectbox)
-  [Salesforce](/docs/services/discovery/connect.html#connectsf)
-  [Microsoft SharePoint Online](/docs/services/discovery/connect.html#connectsp)

La conexión a un origen de datos se puede realizar utilizando la API o el conjunto de herramientas de {{site.data.keyword.discoveryshort}}. El conjunto de herramientas de {{site.data.keyword.discoveryshort}} proporciona un método simplificado de conexión que requiere menos comprensión de los sistemas de origen, y la API proporciona una interfaz más granular y configurable que requería una mayor comprensión del origen de datos al que se está conectando. La visión general del proceso siguiente le ayuda a descubrir qué secciones del documento debe leer a continuación:

1.  Lea los [Requisitos generales de origen](/docs/services/discovery/connect.html#gen_req) para obtener una visión general de lo que será necesario.
2.  Lea los requisitos específicos de su sistema de origen:
    -  [Box](/docs/services/discovery/connect.html#connectbox)
    -  [Salesforce](/docs/services/discovery/connect.html#connectsf)
    -  [Microsoft SharePoint Online](/docs/services/discovery/connect.html#connectsp)
3.  Lea las instrucciones de configuración de origen en función de la opción de configuración que haya elegido:
    -  [Utilización del conjunto de herramientas](/docs/services/discovery/connect.html#source_tooling)
    -  [Utilización de la API](/docs/services/discovery/connect.html#source_api)

## Requisitos generales del origen
{: #gen_req}

Se aplican los siguientes requisitos generales a todos los orígenes de datos:

-  El límite de tamaño del archivo de documento individual para Box, Salesforce y SharePoint Online es 10MB.
-  Necesitará las credenciales y las ubicaciones de archivo (o URL) de cada origen de datos, que normalmente proporciona un desarrollador o administrador del sistema del origen de datos.
-  Necesitará saber qué recursos del origen de datos va a rastrear. Esto lo puede proporcionar el administrador de orígenes. Cuando se rastrean Box o Salesforce, se muestra una lista de recursos disponibles al configurar un origen utilizando el conjunto de herramientas de {{site.data.keyword.discoveryshort}}.
-  El rastreo de un origen de datos utilizará recursos (llamadas de API) del origen de datos. El número de llamadas depende del número de documentos rastreados. Es necesario obtener un nivel de servicio adecuado (por ejemplo Empresa) para el origen de datos y el administrador del sistema de origen consultados.
-  {{site.data.keyword.discoveryshort}} puede ingerir los tipos de archivos siguientes y los demás tipos de documento se ignoran:
   -  Microsoft Word
   -  PDF
   -  HTML
   -  JSON
-  Los rastreos del origen de {{site.data.keyword.discoveryshort}} no suprimen documentos almacenados en una recopilación. Cuando se vuelve a rastrear un origen, se añaden nuevos documentos, los documentos actualizados se cambian a la versión actual y los documentos suprimidos permanecen con la última versión almacenada.

## Box
{: #connectbox}

Al conectarse a un origen de Box, asegúrese de que la instancia a la que tiene previsto conectarse sea un plan Empresa o superior.

Configuración de una cuenta de Box para que trabaje con {{site.data.keyword.discoveryshort}}:

1.  Cree una nueva aplicación personalizada en `https://app.box.com/developers/console` (utilice el URL de Box de la empresa).
1.  A continuación, realice una de las acciones siguientes:
    - Seleccione **Acceso de aplicación** de `Empresa` y, a continuación, siga utilizando los usuarios gestionados existentes.
      O
    - Seleccione **Acceso de aplicación** de `Aplicación` y cree un `Usuario de aplicación` con la aplicación que acaba de crear utilizando la [API de Box ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.box.com/reference#create-app-user){: new_window}.
1.  Habilite los **Ámbitos de aplicación** siguientes:
    - `Leer y escribir todas las carpetas almacenadas en Box`
    - `Gestionar Usuarios`
1.  Habilite las **características avanzadas** siguientes:
    - `Realizar acciones como usuarios`
    - `Generar señales de acceso de usuario`
1.  Solicite al administrador autorice el ID del cliente de aplicación `https://app.box.com/master/settings/openbox` escribiendo el `ID de cliente` de `https://app.box.com/developers/console` en el campo `Clave de API`.
1.  Genere el `par de claves público/privado` (se descargará en el sistema).
1.  Abra el archivo descargado y copie y pegue los campos en {{site.data.keyword.discoveryshort}}. Elimine el salto de línea `\n` al final de `privateKey` cuando lo copie en {{site.data.keyword.discoveryshort}}.

**Nota:** {{site.data.keyword.discoveryshort}} no ofrece soporte al rastreo de la misma aplicación personalizada (no se puede suplantar a sí mismo). 

Las credenciales siguientes son necesarias para conectarse a un origen de Box; deben obtenerse del administrador de Box (a menos que ya las haya obtenido configurando una aplicación personalizada de Box utilizando los pasos anteriores):

-  `client_id` - El valor `client_id` del origen en el que se conectan estas credenciales.    
-  `enterprise_id` - El valor `enterprise_id` del sitio de Box en el que se conectan estas credenciales.
-  `client_secret` - El valor `client_secret` del origen en el que se conectan estas credenciales. Este valor no se devuelve y solo se utiliza al crear o modificar credenciales.
-  `public_key_id` - El valor `public_key_id` del origen al que se conectan estas credenciales. Este valor no se devuelve y solo se utiliza al crear o modificar credenciales.
-  `private_key` - El valor `private_key` del origen en el que se conectan estas credenciales. Este valor no se devuelve y solo se utiliza al crear o modificar credenciales.
-  `passphrase` - El valor `passphrase` del origen en el que se conectan estas credenciales. Este valor no se devuelve y solo se utiliza al crear o modificar credenciales.

Al identificar las credenciales, puede resultar útil consultar la [documentación de desarrollador de Box ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.box.com/){: new_window}.

Otros elementos a tener en cuenta al rastrear Box:

-  Las notas de Box se almacenan en formato JSON, por lo que {{site.data.keyword.discoveryshort}} ingerirá las notas de Box de las carpetas especificadas.
-  Al utilizar la API, necesitará una lista de los ID de carpeta y el ID de propietario asociado para cada carpeta que desee rastrear. El conjunto de herramientas de {{site.data.keyword.discoveryshort}} le permite examinar y seleccionar el contenido que se va a rastrear.

## Salesforce
{: #connectsf}

Al conectarse a un origen de Salesforce, asegúrese de que la instancia en la que tiene previsto conectarse es un plan Empresa o superior.

Las credenciales siguientes son necesarias para conectarse a un origen de Salesforce, deben obtenerse del administrador de Salesforce:
-  `url` - El valor `url` del origen en el que se conectan estas credenciales.
-  `username` - El valor `username` del origen en el que se conectan estas credenciales.
-  `password` - El valor `password` consiste en la contraseña de Salesforce y una señal de seguridad de Salesforce concatenada válida. Este valor no se devuelve y solo se utiliza al crear o modificar credenciales.

Al identificar las credenciales, puede resultar útil consultar la [documentación de desarrollador de Salesforce ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.salesforce.com/docs/){: new_window}.

Otros elementos a tener en cuenta al rastrear Salesforce:

-  Los artículos de conocimiento solo se rastrean si la **versión** se `publica` y el idioma es `en-us`.
-  Al utilizar la API, necesitará una lista de los objetos de Salesforce que desee rastrear. El conjunto de herramientas de {{site.data.keyword.discoveryshort}} le permite examinar y seleccionar el contenido que se va a rastrear.


## SharePoint Online
{: #connectsp}

Al conectarse a un origen de Microsoft SharePoint Online, asegúrese de que la instancia en la que tiene previsto conectarse es un plan Empresa (E1) o superior.

Las credenciales siguientes son necesarias para conectarse a un origen de SharePoint Online deben obtenerse del administrador de SharePoint:

-  `organization_url` - El valor `organization_url` del origen en el que se conectan estas credenciales.
-  `site_collection.path` - El valor `site_collection.path` del origen en el que se conectan estas credenciales.
-  `username` - El valor `client_id` del origen en el que se conectan estas credenciales.
-  `password` - El valor `password` del origen en el que se conectan estas credenciales. Este valor no se devuelve y solo se utiliza al crear o modificar credenciales.

Al identificar las credenciales, puede resultar útil consultar la [documentación de desarrollador de Microsoft SharePoint![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.microsoft.com/en-us/sharepoint/dev/){: new_window}.

Otros elementos a tener en cuenta al rastrear Microsoft SharePoint Online:

-  Al rastrear SharePoint, necesitará una lista de las vías de acceso de recopilación del sitio de SharePoint que desee rastrear. El conjunto de herramientas de {{site.data.keyword.discoveryshort}} le permite examinar y seleccionar el contenido que se va a rastrear. Para rastrear el sitio de SharePoint Online completo, no seleccione varias vías de acceso (URL) en el campo. En este caso de ejemplo, especifique `/` en el campo `site_collection.path`.

## Utilización del conjunto de herramientas
{: #source_tooling}

La conexión a un origen de datos utilizando el conjunto de herramientas de {{site.data.keyword.discoveryshort}} se realiza creando una recopilación específica para un origen. Realice los pasos siguientes para crear una recopilación de origen y rastrearla:

1.  En la página **Gestionar datos** del conjunto de herramientas de {{site.data.keyword.discoveryshort}}, seleccione **Conectar un origen de datos**.
2.  Seleccione el origen de datos en el que desea conectarse.
3.  Escriba las credenciales del origen y pulse Conectar. Las credenciales del origen las proporciona el administrador del sistema de origen.
4.  Seleccione los datos que desea para el rastreo y la frecuencia con la que desea sincronizarlos.
5.  Pulse **Guardar y sincronizar objetos** para empezar a rastrear el origen de datos. A continuación, se le redirigirá a la pantalla de estado de recopilación que se actualiza a medida que se añaden documentos a la recopilación.

El rastreo sincronizará los datos inicialmente y luego en la frecuencia que ha especificado.
**Nota:** Si modifica cualquier valor en la pantalla **Valores de sincronización** y pulsa **Guardar y sincronizar objetos**, se iniciará un rastreo (o se reiniciará si ya se está ejecutando) en ese momento.

## Utilización de la API
{: #source_api}

Utilice el proceso siguiente para crear una recopilación conectada a un origen de datos utilizando la API.
1.  Cree credenciales para el origen de datos al que se está conectando utilizando la [API de credenciales de origen![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#credentials-api){: new_window}. Registre el valor **credential_id** devuelto de las credenciales que acaba de crear.
2.  Cree una nueva configuración utilizando la [API de configuración![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#configurations-api){: new_window}. Esta configuración debe contener un objeto de **origen** que defina lo que se debe rastrear. El objeto de **origen** debe contener el valor **credential_id** que ha registrado anteriormente.
    ```json
    "source" : {
      "type" : "salesforce",
      "credential_id" : "{credential_id}",
      "schedule" : {
        "enabled" : true,
        "time_zone" : "America/New_York",
        "frequency" : "weekly"
      },
      "options" : {
         "site_collections" : [ {
         "site_collection_path" : "/sites/TestSiteA",
         "limit" : 10
         } ]
      }
    }
    ```
    {: codeblock}
    Registre el valor **configuration_id** devuelto de la configuración que acaba de crear.
3.  Cree una nueva recopilación utilizando la [API de recopilaciones![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#configurations-api){: new_window}. El objeto que define la recopilación debe contener el valor **configuration_id** que ha registrado anteriormente.

El rastreo de origen comienza en cuanto se crea la recopilación y, de nuevo, se inicia en la frecuencia que ha especificado.
**Nota:** Si modifica cualquier valor en el objeto de **origen** de la configuración, se iniciará un nuevo rastreo (o se reiniciará si ya se está ejecutando) en ese momento.

## Especificación de `customer_id`
{:# source_customer_id}

Se puede utilizar un campo `customer_id` en el documento de {{site.data.keyword.discoveryshort}} ingerido para suprimir el contenido en función del valor `customer_id` utilizando el método **user-data** en la API. El valor `customer_id` no se asigna automáticamente a los documentos entrantes de un origen de datos cuando se ingieren. Si la aplicación requiere que se defina un `customer_id`, puede especificar uno (o varios) de los campos de entrada del sistema de origen que debe copiarse y utilizarse como `customer_id`. Para ello, debe modificar la configuración que se está utilizando para conectarse al origen.

1.  Realice una consulta de ejemplo e identifiqué el campo que desea utilizar como `customer_id`.
2.  Modifique la configuración. Deberá añadir la sección **Normalización** para poder crear el campo `customer_id`.
    -  En el conjunto de herramientas, navegue hasta la recopilación y pulse el enlace **editar** en la sección de configuración. A continuación, pulse el separador **Normalización** para añadir una normalización de **copia** para crear el campo `customer_id`. Pulse **Aplicar y guardar**.
    ![Normalización de copia](images/norm_copy.png)
    -  Cuando utilice la API, añada el objeto siguiente a la matriz **normalizaciones**"
       ```json
    {
         "operation" : "copy",
         "source_field" : "{original_field_name}",
         "destination_field" : "customer_id"
       }
       ```
       {: codeblock}
3.  El siguiente rastreo planificado agregará el campo `customer_id` a todos los documentos. Si desea que un rastreo se inicie inmediatamente, modifique la configuración de origen (**Valores de sincronización** en el conjunto de herramientas).

Consulte [Seguridad de la información![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.bluemix.net/docs/services/discovery/information-security.html){: new_window} para obtener información e información sobre la supresión basada en `customer_id`.
