---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-25"

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

# Configuration des options de connecteur et de point de départ

Lorsqu'il explore des données, le moteur d'exploration identifie d'abord le type de référentiel de données (connecteur) et l'emplacement de départ spécifié par l'utilisateur (point de départ) pour commencer à télécharger des informations.
{: shortdesc}

**Important :** lorsqu'il utilise Data Crawler, les paramètres de sécurité du référentiel de données sont ignorés.

Les points de départ d'une exploration sont utilisés par Data Crawler pour extraire des données de la ressource qui est identifiée par le connecteur. Généralement, les points de départ configurent des URL permettant d'accéder à des ressources basées sur un protocole, telles que des partages de fichiers, des partages SMB, des bases de données et d'autres référentiels de données accessibles par différents protocoles. De plus, différentes adresses URL de départ ont des fonctionnalités différentes. Les valeurs de départ peuvent également être spécifiques au référentiel, pour
permettre l'exploration d'applications tiers spécifiques, telles que des systèmes CRM
(Customer Relationship Management), des systèmes PLC (Product Life Cycle), des systèmes
CMS (Content Management System), des applications cloud et des applications de base de
données Web.

Pour explorer vos données, vous devez vous assurer que le moteur d'exploration est correctement configuré pour lire votre référentiel de données. Data Crawler fournit des connecteurs pour prendre en charge la collecte de données à partir des référentiels suivants :

-   [Système de fichiers](/docs/services/discovery/data-crawler-seeds.html#configuring-filesystem-crawl-options)
-   [Bases de données, via JDBC](/docs/services/discovery/data-crawler-seeds.html#configuring-database-crawl-options)
-   [CMIS (Content Management Interoperability Services)](/docs/services/discovery/data-crawler-seeds.html#configuring-cmis-crawl-options)
-   [Partages de fichiers SMB (Server Message Block), CIFS (Common Internet Filesystem) ou Samba](/docs/services/discovery/data-crawler-seeds.html#configuring-smbcifssamba-crawl-options)
-   [SharePoint et SharePoint Online](/docs/services/discovery/data-crawler-seeds.html#configuring-sharepoint-crawl-options)
-   [Box](/docs/services/discovery/data-crawler-seeds.html#configuring-box-crawl-options)

Un modèle de configuration de connecteur est également fourni, pour vous permettre de personnaliser un connecteur.

Pour configurer votre connecteur, procédez comme suit :

1.  Ouvrez le fichier dans le répertoire `connectors` correspondant au référentiel auquel vous vous connectez (par exemple, `filesystem.conf` est le fichier de configuration du connecteur de système de fichiers) dans un éditeur de texte.

1.  Modifiez les valeurs concernant votre référentiel :

    -   [Système de fichiers](/docs/services/discovery/data-crawler-seeds.html#filesystem-crawl-options)
    -   [Bases de données, via JDBC](/docs/services/discovery/data-crawler-seeds.html#database-crawl-seed)
    -   [CMIS (Content Management Interoperability Services)](/docs/services/discovery/data-crawler-seeds.html#cmis-crawl-options)
    -   [Partages de fichiers SMB (Server Message Block), CIFS (Common Internet Filesystem) ou Samba](/docs/services/discovery/data-crawler-seeds.html#smb-cifs-samba-crawl-options)
    -   [SharePoint et SharePoint Online](/docs/services/discovery/data-crawler-seeds.html#sharepoint-crawl-options)
    -   [Box](/docs/services/discovery/data-crawler-seeds.html#box-crawl-options)
1.  Sauvegardez et fermez le fichier.
1.  Répétez l'opération pour le fichier `-seed.conf` du répertoire `connectors/seeds` correspondant au référentiel auquel vous vous connectez (par exemple, `filesystem-seed.conf` est le fichier de configuration du point de départ (où se connecter) pour le connecteur de système de fichiers) dans un éditeur de texte.
1.  Vous pouvez maintenant [configurer Data Crawler pour qu'il se connecte à {{site.data.keyword.discoveryshort}}](/docs/services/discovery/data-crawler-discovery.html).

Pour accéder au manuel intégré au produit qui est relatif aux fichiers de configuration de point de départ et de connecteur et qui contient les toutes dernières informations, tapez les commandes suivantes dans le répertoire d'installation de Data Crawler :
-   Pour les options de configuration du connecteur :
    ```bash
    man crawler-options.conf
    ```
    {: pre}
-   Pour les options de configuration du point de départ d'exploration :
    ```bash
    man crawler-seed.conf
    ```
    {: pre}


## Configuration des options d'exploration de système de fichiers
{: #filesystem-crawl-options}

Le connecteur de système de fichiers vous permet d'explorer des fichiers localement dans l'installation Data Crawler.

### Configuration du connecteur de système de fichiers

Vous trouverez ci-après les options de configuration de base requises pour utiliser le connecteur de système de fichiers. Pour définir ces valeurs, ouvrez le fichier `config/connectors/filesystem.conf` et modifiez les valeurs suivantes, propres à vos cas d'utilisation :

-   **`protocol`** - Nom du protocole de connecteur utilisé pour l'exploration. Utilisez `sdk-fs` pour ce connecteur.
-   **`collection`** - Cet attribut permet de décompresser les fichiers temporaires. La valeur par défaut est `crawler-fs`
-   **`logging-config`** - Spécifie le fichier utilisé pour configurer les options de consignation ; il doit être formaté sous forme de chaîne XML `log4j`.
-   **`classname`** - Nom de classe Java du connecteur. Pour utiliser ce connecteur, la valeur doit être `plugin:filesystem.plugin@filesystem`.

### Configuration de la valeur de départ d'exploration de système de fichiers

Les valeurs suivantes peuvent être configurées pour le fichier de départ de l'exploration du système de fichiers. Pour définir ces valeurs, ouvrez le fichier `config/seeds/filesystem-seed.conf` et spécifiez les valeurs suivantes, propres à vos cas d'utilisation :

-   **`url`** - Liste de fichiers et dossiers à explorer, séparés par des retours à la ligne. Les utilisateurs UNIX peuvent utiliser un chemin d'accès tel que le suivant : `/usr/local/`.

    **Remarque :** les URL doivent débuter par `sdk-fs://`. Par conséquent, pour explorer, par exemple, `/home/watson/mydocs`, la valeur de cette adresse URL doit être `sdk-fs:///home/watson/mydocs` (le troisième `/` est nécessaire !)

    Les systèmes de fichiers utilisés par les systèmes informatiques Linux, UNIX et de type UNIX peuvent contenir des types de fichier spéciaux, tels que des noeuds et des fichiers d'unité par caractère et par bloc qui représentent des canaux de communication nommés qui ne peuvent pas être explorés car ils ne contiennent pas de données, mais qui servent de points d'accès d'E-S ou d'unité. Si vous tentez d'explorer ce type de fichier, des erreurs seront générées lors de l'opération. Pour éviter de telles erreurs, vous devez exclure le répertoire `/dev` dans les explorations de niveau supérieur réalisées sur un système de fichiers Linux, UNIX ou de type UNIX. S'ils sont présents sur le système que vous explorez, vous devez également exclure les répertoires système temporaires, tels que `/proc`, `/sys` et `/tmp`, qui contiennent des fichiers transitoires et des informations système.   **`hops`** - Usage interne uniquement.   **`default-allow`** - Usage interne uniquement.
    {: tip}

## Configuration des options d'exploration de base de données

Le connecteur de base de données vous permet d'explorer une base de données en exécutant une commande SQL personnalisée et en créant un document par ligne (enregistrement) et un élément de contenu par colonne (zone). Vous pouvez spécifier une colonne à utiliser comme clé unique, ainsi qu'une colonne contenant un horodatage représentant la date de la dernière modification de chaque enregistrement. Le connecteur extrait tous les enregistrements de la base de données spécifiée et peut être également restreint à des tables ou jointures spécifiques dans l'instruction SQL.

Le connecteur de base de données vous permet d'explorer les bases de données suivantes :

-   {{site.data.keyword.IBM}} DB2
-   MySQL
-   Oracle PostgreSQL
-   Microsoft SQL Server
-   Sybase
-   Autres bases de données compatibles avec SQL, via un pilote compatible avec JDBC 3.0

Le connecteur extrait tous les enregistrements de la base de données et de la table spécifiées.

***JDBC Drivers*** - Le connecteur de base de données est fourni avec le pilote Oracle JDBC (Java Database Connectivity), version 1.5. Tous les pilotes JDBC tiers fournis avec Data Crawler se trouvent dans le répertoire `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` de votre installation Data Crawler, dans lequel vous ajouter, retirer et modifier ces pilotes en fonction de vos besoins. Vous pouvez également utiliser le paramètre `extra_jars_dir` du fichier `crawler.conf` pour spécifier un autre emplacement.

***DB2 JDBC Drivers*** - Data Crawler n'est pas fourni avec les pilotes JDBC DB2 en raison de problèmes d'octroi de licence. Toutefois, toutes les installations DB2 dans lesquelles vous avez installé la prise en charge de JDBC comprennent les fichiers JAR requis par Data Crawler, rendant possible l'exploration d'une installation DB2. Pour explorer une instance DB2, vous devez copier ces fichiers dans le répertoire approprié de votre installation Data Crawler de sorte que le connecteur de base de données puisse les utiliser. Pour permettre à Data Crawler d'explorer une installation DB2, localisez les fichiers JAR `db2jcc.jar` et de licence (généralement, `db2jcc_license_cu.jar`) dans votre installation DB2 et copiez-les dans le sous-répertoire `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` de votre répertoire d'installation de Data Crawler. Vous pouvez aussi utiliser le paramètre `extra_jars_dir` dans le fichier `crawler.conf` pour spécifier un autre emplacement.

***MySQL JDBC Drivers*** - Data Crawler n'est pas fourni avec les pilotes JDBC MySQL en raison de problèmes d'octroi de licence potentiels si ces derniers ont été fournis dans le cadre du produit. Toutefois, le téléchargement du fichier JAR qui contient les pilotes JDBC MySQL et l'intégration de fichier JAR dans votre installation Data Crawler sont assez faciles à effectuer :

1.  Utilisez un navigateur Web pour visiter le site de téléchargement de MySQL et rechercher le lien de téléchargement de la source et du binaire pour le format d'archive à utiliser (généralement zip pour les systèmes Microsoft Windows et fichier compressé gzipped pour les systèmes Linux). Cliquez sur ce lien pour lancer le processus de téléchargement. L'inscription peut être requise.
1.  Utilisez la commande unzip archive-file-name ou tar zxf archive-file-name appropriée pour extraire le contenu de cette archive, en fonction du type et du nom du fichier archive que vous téléchargez.
1.  Passez dans le répertoire qui a été extrait du fichier archive et copiez le fichier JAR à partir de ce répertoire dans le sous-répertoire  `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` du répertoire d'installation de Data Crawler. Vous pouvez aussi utiliser le paramètre `extra_jars_dir` dans le fichier `crawler.conf` pour spécifier un autre emplacement.

### Configuration du connecteur de base de données

Vous trouverez ci-après les options de configuration de base requises pour utiliser le connecteur de base de données. Pour définir ces valeurs, ouvrez le fichier config/connectors/database.conf et modifiez les valeurs suivantes, propres à vos cas d'utilisation :

-   **`protocol`** - Nom du protocole de connecteur utilisé pour l'exploration. La valeur de ce connecteur est basée sur le système de base de données à atteindre.
-   **`collection`** - Cet attribut permet de décompresser les fichiers temporaires.
-   **`classname`** - Nom de classe Java du connecteur. Pour utiliser ce connecteur, la valeur doit être `plugin:database.plugin@database`.
-   **`logging-config`** - Spécifie le fichier utilisé pour configurer les options de consignation ; il doit être formaté sous forme de chaîne XML `log4j`.

### Configuration de la valeur de départ d'exploration de la base de données
{: #database-crawl-seed}

Les valeurs suivantes peuvent être configurées pour le fichier de départ d'exploration de la base de données. Pour définir ces valeurs, ouvrez le fichier `config/seeds/database-seed.conf` et spécifiez les valeurs suivantes, propres à vos cas d'utilisation :

-   **`url`** - Adresse URL de la table ou vue à extraire. Définit l'adresse URL de départ personnalisée de votre base de données SQL. Sa structure est la suivante :

    -   `database-system://host:port/database?[per=num]&[sql=SQL]`

    Le test d'une adresse URL de départ permet d'afficher toutes les adresses URL placées en file d'attente. Par exemple, le test de l'adresse URL suivante d'une base de données contenant 200 enregistrements :
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?per=100&sql=select%20*%20from%20vessel&`

    affiche les adresses URL en file d'attente suivantes :
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=0&`
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=100&`
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=200&`

    Lors des tests, l'adresse URL suivante affichera les données extraites de la ligne 43 :
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?per-1&key-val=43`
-   **`hops`** - Usage interne uniquement.
-   **`default-allow`** - Usage interne uniquement.
-   **`user-password`** - Données d'identification du système de base de données. Le nom d'utilisateur et le mot de passe doivent être séparés par un `:`, et le mot de passe doit être chiffré à l'aide du programme vcrypt fourni avec Data Crawler. Par exemple : `username:[[vcrypt/3]]passwordstring`
-   **`max-data-size`** - Taille maximale des données d'un document. Il s'agit du bloc de mémoire le plus volumineux qui sera chargé en une fois. N'augmentez cette limite que si vous disposez d'une quantité de mémoire suffisante sur votre ordinateur.
-   **`filter-exact-duplicates`** - Usage interne uniquement.
-   **`timeout`** - Usage interne uniquement.
-   **`jdbc-class`** (option Extender) - Si cette chaîne est spécifiée, elle remplace la classe JDBC utilisée par le connecteur lorsque l'option `(other)` est sélectionnée comme système de base de données.
-   **`connection-string`** (option Extender) - Si cette chaîne est spécifiée, elle remplace la chaîne de connexion JDBC générée automatiquement. Cela vous permet de fournir une configuration plus détaillée sur la connexion de base de données, comme l'équilibrage de charge ou les connexions SSL. Par exemple :`jdbc:netezza://127.0.0.1:5480/databasename`
-   **`save-frequency-for-resume`** (option Extender) - Spécifie le nom d'une colonne ou d'un libellé associé, pour pouvoir reprendre une exploration ou effectuer une actualisation partielle. La valeur de départ sauvegarde le nom de cette colonne à intervalles réguliers au cours de l'exploration et la sauvegarde de nouveau une fois que la dernière ligne de votre base de données a été explorée. Lors de la reprise ou de l'actualisation de l'exploration, celle-ci commence à la ligne qui est identifiée dans la valeur sauvegardée pour cette zone.

## Configuration des options d'exploration CMIS
{: #cmis-crawl-options}

Le connecteur CMIS (Content Management Interoperability Services) vous permet d'explorer les référentiels CMS (Content Management System) activés par CMIS, tels que Alfresco, Documentum ou {{site.data.keyword.IBM}} Content Manager, et d'indexer les données qu'ils contiennent.

### Configuration du connecteur CMIS

Vous trouverez ci-après les options de configuration de base requises pour utiliser le connecteur CMIS. Pour définir ces valeurs, ouvrez le fichier `config/connectors/cmis.conf` et spécifiez les valeurs suivantes, propres à vos cas d'utilisation :

-   **`protocol`** - Nom du protocole de connecteur utilisé pour l'exploration. La valeur à utiliser pour ce connecteur doit être `cmis`.
-   **`collection`** - Cet attribut permet de décompresser les fichiers temporaires.
-   **`dns`** - Option inutilisée.
-   **`classname`** - Nom de classe Java du connecteur. Utilisez `plugin:cmis-v1.1.plugin@connector` pour ce connecteur.
-   **`logging-config`** - Spécifie le fichier utilisé pour configurer les options de consignation ; il doit être formaté sous forme de chaîne XML `log4j`.
-   **`endpoint`** - Adresse URL du noeud final de service d'un référentiel compatible CMIS. Par exemple, les structures d'adresse URL pour SharePoint sont les suivantes :

    -   Pour la liaison AtomPub : `http://yourserver/_vti_bin/cmis/rest?getRepositories`
    -   Pour la liaison WebServices : `http://yourserver/_vti_bin/cmissoapwsdl.aspx`
-   **`username`** - Nom d'utilisateur de l'utilisateur de référentiel CMIS utilisé pour accéder au contenu. Cet utilisateur doit avoir accès à tous les dossiers cible et documents à explorer et indexer.
-   **`password`** - Mot de passe du référentiel CMIS utilisé pour accéder au contenu. Le mot de passe ne doit PAS être chiffré ; il doit être spécifié en texte en clair.
-   **`repositoryid`** - ID du référentiel CMIS permettant d'accéder au contenu de ce répertoire spécifique.
-   **`bindingtype`** - Identifie le type de liaison permettant de se connecter à un référentiel CMIS. La valeur est AtomPub ou WebServices.
-   **`authentication`** - Identifie le type de mécanisme d'authentification à utiliser pour contacter un référentiel compatible CMIS : Basic HTTP Authentication, NTLM ou WS-Security(Username token).
-   **`enable-acl`** - Permet d'extraire les listes de contrôle d'accès des données explorées. Si vous n'êtes pas préoccupé par la sécurité pour les documents de cette collection, la désactivation de cette option améliore les performances car ces informations ne sont pas demandées avec le document et elles ne sont donc ni extraites, ni codées. La valeur est true ou false.
-   **`user-agent`** - En-tête envoyé au serveur lors de l'exploration de documents.
-   **`method`** - Méthode (GET ou POST) par laquelle les paramètres seront transmis.
-   **`url-logging`** - Mesure dans laquelle les adresses URL explorées sont consignées. Les valeurs possibles sont les suivantes :

    -   `full-logging` - Permet de consigner toutes les informations relatives à l'URL.
    -   `refined-logging` - Permet de consigner uniquement les informations nécessaires pour parcourir le journal de moteur d'exploration et pour que le connecteur puisse fonctionner correctement. Il s'agit de la valeur par défaut.
    -   `minimal-logging` - Permet de consigner uniquement la quantité minimale d'informations nécessaires pour que le connecteur puisse fonctionner correctement.

    Si vous choisissez la valeur `minimal-logging` pour cette option, la taille des journaux est réduite et les performances sont légèrement améliorées en raison de la moindre quantité d'E/S associée à la minimisation de la quantité de données consignées.
-   **`ssl-version`** - Permet de spécifier une version de SSL à utiliser pour les connexions HTTPS. Par défaut, le protocole le plus fort disponible est utilisé.

### Configuration de la valeur de départ d'exploration CMIS

Les valeurs suivantes peuvent être configurées pour le fichier de départ d'exploration CMIS. Pour définir ces valeurs, ouvrez le fichier `config/seeds/cmis-seed.conf` et modifiez les valeurs suivantes, propres à vos cas d'utilisation :

-   **`url`** - URL d'un dossier à partir du référentiel CMIS qui doit être utilisé en tant que point de départ de l'exploration, par exemple : `cmis://alfresco.test.com:8080/alfresco/cmisatom?folderToProcess-workspace://SpacesStore/guid`

    Pour effectuer une exploration à partir du dossier racine, vous devez fournir l'URL comme suit : `cmis://alfresco.test.com:8080/alfresco/cmisatom?folderToProcess-`
-   **`at`** - Option inutilisée.
-   **`default-allow`** - Usage interne uniquement.

## Configuration des options d'exploration SMB/CIFS/Samba
{: #smb-cifs-samba-crawl-options}

Le connecteur Samba vous permet d'explorer des partages de fichiers SMB (Server Message Block) et CIFS (Common Internet filesystem). Ce type de partage de fichiers est courant sur les réseaux Windows et est également fourni par l'intermédiaire du projet open source Samba.

### Configuration du connecteur Samba

Vous trouverez ci-après les options de configuration de base requises pour utiliser le connecteur Samba. Pour définir ces valeurs, ouvrez le fichier`config/connectors/samba.conf` et spécifiez les valeurs suivantes, propres à vos cas d'utilisation :

-   **`protocol`** - Nom du protocole de connecteur utilisé pour l'exploration. La valeur à utiliser pour ce connecteur est smb.
-   **`collection`** - Cet attribut permet de décompresser les fichiers temporaires.
-   **`classname`** - Nom de classe Java du connecteur. Pour utiliser ce connecteur, la valeur doit être `plugin:smb.plugin@connector`.
-   **`logging-config`** - Spécifie le fichier utilisé pour configurer les options de consignation ; il doit être formaté sous forme de chaîne XML `log4j`.
-   **`username`** - Nom d'utilisateur Samba permettant de s'authentifier. S'il est spécifié, le domaine et le mot de passe doivent l'être également. S'il n'est pas fourni, le compte invité est utilisé.
-   **`password`** - Mot de passe Samba permettant de s'authentifier. Si le nom d'utilisateur est spécifié, ce mot de passe est requis. Le mot de passe doit être chiffré à l'aide du programme vcrypt fourni avec Data Crawler.
-   **`archive`** - Permet au connecteur Samba d'explorer et d'indexer les fichiers compressés dans les fichiers archive. La valeur possible est true ou false ; la valeur par défaut est false.
-   **`max-policies-per-handle`** - Indique le nombre maximal de règles LSA (Local Security Authority) pouvant être ouvertes pour un même descripteur RPC. Ces règles définissent les droits d'accès requis pour interroger ou modifier un système particulier dans diverses conditions. La valeur par défaut de cette option est 255.
-   **`crawl-fs-metadata`** - Lorsque vous activez cette option, Data Crawler ajoute un document VXML contenant les métadonnées de système de fichiers disponibles relatives au fichier (date de création, date de dernière modification, attributs de fichier, etc.).
-   **`enable-arc-connector`** - Option inutilisée.
-   **`disable-indexes`** - Liste d'index à désactiver, séparés par des retours à la ligne, qui peut accélérer l'exploration. Par exemple :

    -   `disable-url-index`
    -   `disable-error-state-index`
    -   `disable-crawl-time-index`
-   **`exact-duplicates-hash-size`** - Définit la taille de la table de hachage utilisée pour résoudre les doublons exacts. Soyez très prudent lorsque vous modifiez ce nombre. La valeur que vous sélectionnez doit être primordiale ; des tailles plus grandes peuvent fournir des recherches plus rapides, mais nécessiteront davantage de mémoire, tandis que des tailles plus petites pourront ralentir les explorations, mais réduiront considérablement la quantité de mémoire requise.
-   **`user-agent`** - Option inutilisée.
-   **`timeout`** - Option inutilisée.
-   **`n-concurrent-requests`** - Nombre de demandes qui seront envoyées en parallèle à une même adresse IP. La valeur par défaut est `1`.
-   **`enqueue-persistence`** - Option inutilisée.

### Configuration de la valeur de départ d'exploration Samba

Les valeurs suivantes peuvent être configurées pour le fichier de départ d'exploration Samba. Pour définir ces valeurs, ouvrez le fichier `config/seeds/samba-seed.conf` et spécifiez les valeurs suivantes, propres à vos cas d'utilisation :

-   **`url`** - Liste de partages à explorer, séparés par des retours à la ligne. Par exemple :

    ```
    smb://share.test.com/office
    smb://share.test.com/cash/money/change
    smb://share.test.com/C$/Program Files
    ```
    {: codeblock}

-   **`hops`** - Usage interne uniquement.
-   **`default-allow`** - Usage interne uniquement.

## Configuration des options d'exploration SharePoint
{: #sharepoint-crawl-options}

**Important :** le connecteur SharePoint requiert Microsoft SharePoint Server 2007 (MOSS 2007), SharePoint Server 2010, SharePoint Server 2013 ou SharePoint Online.

Le connecteur SharePoint vous permet d'explorer les objets SharePoint et d'indexer les informations qu'ils contiennent. Un objet, tel qu'un document, un profil utilisateur, une collecte de site, un blogue, un élément de liste, une liste d'appartenance, une page de répertoire, etc. peut être indexé avec les métadonnées qui lui sont associées. Pour les éléments de liste et les documents, les index peuvent inclure des pièces jointes.

Le connecteur SharePoint respecte l'attribut `noindex` sur tous les objets SharePoint, quel que soit leur type spécifique (blogues, documents, profils utilisateur, etc.). Un seul document est renvoyé pour chaque résultat.
{: tip}

**Important :** le compte SharePoint que vous utilisez pour explorer vos sites SharePoint doit au moins comporter des privilèges d'accès en lecture complets.

### Configuration du connecteur SharePoint

Vous trouverez ci-après les options de configuration de base requises pour utiliser le connecteur SharePoint. Pour définir ces valeurs, ouvrez le fichier `config/connectors/sharepoint.conf` et modifiez les valeurs suivantes, propres à vos cas d'utilisation :

-   **`protocol`** - Nom du protocole de connecteur utilisé pour l'exploration. La valeur à utiliser pour ce connecteur est `io-sp`.
-   **`collection`** - Cet attribut permet de décompresser les fichiers temporaires.
-   **`classname`** - Nom de classe Java du connecteur. Utilisez `plugin:io-sharepoint.plugin@connector` pour ce connecteur.
-   **`logging-config`** - Spécifie le fichier utilisé pour configurer les options de consignation ; il doit être formaté sous forme de chaîne XML `log4j`.
-   **`seed-url-type`** - Identifie le type d'objet SharePoint vers lequel pointent les adresses URL de départ : collections de site ou applications Web (également appelées serveurs virtuels).

    -   `Site Collections` - Si cette valeur est affectée au paramètre Seed URL Type, seuls les enfants de la collection de site référencée par l'URL sont explorés.
    -   `Web Applications` - Si cette valeur est affectée au paramètre Seed URL Type, toutes les collections de site (et leurs enfants) appartenant aux applications Web référencées par chaque URL sont explorées.
-   **`auth-type`** - Mécanisme d'authentification à utiliser lorsque vous contactez le serveur SharePoint : `BASIC`, `NTLM2`, `KERBEROS` ou `CBA`. Le type d'authentification par défaut est `NTLM2`.
-   **`spUser`** - Nom d'utilisateur de l'utilisateur SharePoint utilisé pour accéder au contenu. Cet utilisateur doit avoir accès à tous les sites cible, ainsi qu'à toutes les listes à explorer et indexer et doit pouvoir extraire et résoudre les droits associés. Il est préférable de l'entrer avec le nom de domaine. Par exemple : `MYDOMAIN\\Administrator`.
-   **`spPassword`** - Mot de passe de l'utilisateur SharePoint utilisé pour accéder au contenu. Le mot de passe doit être chiffré à l'aide du programme vcrypt fourni avec Data Crawler.
-   **`cba-sts`** - Adresse URL du noeud final STS (Security Token Service) pour tenter d'authentifier l'utilisateur de l'exploration. Pour SharePoint sur site avec ADFS, il doit s'agir de votre noeud final ADFS. Si le type d'authentification défini est CBA, cette zone est requise.
-   **`cba-realm`** - Identificateur de l'approbation de partie de confiance à utiliser lors d'une demande de jeton de sécurité au service STS. Cette option est parfois appelée valeur "AppliesTo" ou "Domaine". Pour SharePoint Online, elle doit correspondre à l'adresse URL de la racine de l'instance SharePoint Online (par exemple, `https://mycompany.sharepoint.com`). Pour ADFS, il s'agit de la valeur de l'ID de l'approbation de partie de confiance entre SharePoint et ADFS (par exemple, `"urn:SHAREPOINT:adfs"`).
-   **`everyone-group`** - Si ce nom de groupe est spécifié, il est utilisé dans les listes de contrôle d'accès lorsque l'accès doit être octroyé à tous les utilisateurs. Cette zone est requise si l'exploration des profils utilisateur est activée.

    **Remarque :** la sécurité n'est pas respectée par le service Retrieve and Rank.

-   **`user-profile-master-url`** - Adresse URL de base utilisée par le connecteur pour générer les liens aux profils utilisateur. Elle doit être configurée pour pointer vers le formulaire d'affichage des profils utilisateur. Si le jeton `%FIRST_SEED%` est rencontré, il est remplacé par la première adresse URL de départ. Cette zone est requise si l'exploration des profils utilisateur est activée.
-   **`urls`** - Liste d'adresses URL HTTP de collections de site ou d'applications Web SharePoint à explorer, séparées par des retours à la ligne.
-   **`ehcache-config`** - Option inutilisée.
-   **`method`** - Méthode (`GET` ou `POST`) par laquelle les paramètres seront transmis.
-   **`cache-types`** - Option inutilisée.
-   **`cache-size`** - Option inutilisée.
-   **`enable-acl`** - Permet d'activer l'exploration des profils utilisateur SharePoint ; les valeurs sont `true` ou `false` ; la valeur par défaut est `false`.

### Configuration de la valeur de départ d'exploration SharePoint

Les valeurs supplémentaires ci-après peuvent être configurées pour le fichier de départ d'exploration SharePoint. Pour définir ces valeurs, ouvrez le fichier `config/seeds/sharepoint-seed.conf` et spécifiez les valeurs suivantes, propres à vos cas d'utilisation :

-   **`url`** - Liste d'adresses URL de collections de site ou d'applications Web SharePoint à explorer, séparées par des retours à la ligne. Par
exemple :

    ```
    io-sp://a.com
    io-sp://b.com:83/site
    io-sp://c.com/site2
    ```
    {: codeblock}

    Les sites secondaires de ces sites seront également explorés (à moins qu'ils ne soient exclus par d'autres règles d'exploration).

-   **`filter-url`** - Liste d'adresses URL de collections de site ou d'applications Web SharePoint à explorer, séparées par des retours à la ligne. Par
exemple :

    ```
    http://a.com
    http://b.com:83/site
    http://c.com/site2
    ```
    {: codeblock}

-   **`hops`** - Usage interne uniquement.
-   **`n-concurrent-requests`** - Usage interne uniquement.
-   **`delay`** - Usage interne uniquement.
-   **`default-allow`** - Usage interne uniquement.
-   **`seed-protocol`** - Définit le protocole des valeurs de départ des enfants de la collecte du site. Nécessaire si le protocole de la collecte du site est SSL, HTTP ou HTTPS. Cette valeur doit correspondre à celle du protocole de la collecte du site.

## Configuration des options d'exploration Box

Le connecteur Box vous permet d'explorer l'instance Box de votre entreprise et d'indexer les informations qu'elle contient.

### Configuration du connecteur Box

Vous trouverez ci-après les options de configuration de base requises pour utiliser le connecteur Box. Pour définir ces valeurs, ouvrez le fichier `config/connectors/box.conf` et modifiez les valeurs suivantes, propres à vos cas d'utilisation :

-   **`protocol`** - Nom du protocole de connecteur utilisé pour l'exploration. La valeur à utiliser pour ce connecteur est `box`.
-   **`classname`** - Nom de classe Java du connecteur. Utilisez `plugin:box.plugin@connector` pour ce connecteur.
-   **`logging-config`** - Spécifie le fichier utilisé pour configurer les options de consignation ; il doit être formaté sous forme de chaîne XML `log4j`.
-   **`box-crawl-seed-url`** - Adresse URL de base pour Box. La valeur de ce connecteur est `box://app.box.com/`.

    Vous pouvez explorer différents types d'adresse URL. Par exemple :

    -   Pour explorer l'ensemble d'une entreprise : `box://app.box.com/`
    -   Pour explorer un dossier spécifique : `box://app.box.com/user/USER_ID/folder/FOLDER_ID/FolderName`
    -   Pour explorer un utilisateur spécifique : `box://app.box.com/user/USER_ID/`
-   **`client-id`** - Entrez l'ID client fourni par Box lorsque vous avez créé votre application Box.
-   **`client-secret`** - Entrez le secret client fourni par Box lorsque vous avez créé votre application Box.
-   **`path-to-private-key`** - Emplacement sur votre système de fichiers local de la clé privée qui fait partie de la paire de clés privée/publique générée pour les communications avec Box.
-   **`kid`** - Spécifie l'ID clé publique. Il s'agit de l'autre moitié de la paire de clés publiques-privées générée pour la communication avec Box.
-   **`enterprise-id`** - Entreprise dans laquelle votre application était autorisée. L'ID entreprise est indiqué dans la page principale de la console d'administrateur Box.
-   **`enable-acl`** - Usage interne uniquement. Permet d'extraire les listes de contrôle d'accès des données explorées.
-   **`user-agent`** - En-tête envoyé au serveur lors de l'exploration de documents.
-   **`method`** - Méthode (`GET` ou `POST`) par laquelle les paramètres seront transmis.
-   **`url-logging`** - Mesure dans laquelle les adresses URL explorées sont consignées. Les valeurs possibles sont les suivantes :

    -   `full-logging` - Permet de consigner toutes les informations relatives à l'URL.
    -   `refined-logging` - Permet de consigner uniquement les informations nécessaires pour parcourir le journal de moteur d'exploration et pour que le connecteur puisse fonctionner correctement. Il s'agit de la valeur par défaut.
    -   `minimal-logging` - Permet de consigner uniquement la quantité minimale d'informations nécessaires pour que le connecteur puisse fonctionner correctement.

    Si vous choisissez la valeur `minimal-logging` pour cette option, la taille des journaux est réduite et les performances sont légèrement améliorées en raison de la moindre quantité d'E/S associée à la minimisation de la quantité de données consignées.
-   **`ssl-version`** - Permet de spécifier une version de SSL à utiliser pour les connexions HTTPS. Par défaut, le protocole le plus fort disponible est utilisé.

### Configuration de la valeur de départ d'exploration Box
{: #box-crawl-options}

Les valeurs supplémentaires ci-après peuvent être configurées pour le fichier de départ d'exploration Box. Pour définir ces valeurs, ouvrez le fichier `config/seeds/box-seed.conf` et spécifiez les valeurs suivantes, propres à vos cas d'utilisation :

-   **`url`** - Adresse URL à utiliser comme point de départ de l'exploration. La valeur par défaut est `box://app.box.com/`.
-   **`default-allow`** - Usage interne uniquement.

## Limitations

Le connecteur Box possède certaines limitations :

-   Les commentaires et les tâches sur les fichiers ne sont pas extraits.
-   Le corps du contenu des notes est extrait au format JSON. Une conversion supplémentaire des données Notes peut s'avérer nécessaire.
-   Les documents individuels ne peuvent pas être extraits via Test-It. Seules les adresses URL de départ, les adresses URL de dossier et les adresses URL d'utilisateur peuvent être extraites via Test-It.
