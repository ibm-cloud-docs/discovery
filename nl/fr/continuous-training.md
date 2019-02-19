---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-25"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Continuous Relevancy Training
{: #crt}

{{site.data.keyword.discoveryshort}} Continuous Relevancy Training est capable d'apprendre automatiquement à parti de comportement utilisateur, réduisant de manière significative l'effort requis pour améliorer le classement selon la pertinence des résultats. Il utilise des interactions d'utilisateurs pour apprendre comment faire apparaître les résultats les plus pertinents. Il est capable d'apprendre d'interactions telles que des clics pour déterminer quels résultats ont le plus de valeurs pour les utilisateurs et découvrir les signaux les plus importants pour les analyses futures. Continuous Relevancy Training reclasse des documents afin de faire figurer en tête les informations les plus pertinentes. Il sert pour : 

- Aider à améliorer la pertinence des résultats pour les agents de support, en fonction des résultats sur lesquels ils cliquent
- Afficher des résultats plus pertinents dans un agent conversationnel client en fonction des résultats à long terme sélectionnés 
- Fournir des experts avec des réponses plus pertinentes, basées sur les résultats qu'ils explorent

Pour configurer Continuous Relevancy Training :

- Continuous Relevancy Training peut uniquement être activé au niveau environnement. Les requêtes doivent utiliser les noeuds finaux `/api/v1/environment/{environment_id}/query` ou `/api/v1/environments/{environment_id}/query` pour interroger une ou plusieurs collections.
- Les événements {{site.data.keyword.discoveryshort}} `events` (clics) étant utilisés pour créer les données d'apprentissage requises, commencez par intégrer le suivi d'événements. Voir [Usage monitoring](/docs/services/discovery/feedback.html#usage) pour plus de détails.
- Au moins 1 000 requêtes en langage naturel avec clic de souris associé sont requises pour que Continuous Relevancy Training démarre. Les événements et journaux sont conservés pendant 30 jours sur votre instance ; c'est pourquoi les 1 000 clics doivent être collectés sur cette période.
- Continuous Relevancy Training est disponibles pour les plans Advanced de taille `Small` ou supérieure, ainsi que pour les plans Premium. Il n'est pas disponible pour les plans `Lite`. 
- Le nombre de collections pour Continuous Relevancy Training est limité à `5`. Continuous Relevancy Training fonctionnant sur plusieurs collections, les temps d'analyse et d'apprentissage peuvent être étendus.
- Continuous Relevancy Training est appliqué uniquement aux zones de niveau supérieur et il existe des limites liées au nombre de zones pouvant être utilisées dans le processus d'apprentissage. Lorsque le nombre de zones de niveau supérieur dépasse `10`, la fréquence des erreurs d'apprentissage est plus élevée. 

Pour utiliser Continuous Relevancy Training :

Une fois l'apprentissage terminé, Continuous Relevancy Training est utilisé pour influencer les résultats d'une requête `natural_language_query` lors de l'utilisation d'une requête de niveau environnement. 

Continuous Relevancy Training peut être utilisé lors de l'analyse en exécutant une requête `natural_language_query` multi-collection sur l'ensemble des collections de votre environnement. Voir [Exécution d'une requête sur plusieurs collections](/docs/services/discovery/using.html#multiple-collections) pour des instructions. 

**Remarque :** Continuous Relevancy Training n'affecte pas les requêtes effectuées sur un appel de requête à un niveau de collection formé ou non (`/v1/environments/{environment_id}/collections/{collection_id}/query`).  

Statut du suivi :

Le statut de Continuous Relevancy Training peut être consulté depuis le noeud final `/api/v1/environments`. Voir [API reference ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#environments-api){: new_window}. Le `status` fournit des informations sur l'état des opérations d'apprentissage et vous indique si Continuous Relevancy Training est actif :

```
"search_status" : [
        {
            "scope" : "environment",
            "status" : "NO_DATA",
            "status_description" : "Discovery is employing a default strategy for document search natural_language_query. Enable query and event logging so we can initiate relevancy training to improve search accuracy.”
        }
    ]
```
