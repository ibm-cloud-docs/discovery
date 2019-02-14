---

copyright:
  years: 2015, 2018
lastupdated: "2018-01-16"

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

# Migración desde Watson Discovery News Original

El **31 de julio de 2017** se introdujo la nueva versión de {{site.data.keyword.discoverynewsshort}}. La versión original se ha renombrado como {{site.data.keyword.discoverynewsshort}} Original y se retiró del servicio el **15 de enero de 2018**. Si intenta acceder a {{site.data.keyword.discoverynewsshort}} Original, recibirá el mensaje `410 GONE`.
{: shortdesc}

Para migrar desde {{site.data.keyword.discoverynewsshort}} Original a la nueva versión, necesitará hacer varios cambios, entre otros, actualizar las consultas creadas para {{site.data.keyword.discoverynewsshort}} Original.

  **Nota:** {{site.data.keyword.discoverynewsshort}} Original solo está disponible en instancia de {{site.data.keyword.discoveryshort}} creadas antes del **31 de julio de 2017** y se retiró del servicio el **15 de enero de 2018**.

Consulte [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html) para una descripción de esta recopilación.

Para obtener una descripción e información sobre la realización de consultas para {{site.data.keyword.discoverynewsshort}} Original, consulte [Watson Discovery News Original](/docs/services/discovery/discovery-auxiliary.html#watson-discovery-news-original).

## Comparación de servicios

| {{site.data.keyword.discoverynewsshort}} Original         | {{site.data.keyword.discoverynewsshort}}           |
|----------------------------------------|---------------------------------|
| **{{site.data.keyword.discoverynewsshort}} Original** era un conjunto enriquecido de forma previa con los siguientes enriquecimientos de Alchemy Language: Extracción de palabras clave, Extracción de entidades, Etiquetado de conceptos, Extracción de relaciones, Análisis de sentimiento y Clasificación de taxonomías. También se habían añadido los siguientes metadatos adicionales: fecha de rastreo, fecha de publicación, clasificación de URL, clasificación de host y texto de ancla.     | **{{site.data.keyword.discoverynewsshort}}** es un conjunto enriquecido de forma previa con los siguientes enriquecimientos de NLU ({{site.data.keyword.nlushort}}): Extracción de palabras clave, Extracción de entidades, Extracción de roles semánticos, Análisis de sentimiento, Relaciones y Clasificación de categorías. También se añaden los siguientes metadatos adicionales: fecha de rastreo y fecha de publicación. Para conocer más los enriquecimientos de NLU, consulte [Adición de enriquecimientos](/docs/services/discovery/building.html#adding-enrichments).                         |
| **{{site.data.keyword.discoverynewsshort}} Original** era accesible a través de un entorno que era único para su instancia de servicio.                       | Al utilizar **{{site.data.keyword.discoverynewsshort}}**, todos los usuarios consultan a la misma recopilación y el mismo entorno. Esto significa que es necesario cambiar todas las referencias a su entorno y recopilación.      |
| En **{{site.data.keyword.discoverynewsshort}} Original**, recibía información como, por ejemplo, el tamaño de la recopilación, el número de documentos, etc. al recuperar el entorno a través de la API.  | La API de **{{site.data.keyword.discoverynewsshort}}** no devuelve esta información.                          |

Los siguientes nuevos campos están disponibles en **{{site.data.keyword.discoverynewsshort}}**:

`enriched_text.relations.arguments.text`  
`enriched_text.relations.score`  
`enriched_text.relations.sentence`  
`enriched_text.relations.type`  
`enriched_title.relations`  
`enriched_title.relations.arguments`  
`enriched_title.relations.arguments.entities`<br/>
`enriched_title.relations.arguments.entities.text`  
`enriched_title.relations.arguments.entities.type`  
`enriched_title.relations.arguments.text`  
`enriched_title.relations.score`  
`enriched_title.relations.sentence`  
`enriched_title.relations.type`  
`external_links`  
`extracted_metadata`  
`extracted_metadata.file_type`  
`extracted_metadata.filename`  
`extracted_metadata.sha1`  
`forum_title`  
`main_image_url`

También se han eliminado muchos campos, por ejemplo `blekko.hostrank`, `duplicate_url`, `domain`, etc. Consulte <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/News_migration_v_1.01.xlsx" download>AQUÍ <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo" title="Icono de enlace externo" class="style-scope doc-content"></a> para obtener una lista completa.

## Traslado de consultas al nuevo Watson Discovery News

Para trasladar sus consultas desde {{site.data.keyword.discoverynewsshort}} Original al nuevo {{site.data.keyword.discoverynewsshort}}, necesitará modificar todas las consultas existentes de las siguientes maneras:  

- Cambiar el ID de entorno al que la consulta está llamando. El nuevo entorno de noticias se ha estandarizado a través de todas las instancias de servicio de {{site.data.keyword.discoveryshort}} a:

  `system`  

- Cambiar el ID de recopilación al que la consulta está llamando. El nombre de la recopilación de noticias se ha estandarizado a través de todas las instancias de servicio de {{site.data.keyword.discoveryshort}} a:

  `news`

- Modificar la consulta para utilizar la nueva estructura de vías de JSON para el nuevo {{site.data.keyword.discoverynewsshort}}. La mayoría de los campos han cambiado sus vías, se han añadido varios campos y un grupo seleccionado de campos de bajo valor añadido se han eliminado. Consulte <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/News_migration_v_1.01.xlsx" download>AQUÍ <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo" title="Icono de enlace externo" class="style-scope doc-content"></a> la hoja de cálculo de migración de campos para obtener todos los detalles. Por ejemplo, la siguiente consulta:

  `discovery/api/v1/environments/ae5790c2-592f-432a-804a-ee16de7154d7/collections/3edcd8f1-e25a-4f44-a069-58332ad17651/query?version=2017-11-07&query=entities.type:"Company"`

  Se debería cambiar a:

  `discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.type:"Company"`  

## Consultas para Watson Discovery News

Puede consultar {{site.data.keyword.discoverynewsshort}} mediante la API o uno de los {{site.data.keyword.watson}} SDK. Además, puede utilizar la herramienta de creación de consultas para crear consultas de forma interactiva.

**Para iniciar el conjunto de herramientas de {{site.data.keyword.discoveryshort}} y consultar {{site.data.keyword.discoverynewsshort}}:**

1. Pulse **Iniciar herramienta** para {{site.data.keyword.discoveryshort}} bajo **Servicios**.
1. Pulse el mosaico {{site.data.keyword.discoverynewsshort}} para abrir la pantalla **Gestionar datos**.
1. Pulse **Ver esquema de datos** y, a continuación, **Crear consultas** para abrir el creador de consultas.

  Las consultas en {{site.data.keyword.discoverynewsshort}} se estructuran de la misma manera que las consultas escritas para recopilaciones de datos privadas. Consulte [Conceptos de consultas](/docs/services/discovery/using.html) y [Referencia de consultas](/docs/services/discovery/query-reference.html).
  {: tip}

**Nota:** No espere que se devuelvan resultados idénticos para consultas similares en {{site.data.keyword.discoverynewsshort}} Original y {{site.data.keyword.discoverynewsshort}}. Las diferencias en el tiempo de rastreo, las fuentes y los enriquecimientos dan lugar a resultados diferentes.

## Adición de consultas de Watson Discovery News a su aplicación

Utilice uno de los métodos siguientes para añadir consultas a su aplicación. Todos estos ejemplos consultas `enriched_text.entities` con un valor de `text` de `IBM` (`enriched_text.entities.text:IBM`).

En todos los siguientes ejemplos, sustituya `{username}` y `{password}` con el nombre de usuario y la contraseña que aparecen listadas en la página **Credenciales de servicio** de su instancia de servicio.

### Utilización de llamadas directas a la API

```bash
curl -u "{username}":"{password}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

### Utilización de Watson Java SDK

```java
Discovery discovery = new Discovery("2017-11-07");  
discovery.setEndPoint("https://gateway.watsonplatform.net/discovery/api/v1");
discovery.setUsernameAndPassword("{username}", "{password}");  
String environmentId = "system";
String collectionId = "news";

QueryRequest.Builder queryBuilder = new QueryRequest.Builder(environmentId, collectionId);  
queryBuilder.query("enriched_text.entities.text:IBM");  
QueryResponse queryResponse = discovery.query(queryBuilder.build()).execute();
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
  }
);
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
my_query = discovery.query('system', 'news', qopts)  
print(json.dumps(my_query, indent=2))  
```
{: codeblock}
