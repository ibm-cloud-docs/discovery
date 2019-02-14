---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-06"

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

# Amélioration de la pertinence des résultats à l'aide des outils

La pertinence des résultats d'une requête en langage naturel peut être améliorée dans le service {{site.data.keyword.discoveryfull}} à l'aide d'une formation. Vous pouvez former vos collections privées à l'aide des outils {{site.data.keyword.discoveryshort}} ou des API {{site.data.keyword.discoveryshort}}. Si vous préférez utiliser les API, voir [Amélioration de la pertinence des résultats de requête à l'aide de l'API](/docs/services/discovery/train.html).
{: shortdesc}

La formation pour la pertinence est facultative ; si les résultats de vos requêtes répondent à vos besoins, aucune autre formation n'est requise. Pour obtenir une présentation de la création de cas d'utilisation relatifs à la formation, voir l'article de blogue [How to get the most out of Relevancy Training ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developer.ibm.com/dwblog/2017/get-relevancy-training/){: new_window}.

Pour former Watson, vous devrez :

  -   fournir des exemples de requête qui sont représentatifs des requêtes saisies par vos utilisateurs, et
  -   fournir des évaluations afin de spécifier quels résultats sont pertinents et non pertinents pour chaque requête.

Une fois que Watson a suffisamment de données de formation, les informations que vous avez fournies sur les résultats qui sont bons ou mauvais pour chaque requête seront utilisées pour découvrir votre collection. Watson ne fait pas seulement que mémoriser, il tire des enseignements des informations spécifiques relatives aux requêtes individuelles et il applique les modèles qu'il a détectés à toutes les nouvelles requêtes. Pour cela, il utilise des techniques Watson d'apprentissage automatique qui trouvent des signaux dans votre contenu et vos questions. Une fois la formation appliquée, {{site.data.keyword.discoveryshort}} réorganise les résultats de requête afin d'afficher en premier ceux qui sont les plus pertinents. Plus vous ajoutez des données de formation, plus {{site.data.keyword.discoveryshort}} devient précis dans l'organisation des résultats de requête.

**Remarque :** la formation pour la pertinence s'applique uniquement aux requêtes en langage naturel portant sur des collections privées. Elle n'est pas destinée à être utilisée avec des requêtes en langage de requête {{site.data.keyword.discoveryshort}} structurées. Pour en savoir plus sur le langage de requête {{site.data.keyword.discoveryshort}}, voir [Concepts de requête](/docs/services/discovery/using.html).

Les collections formées renverront un score `confidence` dans le résultat d'une requête en langage naturel. Pour plus d'informations, voir [Scores de confiance](/docs/services/discovery/train-tooling.html#confidence).

Voir [Exigences relatives aux données de formation](/docs/services/discovery/train.html#reqs) pour connaître les exigences minimales pour l'apprentissage, ainsi que les limites d'apprentissage.

Voir [Surveillance de l'utilisation](/docs/services/discovery/feedback.html) pour plus de détails sur le suivi de l'utilisation et l'utilisation de ces données pour vous aider à maîtriser et à améliorer vos applications.

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

Si vous souhaitez supprimer toutes les données de formation de votre collection à la fois, vous devez utiliser l'API. Pour plus d'informations, voir [Supprimer toutes les données de formation d'une collection](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-all-training-data). Pour plus d'informations sur la formation via l'API, voir [Amélioration de la pertinence des résultats de requête à l'aide de l'API](/docs/services/discovery/train.html).

## Test de et itération sur la pertinence des résultats

Une fois l'évaluation des résultats terminée et la formation appliquée par Watson, il est recommandé d'effectuer des tests pour voir si les résultats de requête se sont améliorés. Pour cela, exécutez des requêtes de test qui sont liées (mais pas identiques) à vos requêtes de formation. Vérifiez si les résultats de vos requêtes de test se sont améliorés.

Si vous souhaitez améliorer davantage les résultats après les tests, vous pouvez :
- ajouter d'autres documents à votre collection ;
- ajouter d'autres requêtes de formation ;
- évaluer d'autres résultats, en prenant soin d'utiliser les évaluations `Relevant` et `Not relevant`.

Pour plus de conseils sur la formation, voir [Astuces pour la formation de pertinence](/docs/services/discovery/train-tips.html#relevancy-tips).

## Scores de confiance
{: #confidence}

Les collections formées renverront un score `confidence` dans le résultat d'une requête en langage naturel. Le score `confidence` est calculé en fonction du niveau de confiance estimé du résultat, comparé au modèle formé. Le score `confidence` n'est **pas** identique à la valeur `score`. Pour savoir comment déterminer des seuils pour les scores de confiance, voir l'article [How to select a threshold for acting using confidence scores ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developer.ibm.com/watson/blog/2016/06/23/how-to-select-a-threshold-for-acting-using-confidence-scores/). Le `score` ne doit pas être utilisé pour définir des seuils absolus car il s'agit d'un calcul relatif.

Le score `confidence` est compris entre 0.0 et 1.0. Plus le chiffre est élevé, plus le document est pertinent.

Le score `confidence` figure dans les résultats de requête, sous la section `result_metadata` de chaque document. Par exemple :

```json
    "results": [
        {
            "id": "eea16dfd5fe6139a25324e7481a32f89_13",
            "result_metadata": {
                "confidence": 0.5893963975910735,
                "score": 0.5006834
            },
```

**Remarque :** La zone `confidence` est renvoyée uniquement quand la formation de pertinence a abouti. Il peut également y a voir des cas où le modèle formé n'est pas disponible et la zone `confidence` ne sera pas renvoyée.  

Par exemple, le modèle entraîné sera temporairement non valide si de nouvelles zones de niveau supérieur sont introduites, ou si le schéma de la collection a été modifié car de nouveaux documents avec un schéma différent ont été ingérés. Dans ce scénario, `confidence` ne sera pas renvoyé avec les résultats, et les résultats proviendront de la recherche non formée par défaut tant que le modèle n'aura pas été automatiquement entraîné et ne sera pas à nouveau disponible. Durant le nouvel entraînement, `confidence` ne sera pas renvoyé. 

Les applications utilisant `confidence` comme seuil doivent s'assurer qu'elles peuvent gérer ces scénarios. Comme `score` est relatif à la requête, il n'est pas recommandé de l'utiliser en tant que seuil fixe. En revanche, nous conseillons que les applications aient toujours le même comportement pour tous les résultats n'incluant pas la même zone `confidence`. Par exemple, une application peut afficher tous les résultats sans la zone `confidence` ou masquer tous les résultats sans la zone `confidence`, mais elle ne doit pas utiliser la valeur de `score` pour en afficher certains et en masquer d'autres.
