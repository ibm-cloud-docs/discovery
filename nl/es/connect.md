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

# Conexión a orígenes de datos
{: #sources}

El servicio {{site.data.keyword.discoveryshort}} le permite conectarse y rastrear documentos desde orígenes remotos.
{: shortdesc}

Puede conectarse a un origen de datos y extraer documentos de una planificación (si lo desea) en el servicio {{site.data.keyword.discoveryshort}} configurando una recopilación para asociarla con dicho origen. Cada recopilación se puede configurar con un origen de datos si se utiliza el conjunto de herramientas de {{site.data.keyword.discoveryshort}}; si se utiliza la API, puede enviar documentos desde varios orígenes de datos a una única recopilación. El servicio {{site.data.keyword.discoveryshort}} extrae documentos del origen de datos utilizando un proceso denominado rastreo. El rastreo es el proceso de examinar y recuperar sistemáticamente documentos desde la ubicación de inicio especificada. El servicio {{site.data.keyword.discoveryshort}} solo rastrea los elementos especificados explícitamente por el usuario. Se pueden rastrear los tipos de orígenes de datos siguientes:

-  [Box](/docs/services/discovery?topic=discovery-sources#connectbox)
-  [Salesforce](/docs/services/discovery?topic=discovery-sources#connectsf)
-  [Microsoft SharePoint Online](/docs/services/discovery?topic=discovery-sources#connectsp)
-  [Microsoft SharePoint 2016 On-Premise](/docs/services/discovery?topic=discovery-sources#connectsp_op)
-  [Rastreo web](/docs/services/discovery?topic=discovery-sources#connectwebcrawl) (beta)
-  [IBM Cloud Object Storage](/docs/services/discovery?topic=discovery-sources#connectcos)

La conexión a un origen de datos se puede realizar utilizando la API o el conjunto de herramientas de {{site.data.keyword.discoveryshort}}. El conjunto de herramientas de {{site.data.keyword.discoveryshort}} proporciona un método simplificado de conexión que requiere menos comprensión de los sistemas de origen, y la API proporciona una interfaz más granular y configurable que requería una mayor comprensión del origen de datos al que se está conectando. La visión general del proceso siguiente le ayuda a descubrir qué secciones del documento debe leer a continuación:

1.  Lea los [Requisitos generales de origen](/docs/services/discovery?topic=discovery-sources#gen_req) para obtener una visión general de lo que será necesario.
2.  Lea los requisitos específicos de su sistema de origen:
    -  [Box](/docs/services/discovery?topic=discovery-sources#connectbox)
    -  [Salesforce](/docs/services/discovery?topic=discovery-sources#connectsf)
    -  [Microsoft SharePoint Online](/docs/services/discovery?topic=discovery-sources#connectsp)
    -  [Microsoft SharePoint 2016 On-Premise](/docs/services/discovery?topic=discovery-sources#connectsp_op)
    -  [Rastreo web](/docs/services/discovery?topic=discovery-sources#connectwebcrawl) (beta)
    -  [IBM Cloud Object Storage](/docs/services/discovery?topic=discovery-sources#connectcos)
3.  Lea las instrucciones de configuración de origen en función de la opción de configuración que haya elegido:
    -  [Utilización del conjunto de herramientas](/docs/services/discovery?topic=discovery-sources#source_tooling)
    -  [Utilización de la API](/docs/services/discovery?topic=discovery-sources#source_api)

Si selecciona un origen de datos local, primero debe instalar y configurar IBM Secure Gateway. Consulte [Instalación de IBM Secure Gateway para datos locales](/docs/services/discovery?topic=discovery-sources#gateway) para obtener más información.

## Requisitos generales del origen
{: #gen_req}

Se aplican los siguientes requisitos generales a todos los orígenes de datos:

-  El límite de tamaño del archivo de documento individual para Box, Salesforce, SharePoint Online, SharePoint 2016, IBM Cloud Object Storage y el rastreo web es 10 MB.
-  Necesitará las credenciales y las ubicaciones de archivo (o URL) de cada origen de datos, que normalmente proporciona un desarrollador o administrador del sistema del origen de datos.
-  Necesitará saber qué recursos del origen de datos va a rastrear. Esto lo puede proporcionar el administrador de orígenes. Cuando se rastrean Box o Salesforce, se muestra una lista de recursos disponibles al configurar un origen utilizando el conjunto de herramientas de {{site.data.keyword.discoveryshort}}.
-  Si se utiliza el conjunto de herramientas de {{site.data.keyword.discoveryshort}}, se puede configurar una recopilación con un solo origen de datos. Si se utiliza la API, los documentos de varios orígenes de datos se pueden enviar a una única recopilación.
-  El rastreo de un origen de datos utilizará recursos (llamadas de API) del origen de datos. El número de llamadas de API depende del número de documentos que deben rastrearse. Es necesario obtener una licencia de nivel de servicio adecuado (por ejemplo Empresa) para el origen de datos y el administrador del sistema de origen consultados.
-  Los rastreos del origen de {{site.data.keyword.discoveryshort}} no suprimen documentos almacenados en una recopilación. Cuando se vuelve a rastrear un origen, se añaden nuevos documentos, los documentos actualizados se cambian a la versión actual y los documentos suprimidos permanecen con la última versión almacenada.
-  {{site.data.keyword.discoveryshort}} puede ingerir los tipos de archivos siguientes y los demás tipos de documento se ignoran:

Recopilación | Planes Lite | Planes Avanzados 
---------------- | ------------------------------ | ------------------------------------------- 
Recopilaciones existentes creadas específicamente para {{site.data.keyword.discoveryfull}} antes de la publicación de la [Comprensión de documentos inteligentes (SDU)](/docs/services/discovery?topic=discovery-release-notes#22jan19) | Microsoft Word, PDF, HTML, JSON | Microsoft Word, PDF, HTML, JSON     
Recopilaciones creadas tras el release de [SDU](/docs/services/discovery?topic=discovery-sdu#sdu) | PDF, Word, PowerPoint, Excel, JSON\*, HTML\* | PDF, Word, PowerPoint, Excel, PNG\*\*, TIFF\*\*, JPG\*\*, JSON\*, HTML\* 
    
\* {{site.data.keyword.discoveryfull}} soporta documentos JSON y HTML, pero estos no se pueden editar con el editor de SDU. Para cambiar la configuración de los documentos HTML y JSON, debe utilizar la API. Para obtener más información, consulte la [Referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery/){: new_window}.

\*\* Se exploran los archivos de imagen individuales (PNG, TIFF, JPG) y se extrae el texto (si lo hay). También se explorarán las imágenes PNG, TIFF y JPEG incluidas en archivos PDF, Word, PowerPoint y Excel, y se extraerá el texto (si lo hay).

## Box
{: #connectbox}

Necesitará crear una nueva aplicación personalizada de Box para conectarse a {{site.data.keyword.discoveryfull}}. La aplicación de Box que cree debe tener acceso de nivel de empresa o de nivel de aplicación.

-  Si no es el administrador de Box de la organización, se recomienda el acceso a [**nivel de aplicación**](/docs/services/discovery?topic=discovery-sources#applevelbox). Necesitará un administrador para aprobar la aplicación.
-  Si es el administrador de Box de la organización, se recomienda el acceso a [**nivel de empresa**](/docs/services/discovery?topic=discovery-sources#entlevelbox).

Los pasos para configurar el acceso de Box pueden cambiar si hay una actualización de Box. Consulte la [documentación de desarrollador de Box ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.box.com/){: new_window} para ver las actualizaciones.
{: note}

### Configuración del acceso a nivel de aplicación
{: #applevelbox}

1.   Vaya a `https://app.box.com/developers/console` (utilice el URL de Box de la empresa) y pulse **Crear nueva app**.
1.   En la pantalla **Crear nueva app**, seleccione **Integración empresarial** y pulse **Siguiente**.
1.   En la pantalla **Método de autenticación**, seleccione **OAuth 2.0 con JWT (autenticación de servidor)** y pulse **Siguiente**.
1.   Asigne un nombre a la app y pulse el botón **Crear app**. Una vez que se haya creado la app de Box, pulse **Ver la app**.
1.   Al visualizar la app, seleccione **Acceso de aplicación** como **Aplicación**. Puede utilizar los usuarios gestionados existentes para continuar, no es necesario que cree usuarios nuevos.
1.   Desplácese hacia abajo hasta la sección **Ámbitos de aplicación** de la página y habilite los recuadros de selección siguientes: 
     - `Leer y escribir todas las carpetas almacenadas en Box`
     - `Gestionar Usuarios`
1.   Desplácese hacia abajo hasta la sección **Características avanzadas** y habilite los conmutadores siguientes:
     - `Realizar acciones como usuarios`
     - `Generar señales de acceso de usuario` 
1.  Pulse el botón **Guardar cambios**.

En los pasos siguientes es necesaria la ayuda del administrador de la cuenta de Box de la organización. Si no es el administrador de Box de la organización, puede identificar al administrador abriendo la consola del desarrollador de Box y buscando en **Valores de cuenta** > **Detalles de cuenta** > **Valores**.

1.  [Paso de administrador] Autorice el id de cliente de aplicaciones en `https://app.box.com/master/settings/openbox` pulsando el botón **Autorizar nueva app**.
1.  [Paso de administrador] Escriba el **ID de cliente** de `https://app.box.com/developers/console` en el campo **clave de API** y, a continuación, pulse el botón **Autorizar**.
1.  [Paso de administrador] Recupere una señal de desarrollador para la aplicación. Para ello, vaya a `https://app.box.com/developers/console`, desplácese a la sección **Señal de desarrollador** y genere la señal.
1.  Ahora que la aplicación ha sido autorizada por el administrador, vaya a `https://developer.box.com/reference#page-create-an-enterprise-user` y cree un usuario de app utilizando la página de referencia de la API.

   Ejemplo de curl para crear un usuario de app:

   ```bash
    curl https://api.box.com/2.0/users -H "Authorization: Bearer ACCESS_TOKEN" -d '{"name": "NedStark", "is_platform_access_only": true}' -X POST
   ```
   {: pre}

1.  Copie el contenido del campo **id** recién generado y proporciónelo al usuario no administrador que va a conectar la aplicación de Box a {{site.data.keyword.discoveryfull}}.
1.  Una vez que se haya creado el usuario de app, las carpetas que desee rastrear se deben compartir con el usuario de la app, y el usuario de la app debe tener permisos de `Visor` en esas carpetas. Para ello, es necesario el nombre de inicio de sesión del usuario de app de la respuesta del mandato curl anterior. Ejemplo:`"login":"AppUser_737729_jmUo@boxdevedition.com"`.
1.  Vuelva a la consola del desarrollador de Box `https://app.box.com/developers/console` y desplácese a la sección **Añadir y gestionar claves públicas**. Pulse **Generar el par de claves público/privado** y descargue el archivo del par de claves. Abra el archivo.
1.  Desde el archivo del par de claves, corte y pegue los campos siguientes en el conjunto de herramientas de {{site.data.keyword.discoveryshort}}.
    -  `client_id`
    -  `enterprise_id`
    -  `client_secret` 
    -  `public_key_id` 
    -  `private_key` 
    -  `passphrase` 

### Configuración del acceso a nivel de empresa
{: #entlevelbox}

1.  Vaya a `https://app.box.com/developers/console` (utilice el URL de Box de la empresa) y pulse **Crear nueva app**.
1.  En la pantalla **Crear nueva app**, seleccione **Integración empresarial** y pulse **Siguiente**.
1.  En la pantalla **Método de autenticación**, seleccione **OAuth 2.0 con JWT (autenticación de servidor)** y pulse **Siguiente**.
1.  Asigne un nombre a la app y pulse el botón **Crear app**. Una vez que se haya creado la app de Box, pulse **Ver la app**.
1.  Al visualizar la app, seleccione **Acceso de aplicación** como **Empresa**. Puede utilizar los usuarios gestionados existentes para continuar, no es necesario que cree usuarios nuevos.
1.  Desplácese hacia abajo hasta la sección **Ámbitos de aplicación** de la página y habilite los recuadros de selección siguientes: 
    - `Leer y escribir todas las carpetas almacenadas en Box`
    - `Gestionar Usuarios`
    - `Gestionar propiedades de empresa`
1.  Desplácese hacia abajo hasta la sección **Características avanzadas** y habilite los conmutadores siguientes:
    - `Realizar acciones como usuarios`
    - `Generar señales de acceso de usuario` 
1.  Pulse el botón **Guardar cambios**.

`Renovar` sólo está soportado con el acceso de nivel de empresa.
{: note}

Si cambia los valores de app de Box, `vuelva a autorizar` la app para que los cambios entren en vigor.
{: tip}

En los pasos siguientes es necesaria la ayuda del administrador de la cuenta de Box de la organización. Si no es el administrador de Box de la organización, puede identificar al administrador abriendo la consola del desarrollador de Box y buscando en **Valores de cuenta** > **Detalles de cuenta** > **Valores**.

1.  [Paso de administrador] Autorice el id de cliente de aplicaciones navegando a **Consola de administración** > **Valores de empresa** > **Apps** y desplazándose a `Aplicaciones personalizadas`. URL de ejemplo:`https://app.box.com/master/settings/openbox`.
1.  [Paso de administrador] Escriba el **ID de cliente** de `https://app.box.com/developers/console` en el campo **clave de API** y, a continuación, pulse el botón **Autorizar**.
1.  Vuelva a la consola del desarrollador de Box `https://app.box.com/developers/console` y desplácese a la sección **Añadir y gestionar claves públicas**. Pulse **Generar el par de claves público/privado** y descargue el archivo del par de claves. Abra el archivo.
1.  Desde el archivo del par de claves, corte y pegue los campos siguientes en el conjunto de herramientas de {{site.data.keyword.discoveryshort}}.
    -  `client_id`
    -  `enterprise_id`
    -  `client_secret` 
    -  `public_key_id` 
    -  `private_key` 
    -  `passphrase` 

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
-  `site_collection_path` - El valor `site_collection_path` del origen en el que se conectan estas credenciales.
-  `username` - El valor `client_id` del origen en el que se conectan estas credenciales. Este usuario debe tener acceso a todos los sitios y las listas que se deben rastrear e indexar.
-  `password` - El valor `password` del origen en el que se conectan estas credenciales. Este valor no se devuelve y solo se utiliza al crear o modificar credenciales.

Al identificar las credenciales, puede resultar útil consultar la [documentación de desarrollador de Microsoft SharePoint ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.microsoft.com/en-us/sharepoint/dev/){: new_window}.

Otros elementos a tener en cuenta al rastrear Microsoft SharePoint Online:

-  Para rastrear SharePoint, la cuenta de `usuario de rastreo` debe tener permisos de `Administrador de recopilación del sitio`.
-  Al rastrear SharePoint, necesitará la lista de las vías de acceso de recopilación del sitio de SharePoint que desee rastrear. {{site.data.keyword.discoveryshort}} no admite vías de acceso a carpeta como entrada.

## Rastreo web
{: #connectwebcrawl}

Esta característica beta se puede utilizar para rastrear sitios web públicos que no requieren contraseña. Puede seleccionar la frecuencia con la que desea que {{site.data.keyword.discoveryshort}} se sincronice con los sitios web, el idioma y el número de saltos.

-  `Sincronizar los datos`: puede elegir sincronizar cada 5 minutos, cada hora, a diario, semanalmente o mensualmente. 
-  `Seleccionar idioma`: escoja el idioma de los sitios web en la lista de idiomas soportados. Consulte [Soporte de idiomas](/docs/services/discovery?topic=discovery-language-support#supported-languages) para obtener la lista de idiomas admitidos por {{site.data.keyword.discoveryshort}}. Se recomienda crear una colección por separado para cada idioma.
-  `Grupo de URL a sincronizar`: especifique el URL y pulse el signo más para añadirlo al grupo de URL. Para especificar los **valores de rastreo** de este grupo de URL, pulse el icono ![Rueda](images/icon_settings.png). Puede establecer el **Número máximo de saltos**, que es el número de enlaces consecutivos que hay que seguir desde el URL de inicio (el URL de inicio es `0`). El número predeterminado de saltos es `2`, y el máximo es `20` (si se utiliza la API, el máximo es `1000`). 

Para este release beta, el número de páginas web rastreadas es limitado, por lo que el rastreador web puede no rastrear todos los sitios web especificados y alcanzar el número máximo de saltos.
{: note}

Si necesita distintos **Valores de rastreo** para otros URL, pulse **Añadir grupo de URL** y cree un nuevo grupo. Puede crear tantos grupos de URL como necesite.
{: tip}

## SharePoint 2016 On-Premise
{: #connectsp_op}

Microsoft SharePoint 2016 (también conocido como SharePoint Server 2016) es un origen de datos local. Para conectarse a él, primero debe instalar y configurar IBM Secure Gateway. Consulte [Instalación de IBM Secure Gateway para datos locales](/docs/services/discovery?topic=discovery-sources#gateway) para obtener más información.
{: note}

Las credenciales siguientes son necesarias para conectarse a un origen de SharePoint 2016 y deben obtenerse del administrador de SharePoint:

-  `username` - El valor `client_id` del origen en el que se conectan estas credenciales. Este usuario debe tener acceso a todos los sitios y las listas que se deben rastrear e indexar.
-  `password` - El valor `password` del origen en el que se conectan estas credenciales. Este valor no se devuelve y solo se utiliza al crear o modificar credenciales.
-  `web_application_url` - El valor `web_application_url` de SharePoint 2016; por ejemplo, https://sharepointwebapp.com:8443. Si no se proporciona el puerto, toma como valor predeterminado el puerto `80` para http y el puerto `443` para https.
-  `domain` - El valor `domain` de la cuenta de SharePoint 2016.

Al identificar las credenciales, puede resultar útil consultar la [documentación de desarrollador de Microsoft SharePoint ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.microsoft.com/en-us/sharepoint/dev/){: new_window}.

Otros elementos a tener en cuenta al rastrear Microsoft SharePoint 2016:

-  Para rastrear SharePoint 2016, la cuenta de `usuario de rastreo` debe tener permisos de `Administrador de recopilación del sitio`.
-  Al rastrear SharePoint, necesitará la lista de las vías de acceso de recopilación del sitio de SharePoint que desee rastrear. {{site.data.keyword.discoveryshort}} no admite vías de acceso a carpeta como entrada.

## IBM Cloud Object Storage
{: #connectcos}

Cuando se conecta a un origen de IBM Cloud Object Storage, son necesarias las credenciales siguientes. Se deben obtener de su administrador de IBM Cloud Object Storage:

-  `endpoint` - El valor `endpoint` utilizado para interactuar con los datos de IBM Cloud Object Storage.
-  `access_key_id` - El valor `access_key_id` obtenido cuando se creó la instancia de IBM Cloud Object Storage.
-  `secret_access_key` - El valor `secret_access_key` para firmar las solicitudes obtenidas cuando se creó la instancia de IBM Cloud Object Storage.

Después de indicar esta información, puede elegir la frecuencia con la que desea sincronizar los datos y seleccionar los grupos que desea sincronizar.

Otros elementos a tener en cuenta al rastrear IBM Cloud Object Storage:

-  Este conector no es compatible con el rastreo de puntos finales privados.
-  Hay un pequeño problema de rendimiento si se seleccionan todos los grupos. En ese caso, se puede retrasar la indexación de los documentos.

## Utilización del conjunto de herramientas
{: #source_tooling}

La conexión a un origen de datos utilizando el conjunto de herramientas de {{site.data.keyword.discoveryshort}} se realiza creando una recopilación específica para un origen. Realice los pasos siguientes para crear una recopilación de origen y rastrearla:

1.  En la página **Gestionar datos** del conjunto de herramientas de {{site.data.keyword.discoveryshort}}, seleccione **Conectar un origen de datos**.
2.  Seleccione el origen de datos en el que desea conectarse. Si ha seleccionado un origen de datos local, primero tendrá que instalar IBM Secure Gateway; consulte [Instalación de IBM Secure Gateway para datos locales](/docs/services/discovery?topic=discovery-sources#gateway) para obtener más información. 
3.  Escriba las credenciales del origen y pulse Conectar. Las credenciales del origen las proporciona el administrador del sistema de origen.
4.  Seleccione los datos que desea para el rastreo y la frecuencia con la que desea sincronizarlos. Opciones de sincronización:
    -  Cada cinco minutos: se ejecuta cada cinco minutos
    -  Cada hora: se ejecuta cada hora
    -  A diario: se ejecuta todos los días entre las 00:00 y las 06:00 en el huso horario especificado
    -  Semanalmente: se ejecuta cada semana, el domingo, entre las 00:00 y las 06:00 en el huso horario especificado
    -  Mensualmente: se ejecuta cada mes, el primer domingo del mes, entre las 00:00 y las 06:00 en el huso horario especificado
    
    Ejemplo de estado de rastreo:
    
    ```json
    "crawl_status" : {
    "source_crawl" : {
      "status" : "completed",
      "next_crawl" : "2019-02-10T05:00:00-05:00"
    }
    ```
5.  Pulse **Guardar y sincronizar objetos** para empezar a rastrear el origen de datos. A continuación, se le redirigirá a la pantalla de estado de recopilación que se actualiza a medida que se añaden documentos a la recopilación.

El rastreo sincronizará los datos inicialmente y luego en la frecuencia que ha especificado.
**Nota:** Si modifica cualquier valor en la pantalla **Valores de sincronización** y pulsa **Guardar y sincronizar objetos**, se iniciará un rastreo (o se reiniciará si ya se está ejecutando) en ese momento.

## Utilización de la API
{: #source_api}

Utilice el proceso siguiente para crear una recopilación conectada a un origen de datos utilizando la API.

Si tiene previsto conectarse a un origen de datos local, primero tendrá que instalar IBM Secure Gateway; consulte [Instalación de IBM Secure Gateway para datos locales](/docs/services/discovery?topic=discovery-sources#gateway) para obtener más información. 

En el ejemplo siguiente se utiliza el origen de datos de SharePoint.

1.  Cree credenciales para el origen de datos al que se está conectando utilizando la [API de credenciales de origen ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery#create-credentials){: new_window}. Registre el valor **credential_id** devuelto de las credenciales que acaba de crear.
2.  Cree una nueva configuración utilizando la [API de configuración ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery#add-configuration){: new_window}. Esta configuración debe contener un objeto de **origen** que defina lo que se debe rastrear. El objeto de **origen** debe contener el valor **credential_id** que ha registrado anteriormente.
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
3.  Cree una nueva recopilación utilizando la [API de recopilaciones ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery#create-a-collection){: new_window}. El objeto que define la recopilación debe contener el valor **configuration_id** que ha registrado anteriormente.

El rastreo de origen comienza en cuanto se crea la recopilación y, de nuevo, se inicia en la frecuencia que ha especificado.
**Nota:** Si modifica cualquier valor en el objeto de **origen** de la configuración, se iniciará un nuevo rastreo (o se reiniciará si ya se está ejecutando) en ese momento.

### Especificación de `customer_id`
{: #source_customer_id}

Se puede utilizar un campo `customer_id` en el documento de {{site.data.keyword.discoveryshort}} ingerido para suprimir el contenido en función del valor `customer_id` utilizando el método **user-data** en la API. El valor `customer_id` no se asigna automáticamente a los documentos entrantes de un origen de datos cuando se ingieren. Si la aplicación requiere que se defina un `customer_id`, puede especificar uno (o varios) de los campos de entrada del sistema de origen que debe copiarse y utilizarse como `customer_id`. Para ello, debe modificar la configuración que se está utilizando para conectarse al origen.

1.  Realice una consulta de ejemplo e identifiqué el campo que desea utilizar como `customer_id`.
2.  Modifique la configuración. Deberá añadir la sección **Normalización** para poder crear el campo `customer_id`.
    -  En el conjunto de herramientas, navegue hasta la recopilación y pulse el enlace **editar** en la sección de configuración. A continuación, pulse el separador **Normalización** para añadir una normalización de **copia** para crear el campo `customer_id`. Pulse **Aplicar y guardar**.
    ![Normalización de copia](images/norm_copy.png)
    -  Cuando utilice la API, añada el objeto siguiente a la matriz de **normalizaciones**:
       ```json
    {
         "operation" : "copy",
         "source_field" : "{original_field_name}",
         "destination_field" : "customer_id"
       }
       ```
       {: codeblock}
3.  El siguiente rastreo planificado agregará el campo `customer_id` a todos los documentos. Si desea que un rastreo se inicie inmediatamente, modifique la configuración de origen (**Valores de sincronización** en el conjunto de herramientas).

Consulte [Seguridad de la información](/docs/services/discovery?topic=discovery-information-security#information-security) para obtener más información e información sobre la supresión basada en `customer_id`.

## Instalación de IBM Secure Gateway para datos locales 
{: #gateway}

Para conectarse a un origen de datos local, primero tiene que descargar, instalar y configurar IBM Secure Gateway. Después de haber instalado IBM Secure Gateway para su primer origen de datos local, no necesitará repetir este proceso.

1.  En la página **Gestionar datos** del conjunto de herramientas de {{site.data.keyword.discoveryshort}}, seleccione **Conectar un origen de datos**.
1.  Seleccione el origen de datos en el que desea conectarse. Cuando seleccione un origen de datos las instalaciones, vaya a la sección **Conectar a la red local** y pulse el botón **Crear conexión**.
1.  En la pantalla **Descargar e instalar el cliente de Secure Gateway**, descargue la versión adecuada de IBM Secure Gateway.
1.  Después de haber completado la descarga, pulse el botón **Descargar Secure Gateway y continuar**. Durante la instalación, necesitará el **ID de pasarela** y la **Señal** que se proporcionan en la pantalla cuando se lo solicite el cliente de Secure Gateway. Consulte [Instalación del cliente ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/docs/services/SecureGateway/securegateway_install.html#installing-the-client){: new_window} en la documentación de Secure Gateway para ver las instrucciones de instalación.
1.  En la máquina que ejecuta el cliente de Secure Gateway, abra el panel de control de Secure Gateway en http://localhost:9003.
1.  Pulse **añadir ACL** en el panel de control. Añada el URL de punto final de cada recopilación de SharePoint a la lista **Permitir acceso**. Por ejemplo, nombre de host: `mycompany.sharepoint.com` y el puerto: `80`.
1.  Vuelva al conjunto de herramientas de {{site.data.keyword.discoveryshort}} y pulse **Continuar**. Si la conexión es correcta, verá el mensaje `Conexión satisfactoria`. Si la conexión no se ha realizado correctamente, abra el panel de control de Secure Gateway y verifique que los puntos finales de la lista **Permitir acceso** son correctos.

Una vez que la conexión se realice correctamente, puede empezar a especificar las credenciales para el origen de datos local.

## Conexión de origen de datos y aislamiento de datos
{: #source_isolation}

[La conexión a orígenes de datos externos](/docs/services/discovery?topic=discovery-sources#sources) reduce el aislamiento de datos de la instancia de servicio, ya que los datos en tránsito entre el origen y el servicio no se pueden aislar. El resto del aislamiento (en reposo, administración, consulta) permanece en su totalidad. Toda la comunicación en curso entre los servicios y los orígenes de datos, y dentro de ellos, está cifrada con TLS v1.2. Las claves privadas de los certificados TLS se cifran en reposo con AES-256-GCM, los certificados de servicio caducan cada tres años, y las listas de revocación de certificados se actualizan mensualmente. Todas las credenciales se envían a través de una conexión cifrada con TLS v1.2 y se cifran en reposo con AES-256. Las conexiones con los orígenes de datos utilizan los protocolos seguros admitidos por dichos orígenes de datos.
