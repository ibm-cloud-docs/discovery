---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-03"

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

# Téléchargement et installation de Data Crawler

Data Crawler collecte les données brutes qui seront finalement utilisées pour constituer les résultats de recherche du service {{site.data.keyword.discoveryshort}}. Lors de l'exploration des référentiels de données, le moteur d'exploration télécharge des documents et des métadonnées en commençant par une adresse URL de départ spécifiée par l'utilisateur. Le moteur d'exploration découvre des documents dans une hiérarchie, ou liés à partir de l'adresse URL de départ, et les place en file d'attente en vue d'une extraction.
{: shortdesc}

Vous pouvez utiliser les outils ou l'API {{site.data.keyword.discoveryshort}} pour explorer des sources de données Box, Salesforce et Microsoft SharePoint Online. Voir [Connexion à des sources de données](/docs/services/discovery/connect.html) pour plus d'informations.
{: tip}

## Prérequis

-   Java Runtime Environment version 8 ou ultérieure

    Votre variable d'environnement `JAVA_HOME` doit être correctement définie, ou ne pas être définie du tout, pour que le moteur d'exploration puisse être exécuté.
    {: tip}
-   Red Hat Enterprise Linux 6 ou 7, ou Ubuntu Linux 15 ou 16. Pour obtenir des performances optimales, il est recommandé d'exécuter Data Crawler sur sa propre instance de Linux, qu'il s'agisse d'une machine virtuelle, d'un conteneur ou d'un matériel.

-   2 Go de mémoire vive au minimum sur le système Linux

## Télécharger et installer Data Crawler

1.  Ouvrez un navigateur et connectez-vous à votre compte [{{site.data.keyword.Bluemix}}![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.ng.bluemix.net){: new_window}.

1.  A partir de votre tableau de bord {{site.data.keyword.Bluemix_notm}}, sélectionnez le service {{site.data.keyword.discoveryshort}} que vous avez précédemment créé.

1.  A la section **Automate the upload of content to the Discovery service**,cliquez sur le lien approprié pour télécharger Data Crawler pour Linux aux formats DEB, RPM et ZIP.

1.  Assurez-vous que vous utilisez bien Java Runtime Environment version 8 ou ultérieure. Exécutez la commande `java -version` et recherchez **1.8**. Si vous utilisez une version antérieure à la version **1.8**, vous devez effectuer une mise à niveau de Java en installant le kit Java Development Kit (JDK) 8 à l'aide de votre système de gestion de packages, à partir du site Web [IBM JDK ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/developerworks/java/jdk/){: new_window} ou à partir de [java.com ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.java.com){: new_window}.

    Votre variable d'environnement `JAVA_HOME` doit être correctement définie, ou ne pas être définie du tout, pour que le moteur d'exploration puisse être exécuté.
    {: tip}

1.  En tant qu'administrateur, utilisez les commandes appropriées pour installer le fichier archive que vous avez téléchargé :

    -   Sur les systèmes, tels que Red Hat et CentOS, qui utilisent des packages rpm, utilisez une commande semblable à la suivante : `rpm -i /full/path/to/rpm/package/rpm-file-name`
    -   Sur les systèmes, tels que Ubuntu et Debian, qui utilisent des packages deb, utilisez une commande semblable à la suivante : `dpkg -i /full/path/to/deb/package/deb-file-name`
    -   Les scripts Crawler sont installés dans `{installation_directory}/bin` ; par exemple, `/opt/ibm/crawler/bin`. Assurez-vous que `{installation_directory}/bin` est défini dans votre variable d'environnement `PATH` pour que les commandes Crawler fonctionnent correctement.

    Les scripts Crawler sont également installés dans `/usr/local/bin`, par conséquent, cela peut aussi être ajouté à votre variable d'environnement `PATH`.
    {: tip}
1.  Créez votre répertoire de travail en copiant le contenu du répertoire `{installation_directory}/share/examples/config` dans un répertoire de travail sur votre système, par exemple, `/home/config`.

    **Avertissement :** vous ne devez pas modifier directement les exemples de fichier de configuration fournis. Vous devez les copier, puis les éditer. Si vous éditez les exemples de fichier internes, il se peut que votre configuration soit remplacée si vous mettez à niveau Data Crawler ou retirée si vous désinstallez Data Crawler.

    **Remarque :** les fichiers du répertoire `config` mentionnés dans le reste du guide, par exemple, `config/crawler.conf`, font référence aux fichiers de votre répertoire de travail et NON aux fichiers du répertoire `{installation_directory}/share/examples/config` installé.

1.  Vous êtes maintenant prêt à [configurer Data Crawler pour qu'il se connecte à votre référentiel](/docs/services/discovery/data-crawler-seeds.html).

## Structure de Data Crawler

Lors du téléchargement de Data Crawler, les dossiers suivants sont créés sur votre système :

-   `doc` - Contient des fichiers comportant des informations de copyright et de licence.
-   `bin` - Fichiers script permettant d'exécuter le moteur d'exploration.
-   `connectorFramework` - Les fichiers contenus dans ce répertoire vous permettent de communiquer avec vos données. Il peut s'agir de données internes à l'entreprise ou de données externes sur le Web ou dans le cloud.
-   `lib` - Fichiers de bibliothèque utilisés par le moteur d'exploration.
-   `share`
    -   `doc` - Fournit des fichiers de documentation HTML et Markdown.
    -   `examples/config` - Fichiers permettant d'indiquer au moteur d'exploration quels sont les fichiers à utiliser pour l'exploration, où envoyer la collection de fichiers explorés une fois l'exploration terminée, ainsi que d'autres options de gestion de l'exploration.
    -   `man` - Documentation intégrée au produit relative à Data Crawler.

## Limitations connues dans cette édition

-   Data Crawler peut se bloquer lors de l'exécution du connecteur de système de fichiers avec une adresse URL non valide ou manquante.
-   Configurez la valeur `urls_to_filter` dans le fichier `crawler.conf`, de sorte que toutes les URL ou expressions régulières contenues dans la liste blanche soient inclus dans une seule expression régulière. Pour plus d'informations, voir [Configuration des options d'exploration](/docs/services/discovery/data-crawler-discovery.html#configuring-crawl-options).
-   Le chemin d'accès au fichier de configuration transmis via l'option `--config -c` doit être un chemin qualifié, à savoir, au format de chemin d'accès relatif `config/crawler.conf` ou
`./crawler.conf` ou au format de chemin d'accès absolu `/path/to/config/crawler.conf`. Il est possible de spécifier uniquement `crawler.conf` si le fichier `orchestration_service.conf` est intégré au lieu d'être référencé à l'aide de `include` dans le fichier `crawler.conf`.
