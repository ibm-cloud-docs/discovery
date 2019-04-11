---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-11"

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

# Amélioration de la pertinence des résultats à l'aide des outils
{: #improving-result-relevance-with-the-tooling}

La pertinence des résultats d'une requête en langage naturel peut être améliorée dans le service {{site.data.keyword.discoveryfull}} à l'aide d'une formation. Vous pouvez former vos collections privées à l'aide des outils {{site.data.keyword.discoveryshort}} ou des API {{site.data.keyword.discoveryshort}}. Si vous préférez utiliser les API, voir [Amélioration de la pertinence des résultats de requête à l'aide de l'API](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api).
{: shortdesc}

La formation pour la pertinence est facultative ; si les résultats de vos requêtes répondent à vos besoins, aucune autre formation n'est requise. Pour obtenir une présentation de la création de cas d'utilisation relatifs à la formation, voir l'article de blogue [How to get the most out of Relevancy Training ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developer.ibm.com/dwblog/2017/get-relevancy-training/){: new_window}.

Pour former Watson, vous devrez :

  -   fournir des exemples de requête qui sont représentatifs des requêtes saisies par vos utilisateurs, et
  -   fournir des évaluations afin de spécifier quels résultats sont pertinents et non pertinents pour chaque requête.

Une fois que Watson a suffisamment de données de formation, les informations que vous avez fournies sur les résultats qui sont bons ou mauvais pour chaque requête seront utilisées pour découvrir votre collection. Watson ne fait pas seulement que mémoriser, il tire des enseignements des informations spécifiques relatives aux requêtes individuelles et il applique les modèles qu'il a détectés à toutes les nouvelles requêtes. Pour cela, il utilise des techniques Watson d'apprentissage automatique qui trouvent des signaux dans votre contenu et vos questions. Une fois la formation appliquée, {{site.data.keyword.discoveryshort}} réorganise les résultats de requête afin d'afficher en premier ceux qui sont les plus pertinents. Plus vous ajoutez des données de formation, plus {{site.data.keyword.discoveryshort}} devient précis dans l'organisation des résultats de requête.

**Remarque :** la formation pour la pertinence s'applique uniquement aux requêtes en langage naturel portant sur des collections privées. Elle n'est pas destinée à être utilisée avec des requêtes en langage de requête {{site.data.keyword.discoveryshort}} structurées. Pour en savoir plus sur le langage de requête {{site.data.keyword.discoveryshort}}, voir [Concepts de requête](/docs/services/discovery?topic=discovery-query-concepts#query-concepts).

Toutes les collections privées renvoient dans la plupart des cas un score `confidence` dans les résultats de requête. Pour plus d'informations, voir [Scores de confiance](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence).

L'ajout d'une liste de mots à exclure personnalisée peut améliorer la pertinence des résultats pour les requêtes en langage naturel. Pour plus d'informations, voir [Définition des mots à exclure](/docs/services/discovery?topic=discovery-query-concepts#stopwords).

Voir [Exigences relatives aux données de formation](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#reqs) pour connaître les exigences minimales pour l'apprentissage, ainsi que les limites d'apprentissage.

Voir [Surveillance de l'utilisation](/docs/services/discovery?topic=discovery-usage#usage) pour plus de détails sur le suivi de l'utilisation et l'utilisation de ces données pour vous aider à maîtriser et à améliorer vos applications.

## Ajout de requêtes et évaluation de la pertinence des résultats
{: #results}

La formation est constituée des trois parties suivantes : une requête en langage naturel, les résultats de la requête et les évaluations que vous appliquez à ces résultats.

1.  Il existe deux façons d'accéder à la page de formation dans les outils {{site.data.keyword.discoveryshort}} :
    - Pour une collection individuelle, dans l'écran **Build queries**, cliquez sur **Train Watson to improve results** dans la partie supérieure droite. Vous n'avez pas besoin d'entrer une requête sur l'écran **Build queries** pour démarrer la formation. 
    - Depuis le tableau de bord Performance. Cliquez sur l'icône **View data metrics** à gauche pour ouvrir le tableau de bord. Vous êtes invité à choisir une collecte pour la formation ;
1.  Sur l'écran **Train Watson**, cliquez sur **Add a natural language query**, par exemple : "IBM Watson in healthcare" et ajoutez cette requête. Vos requêtes doivent être écrites à la manière dont vos utilisateurs les énonceraient. De plus, les requêtes de formation doivent inclure un chevauchement de termes entre la requête et la réponse souhaitée. Cela permettra d'améliorer les résultats initiaux lors de l'exécution de la requête en langage naturel. La formation pour la pertinence utilise uniquement des requêtes en langage naturel. Par conséquent, vous ne devez pas entrer de requêtes écrites dans le langage de requête {{site.data.keyword.discoveryshort}}.
1.  Pour afficher les résultats de votre requête, cliquez sur le bouton **Rate Results** situé en regard de votre requête. Si vous estimez que les résultats obtenus ne sont pas suffisants, vous pouvez réécrire la requête ou ajouter d'autres documents à cette collection via l'écran **Manage data**.
1.  Commencez par évaluer les résultats comme étant pertinents (`Relevant`) ou non pertinents (`Not relevant`). Lorsque vous avez terminé, cliquez sur **Back to queries**. Dans les outils {{site.data.keyword.discoveryshort}}, le score de l'évaluation `Relevant` est`10` et le score de l'évaluation `Not relevant` est `0`. Si vous avez déjà commencé à évaluer les résultats de cette collection à l'aide de l'API et utilisé une échelle d'évaluation différente, un avertissement s'affiche avec des options permettant de résoudre ce problème.
    En haut de l'écran, Watson indique le statut de la formation et fournit des astuces destinées à vous permettre d'améliorer les résultats. La mention "Add more variety to your ratings" signifie que vous devriez utiliser à la fois l'évaluation `Relevant` et l'évaluation `Not relevant`. Une fois ces exigences satisfaites, la formation sera mise à jour régulièrement. Cette opération durera moins de 30 minutes et vous pourrez continuer à travailler pendant la mise à jour de Watson.
1.  Continuez à ajouter des requêtes et à évaluer des résultats.

Pour revenir à tout moment à l'écran **Build queries** principal, cliquez sur **Build queries** dans l'angle supérieur gauche.
{: tip}
Pour revenir à l'écran **Manage data**, cliquez sur le nom de la collection dans l'angle supérieur droit.
{: tip}

Si vous souhaitez supprimer toutes les données de formation de votre collection à la fois, vous devez utiliser l'API. Pour plus d'informations, voir [Supprimer toutes les données de formation d'une collection](https://{DomainName}/apidocs/discovery#delete-all-training-data). Pour plus d'informations sur la formation via l'API, voir [Amélioration de la pertinence des résultats de requête à l'aide de l'API](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api).

## Test de et itération sur la pertinence des résultats
{: #testing-results}

Une fois l'évaluation des résultats terminée et la formation appliquée par Watson, il est recommandé d'effectuer des tests pour voir si les résultats de requête se sont améliorés. Pour cela, exécutez des requêtes de test qui sont liées (mais pas identiques) à vos requêtes de formation. Vérifiez si les résultats de vos requêtes de test se sont améliorés.

Si vous souhaitez améliorer davantage les résultats après les tests, vous pouvez :
- ajouter d'autres documents à votre collection ;
- ajouter d'autres requêtes de formation ;
- évaluer d'autres résultats, en prenant soin d'utiliser les évaluations `Relevant` et `Not relevant`.

Pour plus de conseils sur la formation, voir [Astuces pour la formation de pertinence](/docs/services/discovery?topic=discovery-relevancy-tips#relevancy-tips).

## Scores de confiance
{: #confidence}

{{site.data.keyword.discoveryshort}} renvoie un score `confidence` à la fois pour les requêtes en langage naturel et celles écrites avec le langage de requête {{site.data.keyword.discoveryshort}}.

Le score `confidence` sera renvoyé à la fois pour les collections privées entraînées et non entraînées (à l'exception des requêtes de filtrage uniquement des collections non entraînées). De plus, {{site.data.keyword.discoveryshort}} renvoie une zone `document_retrieval_strategy` qui indique la source du score `confidence` : 
-  `untrained`
-  `relevancy_training` ou
-  `continuous_relevancy_training`

L'élément `document_retrieval_strategy` peut être utilisé avec le score `confidence` pour déterminer comment les résultats fournis doivent être utilisés. Lorsque la charge est élevée, l'élément `document_retrieval_strategy` renvoyé peut être de type `untrained` même si la collection a été entraînée.

Le score `confidence` est compris entre 0.0 et 1.0. Plus le chiffre est élevé, plus le document est pertinent.

Le score `confidence` figure dans les résultats de requête, sous la section `result_metadata` de chaque document. L'élément `document_retrieval_strategy` est indiqué sous l'élément `retrieval_details`.

```json
{
  "matching_results": 4,
  "session_token": "1_2gYuWJyaWx792Ni4_DQ4C5cbnW",
  "retrieval_details" : {
    "document_retrieval_strategy" : "relevancy_training",
  },
  "results": [
    {
      "id": "eea16dfd5fe6139a25324e7481a32f89_13",
            "result_metadata": {
        "confidence": 0.5893963975910735,
        "score": 0.5006834
      }
    }
  ]
}
```
{: codeblock}

Pour les collections entraînées, le nombre correspondant à `confidence` est calculé en fonction du niveau de confiance estimé du résultat, comparé au modèle entraîné. Les collections entraînées calculent les scores `confidence` uniquement pour les requêtes en langage naturel. Si vous interrogez une collection entraînée en utilisant le langage de requête {{site.data.keyword.discoveryshort}} ou si le modèle entraîné est temporairement indisponible, le nombre `confidence` renvoyé aura la valeur `untrained` pour `document_retrieval_strategy`. Le score `confidence` pour un résultat avec la valeur `untrained` appliquée à `document_retrieval_strategy` est une estimation non supervisée du degré de pertinence entre les résultats de document et la requête. Il n'est pas interchangeable avec le score renvoyé pour les collections entraînées. Une collection entraînée peut fournir de meilleures réponses aux requêtes que les collections non entraînées.

Notez que le score `confidence` n'est **pas** identique à la valeur `score`. Pour savoir comment déterminer des seuils pour les scores de confiance, voir l'article [How to select a threshold for acting using confidence scores ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developer.ibm.com/watson/blog/2016/06/23/how-to-select-a-threshold-for-acting-using-confidence-scores/). Le `score` ne doit pas être utilisé pour définir des seuils absolus car il s'agit d'un calcul relatif. En revanche, nous conseillons que les applications aient toujours le même comportement pour tous les résultats n'incluant pas la même zone `confidence`. Par exemple, une application peut afficher tous les résultats sans la zone `confidence` ou masquer tous les résultats sans la zone `confidence`, mais elle ne doit pas utiliser la valeur de `score` pour en afficher certains et en masquer d'autres. Etant donné que le mode de calcul de `confidence` varie selon les différentes méthodes d'extraction, vous devez prendre en compte `document_retrieval_strategy` lors de la définition d'un seuil et consulter les valeurs avant et après l'entraînement.

Pour plus d'informations sur l'interrogation, voir [Initiation à l'écriture de requêtes](/docs/services/discovery?topic=discovery-getting-started-with-querying#getting-started-with-querying).

Pour plus d'informations sur les méthodes d'entraînement supervisé, voir
-  [Formation de pertinence](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling) et
-  [Continuous Relevancy Training](/docs/services/discovery?topic=discovery-crt#crt)
