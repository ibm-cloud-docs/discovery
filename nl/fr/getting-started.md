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

# Initiation à l'API

Dans ce bref tutoriel, nous allons vous présenter l'API {{site.data.keyword.discoveryshort}} et vous montrer comment créer une collection de données privées et comment effectuer des recherches dans cette dernière.
{: shortdesc}

## Avant de commencer
{: #before-you-begin}

- Créez une instance du service :
    - {: download} Si cela s'affiche, vous avez créé votre instance de service. A présent, procurez-vous vos données d'identification. 
    - Créez un projet à partir d'un service :
        1.  Accédez à la page {{site.data.keyword.watson}} Developer Console [Services ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.{DomainName}/developer/watson/services){: new_window}. 
        1.  Sélectionnez {{site.data.keyword.discoveryshort}}, cliquez sur **Add Services**, puis inscrivez-vous afin d'obtenir un compte {{site.data.keyword.Bluemix_notm}} gratuit ou connectez-vous. 
        1.  Tapez `discovery-tutorial` comme nom de projet et cliquez sur **Créer un projet**.
- Copiez les données d'identification afin de vous authentifier auprès de votre instance de service :
    - {: download} Depuis le tableau de bord de service (ce que vous voyez) :
        1.  Cliquez sur l'onglet **Données d'identification du service**. 
        1.  Cliquez sur **Afficher les données d'identification** sous **Actions**.
        1.  Copiez les valeurs `username`, `password` et `url`.
        {: download}
    - Depuis votre projet **discovery-tutorial** dans Developer Console, copiez les valeurs `username`, `password` et `url` pour `"discovery"` à partir de la section **Données d'identification**. 

<!-- Remove this text after dedicated instances have the Developer Console: begin -->

Si vous utilisez {{site.data.keyword.Bluemix_dedicated_notm}}, créez votre instance de service à partir de la page [{{site.data.keyword.discoveryshort}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.{DomainName}/catalog/services/discovery/){: new_window} dans le catalogue. Pour savoir comment trouver vos données d'identification du service, voir [Données d'identification de service pour les services Watson![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](/docs/services/watson/getting-started-credentials.html#getting-credentials-manually){: new_window}.

<!-- Remove this text after dedicated instances have the Developer Console: end -->

## Etape 1 : Création d'un environnement
{: #create-an-environment}

Dans un interpréteur de commandes bash ou un environnement équivalent, tel que Cygwin, utilisez la méthode `POST /v1/environments` pour créer un environnement. Considérez votre environnement comme un entrepôt dans lequel vous
stockez toutes vos boîtes de documents.

1.  Exécutez la commande suivante pour créer un environnement nommé `my-first-environment`. Remplacez `{username}` et `{password}` par les données d'identification de service que vous avez copiées précédemment :

    ```bash
    curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    L'API renvoie des informations, telles que votre ID d'environnement, le
statut de l'environnement et le volume de stockage utilisé par votre environnement. 

1.  Vérifiez le statut de l'environnement régulièrement jusque ce que le statut `ready` s'affiche.
    - Appelez la méthode `GET /v1/environments/{environment_id}` afin d'extraire le statut de votre environnement. Remplacez `{username}`, `{password}` et `{environment_id}` par vos informations : 

    ```bash
    curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}?version=2017-11-07
    ```
    {: pre}

    Vous ne pouvez créer une collection que lorsque le statut passe à `ready`. 

## Etape 2 : Création d'une collection
{: #create-a-collection}

A présent que l'environnement est prêt, vous pouvez créer une collection. Considérez
une collection comme une boîte dans laquelle vous stockez vos documents dans votre
environnement.

1.  Vous avez besoin en priorité de l'ID de votre configuration par défaut. Pour rechercher votre `configuration_id` par défaut, utilisez la méthode `GET /v1/environments/{environment_id}/configurations`. Remplacez `{username}`, `{password}` et `{environment_id}` par vos informations : 

    ```bash
      curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07
    ```
    {: pre}
1.  Utilisez la méthode `POST /v1/environments/{environment_id}/collections` pour créer une collection nommée **my-first-collection**. Remplacez`{username}`, `{password}`, `{environment_id}` et `{configuration_id}` par vos informations :

    ```bash
    curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{"name": "my-first-collection", "description": "exploring collections", "configuration_id":"{configuration_id}" , "language": "en_us"}' https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07
    ```
    {: pre}

L'API renvoie des informations, telles que votre ID de collection, le statut de la collection et le volume de stockage utilisé par votre collection.
1.  Vérifiez le statut de la collection régulièrement jusque ce que le statut `online` s'affiche.
    - Appelez la méthode `GET /v1/environments/{environment_id}/collections/{collection_id}` afin d'extraire le statut de votre collection. Une fois encore, remplacez `{username}`, `{password}`, `{environment_id}` et `{configuration_id}` par vos informations :

    ```bash
    curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07
    ```
    {: pre}

## Etape 3 : Téléchargement des exemples de document
{: #download-sample-documents}

Téléchargez les exemples de document suivants : <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe" class="style-scope doc-content"></a> et <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe" class="style-scope doc-content"></a>.

## Etape 4 : Téléchargement des documents
{: #upload-the-documents}

1.  A présent, ajoutez les exemples de document à votre collection. Cet exemple télécharge le document **test-doc1.html** dans votre collection. Remplacez  `{username}`, `{password}`, `{environment_id}` et `{configuration_id}` par vos informations. Modifiez l'emplacement de l'exemple de document afin de pointer vers l'endroit où vous avez sauvegardé le fichier `test-doc1.html`. 
    - Utilisez la méthode `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` :

        ```bash
        curl -X POST -u "{username}":"{password}" -F "file=@test-doc1.html" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2017-11-07
        ```
        {: pre}

    Vous pouvez aussi utiliser l'un des SDK répertoriés dans le document [API Reference ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window} :
    - Java :

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

    - Python :

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

    - Node.js :

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

1.  Répétez cette procédure pour chacun des 3 autres exemples de fichier. 

## Etape 5 : Lancement d'une requête sur votre collection
{: #query-your-collection}

Finalement, utilisez la méthode `GET
/v1/environments/{environment_id}/collections/{collection_id}/query` pour lancer une recherche dans votre collection de documents.

L'exemple ci-après renvoie toutes les entités nommées **IBM**. Remplacez`{username}`, `{password}`, `{environment_id}` et `{configuration_id}` par vos informations :

```bash
curl -u "{username}":"{password}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}*/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

## Etapes suivantes
{: #next-steps}

Vous avez lancé des requêtes sur des documents dans l'environnement et la collection que vous avez créés. A présent, vous pouvez commencer à personnaliser votre collection en ajoutant d'autres documents et enrichissements et en personnalisant les paramètres de conversion. Pour plus d'informations sur l'API, voir le document [API Reference ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}.
