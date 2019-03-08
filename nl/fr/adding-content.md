---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-15"

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

# Ajout de contenu
{: #addcontent}

Comment choisir la méthode à utiliser pour télécharger le document ?
{: shortdesc}

-   Utilisez l'[API](/docs/services/discovery/getting-started.html) si vous intégrez le téléchargement de contenu à une application existante ou si vous créez votre propre mécanisme de téléchargement personnalisé.
-   Utilisez les [outils {{site.data.keyword.discoveryshort}} ](/docs/services/discovery/getting-started-tool.html) si vous souhaitez télécharger rapidement des fichiers accessibles localement.
    Lorsque vous téléchargez des documents à l'aide des outils {{site.data.keyword.discoveryshort}}, tous les documents doivent porter un nom de fichier unique. Si deux fichiers portent le même nom, le nom d'origine est remplacé lorsque la version plus récente est téléchargée. Si vous préférez faire coexister dans votre collection des documents portant le même nom de fichier, l'ID document doit être spécifié. Vous pouvez indiquer l'ID document si vous téléchargez des documents à l'aide de l'API ou de Data Crawler.
-   Utilisez les outils ou l'API {{site.data.keyword.discoveryshort}} pour vous connecter à des sources de données Box, Salesforce et Microsoft SharePoint Online. Voir [Connexion à des sources de données](/docs/services/discovery/connect.html) pour plus d'informations. 
-   Utilisez [Data Crawler](/docs/services/discovery/data-crawler.html) si vous souhaitez télécharger de manière gérée un nombre important de fichiers ou si vous souhaitez extraire le contenu d'un référentiel pris en charge (par exemple, une base de données DB2).

## Ajout de contenu à l'aide de l'API ou d'outils

Tenez compte des points suivants lorsque vous êtes prêt à ajouter des documents à votre collection :

-   La taille de fichier maximale qui peut être téléchargée sur le service {{site.data.keyword.discoveryshort}} est de 50 Mo.
-   Les exemples de document ne sont pas ajoutés automatiquement à la collection. Vous devez les ajouter si vous souhaitez qu'ils fassent partie de votre collection.
-   Seuls les 50 000 premiers caractères de chaque zone JSON sélectionnée pour enrichissement seront enrichis.
-   Lorsque vous créez une collection, vous sélectionnez la langue du document (l'anglais est la langue par défaut). Pour obtenir la liste de langues, voir [Support de langue](/docs/services/discovery/language-support.html). Vos documents seront enrichis dans la langue sélectionnée. Vous ne devez pas utiliser plusieurs langues dans une même collection.
-   Vous pouvez ajouter des documents Microsoft Word, PDF, HTML et JSON à votre collection. **Remarque :** les PDF qui sont des fichiers d'images scannées ne peuvent pas être convertis ni enrichis.
-   Les documents de votre collection seront convertis à l'aide du fichier de configuration fourni, nommé Default Configuration, sauf si vous choisissez un autre fichier de configuration. Pour toute information sur la création d'un fichier de configuration, voir [Configuration personnalisée](/docs/services/discovery/building.html#custom-configuration).
-   Lorsque des documents sont téléchargés dans une collection de données, ils sont convertis et enrichis à l'aide du fichier de configuration choisi pour cette collection. Si vous décidez ensuite d'affecter un autre fichier de configuration à une collection, vous pouvez le faire, mais les documents que vous avez déjà téléchargés resteront convertis via le fichier de configuration d'origine. Tous les documents téléchargés après le changement de fichier de configuration utiliseront le nouveau fichier de configuration. Si vous souhaitez que **toute** la collection utilise la nouvelle configuration, vous devrez créer une nouvelle collection, choisir ce nouveau fichier de configuration et télécharger à nouveau tous les documents.
-   Vous ne pouvez pas spécifier le `data type` (par exemple : `text` or `date`) des zones. Lors de l'ingestion de documents, si une zone est détectée alors qu'elle n'existe pas encore dans l'index, {{site.data.keyword.discoveryshort}} détectera automatiquement le `data type` de cette zone en fonction de la valeur de la zone pour le premier document indexé.
-   L'ingestion d'un document peut échouer en raison d'une non-concordance de type entre les données présentes dans les document en cours et des données similaires présentes dans un document déjà versé. Par exemple, une zone peut être du type `date` dans un document et être du type `string` dans un document suivant, ce qui empêche l'indexation de ce dernier.
-   Si vous prévoyez d'utiliser un marquage sémantique personnalisé (actuellement disponible uniquement pour les collections en langue japonaise lors de l'utilisation de l'API {{site.data.keyword.discoveryshort}}), le dictionnaire de marquage sémantique pour votre collection doit être ajouté avant le téléchargement des documents.

Les limites suivantes s'appliquent lors du téléchargement de documents :

-   Plans **Lite** : 21 documents en cours
-   Plans **Advanced** : 105 documents en cours (à l'exception des plans X-Small Advanced, dont la limite est à 50 documents en cours)
-   Plans **Premium** : 210 documents en cours

Ces limites sont susceptibles d'être modifiées. 

Lors de l'utilisation du service Discovery, le téléchargement en cours (in-flight) représente le document en cours de téléchargement et de traitement avant son ajout à la collection. Si vous atteignez votre limite en cours, vous devez ralentir le débit d'ingestion. Une option consiste à ajouter un mécanisme de retrait automatisé avec relances.

## Téléchargement de documents à l'aide des outils Discovery

1.  Créez une collection. Voir [Préparation du service pour vos documents](/docs/services/discovery/building.html#preparing-the-service-for-your-documents).
1.  Cliquez sur la collection pour l'ouvrir.
1.  Cliquez sur le bouton **Upload documents** et commencez le téléchargement de vos documents via les fonctions glisser-déplacer ou le bouton Browse.

Vos documents ont maintenant été ajoutés à la file d'attente pour être convertis et enrichis. La durée d'exécution de cette opération dépend de la taille de votre collection. Une fois les documents indexés et enrichis, les détails de la collection s'affichent dans la section **Overview**.

-   Zones de date **Created** et **Last updated** (cliquez sur **Use this collection in API** pour voir les paramètres `collection_id`, `configuration_id` et `environment_id`)
-   Zone **Number of documents** pour votre collection
-   **Configuration** — Nom du fichier de configuration utilisé pour convertir cette collection
-   **Errors and Warnings**

Pour plus d'informations sur le mode de connexion aux sources de données Box, Salesforce et Microsoft SharePoint Online avec les outils {{site.data.keyword.discoveryshort}}, voir [Connexion à des sources de données](/docs/services/discovery/connect.html).


## Téléchargement de documents à l'aide de l'API

Pour obtenir un tutoriel détaillé, voir [Initiation à l'API {{site.data.keyword.discoveryshort}} ](/docs/services/discovery/getting-started.html).

Pour plus d'informations sur l'API, voir le document [API Reference ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}.

1.  Utilisez la méthode `POST /v1/environments/{environment_id}/collections` pour créer une collection.
1.  Utilisez ensuite la méthode `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` pour ajouter des documents à votre collection.

## Exploration d'URL

Vous pouvez explorer des URL et les indexer à l'aide d'{{site.data.keyword.IBM_notm}} {{site.data.keyword.watson}} {{site.data.keyword.discoveryshort}} Service [Indexing plugin for Apache Nutch ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/IBM-Watson/nutch-indexer-discovery). L'exploration n'est pas mise à jour automatiquement, par conséquent, la procédure devra être répétée régulièrement pour que l'index reste à jour.
