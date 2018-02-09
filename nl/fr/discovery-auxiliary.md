---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-31"

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

# Archives Discovery

Cette rubrique contient des informations relatives aux fonctions {{site.data.keyword.discoveryshort}} qui sont peut-être encore disponibles, mais qui ont été remplacées par de nouvelles options.
{: tip}

## Enrichissements AlchemyLanguage
{: #AlchemyLanguage-enrichments}

Le **18 juillet 2017**, {{site.data.keyword.discoveryfull}} a introduit une nouvelle technologie d'enrichissement, nommée {{site.data.keyword.nlushort}}. Ces enrichissements sont les mêmes que vos enrichissements existants mais ils nécessitent une configuration et un schéma légèrement différents. Les enrichissements d'origine, nommés enrichissements {{site.data.keyword.alchemylanguageshort}}, seront dépréciés et à compter du **15 janvier 2018**, ils ne seront plus pris en charge. 

La chaîne de version d'API `2017-10-16` rend obsolète la prise en charge du téléchargement de nouveaux documents dans des collections existantes enrichies avec {{site.data.keyword.alchemylanguageshort}}, ainsi que la création de collections et leur enrichissement avec {{site.data.keyword.alchemylanguageshort}}. Utilisez une chaîne de version d'API antérieure pour continuer d'utiliser {{site.data.keyword.alchemylanguageshort}} jusqu'à la fin de la prise en charge prévue le **15 janvier 2018**.

Les collections existantes enrichies avec AlchemyLanguage doivent être migrées vers les enrichissements Natural Language Understanding dès que possible. Pour plus d'informations sur la migration des collections et des fichiers de configuration qui utilisent les enrichissements {{site.data.keyword.alchemylanguageshort}}, voir [Migration des enrichissements vers {{site.data.keyword.nlushort}}](/docs/services/discovery/migrate-nlu.html).

**Remarque :** les outils {{site.data.keyword.discoveryshort}} utilisent toujours la chaîne de version d'API la plus récente, par conséquent, avec la chaîne de version d'API `2017-10-16`, vous ne pourrez plus télécharger des documents dans des collections {{site.data.keyword.alchemylanguageshort}} existantes ni créer de nouvelles collections enrichies avec {{site.data.keyword.alchemylanguageshort}} à l'aide des outils {{site.data.keyword.discoveryshort}}. Si vous souhaitez continuer à utiliser les outils Discovery pour enrichir des collections, commencez par faire migrer ces dernières vers Natural Language Understanding. Pour plus d'informations, voir [Migration des enrichissements vers {{site.data.keyword.nlushort}}](/docs/services/discovery/migrate-nlu.html). 

### Entity Extraction (AlchemyLanguage)
{: #entity-extraction-al}

Renvoie des éléments, tels que des personnes, des espaces et des organisations qui sont présents dans le texte d'entrée. La fonction Entity Extraction ajoute des connaissances sémantiques au contenu pour mieux comprendre le sujet et le contexte du texte en cours d'analyse. Les techniques Entity Extraction sont basées sur des algorithmes statistiques sophistiqués et sur une technologie de traitement automatique du langage naturel. Elles sont uniques dans le secteur d'activité car elles prennent en charge l'analyse multilingue, l'éclaircissement contextuel et l'extraction des guillemets. 

Exemple de partie d'un document enrichie à l'aide d'Entity Extraction :

```json
{
      "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
      "enriched-text": {
        "status": "OK",
        "language": "english",
        "entities": [
          {
            "type": "City",
            "relevance": 0.532754,
            "sentiment": {
              "type": "positive",
              "score": 0.527541,
              "mixed": false
            },
            "count": 1,
            "text": "Atlanta",
            "disambiguated": {
              "subType": [
                "AdministrativeDivision",
                "GovernmentalJurisdiction",
                "OlympicHostCity",
                "PlaceWithNeighborhoods"
              ],
              "name": "Atlanta",
              "website": "http://www.atlantaga.gov/",
              "dbpedia": "http://dbpedia.org/resource/Atlanta",
              "freebase": "http://rdf.freebase.com/ns/m.013yq"
            }
          }
        ]
      }
    }
```
{: codeblock}
Dans l'exemple précédent, vous pouvez faire une requête portant sur le type d'entité en accédant à `enriched_text.entities.type`

L'élément `sentiment` est calculé pour les types d'entité même si l'enrichissement **sentiment** n'est pas sélectionné. Pour en savoir plus sur l'évaluation de l'élément sentiment, voir [Sentiment Analysis](/docs/services/discovery/discovery-auxiliary.html#sentiment-analysis-al).

L'élément `relevance` est compris entre `0.0` et `1.0`. Plus le score est élevé, plus l'entité est pertinente. La zone `disambiguated` contient les informations d'éclaircissement pour l'entité, ce qui inclut les informations `subType` de l'entité et les liens vers la ou les ressource(s), le cas échéant. L'élément `count` correspond nombre de fois que l'entité est mentionnée dans le document.

### Keyword Extraction (AlchemyLanguage)
{: #keyword-extraction-al}

Rubriques importantes de votre contenu généralement utilisées lors de l'indexation de données, la génération de nuages d'étiquettes ou les recherches. Le service {{site.data.keyword.discoveryshort}} identifie automatiquement les langues prises en charge dans votre contenu d'entrée, puis identifie et classe les mots clés dans ce contenu. 

Exemple de partie d'un document enrichie à l'aide de Keyword Extraction :

```json
{
    "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched-text": {
        "status": "OK",
        "language": "english",
        "keywords": [
          {
            "relevance": 0.66497,
            "sentiment": {
              "score": 0.527541,
              "type": "positive",
              "mixed": false
            },
            "text": "stockholders"
          }
        ]
      }
    }
```
{: codeblock}

Dans l'exemple précédent, vous pouvez faire une requête portant sur le mot clé en accédant à `enriched_text.keywords.text`

L'élément `sentiment` est calculé pour les mots-clés même si l'enrichissement **sentiment** n'est pas sélectionné. Pour en savoir plus sur l'évaluation de l'élément sentiment, voir [Sentiment Analysis](/docs/services/discovery/discovery-auxiliary.html#sentiment-analysis-al).

L'élément `relevance` est compris entre `0.0` et `1.0`. Plus le score est élevé, plus le mot clé est pertinent. 

### Taxonomy Classification (AlchemyLanguage)
{: #taxonomy-classification-al}

Permet de catégoriser un texte d'entrée, un contenu HTML ou un contenu Web dans une taxonomie hiérarchique de cinq niveaux au maximum. Les niveaux les plus profonds vous permettent de classifier le contenu dans des sous-segments plus précis et utiles. 

Exemple de partie d'un document enrichie à l'aide de Taxonomy Classification :

```json
  {
    "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched-text": {
        "status": "OK",
        "language": "english",
        "taxonomy": [
          {
            "label": "/business and industrial/company/merger and acquisition",
            "score": 0.517533,
            "confident": false
          }
        ]
      }
    }
```
{: codeblock}

Dans l'exemple précédent, vous pouvez faire une requête portant sur le libellé de taxonomie en accédant à `enriched_text.taxonomy.label`

L'élément `label` est la catégorie de taxonomie détectée. Les niveaux de structure hiérarchique sont séparés par des barres obliques. L'élément `score` pour cette catégorie est compris entre `0.0` et `1.0`. Plus le score est élevé, plus le niveau de confiance dans cette catégorie est élevé. 

### Concept Tagging (AlchemyLanguage)
{: #concept-tagging-al}

Identifie les concepts auxquels le texte d'entrée est associé, en fonction d'autres concepts et entités présents dans ce texte. La fonction Concept Tagging comprend de quelle façon les concepts sont liés et peut identifier les concepts qui ne sont pas directement référencés dans le texte. Par exemple, si un article mentionne CERN et le boson de Higgs, les fonctions Concepts API identifieront Large Hadron Collider comme un concept même si ce terme n'est pas mentionné explicitement sur la page. La fonction Concept Tagging permet d'effectuer des analyses de contenu d'entrée de niveau supérieure par rapport à celles de l'identification de mot clé de base. 

Exemple de partie d'un document enrichie à l'aide de Concept Tagging :

```json
{
    "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
      "enriched_text": {
        "status": "OK",
        "language": "english",
        "concepts": [
          {
            "text": "Acme Corporation",
            "relevance": 0.91136,
            "dbpedia": "http://dbpedia.org/resource/Acme_Corporation",
            "freebase": "http://rdf.freebase.com/ns/m.0dndy",
            "yago": "http://yago-knowledge.org/resource/Acme_Corporation"
          }
        ]
      }
    }
```
{: codeblock}

Dans l'exemple précédent, vous pouvez faire une requête portant sur le type de texte de concept en accédant à `enriched_text.concepts.text`

L'élément `relevance` est compris entre `0.0` et `1.0`. Plus le score est élevé, plus le concept est pertinent. Des liens vers la ou les ressource(s) sont fournis, le cas échéant. 

### Relation Extraction (AlchemyLanguage)
{: #relation-extraction-al}

Identifie les relations subject, action et object dans les phrases du contenu d'entrée. Les informations de relation peuvent être utilisées pour identifier automatiquement l'achat de signaux, d'événements clés et d'autres actions importantes. 

Exemple de partie d'un document enrichie à l'aide de Relation  Extraction :

```json
{
      "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
      "enriched-text": {
        "status": "OK",
        "language": "english",
        "relations": [
          {
            "sentence": " The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, GA.",
            "subject": {
              "text": "The stockholders",
            "keywords": [
              {
                  "text": "stockholders"
              }
              ]
            },
          "action": {
              "text": "were",
              "lemmatized": "be",
              "verb": {
              "text": "be",
              "tense": "past"
            }
            },
            "object": {
              "text": "pleased that Acme Corporation plans to build a new factory in Atlanta, GA",
              "sentiment": {
                "type": "positive",
                "score": 0.834516,
                "mixed": false
              },
              "entities": [
                {
                  "type": "Company",
                "text": "Acme Corporation"
                },
                {
                  "type": "City",
                  "text": "Atlanta",
                  "disambiguated": {
                    "subType": [
                      "AdministrativeDivision",
                      "GovernmentalJurisdiction",
                      "OlympicHostCity",
                      "PlaceWithNeighborhoods"
                    ],
                    "name": "Atlanta",
                    "website": "http://www.atlantaga.gov/",
                    "dbpedia": "http://dbpedia.org/resource/Atlanta",
                    "freebase": "http://rdf.freebase.com/ns/m.013yq"
                  }
                },
                {
                  "type": "StateOrCounty",
                  "text": "GA"
                }
              ],
              "keywords": [
                {
                  "text": "Acme Corporation"
                },
                {
                  "text": "new factory"
                },
                {
                  "text": "GA"
                },
                {
                "text": "Atlanta"
                }
              ]
            }
          }
        ]
      }
    }
```
{: codeblock}

Dans l'exemple précédent, vous pouvez faire une requête portant sur le texte de sujet de relation en accédant à `enriched_text.relations.subject.text`

L'élément `sentiment` est calculé pour les relations même si l'enrichissement **sentiment** n'est pas sélectionné. Pour en savoir plus sur l'évaluation de l'élément sentiment, voir [Sentiment Analysis](/docs/services/discovery/discovery-auxiliary.html#sentiment-analysis-al). Ni `entities` ni `keywords` ne seront extraits (comme illustré dans l'exemple) sauf si vous sélectionnez également les enrichissements **entity** et **keyword**. Pour plus d'informations sur ces enrichissements, voir [Entity Extraction](/docs/services/discovery/discovery-auxiliary.html#entity-extraction-al) et [Keyword Extraction](/docs/services/discovery/discovery-auxiliary.html#keyword-extraction-al). 

Les éléments `subject`, `action` et `object` sont extraits pour chaque phrase contenant une relation.

### Sentiment Analysis (AlchemyLanguage)
{: #sentiment-analysis-al}

Identifie une attitude, des opinions ou des sentiments dans le contenu en cours d'analyse. Le service {{site.data.keyword.discoveryshort}} peut calculer le sentiment global dans un document, le sentiment pour des cibles spécifiées par l'utilisateur, le sentiment de niveau entité, le sentiment de niveau citation, le sentiment directionnel et le sentiment de niveau mot clé. La combinaison de ces aptitudes prend en charge une grande variété de cas d'utilisation qui vont de la surveillance des médias sociaux à l'analyse des tendances. 

Exemple de partie d'un document enrichie à l'aide de Sentiment Analysis :

```json
{
      "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
      "enriched_text": {
        "status": "OK",
        "language": "english",
        "docSentiment": {
          "type": "positive",
          "score": 0.0966252,
          "mixed": true
        }
      }
    }
```
{: codeblock}

Dans l'exemple précédent, vous pouvez faire une requête portant sur le type docSentiment en accédant à `enriched_text.docSentiment.type`

L'élément `type` est le sentiment global du document (`positive`, `negative` ou  `neutral`). Le `type` de sentiment est basé sur l'élément `score`. Le score `0.0` indique que le document est neutre (`neutral`), un nombre positif indique que le document est positif (`positive`), un nombre négatif indique que le document est négatif (`negative`). Si `mixed` a pour valeur `true`, cela signifie que le document contient à la fois des sentiments positifs et des sentiments négatifs (cette zone n'est pas déterminée par le `score`).

### Emotion Analysis (AlchemyLanguage)
{: #emotion-analysis-al}

Détecte la colère, le dégoût, la peur, la joie et la tristesse suggérés dans le texte anglais. Les fonction Emotion Analysis peut détecter des émotions qui sont associées à des phrases, des entités ou des mots clés ciblés ou elle peut analyser la tonalité affective globale de votre contenu. 

Exemple de partie d'un document enrichie à l'aide de Emotion Analysis :

```json
{
      "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
      "enriched_text": {
        "status": "OK",
        "language": "english",
        "docEmotions": {
          "anger": "0.077394",
          "disgust": "0.044024",
          "fear": "0.092664",
          "joy": "0.553327",
          "sadness": "0.3969"
        }
      }
    }
```
{: codeblock}

Dans l'exemple précédent, vous pouvez faire une requête portant sur l'objet docEmotion `joy` en accédant à `enriched_text.docEmotions.joy`

La fonction Emotion Analysis analyse votre texte et calcule un score pour chaque émotion (colère, dégoût, peur, joie, tristesse) sur une échelle de `0.0` à `1.0`. Si le score obtenu pour une émotion est `0.5` ou plus, cette émotion a été détectée (plus le score est supérieur à `0.5`, plus la pertinence est grande). Dans le fragment illustré, l'émotion `joy` est associée à un score supérieur à 0.5, par conséquent, {{site.data.keyword.watson}} a détecté de la joie. 


## Watson Discovery News Original

Une nouvelle version de {{site.data.keyword.discoverynewsfull}} a débuté le **31 juillet 2017**. Le retrait de {{site.data.keyword.discoverynewsfull}} Original est prévu le **15 janvier 2018**. Pour plus d'informations sur cette nouvelle version, voir [Watson Discovery News](watson-discovery-news.html). 

{{site.data.keyword.discoverynewsfull}} Original est un fichier contenant des sources d'information rédigées principalement en anglais qui est continuellement mis à jour et auquel environ 300 000 nouveaux articles et bloques sont ajoutés quotidiennement. Ce fichier indexé est préenrichi avec les enrichissements {{site.data.keyword.alchemylanguageshort}} suivants : **Keyword Extraction**, **Entity Extraction**, **Concept Tagging**, **Relation Extraction**, **Sentiment Analysis** et **Taxonomy Classification**. Les métadonnées suivantes sont également ajoutées : date d'exploration, date de publication, classement d'URL, classement d'hôte et texte d'ancrage. Il est possible de rechercher dans l'historique des articles de nouvelles parus au cours des 60 derniers jours. 

{{site.data.keyword.discoverynewsfull}} Original est enrichi avec des enrichissements {{site.data.keyword.alchemylanguageshort}}. Pour plus d'informations sur ces enrichissements, voir [Enrichissements {{site.data.keyword.alchemylanguageshort}}](discovery-auxiliary.html#AlchemyLanguage-enrichments).

### Exécution de requêtes sur Watson Discovery News Original

Une nouvelle version de {{site.data.keyword.discoverynewsfull}} a débuté le **31 juillet 2017**. Le retrait de {{site.data.keyword.discoverynewsfull}} Original est prévu le **15 janvier 2018**. Pour plus d'informations sur cette nouvelle version, voir [Watson Discovery News](watson-discovery-news.html). 

**Remarque :** le nombre maximal de résultats pouvant être renvoyés pour une requête Watson Discovery News est `50`. Utilisez d'autres requêtes ainsi  que le paramètre `offset` pour renvoyer plus de `50` résultats. 

{{site.data.keyword.discoverynewsfull}} Original utilise un schéma légèrement différent de celui utilisé pour les collections privées. Vous n'avez pas besoin d'inclure `enriched_text` dans vos requêtes. 

**Comment structurer une requête {{site.data.keyword.discoverynewsfull}} Original**

![Exemple de structure de requête Watson Discovery News Original](images/news_query_structure.png)

L'exemple de requête suivant renvoie les 10 premiers articles de {{site.data.keyword.discoverynewsfull}} Original concernant les Stellers de Pittsburgh et comportant un sentiment positif. 

1.  Sur l'écran **Manage data**, choisissez la collection {{site.data.keyword.discoverynewsfull}}. 
1.  Cliquez sur **View data schema**, puis sur **Build queries**.
1.  Sous **Search for documents**, cliquez sur **Use the {{site.data.keyword.discoveryshort}} Query Language**, puis entrez `text:Pittsburgh Steelers, docSentiment.type:positive` dans la zone **Enter query here**. 
1.  Cliquez sur **More options**, puis entrez `10` (valeur par défaut) dans la zone `Number of documents to return`. 
1.  Cliquez sur **Run query**. Les 10 premiers articles concernant les Steelers de Pittsburgh et comportant un sentiment positif s'affichent. 

**Autre exemple de requête {{site.data.keyword.discoverynewsfull}} Original**

-  `concepts.text:"Health care"` - Sous **Search for documents**, cliquez sur **Use the {{site.data.keyword.discoveryshort}} Query Language**, puis entrez cette requête. Tous les articles comportant le concept `health care` sont renvoyés. Si vous spécifiez un comptage, par exemple 50, dans la zone **Number of documents to return**, vous ne recevez que les 50 articles les plus pertinents.

**Comment structurer une requête d'agrégation {{site.data.keyword.discoverynewsfull}} Original**

![Exemple de structure de requête d'agrégation Watson Discovery News Original](images/news_aggregation_structure.png)

L'exemple d'agrégation suivant renvoie le nombre d'articles concernant les Steelers de Pittsburgh trouvés dans {{site.data.keyword.discoverynewsfull}} Original en fonction des sentiments qu'ils contiennent. 

1.  Sur l'écran **Manage data**, choisissez la collection {{site.data.keyword.discoverynewsfull}} Original.
1.  Cliquez sur **View data schema**, puis sur **Build queries**.
1.  Sous **Include analysis of your results**, entrez `filter(text:"Pittsburgh Steelers").term(docSentiment.type,count:3)` dans la zone **Write an aggregation query using the {{site.data.keyword.discoveryshort}} Query Language**. 
1.  Cliquez sur **More options**, puis entrez `0` dans la zone **Number of documents to return**. 
1.  Cliquez sur **Run query**. Les résultats renvoyés spécifient le nombre de documents relatifs aux Steelers de Pittsburgh et indiquent combien d'entre eux contiennent un objet docSentiment positif (`positive`), négatif (`negative`) ou neutre (`neutral`). 

**Autre exemple d'agrégation {{site.data.keyword.discoverynewsfull}} Original**

-  `filter(entities.text:twitter).term(docSentiment.type,count:3)` - Si vous entrez cette requête d'agrégation dans la zone**Write an aggregation query using the {{site.data.keyword.discoveryshort}} Query Language**, elle commence par limiter (filtrer) le groupe d'articles à ceux qui incluent le texte d'entité de Twitter, puis elle divise ces articles en fonction des types de sentiment de document. Seuls les trois premiers types de sentiment de document (`positive`, `negative`, `neutral`) sont renvoyés. 

Le fait d'ajouter `nested` avant une requête d'agrégation permet de limiter l'agrégation à la zone des résultats spécifiés. Par exemple : `nested(text.entities)` signifie que seuls les composants `text.entities` de n'importe quel résultat sont utilisés pour l'agrégation. Cela peut être facilement vérifiable en examinant les différences entre les deux requêtes suivantes : `filter(text.entities.type::City)` : l'agrégation compte le nombre de *résultats* contenant un ou plusieurs éléments `entity` avec le type `City`, et `nested(text.entities).filter(text.entities.type::City)` : l'agrégation compte le nombre d'instance d'un élément `entity` avec le type `City` dans les résultats. De plus, n'importe quelle opération suivante aura pour conséquence de restreindre davantage l'ensemble de résultats sur lequel effectuer l'agrégation. Par exemple `nested(text.entities).filter(text.entities.type::City)` signifie que seules les entités `type::City` seront agrégées. Par exemple : `nested(text.entities).filter(text.entities.type::City).term(text.entities.text,count:3)` agrégera les trois premières entités de type `City` tandis que `filter(text.entities.type::City).term(text.entities.text,count:3)` renverra les trois premières entités là où le résultat contient au moins une entité de type `City`.

**Remarque** : vous ne pouvez pas ajuster la configuration de {{site.data.keyword.discoverynewsfull}} Original, former ou ajouter des documents à cette collection. 

## Intégration à Watson Knowledge Studio à l'aide des enrichissements AlchemyLanguage

Vous pouvez intégrer un modèle personnalisé à partir de {{site.data.keyword.knowledgestudiofull}} au service {{site.data.keyword.discoveryshort}} afin de fournir des enrichissements personnalisés.
{: shortdesc}

### Avant de commencer

Avant de pouvoir intégrer un modèle personnalisé à partir de {{site.data.keyword.knowledgestudioshort}} au service {{site.data.keyword.discoveryshort}}, vous devez créer et déployer le modèle à l'aide de {{site.data.keyword.knowledgestudioshort}}. Pour plus d'informations sur la création et le déploiement de modèles, voir la documentation {{site.data.keyword.knowledgestudioshort}}. Vous avez besoin de l'ID unique du modèle déployé pour l'intégrer au service {{site.data.keyword.discoveryshort}}. 

### A propos de cette tâche

Vous pouvez utiliser un modèle personnalisé développé dans {{site.data.keyword.knowledgestudioshort}} pour enrichir des documents dans le service {{site.data.keyword.discoveryshort}}. Vous avez ainsi la possibilité d'appliquer les fonctions d'amélioration de document du service {{site.data.keyword.discoveryshort}} avec des informations propres à certains domaines, tels qu'un secteur d'activité ou une discipline scientifique. Vous pouvez utiliser à la fois des données publiques et vos propres données exclusives dans votre modèle d'enrichissement. 

Vous devez utiliser l'API de service pour intégrer un modèle {{site.data.keyword.knowledgestudioshort}} au service {{site.data.keyword.discoveryshort}}. Vous ne pouvez pas utiliser les outils {{site.data.keyword.discoveryshort}} pour intégrer un modèle personnalisé.

### Procédure

1.  Procurez-vous l'ID de votre environnement {{site.data.keyword.discoveryshort}} en procédant comme indiqué dans l'article [List environments ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_environments){: new_window}. Notez l'ID de l'environnement. 
1.  Répertoriez les ID de votre configuration ou de vos configurations {{site.data.keyword.discoveryshort}} en cours en procédant comme indiqué dans l'article [List configurations ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_configurations){: new_window} Notez l'ID de la configuration que vous souhaitez intégrer à votre modèle personnalisé {{site.data.keyword.knowledgestudiofull}}. 
1.  Téléchargez une copie de votre configuration {{site.data.keyword.discoveryshort}} en cours en exécutant les commandes suivantes dans un interpréteur de commandes bash ou un environnement équivalent, tel que Cygwin pour Windows. Remplacez `{environment_id}` et `{configuration_id}` par les ID que vous avez notés au cours des deux étapes précédentes. 

    ```bash
    curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-09-01" > my_config.json
    ```
    {: pre}

    Cette commande permet d'afficher le contenu de votre fichier de collection et de placer ce contenu dans un fichier JSON nommé `my_config.json`.
1.  Ouvrez le fichier `my_config.json` dans un éditeur de texte et effectuez les modifications suivantes :
    1.  Remplacez la valeur de la zone `"name"` par un texte décrivant la finalité de la nouvelle configuration. Vous pouvez éventuellement modifier également la valeur de la zone `"description"`. 

        ```json
        ...
        "name": "wks-config",
        "description": "This is a configuration to use with a WKS model",
        ...
        ```
        {: codeblock}

    1.  Mettez à jour les zones d'enrichissement avec des informations relatives au modèle {{site.data.keyword.knowledgestudioshort}}. En supposant que les zones d'enrichissement contenaient à l'origine : 

        ```json
        "enrichments": [
        {
            "destination_field": "enriched_text",
            "source_field": "text",
            "enrichment": "alchemy_language",
            "options": {
              "extract": "keyword, entity, doc-sentiment, taxonomy, concept, relation",
              "sentiment": true,
              "quotations": true
            }
          }
        ]
        ```
        {: codeblock}

    1.  Mettez à jour le fichier comme suit, en remplaçant l'ID unique du modèle {{site.data.keyword.knowledgestudioshort}} décrit dans la section "Avant de commencer" pour  `{watson_knowledge_studio_model_ID}` :

        ```json
        "enrichments": [
        {
            "destination_field": "enriched_text",
            "source_field": "text",
            "enrichment": "alchemy_language",
            "options": {
              "extract": "keyword, entity, doc-sentiment, taxonomy, concept, relation, typed-rels",
              "sentiment": true,
              "quotations": true,
              "model": "{watson_knowledge_studio_model_ID}"
            }
          }
        ]
        ```
        {: codeblock}

1.  Vous pouvez éventuellement activer la normalisation d'entité en procédant comme indiqué dans la rubrique [Création d'une configuration personnalisée pour normaliser des entités](/docs/services/discovery/normalize-entities.html).
1.  Sauvegardez le fichier `my_config.json`.
1.  Utilisez un valideur JSON, tel que [JSLint ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://jslint.com){: new_window} pour valider, et le cas échéant, corriger votre fichier JSON édité avant d'exécuter les étapes suivantes.
1.  Mettez à jour la configuration comme indiqué ci-après. Une fois de plus, vous avez besoin des ID `{environment_id}` et `{configuration_id}` que vous avez collectés au début de cette procédure. 

    ```bash
    curl -X PUT -u "{username}":"{password}" -H "Content-Type: application/json" -d @my_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-09-01"
    ```
    {: pre}

    La commande renvoie le contenu du fichier de configuration mis à jour.
1.  Utilisez le service {{site.data.keyword.discoveryshort}} normalement. Les documents que vous ingérez avec la configuration mise à jour sont automatiquement enrichis avec les données provenant de votre modèle personnalisé. 

## Création d'une configuration personnalisée pour normaliser des entités AlchemyLanguage
{: #normalizing-entities}

Vous pouvez configurer le service {{site.data.keyword.discoveryshort}} afin d'inclure des *entités normalisées*, également appelées *noms canoniques*, dans le résultat de vos requêtes.
{: shortdesc}

**Remarque :** l'édition de la configuration pour activer des entités normalisées est une tâche manuelle qui doit être effectuée à l'aide d'un éditeur de texte et d'appels API. Pour l'instant, elle n'est pas prise en charge par les outils. 

**Remarque :** la normalisation d'entité est disponible uniquement lorsque vous utilisez avec le service Discovery avec un modèle personnalisé généré par Watson Knowledge Studio, comme indiqué dans la rubrique [Intégration à {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery/integrate-wks.html).

La normalisation d'entité insère des noms normalisés (canoniques) pour différentes références à la même personne ou au même objet dans le document source. Par exemple, si vous activez la normalisation d'entité et que vous ingérez un ou plusieurs documents contenant "J.R. Cash" et "John R. Cash", la sortie traitée comportera l'élément `canonical_name` "Johnny Cash" avec chaque terme apparié. Elle contiendra également les noms canoniques pertinents pour d'autres entités de texte trouvées dans le document. Vous trouverez un exemple de sortie à la fin de cette section. 

Après avoir enrichi un document avec des noms canoniques, vous pouvez rechercher plus facilement des éléments spécifiques ayant le même nom canonique. 

Les noms canoniques sont dérivés d'un dictionnaire public. Si un nom canonique approprié est introuvable dans le dictionnaire, le service utilise la référence d'entité qui convient le mieux dans le document comme nom canonique. Avant d'exécuter une requête portant sur un ou plusieurs noms canoniques dans un document dont les entités sont normalisées, examinez le document JSON enrichi afin de vérifier que le ou les noms canoniques générés par le service correspondent aux noms que vous attendez. 

### Procédure

1.  Procurez-vous l'ID de votre environnement {{site.data.keyword.discoveryshort}} en procédant comme indiqué dans l'article [List environments ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_environments){: new_window}. Notez l'ID de l'environnement. 
1.  Répertoriez les ID de votre configuration ou de vos configurations {{site.data.keyword.discoveryshort}} en cours en procédant comme indiqué dans l'article [List configurations ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_configurations){: new_window}. Notez l'ID de la configuration que vous souhaitez mettre à jour. 
1.  Téléchargez une copie de votre configuration {{site.data.keyword.discoveryshort}} en cours en exécutant les commandes suivantes dans un interpréteur de commandes bash ou un environnement équivalent, tel que Cygwin pour Windows. Remplacez `{environment_id}` et `{configuration_id}` par les ID que vous avez notés au cours des deux étapes précédentes. 

    ```bash
    curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-09-01" > new_config.json
    ```
    {: pre}

    Cette commande permet d'afficher le contenu de votre fichier de collection et de placer ce contenu dans un fichier JSON nommé `new_config.json`.


1.  Ouvrez le fichier `new_config.json` dans un éditeur de texte et effectuez les modifications suivantes :
    1. Remplacez la valeur de la zone `"name"` par un texte décrivant la finalité de la nouvelle configuration. Vous pouvez éventuellement modifier également la valeur de la zone `"description"`. 

       ```json
        ...
        "name": "normalize-entities-config",
        "description": "This configuration enables entity normalization",
        ...
       ```
       {: codeblock}

    1. Mettez à jour les zones d'enrichissement avec des informations relatives au modèle {{site.data.keyword.knowledgestudioshort}}. En supposant que les zones d'enrichissement contenaient à l'origine : 

       ```json
       "enrichments": [
        {
           "destination_field": "enriched_text",
           "source_field": "text",
           "enrichment": "alchemy_language",
           "options": {
             "extract": "keyword, entity, doc-sentiment, taxonomy, concept, relation, typed-rels",
             "sentiment": true,
             "quotations": true,
             "model": "{watson_knowledge_studio_model_ID}"
           }
         }
       ]
       ```
       {: codeblock}

    1. Mettez à jour le fichier comme suit :

       ```json
       "enrichments": [
        {
           "destination_field": "enriched_text",
           "source_field": "text",
           "enrichment": "alchemy_language",
           "options": {
             "extract": "keyword, entity, doc-sentiment, taxonomy, concept, relation, typed-rels",
             "sentiment": true,
             "quotations": true,
             "model": "{watson_knowledge_studio_model_ID}"
             "normalizeEntities": 1
           }
         }
       ]
       ```
       {: codeblock}

    1. Sauvegardez le fichier `new_config.json`. 

1.  Utilisez un valideur JSON, tel que [JSLint ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://jslint.com){: new_window}, pour valider votre fichier JSON édité avant d'exécuter les étapes suivantes. 

1.  Mettez à jour la configuration comme indiqué ci-après. Une fois de plus, vous avez besoin des ID `{environment_id}` et `{configuration_id}` que vous avez collectés au début de cette procédure. 

    ```bash
    curl -X PUT -u "{username}":"{password}" -H "Content-Type: application/json" -F configuration-@new_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-09-01"
    ```
    {: pre}

    La commande renvoie le contenu du fichier de configuration mis à jour. 

1.  Utilisez le service {{site.data.keyword.discoveryshort}} normalement. Les documents que vous ingérez avec la configuration mise à jour sont automatiquement enrichis avec des entités normalisées, comme illustré dans les extraits de sortie ci-après. 

### Exemples de sortie

Fragment de sortie **sans** `"normalizeEntities": 1` :

```json
{
  "enriched_text": {
  ...
  ...
  ...
    "entity_relations": {
      "entities": {
        "entity": [
          {
            "class": "SPC",
            "eid": "-E0",
            "generic": false,
            "level": "NAM",
            "mentref": [
              {
                "mid": "-M0",
                "text": "J.R. Cash"
              },
              {
                "mid": "-M6",
                "text": "musician"
              },
              {
                "mid": "-M7",
                "text": "who"
              },
              {
                "mid": "-M13",
                "text": "He"
              },
              {
                "mid": "-M20",
                "text": "He"
              }
            ],
            "score": 0.7874817061794613,
            "subtype": "OTHER",
            "type": "PERSON"
          },
        ...
        ...
        ...
        ]
      },
                    "relations": {
        "relation": [
          {
            "rel_entity_arg": [
              {
                "argnum": 1,
                "eid": "-E0"
              },
              {
                "argnum": 2,
                "eid": "-E1"
              }
            ],
            "relmentions": {
              "relmention": [
                {
                  "class": "SPECIFIC",
                  "modality": "ASSERTED",
                  "rel_mention_arg": [
                    {
                      "argnum": 1,
                      "mid": "-M0",
                      "text": "John R. Cash",
                    },
                    {
                      "argnum": 2,
                      "mid": "-M1",
                      "text": "country"
                    }
                  ],
                  "rmid": "-R1-1",
                  "score": 0.49918343781296,
                  "tense": "UNSPECIFIED"
                }
              ]
            },
            "rid": "-R1",
            "subtype": "OTHER",
            "type": "knownAs"
          },
          ...
          ...
          ...
        ]
      }
    }
  }
}
```
{: codeblock}

Fragment de sortie **avec** `"normalizeEntities": 1` :

```json
{
  "enriched_text": {
  ...
  ...
  ...
    "entity_relations": {
      "entities": {
        "entity": [
          {
            "class": "SPC",
            "eid": "-E0",
            "generic": false,
            "level": "NAM",
            "mentref": [
              {
                "mid": "-M0",
                "text": "J.R. Cash"
              },
              {
                "mid": "-M6",
                "text": "musician"
              },
              {
                "mid": "-M7",
                "text": "who"
              },
              {
                "mid": "-M13",
                "text": "He"
              },
              {
                "mid": "-M20",
                "text": "He"
              }
            ],
            "score": 0.7874817061794613,
            "subtype": "OTHER",
            "type": "PERSON",
            "canonical_name": "Johnny Cash"
          },
        ...
        ...
        ...
        ]
      },
                    "relations": {
        "relation": [
          {
            "rel_entity_arg": [
              {
                "argnum": 1,
                "eid": "-E0"
              },
              {
                "argnum": 2,
                "eid": "-E1"
              }
            ],
            "relmentions": {
              "relmention": [
                {
                  "class": "SPECIFIC",
                  "modality": "ASSERTED",
                  "rel_mention_arg": [
                    {
                      "argnum": 1,
                      "mid": "-M0",
                      "text": "John R. Cash",
                      "canonical_name": "Johnny Cash"
                    },
                    {
                      "argnum": 2,
                      "mid": "-M1",
                      "text": "country",
                      "canonical_name": "country music"
                    }
                  ],
                  "rmid": "-R1-1",
                  "score": 0.49918343781296,
                  "tense": "UNSPECIFIED"
                }
              ]
            },
            "rid": "-R1",
            "subtype": "OTHER",
            "type": "knownAs"
          },
          ...
          ...
          ...
        ]
      }
    }
  }
}
```
{: codeblock}
