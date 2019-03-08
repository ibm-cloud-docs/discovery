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

# Descarga e instalación de Data Crawler
{: #downloading-and-installing-the-data-crawler}

Data Crawler recopila los datos sin procesar que al final se acaban utilizando para generar resultados de búsquedas para el servicio {{site.data.keyword.discoveryshort}}. Cuando el rastreador rastrea repositorios de datos, descarga documentos y metadatos, tomando como punto de partida un URL semilla que especifica el usuario. El rastreador descubre documentos en una jerarquía, o enlazados desde el URL semilla, y coloca en cola dichos documentos para recuperarlos.
{: shortdesc}

Puede utilizar la herramienta o la API de {{site.data.keyword.discoveryshort}} para rastrear orígenes de datos de Box, Salesforce y Microsoft SharePoint Online. Consulte [Conexión a orígenes de datos](/docs/services/discovery/connect.html) para obtener más información.
{: tip}

## Requisitos previos

-   Java Runtime Environment versión 8 o superior

    La variable de entorno `JAVA_HOME` debe estar correctamente establecida, o no estar establecida con ningún valor, para ejecutar el rastreador.
    {: tip}
-   Red Hat Enterprise Linux 6 o 7, o Ubuntu Linux 15 o 16. Para un rendimiento óptimo, Data Crawler se debería ejecutar en su propia instancia de Linux, independientemente de si corresponde a una máquina virtual, un contenedor o a hardware.

-   Un mínimo en 2 GB en el sistema Linux.

## Descarga e instalación de Data Crawler

1.  Abra un navegador e inicie una sesión en su cuenta de [{{site.data.keyword.Bluemix}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net){: new_window}.

1.  Desde el panel de control de {{site.data.keyword.Bluemix_notm}}, seleccione el servicio {{site.data.keyword.discoveryshort}} creado con anterioridad.

1.  En la sección **Automatizar la carga del contenido en el servicio Discovery**, pulse el enlace adecuado para descargar Data Crawler para Linux en los formatos DEB, RPM y ZIP.

1.  Verifique que está ejecutando Java Runtime Environment versión 8 o superior. Ejecute el mandato `java -version` y busque **1.8**. Si está ejecutando una versión anterior a la **1.8**, necesitará actualizar Java instalando Java Developer Kit (JDK) 8 desde su sistema de gestión de paquetes, desde el sitio web de [IBM JDK ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/developerworks/java/jdk/){: new_window} o desde [java.com ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.java.com){: new_window}.

    La variable de entorno `JAVA_HOME` debe estar correctamente establecida, o no estar establecida con ningún valor, para ejecutar el rastreador.
    {: tip}

1.  Como administrador, utilice los mandatos adecuados para instalar el archivo de archivado que ha descargado:

    -   En sistemas como Red Hat y CentOS que utilizan paquetes rpm, utilice un mandato como el siguiente:
`rpm -i /full/path/to/rpm/package/rpm-file-name`
    -   En sistemas como Ubuntu y Debian que utilizan paquetes deb, utilice un mandato como el siguiente:
`dpkg -i /full/path/to/deb/package/deb-file-name`
    -   Los scripts del rastreador se instalan en `{installation_directory}/bin`; por ejemplo, `/opt/ibm/crawler/bin`. Asegúrese de que `{installation_directory}/bin` se encuentra en su variable de entorno `PATH` para que los mandatos del rastreador funcionen correctamente.

    Los scripts del rastreador también se instalan en `/usr/local/bin`. Pueden también añadir esta vía a la variable de entorno `PATH`.
    {: tip}
1.  Cree su directorio de trabajo copiando el contenido del directorio `{installation_directory}/share/examples/config` a un directorio de trabajo en su sistema, por ejemplo, `/home/config`.

    **Aviso:** No modifique directamente los archivos de ejemplo de configuración. Cópielos y luego edítelos. Si edita los archivos de ejemplo en la ubicación original, su configuración podría ser sobrescrita al actualizar Data Crawler, o ser eliminados al desinstalarlo.

    **Nota:** Las referencias en el resto de esta guía a archivos en el directorio `config`, como por ejemplo `config/crawler.conf`, hacen referencia a dicho archivo en su directorio de trabajo y NO al directorio de `{installation_directory}/share/examples/config` instalado.

1.  Estará ahora listo para [configurar Data Crawler para que se conecte a su repositorio](/docs/services/discovery/data-crawler-seeds.html).

## Estructura de Data Crawler

Data Crawler añade las siguientes carpetas en su sistema:

-   `doc` - Contiene archivos con información de licencias y copyright.
-   `bin` - Archivos de script para ejecutar el rastreador.
-   `connectorFramework` - Los archivos en este directorio son los que le permiten interactuar con los datos internos en la empresa o con los datos externos en la web o en un entorno de nube.
-   `lib` - Archivos de biblioteca utilizados por el rastreador.
-   `share`
    -   `doc` - Archivos de documentación en formato HTML y MD (Markdown).
    -   `examples/config` - Archivos que permiten indicar al rastreador los datos que debe rastrear, a dónde enviar la recopilación de los datos rastreados una vez se haya completado el rastreo así como otras opciones de gestión del rastreo.
    -   `man` - Documentación del rastreador con la página manual en el producto.

## Limitaciones conocidas en este release

-   Data Crawler puede colgarse al ejecutar el conector de sistema de archivos con un URL no válido o ausente.
-   Configure el valor de `urls_to_filter` en el archivo `crawler.conf`, de forma que todos los RegEx o URL de lista blanca se incluyan en una única expresión RegEx. Consulte [Configuración de opciones de rastreo](/docs/services/discovery/data-crawler-discovery.html#configuring-crawl-options) para obtener más información.
-   La vía de acceso al archivo de configuración que se pasa con la opción `--config -c` debe ser una vía de acceso calificada. Esto es, debe estar en los formatos relativos `config/crawler.conf` o `./crawler.conf`, o como una vía de acceso absoluta `/path/to/config/crawler.conf`. Únicamente es posible especificar `crawler.conf` si el archivo `orchestration_service.conf` está inline en lugar de ser referenciado con `include` en el archivo `crawler.conf`.
