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

# Astuces relatives à la formation à la pertinence
{: #relevancy-tips}

 Réponses aux questions fréquentes concernant la formation d'une collection et explications des messages d'erreur et d'avertissement couramment reçus. Pour plus d'informations sur l'amélioration de la pertinence des requêtes en langage naturel, voir [Amélioration de la pertinence des résultats à l'aide des outils](/docs/services/discovery/train-tooling.html) et [Amélioration de la pertinence des résultats à l'aide de l'API](/docs/services/discovery/train.html).
{: shortdesc}

## Compréhension de la formation

Réponses aux questions fréquentes concernant la formation d'une collection.

### Comment puis-je savoir si mon système a été formé ?

Utilisez la commande d'API qui permet d'[afficher les détails d'une collection ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/watson/developercloud/discovery/api/v1/?curl#list-collection-details){: new_window} pour vérifier que votre système a été formé.  

```bash
curl -u "apikey":"{apikey_value}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07"
```
{: pre}

Exemple de réponse :

```json
{
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

Pour que les exigences en matière de formation soient satisfaites, les éléments suivants doivent tous avoir pour valeur `true` :
- `minimum_queries_added`
- `minimum_examples_added`
- `sufficient_label_diversity`   

Dans la réponse :
- `successfully_trained` est la date à laquelle la formation a abouti pour la dernière fois.
- `available: true` indique que la formation a eu lieu et qu'un modèle est disponible.
- `processing: true` indique que la formation est en cours.
-  Si la date `data_updated` est ultérieure à la date `successfully_trained`, cela signifie qu'un nouveau modèle n'a pas été formé depuis un téléchargement de données récent.  

### Comment puis-je vérifier les erreurs et les avertissements ?

Vous pouvez utiliser l'[API notices![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-notices){: new_window} pour visualiser les erreurs ou les avertissements.  

```bash
curl -u "apikey":"{apikey_value}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/notices?version=2017-11-07"
```
{: pre}

D'autres opérations d'API sont indiquées dans la rubrique [Exécution d'autres opérations de requête de données de formation](/docs/services/discovery/train.html#training-data-operations).

### Comment puis-je interpréter le score `confidence` qui s'affiche dans les résultats de la requête en langage naturel après la formation ?

Les collections formées renverront un score `confidence` dans le résultat d'une requête en langage naturel. Le score `confidence` est calculé en fonction du niveau de confiance du résultat, comparé au modèle formé. Le score `confidence` n'est **pas** identique à la valeur `score`. Pour plus d'informations, voir [Scores de confiance](/docs/services/discovery/train-tooling.html#confidence).  

## Interprétation des erreurs et des avertissements

Explications des messages d'erreur et d'avertissement couramment reçus.

### Avertissement : `Invalid training data found: The document was not returned in the top 100 search results for the given query, and will not be used for training`

Ce message d'avertissement est généré parce que l'élément `document_ids` dans vos données de formation ne correspond pas à l'élément `document_ids` dans une recherche effectuée sur la collection. Vérifiez vos requêtes et assurez-vous que la valeur `document_id` du document que vous évaluez fait partie des 100 premiers résultats renvoyés pour cette requête. Si tel n'est pas le cas, il est recommandé de vérifier les deux points suivants :  

- Si le document ne figure pas parmi les 100 premiers résultats renvoyés, il ne s'agit peut-être pas d'un bon exemple de résultat de qualité et vous souhaiterez peut-être reconsidérer le choix de ce document.  

- Si le document n'est pas renvoyé du tout, il est recommandé de chercher pourquoi ce document n'est pas renvoyé et de vérifier s'il ne comporte pas un texte correspondant à des parties de la requête.  

**Remarque :** ce message d'avertissement signale l'existence probable d'une ou de plusieurs requêtes incorrectes, mais ne signifie pas pour autant que la formation n'aura pas lieu.  

### Erreur : `Invalid training data found: Syntax error when parsing query`

- Il existe un problème au niveau de la syntaxe de requête réelle. Assurez-vous que les requêtes renvoient des résultats et ne génèrent aucune erreur de syntaxe. Cette erreur ne peut être provoquée que si vous avez ajouté un filtre à votre requête en langage naturel.

### Erreur : `Invalid training data found: The query string provided exceeds the maximum length, please provide a shorter one`

- La longueur maximale de la chaîne de requête est de `2048`. Vous devez raccourcir la requête spécifique. Vous pouvez ajouter un filtre dans votre requête pour contourner ce problème.  

### Erreur : `This collection cannot be trained: your plan does not support training on this many top-level text fields.`

- Cette erreur ne se produit qu'avec les plans `Lite`. Les zones de niveau supérieur sont des zones qui ne sont pas imbriquées sous une autre zone. La formation n'a lieu que sur des zones de niveau supérieur et le nombre de zones pouvant être utilisées dans le processus de formation est limité. Plus une collection comporte de zones de niveau supérieur, plus les données d'apprentissage sont nécessaires. Aussi, au-delà de `10` zones de niveau supérieur, la fréquence des erreurs d'apprentissage est plus élevée. 

### Erreur : `Training data quality standards not met: You will need additional training queries with labeled examples. (To be considered for training, each example must appear in the top 100 search results for its query.)`

- Cela signifie que vous devez ajouter davantage de données de formation pour que la formation aboutisse. Vous avez besoin d'au moins 49 requêtes de formation uniques et au moins un document évalué doit être associé à chacune d'elles. Minimum ne signifie pas optimal ; la taille de collection et d'autres facteurs peuvent augmenter le nombre d'exemples de formation nécessaires pour satisfaire aux conditions minimales.  

### Erreur : `Training data quality standards not met: Insufficient number of unique training queries. Expected at least n, but found m.`

- Afin que les conditions minimales requises pour la formation soient satisfaites, vous avez besoin d'au moins 49 requêtes de formation uniques et au moins un document évalué doit être associé à chacune d'elles. Si cette erreur persiste alors que vos conditions dépassent le minimum requis, recherchez la présence d'autres erreurs dans vos avis.  

### Erreur : `Training data quality standards not met: No documents found with non-zero relevance labels.`

- Les données de formation ont besoin d'avoir suffisamment de données de libellé qui spécifient quels sont les documents de grande valeur. Cela signifie que vous devez évaluer certains documents avec des valeurs autres que zéro. Si vous utilisez les outils Discovery, vous devez évaluer certains documents comme étant pertinents (`10`) ; si vous utilisez l'API, vous devez libeller certains documents avec le score `1` ou plus.   

### Erreur : `Training data quality standards not met: Training examples have no relevance label variety for X queries.`

- L'une des exigences relatives à la formation est d'avoir suffisamment de diversité au niveau des libellés. Cela signifie que si vous souhaitez obtenir un système bien formé, vous devez ajouter non seulement les documents qui obtiennent les meilleures scores de pertinence, mais également les documents qui obtiennent de bons scores de pertinence. En d'autres termes, sur une échelle de 0 à 4, il est utile d'avoir des documents dont le score est 2 et des documents dont le score est 3, en plus des documents dont le score est 4. (Si vous utilisez les outils Discovery, les documents sont évalués comme étant pertinents (`10`) ou non pertinents (`0`).) Au moins 25 % des questions doivent présenter une diversité au niveau des libellés.   
