---

copyright:
  years: 2015, 2018
lastupdated: "2018-01-16"

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

# Migration à partir de Watson Discovery News Original
{: #migrate-bwdn}

Une nouvelle version de {{site.data.keyword.discoverynewsshort}} a débuté le **31 juillet 2017**. La version d'origine a été renommée {{site.data.keyword.discoverynewsshort}} Original et retirée du service le **15 janvier 2018**. Si vous tentez d'accéder à {{site.data.keyword.discoverynewsshort}} Original, vous recevrez le message `410 GONE`.
{: shortdesc}

Pour effectuer une migration à partir de {{site.data.keyword.discoverynewsshort}} Original vers la nouvelle version, vous devez effectuer plusieurs modifications, y compris la mise à jour des requêtes créées pour {{site.data.keyword.discoverynewsshort}} Original.

  **Remarque :** {{site.data.keyword.discoverynewsshort}} Original était disponible uniquement dans les instances de {{site.data.keyword.discoveryshort}} créées avant le **31 juillet 2017** et a été retiré du service le **15 janvier 2018**.

Pour visualiser une description de cette collection, voir [Watson Discovery News](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news).

Pour obtenir une description et des informations relatives à la création de requêtes sur {{site.data.keyword.discoverynewsshort}} Original, voir [Watson Discovery News Original](/docs/services/discovery?topic=discovery-discovery-archives#watson-discovery-news-original).

## Comparaison des services
{: #service-bwdn}

| {{site.data.keyword.discoverynewsshort}} Original         | {{site.data.keyword.discoverynewsshort}}           |
|----------------------------------------|---------------------------------|
| **{{site.data.keyword.discoverynewsshort}} Original** était préenrichi avec les enrichissements Alchemy Language suivants : Keyword Extraction, Entity Extraction, Concept Tagging, Relation Extraction, Sentiment Analysis et Taxonomy Classification. Les métadonnées suivantes étaient également ajoutées : date d'exploration, date de publication, classement d'URL, classement d'hôte et texte d'ancrage.     | **{{site.data.keyword.discoverynewsshort}}** est préenrichi avec les enrichissements suivants : {{site.data.keyword.nlushort}} (NLU) : Keyword Extraction, Entity Extraction, Semantic Role Extraction, Sentiment Analysis, Relations et Category Classification. Les métadonnées suivantes sont également ajoutées : date d'exploration et date de publication. Pour en savoir plus sur les enrichissements NLU, voir [Ajout d'enrichissements](/docs/services/discovery?topic=discovery-configservice#adding-enrichments).                         |
| **{{site.data.keyword.discoverynewsshort}} Original** était accessible via un environnement qui était unique pour votre instance de service.                       | Lorsque **{{site.data.keyword.discoverynewsshort}}** est utilisé, tous les utilisateurs exécutent une requête portant sur le même environnement et la même collection. Cela signifie que toutes les références à votre environnement et à votre collection doivent être modifiées.      |
| Dans **{{site.data.keyword.discoverynewsshort}} Original**, vous avez reçu des informations, telles que la taille de la collection, le nombre de documents, etc. lors de l'extraction de l'environnement via l'API.  | L'API **{{site.data.keyword.discoverynewsshort}}** ne renvoie pas ces informations.                          |

Les nouvelles zones suivantes sont disponibles dans **{{site.data.keyword.discoverynewsshort}}** :

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

De nombreuses zones ont également été retirées, par exemple, `blekko.hostrank`, `duplicate_url`, `domain`, etc. Pour obtenir une liste complète, cliquez <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/News_migration_v_1.01.xlsx" download>ICI <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe"></a>.

## Déplacement de requêtes vers le nouveau service Watson Discovery News
{: #queries-bwdn}

Pour déplacer vos requêtes depuis {{site.data.keyword.discoverynewsshort}} Original vers le nouveau service {{site.data.keyword.discoverynewsshort}}, vous devez modifier toutes les requêtes existantes en procédant comme suit :  

- Modifiez l'ID d'environnement appelé par la requête. Le nom d'environnement News normalisé sur toutes les instances de service {{site.data.keyword.discoveryshort}} est le suivant :

  `system`  

- Modifiez l'ID de collection appelé par la requête. Le nom de collection News normalisé sur toutes les instances de service {{site.data.keyword.discoveryshort}} est le suivant :

  `news`

- Modifiez la requête pour utiliser la nouvelle structure de chemin JSON pour le nouveau service {{site.data.keyword.discoverynewsshort}}. Le chemin de la plupart des zones a été changé, plusieurs zones ont été ajoutées et un groupe choisi de valeurs inférieures a été retiré. Pour plus d'informations sur la feuille de calcul de migration des zones, cliquez <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/News_migration_v_1.01.xlsx" download>ICI  <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe"></a>). Par exemple, la requête suivante :

  `discovery/api/v1/environments/ae5790c2-592f-432a-804a-ee16de7154d7/collections/3edcd8f1-e25a-4f44-a069-58332ad17651/query?version=2017-11-07&query=entities.type:"Company"`

  Doit être remplacée par :

  `discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.type:"Company"`  

## Exécution de requêtes sur Watson Discovery News
{: #querying-bwdn}

Vous pouvez exécuter des requêtes sur {{site.data.keyword.discoverynewsshort}} à l'aide de l'API ou de l'un des logiciels SDK {{site.data.keyword.watson}}. De plus, vous pouvez utiliser l'outil de génération de requête pour construire des requêtes de façon interactive.

**Pour lancer les outils {{site.data.keyword.discoveryshort}} et exécuter des requêtes sur {{site.data.keyword.discoverynewsshort}} :**

1. Cliquez sur **Lanch Tool** pour {{site.data.keyword.discoveryshort}} sous **Services**.
1. Cliquez sur la vignette {{site.data.keyword.discoverynewsshort}} pour ouvrir l'écran **Manage data**.
1. Cliquez sur **View data schema**, puis sur **Build queries** pour ouvrir le générateur de requête.

  Les requêtes dans {{site.data.keyword.discoverynewsshort}} sont structurées de la même façon que les requêtes écrites pour des collections de données privées. Voir [Concepts de requête](/docs/services/discovery?topic=discovery-query-concepts#query-concepts) et [Référence de requête](/docs/services/discovery?topic=discovery-query-reference#query-reference).
  {: tip}

**Remarque :** ne vous attendez pas à obtenir des résultats identiques pour des requêtes similaires dans {{site.data.keyword.discoverynewsshort}} Original et {{site.data.keyword.discoverynewsshort}}. La durée d'exploration, les sources et les enrichissements sont autant de facteurs qui contribuent à générer des résultats différents.

## Ajout de requêtes Watson Discovery News à votre application
{: #add-queries-bwdn}

Utilisez l'une des méthodes ci-après pour ajouter des requêtes à votre application. Tous ces exemples illustrent une requête portant sur `enriched_text.entities` avec la `IBM` pour `text` (`enriched_text.entities.text:IBM`).

Dans tous les exemples suivants, remplacez `{username}` et `{password}` par le nom d'utilisateur et le mot de passe indiqués sur la page **Service Credentials** de votre instance de service.

### Utilisation d'appels directs vers l'API
{: #api-bwdn}

```bash
curl -u "{username}":"{password}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

### Utilisation du logiciel SDK Watson Java
{: #javasdk-bwdn}

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

### Utilisation du logiciel SDK Watson Node.js
{: #nodesdk-bwdn}

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

### Utilisation du logiciel SDK Watson Python
{: #pythonsdk-bwdn}

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
