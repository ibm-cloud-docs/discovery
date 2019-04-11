---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-01-14"

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

# Amélioration de la pertinence des résultats à l'aide de l'API
{: #improving-result-relevance-with-the-api}

Vous pouvez former le service {{site.data.keyword.discoveryshort}} afin d'améliorer la pertinence des résultats de requête pour votre organisation ou votre domaine. Lorsque vous fournissez des *données de formation* à une instance {{site.data.keyword.discoveryshort}}, le service utilise des techniques Watson d'apprentissage automatique pour retrouver des signaux dans votre contenu et vos questions. Ensuite, le service réorganise les résultats de requête afin d'afficher en premier ceux qui sont les plus pertinents. A mesure que vous ajoutez des données de formation, l'instance de service devient plus précise et plus sophistiquée dans l'organisation des résultats qu'elle renvoie.
{: shortdesc}

La formation pour la pertinence est facultative ; si les résultats de vos requêtes répondent à vos besoins, aucune autre formation n'est requise. Pour obtenir une présentation de la création de cas d'utilisation relatifs à la formation, voir l'article de blogue [How to get the most out of Relevancy Training ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developer.ibm.com/dwblog/2017/get-relevancy-training/){: new_window}.

Pour des informations complètes sur les API de formation, voir le document [API Reference ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery){: new_window}.

Si vous préférez utiliser les outils {{site.data.keyword.discoveryshort}} pour former {{site.data.keyword.discoveryshort}}, voir [Amélioration de la pertinence des résultats à l'aide des outils](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling).

**Remarque :** la formation pour la pertinence s'applique uniquement aux requêtes en langage naturel portant sur des collections privées. Elle n'est pas destinée à être utilisée avec des requêtes en langage de requête {{site.data.keyword.discoveryshort}} structurées.  Pour en savoir plus sur le langage de requête {{site.data.keyword.discoveryshort}}, voir [Concepts de requête](/docs/services/discovery?topic=discovery-query-concepts#query-concepts).

Les collections formées renverront un score `confidence` dans le résultat d'une requête en langage naturel. Pour plus d'informations, voir [Scores de confiance](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence).

L'ajout d'une liste de mots à exclure personnalisée peut améliorer la pertinence des résultats pour les requêtes en langage naturel. Pour plus d'informations, voir [Définition des mots à exclure](/docs/services/discovery?topic=discovery-query-concepts#stopwords).

Voir [Exigences relatives aux données de formation](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#reqs) pour connaître les exigences minimales pour l'apprentissage, ainsi que les limites d'apprentissage.

Voir [Surveillance de l'utilisation](/docs/services/discovery?topic=discovery-usage#usage) pour plus de détails sur le suivi de l'utilisation et l'utilisation de ces données pour vous aider à maîtriser et à améliorer vos applications.

<!-- A trained Discovery service instance is intended primarily for use with natural language queries, but it works equally well with queries that use structured syntax. -->  <!-- See [Query Concepts](/docs/services/discovery?topic=discovery-query-concepts#query-concepts) and the [Query reference](/docs/services/discovery?topic=discovery-query-reference#query-reference) for information about structured queries and natural language queries. -->

Les composants nécessaires pour former une instance Discovery sont notamment les suivants :

 - **Données de formation**. Ensemble de *requêtes* et d'*exemples* que le service utilise pour affiner les résultats de la requête.
 - **Requête**. Requête en langage naturel qui s'applique au jeu de données de formation.
   Chaque requête peut être associée à un ou plusieurs *exemples*, comme décrit dans le point suivant.
   Chaque requête doit être unique au sein du jeu de données de formation.
 - **Exemple**. Document indexé dans une collection Discovery qui agit en tant que modèle exemplaire, **bon ou mauvais**, pour la requête associée. Lorsque vous ajoutez un exemple à une requête de données de formation, vous incluez un libellé de pertinence qui indique la pertinence (ou "bonne qualité" par opposition à "mauvaise qualité") du document par rapport à la requête spécifiée.

   Les exemples sont identifiés par l'ID de document indexé. Comme indiqué, chaque exemple doit inclure un libellé qui indique la "bonne qualité" ou la "mauvaise qualité" du document en ce qui concerne la requête.

   Les exemples peuvent éventuellement spécifier une requête de référence croisée. La requête de référence croisée ne doit renvoyer que l'exemple de document et doit être indépendante de l'ID de document Watson Discovery unique. Pour l'instant, les requêtes de référence croisée ne sont pas utilisées automatiquement mais elles peuvent servir à réparer les données de formation lorsque de nouveaux ID sont affectés à des documents au cours d'un événement d'ingestion.

## Exigences relatives aux données de formation
{: #reqs}

Les données de formation doivent respecter les critères de qualité **minimum** ci-après pour améliorer de manière significative la pertinence des réponses qui sont renvoyées par le service Discovery. Notez que **minimum** ne signifie pas **optimal**. Le service vérifie les données de formation régulièrement afin de déterminer si ces exigences sont respectées, puis il se met à jour automatiquement en fonction des éventuelles modifications effectuées.

- Le jeu de données de formation d'une collection doit contenir au moins 49 requêtes de formation uniques (autrement dit, des ensembles de requêtes et d'exemples). Selon la taille et la complexité de votre collection, votre jeu devra peut-être contenir plus de 49 requêtes de formation pour permettre à Watson d'appliquer une formation de pertinence à la collection. Watson fournit des commentaires s'il a besoin de requêtes supplémentaires pour se former.
- Lors de l'affectation de niveaux de pertinence via l'API : Le score de pertinence pour chaque requête de formation doit être un nom entier non négatif, par exemple, `0` pour *non pertinent*, `1` pour *plutôt pertinent* et `2` pour *très pertinent*. Toutefois, pour fournir un maximum de flexibilité, le service accepte des entiers non négatifs compris entre `0` et `100` pour les utilisateurs avancés qui expérimentent différents schémas d'évaluation. Quelle que soit la plage que vous utilisez, le nombre entier le plus élevé dans le jeu de requêtes de formation indique une pertinence maximale.
- Lors de l'affectation de niveaux de pertinence via les outils : Les outils {{site.data.keyword.discoveryshort}} utilisent les scores de pertinence `0` pour *non pertinent* et `10` pour *pertinent*. Vous devez appliquer les deux évaluations disponibles suivantes à vos résultats : `Relevant` et `Not relevant`. Si vous n'évaluez que les documents `pertinents`, les données fournies ne seront pas suffisantes.  Si vous prévoyez d'évaluer vos documents à l'aide des outils et de l'API {{site.data.keyword.discoveryshort}} ou si vous prévoyez de commencer avec l'API, puis d'utiliser les outils, utilisez les scores de pertinence `0` et `10`.
- Les requêtes de formation doivent inclure un chevauchement de termes entre la requête et la réponse souhaitée de manière à permettre l'extraction de celle-ci par la recherche initiale du service Discovery dont la portée est étendue.

**Remarque :** Watson utilise des données de formation pour apprendre des modèles et pour généraliser, et non mémoriser, des requêtes de formation individuelles. Par conséquent, il peut arriver que le service ne reproduise pas toujours des résultats ayant une pertinence identique pour une requête de formation donnée.

La formation ne doit pas dépasser les exigences **maximales** suivantes :
  - Vous ne pouvez pas dépasser 24 collections formées par environnement.
  - Au sein d'une même collection, vous êtes limité à 10 000 requêtes de formation, avec un maximum de 100 exemples par requête. 

## Ajout d'une requête au jeu de données de formation
{: #adding-a-query}

Utilisez la méthode `POST /v1/environments/{environment_id}/collections/{collection_id}/training_data` pour ajouter une requête au jeu de données de formation d'une collection. La requête est spécifiée en tant qu'objet JSON au format suivant :

```json
{
  "query_id": "string",
  "natural_language_query": "string",
  "filter": "string",
  "examples": [
    {
      "document_id": "string",
      "cross_reference": "string",
      "relevance": 0
    }
  ]
}
```
{: codeblock}

Les valeurs présentes dans cet objet sont les suivantes :

- `query_id` : ID unique de la requête. Si vous ne renseignez pas cette zone, un ID est généré automatiquement par le service.
- `natural_language_query` : requête en langage naturel qui s'applique au jeu de données de formation. <!-- The `natural_language_query` parameter is preferred. -->
- `filter` : filtre facultatif pour la requête, tel qu'il est décrit dans la rubrique [Référence de requête](/docs/services/discovery?topic=discovery-query-reference#parameter-descriptions).

    **Remarque :** si vous incluez des filtres dans vos requêtes de données de formation, prenez soin d'utiliser les mêmes filtres lorsque vous exécutez des requêtes en langage naturel dans votre collection formée. Si vous formez la collection avec des données filtrées et que vous n'utilisez pas les mêmes types de filtre lorsque vous exécutez une requête sur la collection, les résultats peuvent être imprévisibles.

- `examples` : tableau qui contient les valeurs suivantes :

   - `document_id` : ID unique du document qui s'applique au jeu de données de formation. Il s'agit de l'élément *example* décrit précédemment.
   - `cross_reference` : libellé facultatif, composé généralement d'une zone dans le document référencé, qui "épingle" le document et les informations de la zone si l'ID du document vient à changer, par exemple, si le même ID est affecté à un document nouvellement ingéré. Le fait de spécifier une valeur pour `cross-reference` ne permet **pas** de lier un document à un autre, mais cela permet de s'assurer que le service conserve les informations pertinentes du document si ce dernier est renommé ou écrasé.
   - `relevance` : entier compris entre `0` et `100` (inclus) indiquant la pertinence relative de la requête par rapport aux données de formation. Des valeurs supérieures indiquent une pertinence plus élevée. La valeur `0` indique qu'il n'y a aucune pertinence par rapport à la requête, tandis que la valeur `100` indique que la pertinence avec la requête est absolue.

   **Remarque :** bien que les valeurs possibles pour le paramètre `relevance` soient comprises entre `0` et `100` pour fournir un maximum de flexibilité, vous pouvez utiliser une plus petite plage de valeurs pour simplifier les exemples d'évaluation. Une plage de valeurs standard peut s'étendre de `0` à `4`, ou vous pouvez utiliser la plage dans son intégralité, mais vous ne devez utiliser que des incréments de 20 (`0`, `20`, `40`, `60`, `80` et `100`). Les outils {{site.data.keyword.discoveryshort}} utilisent les scores de pertinence `0` pour *non pertinent* et `10` pour *pertinent*. Si vous prévoyez d'évaluer vos documents à l'aide des outils et de l'API {{site.data.keyword.discoveryshort}} ou si vous prévoyez de commencer avec l'API, puis d'utiliser les outils, utilisez les scores de pertinence `0` et `10`.

L'objet suivant illustre une requête de données de formation renseignée :

```json
{
  "natural_language_query": "why is the sky blue",
  "filter": "text:meteorology",
  "examples": [
    {
      "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877",
      "relevance": 0
    },
    {
      "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81",
      "relevance": 1
    },
    {
      "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da",
          "cross_reference": "my_id_field:1463",
          "relevance": 4
        }
  ]
}
```
{: codeblock}

L'exemple suivant ajoute la requête de données de formation précédente à une collection nommée `99040100-fe6a-4782-a4f5-28f9eee30850` dans un environnement nommé `a56dd9b4-040b-4ea3-a736-c1e7a467e191`:

```bash
curl -X POST -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" -H "Content-Type: application/json" -d
'{
  "natural_language_query": "why is the sky blue",
  "filter": "text:meteorology",
  "examples": [
    {
    "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877",
          "relevance": 0
    },
    {
      "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81",
      "relevance": 1
    },
    {
      "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da",
          "cross_reference": "my_id_field:1463",
          "relevance": 4
        }
  ]
}'
"https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data?version=2016-12-01"
```
{: pre}

## Ajout d'un exemple à une requête de données de formation
{: #adding-an-example}

Après avoir créé une requête de données de formation, vous pouvez continuer à y ajouter des exemples afin d'améliorer l'exactitude de la formation. Utilisez la méthode `POST /v1/environments/{environment_id}/collections/{collection_id}/training_data/{query_id}` pour ajouter un exemple à une requête de données de formation existante.

Procédez comme suit pour ajouter un exemple à une requête de données de formation :

1. Procurez-vous l'ID de requête de la requête de données de formation à laquelle vous souhaitez ajouter un nouvel exemple en[répertoriant les requêtes de données de formation d'une collection ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery#list-training-data){: new_window} :

   ```bash
    curl -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" "https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data?version=2016-12-01"
   ```
   {: pre}

   L'objet JSON renvoyé est au format suivant :

   ```json
    {
      "query_id": "484baad4-d440-44b7-a0dd-70bb2ac77baa",
      "natural_language_query": "why is the sky blue",
      "filter": "text:meteorology",
      "examples": [
        {
          "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877",
          "relevance": 0
        },
        {
          "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81",
          "relevance": 1
        },
        {
          "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da",
          "cross_reference": "my_id_field:1463",
          "relevance": 4
        }
      ]
    }
   ```
   {: codeblock}

1. Ajoutez le nouvel exemple en employant la même syntaxe que celle utilisée pour définir des exemples lors de la création d'une nouvelle requête de données de formation. L'exemple de commande suivant n'inclut pas de référence croisée :

   ```bash
    curl -u -X POST -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" -H "Content-Type: application/json" -d
    '{
      "document_id": "46b52fdc-3a72-4700-9849-ac217532b373",
      "relevance": 3
    }' "https://gateway.watsonplatform.net/discovery/api/v1/environments//a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data/484baad4-d440-44b7-a0dd-70bb2ac77baa?version=2016-12-01"
   ```
   {: pre}

1. Vérifiez que le nouvel exemple a été ajouté à la requête de données de formation en[répertoriant une nouvelle fois les requêtes de données de formation d'une collection ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery#list-training-data){: new_window} :

   ```bash
    curl -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" "https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data?version=2016-12-01"
   ```
   {: pre}

   L'objet JSON renvoyé est au format suivant :

   ```json
    {
      "query_id": "484baad4-d440-44b7-a0dd-70bb2ac77baa",
      "natural_language_query": "why is the sky blue",
      "filter": "text:meteorology",
      "examples": [
        {
          "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877",
          "relevance": 0
        },
        {
          "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81",
          "relevance": 1
        },
        {
          "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da",
          "cross_reference": "my_id_field:1463",
          "relevance": 4
        },
        {
          "document_id": "46b52fdc-3a72-4700-9849-ac217532b373",
          "relevance": 3
        }
      ]
    }
   ```
   {: codeblock}

1. Vérifiez le statut de la formation en utilisant la méthode qui consiste à [afficher les détails d'une collection ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery#get-collection-details){: new_window} et en recherchant la valeur de la zone `"training"`/`"available"`. Lorsque vous avez ajouté suffisamment de requêtes et d'exemples pour répondre aux exigences de formation, la valeur renvoyée pour la zone est `true` et le service commence automatiquement à utiliser les données de formation.

   ```bash
    curl -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" "https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850?version=2016-12-01"
   ```
   {: pre}

   L'objet JSON renvoyé est au format suivant :

   ```json
    {
      "collection_id": "99040100-fe6a-4782-a4f5-28f9eee30850",
      "name": "democollection",
      "configuration_id": "def9bd08-8472-470f-ab5a-e377f77e9300",
      "language": "en_us",
      "status": "available",
      "description": "this is a demo collection",
      "created": "2015-08-24T18:42:25.324Z",
      "updated": "2015-08-24T18:42:25.324Z",
      "document_counts": {
        "available": 1000,
        "processing": 20,
        "failed": 180
      },
      "disk_usage": {
        "used_bytes": 895111
      },
      "training_status": {
        "data_updated": "2017-02-10T14:18:22.786Z",
        "total_examples": 54,
        "sufficient_label_diversity": false,
        "processing": false,
        "minimum_examples_added": true,
        "successfully_trained": "2017-02-08T14:18:22.786Z",
        "available": true,
        "notices": 13,
        "minimum_queries_added": true
      }
    }
   ```
   {: codeblock}

1. Lorsque la valeur renvoyée pour les zones suivantes à l'étape précédente est `true`, exécutez des exemples de requête pour voir si le service renvoie des résultats plus pertinents :

   - `minimum_queries_added`
   - `minimum_examples_added`
   - `sufficient_label_diversity`

   Si la pertinence de vos résultats ne s'est pas améliorée, ajoutez d'autres requêtes de formation jusqu'à ce que les résultats soient conformes à vos attentes.

Pour plus de conseils sur la formation, voir [Astuces pour la formation de pertinence](/docs/services/discovery?topic=discovery-relevancy-tips#relevancy-tips).   

## Exécution d'autres opérations de requête de données de formation
{: #training-data-operations}

Vous pouvez administrer et gérer des requêtes de données de formation en utilisant d'autres méthodes API, comme indiqué dans le document [API Reference ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery){: new_window}:

 - [Afficher les données de formation d'une collection ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery#list-training-data){: new_window}
 - [Supprimer toutes les données de formation d'une collection ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery#delete-all-training-data){: new_window}
 - [Afficher le contenu d'une requête de données de formation spécifiée![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery#get-details-about-a-query){: new_window}
 - [Supprimer une requête de données de formation de la collection![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/watson/developercloud/discovery/api/v1#delete-example-for-training-data-query){: new_window}
 - [Modifier le libellé de pertinence ou la référence croisée d'un exemple de requête de données de formation![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery#change-label-or-cross-reference-for-example){: new_window}
 - [Supprimer un exemple de document d'une requête de données de formation![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery#list-training-data){: new_window}

 **Surveillance des erreurs :** des erreurs de données de formation apparaissent dans les avis et vous pouvez les surveiller à l'aide de l'[API notices ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery#query-system-notices){: new_window}
 (`GET /v1/environments/{environment_id}/collections/{collection_id}/notices`).
