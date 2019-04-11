---
copyright:
  years: 2015, 2018
lastupdated: "2018-12-19"

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

# Iniciación a la API
{: #gs-api}

En esta breve guía de aprendizaje, introduciremos la {{site.data.keyword.discoveryshort}} API y recorreremos el proceso de creación de una recopilación de datos privados en los que buscar.
{: shortdesc}

Si prefiere trabajar en el conjunto de herramientas de {{site.data.keyword.discoveryshort}}, consulte [Iniciación](/docs/services/discovery?topic=discovery-getting-started#getting-started).
{: tip}

## Antes de empezar
{: #before-you-begin-api}

- Cree una instancia del servicio:
    1.  Vaya a la página [{{site.data.keyword.discoveryshort}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/catalog/services/discovery) en el catálogo de {{site.data.keyword.cloud_notm}}.
        La instancia de servicio se crea en el grupo de recursos **predeterminado** si no elige uno diferente, y *no se puede* cambiar posteriormente. Este grupo es suficiente para probar el servicio.
        Si va a crear una instancia para un uso más potente, obtenga más información sobre los [grupos de recursos ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/docs/resources/bestpractice_rgs.html#bp_resourcegroups){: new_window}.
    1.  Regístrese para obtener una cuenta de {{site.data.keyword.cloud_notm}} gratuita o inicie sesión.
    1.  Pulse **Crear**. Después de crear una instancia del servicio de {{site.data.keyword.discoveryshort}}, aparecerá su lista de servicios.
- Copie las credenciales para autenticarse en la instancia de servicio:
    1.  En la [lista de recursos](https://{DomainName}/dashboard/), pulse la instancia de servicio {{site.data.keyword.discoveryshort}} para ir a la página del panel de control del servicio {{site.data.keyword.discoveryshort}}.
    1.  En la página **Gestionar**, pulse **Mostrar credenciales** para visualizar las credenciales.
    1.  Copie los valores de `Clave de API` y `URL`.

        En algunas instancias, la autenticación se lleva a cabo proporcionando una autenticación básica. Si visualiza `nombre de usuario` y `contraseña` en las credenciales, utilice estos valores en lugar de `"apikey:{apikey}"` de los ejemplos de esta guía de aprendizaje.
        {: tip}

## Paso 1: Crear un entorno
{: #create-an-environment}

En un shell bash o un entorno similar, como Cygwin, con la aplicación `curl` instalada, utilice el método `POST /v1/environments` para crear un entorno. Piense en un entorno como el almacén donde se almacenan todas las cajas de documentos.

Esta guía de aprendizaje utiliza la clave de API para realizar la autenticación. Para los usos de producción, asegúrese de revisar las [mejores prácticas](/docs/services/watson/apikey-bp.html#api-bp) de la clave de API.
{: important}

1.  Emita el siguiente mandato para crear un entorno denominado `my-first-environment`. Sustituya `{apikey}` y `{url}` con la clave de API y el URL que ha copiado anteriormente:

    ```bash
    curl -X POST -u "apikey:{apikey}" -H "Content-Type: application/json" -d "{\"name\":\"my-first-environment\", \"description\":\"exploring environments\"}" "{url}/v1/environments?version=2018-12-03"
    ```
    {: pre}

    La API devuelve información como el ID de entorno, el estado del entorno y cuánto almacenamiento utiliza su entorno.

1.  Compruebe el estado del entorno periódicamente hasta que vea un estado `active`.

    Emita una llamada al método `GET /v1/environments/{environment_id}` para recuperar el estado del entorno. Sustituya `{apikey}`, `{url}` y `{environment_id}` por su información:

    ```bash
    curl -u "apikey:{apikey}" "{url}/v1/environments/{environment_id}?version=2018-12-03"
    ```
    {: pre}

    Para poder crear una recopilación, el estado debe ser `active`.

## Paso 2: Crear una recopilación
{: #create-a-collection-api}

Ahora que el entorno está listo, puede crear una recopilación. Piense en una recopilación como una caja donde se almacenarán los documentos en su entorno.

1.  En primer lugar necesitará el ID de su configuración predeterminada. Para encontrar el `configuration_id`, utilice el método `GET /v1/environments/{environment_id}/configurations`. Sustituya `{apikey}`, `{url}` y `{environment_id}` por su información:
    ```bash
      curl -u "apikey:{apikey}" "{url}/v1/environments/{environment_id}/configurations?version=2018-12-03"
    ```
    {: pre}
1.  Utilice el método `POST /v1/environments/{environment_id}/collections` para crear una recopilación denominada **my-first-collection**. Sustituya `{apikey}`, `{url}`, `{environment_id}` y `{configuration_id}` por su información:
    ```bash
    curl -X POST -u "apikey:{apikey}" -H "Content-Type: application/json" -d "{\"name\": \"my-first-collection\", \"description\": \"exploring collections\", \"configuration_id\":\"{configuration_id}\" , \"language": \"en_us\"}" "{url}/v1/environments/{environment_id}/collections?version=2018-12-03"
    ```
    {: pre}
    La API devuelve información como, por ejemplo, su ID de recopilación, el estado de la recopilación y el almacenamiento que su recopilación está utilizando.
1.  Compruebe el estado de la recopilación periódicamente hasta que vea un estado `active`.

    Emita una llamada al método `GET /v1/environments/{environment_id}/collections/{collection_id}` para recuperar el estado de su recopilación.  De nuevo, sustituya `{apikey}`, `{url}`, `{environment_id}` y `{configuration_id}` por su información:

    ```bash
    curl -u "apikey:{apikey}" "{url}/v1/environments/{environment_id}/collections/{collection_id}?version=2018-12-03"
    ```
    {: pre}

## Paso 3: Descargar los documentos de ejemplo
{: #download-sample-documents}

Descargue estos documentos de ejemplo: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo" title="Icono de enlace externo"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo" title="Icono de enlace externo"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo" title="Icono de enlace externo"></a> y <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo" title="Icono de enlace externo"></a>.

En algunos navegadores, los enlaces anteriores se abrirán en una nueva ventana en lugar de guardarse localmente. Si esto ocurre, seleccione `Guardar como` en el menú `Archivo` de su navegador para guardar una copia del archivo.
{: tip}

## Paso 4: Cargar los documentos
{: #upload-the-documents}

1.  Ahora, añada los documentos de ejemplo a su recopilación. Este ejemplo carga el documento **test doc1.html** en su recopilación. Sustituya `{apikey}`, `{url}`, `{environment_id}` y `{collection_id}` por su información. Modifique la ubicación del documento de ejemplo para que apunte a al lugar donde guardó el archivo `test-doc1.html`.
    - Utilice el método `POST /v1/environments/{environment_id}/collections/{collection_id}/documents`:

        ```bash
        curl -X POST -u "apikey:{apikey}" -F "file=@test-doc1.html" "{url}/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2018-12-03"
        ```
        {: pre}

        Como alternativa, utilice uno de los SDK que se indican en la [Referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery){: new_window}:
    - Java:
      ```java
      Discovery discovery = new Discovery("2018-12-03");
      discovery.setEndPoint("{url}");

      IamOptions options = new IamOptions.Builder()
        .apiKey("{apikey}")
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
          version='2018-12-03',
          iam_apikey='{apikey}',
          url='{url}'
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
        version_date: '2018-12-03',
        iam_apikey: '{apikey}',
        url: '{url}'
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

El ejemplo siguiente devuelve todas las entidades denominadas **IBM**. Sustituya `{apikey}`, `{environment_id}` y `{collection_id}` por su información:

```bash
curl -u "apikey:{apikey}" "{url}/v1/environments/{environment_id}/collections/{collection_id}/query?version=2018-12-03&query=enriched_text.entities.text:IBM"
```
{: pre}

## Pasos siguientes
{: #next-steps-api}

Ha consultado satisfactoriamente los documentos en el entorno y la recopilación que ha creado. Ahora puede empezar a personalizar su recopilación añadiendo más documentos y enriquecimientos, y personalizar los valores de conversión.

- Consulte información sobre la API en la [Referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery){: new_window}
- [Configurar](/docs/services/discovery?topic=discovery-configservice#configservice) su servicio
- Obtenga más información sobre la [autenticación con IAM ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/docs/services/watson/getting-started-iam.html#iam){: new_window}
