---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-08"

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


# Tutoriel : Migration à partir du service Retrieve and Rank

Migration à partir du service {{site.data.keyword.retrieveandrankshort}} vers le service {{site.data.keyword.discoveryfull}}. Il s'agit d'une suite du tutoriel d'initiation à Cranfield. 

## Présentation générale
{: #overview}
Ce tutoriel vous guide lors du processus de création et de formation d'un service {{site.data.keyword.discoveryfull}} avec des exemples de données. Ce tutoriel utilise le même jeu de données que celui ayant servi dans le [Tutoriel d'initiation à {{site.data.keyword.retrieveandrankshort}}](/docs/services/retrieve-and-rank/getting-started.html), mais vous pouvez utiliser la même approche pour créer une instance de service qui utilise vos propres données. 

Le processus de migration de données à partir du service {{site.data.keyword.retrieveandrankshort}} vers {{site.data.keyword.discoveryshort}} comprend deux étapes principales. 

1. Faire migrer les données de collection
2. Faire migrer les données de formation

Lorsque vous faites migrer vos données de collection formées, le **plus** important est de _conserver les mêmes ID de document _. En effet, vos données de formation utilisent ces ID pour faire référence aux données de référence, par conséquent, si les ID sont modifiés lors de la migration du service {{site.data.keyword.retrieveandrankshort}} vers le service {{site.data.keyword.discoveryshort}}, le nouveau classement sera complètement désactivé (ou il se peut même que la formation ne démarre pas). {{site.data.keyword.discoveryshort}} vous permet de spécifier l'ID de document dans le processus de téléchargement d'API et d'éviter ce problème en suivant les instructions du présent document. Les données de formation {{site.data.keyword.retrieveandrankshort}} sont généralement stockées dans un fichier `csv`. Dans ce tutoriel, ce fichier `csv` est utilisé pour télécharger les exemples de données de formation dans {{site.data.keyword.discoveryshort}}. Le processus de migration des données de formation exportées à partir des outils {{site.data.keyword.retrieveandrankshort}} est décrit en détail dans la rubrique [Migration des données de formation à partir du service](/docs/services/discovery/migrate-dcs-rr.html#extract-train).

Ce tutoriel part du principe que la configuration du service {{site.data.keyword.retrieveandrankshort}} est similaire à celle utilisée dans le [Tutoriel d'initiation à {{site.data.keyword.retrieveandrankshort}}](/docs/services/retrieve-and-rank/getting-started.html) et il utilise la procédure de migration à partir du chemin source décrite [ici](/docs/services/discovery/migrate-dcs-rr.html#source). Pour connaître les autres options de migration, voir la rubrique [Evaluation de votre chemin de migration vers le service Watson Discovery](/docs/services/discovery/migrate-dcs-rr.html#evaluate). 

Pour suivre le tutoriel, vous avez besoin des éléments suivants :

-  **cURL.** Vous pouvez installer la version de cURL correspondant à votre système d'exploitation à partir du site [haxx.se ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://curl.haxx.se/){: new_window}. Vous devez installer la version qui prend en charge le protocole Secure Sockets Layer (SSL). Prenez soin d'inclure le fichier binaire installé sur votre variable d'environnement PATH. 
-  Exemples de données Cranfield. Ce tutoriel utilise les exemples de données de collection provenant du tutoriel Initiation à {{site.data.keyword.retrieveandrankshort}}. [Données JSON Cranfield ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-data.json){: new_window}
-  **Exemples de données de référence**. Ce tutoriel utilise les exemples de données de référence Cranfield provenant du tutoriel Initiation à {{site.data.keyword.retrieveandrankshort}}. [Fichier CSV de données de référence Cranfield![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-gt.csv){: new_window}
-  **Python version 2.** Pour vérifier si Python est installé, entrez `python --version` dans une invite de commande et vérifiez que le numéro de version commence par 2. Si vous devez installer Python, voir le document [Downloading Python ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://wiki.python.org/moin/BeginnersGuide/Download){: new_window}.
-  Script de téléchargement de données : [Programme de téléchargement de document Discovery ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-upload.py){: new_window}
-  Script de téléchargement de données de formation :  [Programme de téléchargement des données de formation Discovery ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-train.py){: new_window}

Avant de commencer ce tutoriel, vous devez avoir réuni les conditions préalables suivantes :

-  Ce tutoriel part du principe que vous avez déjà créé une instance {{site.data.keyword.discoveryshort}} ; si vous avez besoin d'instructions pour créer une instance {{site.data.keyword.discoveryshort}}, reportez-vous au [tutoriel suivant](/docs/services/discovery/getting-started.html).

-  Ce tutoriel part du principe que vous disposez de vos données d'identification de service. 
   -  Lorsque vous êtes dans le service Watson {{site.data.keyword.discoveryshort}} sur {{site.data.keyword.Bluemix_notm}}, cliquez sur **Service credentials**.
   -  Cliquez sur **View credentials** sous Actions.
   -  Copiez les valeurs `username` et `password` et assurez-vous que la valeur `url` correspond à celle qui figure dans les exemples ci-après. Si tel n'est pas le cas, remplacez-la également. 

## Ajout de données Cranfield à Discovery

1.  Créez un environnement. 

    ```bash
    curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{ "name": "my_environment", "description": "My environment" }' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    Copiez la valeur `environment-id` figurant dans le document JSON renvoyé. 

1. Créez une collection. 

    ```bash
    curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{ "name": "test_collection", "description": "My test collection", "configuration_id": "{configuration_id}", "language_code": "en" }' "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07"
    ```
    {: pre}

    Copiez la valeur `collection-id` figurant dans le document JSON renvoyé. 

1.  Ajoutez les documents sur lesquels porteront les recherches. 
    1.  Téléchargez le fichier [cranfield-data.json ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-data.json){: new_window}, le cas échéant. Il s'agit de la source des documents utilisés dans {{site.data.keyword.retrieveandrankshort}}. Les documents de la collection Cranfield sont au format JSON, accepté par {{site.data.keyword.retrieveandrankshort}} et de surcroît parfaitement compatible avec Watson {{site.data.keyword.discoveryshort}}.
        **Remarque :** {{site.data.keyword.discoveryshort}} ne requiert pas de télécharger le schéma Solr. Cela est dû au fait que {{site.data.keyword.discoveryshort}} déduit automatiquement le schéma à partir de la structure JSON. 
    1.  Téléchargez le script de téléchargement de données[ici![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-upload.py){: new_window}. Ce script téléchargera le document JSON Cranfield dans {{site.data.keyword.discoveryshort}}.
        Le script parcourt le fichier JSON et envoie chaque document JSON individuel au service {{site.data.keyword.discoveryshort}} à l'aide d'une configuration par défaut définie dans in {{site.data.keyword.discoveryshort}}.
        **Remarque :** la configuration par défaut définie dans {{site.data.keyword.discoveryshort}} fournit des paramètres similaires à ceux de la configuration Solr par défaut définie dans {{site.data.keyword.retrieveandrankshort}}.
    1.  Exécutez la commande suivante pour télécharger les données `cranfield-data-json` dans la collection `cranfield_collection`. Remplacez `{username}`, `{password}`, `{path_to_file}`, `{environment_id}`, `{collection_id}` par vos informations. Notez  qu'il existe des options supplémentaires, -d pour le débogage et –v pour la sortie prolixe générée par curl.

        ```bash
        python ./disco-upload.py -u {username}:{password} -i {path_to_file}/cranfield-data.json –e {environment_id} -c {collection_id}
        ```
        {: pre}

1.  Une fois le processus de téléchargement terminé, vous pouvez vérifier que les documents sont bien là en exécutant la commande suivante pour afficher les détails de la collection : 

    ```bash
    curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07"
    ```
    {: pre}

    La sortie se présente approximativement comme suit :

    ```json
    {
      "collection_id": "f1360220-ea2d-4271-9d62-89a910b13c37",
      "name": "democollection",
      "description": "this is a demo collection",
      "created": "2015-08-24T18:42:25.324Z",
      "updated": "2015-08-24T18:42:25.324Z",
      "status": "available",
      "configuration_id": "6963be41-2dea-4f79-8f52-127c63c479b0",
      "language": "en",
      "document_counts": {
        "available": 1000,
        "processing": 20,
        "failed": 180
      },
      "disk_usage": {
        "used_bytes": 260
      },
      "training": {
        "total_examples": 0,
        "available": false,
        "processing": false,
        "minimum_queries_added": false,
        "minimum_examples_added": true,
        "sufficient_label_diversity": false,
        "notices": 0,
        "successfully_trained": null,
        "data_updated": null
      }
    }
    ```
    {: codeblock}

Reportez-vous à la section `document_counts` pour voir combien de documents ont été téléchargés. Aucune erreur de document ne devrait se produire avec cet exemple de jeu de données. En revanche, avec d'autres jeux de données, vous verrez peut-être des nombres de documents en échec. Si cela se produit, vous pouvez exécuter l'API notices pour voir les messages d'erreur. Reportez-vous à la section [ici ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-notices){: new_window} pour visualiser la commande API notices. 

La section `training` renvoyée fournit des informations sur votre formation. Nous examinerons cette section une fois que vos données de formation auront été téléchargées. 

## Ajout de données de formation à Discovery

Le service Watson {{site.data.keyword.discoveryshort}} utilise un modèle d'apprentissage automatique pour relancer le classement de documents. Pour ce faire, vous devez former un modèle. La formation a lieu une fois que vous avez téléchargé suffisamment de requêtes avec les documents classés appropriés. En chargeant suffisamment d'exemples présentant suffisamment de variance dans Watson {{site.data.keyword.discoveryshort}}, vous apprenez à ce dernier à reconnaître un "bon" document. Dans cette étape, vous vous servirez des "données de référence" Cranfield qui sont utilisées dans {{site.data.keyword.retrieveandrankshort}} pour former Watson {{site.data.keyword.discoveryshort}}.

1.  Téléchargez l'exemple de [fichier CSV de données de référence Cranfield ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-gt.csv){: new_window} à partir du tutoriel {{site.data.keyword.retrieveandrankshort}}, le cas échéant. 

   Le fichier regroupe les questions qu'un utilisateur peut se poser au sujet des documents. Il fournit des exemples d'informations permettant de former le dispositif de classement dans {{site.data.keyword.retrieveandrankshort}} et une formation pour la pertinence dans {{site.data.keyword.discoveryshort}} pour les questions et les réponses pertinentes. 

   Pour chaque question, il existe au moins un identificateur pour une réponse (ID de document). Chaque ID de document inclut un nombre indiquant le niveau de pertinence de la réponse par rapport à la question. L'ID de document pointe vers la réponse dans le fichier `cranfield-data.json` que vous avez téléchargé dans {{site.data.keyword.discoveryshort}} à l'étape précédente. 

1.  Téléchargez le script de téléchargement des données de formation. Vous utiliserez ce script pour télécharger les données de formation dans {{site.data.keyword.discoveryshort}}. Le script transforme le fichier `csv` en un ensemble de requêtes JSON et d'exemples et il les envoie au service {{site.data.keyword.discoveryshort}} à l'aide des [API de données de formation ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#training-data){: new_window}
    **Remarque :** {{site.data.keyword.discoveryshort}} gère les données de formation dans le service, par conséquent, lorsque de nouveaux exemples et de nouvelles requêtes de formation sont générés, elles peuvent être stockées dans le service {{site.data.keyword.discoveryshort}} proprement dit et non dans un fichier CSV distinct qui doit être géré. 
1.  Exécutez le script de téléchargement des données de formation pour télécharger les données de formation dans {{site.data.keyword.discoveryshort}}. Remplacez `{username}`, `{password}`, `{path_to_file}`, `{environment_id}`, `{collection_id}` par vos informations. Notez  qu'il existe des options supplémentaires, `-d` pour le débogage et `–v` pour la sortie prolixe générée par curl.

    ```bash
    python ./disco-train.py -u {username}:{password} -i {path_to_file}/cranfield-gt.csv –e {environment_id} -c {collection_id}
    ```
    {: pre}

1.  Une fois les données chargées, vous pouvez vérifier le statut de la formation à l'aide de la commande d'affichage des détails de collection que nous avons décrite dans la section précédente. {{site.data.keyword.discoveryshort}} effectue une vérification toutes les heures pour voir si de nouvelles données sont arrivées. Si tel est le cas, il commence à les traiter et à les transformer en un modèle d'apprentissage automatique. Lorsqu'un modèle est en cours de formation, l'état de la section de formation passe de `"processing": false` à `"processing": true`. Une fois la formation du modèle terminé, l'état de la section de formation passe de `"available": false` à `"available": true`. La date de la valeur `"successfully_trained"` est également modifiée. Si des erreurs se sont produites, vous pouvez les afficher à l'aide de l'**API notices** comme indiqué dans la section précédente. 

## Recherche de documents
{: search}

Le service {{site.data.keyword.discoveryshort}} utilise automatiquement un modèle formé pour classer à nouveau les éventuels résultats de recherche. Lorsqu'un [appel d'API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection){: new_window} est émis à l'aide d'une requête `natural_language_query` au lieu d'une requête `query`, le système vérifie si un modèle est disponible. Si tel est le cas, le service {{site.data.keyword.discoveryshort}} utilise ce modèle pour classer à nouveau les résultats. Dans un premier temps, nous effectuerons une recherche dans des documents non classés, puis nous effectuerons une recherche à l'aide du modèle de classement. 

1.  Vous pouvez rechercher des documents dans votre collection à l'aide d'une commande cURL. Effectuez une requête à l'aide de l'appel d'API query pour voir les résultats non classés. Remplacez `{username}`, `{password}`, `{environment_id}`, `{collection_id}` par vos propres valeurs. Les résultats renvoyés seront des résultats non classées qui utiliseront les formules de classement {{site.data.keyword.discoveryshort}} par défaut. Vous pouvez essayer d'autres requêtes en ouvrant le fichier `csv` contenant les données de formation et en copiant la valeur de la première colonne dans le paramètre de requête. 

    ```bash
    curl -u "{username}":"{password}""https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&query=what is the basic mechanism of the transonic aileron buzz"
    ```
    {: pre}

1.  A présent, effectuez une recherche à l'aide du modèle en définissant le paramètre `natural_language_query`. Auparavant, prenez soin de vérifier que vous disposez d'un modèle formé comme indiqué dans la section précédente. Collez le code suivant dans votre console, en remplaçant `{username}`, `{password}`, `{environment_id}`, `{collection_id}` par vos valeurs. 

    ```bash
    curl -u "{username}":"{password}""https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&natural_language_query=what is the basic mechanism of the transonic aileron buzz"
    ```
    {: pre}

    Cette commande renverra les résultats non classés à l'aide du modèle que vous avez formé précédemment. Comparez les résultats de cette recherche avec les résultats de certaines des autres recherches que vous avez effectuées précédemment. Vous constaterez peut-être des différences de résultats par rapport à ce qui est affiché dans {{site.data.keyword.retrieveandrankshort}}. Cela est dû au fait que certaines des techniques utilisées pour la recherche ont été modifiées afin de simplifier l'expérience et d'améliorer les résultats, mais dans l'ensemble, la qualité des résultats est similaire. 

Après avoir évalué les résultats de recherche ayant fait l'objet d'un nouveau classement, vous pouvez les affiner dans {{site.data.keyword.discoveryshort}} en répétant l'étape de téléchargement des données de formation avec des exemples et des requêtes de formation supplémentaires et en visualisant les résultats de recherche. Vous pouvez également ajouter de nouveaux documents, comme indiqué dans la première étape, pour élargir la portée de la recherche. Comme pour le service {{site.data.keyword.retrieveandrankshort}}, l'amélioration des résultats par formation est un processus itératif. 
