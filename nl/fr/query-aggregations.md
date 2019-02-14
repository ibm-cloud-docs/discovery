---

copyright:
  years: 2015, 2018
lastupdated: "2018-05-09"

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

# Agrégations de requête
{: #query-aggregations}

Les agrégations renvoient un ensemble de valeurs de données. Pour obtenir la liste complète des agrégations disponibles, voir la rubrique [Référence de requête](/docs/services/discovery/query-reference.html#aggregations).

## term
{: #term}

Renvoie les premières valeurs (par score et par fréquence) pour les enrichissements sélectionnés. Tous les enrichissements sont des valeurs valides. Vous pouvez éventuellement utiliser `count` pour spécifier le nombre de termes à renvoyer. Le paramètre `count` possède la valeur par défaut de 10. Cet exemple renvoie le texte intégral et les enrichissements des premières valeurs avec l'enrichissement de concept, et spécifie que 10 termes doivent être renvoyés.

Par
exemple :
```bash
term(enriched_text.concepts.text,count:10)
```
{: codeblock}

## filter
{: #filter}

Modificateur qui permet d'affiner le groupe de documents de la requête d'agrégation qu'il précède. Cet exemple permet de filtrer le groupe de documents incluant le concept Cloud Computing.

Par
exemple :
```bash
filter(enriched_text.concepts.text:"cloud computing")
```
{: codeblock}

## nested
{: #nested}

Le fait d'appliquer nested avant une requête d'agrégation permet de limiter l'agrégation à la zone des résultats spécifiés. Par exemple : `nested(enriched_text.entities)` signifie que seuls les composants `enriched_text.entities` de n'importe quel résultat sont utilisés pour l'agrégation.

Par
exemple :
```bash
nested(enriched_text.entities)
```
{: codeblock}

## histogram
{: #histogram}

Permet de créer des segments d'intervalle numériques pour classer des documents. Utilisez les valeurs de zone d'une zone numérique unique pour décrire la catégorie. La zone utilisée pour créer l'histogramme doit être de type numérique (`integer`, `float`, `double` ou `date`). Les types non numériques, tels que `string`, ne sont pas pris en charge. Par exemple, "price": 1.30 est une valeur numérique qui fonctionne, et "price": "1.30" est une chaîne, non valide. Utilisez l'argument `interval` pour définir la taille des sections de résultats fractionnées. Les valeurs d'intervalle doivent être des nombres entiers non négatifs et sont définies de manière à rendre logique la segmentation de vos valeurs de zone possibles. Par exemple, si votre jeu de données inclut le prix de plusieurs articles : “price”: 1.30, “price”: 1.99 et “price”: 2.99, vous pouvez utiliser des intervalles de 1 de sorte que tout soit regroupé entre 1 et 2 et entre 2 et 3. N'utilisez pas un intervalle de 100, car toutes les données finiraient dans le même segment. Les histogrammes peuvent traiter des valeurs décimales, mais les intervalles doivent être des nombres entiers. La syntaxe est `histogram(<field>,<interval>)`, comme illustré dans l'exemple suivant :

Par
exemple :
```bash
histogram(product.price,interval:1)
```
{: codeblock}

## timeslice
{: #timeslice}

Histogramme spécialisé qui utilise des dates pour créer des segments d'intervalle. Les valeurs d'intervalle de date valides sont `second/seconds` `minute/minutes`, `hour/hours`, `day/days`, `week/weeks`, `month/months` et `year/years`. La syntaxe est `timeslice(<field>,<interval>,<time_zone>)`. L'utilisation de `timeslice` n'est possible que si les zones d'heure dans vos documents correspondent au type de données `date` et sont au format d'[heure UNIX ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://en.wikipedia.org/wiki/Unix_time){: new_window}. Ces deux conditions doivent être réunies pour que le paramètre `timeslice` fonctionne correctement. Vous pouvez créer un intervalle de temps si vos documents comprennent des zones `date` contenant des valeurs, telles que `1496228512`. La valeur doit être au format numérique (par exemple, `float` ou `double`) et ne doit pas être placée entre apostrophes. Le service traite les dates figurant dans un texte et les dates indiquées au format ISO 8601 comme des données de type `string` et non comme des données de type `date`. Vous pouvez détecter des anomalies dans les agrégations timeslice. Pour plus d'informations, voir [Détection d'anomalies Timeslice](#anomaly-detection). Cet exemple renvoie des valeurs pour "sales" ("product.sales") tous les 2 jours dans le fuseau horaire de la ville de New York.

Par
exemple :
```bash
timeslice(product.sales,2day,America/New York)
```
{: codeblock}

### Détection d'anomalies Timeslice
{: #anomaly-detection}

Vous pouvez éventuellement appliquer une détection d'anomalies aux résultats d'une agrégation `timeslice`. La détection d'anomalies est utilisée pour localiser des points de données inhabituels dans une série temporelle et pour les baliser afin qu'ils soient examinés de manière plus approfondie. Les exemples d'utilisation de la détection d'anomalies concernent l'identification de pics d'utilisation de cartes de crédit et la recherche de groupes d'articles relatifs à un sujet donné dans Watson Discovery News.

Pour appliquer la détection d'anomalies, utilisez la syntaxe suivante dans votre agrégation :

```bash
timeslice(field:<date>,interval:<interval>,anomaly:true)`
```
{: codeblock}

Si vous spécifiez `anomaly:true` avec l'agrégation `timeslice`, les résultats incluent les deux zones supplémentaires suivantes, illustrées dans l'exemple ci-dessous :

  - `"anomaly": true` pour indiquer que le détection d'anomalies a été effectuée.
  - Une zone `anomaly` dans les points considérés comme des anomalies dans le tableau de résultats de la sortie. La zone anomaly comporte une valeur de données du type`float` indiquant l'ampleur du comportement anormal. Plus la valeur de la zone anomaly est proche de `1`, plus il est probable que le résultat sera anormal.

  - Les zones `key` et `key_as_string` dans chacun des objets du tableau `results` constituent une valeur d'horodatage UNIX, exprimée en secondes.
  - Le score d'anomalie est relatif à une requête et non à plusieurs requêtes.

```json
"type": "timeslice",
"field": "blekko.chrondate",
"interval": "1d",
"anomaly": true,
"results": [
  {
    "matching_results": 2933,
    "anomaly": 1,
    "key_as_string": "1496880000",
    "key": 1496880000000
  },
  {
    "matching_results": 3435,
    "anomaly": 1,
    "key_as_string": "1496966400",
    "key": 1496966400000
  },
  {
    "matching_results": 3692,
    "anomaly": 0.598226,
    "key_as_string": "1496016000",
    "key": 1496016000000
  },
  {
    "matching_results": 4551,
    "anomaly": 0.828498,
    "key_as_string": "1495411200",
    "key": 1495411200000
  },
  {
    "matching_results": 947,
    "key_as_string": "1489968000",
    "key": 1489968000000
  },
 ...
]
...
```
{: codeblock}

#### Limitations de la détection d'anomalies

- Pour l'instant, la détection d'anomalies est disponible uniquement sur les agrégations `timeslice` de niveau supérieur. Elle n'est pas disponible dans les agrégations de niveau inférieur (imbriquées).
- Le nombre maximal de points pouvant être traités par la détection d'anomalies dans n'importe quelle agrégation `timeslice` donnée est `1500`.
- Le nombre maximal d'agrégations timeslice de niveau supérieur pouvant être traitées par la détection d'anomalies est `20`.

<!--
#### Anomaly detection workflow

The following example workflow detects an anomaly for the text entity `London` and retrieves additional information about the anomalous datapoint.

  1. Timeslice aggregation: `query=entities.text:London&count=0&aggregation=timeslice(blekko.last_crawled,1day,anomaly:true)`
  1. Term aggregation to retrieve top keywords: `query=entities.text:London&count=0&aggregation=term(keywords.text,count:5)&filter=blekko.last_crawled>=1490140800,<=1490227200`
  1. Query to retrieve top enriched title: `query=entities.text:London,keywords.text:Westminster Bridge|police officer|people|Prime Minister Theresa|parliament&count=1&filter=blekko.last_crawled>=1490140800,<=1490227200&return=enrichedTitle.text`
  -->

## top_hits
{: #top_hits}

Renvoie les documents classés en fonction du score de la requête ou de l'enrichissement. Peut être utilisé avec n'importe quel paramètre de requête ou agrégation. Cet exemple renvoie les 10 premiers accès pour une agrégation term.

Par
exemple :
```bash
term(enriched_text.concepts.text).top_hits(10)
```
{: codeblock}

## unique_count
{: #unique_count}

Renvoie un comptage des instances uniques de la zone spécifiée dans la collection.

Exemples :
```bash
unique_count(enriched_text.keyword.text)
```
{: codeblock}

```bash
nested(enriched_text.entities).term(enriched_text.entities.text,count:3).unique_count(enriched_text.entities.type)
```
{: codeblock}

## max
{: #max}

Renvoie la valeur maximale de la zone spécifiée dans tous les documents correspondants.

Par
exemple :
```bash
max(product.price)
```
{: codeblock}

## min
{: #min}

Renvoie la valeur minimale de la zone spécifiée dans tous les documents correspondants.

Par
exemple :
```bash
min(product.price)
```
{: codeblock}

## average
{: #average}

Renvoie la moyenne des valeurs de la zone spécifiée dans tous les documents correspondants.

Par
exemple :
```bash
average(product.price)
```
{: codeblock}

## sum
{: #sum}

Additionne les valeurs de la zone spécifiée dans tous les documents correspondants.

Par
exemple :
```bash
sum(product.price)
```
{: codeblock}
