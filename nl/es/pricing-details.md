---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-17"

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

# Planes de precios de Discovery
{: #discovery-pricing-plans}

El servicio {{site.data.keyword.discoveryfull}} ofrece tres planes, **Lite**, **Avanzado** y **Premium**, que proporcionan distintos niveles de recursos y prestaciones para adaptarse a sus necesidades.
{: shortdesc}

Los **casos de uso de datos privados** tienen las características, límites y precios siguientes:

## Lite
{: #lite}

Tamaño | Límite de almacenamiento de documentos | Número de documentos\* | Precio 
------ | ------ | ------ | ------  
N/D | 50 MB | 1.000 al mes | Gratuito 

El plan Lite es un plan de inicio y no se debe utilizar en la producción. Si actualiza a un plan de pago, podrá guardar todos los documentos ingeridos.  Las instancias del plan Lite se suprimen tras 30 días de inactividad. 

Atributos:
- 1 entorno
- Hasta 2 recopilaciones
- Enriquecimientos NLU gratuitos\*\*
- 20 documentos en curso\*\*\*\* 

Opciones adicionales:<br> [Modelos personalizados](/docs/services/discovery/integrate-wks.html#integrating-your-custom-model):<br>
Un modelo de Watson Knowledge Studio incluido. Modelos adicionales: No disponibles<br>[Clasificación de elementos](/docs/services/discovery/element-classification.html)\*\*\*:
500 páginas incluidas al mes. Páginas adicionales: No disponible <br>[Nuevas consultas](/docs/services/discovery/watson-discovery-news.html):
200 nuevas consultas incluidas al mes. Consultas adicionales: No disponible<br>[Expansiones de consulta](/docs/services/discovery/using.html#query-expansion):
500 expansiones de consulta con 1.000 términos totales. Expansiones adicionales: No disponible

Para obtener información sobre la actualización de Lite a Avanzado, consulte [Actualización del servicio](/docs/services/discovery/upgrading.html#service)

## Avanzado
{: #advanced}

Tamaño | Límite de almacenamiento de documentos | Número de documentos\* | Precio 
------ | ------ | ------ | ------ 
Extra pequeño\*\*\*\*\* | 40 GB | Hasta 50.000 documentos al mes | A partir de 500 dólares al mes  
Pequeño | 160 GB | Hasta 1M de documentos al mes | A partir de 1.500 al mes  
Medio pequeño | 320 GB | Hasta 2M de documentos al mes | A partir de 3.000 dólares al mes 
Medio| 640 GB | Hasta 4M de documentos al mes | A partir de 5.000 dólares al mes 
Medio grande | 1,2 TB | Hasta 8M de documentos al mes | A partir de 10.000 dólares al mes 
Grande| 2,4 TB | Hasta 16M de documentos al mes | A partir de 15.000 dólares al mes 
Extra grande| 4 TB | Hasta 32M de documentos al mes | A partir de 20.000 dólares al mes 
Extra extra grande | 5.5 TB | Hasta 64M de documentos al mes | A partir de 35.000 dólares al mes 
Extra extra extra grande | 12 TB | Hasta 100M de documentos al mes | A partir de 45.000 dólares al mes 

El entorno extra pequeño es el tamaño más pequeño disponible y se recomienda solo para desarrollo y realización de pruebas.\*\*\*\*\*

El paso de un nivel de Avanzado a otro no requiere la creación de nuevas instancias. Se necesitarán nuevas instancias si se pasa de un plan Avanzado a uno Premium. Para obtener información sobre la actualización de un nivel de Avanzado a otro, consulte [Paso de un nivel de Avanzado a otro](/docs/services/discovery/upgrading.html#advanced).

\*\*\*\*\*Atributos de los planes extra pequeños: 
- 1 entorno
- Hasta 4 recopilaciones
- Enriquecimientos NLU gratuitos\*\*
- 50 documentos en curso\*\*\*\*

Atributos del resto de planes Avanzados:
- 1 entorno
- Hasta 100 recopilaciones
- Enriquecimientos NLU gratuitos\*\*
- 105 documentos en curso\*\*\*\*

Opciones adicionales:<br> [Modelos personalizados](/docs/services/discovery/integrate-wks.html#integrating-your-custom-model):<br>
Un modelo de Watson Knowledge Studio incluido. Modelos adicionales: 800 dólares cada uno<br>[Clasificación de elementos](/docs/services/discovery/element-classification.html)\*\*\*:
500 páginas incluidas al mes. Páginas adicionales: 0,40 dólares cada una <br>[Nuevas consultas](/docs/services/discovery/watson-discovery-news.html):
200 nuevas consultas incluidas al mes  
10.000 consultas adicionales (al mes): 0,10 dólares por consulta<br>
10.001 - 100.000 consultas adicionales (al mes): 0,05 dólares por consulta<br>
Más de 100.000 consultas (al mes): 0,03 dólares por consulta<br>
[Expansiones de consulta](/docs/services/discovery/using.html#query-expansion):
5.000 expansiones de consulta con 25.000 términos totales

## Premium
   
Los planes Premium ofrecen a los desarrolladores y a las organizaciones una instancia de un solo arrendatario de uno o más servicios Watson, para obtener mejor seguridad y aislamiento. Estos planes ofrecen aislamiento a nivel de cálculo sobre la plataforma compartida existente, así como cifrado de datos de extremo a extremo, tanto en tránsito como en reposo. 

Para obtener más información o comprar un plan Premium, póngase en contacto con [Ventas](https://ibm.biz/contact-wdc-premium). 
<br>
<br> 

**Nota:** La fecha de versión de la API se ha actualizado a `2018-08-01`. Para aprovechar las nuevas opciones de dimensionamiento del nuevo entorno (`LT`, `XS`, `S`, `MS`, `M`, `ML`, `L`, `XL`, `XXL`, `XXXL`), debe utilizar esta fecha de versión al crear entornos con la API. Los tamaños entorno ahora tienen el tipo `string` (anteriormente el tipo era `integer`).

\ * El límite de documentos presupone un tamaño de documento promedio de 100KB en disco. El tamaño del documento se calcula después de que haya pasado el proceso de conversión y enriquecimiento, por lo que puede cambiar de forma significativa respecto a la entrada original. Puede ver el número de documentos almacenados y la cantidad total de almacenamiento utilizado con la API [Entornos](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#environments-api) o [Recopilaciones](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#collections-api) o mediante el conjunto de herramientas. Si tiene documentos con un promedio mayor de 100KB en disco, alcanzará el límite de almacenamiento del plan antes de alcanzar el límite del número máximo de documentos. Si realiza una [segmentación de documentos](https://console.bluemix.net/docs/services/discovery/building.html#doc-segmentation) en los documentos, cada segmento cuenta como un documento aparte.

\*\* Los enriquecimientos de [Natural Language Understanding (NLU)](https://console.bluemix.net/docs/services/discovery/building.html#adding-enrichments) son: Extracción de entidades, Análisis de sentimiento, Clasificación de categorías, Etiquetado de conceptos, Extracción de palabras clave, Extracción de relaciones, Análisis de emociones, Clasificación de elementos, Extracción de roles semánticos.  Solo se enriquecen los primeros 50.000 caracteres de cada documento. 

\*\*\* La Clasificación de elementos es un enriquecimiento que analiza documentos normativos para convertir, identificar y clasificar elementos de importancia. Utiliza Natural Language Processing para extraer los siguientes elementos de documentos PDF: parte (a quién se refiere), naturaleza (tipo de elemento) y categoría (clase específica).

\*\*\*\* Si alcanza el límite en curso, debe reducir la velocidad de la ingestión.  Al utilizar el servicio de Discovery, un documento estará "en curso" mientras se carga, enriquece y procesa antes de añadirse a una colección.

Para obtener información sobre cómo calcular costes, consulte [IBM Cloud Pricing Calculator ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.bluemix.net/pricing/platform/watson){: new_window}.

Para obtener información sobre la seguridad de IBM Cloud, consulte [Seguridad y privacidad en los servicios Cloud![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/software/sla/sladb.nsf/sla/csdsp?OpenDocument){: new_window}.

Para obtener información adicional sobre los precios, consulte el catálogo de [{{site.data.keyword.discoveryshort}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.bluemix.net/catalog/services/discovery){: new_window}.

## Notas para los clientes con planes existentes

- A partir del **1 de agosto de 2018**, la facturación y uso se basarán en este plan de precios.
- El plan Lite se ha reducido de 2.000 documentos/400 consultas de {{site.data.keyword.discoverynewsshort}} al mes a 1.000 documentos/200 consultas de {{site.data.keyword.discoverynewsshort}} al mes.  Si ya ha superado el límite del nuevo plan Lite, no podrá añadir más documentos. Sin embargo, puede seguir utilizándolo o actualizarlo a un plan Avanzado o Premium.
- El plan Estándar se ha retirado y no estará disponible para nuevos usuarios. Si actualmente utiliza un plan Estándar, puede seguir utilizándolo o actualizarlo a un plan Avanzado o Premium.
- Los planes Avanzado y Premium ahora se basan en niveles de documentos, ya no se basan en horas de documento. Su factura mensual no variará en función del número de documentos a menos que intercambie las capas.
- Los clientes de Premium pueden ponerse en contacto con [Ventas](https://ibm.biz/contact-wdc-premium) para obtener detalles sobre los cambios de facturación.	
