---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-09"

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

# Planes de precio de Discovery

El servicio {{site.data.keyword.discoveryfull}} ofrece tres planes que proporcionan diferentes niveles de recursos y funcionalidades para adaptarse a sus necesidades.
{: shortdesc}

Los **casos de uso de datos privados** tienen los siguientes límites y precios: 

| Lite                     |  Standard         | Advanced          | Premium          |
|--------------------------|-------------------|-------------------|-------------------|
| Hasta 2.000 documentos simultáneos por mes\*   |Hasta 100.000 documentos simultáneos por mes\*   <br/> 10$ por 1.000 documentos simultáneos por mes (0,0139$ USD/1000Doc/Hr)\*\*\*<br/> 2.000 documentos por mes gratuitamente\*\*\*\*  | **Entorno reservado**</br>Precio base 1.000$/mes<br/> Hasta 1.000.000 de documentos por mes\*<br/> 5$ por 1.000 documentos simultáneos por mes(0,00694$ USD/1000Doc/Hr)\*\*\*<br/> Incluidos 100.000 documentos por mes\*\*\*\*</br> Para entornos más grandes, póngase en contacto con el departamento de [Ventas ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/marketing/iwm/dre/signup?source=MAIL-watson){: new_window}. | Los **planes Premium** ofrecen a los desarrolladores y a las organizaciones una instancia de un solo arrendatario de uno o más servicios Watson, para obtener mejor seguridad y aislamiento. Estos planes ofrecen aislamiento a nivel de cálculo sobre la plataforma compartida existente, así como cifrado de datos de extremo a extremo, tanto en tránsito como en reposo. Para obtener más información, o para comprar un plan Premium, póngase en contacto con el departamento de [Ventas ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://ibm.biz/contact-wdc-premium){: new_window} |
| 200MB\*\*                  |10GB\*\*  | 80GB\*\* |-|
| Hasta 2 recopilaciones |Hasta 4 recopilaciones | Hasta 100 recopilaciones |-|
| Hasta 1 modelo personalizado de {{site.data.keyword.knowledgestudiofull}} |Hasta 1 modelo personalizado de {{site.data.keyword.knowledgestudioshort}} | Número ilimitado de modelos personalizados de {{site.data.keyword.knowledgestudioshort}} <br/>Incluido 1 modelo personalizado de {{site.data.keyword.knowledgestudioshort}} <br/>800$ adicionales por modelo de {{site.data.keyword.knowledgestudioshort}} por mes |-|

**Nota:** En todos los planes, las primeras 1.000 consultas de {{site.data.keyword.discoverynewsshort}} por mes son gratuitas. Las consultas de {{site.data.keyword.discoverynewsshort}} tienen un coste de 0.10$ por consultas después de las primeras 1.000 consultas. 

**Nota:** Los servicios del plan Lite se suprimen después de 30 días de inactividad. En los planes Lite se asigna un entorno gratuito por organización. 

 \* El límite de documento presupone un tamaño de documento promedio de 100KB en disco. Este es el tamaño de un documento en una recopilación después de que haya pasado el proceso de conversión y enriquecimiento, de forma que el tamaño puede cambiar de forma significativa respecto a la entrada original. Puede ver el número de documentos almacenados y la cantidad total de almacenamiento utilizado con la API `environments` o `collections` o mediante el conjunto de herramientas. 

 \*\* Si tiene documentos con un promedio mayor de 100KB en disco, alcanzará el límite de almacenamiento del plan antes de alcanzar el límite del número máximo de documentos. 

 \*\*\* El precio se basa en el número de horas en el que se almacena un lote de 1.000 documentos en el servicio (al que se hace referencia como Mil documentos-hora (Thousand Document-Hour o 1000Doc/Hour)). Para los cálculos de los precios, este es el número que se debería especificar (`número de documentos * número de horas que estos documentos se almacenan en un mes / 1000`). 

 \*\*\*\* Las cantidades gratuitas se basan en el equivalente de documentos almacenados durante un mes. Por ejemplo, en el plan Standard, la cantidad gratuita equivale a 2.000 documentos * 720 horas / 1000 documentos = 1440 Mil documentos-Horas. 

**Ejemplo:** Un usuario en el plan Standard almacena 4.000 documentos durante todo el mes. El coste será el siguiente: 

- `4000 documentos * 720 horas (en un mes) / 1000 = 2.880` Mil documentos-horas consumidos

- `2.880 - 1.440 (horas documento gratuitas) = 1.440` Mil documentos-horas facturables. 

- `1.440 * 0,0139$` (precio por Mil documentos-hora) = `20,00$` por el mes

**Nota:** Al calcular la cantidad facturada cada hora, el número total de documentos almacenados se redondea al millar más cercano en el cálculo. Por ejemplo, si tiene 4.678 documentos almacenados durante 1 hora, serían redondeados a 5.000 y darían lugar a 5 Mil documentos-horas a facturar para la cuenta. 

**Nota:** No hay cargo alguno por los enriquecimientos. 

Para obtener información sobre la seguridad de {{site.data.keyword.Bluemix_notm}}, consulte [ Descripción del servicio {{site.data.keyword.Bluemix_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=IBM+Bluemix+Service+Description){: new_window}.

## Conversión de los planes de precios anteriores

Los clientes que suscribieron un plan anterior al **1 de agosto de 2017** fueron migrados a uno de los nuevos planes.  

- Los clientes con el plan anterior de 30 días gratuitos de prueba se migraron al plan **Lite**.
  Como resultado de esta transición, los usuarios existentes pueden haber alcanzado o superado el límite del plan con relación a los documentos _(2000)_, almacenamiento _(200Mb)_ o número de recopilaciones _(2)_. Si ha excedido el límite del plan **Lite**, no podrá añadir contenido adicional en el servicio, aún así, podrá seguir realizando consultas a las recopilaciones. Puede ver el estado actual de todos estos límites mediante el conjunto de herramientas de {{site.data.keyword.discoveryshort}} o la API. Para poder reanudar la adición de contenido a la instancia de {{site.data.keyword.discoveryshort}}, debe decidir entre: 
  - eliminar recopilaciones y/o documentos de forma que no se superen los límites del plan **Lite**. Los documentos se pueden suprimir de forma individual a través de la API con el método [delete-doc ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-doc){: new_window} o se pueden suprimir recopilaciones completas con el conjunto de herramientas o la API con el método [delete-collection ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-collection){: new_window}. 
  - actualice su plan a un nivel que satisfaga sus necesidades de almacenamiento. 
- Los clientes con entornos de tamaño **`1`** **`2`** o **`3`** se han migrado de forma automática al plan **Advanced**. Si ha sido ubicado en el nivel Advanced y tiene menos de 100.000 documentos y 4 recopilaciones, puede pasar al nivel Standard para reducir los costes. Para ello necesita crear una nueva instancia de Discovery en el plan Standard y volver a ingerir los datos en la nueva instancia. La ingestión se puede realizar a través del conjunto de herramientas, las API o Data Crawler.

Consulte [Catálogo de {{site.data.keyword.discoveryshort}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window} para obtener información adicional sobre los precios. 
