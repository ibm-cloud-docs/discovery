---

copyright:
  years: 2015, 2017
lastupdated: "2017-12-15"

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

# Concepts de requête

Le service {{site.data.keyword.discoveryfull}} offre des fonctions de recherche de contenu puissantes. Une fois votre contenu téléchargé et enrichi par le service {{site.data.keyword.discoveryshort}}, vous pouvez créer des requêtes, intégrer {{site.data.keyword.discoveryshort}} dans vos propres projets ou créer une application personnalisée en utilisant {{site.data.keyword.watson}} Explorer Application Builder. 
{: shortdesc}

  Les requêtes que vous écrivez varient d'une collection à une autre, car toutes les collections comportent un contenu unique.
  {: tip}

Lorsque vous créez une requête ou un filtre, {{site.data.keyword.discoveryshort}} examine chaque résultat et tente de mettre en correspondance les chemins que vous avez définis. Lorsque des correspondances sont trouvées, elles sont ajoutées à l'ensemble de résultats. Lorsque vous créez une requête, vous pouvez être aussi vague ou spécifique que vous le souhaitez. Plus la requête est spécifique, plus les résultats seront ciblés. 

Vous avez également la possibilité d'activer l'extraction de passage. Les passages sont des extraits pertinents et courts issus des documents entiers renvoyés par votre requête. Ces passages ciblés sont extraits des zones `text` contenues dans les documents de votre collection. Par défaut, jusqu'à 10 passages contenant environ 400 caractères chacun seront renvoyés pour une requête. Un maximum de trois passages sont extraits à partir d'un résultat. Le paramètre `passages` n'est disponible que pour les collections privées ; il n'est pas disponible dans la collection {{site.data.keyword.discoverynewsshort}}. Pour plus d'informations sur la manière dont les passages sont identifiés, voir [Passages](/docs/services/discovery/query-parameters.html#passages). 

  Vous pouvez écrire des requêtes en langage naturel (par exemple, "IBM Watson partnerships") à l'aide des outils ou de l'API {{site.data.keyword.discoveryshort}}. {: tip}

Les collections formées renverront un score `confidence` dans le résultat d'une requête en langage naturel. Pour plus d'informations, voir [Scores de confiance](/docs/services/discovery/train-tooling.html#confidence). 

{{site.data.keyword.discoveryfull}} Visual Insights est une fonction expérimentale que vous pouvez utiliser pour explorer visuellement les connexions identifiées au travers de la compréhension d'éléments sémantiques, de relations, de concepts, etc. par {{site.data.keyword.discoveryshort}}. Pour plus d'informations, voir [{{site.data.keyword.discoveryfull}} Visual Insights](/docs/services/discovery/visual-insights.html).

{{site.data.keyword.discoveryfull}} Knowledge Graph est une fonction bêta qui fournit des noeuds finaux permettant d'exécuter des requêtes sur des entités et des relations figurant dans des documents. Cela inclut des recherches contextuelles et un classement par pertinence. Pour plus d'informations, voir [{{site.data.keyword.discoveryfull}} Knowledge Graph](/docs/services/discovery/building-kg.html). 

Pour plus d'informations sur l'écriture de requêtes, voir :
- [Initiation à l'écriture de requêtes](/docs/services/discovery/getting-started-query.html)
- [Référence de requête](/docs/services/discovery/query-reference.html) (comprend la liste des paramètres, opérateurs et agrégations disponibles dans le langage de requête {{site.data.keyword.discoveryshort}})

## Schéma de données Discovery
{: #discovery-schema}

Commençons par découvrir l'objet JSON {{site.data.keyword.discoveryshort}}. Pour comprendre comment créer une requête à l'aide du langage de requête {{site.data.keyword.discoveryshort}}, il est utile de connaître l'objet JSON produit par {{site.data.keyword.discoveryshort}} après que celui-ci a enrichi les documents de votre collection. Une fois que vous aurez découvert le schéma de données de vos documents, il vous sera plus facile d'écrire des requêtes dans le langage de requête {{site.data.keyword.discoveryshort}}. Trois méthodes sont possibles. 

  1. Dans les outils {{site.data.keyword.discoveryshort}}, ouvrez l'écran **Manage data**, choisissez la collection {{site.data.keyword.IBM_notm}} Press Releases.  Cliquez sur le bouton **View Data Schema**. L'écran **View data schema** affiche de deux manières différentes les zones et les valeurs contenues dans vos documents transformés : par document (**vue de document**) ou par zone (**vue de collection**). La **vue de document** peut afficher jusqu'à 50 documents. La **vue de collection** affiche toutes les zones de la collection. 

    Dans la **vue de collection**, sous `enriched_text`, se trouvent les enrichissements que vous avez appliqués au fichier **Default Configuration**. Cliquez sur `categories`, `concepts`, `entities` et `sentiment` pour voir de quelle façon votre collection a été enrichie avec des connaissances Watson. 

  1. Exécutez une requête "empty" pour visualiser l'objet JSON. Sur l'écran **View data schema**, cliquez sur le bouton **Build queries**,puis cliquez sur **Run Query**. Les résultats s'affichent sur la droite, sous deux onglets, **Summary** (présentation générale des résultats de la requête) et **JSON**. Ouvrez d'abord l'onglet **JSON**. 

     -  Chacun des quatre documents sera précédé d'un numéro (`id`). 
     -  Faites défiler l'écran jusqu'à la zone `enriched_text`. Examinez chaque enrichissement pour savoir quelles sont les zones JSON sur lesquelles vous pouvez exécuter une requête. 

        ![Zones de configuration par défaut](images/JSON.png)

     -  **entities** - Commencez par rechercher la zone `text`, puis examinez les autres informations d'enrichissement. 
     -  **sentiment** - Commencez par rechercher la zone `label`, puis examinez les autres informations d'enrichissement. 
     -  **concepts** - Commencez par rechercher la zone `text`, puis examinez les autres informations d'enrichissement. 
     -  **categories** - Commencez par rechercher la zone `document`, puis examinez les autres informations d'enrichissement. 

     Après avoir consulté les indications contenues dans le premier document, vous pouvez examiner les autres trois documents si vous le souhaitez.

  1. Consultez les zones disponibles dans le **générateur de requête visuelle**. Sur l'écran **Build queries**, cliquez sur **Search for documents**, puis sur **Use the {{site.data.keyword.discoveryshort}} Query Language**. Cliquez sur la liste déroulante **Field** pour voir les zones disponibles dans vos données. Cliquez sur **Edit in query language** pour créer des requêtes manuellement à l'aide du langage de requête {{site.data.keyword.discoveryshort}}.       

### Comment structurer une requête de base
{: #structure-basic-query}

Comme vous l'avez remarqué, l'objet JSON est de nature hiérarchique, par conséquent, les requêtes doivent être écrites en utilisant la même hiérarchie. Si votre objet JSON se présente comme suit :

```json
"enriched_text": {
  "concepts": [
    {
    "text": "Cloud computing",
    "relevance": 0.610029}
    ]
  }
```
{: codeblock}

Votre requête doit être structurée comme suit :

![Exemple de structure de requête](images/query_structure2.png)


Remarques :

- Vous ne savez pas quand exécuter une requête sur une entité, un concept ou un mot clé ? Voir [Compréhension de la différence entre Entities, Concepts et Keywords](/docs/services/discovery/building.html#udbeck).

- **Remarque :** après avoir cliqué sur **Run query** et ouvert l'onglet **JSON**, vous constaterez que la mise en évidence des requêtes est activée par défaut. Cela ajoutera une zone `highlight` à vos résultats de requête. Dans la zone `highlight`, les mots qui correspondent à votre requête seront encapsulés dans les balises HTML `<em>` (mise en évidence). Pour plus d'informations, voir[Paramètres de requête](/docs/services/discovery/query-parameters.html#highlight). 

## Création de requêtes combinées
{: #building-combined-queries}

Vous pouvez combiner des paramètres de requête afin de créer des requêtes davantage ciblées. Par exemple, vous pouvez utiliser en même temps les paramètres `filter` et `query`. Pour en savoir plus sur ce qui différencie le filtrage de la création de requêtes, voir [Différences entre les paramètres de requête et de filtre](/docs/services/discovery/query-parameters.html#filtervquery).

## Comment structurer une agrégation
{: #structure-aggregation}

Les agrégations renvoient un groupe de valeurs de données. Par exemple, des mots clés principaux, des sentiments d'entités globaux, etc. Pour obtenir la liste complète des options d'agrégation, voir [Agrégations](/docs/services/discovery/query-reference.html#aggregations).

![Exemple de structure de requête d'agrégation](images/aggregation_structure.png)

Cet exemple d'agrégation trouvera tous les `concepts` dans votre collection. Le délimiteur dans cette requête est `.` et l'opérateur est  `()`. Pour découvrir les autres opérateurs disponibles dans le langage de requête {{site.data.keyword.discoveryshort}}, voir [Opérateurs de requête](/docs/services/discovery/query-operators.html). 

### Exemple de requêtes d'agrégation
{: #example-aggregations}

Il existe plusieurs façons d'agréger des résultats avec {{site.data.keyword.discoverynewsshort}}, y compris les valeurs supérieures, les sommes, le minimum, le maximum, la moyenne, l'intervalle de temps et l'histogramme. Vous pouvez également ajouter des filtres et imbriquer des agrégations. 

#### Agrégations filtrées
{: #filter-aggregations}

Cet exemple d'agrégation renvoie le nombre d'articles trouvés dans {{site.data.keyword.discoverynewsshort}} au sujet des Steelers de Pittsburgh et indique combien d'entre eux contiennent un sentiment positif (`positive`), négatif (`negative`) ou neutre (`neutral`). 

- `filter(enriched_text.entities.text:"Pittsburgh Steelers").term(enriched_text.sentiment.document.label,count:3)`


Cet exemple d'agrégation commence par limiter (filtrer) le groupe d'articles dans {{site.data.keyword.discoverynewsshort}} à ceux qui incluent le texte d'entité de Twitter, puis il divise ces articles en fonction des types de sentiment de document. Seuls les trois premiers types de sentiment de document (`positive`, `negative`, `neutral`) sont renvoyés. 

- `filter(enriched_text.entities.text:twitter).term(enriched_text.sentiment.document.label,count:3)`

#### Agrégations imbriquées
{: #nested-aggregations}

Le fait d'ajouter `nested` avant une agrégation permet de limiter l'agrégation à la zone des résultats spécifiés. Par exemple : `nested(enriched_text.entities)` signifie que seuls les composants `enriched_text.entities` de n'importe quel résultat sont utilisés pour l'agrégation.  

Cela peut être facilement vérifiable en examinant les différences entre les deux requêtes :
- `filter(enriched_text.entities.disambiguation.subtype::City)` - L'agrégation compte le nombre de *résultats* contenant un ou plusieurs éléments `entity` avec le type `City`. 
- `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City)` - L'agrégation compte le nombre d'instance d'un élément `entity` avec le type `City` dans les résultats.    

De plus, n'importe quelle opération suivante aura pour conséquence de restreindre davantage l'ensemble de résultats sur lequel effectuer l'agrégation. Par exemple :

- `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City)` signifie que seules les entités `subtype::City` seront agrégées. 
- `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City).term(enriched_text.entities.text,count:3)` agrégera les 3 premières entités du sous-type `City`. 
- `filter(enriched_text.entities.disambiguation.subtype::City).term(enriched_text.entities.text,count:3)` renverra les 3 premières entités dont le résultat contient au moins une entité du sous-type `City`.

## Exécution de requêtes sur Watson Discovery News
{: #querying-news}

{{site.data.keyword.discoverynewsshort}}, fichier public qui a été pré-enrichi avec des renseignements cognitifs, est également inclus avec {{site.data.keyword.discoveryshort}}. Pour plus d'informations sur cette collection, voir [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html#watson-discovery-news). 

Vous pouvez exécuter une requête sur cette collection en utilisant des requêtes en langage naturel, par exemple, "IBM Watson partnerships", ou le langage de requête {{site.data.keyword.discoveryshort}}. Pour en savoir plus sur les requêtes en langage naturel, voir la rubrique [Requête en langage naturel](/docs/services/discovery/query-parameters.html#nlq).

Vous ne pouvez pas ajuster la configuration de {{site.data.keyword.discoverynewsshort}}, former ou ajouter des documents à la collection {{site.data.keyword.discoverynewsshort}}. Regardez une démonstration illustrant ce que vous pouvez créer avec {{site.data.keyword.discoverynewsshort}} [en cliquant ici ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://discovery-news-demo.mybluemix.net/){: new_window}.

La version anglaise de Watson {{site.data.keyword.discoverynewsshort}} est disponible via les outils et l'API {{site.data.keyword.discoveryshort}}. La version coréenne (`collection_id` : `news-ko`) et la version espagnole (`collection_id` : `news-es`) sont disponibles uniquement via l'API. Pour plus d'informations sur l'exécution d'une requête sur une collection via l'API, voir le document [API Reference ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection){: new_window}. La référence `collection_id` de la version anglaise de Watson {{site.data.keyword.discoverynewsshort}} est `news-en`. Anciennement, la référence `collection_id` était `news`. Si vous utilisiez l'ancienne référence `collection_id`, elle continuera de fonctionner, cela dit, vous souhaiterez peut-être utiliser la nouvelle référence `collection_id` pour vos nouveaux projets. 

**Remarque :** le nombre maximal de résultats pouvant être renvoyés pour une requête Watson Discovery News est `50`. Utilisez d'autres requêtes ainsi  que le paramètre `offset` pour renvoyer plus de `50` résultats. 

Si vous utilisez le langage de requête {{site.data.keyword.discoveryshort}}, vous pouvez inclure une plage de dates relative dans vos requêtes {{site.data.keyword.discoverynewsshort}}, par exemple, `crawl_date>=now-1month`. Les valeurs de plage de dates valides sont les suivantes :`second/seconds` `minute/minutes`, `hour/hours`, `day/days`, `week/weeks`, `month/months` et `year/years`. `now` n'est pas concerné par le paramètre `time_zone` ; le fuseau horaire `UTC` est défini par défaut. 

Les articles de journal peuvent être syndiqués vers plusieurs organes de presse. {{site.data.keyword.discoverynewsfull}} sélectionnera chacun d'eux, générant ainsi des articles en double. Cela signifie qu'une requête sur {{site.data.keyword.discoverynewsfull}} peut potentiellement renvoyer plusieurs articles identiques ou quasiment identiques dans les résultats de requête. Vous pouvez gérer cette situation à l'aide du dédoublonnage. Pour en savoir plus sur cette fonction bêta, voir [Exclusion des documents en double dans les résultats de requête](/docs/services/discovery/query-parameters.html#deduplication).

## Exécution d'une requête sur plusieurs collections
{: #multiple-collections}

Si vous disposez de plusieurs collections dans votre environnement, vous pouvez être amené à afficher des résultats sur ces collections. Les méthodes de requête (`query`, `fields` et `notices`) au niveau `environments` vous permettent d'exécuter des requêtes sur plusieurs collections spécifiées. Pour l'instant, la fonction permettant d'exécuter des requêtes sur plusieurs collections n'est pas disponible dans les outils {{site.data.keyword.discoveryshort}}. 

Vous pouvez exécuter des requêtes sur plusieurs collections dans le même environnement à l'aide de la méthode d'API `environments/{environment_id}/query`. Lorsque vous exécutez des requêtes sur plusieurs collections, tenez compte des points suivants : 
-  Le paramètre `collection_ids` doit être spécifié lorsque cette méthode est utilisée. `collection_ids` est une liste des collections de l'environnement qui fera l'objet d'une requête, séparées par des virgules. 
-  Le paramètre `passages` et tous ses sous-paramètres ne sont pas pris en charge lors de l'exécution de requêtes sur plusieurs collections. 
-  Une nouvelle zone, `collection_id`, est renvoyée avec chaque objet de résultat. Cette zone indique la collection dans laquelle le résultat a été trouvé.
-  {{site.data.keyword.discoverynewsshort}} fait partie de l'environnement `system` et ne peut pas être inclus dans plusieurs requêtes de collection. 
-  Aucune partie d'une requête portant sur plusieurs collections ne fait l'objet d'un nouveau classement, même si toutes les collections de la requête ont été formées. 

Pour plus d'informations, voir la section [Multiple collection querying dans le document API Reference ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-multi-collections){: new_window}. 

Vous pouvez afficher des avis dans plusieurs collections au sein d'un même environnement à l'aide de la méthode d'API `environments/{environment_id}/notices`. 
-  Le paramètre `collection_ids` doit être spécifié lorsque cette méthode est utilisée. `collection_ids` est une liste des collections de l'environnement qui fera l'objet d'une requête, séparées par des virgules. 
-  Le paramètre `passages` et tous ses sous-paramètres ne sont pas pris en charge lors de l'exécution de requêtes sur plusieurs collections. 

Pour plus d'informations, voir la section [Notices across multiple collections dans le document API Reference ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#collections-notices){: new_window}. 

Vous pouvez afficher les zones disponibles sur les collections d'un environnement à l'aide de la méthode d'API `environments/{environment_id}/fields`. Pour plus d'informations, voir la section [List fields across collections dans le document API Reference ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#multi-list-fields){: new_window}. 
