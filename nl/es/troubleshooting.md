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

# Resolución de problemas 

Sugerencias para la resolución de problemas al utilizar el servicio {{site.data.keyword.discoveryshort}}. 

Si se le presentan problemas al utilizar el servicio {{site.data.keyword.discoveryshort}}, intente una o varias de las siguientes sugerencias para la resolución de problemas. 

-   Un documento podría no ingerirse debido a una discrepancia entre el tipo de los datos en el documento actual y datos parecidos en un documento ingerido con anterioridad. Por ejemplo, un campo podría definirse como **date** en un documento y como **string** en un documento posterior, impidiendo que éste último se indexase de forma correcta. 

    La operación de vista previa no puede predecir las discrepancias en el tipo porque únicamente verifica un único documento y no conserva un registro de los resultados de la conversión.
-   La indexación rápida o muy grande de documentos a veces puede dar lugar a un reinicio del servicio de búsqueda de fondo. Si esto ocurre, póngase en contacto con el soporte de {{site.data.keyword.IBM}} para obtener ayuda. 
