---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-02-08"

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

# Initiation
{: #getting-started}

Dans ce bref tutoriel, nous allons vous présenter les outils {{site.data.keyword.discoveryshort}} et vous montrer comment créer une collection de données privées et comment effectuer des recherches dans cette dernière.
{: shortdesc}

Si vous préférez travailler dans l'API, voir [Initiation à l'API](/docs/services/discovery?topic=discovery-gs-api#gs-api).
{: tip}

## Avant de commencer
{: #before-you-begin-tool}
{: hide-dashboard}

Vous avez besoin d'une instance de service pour commencer.
{: hide-dashboard}

1.  {: hide-dashboard}Accédez à la page [{{site.data.keyword.discoveryshort}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/catalog/services/discovery) du catalogue {{site.data.keyword.cloud_notm}}.

    Si vous ne choisissez pas de groupe de ressources, l'instance de service est créée dans le groupe **default**. Vous ne pourrez plus en changer** ultérieurement. Ce groupe est suffisant lorsque vous essayez le service.

    Si vous créez une instance pour une utilisation plus avancée, consultez les informations présentant les [groupes de ressources ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/docs/resources/bestpractice_rgs.html#bp_resourcegroups){: new_window}.
1.  {: hide-dashboard} Inscrivez-vous pour un compte {{site.data.keyword.cloud_notm}} gratuite ou connectez-vous.
1.  {: hide-dashboard} Cliquez sur **Create**.

## Etape 1 : Lancement des outils
{: #launch-the-tooling}

Une fois que vous avez créé une instance du service {{site.data.keyword.discoveryshort}}, la liste de vos services s'affiche.
{: hide-dashboard}

1.  {: hide-dashboard} Cliquez sur l'instance de service {{site.data.keyword.discoveryshort}} que vous avez créée pour accéder au tableau de bord du service.
1.  Sur la page **Manage**, cliquez sur **Launch tool**. Si vous êtes invité à vous connecter aux outils, entrez vos données d'identification {{site.data.keyword.cloud_notm}}.

<!-- To do: Add screenshot for developer console -->

## Etape 2 : Création d'une collection
{: #create-a-collection-tool}

Votre première étape dans les outils {{site.data.keyword.discoveryshort}} consiste à créer une collection de données.

Une collection regroupe certains de vos documents. *Pourquoi devrais-je avoir besoin de plusieurs collections ?* Il existe plusieurs raisons :

- Vous pouvez être amené à vouloir posséder plusieurs collections afin de séparer les résultats pour différents publics.
- Il peut arriver que les données soient très différentes, et dans ce cas, il ne serait pas logique qu'elles soient toutes ciblées par une requête.

Vous pouvez également utiliser la collection de données {{site.data.keyword.discoverynewsshort}} préenrichie publique qui est à votre disposition. Elle est prête à faire l'objet d'une requête et vous pouvez dès maintenant commencer à l'utiliser comme cible pour vos requêtes. Vous ne pouvez pas ajuster sa configuration ni ajouter de documents à{{site.data.keyword.discoverynewsshort}}.

1.  Cliquez sur ![Environment details](images/env_icon.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> et choisissez **Create environment**.
1.  Lorsque votre environnement est prêt, cliquez sur le bouton **Upload your own data**, puis vous pouvez donner un nom à votre nouvelle collection (**Name your new collection**). Nommez votre collection **InstallDocs**.

    Lors de la création d'une collection, sous **Advanced**, vous avez la possibilité de choisir un fichier de configuration nommé **Default Contract Configuration**. Cette configuration prend en charge uniquement l'enrichissement Element Classification, qui peut être utilisé pour extraire la partie prenante, la nature et la catégorie d'éléments dans des fichiers PDF. Voir [Element Classification](/docs/services/discovery?topic=discovery-element-classification#element-collection) pour plus de détails. Ne choisissez pas cette option pour ce tutoriel.

Vous pouvez également explorer les sources de données Box, Salesforce, Microsoft SharePoint Online, IBM Cloud Object Storage et Microsoft SharePoint 2016 ou effectuer une exploration Web avec les outils {{site.data.keyword.discoveryshort}}. Cliquez sur le bouton **Connect a data source** et consultez [Connexion à des sources de données](/docs/services/discovery?topic=discovery-sources#sources) pour plus d'informations.
{: tip}

## Etape 3 : Téléchargement du document exemple et envoi par téléchargement dans votre collection
{: create-custom-configuration}

1.  Téléchargez ce document PDF exemple : <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/watsonexplorerinstall.pdf" download>Watson Explorer Installation Guide <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe"></a>. Pour obtenir la liste complète des types de document pris en charge dans {{site.data.keyword.discoveryshort}}, voir [Supported document types](/docs/services/discovery?topic=discovery-sdu#doctypes). 

    Dans certains navigateurs, les liens s'ouvrent dans une nouvelle fenêtre au lieu d'être sauvegardés localement. Dans ce cas, sélectionnez `Save As` dans le menu `File` de votre navigateur pour sauvegarder une copie du fichier.
    {: tip}

1.  Téléchargez le document dans votre collection. Faites-le glisser dans votre collection ou cliquez sur l'option de téléchargement à partir de l'ordinateur**** pour télécharger des documents. Une fois le téléchargement terminé, les informations suivantes s'affichent :
    -  Nombre de documents (1).
    -  Zones identifiées à partir de votre document. Vous devez voir une zone identifiée, `text`. Nous allons identifier les zones supplémentaires dans quelques instants.
    -  Enrichissements appliqués à votre document. Les enrichissements Entity Extraction, Sentiment Analysis, Category Classification et Concept Tagging sont automatiquement appliqués à la zone `text` par {{site.data.keyword.discoveryshort}}. Pour plus d'informations sur les enrichissements, cliquez [ici](/docs/services/discovery?topic=discovery-configservice#adding-enrichments). 
    -  Des requêtes pré-générées que vous pouvez exécuter immédiatement.
1.  Créons rapidement une requête en langage naturel ! Cliquez sur **Build your own query** dans la partie inférieure droite.
1.  Sur l'écran **Build queries**, cliquez sur **Search for documents** puis sur **Use natural language**. Entrez `What are the minimum hardware requirements` puis cliquez sur le bouton **Run query**. Cliquez sur l'onglet **JSON** sur le côté droit. Le résultat n'est pas aussi précis qu'il pourrait l'être. Améliorons-le en utilisant Smart Document Understanding.
1.  Cliquez sur le nom de la collection (**InstallDocs**) dans la partie supérieure gauche pour accéder à nouveau à l'écran **Overview**.  
 
## Etape 4 : Annotation de votre document
{: #upload-your-documents}

Pour plus d'informations sur l'annotation de documents, voir [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu).
{: tip}

1.  Cliquez sur **Configure data** dans la partie supérieure droite. 
1.  Sur l'écran **Configure data**, trois onglets sont disponibles : **Identify fields**, **Manage fields** et **Enrich fields**.
1.  Le document `Watson Explorer Installation Guide` s'affiche et est prêt à être annoté dans l'onglet **Identify fields**. Toutes les zones disponibles (`answer`, `author`, `footer`, `header`, `question`, `subtitle`, `table_of_contents`, `text` et `title`) s'affichent dans la liste **Field labels** sur la droite. Si vous achetez un plan Advanced ou Premium, vous pouvez créer vos propres étiquettes personnalisées.

    Etant donné que l'intégralité du document est actuellement identifiée en tant que `text`, les marqueurs sur le côté droit sont entièrement en jaune. Lors de l'annotation (début de la prédiction par le système), les couleurs sont mises à jour.
    {: tip}

1.  Cliquez sur `title`, puis sélectionnez le marqueur en regard de l'élément `Installation and Integration Guide`. Cliquez sur le bouton **Submit page**.
1.  Dans l'aperçu, cliquez sur la page 3. Notez que l'élément `title` a déjà été prédit pour cette page. Cliquez sur le bouton **Submit page**.
1.  Sur la page 4, sélectionnez l'étiquette `footer` puis sélectionnez le marqueur en regard du pied de page. Cliquez sur le bouton **Submit page**.
1.  Sur les pages 5 et 6, annotez les pieds de page avec l'étiquette `footer`. Soumettez chaque page. Parcourez quelques pages supplémentaires, vous verrez alors que le pied de page a été correctement prévu par {{site.data.keyword.discoveryshort}}. Annotez les éléments `title` (justification à gauche) et `subtitle` (mise en retrait) sur les pages 7, 9 et 10 et soumettez chaque page individuellement.
1.  Parcourez quelques pages supplémentaires et vérifiez les titres et les sous-titres prévus. S'il est nécessaire de modifier des éléments, annotez ces pages puis cliquez sur le bouton **Submit page**.
1.  Cliquez maintenant dans l'onglet **Manage fields** puis sous **Improve query results by splitting your documents**, fractionnez le document en fonction de l'élément `subtitle`. 
1.  Les annotations devraient désormais être suffisantes. Cliquez sur le bouton **Apply changes to collection** dans la partie supérieure droite. Une boîte de dialogue **Upload your documents** s'affiche. Recherchez le fichier `watsonexplorerinstall.pdf` d'origine et téléchargez-le. Cette opération doit être effectuée pour toutes les annotation de votre index. Une fois l'indexation terminée, l'écran **Overview** s'affiche. Vous devez voir actuellement 30 documents ou plus et quatre zones identifiées dans vos données : `footer`, `subtitle`, `text` et `title`. (Si les modifications ne s'affichent pas après quelques minutes, actualisez la fenêtre du navigateur.)

    Vous pouvez exclure des zones (`footer`, par exemple) de l'indexation en ouvrant l'onglet **Manage fields** et en choisissant l'option `off` pour cette zone.
    {: tip}

## Etape 5 : Création d'une requête
{: #build-a-query}

1.  Cliquez sur **Build your own query** dans la partie inférieure droite.
1.  Sur l'écran **Build queries**, cliquez sur **Search for documents** puis sur **Use natural language**. Entrez `What are the minimum hardware requirements` puis cliquez sur le bouton **Run query**. 
1.  Cliquez sur l'onglet **JSON** sur le côté droit. Consultez l'élément `text` sous `results`. Les réponses renvoyées pour cette requête sont beaucoup plus précises.

Ressources supplémentaires :
-  Pour en savoir plus sur le schéma de données de vos documents, cliquez sur l'icône **View Data Schema** dans la partie gauche ou sur l'onglet **JSON**. Pour plus de détails, voir [Schéma de données Discovery](/docs/services/discovery?topic=discovery-query-concepts#discovery-schema).
-  Cliquez sur le bouton **Use a sample query** pour tester les requêtes exemple créées avec {{site.data.keyword.discoveryshort}} Query Language.

## Etapes suivantes
{: #next-steps-tool}

Vous disposez à présent d'une instance de service {{site.data.keyword.discoveryshort}} opérationnelle et remplie. Vous pouvez à présent commencer à personnaliser votre collection en ajoutant d'autres documents et enrichissements et en annotant des documents supplémentaires. Pour plus d'informations, voir [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu).
