---

copyright:
  years: 2019
lastupdated: "2019-03-07"

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

# Haute disponibilité et reprise après incident
{: #recovery}

{{site.data.keyword.discoveryfull}} prend en charge la haute disponibilité sans aucun point de défaillance unique. De plus, le client a la charge de sauvegarder vos données {{site.data.keyword.discoveryshort}} en complément de votre plan de reprise après incident afin que vous puissiez recréer votre service.
{: shortdesc}

L'équilibrage de charge du trafic {{site.data.keyword.discoveryshort}} est effectué dans les différentes zones d'une région. Chaque zone est un centre de données de la même région. Pour plus d'informations, voir [Comment garantir une disponibilité permanente ? ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/docs/overview?topic=overview-zero-downtime#zero-downtime){: new_window}.

## Sauvegarde de vos données dans Watson Discovery
{: #backup}

Plusieurs méthodes permettent de sauvegarder les données stockées dans {{site.data.keyword.discoveryfull}}. Elles doivent être intégrées à votre plan de reprise après incident. 

-  Données pour lesquelles vous devez conserver une copie (documents source, par exemple)
-  Données stockées par {{site.data.keyword.discoveryshort}} que vous devez extraire et sauvegarder
  
Certaines données devront être intégralement recréées (par exemple, les données que vous ne pouvez pas sauvegarder, comme les événements de commentaires en retour) 

### Documents ingérés
{: #backupdocs}

Vos documents téléchargés sont convertis et enrichis, puis stockés dans l'index de recherche. Ce dernier ne peut pas être récupéré après un sinistre et vous devez donc stocker une sauvegarde de tous les documents source à un emplacement sûr.

Si vous importez également des documents en effectuant des explorations planifiées des sources de données externes, vous devez conserver vos données d'identification de source de données en externe afin de pouvoir réétablir vos sources de données rapidement. Pour obtenir la liste des sources disponibles et des données d'identification requises pour chacune d'entre elles, voir [Connexion à des sources de données](/docs/services/discovery?topic=discovery-sources#sources).

### Configurations
{: #backupconfigs}

Vous devez sauvegarder vos configurations d'instance et les stocker localement en cas de sinistre. 

Pour cela, [répertoriez tout d'abord vos configurations](https://cloud.ibm.com/apidocs/discovery#list-configurations) pour chaque instance. 

Une fois que vous avez obtenu la liste des configurations, [procurez-vous les détails](https://cloud.ibm.com/apidocs/discovery#get-configuration-details) de chaque configuration.

### Données d'apprentissage
{: #backuptraining}

Vous devez sauvegarder vos données d'apprentissage pour chaque collection et les stocker localement en cas de sinistre.  

Les données d'apprentissage sont utilisées pour l'apprentissage explicite de vos collections et sont stockées pour chacune d'entre elles. 

Pour extraire les données d'apprentissage, utilisez l'API pour télécharger les requêtes et les évaluations de {{site.data.keyword.discoveryshort}}. 

1.  [Répertoriez les données d'apprentissage](https://cloud.ibm.com/apidocs/discovery#list-training-data)
1.  [Répertoriez les exemples](https://cloud.ibm.com/apidocs/discovery#list-examples-for-a-training-data-query) pour chaque requête.
1.  [Procurez-vous des informations détaillées](https://cloud.ibm.com/apidocs/discovery#get-details-for-training-data-example) sur les exemples de données d'apprentissage. 

Les `ID de document` que vous utilisez dans vos données d'apprentissage désignent les documents de votre collection en cours. Vous DEVEZ utiliser les mêmes `ID de document` dans vos nouvelles collections afin de garantir que les ID corrects sont référencés. Dans le cas contraire, votre entraînement visant à améliorer la pertinence restauré NE FONCTIONNERA PAS.
{: important} 

### Requêtes
{: #backupqueries}

Par défaut (sauf si vous vous désinscrivez), {{site.data.keyword.discoveryshort}} stocke les requêtes que vous lui envoyez. 

Si vous souhaitez pouvoir restaurer ces éléments à des [fins de statistiques](https://cloud.ibm.com/apidocs/discovery#number-of-queries-over-time), vous devez stocker ces requêtes séparément. 

Vous pouvez [extraire des requêtes](https://cloud.ibm.com/apidocs/discovery#search-the-query-and-event-log) de {{site.data.keyword.discoveryshort}}. Toutefois, le nombre de requêtes stockées est limité à 10 000. Il n'existe actuellement aucune API de pagination. La restauration des requêtes n'est pas recommandée. Nous vous conseillons de repartir de zéro 

### Commentaires/clics
{: #clicks}

Si vous stockez des clics sous la forme d'événements de commentaires, il n'existe actuellement aucune méthode permettant de facilement sauvegarder et restaurer ces informations. Nous vous recommandons de repartir de zéro en utilisant l'API [clicks/feedback data](https://cloud.ibm.com/apidocs/discovery#create-event). 

### Listes d'extension
{: #backupexpansions}

Si vous utilisez des extensions pour la modification des requêtes, vous devez sauvegarder votre liste d'extensions et la stocker localement. Pour cela, demandez la liste d'extensions en utilisant la commande d'API [get expansion list](https://cloud.ibm.com/apidocs/discovery#get-the-expansion-list) et stockez-la localement.

### Marquage sémantique des dictionnaires ou des mots à exclure
{: #backupstopwords}

Si vous utilisez ces fonctions, vous devez sauvegarder ces fichiers et les stocker localement. Pour les mots à exclure, sauvegardez le fichier texte. Pour le marquage sémantique, vous devez sauvegarder le fichier JSON. Pour plus d'informations sur chaque type de fichier, voir [Création de dictionnaires de marquage sémantique personnalisés](/docs/services/discovery?topic=discovery-query-concepts#tokenization) et [Définition des mots à exclure](/docs/services/discovery?topic=discovery-query-concepts#stopwords).

### Informations sur la collection
{: #collectioninfo}

Il est recommandé, mais non obligatoire, de régulièrement [extraire le statut](https://cloud.ibm.com/apidocs/discovery#get-collection-details) de chaque collection et de stocker localement les informations. En conservant ces statistiques, vous pouvez ultérieurement vérifier si vos processus de restauration ont abouti, si nécessaire.
{: tip} 


### Modèles Smart Document Understanding
{: #backupsdu}

Si vous utilisez Smart Document Understanding (SDU), vous disposez de modèles associés à votre configuration. Pour éviter de perdre des informations, vous devez [exporter vos modèles](/docs/services/discovery?topic=discovery-sdu#import), les sauvegarder puis les stocker localement. Les modèles SDU ont l'extension de fichier `.sdumodel`.


## Restauration de vos données dans une nouvelle instance Watson Discovery
{: #restore}

Pensez à utiliser vos sauvegardes pour effectuer une restauration dans une nouvelle instance {{site.data.keyword.discoveryshort}} d'un autre centre de données (également appelé région/emplacement, par exemple Dallas, Houston, Washington, DC). 
{: note}

Pour lancer la restauration, commencez par consulter la liste des collections et des sources de données associées, ainsi que vos sauvegardes de fichier.

-  Créez votre [environnement](https://cloud.ibm.com/apidocs/discovery#create-an-environment) et vos [collections](https://cloud.ibm.com/apidocs/discovery#create-a-collection) en utilisant les informations de configuration sauvegardées. Vérifiez que la configuration appropriée ainsi que la langue de la collection sont définies correctement. Le non-respect de cette précaution retarde le bon fonctionnement de votre système.
-  Si vous avez des configurations personnalisées définies dans {{site.data.keyword.discoveryshort}}, vous devez [recréer ces configurations personnalisées](/docs/services/discovery?topic=discovery-configservice#when-you-need-a-custom-configuration). 
-  Ajoutez des dictionnaires de marquage sémantique ou des mots à exclure dans les collections. Voir [Création de dictionnaires de marquage sémantique personnalisés](/docs/services/discovery?topic=discovery-query-concepts#tokenization) et [Définition des mots à exclure](/docs/services/discovery?topic=discovery-query-concepts#stopwords). 
-  Si vous avez une extension de requête personnalisée, vous devez également [ajouter vos extensions de requête](https://cloud.ibm.com/apidocs/discovery#create-or-update-expansion-list) pour chaque collection. 
-  Si vous utilisez des modèles d'entité personnalisés de Watson Knowledge Studio (WKS) pour l'enrichissement, vous devez [réimporter ce modèle](/docs/services/discovery?topic=discovery-configservice#custom-entity-model) dans votre instance {{site.data.keyword.discoveryshort}}. 

Une fois que vos collections sont configurées comme elles l'étaient auparavant, vous devez commencer à ingérer vos documents source. En fonction du mode d'ingestion des documents utilisé précédemment, vous pouvez utiliser :
-  L'API [](https://cloud.ibm.com/apidocs/discovery#add-a-document)
-  Un connecteur [](/docs/services/discovery?topic=discovery-sources#sources) 
-  [Data Crawler](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler)
-  Ou une autre méthode

### Restauration des données d'apprentissage
{: #restoretraining}

Une fois que les collections ont été restaurées, vous pouvez commencer à [recréer vos modèles d'entraînement visant à améliorer la pertinence](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api). 

Extrayez les données d'apprentissage sauvegardées, puis :

1. [téléchargez vos requêtes](https://cloud.ibm.com/apidocs/discovery#add-query-to-training-data)
1. [téléchargez vos documents exemple](https://cloud.ibm.com/apidocs/discovery#add-example-to-training-data-query) pour chaque requête.
1.  Une fois que les données d'apprentissage sont téléchargées, consultez cet [article de blogue](https://developer.ibm.com/dwblog/2017/get-relevancy-training/) pour vous assurer que les valeurs de précision précédentes sont respectées. Gardez à l'esprit que les anciens `ID de document` doivent être transférés vers les nouvelles données d'apprentissage ou être mis à jour afin de refléter les nouveaux ID de document de votre nouvelle collection.


### Restauration de connexions dans des sources de données externes
{: #restoreconnections}

Lorsqu'une perte de données inattendue a lieu, vous pouvez perdre vos explorations planifiées des sources de données externes. Pour obtenir la liste des sources disponibles, voir [Connexion à des sources de données](/docs/services/discovery?topic=discovery-sources#sources).

Pour restaurer vos données externes, vous devez réétablir vos connexions à ces sources de données puis les explorer à nouveau.

Recherchez les données d'identification de source de données stockées précédemment et suivez les instructions présentées [ici](/docs/services/discovery?topic=discovery-sources#sources). Vous pourrez ensuite vous reconnecter à vos sources de données et obtenir les données importées dans {{site.data.keyword.discoveryshort}}.


### Restauration des modèles Smart Document Understanding
{: #restoresdu}

Pour importer un modèle Smart Document Understanding (SDU) précédemment exporté, suivez les instructions présentées [ici](/docs/services/discovery?topic=discovery-sdu#import). Les modèles SDU ont l'extension de fichier `.sdumodel`.

Lors de l'importation d'un modèle existant SDU dans une nouvelle collection, il est recommandé de créer la nouvelle collection, d'ajouter un document, d'importer ensuite le modèle puis de télécharger le reste de vos documents. 
