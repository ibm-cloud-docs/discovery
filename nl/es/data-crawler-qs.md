---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-03"

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

# Iniciación a Data Crawler

Este tema explica cómo utilizar el rastreador de datos para ingerir archivos desde su sistema de archivos local, para utilizar con el servicio {{site.data.keyword.discoveryfull}}.
{: shortdesc}

Antes de intentar esta tarea, cree una instancia del servicio {{site.data.keyword.discoveryshort}} en {{site.data.keyword.Bluemix}}. Para completar esta guía, necesitará utilizar las credenciales que están asociadas con la instancia de servicio que cree.

Puede utilizar la herramienta o la API de {{site.data.keyword.discoveryshort}} para rastrear orígenes de datos de Box, Salesforce y Microsoft SharePoint Online. Consulte [Conexión a orígenes de datos](/docs/services/discovery/connect.html) para obtener más información.
{: tip}

## Crear un entorno

Utilice con bash el método POST /v1/environments para crear un entorno. Piense en un entorno como el almacén donde se almacenan todas las cajas de documentos. En el siguiente ejemplo se crea un entorno denominado `my-first-environment`:

Sustituya `{username}` y `{password}` con sus credenciales de servicio.

```bash
curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
```
{: pre}

La API devuelve una respuesta que incluye información como el ID de entorno, el estado del entorno y cuánto almacenamiento utiliza su entorno. No pase al siguiente paso hasta que el estado del entorno sea `ready`. Cuando se crea el entorno, si el estado es `status:pending`, utilice el método `GET /v1/environments/{environment_id}` para comprobar el estado hasta que sea ready. En este ejemplo, sustituya `{username}` y `{password}` con sus credenciales de servicio, y sustituya `{environment_id}` con el ID de entorno que se devolvió al crear el entorno.

```bash
curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}?version=2017-11-07
```
{: pre}

## Creación de una recopilación

A continuación, utilice el método `POST /v1/environments/{environment_id}/collections` para crear una recopilación. Piense en una recopilación como una caja donde se almacenarán los documentos en su entorno. Este ejemplo crea una recopilación que se denomina `my-first-collection` en el entorno que ha creado en el paso anterior, y utiliza la siguiente configuración predeterminada:

-   Sustituya `{username}` y `{password}` con sus credenciales de servicio.
-   Sustituya `{environment_id}` con el ID de entorno creado en el paso 1.

Antes de crear una recopilación debe obtener el ID de la configuración predeterminada. Para encontrar el `configuration_id` predeterminado, utilice el método `GET /v1/environments/{environment_id}/configurations`:

```bash
curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07
```
{: pre}

Una vez que tenga el ID de configuración predeterminado, utilícelo para la recopilación. Sustituya `{configuration_id}` con el ID de configuración predeterminado de su entorno.

```bash
curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{"name": "my-first-collection", "description": "exploring collections", "configuration_id":"{configuration_id}" , "language": "en_us"}' https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07
```
{: pre}

La API devuelve una respuesta que incluye información como, por ejemplo, el ID de la recopilación, el estado de la recopilación y el almacenamiento que está utilizando la recopilación. No pase al siguiente paso hasta que el estado de la recopilación sea `online`. Cuando crea la recopilación, si el estado devuelve `status:pending`, utilice el método `GET /v1/environments/{environment_id}/collections/{collection_id}` para comprobar el estado hasta que sea ready. En este ejemplo, sustituya `{username}` y `{password}` con sus credenciales de servicio, sustituya `{environment_id}` con su ID de entorno y sustituya `{collection_id}` con el ID de recopilación que se devolvió con anterioridad en este paso.

```bash
curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07
```
{: pre}

## Descarga de los documentos de ejemplo
Descargue estos documentos:

-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo" title="Icono de enlace externo" class="style-scope doc-content"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo" title="Icono de enlace externo" class="style-scope doc-content"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo" title="Icono de enlace externo" class="style-scope doc-content"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo" title="Icono de enlace externo" class="style-scope doc-content"></a>

## Descarga e instalación de Data Crawler

1.  Verifique los requisitos previos del sistema

    -   Java Runtime Environment versión 8 o superior

        **Nota:** La variable de entorno `JAVA_HOME` debe estar correctamente establecida, o no estar establecida con ningún valor, para ejecutar el rastreador.
    -   Red Hat Enterprise Linux 6 o 7, o Ubuntu Linux 15 o 16. Para un rendimiento óptimo, Data Crawler se debería ejecutar en su propia instancia de Linux, independientemente de si corresponde a una máquina virtual, un contenedor o a hardware.
    -   Un mínimo en 2 GB en el sistema Linux.

1.  Abra un navegador e inicie una sesión en su cuenta de [{{site.data.keyword.Bluemix_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net){: new_window}.
1.  Desde el panel de control de {{site.data.keyword.Bluemix_notm}}, seleccione el servicio {{site.data.keyword.discoveryshort}} creado con anterioridad.
1.  En **Automatizar la carga de contenido en el servicio de Discovery**, seleccione el enlace de descarga adecuado para el sistema (DEB, RPM o ZIP) para descargar Data Crawler.
1.  Como administrador, utilice los mandatos adecuados para instalar el archivo de archivado que ha descargado:

    -   En sistemas como Red Hat y CentOS que utilizan paquetes rpm, utilice un mandato como el siguiente:
`rpm -i /full/path/to/rpm/package/rpm-file-name`
    -   En sistemas como Ubuntu y Debian que utilizan paquetes deb, utilice un mandato como el siguiente:
`dpkg -i /full/path/to/deb/package/deb-file-name`
    -   Los scripts del rastreador se instalan en `{installation directory}/bin`; por ejemplo, `/opt/ibm/crawler/bin`. Asegúrese de que `{installation_directory}/bin` se encuentra en su variable de entorno `PATH` para que los mandatos del rastreador funcionen correctamente.

    Los scripts del rastreador también se instalan en `/usr/local/bin`. Pueden también añadir esta vía a la variable de entorno `PATH`.
    {: tip}

## Creación de su directorio de trabajo

Copie el contenido del directorio `{installation_directory}/share/examples/config` a un directorio de trabajo en su sistema, por ejemplo, `/home/config`.

**Aviso:** No modifique directamente los archivos de ejemplo de configuración. Cópielos y luego edítelos. Si edita los archivos de ejemplo en la ubicación original, su configuración podría ser sobrescrita al actualizar Data Crawler, o ser eliminados al desinstalarlo.

**Nota:** Las referencias en esta guía a archivos en el directorio `config`, como por ejemplo `config/crawler.conf`, hacen referencia a dicho archivo en su directorio de trabajo y NO al directorio de `{installation_directory}/share/examples/config` instalado.

## Configuración de las opciones del rastreador

Para configurar Data Crawler para que rastree su repositorio, debe especificar los archivos del sistema local que desea rastrear y el servicio {{site.data.keyword.discoveryshort}} al que enviar la recopilación de archivos rastreados, una vez se el rastreo se haya completado.

1.  **`filesystem-seed.conf`** - Abra el archivo `seeds/filesystem-seed.con` en un editor de texto. Modifique el atributo `value` directamente bajo el atributo `name-"url"` con la vía de acceso de archivos que desea rastrear. Por ejemplo: `value-"sdk-fs:///TMP/MY_TEST_DATA/"`

    **Nota:** Los URL deben empezar por `sdk-fs://`. Por ejemplo, para rastrear `/home/watson/mydocs`, el valor de este URL sería `sdk-fs:///home/watson/mydocs` - la tercera / es necesaria.

    Guarde y cierre el archivo.

1.  **`discovery_service.conf`** - Abra el archivo `discovery/discovery_service.conf` en un editor de texto. Modifique los siguientes valores específicos del servicio {{site.data.keyword.discoveryshort}} que ha creado anteriormente en {{site.data.keyword.Bluemix_notm}}:

    -   `environment_id` - ID de entorno de servicio {{site.data.keyword.discoveryshort}}.
    -   `collection_id` - ID de recopilación de servicio {{site.data.keyword.discoveryshort}}.
    -   `configuration_id` - ID de configuración de servicio {{site.data.keyword.discoveryshort}}.
    -   `configuration` - Ubicación de vía de acceso completa del archivo `discovery_service.conf`, por ejemplo, `/home/config/discovery/discovery_service.conf`.
    -   `username` - Credencial de nombre de usuario para el servicio {{site.data.keyword.discoveryshort}}.
    -   `password` - Credencial de contraseña para el servicio {{site.data.keyword.discoveryshort}}.
1.  **`crawler.conf`** - Abra el archivo `config/crawler.conf` en un editor de texto.

    -   Configure la `class` `output_adapter` y las opciones de `config` para el servicio {{site.data.keyword.discoveryshort}} tal como se indica a continuación:

        ```bash
        class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

        config - "discovery_service"

        discovery_service {
          include "discovery/discovery_service.conf"
        }
        ```
        {: pre}

1.  Después de modificar estos archivos, estará listo para rastrear los datos.

## Rastreo de los datos

Ejecute el siguiente mandato: `crawler crawl --config [config/crawler.conf]`

Con este mandato se ejecuta un rastreo con el archivo de configuración `crawler.conf`.

**Nota:** La vía de acceso al archivo de configuración que se pasa con la opción `-- config` debe ser una vía de acceso calificada. Esto es, puede estar en un formato relativo como `config/crawler.conf` o `./crawler.conf` o en una vía de acceso absoluta como `/path/to/config/crawler.conf`.

## Búsquedas en sus documentos

Finalmente, utilice el método `GET /v1/environments/{environment_id}/collections/{collection_id}/query` para realizar búsquedas en la recopilación de documentos. El ejemplo siguiente devuelve todas las entidades denominadas `IBM`:

-   Sustituya `{username}` y `{password}` con sus credenciales de servicio.
-   Sustituya `{environment_id}` con el ID de entorno creado que ha creado en el paso 1.
-   Sustituya `{collection_id}` con el ID de la recopilación que ha creado en el paso 2.

```bash
curl -u "{username}":"{password}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&query-enriched_text.entities.text:IBM'
```
{: pre}

## Resultados

Ahora ha consultado satisfactoriamente los documentos en un entorno en recopilación que ha creado. Ahora puede empezar la personalización añadiendo más documentos a la recopilación.
