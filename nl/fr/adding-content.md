---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-10"

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

Comment choisir la méthode à utiliser pour télécharger le document ?
{: shortdesc}

-   Utilisez l'[API](/docs/services/discovery/getting-started.html) si vous intégrez le téléchargement de contenu à une application existante ou si vous créez votre propre mécanisme de téléchargement personnalisé. 
-   Utilisez les [outils {{site.data.keyword.discoveryshort}} ](/docs/services/discovery/getting-started-tool.html) si vous souhaitez télécharger rapidement des fichiers accessibles localement.
    Lorsque vous téléchargez des documents à l'aide des outils {{site.data.keyword.discoveryshort}}, tous les documents doivent porter un nom de fichier unique. Si deux fichiers portent le même nom, le nom d'origine est remplacé lorsque la version plus récente est téléchargée. Si vous préférez faire coexister dans votre collection des documents portant le même nom de fichier, l'ID document doit être spécifié. Vous pouvez indiquer l'ID document si vous téléchargez des documents à l'aide de l'API ou de Data Crawler.
-   Utilisez [Data Crawler](/docs/services/discovery/data-crawler.html) si vous souhaitez télécharger de manière gérée un nombre important de fichiers ou si vous souhaitez extraire le contenu d'un référentiel pris en charge (par exemple, une base de données DB2). 

## Ajout de contenu à l'aide de l'API ou d'outils

Tenez compte des points suivants lorsque vous êtes prêt à ajouter des documents à votre collection :

-   La taille de fichier maximale qui peut être téléchargée sur le service {{site.data.keyword.discoveryshort}} est de 50 Mo. 

-   Les exemples de document ne sont pas ajoutés automatiquement à la collection. Vous devez les ajouter si vous souhaitez qu'ils fassent partie de votre collection.

-   Lorsque vous créez une collection, vous sélectionnez la langue du document (l'anglais est la langue par défaut). Pour obtenir la liste de langues, voir [Support de langue](/docs/services/discovery/language-support.html). Vos documents seront enrichis dans la langue sélectionnée. Vous ne devez pas utiliser plusieurs langues dans une même collection. 

-   Vous pouvez ajouter des documents Microsoft Word, PDF, HTML et JSON à votre collection. **Remarque :** les PDF qui sont des fichiers d'images scannées ne peuvent pas être convertis ni enrichis.  

-   Les documents de votre collection seront convertis à l'aide du fichier de configuration fourni, nommé Default Configuration, sauf si vous choisissez un autre fichier de configuration. Pour toute information sur la création d'un fichier de configuration, voir [Configuration personnalisée](/docs/services/discovery/building.html#custom-configuration).

-   Lorsque des documents sont téléchargés dans une collection de données, ils sont convertis et enrichis à l'aide du fichier de configuration choisi pour cette collection. Si vous décidez ensuite d'affecter un autre fichier de configuration à une collection, vous pouvez le faire, mais les documents que vous avez déjà téléchargés resteront convertis via le fichier de configuration d'origine. Tous les documents téléchargés après le changement de fichier de configuration utiliseront le nouveau fichier de configuration. Si vous souhaitez que **toute** la collection utilise la nouvelle configuration, vous devrez créer une nouvelle collection, choisir ce nouveau fichier de configuration et télécharger à nouveau tous les documents. 

## Téléchargement de documents à l'aide des outils Discovery

1.  Créez une collection. Voir [Préparation du service pour vos documents](/docs/services/discovery/building.html#preparing-the-service-for-your-documents).
1.  Cliquez sur la collection pour l'ouvrir.
1.  Cliquez sur le bouton **Upload documents** et commencez le téléchargement de vos documents via les fonctions glisser-déplacer ou le bouton Browse. 

Vos documents ont maintenant été ajoutés à la file d'attente pour être convertis et enrichis. La durée d'exécution de cette opération dépend de la taille de votre collection. Une fois les documents indexés et enrichis, les détails de la collection s'affichent dans la section **Overview**. 

-   Zones de date **Created** et **Last updated** (cliquez sur **Use this collection in API** pour voir les paramètres `collection_id`, `configuration_id` et `environment_id`)
-   Zone **Number of documents** pour votre collection
-   **Configuration** — Nom du fichier de configuration utilisé pour convertir cette collection
-   **Errors and Warnings**

## Téléchargement de documents à l'aide de l'API

Pour obtenir un tutoriel détaillé, voir [Initiation à l'API {{site.data.keyword.discoveryshort}} ](/docs/services/discovery/getting-started.html). 

Pour plus d'informations sur l'API, voir le document [API Reference ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}.

1.  Utilisez la méthode `POST /v1/environments/{environment_id}/collections` pour créer une collection.
1.  Utilisez ensuite la méthode `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` pour ajouter des documents à votre collection.

## Exploration d'URL

Vous pouvez explorer des URL et les indexer à l'aide d'{{site.data.keyword.IBM_notm}} {{site.data.keyword.watson}} {{site.data.keyword.discoveryshort}} Service [Indexing plugin for Apache Nutch ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/IBM-Watson/nutch-indexer-discovery). L'exploration n'est pas mise à jour automatiquement, par conséquent, la procédure devra être répétée régulièrement pour que l'index reste à jour. 
