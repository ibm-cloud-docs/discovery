---

copyright:
  years: 2015, 2018, 2019
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

# Ajout de contenu
{: #addcontent}

Comment choisir la méthode à utiliser pour télécharger le document ?
{: shortdesc}

-   Utilisez l'[API](/docs/services/discovery?topic=discovery-gs-api#gs-api) si vous intégrez le téléchargement de contenu à une application existante ou si vous créez votre propre mécanisme de téléchargement personnalisé.
-   Utilisez les [outils {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-getting-started#getting-started) si vous souhaitez télécharger rapidement des fichiers accessibles localement.
    Lorsque vous téléchargez des documents à l'aide des outils {{site.data.keyword.discoveryshort}}, tous les documents doivent porter un nom de fichier unique. Si deux fichiers portent le même nom, le nom d'origine est remplacé lorsque la version plus récente est téléchargée. Si vous préférez faire coexister dans votre collection des documents portant le même nom de fichier, l'ID document doit être spécifié. Vous pouvez indiquer l'ID document si vous téléchargez des documents à l'aide de l'API ou de Data Crawler.
-   Utilisez les outils {{site.data.keyword.discoveryshort}} ou l'API pour vous connecter à des sources de données Box, Salesforce, Microsoft SharePoint Online, IBM Cloud Object Storage et Microsoft SharePoint 2016 ou effectuer une exploration Web. Voir [Connexion à des sources de données](/docs/services/discovery?topic=discovery-sources#sources) pour plus d'informations.
-   Utilisez [Data Crawler](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler) si vous souhaitez télécharger de manière gérée un nombre important de fichiers ou si vous souhaitez extraire le contenu d'un référentiel pris en charge (par exemple, une base de données DB2).

## Ajout de contenu à l'aide de l'API ou d'outils
{: #adding-content-with-the-api-or-tooling}

Tenez compte des points suivants lorsque vous êtes prêt à ajouter des documents à votre collection :

-   La taille de fichier maximale qui peut être téléchargée sur le service {{site.data.keyword.discoveryshort}} est de 50 Mo.
-   Les exemples de document ne sont pas ajoutés automatiquement à la collection. Vous devez les ajouter si vous souhaitez qu'ils fassent partie de votre collection. (S'applique uniquement aux collections créées avant la sortie de [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu).)
-   Seuls les 50 000 premiers caractères de chaque zone JSON sélectionnée pour enrichissement seront enrichis.
-   Lorsque vous créez une collection, vous sélectionnez la langue du document (l'anglais est la langue par défaut). Pour obtenir la liste de langues, voir [Support de langue](/docs/services/discovery?topic=discovery-language-support#language-support). Vos documents seront enrichis dans la langue sélectionnée. Vous ne devez pas utiliser plusieurs langues dans une même collection.
-   Les types de fichier suivants peuvent être ingérés dans {{site.data.keyword.discoveryshort}}, tous les autres types de document sont ignorés :

Collection | Plans Lite | Plans Advanced 
---------------- | ------------------------------ | ------------------------------------------- 
Collections existantes créées spécifiquement pour {{site.data.keyword.discoveryfull}} avant la sortie de [Smart Document Understanding (SDU)](/docs/services/discovery?topic=discovery-release-notes#22jan19) | Microsoft Word, PDF, HTML, JSON | Microsoft Word, PDF, HTML, JSON     
Collections créées après la sortie de [SDU](/docs/services/discovery?topic=discovery-sdu#sdu) | PDF, Word, PowerPoint, Excel, JSON\*, HTML\* | PDF, Word, PowerPoint, Excel, PNG\*\*, TIFF\*\*, JPG\*\*, JSON\*, HTML\* 
    
\* Les documents JSON et HTML sont pris en charge par {{site.data.keyword.discoveryfull}} mais ne peuvent pas être modifiés à l'aide de l'éditeur SDU. Pour changer la configuration des documents HTML et JSON, vous devez utiliser l'API. Pour plus d'informations, voir la page de [référence d'API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery/){: new_window}.

\*\* Les fichiers individuels (PNG, TIFF, JPG) sont analysés et le texte (le cas échéant) est extrait. Les images PNG, TIFF et JPEG intégrées dans des fichiers PDF, Word, PowerPoint et Excel sont également analysées et le texte (le cas échéant) est extrait.
-   Les documents de votre collection sont convertis en utilisant la configuration en cours, sauf si vous choisissez un autre fichier de configuration. Pour toute information sur la création d'un fichier de configuration, voir [Configuration personnalisée](/docs/services/discovery?topic=discovery-configservice#custom-configuration). (S'applique uniquement aux collections créées avant la sortie de [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu).)
-   Lorsque des documents sont téléchargés dans une collection de données, ils sont convertis et enrichis à l'aide du fichier de configuration choisi pour cette collection. Si vous décidez ensuite d'affecter un autre fichier de configuration à une collection, vous pouvez le faire, mais les documents que vous avez déjà téléchargés resteront convertis via le fichier de configuration d'origine. Tous les documents téléchargés après le changement de fichier de configuration utiliseront le nouveau fichier de configuration. Si vous souhaitez que **toute** la collection utilise la nouvelle configuration, vous devrez créer une nouvelle collection, choisir ce nouveau fichier de configuration et télécharger à nouveau tous les documents. (Si vous utilisez [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu), vous êtes invité à recharger vos documents une fois que vous avez cliqué sur le bouton **Apply changes to collection**.)
-   Vous ne pouvez pas spécifier le `data type` (par exemple : `text` or `date`) des zones. Lors de l'ingestion de documents, si une zone est détectée alors qu'elle n'existe pas encore dans l'index, {{site.data.keyword.discoveryshort}} détectera automatiquement le `data type` de cette zone en fonction de la valeur de la zone pour le premier document indexé.
-   L'ingestion d'un document peut échouer en raison d'une non-concordance de type entre les données présentes dans les document en cours et des données similaires présentes dans un document déjà versé. Par exemple, une zone peut être du type `date` dans un document et être du type `string` dans un document suivant, ce qui empêche l'indexation de ce dernier.
-   Si vous prévoyez d'utiliser un marquage sémantique personnalisé (actuellement disponible uniquement pour les collections en langue japonaise lors de l'utilisation de l'API {{site.data.keyword.discoveryshort}}), le dictionnaire de marquage sémantique pour votre collection doit être ajouté avant le téléchargement des documents.

## Téléchargement de documents à l'aide des outils Discovery
{: #upload_tooling}

1.  Créez une collection. Voir [Préparation du service pour vos documents](/docs/services/discovery?topic=discovery-configservice#preparing-the-service-for-your-documents).
1.  Cliquez sur la collection pour l'ouvrir.
1.  Cliquez sur le bouton **Upload documents** et commencez le téléchargement de vos documents via les fonctions glisser-déplacer ou le bouton Browse.

Vos documents ont maintenant été ajoutés à la file d'attente pour être convertis et enrichis. La durée d'exécution de cette opération dépend de la taille de votre collection. Une fois les documents indexés et enrichis, les détails de la collection s'affichent dans la section **Overview**.

-   Les zones **Fields identified** de votre collection (Smart Document Understanding uniquement.)
-   Les zones de date **Created** et **Last updated** (cliquez sur **Use this collection in API** pour voir les paramètres `collection_id`, `configuration_id` et `environment_id`)
-   La zone **Number of documents** pour votre collection
-   La zone **Configuration** — Nom du fichier de configuration utilisé pour convertir cette collection (uniquement pour les collections créées avant la sortie de [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu)). 
-   La zone **Errors and Warnings**

Pour plus d'informations sur le mode de connexion aux sources de données Box, Salesforce, Microsoft SharePoint Online, IBM Cloud Object Storage et Microsoft SharePoint 2016 ou pour effectuer une exploration Web avec les outils {{site.data.keyword.discoveryshort}}, voir [Connexion à des sources de données](/docs/services/discovery?topic=discovery-sources#sources).


## Téléchargement de documents à l'aide de l'API
{: #upload_api}

Pour accéder à un tutoriel détaillé, voir [Initiation à l'API {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-gs-api#gs-api).

Pour plus d'informations sur l'API, voir la page de [référence d'API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery/){: new_window}.

1.  Utilisez la méthode `POST /v1/environments/{environment_id}/collections` pour créer une collection.
1.  Utilisez ensuite la méthode `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` pour ajouter des documents à votre collection.

## Exploration d'URL
{: #crawl_urls}

Vous pouvez explorer des URL et les indexer à l'aide d'{{site.data.keyword.IBM_notm}} {{site.data.keyword.watson}} {{site.data.keyword.discoveryshort}} Service [Indexing plugin for Apache Nutch ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/IBM-Watson/nutch-indexer-discovery). L'exploration n'est pas mise à jour automatiquement, par conséquent, la procédure devra être répétée régulièrement pour que l'index reste à jour. 

Vous avez également la possibilité d'utiliser la version bêta du connecteur Web Crawl. Voir [Connexion à des sources de données](/docs/services/discovery?topic=discovery-sources#connectwebcrawl).
