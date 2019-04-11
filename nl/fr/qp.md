---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-18"

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

# Performances des requêtes
{: #qp}

Les performances des requêtes dans {{site.data.keyword.discoveryshort}} dépendent de plusieurs facteurs. 

## Evaluation des performances 
{: #qp-evaluate}

Si vous attendez une charge simultanée élevée sur votre application, il est important d'évaluer les performances de votre application {{site.data.keyword.discoveryshort}}. Plusieurs facteurs sont généralement utilisés pour mesurer les performances :
1.  **Temps d'attente des réponses** - Durée s'écoulant avant que {{site.data.keyword.discoveryshort}} ne renvoie les résultats de votre requête. 
    - Le temps d'attente peut varier en fonction du nombre de facteurs. Pour plus d'informations, voir [Facteurs ayant un impact sur les performances](/docs/services/discovery?topic=discovery-qp#perffactors). 
    - Il est important d'exécuter des tests dans votre environnement de production en utilisant un ensemble représentatif de requêtes afin de déterminer votre durée d'attente moyenne. 
1.   **Débit de requête** - Nombre de requêtes pouvant être traitées dans une période donnée. Cette mesure s'effectue généralement en requêtes par seconde (QPS). Elle est importante lorsque vous attendez une charge simultanée élevée sur votre application.  
     - Le débit pouvant être atteint dépend d'un grand nombre de facteurs, comme le temps d'attente. 
     - Le débit de requête doit également être évalué avec des requêtes représentatives et au niveau des charges prévues. Pensez à prendre en compte les pics de charge lors du test.

## Facteurs ayant un impact sur les performances
{: #perffactors}

Les performances des requêtes dans {{site.data.keyword.discoveryshort}} varient en fonction de plusieurs facteurs, incluant la taille du plan, la complexité des requêtes, les fonctions utilisées ainsi que la complexité et la taille de la collection.

### Taille de plan
{: #qp-plansize}

Les plans de tarification {{site.data.keyword.discoveryshort}} limitent le nombre de documents disponibles et offrent également la possibilité de gérer une charge de requête. Plus la taille du plan est importante, plus le nombre de ressources permettant de gérer les requêtes sera important. Les limites de débit moyen varient également en fonction de la taille du plan. La mise à niveau de votre plan peut améliorer les performances. Pour connaître les plans et les limites, voir [Plans de tarification {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans). 

### Complexité des requêtes
{: #qp-query}

Il existe plusieurs méthodes permettant d'exécuter des requêtes dans {{site.data.keyword.discoveryshort}} et les différentes opérations utilisées peuvent avoir des conséquences sur les performances. Ces caractéristiques de requête peuvent avoir des conséquences sur les performances :

1.   **£Longueur** - Les requêtes plus longues ont généralement des performances plus faibles. 
1.   **Agrégations** - Les agrégations constituent un type de requête complexe, avec des agrégations imbriquées ayant des conséquences plus élevées sur les performances. 
1.   **Opérateurs** - L'utilisation de caractères génériques et de la correspondance partielle peut avoir des conséquences sur les performances.
1.   **Nombres** - La réduction du nombre de documents renvoyés peut améliorer les performances. Si vous avez besoin de parcourir les résultats, utilisez le paramètre `offset`. 
1.   **Zones renvoyées** - La limitation du nombre de zones renvoyées aux seules zones requises pour votre application peut être bénéfique (par exemple, ne renvoyez pas le texte complet du document si seuls le titre et un passage du texte sont requis).  

Pour plus de détails, voir [Référence de requête](/docs/services/discovery?topic=discovery-query-reference#query-reference).

### Fonctions utilisées
{: #qp-features}

Il existe plusieurs fonctions qui améliorent les résultats des requêtes. Les fonctions suivantes peuvent avoir des conséquences sur les performances :
 
1.   **Extraction de passages** - L'extraction de passages effectue des recherches dans des documents afin de trouver des fragments de texte correspondant à votre requête. Vous pouvez modifier les zones des documents dans lesquels la fonction d'extraction de passages effectue la recherche avec le paramètre `passages.fields`. Si votre contenu comporte un grand nombre de zones, cette opération permet de réduire la durée de l'extraction de passages. Pour plus d'informations sur l'extraction de passages, voir [Passages](/docs/services/discovery?topic=discovery-query-parameters#passages).
1.   **Entraînement visant à améliorer la pertinence** - L'entraînement visant à améliorer la pertinence calcule des fonctions pour chaque zone de texte de niveau supérieur (zones au même niveau que l'élément `document_id` dans JSON) de la collection. Si le nombre de zones de niveau supérieur est trop élevé, cela peut avoir des conséquences sur les performances pour un élément `natural_language_query` lors de l'utilisation de cette fonction. La réduction du nombre de zones de niveau supérieur peut améliorer les performances. Cette action peut être effectuée via la normalisation ou en éditant manuellement l'élément JSON afin de placer dans un élément structuré imbriqué les zones qui ne sont pas utiles à la recherche de contenu approprié. Le fait de changer les zones utilisées pour l'entraînement a également des conséquences sur le modèle. Vous devez prendre en compte à la fois les conséquences sur les performances et la précision des résultats si vous effectuez ce changement. Pour plus d'informations sur l'entraînement visant à améliorer la pertinence, voir [Amélioration de la pertinence des résultats à l'aide des outils](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling). 
1.  **Continuous Relevancy Training** - L'entraînement continu visant à améliorer la pertinence effectue des recherches dans toutes les collections d'un environnement. Plus le nombre de collections d'un environnement est élevé, plus les conséquences sur les performances sont importantes. Pour plus d'informations, voir [Continuous Relevancy Training](/docs/services/discovery?topic=discovery-crt#crt).

### Taille de collection et complexité
{: #qp-collection} 

Les documents composant une collection privée peuvent avoir des conséquences sur les performances des requêtes :
1.  **Nombre total de documents** - Les performances peuvent être réduites lorsque vous vous approchez des limites maximales de `nombre de documents` pour les tailles de plan Advanced. 
1.  **Taille des documents** - Pour les documents de très grande taille (plusieurs Mo), il est nécessaire de déplacer une grande quantité de données par demande, ce qui peut avoir des conséquences négatives sur les performances, principalement lors de l'utilisation des fonctions d'extraction de passages et d'entraînement visant à améliorer la pertinence. 
1.  **Nombre d'enrichissements** - Les enrichissements permettent de rendre plus complexes les documents en ajoutant un nombre significatif de zones imbriquées. Si aucun enrichissement n'est nécessaire pour votre cas d'utilisation, pensez à désactiver cette fonction lors de l'ingestion. Les enrichissements ne sont pas directement utilisés pour la pertinence de recherche `natural_language_query`. Pour plus d'informations sur les enrichissements, voir [Ajout d'enrichissements](/docs/services/discovery?topic=discovery-configservice#adding-enrichments).
