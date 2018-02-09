---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-30"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:curl: #curl .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}

# Iniciación a la API

En esta breve guía de aprendizaje, introduciremos la {{site.data.keyword.discoveryshort}} API y recorreremos el proceso de creación de una recopilación de datos privados en los que buscar.
{: shortdesc}

## Antes de empezar
{: #before-you-begin}

- Cree una instancia del servicio:
    - {: download} Si está viendo esto, ha creado la instancia de servicio. Ahora debe obtener las credenciales.
    - Cree un proyecto a partir de un servicio: 
        1.  Vaya a la página [Servicios ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.{DomainName}/developer/watson/services){: new_window} de {{site.data.keyword.watson}} Developer Console. 
        1.  Seleccione {{site.data.keyword.discoveryshort}}, pulse **Añadir servicios** y regístrese con una cuenta gratuita de {{site.data.keyword.Bluemix_notm}} o inicie una sesión. 
        1.  Escriba `discovery-tutorial` como nombre de proyecto y pulse **Crear proyecto**.
- Copie las credenciales para autenticar su instancia de servicio:
    - {: download} Desde el panel de control del servicio (lo que esta viendo):
        1.  Pulse el separador **Credenciales de servicio**.
        1.  Pulse **Ver credenciales** bajo **Acciones**.
        1.  Copie los valores de `username`, `password` y `url`.
        {: download}
    - En el proyecto **discovery-tutorial** en Developer Console, copie los valores de `username`,  `password` y `url` para `"discovery"` desde la sección **Credenciales**. 

<!-- Remove this text after dedicated instances have the Developer Console: begin -->

Si utiliza {{site.data.keyword.Bluemix_dedicated_notm}}, cree su instancia de servicio desde la página de [{{site.data.keyword.discoveryshort}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.{DomainName}/catalog/services/discovery/){: new_window} en el Catálogo. Para obtener más información sobre cómo encontrar sus credenciales de servicio, consulte [Credenciales de servicio para los servicios de Watson ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](/docs/services/watson/getting-started-credentials.html#getting-credentials-manually){: new_window}. 

<!-- Remove this text after dedicated instances have the Developer Console: end -->

## Paso 1: Crear un entorno
{: #create-an-environment}

En un shell bash o un entorno similar a Cygwin, utilice el método `POST /v1/environments` para crear un entorno. Piense en un entorno como el almacén donde se almacenan todas las cajas de documentos. 

1.  Emita el siguiente mandato para crear un entorno denominado `my-first-environment`. Sustituya `{username}` y `{password}` con las credenciales de servicio que copió con anterioridad: 

    ```bash
    curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    La API devuelve información como el ID de entorno, el estado del entorno y cuánto almacenamiento utiliza su entorno.

1.  Compruebe el estado del entorno periódicamente hasta que vea un estado `ready`.
    - Emita una llamada al método `GET /v1/environments/{environment_id}` para recuperar el estado del entorno. Sustituya `{username}`, `{password}` y `{environment_id}` con su información: 

    ```bash
    curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}?version=2017-11-07
    ```
    {: pre}

    El estado debe ser `ready` antes de crear una recopilación. 

## Paso 2: Crear una recopilación
{: #create-a-collection}

Ahora que el entorno está listo, puede crear una recopilación. Piense en una recopilación como una caja donde se almacenarán los documentos en su entorno.

1.  En primer lugar necesitará el ID de su configuración predeterminada. Para encontrar el `configuration_id`, utilice el método `GET /v1/environments/{environment_id}/configurations`. Sustituya `{username}`, `{password}` y `{environment_id}` con su información: 

    ```bash
      curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07
    ```
    {: pre}
1.  Utilice el método `POST /v1/environments/{environment_id}/collections` para crear una recopilación denominada **my-first-collection**. Sustituya `{username}`, `{password}`, `{environment_id}` y `{configuration_id}` con su información: 

    ```bash
    curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{"name": "my-first-collection", "description": "exploring collections", "configuration_id":"{configuration_id}" , "language": "en_us"}' https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07
    ```
    {: pre}

    La API devuelve información como, por ejemplo, su ID de recopilación, el estado de la recopilación y el almacenamiento que su recopilación está utilizando.
1.  Compruebe el estado de la recopilación periódicamente hasta que vea un estado `online`.
    - Emita una llamada al método `GET /v1/environments/{environment_id}/collections/{collection_id}` para recuperar el estado de su recopilación. De nuevo, sustituya `{username}`, `{password}`, `{environment_id}` y `{configuration_id}` con su información: 

    ```bash
    curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07
    ```
    {: pre}

## Paso 3: Descargar los documentos de ejemplo
{: #download-sample-documents}

Descargue estos documentos de ejemplo: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo" title="Icono de enlace externo" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo" title="Icono de enlace externo" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo" title="Icono de enlace externo" class="style-scope doc-content"></a> y <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo" title="Icono de enlace externo" class="style-scope doc-content"></a>.

## Paso 4: Cargar los documentos
{: #upload-the-documents}

1.  Ahora, añada los documentos de ejemplo a su recopilación. Este ejemplo carga el documento **test doc1.html** en su recopilación. Sustituya `{username}`, `{password}`, `{environment_id}` y `{configuration_id}`con su información. Modifique la ubicación del documento de ejemplo para que apunte a al lugar donde guardó el archivo `test-doc1.html`. 
    - Utilice el método `POST /v1/environments/{environment_id}/collections/{collection_id}/documents`: 

        ```bash
        curl -X POST -u "{username}":"{password}" -F "file=@test-doc1.html" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2017-11-07
        ```
        {: pre}

    Como alternativa, utilice uno de los SDK que se indican en la [Referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}:
    - Java:

      ```java
      Discovery discovery = new Discovery("2017-11-07");
      discovery.setEndPoint("https://gateway.watsonplatform.net/discovery/api/v1");
      discovery.setUsernameAndPassword("{username}", "{password}");
      String environmentId = "{environment_id}";
      String collectionId = "{collection_id}";
      String documentJson = "{\"field\":\"value\"}";
      InputStream documentStream = new ByteArrayInputStream(documentJson.getBytes());

      CreateDocumentRequest.Builder builder = new CreateDocumentRequest.Builder(environmentId, collectionId);
      builder.inputStream(documentStream, HttpMediaType.APPLICATION_JSON);
      CreateDocumentResponse createResponse = discovery.createDocument(builder.build()).execute();
      ```
      {: codeblock}

    - Python:

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

      with open((os.path.join(os.getcwd(), '{path_element}', '{filename}' as fileinfo:
        add_doc = discovery.add_document('{environment_id}', '{collection_id}', file_info=fileinfo)
      print(json.dumps(add_doc, indent=2))
      ```
      {: codeblock}

    - Node.js:

      ```javascript
      var DiscoveryV1 = require('watson-developer-cloud/discovery/v1');
      var fs = require('fs');

      var discovery = new DiscoveryV1({
        username: '{username}',
        password: '{password}',
        version_date: '2017-11-07'
      });

      var file = fs.readFileSync('{/path/to/file}');

      discovery.addDocument(('{environment_id}', '{collection_id}', file),
      function(error, data) {
        console.log(JSON.stringify(data, null, 2));
        }
      );
      ```
      {: codeblock}

1.  Repita este proceso para cada uno de los otros 3 archivos de ejemplo. 

## Paso 5: Consultar su recopilación
{: #query-your-collection}

Finalmente, utilice el método `GET /v1/environments/{environment_id}/collections/{collection_id}/query` para realizar búsquedas en la recopilación de documentos. 

El ejemplo siguiente devuelve todas las entidades denominadas **IBM**.  Sustituya `{username}`, `{password}`, `{environment_id}` y `{configuration_id}` con su información: 

```bash
curl -u "{username}":"{password}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}*/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

## Siguientes pasos
{: #next-steps}

Ha consultado satisfactoriamente los documentos en el entorno y la recopilación que ha creado. Ahora puede empezar a personalizar su recopilación añadiendo más documentos y enriquecimientos, y personalizar los valores de conversión. Para obtener más información sobre la API, consulte la [Referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}. 
