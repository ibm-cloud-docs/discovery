---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-25"

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

# Actualización del plan
{: #upgrading-your-plan}

El servicio {{site.data.keyword.discoveryfull}} ofrece tres planes que proporcionan diferentes niveles de recursos y funcionalidades para adaptarse a sus necesidades.
{: shortdesc}

Consulte [Planes de precios de {{site.data.keyword.discoveryshort}}](/docs/services/discovery/pricing-details.html) y el [catálogo de {{site.data.keyword.discoveryshort}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window} para obtener detalles.

## Actualización del servicio
{: #service} 

Para redimensionar el plan de Lite a Avanzado:

1. Abra el panel de control de [{{site.data.keyword.Bluemix_notm}}](https://console.{DomainName}/dashboard). 
1. Pulse en la instancia de servicio de {{site.data.keyword.discoveryshort}} para abrir el panel de control del servicio {{site.data.keyword.discoveryshort}}.
1. En la página **Gestionar** del servicio de {{site.data.keyword.discoveryshort}}, pulse **Actualizar** para elegir un plan avanzado. Se abrirá la página **Plan**. Siga los pasos para completar la actualización. 
1. Vuelva a la página **Gestionar** y pulse **Iniciar herramienta** para abrir el conjunto de herramientas de {{site.data.keyword.discoveryshort}}.
   - Si nunca ha creado un entorno para el plan Lite antes de la actualización a Avanzado, pulse el icono ![Cog](images/icon_settings.png) y seleccione **Crear entorno**. Una pantalla mostrará las opciones para el plan Avanzado. Seleccione la que se adapte a sus necesidades.  (`Extra pequeño`, `Pequeño`, `Medio pequeño`, `Medio`, `Medio grande`, `Grande`, `Extra grande`, `Extra extra grande`).
   - Si ha creado un entorno para el plan Lite antes de la actualización a Avanzado, el nuevo entorno del plan Avanzado será `Pequeño` por defecto. 

## Cambiar del nivel Avanzado a otro nivel
{: #advanced} 

Si ya dispone de un plan Avanzado y desea actualizarlo a un plan más grande, puede hacerlo utilizando la API [![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#update-environment){: new_window}. 

Para obtener información detallada sobre el precio y los límites de almacenamiento del plan avanzado, consulte [Planes de precios del plan Avanzado](/docs/services/discovery/pricing-details.html#advanced).

Puede actualizar el tamaño del plan Avanzado, pero no puede reducir el tamaño a uno más pequeño. Los tamaños del plan Avanzado disponibles son: 

Tamaño del plan | Etiqueta  
--------- | ------ 
Extra pequeño | XS 
Pequeño | S 
Medio pequeño | MS 
Medio | M 
Medio grande | ML 
Grande | L
Extra grande | XL 
Extra extra grande | XXL 

- La consulta y la indexación pueden continuar durante la actualización. El tiempo necesario para la actualización depende de una serie de factores. Puede sondear el entorno utilizando la API mientras se completa la actualización.
- El paso de un nivel de Avanzado a otro no requiere la creación de nuevas instancias. 
- Una vez se haya completado la actualización, se le facturará a la nueva tarifa del plan.

## Actualización a un plan Premium
{: #premium}

Si está interesado en un plan Premium, póngase en contacto con [Ventas](https://ibm.biz/contact-wdc-premium).  
