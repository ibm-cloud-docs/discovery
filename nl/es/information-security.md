---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-26"

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

# Seguridad de la información
{: #information-security}

IBM está comprometido con ofrecer a nuestros clientes y partners soluciones innovadoras de privacidad, seguridad y control de los datos.
{: shortdesc}

**Aviso:**
Los clientes son responsables de garantizar su propio cumplimiento con diversas leyes y reglamentos, incluido el Reglamento General de Protección de Datos de la Unión Europea. Los clientes son los únicos responsables de obtener asesoramiento legal competente referente a la identificación y la interpretación de cualquier ley relevante que pudiera afectar a su negocio, así como cualquier medida que debieran tomar para cumplir con dichas leyes y normativas.

Los productos, los servicios y otras prestaciones descritas en este documento no son adecuados para todas las situaciones de los clientes y su disponibilidad puede estar restringida. IBM no proporciona recomendaciones legales, contables o de auditoría ni garantiza que sus servicios o productos garantizarán que los clientes cumplan ninguna legislación o normativa.

Si tiene que solicitar soporte de GDPR para los recursos de {{site.data.keyword.cloud}} {{site.data.keyword.watson}} que se crean

-   En la Unión Europea (UE), consulte [Solicitud de soporte para recursos de IBM Cloud Watson creados en la Unión Europea ](/docs/services/watson/getting-started-gdpr-sar.html#request-EU).
-   Fuera de la Unión Europea, consulte [Solicitud de soporte para recursos fuera de la Unión Europea](/docs/services/watson/getting-started-gdpr-sar.html#request-non-EU).

## Reglamento General de Protección de Datos de la Unión Europea (GDPR)
{: #gdpr}

IBM se ha comprometido a proporcionar a nuestros clientes y socios soluciones innovadoras de privacidad, seguridad y gobierno de datos para ayudarles a cumplir con el GDPR.

Obtenga más información sobre la implantación del GDPR en IBM y las prestaciones y las ofertas de GDPR para ayudarle a cumplirlo [aquí ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/gdpr){: new_window}.

## Cómo etiquetar y suprimir datos en {{site.data.keyword.discoveryshort}}
{: #gdpr-discovery}

El servicio {{site.data.keyword.discoveryshort}} incluye una API para etiquetar datos por llamada.

Con esta API puede:

- Etiquetar datos con un ID de cliente.
- Suprimir todos los datos de un ID de cliente determinado, incluidos los avisos relacionados.

Los datos se etiquetan añadiendo el `customer_id` de su elección (consulte las restricciones en [Cómo etiquetar datos](/docs/services/discovery/information-security.html#labeling)) en la cabecera opcional de `X-Watson-Metadata`. {{site.data.keyword.discoveryshort}} podrá suprimirlo mediante el `customer_id`.

En una llamada REST, es posible enviar una cabecera opcional `X-Watson-Metadata` con los pares `field=value` separados por punto y coma, en los que actualmente solo se conserva el `customer_id`. Al agregar el `customer_id` en la cabecera `X-Watson-Metadata`, la solicitud indicará que contiene datos que pertenecen al `customer_id`.

Los `customer_id` son exclusivos en una sola instancia de servicio de {{site.data.keyword.discoveryshort}}. No son exclusivos por entorno o recopilación. No deben incluir datos personales.

**Nota:** Las características experimentales y beta no están pensadas para su uso en un entorno de producción y, por lo tanto, no se garantiza que funcionen como se espera al etiquetar y suprimir datos. Las características experimentales y beta no deben utilizarse al implementar una solución que requiera el etiquetado y supresión de datos.

## Métodos que ofrecen soporte al etiquetado de datos
{: #pi_methods}

La siguiente información almacenada puede suprimirse utilizando el `customer_id` si el `customer_id` se especificó al añadir la información utilizando el método asociado:

- consultas (`/v1/environments/{environment_id}/collections/{collection_id}/query`) Solo cuando se utiliza con los parámetros `passages` o `natural_language_query`
- sucesos (`/v1/events`)
- documentos (`/v1/environments/{environment_id}/collections/{collection_id}/documents`)
- avisos (`/v1/environments/{environment_id}/collections/{collection_id}/notices`) Solo se etiquetan los `avisos` de ingestión.
- Entidades de Knowledge Graph (`/v1/environments/{environment_id}/collections/{collection_id}/query_entities`)
- Relaciones de Knowledge Graph (`/v1/environments/{environment_id}/collections/{collection_id}/query_relations`)
- datos de entrenamiento (`/v1/environments/{environment_id}/collections/{collection_id}/training_data`)

La información almacenada siguiente no se etiqueta explícitamente y no se puede suprimir especificando el `customer_id`. En estos campos no se ofrece soporte a los datos personales.

Cualquier campo de serie (incluidos, aunque sin limitarse a los mismos, el `nombre` y la `descripción`) de los siguientes elementos almacenados:
- configuraciones
- recopilaciones
- entornos

## Etiquetado de datos
{: #labeling}

Al ingerir documentos, incluya la cabecera `X-Watson-Metadata` utilizando las operaciones `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` o `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/ID`. El campo `customer_id` se añade al campo `extracted_metadata` de los documentos. La aplicación debería configurarse para proporcionar el `customer_id` en la cabecera `X-Watson-Metadata` al realizar cualquier operación.

De forma opcional, puede incluir el campo `customer_id` con `metadata` en lugar de utilizar la cabecera `X-Watson-Metadata`.

**Nota:** Si los documentos ya se han ingerido, tendrá que volver a ingerirlos para añadir la cabecera `X-Watson-Metadata` y el `customer_id`.

**Nota:** Si especifica un `customer_id` en la parte de varias partes de `metadata` y la cabecera `X-Watson-Metadata` en el mismo documento, se utilizará el `customer_id` de la cabecera `X-Watson-Metadata`.

Restricciones:

- El valor de la cabecera `X-Watson-Metadata` no puede superar los 4 kilobytes de texto.
- La cabecera `X-Watson-Metadata` debe contener una lista separada por punto y coma de los pares `field=value`. Los valores `field` y `value` no pueden contener punto y coma (`;`) o signos de igual (`=`).
- Los `customer_id` son exclusivos en cada instancia de {{site.data.keyword.discoveryshort}}. No son exclusivos por entorno o recopilación.
- Un `customer_id` no puede tener más de 256 caracteres.
- Si un `customer_id` contiene solo espacios en blanco o está completamente vacío, se considerará que no se ha proporcionado ninguno y no se devolverá ningún mensaje de error.

### Cómo etiquetar datos con el conjunto de herramientas de Discovery
{: #labelingtooling}

Los datos se pueden etiquetar con el campo `customer_id` al utilizar el conjunto de herramientas de {{site.data.keyword.discoveryshort}}. Pulse el icono ![Cog](images/icon_settings.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> y escriba el `customer_id` en el campo **Etiqueta de datos de GDPR**. Una vez se haya establecido el campo, todos los datos cargados mediante la sesión del navegador se etiquetarán con el `customer_id` especificado; este campo debe modificarse manualmente si el ID de cliente asociado cambia.

La adición de un `customer_id` con el campo **Etiqueta de datos del GDPR** etiquetará los documentos, avisos, entidades y relaciones de Knowledge Graph y los datos de entrenamiento en el dominio de URL a partir de dicho punto, incluida cada instancia del mismo dominio. Las acciones (incluidas las cargas de documentos) que se han producido en el conjunto de herramientas de {{site.data.keyword.discoveryshort}} antes de añadir el campo **Etiqueta de datos del GDPR** no se etiquetarán.

**Nota:** Si cambia dominios o navegadores, vacía la memoria caché de navegador o inicia una sesión de incógnito después de especificar el `customer_id` utilizando el campo **Etiqueta de datos del GDPR** del conjunto de herramientas de {{site.data.keyword.discoveryshort}}, el `customer_id` no se conservará y los datos no se etiquetarán. Si debe cambiar dominios y navegadores, vuelva a especificar el `customer_id` en el campo **Etiqueta de datos del GDPR**.

### Cómo etiquetar documentos utilizando Data Crawler
{: #labelingdc}

Si los documentos ya se han rastreado con Data Crawler, tendrá que volver a rastrearlos para añadir la cabecera `X-Watson-Metadata` y el `customer_id`.

1. Actualice la configuración del adaptador de salida de Data Crawler de {{site.data.keyword.discoveryshort}} para que incluya el `customer_id`. Consulte [Configuración del adaptador de salida](/docs/services/discovery/data-crawler-discovery.html#output-adapter).
1. Planifique un rastreo. Los documentos se envían a {{site.data.keyword.discoveryshort}} utilizando la cabecera `X-Watson-Metadata` y se etiquetarán con el `customer_id` configurado.

## Supresión de datos etiquetados
{: #deletingdata}

Los datos deben estar etiquetados con un `customer_id` para poder suprimirlos posteriormente.

1. Utilice la operación `DELETE /v1/user_data` y proporcione el `customer_id` de los datos que desea suprimir. `DELETE /v1/user_data` suprime todos los datos asociados a un `customer_id` determinado de la instancia de servicio, como se especifica en [Métodos que admiten el etiquetado de datos](/docs/services/discovery/information-security.html#pi_methods). Consulte también la [Referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html#delete-user-data){: new_window}

Las supresiones se realizan de forma asíncrona. No puede realizar un seguimiento del progreso de las supresiones.

Si se proporciona un `customer_id` no existente, no se realizará ninguna supresión, pero se devolverá la respuesta `200 - OK`.

Los entornos y recopilaciones no se etiquetan con un `customer_id`, aunque se haya incluido una cabecera `X-Watson-Metadata` en la solicitud para crear el entorno o recopilación. Solo se etiquetarán documentos individuales en la recopilación de un entorno. Por lo tanto, cuando se supriman datos, los entornos y recopilaciones individuales no se suprimirán.

No puede suprimir datos etiquetados utilizando el conjunto de herramientas de {{site.data.keyword.discoveryshort}}.
