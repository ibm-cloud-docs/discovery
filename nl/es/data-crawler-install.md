---

copyright:
  years: 2015, 2018, 2019
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

# Descarga e instalación de Data Crawler
{: #downloading-and-installing-the-data-crawler}

Data Crawler recopila los datos sin procesar que al final se acaban utilizando para generar resultados de búsquedas para el servicio {{site.data.keyword.discoveryshort}}. Cuando el rastreador rastrea repositorios de datos, descarga documentos y metadatos, tomando como punto de partida un URL semilla que especifica el usuario. El rastreador descubre documentos en una jerarquía, o enlazados desde el URL semilla, y coloca en cola dichos documentos para recuperarlos.
{: shortdesc}

Data Crawler solo debe utilizarse para rastrear comparticiones de archivos o bases de datos, en todos los demás casos debe utilizar el conector adecuado de {{site.data.keyword.discoveryshort}}. Consulte [Conexión a orígenes de datos](/docs/services/discovery?topic=discovery-sources#sources) para obtener más información. Ya no se proporciona asistencia para Data Crawler si lo está utilizando con un origen de datos soportado por los conectores de {{site.data.keyword.discoveryshort}}.
{: important}

## Requisitos previos
{: #dc-prerequisites}

-   Java Runtime Environment versión 8 o superior

    La variable de entorno `JAVA_HOME` debe estar correctamente establecida, o no estar establecida con ningún valor, para ejecutar el rastreador.
    {: tip}
-   Red Hat Enterprise Linux 6 o 7, o Ubuntu Linux 15 o 16. Para un rendimiento óptimo, Data Crawler se debería ejecutar en su propia instancia de Linux, independientemente de si corresponde a una máquina virtual, un contenedor o a hardware.

-   Un mínimo de 2 GB en el sistema Linux.

## Descarga e instalación de Data Crawler
{: #dc-download-install}

1.  Abra un navegador e inicie una sesión en su cuenta de [{{site.data.keyword.Bluemix}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/){: new_window}.

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

1.  Estará ahora listo para [configurar Data Crawler para que se conecte a su repositorio](/docs/services/discovery?topic=discovery-configuring-connector-and-seed-options#configuring-connector-and-seed-options).

## Estructura de Data Crawler
{: #dc-structure}

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
{: #dc-limitations}

-   Data Crawler puede colgarse al ejecutar el conector de sistema de archivos con un URL no válido o ausente.
-   Configure el valor de `urls_to_filter` en el archivo `crawler.conf`, de forma que todos los RegEx o URL de lista blanca se incluyan en una única expresión RegEx. Consulte [Configuración de opciones de rastreo](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-crawl-options) para obtener más información.
-   La vía de acceso al archivo de configuración que se pasa con la opción `--config -c` debe ser una vía de acceso calificada. Esto es, debe estar en los formatos relativos `config/crawler.conf` o `./crawler.conf`, o como una vía de acceso absoluta `/path/to/config/crawler.conf`. Únicamente es posible especificar `crawler.conf` si el archivo `orchestration_service.conf` está inline en lugar de ser referenciado con `include` en el archivo `crawler.conf`.
