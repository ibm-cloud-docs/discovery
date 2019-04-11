---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-17"

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

# Surveillance de l'utilisation
{: #usage}

Vous pouvez surveiller et suivre l'utilisation de votre instance {{site.data.keyword.discoveryshort}}, et utiliser ces données pour vous aider à comprendre et à améliorer le fonctionnement de vos applications. L'[API d'événement ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery#create-event){: new_window} peut être utilisée pour créer des entrées de journal associées à des requêtes et actions spécifiques en langage naturel. Vous pouvez, par exemple, enregistrer quels documents d'un ensemble de résultats ont été "cliqués" par utilisateur et quand le clic s'est produit.

**Remarque :** Les journaux et événements sont surveillés uniquement pour les requêtes en langage naturel sur des collections de données privées. Les journaux ne sont pas collectés sur {{site.data.keyword.discoverynewsfull}}.

{{site.data.keyword.discoveryshort}} peut consigner les informations suivantes :
- **Queries** - Requêtes en langage naturel exécutées sur des collections de votre environnement 
- **Impressions** (ou **Results**) -  Résultats renvoyés pour une requête particulière, généralement des documents ou des passages 
- **Events** (événements) - Interactions effectuées par un utilisateur sur un résultat ou un ensemble de résultats dans {{site.data.keyword.discoveryshort}} (par exemple, un clic sur un résultat de document)

Les **requêtes** et **impressions** sont automatiquement consignées ; la consignation des **événements** peut être intégrée à votre application via l'API.

## Affichage des journaux
{: #viewlogs}

Vous pouvez effectuer une recherche dans la requête et le journal des événements afin de trouver les session de requête correspondant aux critères spécifiés. La recherche sur le noeud final `logs` utilise la syntaxe de requête {{site.data.keyword.discoveryshort}} standard pour les paramètres pris en charge. Le noeud final fournit une fonction de requête de base pour l'affichage et la recherche dans les données enregistrées.  

Le noeud final `/api/v1/logs` prend en charge les paramètres de requête {{site.data.keyword.discoveryshort}} suivants :
- query 
- filter
- sort
- count 
- offset
- version

Pour des détails supplémentaires sur la fonction et la syntaxe des paramètres, voir [Paramètres de requête](/docs/services/discovery?topic=discovery-query-parameters#query-parameters).

Exemple de recherche dans les journaux d'une requête en langage naturel contenant le terme “train” :

`https://gateway.watsonplatform.net/discovery/api/v1/logs?version=2018-03-28&query=train`

La réponse d'une requête `logs` inclut les résultats qui semblent similaires aux résultats du document {{site.data.keyword.discoveryshort}}. Chaque résultat est une requête ou un événement, spécifié dans la zone `type` du document.  

Exemple de journal des requêtes :

```
{
            "customer_id": "",
            "environment_id": "252e6e82-c2d2-450e-9670-0008b0a3a99c",
            "natural_language_query": "how do i get from the airport to the city",
            "query_id": "_Qs35yOoa7",
            "document_results": {
                "count": 2,
                "results": [
                    {
                        "collection_id": "af9e1f41-6114-4d77-bca6-c9b99b2601b1",
                        "score": 6.724753491503856,
                        "position": 1,
                        "document_id": "4193eaa727d79b0f74597356dbcbb9a7"
                    },
                    {
                        "collection_id": "af9e1f41-6114-4d77-bca6-c9b99b2601b1",
                        "score": 5.791631414211986,
                        "position": 2,
                        "document_id": "bdcd6a9cc1438a3faa8c925f6a8d9429"
                    }
                ]
            },
            "event_type": "query",
            "session_token": "1_LKczxWGEWx5TJAi1_Qs35yOoa7",
            "created_timestamp": "2018-09-12T05:20:07.469Z"
        }
```

Les journaux de requêtes vous permettent d'examiner le type des résultats renvoyés à vos utilisateurs finaux ainsi que d'étudier les façons d'améliorer la qualité des résultats à l'aide des approches disponibles dans {{site.data.keyword.discoveryshort}}. Par exemple : 
- Entraînement visant à améliorer la pertinence (voir [Amélioration de la pertinence des résultats à l'aide de l'API](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api) et [Amélioration de la pertinence des résultats à l'aide des outils](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling))
- [Opérateurs de requête](/docs/services/discovery?topic=discovery-query-operators#query-operators)
- [Extension de requête](/docs/services/discovery?topic=discovery-query-concepts#query-expansion)
- Configurations personnalisées (voir la [Référence de configuration](/docs/services/discovery?topic=discovery-configref#configref))

## Création de journaux des événements
{: #eventlogs}

Les journaux des événements sont utilisés pour le suivi des interactions des utilisateurs au sein de votre application. Ils peuvent vous aider à comprendre comment votre application s'exécute, ainsi qu'à identifier les zones sur lesquelles vous concentrer pour améliorer les résultats. {{site.data.keyword.discoveryshort}} fournit une API qui peut être imbriquée dans votre application pour suivre les événements. L'appel de cette API avec les informations appropriées lorsqu'un utilisateur effectue une action retourne un signal à {{site.data.keyword.discoveryshort}} qui peut être consulté dans les journaux. 

Les événements permettent de collecter des informations sur les métriques de calcul (comme le taux de clics de sortie) afin de mesurer l'efficacité de l'application pour aider les utilisateurs finaux à trouver les informations pertinentes, ou ils peuvent être utilisés pour faciliter l'apprentissage via l'examen des requêtes et des clics pour commencer à générer des données de référence. 

Vous pouvez ajouter cette API partout où des utilisateurs interagissent avec vos résultats. Ainsi, dans une interface utilisateur de recherche, vous pouvez vouloir l'ajouter quand un utilisateur clique sur un lien de document, ou bien, dans une interface d'agent conversationnel, vous pouvez vouloir l'utiliser pour le suivi quand un utilisateur clique sur un bouton **Expand** (développer) ou **More details** (plus de détails).

Les résultats de {{site.data.keyword.discoveryshort}} renvoient des informations supplémentaires utilisables pour des événements de suivi, notamment un jeton de session. 

`"matching_results": 179,`
`"session_token": "1_LKczxWGEWx59fYD0_VV8HFUpb6"`

Pour enregistrer un événement, exécutez une commande POST sur le noeud final `/api/v1/events`. Voir
l'[API Events ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery#create-event){: new_window} pour plus de détails.

Une fois qu'un événement est enregistré, il peut être relu via le noeud final `/api/v1/logs`. Joignez des événements à la requête associée en utilisant `session_token`.
