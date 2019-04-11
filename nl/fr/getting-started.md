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

# Initiation à l'API
{: #gs-api}

Dans ce bref tutoriel, nous allons vous présenter l'API {{site.data.keyword.discoveryshort}} et vous montrer comment créer une collection de données privées et comment effectuer des recherches dans cette dernière.
{: shortdesc}

Si vous préférez travailler dans les outils {{site.data.keyword.discoveryshort}}, voir [Initiation](/docs/services/discovery?topic=discovery-getting-started#getting-started).
{: tip}

## Avant de commencer
{: #before-you-begin-api}

- Créez une instance du service :
    1.  Accédez à la page [{{site.data.keyword.discoveryshort}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/catalog/services/discovery) du catalogue {{site.data.keyword.cloud_notm}}.
        Si vous ne choisissez pas de groupe de ressources, l'instance de service est créée dans le groupe **default**. Vous ne pourrez plus en changer** ultérieurement. Ce groupe est suffisant lorsque vous essayez le service.
        Si vous créez une instance pour une utilisation plus avancée, consultez les informations présentant les [groupes de ressources ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/docs/resources/bestpractice_rgs.html#bp_resourcegroups){: new_window}.
    1.  Inscrivez-vous pour un compte {{site.data.keyword.cloud_notm}} gratuite ou connectez-vous.
    1.  Cliquez sur **Create**. Une fois que vous avez créé une instance du service {{site.data.keyword.discoveryshort}}, la liste de vos services s'affiche.
- Copiez les données d'identification afin de vous authentifier auprès de votre instance de service :
    1.  Dans la [liste de ressources](https://{DomainName}/dashboard/), cliquez sur votre instance de service {{site.data.keyword.discoveryshort}} pour accéder à la page du tableau de bord du service {{site.data.keyword.discoveryshort}}.
    1.  Sur la page **Manage**, cliquez sur **Show Credentials** pour afficher vos données d'identification.
    1.  Copiez la clé d'API`` et les valeurs d'URL``.

        Dans certaines instances, vous vous authentifiez en fournissant une authentification de base. Si vous voyez `username` et `password` dans les données d'identification, utilisez ces valeurs et non `"apikey:{apikey}"` dans les exemples de ce tutoriel.
        {: tip}

## Etape 1 : Création d'un environnement
{: #create-an-environment}

Dans un interpréteur de commandes bash ou un environnement équivalent, tel que Cygwin avec l'application `curl`, utilisez la méthode `POST /v1/environments` pour créer un environnement. Considérez votre environnement comme un entrepôt dans lequel vous
stockez toutes vos boîtes de documents.

Ce tutoriel utilise une clé d'interface de programmation (API) pour l'authentification. Pour une utilisation en production, veillez à étudier les [pratiques recommandées](/docs/services/watson/apikey-bp.html#api-bp) en matière de clé d'API.
{: important}

1.  Exécutez la commande suivante pour créer un environnement nommé `my-first-environment`. Remplacez `{apikey}` et `{url}` par la clé d'API et l'URL copiées précédemment :

    ```bash
    curl -X POST -u "apikey:{apikey}" -H "Content-Type: application/json" -d "{\"name\":\"my-first-environment\", \"description\":\"exploring environments\"}" "{url}/v1/environments?version=2018-12-03"
    ```
    {: pre}

    L'API renvoie des informations, telles que votre ID d'environnement, le
statut de l'environnement et le volume de stockage utilisé par votre environnement.

1.  Vérifiez le statut de l'environnement régulièrement jusqu'à ce que le statut `active` s'affiche.

    Appelez la méthode `GET /v1/environments/{environment_id}` afin d'extraire le statut de votre environnement. Remplacez `{apikey}`, `{url}` et `{environment_id}` par vos informations :

    ```bash
    curl -u "apikey:{apikey}" "{url}/v1/environments/{environment_id}?version=2018-12-03"
    ```
    {: pre}

    Vous ne pouvez pas créer de collection tant que le statut n'est pas passé à `active`.

## Etape 2 : Création d'une collection
{: #create-a-collection-api}

A présent que l'environnement est prêt, vous pouvez créer une collection. Considérez
une collection comme une boîte dans laquelle vous stockez vos documents dans votre
environnement.

1.  Vous avez besoin en priorité de l'ID de votre configuration par défaut. Pour rechercher votre `configuration_id` par défaut, utilisez la méthode `GET /v1/environments/{environment_id}/configurations`. Remplacez `{apikey}`, `{url}` et `{environment_id}` par vos informations :
    ```bash
      curl -u "apikey:{apikey}" "{url}/v1/environments/{environment_id}/configurations?version=2018-12-03"
    ```
    {: pre}
1.  Utilisez la méthode `POST /v1/environments/{environment_id}/collections` pour créer une collection nommée **my-first-collection**. Remplacez `{apikey}`, `{url}`, `{environment_id}` et `{configuration_id}` par vos informations :
    ```bash
    curl -X POST -u "apikey:{apikey}" -H "Content-Type: application/json" -d "{\"name\": \"my-first-collection\", \"description\": \"exploring collections\", \"configuration_id\":\"{configuration_id}\" , \"language": \"en_us\"}" "{url}/v1/environments/{environment_id}/collections?version=2018-12-03"
    ```
    {: pre}
    L'API renvoie des informations, telles que votre ID de collection, le statut de la collection et le volume de stockage utilisé par votre collection.
1.  Vérifiez le statut de la collection régulièrement jusqu'à ce que le statut `active` s'affiche.

    Appelez la méthode `GET /v1/environments/{environment_id}/collections/{collection_id}` afin d'extraire le statut de votre collection. Une fois encore, remplacez `{apikey}`, `{url}`, `{environment_id}` et `{configuration_id}` par vos informations :

    ```bash
    curl -u "apikey:{apikey}" "{url}/v1/environments/{environment_id}/collections/{collection_id}?version=2018-12-03"
    ```
    {: pre}

## Etape 3 : Téléchargement des exemples de document
{: #download-sample-documents}

Téléchargez les exemples de document suivants : <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe"></a> et <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe"></a>.

Dans certains navigateurs, les liens précédents s'ouvrent dans une nouvelle fenêtre au lieu d'être sauvegardés localement. Dans ce cas, sélectionnez `Save As` dans le menu `File` de votre navigateur pour sauvegarder une copie du fichier.
{: tip}

## Etape 4 : Téléchargement des documents
{: #upload-the-documents}

1.  A présent, ajoutez les exemples de document à votre collection. Cet exemple télécharge le document **test-doc1.html** dans votre collection. Remplacez `{apikey}`, `{url}`, `{environment_id}` et `{collection_id}` par vos informations. Modifiez l'emplacement de l'exemple de document afin de pointer vers l'endroit où vous avez sauvegardé le fichier `test-doc1.html`.
    - Utilisez la méthode `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` :

        ```bash
        curl -X POST -u "apikey:{apikey}" -F "file=@test-doc1.html" "{url}/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2018-12-03"
        ```
        {: pre}

        Vous pouvez aussi utiliser l'un des SDK répertoriés dans le document [API Reference ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery){: new_window} :
    - Java :
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
    - Python :
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

    - Node.js :
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

1.  Répétez cette procédure pour chacun des 3 autres exemples de fichier.

## Etape 5 : Lancement d'une requête sur votre collection
{: #query-your-collection}

Finalement, utilisez la méthode `GET
/v1/environments/{environment_id}/collections/{collection_id}/query` pour lancer une recherche dans votre collection de documents.

L'exemple ci-après renvoie toutes les entités nommées **IBM**. Remplacez `{apikey}`, `{environment_id}` et `{collection_id}` par vos informations :

```bash
curl -u "apikey:{apikey}" "{url}/v1/environments/{environment_id}/collections/{collection_id}/query?version=2018-12-03&query=enriched_text.entities.text:IBM"
```
{: pre}

## Etapes suivantes
{: #next-steps-api}

Vous avez lancé des requêtes sur des documents dans l'environnement et la collection que vous avez créés. A présent, vous pouvez commencer à personnaliser votre collection en ajoutant d'autres documents et enrichissements et en personnalisant les paramètres de conversion.

- Lisez les informations sur l'API dans [API reference ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery){: new_window}
- [Configurez](/docs/services/discovery?topic=discovery-configservice#configservice) votre service.
- En savoir plus sur l'[authentification avec IAM ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/docs/services/watson/getting-started-iam.html#iam){: new_window}
