---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-18"

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
{: #gs-api}

En esta breve guía de aprendizaje, introduciremos la {{site.data.keyword.discoveryshort}} API y recorreremos el proceso de creación de una recopilación de datos privados en los que buscar.
{: shortdesc}

Si prefiere trabajar en el conjunto de herramientas de {{site.data.keyword.discoveryshort}}, consulte [Iniciación](/docs/services/discovery/getting-started-tool.html).
{: tip}

## Antes de empezar
{: #before-you-begin}

- Cree una instancia del servicio:
    1.  Vaya a la página de [{{site.data.keyword.discoveryshort}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.{DomainName}/catalog/services/discovery){: new_window} en el catálogo de {{site.data.keyword.Bluemix_notm}}.
    1.  Regístrese para obtener una cuenta de {{site.data.keyword.Bluemix_notm}} gratuita o inicie sesión.
    1.  Pulse **Crear**.
- Copie las credenciales para autenticarse en la instancia de servicio:
    1. En el panel de control de [{{site.data.keyword.Bluemix_notm}} ](https://console.{DomainName}/dashboard/apps), pulse la instancia de servicio {{site.data.keyword.discoveryshort}} para ir a la página del panel de control del servicio {{site.data.keyword.discoveryshort}}.
    1.  En la página **Gestionar**, pulse **Mostrar** para visualizar las credenciales.
    1.  Copie los valores `apikey` y `url`.

    En algunas instancias, la autenticación se lleva a cabo proporcionando una autenticación básica. Si visualiza `nombre de usuario` y `contraseña` en las credenciales, utilice estos valores en lugar de `"apikey":"{apikey_value}"` de los ejemplos de esta guía de aprendizaje.
{: tip}

## Paso 1: Crear un entorno
{: #create-an-environment}

En un shell bash o un entorno similar como Cygwin, con la aplicación `curl` instalada, utilice el método `POST /v1/environments` para crear un entorno. Piense en un entorno como el almacén donde se almacenan todas las cajas de documentos.

Esta guía de aprendizaje utiliza la clave API para realizar la autenticación. Para los usos de producción, asegúrese de revisar las [mejores prácticas](/docs/services/watson/apikey-bp.html#api-bp) de la clave API.
{: tip}

1.  Emita el siguiente mandato para crear un entorno denominado `my-first-environment`. Sustituya `{apikey_value}` por la clave API que ha copiado anteriormente:

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    La API devuelve información como el ID de entorno, el estado del entorno y cuánto almacenamiento utiliza su entorno.

1.  Compruebe el estado del entorno periódicamente hasta que vea un estado `active`.
    - Emita una llamada al método `GET /v1/environments/{environment_id}` para recuperar el estado del entorno. Sustituya `{apikey_value}` y `{environment_id}` por su información:

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}?version=2017-11-07"
    ```
    {: pre}

    Para poder crear una recopilación, el estado debe ser `active`.

## Paso 2: Crear una recopilación
{: #create-a-collection}

Ahora que el entorno está listo, puede crear una recopilación. Piense en una recopilación como una caja donde se almacenarán los documentos en su entorno.

1.  En primer lugar necesitará el ID de su configuración predeterminada. Para encontrar el `configuration_id`, utilice el método `GET /v1/environments/{environment_id}/configurations`. Sustituya `{apikey_value}` y `{environment_id}` por su información:

    ```bash
      curl -u "apikey":"{apikey_value}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07
    ```
    {: pre}
1.  Utilice el método `POST /v1/environments/{environment_id}/collections` para crear una recopilación denominada **my-first-collection**. Sustituya `{apikey_value}`, `{environment_id}` y `{configuration_id}` por su información:

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d '{"name": "my-first-collection", "description": "exploring collections", "configuration_id":"{configuration_id}" , "language": "en_us"}' https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07
    ```
    {: pre}

    La API devuelve información como, por ejemplo, su ID de recopilación, el estado de la recopilación y el almacenamiento que su recopilación está utilizando.
1.  Compruebe el estado de la recopilación periódicamente hasta que vea un estado `active`.
    - Emita una llamada al método `GET /v1/environments/{environment_id}/collections/{collection_id}` para recuperar el estado de su recopilación.  De nuevo, sustituya `{apikey_value}`, `{environment_id}` y `{configuration_id}` por su información:

    ```bash
    curl -u "apikey":"{apikey_value}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07
    ```
    {: pre}

## Paso 3: Descargar los documentos de ejemplo
{: #download-sample-documents}

Descargue estos documentos de ejemplo: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo" title="Icono de enlace externo" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo" title="Icono de enlace externo" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo" title="Icono de enlace externo" class="style-scope doc-content"></a> y <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo" title="Icono de enlace externo" class="style-scope doc-content"></a>.

**Nota:** En algunos navegadores, los enlaces anteriores se abrirán en una nueva ventana en lugar de guardarse localmente. Si esto ocurre, seleccione `Guardar como` en el menú `Archivo` de su navegador para guardar una copia del archivo.

## Paso 4: Cargar los documentos
{: #upload-the-documents}

1.  Ahora, añada los documentos de ejemplo a su recopilación. Este ejemplo carga el documento **test doc1.html** en su recopilación. Sustituya `{apikey_value}`, `{environment_id}` y `{configuration_id}` por su información. Modifique la ubicación del documento de ejemplo para que apunte a al lugar donde guardó el archivo `test-doc1.html`.
    - Utilice el método `POST /v1/environments/{environment_id}/collections/{collection_id}/documents`:

        ```bash
        curl -X POST -u "apikey":"{apikey_value}" -F "file=@test-doc1.html" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2017-11-07
        ```
        {: pre}

    Como alternativa, utilice uno de los SDK que se indican en la [Referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}:
    - Java:

      ```java
      Discovery discovery = new Discovery("2017-11-07");
      discovery.setEndPoint("https://gateway.watsonplatform.net/discovery/api/v1");
      IamOptions options = new IamOptions.Builder()
        .apiKey("{apikey_value}")
        .build();
      discovery.setIamCredentials(options);
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
        version='2017-11-07',
        api_key='{apikey_value}'
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
        version_date: '2017-11-07',
        iam_apikey: '{apikey_value}',
      });

      var file = fs.readFileSync('{/path/to/file}');

      discovery.addDocument({ environment_id: '{environment_id}', collection_id: '{collection_id}', file: file },
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

El ejemplo siguiente devuelve todas las entidades denominadas **IBM**. Sustituya `{apikey_value}`, `{environment_id}` y `{configuration_id}` por su información:

```bash
curl -u "apikey":"{apikey_value}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

## Pasos siguientes
{: #next-steps}

Ha consultado satisfactoriamente los documentos en el entorno y la recopilación que ha creado. Ahora puede empezar a personalizar su recopilación añadiendo más documentos y enriquecimientos, y personalizar los valores de conversión.

- Consulte información sobre la API en la [Referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}
- [Configurar](/docs/services/discovery/building.html) su servicio
- Obtenga más información sobre la [autenticación con IAM](/docs/services/watson/getting-started-iam.html)
