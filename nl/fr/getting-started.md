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

# Initiation à l'API
{: #gs-api}

Dans ce bref tutoriel, nous allons vous présenter l'API {{site.data.keyword.discoveryshort}} et vous montrer comment créer une collection de données privées et comment effectuer des recherches dans cette dernière.
{: shortdesc}

Si vous préférez travailler dans les outils {{site.data.keyword.discoveryshort}}, voir [Initiation](/docs/services/discovery/getting-started-tool.html).
{: tip}

## Avant de commencer
{: #before-you-begin}

- Créez une instance du service :
    1.  Accédez à la page [{{site.data.keyword.discoveryshort}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.{DomainName}/catalog/services/discovery){: new_window} du catalogue {{site.data.keyword.Bluemix_notm}}.
    1.  Inscrivez-vous pour un compte {{site.data.keyword.Bluemix_notm}} gratuite ou connectez-vous.
    1.  Cliquez sur **Create**.
- Copiez les données d'identification afin de vous authentifier auprès de votre instance de service :
    1. Depuis le [tableau de bord {{site.data.keyword.Bluemix_notm}}](https://console.{DomainName}/dashboard/apps), cliquez sur votre instance de service {{site.data.keyword.discoveryshort}} pour accéder à la page de tableau de bord du service {{site.data.keyword.discoveryshort}}. 
    1.  Sur la page **Manage**, cliquez sur **Show** pour afficher vos données d'identification. 
    1.  Copiez les valeurs pour `apikey` et `url`. 

    Dans certaines instances, vous vous authentifiez en fournissant une authentification de base. Si vous voyez `username` et `password` dans les données d'identification, utilisez ces valeurs à la place de `"apikey":"{apikey_value}"` dans les exemples de ce tutoriel.
{: tip}

## Etape 1 : Création d'un environnement
{: #create-an-environment}

Dans un interpréteur de commandes bash ou un environnement équivalent, tel que Cygwin avec l'application `curl`, utilisez la méthode `POST /v1/environments` pour créer un environnement. Considérez votre environnement comme un entrepôt dans lequel vous
stockez toutes vos boîtes de documents.

Ce tutoriel utilise une clé d'interface de programmation (API) pour l'authentification. Pour une utilisation en production, veillez à étudier les [pratiques recommandées](/docs/services/watson/apikey-bp.html#api-bp) en matière de clé d'API.
{: tip}

1.  Exécutez la commande suivante pour créer un environnement nommé `my-first-environment`. Remplacez `{apikey_value}` par la clé d'API copiée précédemment.

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    L'API renvoie des informations, telles que votre ID d'environnement, le
statut de l'environnement et le volume de stockage utilisé par votre environnement.

1.  Vérifiez le statut de l'environnement régulièrement jusqu'à ce que le statut `active` s'affiche.
    - Appelez la méthode `GET /v1/environments/{environment_id}` afin d'extraire le statut de votre environnement. Remplacez `{apikey_value}` et `{environment_id}` par vos informations :

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}?version=2017-11-07"
    ```
    {: pre}

    Vous ne pouvez pas créer de collection tant que le statut n'est pas passé à `active`. 

## Etape 2 : Création d'une collection
{: #create-a-collection}

A présent que l'environnement est prêt, vous pouvez créer une collection. Considérez
une collection comme une boîte dans laquelle vous stockez vos documents dans votre
environnement.

1.  Vous avez besoin en priorité de l'ID de votre configuration par défaut. Pour rechercher votre `configuration_id` par défaut, utilisez la méthode `GET /v1/environments/{environment_id}/configurations`. Remplacez `{apikey_value}` et `{environment_id}` par vos informations :

    ```bash
      curl -u "apikey":"{apikey_value}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07
    ```
    {: pre}
1.  Utilisez la méthode `POST /v1/environments/{environment_id}/collections` pour créer une collection nommée **my-first-collection**. Remplacez `{apikey_value}`, `{environment_id}` et `{configuration_id}` par vos informations :

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d '{"name": "my-first-collection", "description": "exploring collections", "configuration_id":"{configuration_id}" , "language": "en_us"}' https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07
    ```
    {: pre}

    L'API renvoie des informations, telles que votre ID de collection, le statut de la collection et le volume de stockage utilisé par votre collection.
1.  Vérifiez le statut de la collection régulièrement jusqu'à ce que le statut `active` s'affiche.
    - Appelez la méthode `GET /v1/environments/{environment_id}/collections/{collection_id}` afin d'extraire le statut de votre collection.  Une nouvelle fois, remplacez `{apikey_value}`, `{environment_id}` et `{configuration_id}` par vos informations :

    ```bash
    curl -u "apikey":"{apikey_value}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07
    ```
    {: pre}

## Etape 3 : Téléchargement des exemples de document
{: #download-sample-documents}

Téléchargez les exemples de document suivants : <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe" class="style-scope doc-content"></a> et <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe" class="style-scope doc-content"></a>.

**Remarque :** Dans certains navigateurs, les liens précédents s'ouvrent dans une nouvelle fenêtre plutôt que d'être sauvegardés en local. Dans ce cas, sélectionnez `Save As` dans le menu `File` de votre navigateur pour sauvegarder une copie du fichier.

## Etape 4 : Téléchargement des documents
{: #upload-the-documents}

1.  A présent, ajoutez les exemples de document à votre collection. Cet exemple télécharge le document **test-doc1.html** dans votre collection. Remplacez `{apikey_value}`, `{environment_id}` et `{configuration_id}` par vos informations. Modifiez l'emplacement de l'exemple de document afin de pointer vers l'endroit où vous avez sauvegardé le fichier `test-doc1.html`.
    - Utilisez la méthode `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` :

        ```bash
        curl -X POST -u "apikey":"{apikey_value}" -F "file=@test-doc1.html" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2017-11-07
        ```
        {: pre}

    Vous pouvez aussi utiliser l'un des SDK répertoriés dans le document [API Reference ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window} :
    - Java :

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

    - Python :

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

    - Node.js :

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

1.  Répétez cette procédure pour chacun des 3 autres exemples de fichier.

## Etape 5 : Lancement d'une requête sur votre collection
{: #query-your-collection}

Finalement, utilisez la méthode `GET
/v1/environments/{environment_id}/collections/{collection_id}/query` pour lancer une recherche dans votre collection de documents.

L'exemple ci-après renvoie toutes les entités nommées **IBM**. Remplacez `{apikey_value}`, `{environment_id}` et `{configuration_id}` par vos informations :

```bash
curl -u "apikey":"{apikey_value}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

## Etapes suivantes
{: #next-steps}

Vous avez lancé des requêtes sur des documents dans l'environnement et la collection que vous avez créés. A présent, vous pouvez commencer à personnaliser votre collection en ajoutant d'autres documents et enrichissements et en personnalisant les paramètres de conversion.

- Lisez les informations sur l'API dans [API reference ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}
- [Configurez](/docs/services/discovery/building.html) votre service.
- En savoir plus sur l'[authentification avec IAM](/docs/services/watson/getting-started-iam.html)
