---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-08"

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

# Migración desde AlchemyData News

El **31 de julio de 2017** se introdujo la nueva versión de {{site.data.keyword.discoverynewsfull}}. Consulte [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html) para una descripción de esta recopilación. 

AlchemyData News ha sido retirado con una fecha de eliminación del servicio del **7 de marzo de 2018**

## Comparación de servicios
{: shortdesc}

Se destacan las siguientes diferencias al pasar de AlchemyData News a {{site.data.keyword.discoverynewsshort}} en el servicio {{site.data.keyword.discoveryshort}}.  

- Los cargos de {{site.data.keyword.discoveryshort}} para las consultas sobre las noticias son únicamente por consulta. Todos los campos están disponibles en cualquier resultado sin coste adicional. 
- Cada consulta de {{site.data.keyword.discoveryshort}} puede devolver hasta un máximo de 50 resultados. El parámetro `offset` está disponible de forma que pueda paginar consultas hasta el número de noticias que necesite. 
- Además {{site.data.keyword.discoveryshort}} da soporte a las agregaciones. Consulte la sección [agregaciones](/docs/services/discovery/query-reference.html#aggregations) de la documentación de {{site.data.keyword.discoveryshort}} para obtener más información. 
- {{site.data.keyword.discoverynewsfull}} no clasifica de la misma manera que lo hace AlchemyData News. Actualmente no hay un campo para la clasificación. 
- La estructura de la consulta y la estructura de los datos devueltos es distinta para {{site.data.keyword.discoverynewsshort}} y para AlchemyData News. Una buena manera de entender la estructura JSON es realizar una consulta para un resultado individual en {{site.data.keyword.discoverynewsshort}} e inspeccionar el resultado. 
- {{site.data.keyword.discoverynewsshort}} no da soporte a la salida XML. 
- La desduplicación es una característica beta en {{site.data.keyword.discoverynewsshort}}.

## Diferencias de autenticación

El servicio {{site.data.keyword.discoveryshort}} utiliza las credenciales {{site.data.keyword.Bluemix_notm}} `username` y `password` estándar para acceder a las consultas. Esto sustituye el método de clave de API existente que se utilizaba con AlchemyData News. Todas las consultas de {{site.data.keyword.discoveryshort}} deben realizarse con la combinación de nombre de usuario y contraseña que crea la instancia de servicio de {{site.data.keyword.discoveryshort}}. 

Es posible gestionar las credenciales de servicio visualizando el separador **Credenciales de servicio** en {{site.data.keyword.Bluemix_notm}}. 

## Configuración de una instancia de Discovery

Una instancia de servicio de {{site.data.keyword.discoveryshort}} se crea del mismo modo que el que se utilizaba para crear la instancia AlchemyData. 

1. Vaya a [{{site.data.keyword.Bluemix_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window}, inicie una sesión, seleccione {{site.data.keyword.discoveryshort}} del catálogo de servicios. 
1. Seleccione el plan adecuado para sus necesidades y pulse **Crear**. 

  El servicio {{site.data.keyword.discoveryshort}} ofrece un plan Lite ofreciendo 1000 consultas de noticias por mes. Puede utilizar una instancia de este plan para identificar consultas equivalente sin tener que pagar por ellas.
  {: tip}

1. Pulse en el separador **Credenciales de servicio** y seleccione **Ver credenciales** para identificar los valores de `url`, `username` y `password` para esta instancia. 

## Consultas para Watson Discovery News

Puede consultar {{site.data.keyword.discoverynewsfull}} mediante la API o uno de los {{site.data.keyword.watson}} SDK. Además, puede utilizar la herramienta de creación de consultas para crear consultas de forma interactiva. 

Para iniciar el conjunto de herramientas de {{site.data.keyword.discoveryshort}} y consultar {{site.data.keyword.discoverynewsshort}}:

1. Pulse **Iniciar herramienta** para {{site.data.keyword.discoveryshort}} bajo **Servicios**.
1. Pulse el mosaico {{site.data.keyword.discoverynewsshort}} para abrir la pantalla **Gestionar datos**. 
1. Pulse **Ver esquema de datos** y, a continuación, **Crear consultas** para abrir el creador de consultas. 

  Las consultas en {{site.data.keyword.discoverynewsfull}} se estructuran de la misma manera que las consultas escritas para recopilaciones de datos privadas. Consulte [Conceptos de consultas](/docs/services/discovery/using.html) y [Referencia de consultas](/docs/services/discovery/query-reference.html).
  {: tip}

**Nota**: No espere que se devuelvan resultados idénticos para consultas similares en AlchemyData y {{site.data.keyword.discoverynewsfull}}. Las diferencias en el tiempo de rastreo, las fuentes y los enriquecimientos dan lugar a resultados diferentes. 

## Adición de consultas de Watson Discovery News a su aplicación

Utilice uno de los métodos siguientes para añadir consultas a su aplicación. Todos estos ejemplos consultas `enriched_text.entities` con un valor de `text` de `IBM` (`enriched_text.entities.text:IBM`). 

En todos los siguientes ejemplos, sustituya `{username}` y `{password}` con el nombre de usuario y la contraseña que aparecen listadas en la página **Credenciales de servicio** de su instancia de servicio. 

### Utilización de llamadas directas a la API

```bash
curl -u "{username}":"{password}"  'https://gateway.watsonplatform.net/discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

### Utilización del Java SDK

```java
Discovery discovery = new Discovery("2017-11-07");
discovery.setEndPoint("https://gateway.watsonplatform.net/discovery/api/v1");
discovery.setUsernameAndPassword("{username}", "{password}");  
String environmentId = "system";
  String collectionId = "news";

QueryRequest.Builder queryBuilder = new QueryRequest.Builder(environmentId,collectionId);  
queryBuilder.query("enriched_text.entities.text:IBM");  
QueryResponse queryResponse =  
discovery.query(queryBuilder.build()).execute();
```
{: codeblock}

### Utilización de Watson Node.js SDK

```javascript
var watson = require('watson-developer-cloud');

var discovery = new DiscoveryV1({  
  username: '{username}',  
  password: '{password}',  
  version_date: '2017-11-07'  
});  

discovery.query(('system', 'news', 'enriched_text.entities.text:IBM'),  
  function(error, data) {  
  console.log(JSON.stringify(data, null, 2));  
```
{: codeblock}

### Utilización de Watson Python SDK

```python
import sys
import os
import json
from watson_developer_cloud import DiscoveryV1

discovery = DiscoveryV1(
  username="{username}",
  password="{password}",
  version="2017-11-07"
)

qopts = {'query': 'enriched_text.entities.text:IBM'}
my_query = discovery.query('{environment_id}', '{collection_id}', qopts)
print(json.dumps(my_query, indent=2))
```
{: codeblock}
