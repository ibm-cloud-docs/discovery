---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-18"

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

# Rastreo de su repositorio de datos
{: #crawling-your-data-repository}

Después de haber configurado correctamente las opciones del rastreador, podrá ejecutar un rastreo en el repositorio de datos.
{: shortdesc}

Nunca ejecute el rastreador como `root`, a menos que necesite acceso a los archivos que solo `root` puede leer.
{: tip}

Ejecute el siguiente mandato: `crawler`

El rastreador le presentará la documentación que explica lo que se debe hacer. Puede ejecutar un rastreo de prueba, o ejecutar un rastreo, además de establecer otras opciones de rastreo.

## Ejecución de un rastreo de prueba

Ejecute el siguiente mandato: `crawler testit`

Este mandato ejecuta un rastreo de prueba, que sólo rastrea el URL de semilla y muestra los URL que se colocan en cola. Si el URL de semilla da lugar a contenido indexable (por ejemplo, es un documento), entonces dicho contenido se envía al adaptador de salida, y el contenido se imprime en la pantalla. Si la recuperación del URL de semilla coloca en cola varios URL, dichos URL se mostrarán y no se enviará ningún contenido al adaptador de salida. De forma predeterminada, se muestran cinco URL en cola.

También se puede especificar un archivo de configuración personalizado como una opción para el mandato de rastreo, por ejemplo: `crawler testit --config [config/myconfigfile.conf]`

La vía de acceso al archivo de configuración que se pasa con la opción `--config` debe ser una vía de acceso calificada. Esto es, debe estar en un formato relativo como, por ejemplo, `config/myconfigfile.conf` o `./myconfigfile.conf`, o en una vía de acceso absoluta como `/path/to/config/myconfigfile.conf`.

Además, se puede establecer el límite para el número de URL en cola que se visualizan como una opción para el mandato testit, por ejemplo: `crawler testit --limit [number] `

## Ejecución de un rastreo

Ejecute el siguiente mandato: `crawler crawl`

Este mandato ejecuta un rastreo con el archivo de configuración predeterminado (`crawler.conf`).

También se puede especificar un archivo de configuración personalizado como una opción para el mandato de rastreo, por ejemplo: `crawler crawl --config [config/myconfigfile.conf]`

La vía de acceso al archivo de configuración que se pasa con la opción `--config` debe ser una vía de acceso calificada. Esto es, debe estar en un formato relativo como, por ejemplo, `config/myconfigfile.conf` o `./myconfigfile.conf`, o en una vía de acceso absoluta como `/path/to/config/myconfigfile.conf`.

## Reinicio de un rastreo

Ejecute el siguiente mandato: `crawler restart`

Este mandato ejecuta un reinicio de rastreo iniciando un nuevo rastreo con el archivo de configuración predeterminado (`crawler.conf`).

También se puede especificar un archivo de configuración personalizado como una opción para el mandato de reinicio, por ejemplo: `crawler restart --config [config/myconfigfile.conf]`

La vía de acceso al archivo de configuración que se pasa con la opción `--config` debe ser una vía de acceso calificada. Esto es, debe estar en un formato relativo como, por ejemplo, `config/myconfigfile.conf` o `./myconfigfile.conf`, o en una vía de acceso absoluta como `/path/to/config/myconfigfile.conf`.

## Reanudación de un rastreo

Ejecute el siguiente mandato: `crawler resume`

Este mandato reanuda un rastreo a partir del lugar en donde se detuvo con el archivo de configuración predeterminado (`crawler.conf`).

También se puede especificar un archivo de configuración personalizado como una opción para el mandato de reanudación, por ejemplo: `crawler resume --config [config/myconfigfile.conf]`

La vía de acceso al archivo de configuración que se pasa con la opción `--config` debe ser una vía de acceso calificada. Esto es, debe estar en un formato relativo como, por ejemplo, `config/myconfigfile.conf` o `./myconfigfile.conf`, o en una vía de acceso absoluta como `/path/to/config/myconfigfile.conf`.

## Renovación de un rastreo

Ejecute el siguiente mandato: `crawler refresh`

Este mandato renueva un rastreo anterior con el archivo de configuración predeterminado (`crawler.conf`).

También se puede especificar un archivo de configuración personalizado como una opción para el mandato de renovación, por ejemplo: `crawler refresh --config [config/myconfigfile.conf]`

La vía de acceso al archivo de configuración que se pasa con la opción `--config` debe ser una vía de acceso calificada. Esto es, debe estar en un formato relativo como, por ejemplo, `config/myconfigfile.conf` o `./myconfigfile.conf`, o en una vía de acceso absoluta como `/path/to/config/myconfigfile.conf`.
