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

# Actualización del plan
{: #upgrading-your-plan}

El servicio {{site.data.keyword.discoveryfull}} ofrece tres planes que proporcionan diferentes niveles de recursos y funcionalidades para adaptarse a sus necesidades.
{: shortdesc}

Consulte [Planes de precios de {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans) y el [catálogo de {{site.data.keyword.discoveryshort}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/catalog/services/discovery){: new_window} para obtener detalles.

## Actualización del servicio
{: #service}

Para redimensionar el plan de Lite a Avanzado:

1. Abra el [panel de control de {{site.data.keyword.Bluemix_notm}}](https://{DomainName}/dashboard). 
1. Pulse en la instancia de servicio de {{site.data.keyword.discoveryshort}} para abrir el panel de control del servicio {{site.data.keyword.discoveryshort}}.
1. En la página **Gestionar** del servicio de {{site.data.keyword.discoveryshort}}, pulse **Actualizar** para elegir un plan avanzado. Se abrirá la página **Plan**. Siga los pasos para completar la actualización. 
1. Vuelva a la página **Gestionar** y pulse **Iniciar herramienta** para abrir el conjunto de herramientas de {{site.data.keyword.discoveryshort}}.
   - Si nunca ha creado un entorno para el plan Lite antes de la actualización a Avanzado, pulse el icono ![Cog](images/icon_settings.png) y seleccione **Crear entorno**. Una pantalla mostrará las opciones para el plan Avanzado. Seleccione la que se adapte a sus necesidades.  (`Extra pequeño`, `Pequeño`, `Medio pequeño`, `Medio`, `Medio grande`, `Grande`, `Extra grande`, `Extra extra grande`).
   - Si ha creado un entorno para el plan Lite antes de la actualización a Avanzado, el nuevo entorno del plan Avanzado será `Pequeño` por defecto. 

## Cambiar del nivel Avanzado a otro nivel
{: #switchadvanced} 

Si ya dispone de un plan Avanzado y desea actualizarlo a un plan más grande, puede hacerlo utilizando la [API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery#update-an-environment){: new_window}. 

Para obtener información detallada sobre el precio y los límites de almacenamiento del plan avanzado, consulte [Planes de precios del plan Avanzado](/docs/services/discovery?topic=discovery-discovery-pricing-plans#advanced).

Los tamaños del plan Avanzado disponibles son: 

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
- Si más adelante descubre que necesita un tamaño de plan más pequeño, debe configurar el tamaño del plan adecuado, migrar los datos y, a continuación, cancelar el plan más grande. 

## Actualización a un plan Premium
{: #premium}

Si está interesado en un plan Premium, póngase en contacto con [Ventas](https://ibm.biz/contact-wdc-premium).  
