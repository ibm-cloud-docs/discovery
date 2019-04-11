---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-08"

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

# Migration à partir de AlchemyData News
{: #migrate-adn}

Une nouvelle version de {{site.data.keyword.discoverynewsfull}} a débuté le **31 juillet 2017**. Pour visualiser une description de cette collection, voir [Watson Discovery News](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news).

Le retrait de AlchemyData News est prévu le **7 mars 2018**.

## Comparaison des services
{: #service-adn}

Les différentes suivantes sont notables lors du passage de AlchemyData News à {{site.data.keyword.discoverynewsshort}} dans le service {{site.data.keyword.discoveryshort}} :

- {{site.data.keyword.discoveryshort}} facture les requêtes de nouvelles par requête uniquement. Toutes les zones sont disponibles pour être renvoyées avec chaque résultat sans coût supplémentaire.
- Chaque requête {{site.data.keyword.discoveryshort}} peut renvoyer un maximum de 50 résultats. Un paramètre `offset` est disponible et vous permet de paginer les requêtes en fonction du nombre de résultats dont vous avez besoin.
- Par ailleurs, {{site.data.keyword.discoveryshort}} prend en charge les agrégations. Pour plus d'informations, voir la section [aggregations](/docs/services/discovery?topic=discovery-query-reference#aggregations) de la documentation {{site.data.keyword.discoveryshort}}.
- La méthode de classement utilisée par {{site.data.keyword.discoverynewsfull}} est différente de celle utilisée par AlchemyData News. Il n'existe actuellement aucune zone à classer.
- La structure de requête et la structure de données renvoyées diffèrent entre {{site.data.keyword.discoverynewsshort}} et AlchemyData News. Une méthode efficace pour bien comprendre la structure JSON consiste à exécuter une requête sur un seul résultat dans {{site.data.keyword.discoverynewsshort}} et à inspecter le résultat.
- {{site.data.keyword.discoverynewsshort}} ne prend pas en charge les sorties XML.
- Le dédoublonnage est une fonction bêta dans {{site.data.keyword.discoverynewsshort}}.

## Différences d'authentification
{: #auth-adn}

Le service {{site.data.keyword.discoveryshort}} utilise les données d'identification {{site.data.keyword.Bluemix_notm}} `username` et `password` standard pour accéder aux requêtes. Cela remplace la méthode de clé d'API existante utilisée par AlchemyData News. Toutes les requêtes {{site.data.keyword.discoveryshort}} doivent être écrites avec une combinaison de nom d'utilisateur et de mot de passe créée par une instance de service {{site.data.keyword.discoveryshort}}.

Vous pouvez gérer les données d'identification de service en consultant l'onglet **Service Credentials** de votre service dans {{site.data.keyword.Bluemix_notm}}.

## Configuration d'une instance Discovery
{: #config-adn}

La méthode de création d'une instance de service {{site.data.keyword.discoveryshort}} est identique à celle qui permet de créer une instance AlchemyData News.

1. Accédez à [{{site.data.keyword.Bluemix_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/catalog/services/discovery){: new_window}, connectez-vous et sélectionnez  {{site.data.keyword.discoveryshort}} dans le catalogue de service.
1. Sélectionnez le plan adapté à vos besoins et cliquez sur **Create**.

  Le service {{site.data.keyword.discoveryshort}} offre un plan Lite avec 1000 requêtes de nouvelles disponibles tous les mois. Vous pouvez utiliser une instance de ce plan pour identifier des requêtes équivalentes sans avoir à les payer.
  {: tip}

1. Cliquez sur l'onglet **Service Credentials** et sélectionnez **View Credentials** pour identifier les valeurs `url`, `username` et `password` associées à cette instance.

## Exécution de requêtes sur Watson Discovery News
{: #querying-adn}

Vous pouvez exécuter des requêtes sur {{site.data.keyword.discoverynewsfull}} à l'aide de l'API ou de l'un des logiciels SDK {{site.data.keyword.watson}}. De plus, vous pouvez utiliser l'outil de génération de requête pour construire des requêtes de façon interactive.

Pour lancer les outils {{site.data.keyword.discoveryshort}} et exécuter des requêtes sur {{site.data.keyword.discoverynewsshort}} :

1. Cliquez sur **Lanch Tool** pour {{site.data.keyword.discoveryshort}} sous **Services**.
1. Cliquez sur la vignette {{site.data.keyword.discoverynewsshort}} pour ouvrir l'écran **Manage data**.
1. Cliquez sur **View data schema**, puis sur **Build queries** pour ouvrir le générateur de requête.

  Les requêtes dans {{site.data.keyword.discoverynewsfull}} sont structurées de la même façon que les requêtes écrites pour des collections de données privées. Voir [Concepts de requête](/docs/services/discovery?topic=discovery-query-concepts#query-concepts) et [Référence de requête](/docs/services/discovery?topic=discovery-query-reference#query-reference).
  {: tip}

Ne vous attendez pas à obtenir des résultats identiques pour des requêtes similaires dans AlchemyData News et dans {{site.data.keyword.discoverynewsfull}}. La durée d'exploration, les sources et les enrichissements sont autant de facteurs qui contribuent à générer des résultats différents.
{: note}

## Ajout de requêtes Watson Discovery News à votre application
{: #queries-adn}

Utilisez l'une des méthodes ci-après pour ajouter des requêtes à votre application. Tous ces exemples illustrent une requête portant sur `enriched_text.entities` avec la `IBM` pour `text` (`enriched_text.entities.text:IBM`).

Dans tous les exemples suivants, remplacez `{username}` et `{password}` par le nom d'utilisateur et le mot de passe indiqués sur la page **Service Credentials** de votre instance de service.

### Utilisation d'appels directs vers l'API
{: #api-adn}

```bash
curl -u "{username}":"{password}"  'https://gateway.watsonplatform.net/discovery/api/v1/environments/system/collections/news/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

### Utilisation du logiciel SDK Java
{: #javasdk-adn}

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

### Utilisation du logiciel SDK Watson Node.js
{: #nodesdk-adn}

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

### Utilisation du logiciel SDK Watson Python
{: #pythonsdk-adn}

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
