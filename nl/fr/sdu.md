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
{:gif: data-image-type='gif'}

# Smart Document Understanding
{: #sdu}

Smart Document Understanding (SDU) constitue une nouvelle façon d'entraîner {{site.data.keyword.discoveryfull}} à extraire des zones personnalisées dans vos documents. Personnaliser la façon dont vos documents sont indexés dans {{site.data.keyword.discoveryshort}} va améliorer les réponses renvoyées par votre application.

Avec SDU, vous annotez les zones dans vos documents afin d'entraîner des modèles de conversion personnalisés. Lors de l'annotation, Watson apprend et commence à prévoir des annotations. Les modèles SDU peuvent être exportés et utilisés dans d'autres collections. 

## Navigateurs et types de document pris en charge
{: #doctypes}

Types de document pris en charge pour Smart Document Understanding : 
-  Plans Lite : PDF, Word, PowerPoint, Excel, JSON\*, HTML\*
-  Plans Advanced : PDF, Word, PowerPoint, Excel, PNG\*\*, TIFF\*\*, JPG\*\*, JSON\*, HTML\* 

\* Les documents JSON et HTML sont pris en charge par {{site.data.keyword.discoveryfull}} mais ne peuvent pas être modifiés à l'aide de l'éditeur SDU. Pour changer la configuration des documents HTML et JSON, vous devez utiliser l'API. Pour plus d'informations, voir la page de [référence d'API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery/){: new_window}.

\*\* Les fichiers individuels (PNG, TIFF, JPG) sont analysés et le texte (le cas échéant) est extrait. Les images PNG, TIFF et JPEG intégrées dans les fichiers PDF, Word, PowerPoint et Excel sont également analysés et le texte (le cas échéant) est extrait.

Navigateurs pris en charge : Chrome et Firefox.

## Utilisation de l'éditeur Smart Document Understanding
{: #annotate}

L'éditeur SDU est disponible uniquement pour les nouvelles collections qui contiennent des types de document pris en charge et auxquelles l'enrichissement Element Classification n'est pas appliqué. Les collections privées existantes utilisent la méthode de configuration d'origine. Si vous souhaitez utiliser l'éditeur SDU sur une collection existante, vous devez créer une collection et télécharger ces documents dans cette dernière. Si vous ne souhaitez pas utiliser l'éditeur SDU, vous pouvez définir votre configuration en utilisant l'API. Pour plus d'informations, voir la page de [référence d'API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery/){: new_window}.
{: important}

Les fonctions de l'éditeur SDU sont disponibles uniquement dans les outils {{site.data.keyword.discoveryshort}}, elles ne sont pas disponibles dans l'API.
{: note}

Navigation dans l'éditeur Smart Document Understanding :

Si vous n'avez pas encore créé d'environnement et d'instance {{site.data.keyword.discoveryshort}}, consultez la page [Initiation](/docs/services/discovery?topic=discovery-getting-started#getting-started) pour obtenir des instructions.
{: tip}

1. Sur l'écran **Manage Data**, cliquez sur le bouton **Upload your own data** et créez une nouvelle collection privée dans {{site.data.keyword.discoveryshort}}.
1. Si vous le souhaitez, faites glisser les documents dans votre collection ou cliquez sur l'option de téléchargement à partir de l'ordinateur**** pour télécharger des documents. Une fois le téléchargement terminé, les informations suivantes s'affichent :
   -  Les zones identifiées dans vos documents.
   -  Les enrichissements appliqués à vos documents. Les enrichissements Entity Extraction, Sentiment Analysis, Category Classification et Concept Tagging sont automatiquement appliqués à la zone `text` par {{site.data.keyword.discoveryshort}} (sauf si vous importez des documents en utilisant un connecteur). Vous pouvez ajouter (ou retirer) des enrichissements supplémentaires dans la zone `text`.
   -  Des requêtes pré-générées que vous pouvez exécuter immédiatement.
1. Cliquez sur **Configure data** dans la partie supérieure droite. 
1. Sur l'écran **Configure data**, trois onglets sont disponibles : **Identify fields**, **Manage fields** et **Enrich fields**.

   - L'onglet **Identify fields** contient l'éditeur SDU. Cet onglet remplace les onglets **Convert** et **Normalize** de votre écran {{site.data.keyword.discoveryshort}} d'origine. 
   - L'onglet **Manage fields** répertorie toutes les zones indexées (toutes les zones sont indexées par défaut). Désactivez les zones que vous ne souhaitez pas indexer. Par exemple, vos fichiers PDF peuvent inclure un en-tête ou un pied de page qui ne contient pas d'informations utiles, vous pouvez donc exclure ces zones de l'index. Vous pouvez également fractionner les documents ici, en fonction des zones. Pour plus d'informations, voir [Fractionnement de documents](/docs/services/discovery?topic=discovery-sdu#splitting).
   - **Enrich fields** est identique à l'onglet **Enrich** de l'écran d'origine. Pour plus d'informations sur les enrichissements, voir [Ajout d'enrichissements](/docs/services/discovery?topic=discovery-configservice#adding-enrichments). L'option **Upload sample documents** n'est pas disponible avec les collections SDU.

   Si vous n'avez pas téléchargé de documents auparavant, accédez à nouveau à l'écran **Overview** en cliquant sur le nom de votre collection dans la partie supérieure gauche ou cliquez sur l'icône ![Manage Data](/images/icon_yourData.png) et choisissez votre collection. Faites glisser vos documents dans votre collection ou cliquez sur l'option de téléchargement à partir de l'ordinateur****. Une fois que vous avez effectué un téléchargement initial, le bouton **Upload documents** s'affiche dans la partie supérieure droite de la fenêtre.
   {: important}

   Lors de l'utilisation de Smart Document Understanding, seule la zone `text` peut être enrichie. Ne tentez pas d'enrichir d'autres zones.
   {: important}

1. Ouvrez l'onglet **Identify fields**. Jusqu'à vingt (20) documents de votre collection sont automatiquement chargés dans l'éditeur Smart Document Understanding.

La barre d'outils située en haut permet d'effectuer les actions suivantes :
- Choisir un document à annoter
- Accéder au document affiché
- Ajuster la vue de page (`single page view`, `zoom in`, `zoom out`), `clear changes` et `export/import models`. Cliquez sur `single page view` pour changer l'affichage. Vous pouvez afficher vos annotations et vos documents ensemble ou séparément.

Vous pouvez également explorer les sources de données Box, Salesforce, Microsoft SharePoint Online, IBM Cloud Object Storage et Microsoft SharePoint 2016 ou effectuer une exploration Web avec les outils {{site.data.keyword.discoveryshort}}. Cliquez sur le bouton **Connect a data source** et consultez [Connexion à des sources de données](/docs/services/discovery?topic=discovery-sources#sources) pour plus d'informations. Si vous créez une collection en utilisant cette méthode, aucun enrichissement ne sera automatiquement appliqué.
{: tip}

## Mode d'annotation d'un document
{: #documents}

**Remarque :** Les tables sont annotées au cours d'une étape distincte.

Voir [Meilleures pratiques pour annoter des documents et des tables](/docs/services/discovery?topic=discovery-sdu#bestpractices) avant de commencer à annoter.

1. Un ensemble de zones par défaut apparaît à droite de votre document. Zones disponibles : `answer`, `author`, `footer`, `header`, `question`, `subtitle`, `table_of_contents`, `text` et `title`. Si vous souhaitez créer un ou plusieurs nouveaux libellés de zone personnalisés, cliquez sur **Create new**. Le nombre de libellés personnalisés est limité en fonction du type de plan (Plans Lite - `0`, plans Advanced - `5`, plans Premium - `20`).
1. Cliquez sur un libellé de zone à droite pour activer la zone.
1. Cliquez sur le contenu représentant cette zone dans l'éditeur SDU. Le contenu est alors mis en évidence. 
   - Vous pouvez également sélectionner un libellé de zone sur la droite, puis le faire glisser vers le contenu dans l'éditeur SDU. 
   - Pour effacer une modification, cliquez sur le bouton **Clear change** dans la barre d'outils.
1. Cliquez sur **Submit**.
   **Remarque :** Lorsque vous annotez, Watson apprend et commence à prévoir des annotations. Continuez vos annotations jusqu'à ce que Watson identifie les zones correctement et de manière cohérente.
1. Lorsque vous avez fini d'annoter, cliquez sur **Apply changes to collection**. L'écran **Upload your documents** s'affiche. Téléchargez à nouveau les documents dans votre collection. Une fois le téléchargement terminé, vous êtes redirigé vers l'écran **Manage Data**.

Zone | Définition  
------ | ------ 
answer | Dans une paire Q/R (souvent dans une FAQ), la réponse à la question.
author | Nom de l'auteur (ou des auteurs).
footer | Utilisez cette balise pour désigner les méta-informations relatives au document (numéro de page ou références, par exemple), qui apparaissent au bas de la page.
header | Utilisez cette balise pour désigner les méta-informations relatives au document qui apparaissent en haut de la page.
question | Dans une paire Q/R (souvent dans une FAQ), la question.
subtitle | Titre secondaire du document en cours d'annotation. 
table_of_contents | Utilisez cette balise sur les listes de la table des matières du document.
text | Utilisez cette balise pour le texte classique, incluant les paragraphes, définitions, ou tout ensemble de mots qui ne constitue pas un titre, une partie de table, réponse, sous-titre, en-tête ou pied de page. 
title | Titre principal du document en cours d'annotation.

## Mode d'annotation d'une table
{: #tables}

L'annotation de table est en version bêta. Une instruction décrivant les fonctions bêta est disponible [ici](/docs/services/discovery?topic=discovery-release-notes#beta-features).
{: important}

Voir [Meilleures pratiques pour libeller des documents et des tables](/docs/services/discovery?topic=discovery-sdu#bestpractices) avant de commencer à annoter.

1. Sélectionnez la zone `table` sur le côté droit de l'éditeur SDU puis sélectionnez la table dans le document. 
1. Survolez la table pour afficher le bouton **Annotate table**. Cliquez sur le bouton pour ouvrir l'éditeur de table.
1. Pour commencer, délimitez la table :
   - Sélectionnez la zone `column`.
   - Cliquez sur une colonne de la table pour l'activer.
   - Sélectionnez la zone `row`.
   - Cliquez sur une ligne de la table pour l'activer.

   Le contour de la table apparaît dans l'aperçu sur la gauche.

   **Remarque :** Lorsque vous annotez des tables, Watson apprend et commence à prévoir des annotations.
1. Libellez ensuite le contenu de la table.
1. Quand vous avez fini d'annoter la table, cliquez sur **Done annotating**.
1. Cliquez sur **Apply changes to collection**. L'écran **Upload your documents** s'affiche. Téléchargez à nouveau les documents dans votre collection. Une fois le téléchargement terminé, vous êtes redirigé vers l'écran **Manage Data**.

Utilisez cette vidéo en tant que guide ![vidéo d'annotation de table](images/SDU_table_demo.gif){: gif}

Zone | Définition  
------ | ------ 
body | Toute cellule autre que d'en-tête qui contient des informations
column header | Cellule d'en-tête (le cas échéant) pour chaque colonne de la table 
multi-column header | Toute cellule d'en-tête qui s'étend sur plusieurs colonnes
row title | En-tête de la colonne des en-têtes de ligne (le cas échéant)
row header | Libellé de ligne (le cas échéant) pour chaque ligne de la table
multi-row header | Tout libellé de ligne s'étendant sur plusieurs lignes

## Fractionnement de documents
{: #splitting}

L'onglet **Manage fields** contient l'option **Improve query results by splitting your documents**. Cette option vous permet de fractionner vos documents dans des segments en fonction d'un nom de zone. Une fois le fractionnement effectué, chaque segment constitue un document distinct qui sera enrichi, indexé et renvoyé en tant que résultat de requête séparé. 

Les documents sont fractionnés en fonction d'un nom de zone unique, par exemple `title`, `author` et `question`. 

Remarques :

  - Le nombre de segments par document est limité à `250`. Tout contenu de document dépassant `249` segments sera stocké dans le segment `250`.

  - Chaque segment est pris en compte pour la limite de document de votre plan. {{site.data.keyword.discoveryshort}} indexe les segments jusqu'à ce que la limite du plan soit atteinte. Voir [Plans de tarification Discovery](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans) pour connaître les limites de documents.

  - Les métadonnées PDF et Word, ainsi que les métadonnées personnalisées, sont extraites et incluses dans l'index avec chaque segment. Chaque segment d'un document inclut des métadonnées identiques.

  - Si un document fractionné a été mis à jour et doit être chargé à nouveau, remplacez-le en utilisant la méthode de [mise à jour de document ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery#update-a-document){: new_window}. Le document doit être téléchargé en utilisant la méthode POST de l'API `/environments/{environment_id}/collections/{collection_id}/documents/{document_id}`, en spécifiant le contenu de la zone `parent_id` de l'un des segments actuels comme variable de chemin `{document_id}`. Tous les segments sont remplacés, sauf si la version mise à jour du document comporte moins de sections que la version d'origine. Les segments plus anciens restent dans l'index et peuvent être supprimés individuellement à l'aide de l'API. Pour plus d'informations, voir la page de [référence d'API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery#delete-a-document){: new_window}. 

## Importation et exportation de modèles
{: #import}

Une fois que vous avez défini un modèle avec l'éditeur SDU, vous pouvez le sauvegarder et le réutiliser dans d'autres collections.

Vous pouvez importer ou exporter votre modèle SDU terminé en utilisant la barre d'outils se trouvant dans la partie supérieure de l'éditeur. Cliquez sur la dernière icône et sélectionnez `Import model` ou `Export model`.

Les modèles exportés ont l'extension de fichier `.sdumodel`. 

Un modèle importé est conçu pour être utilisé avec des annotations supplémentaires. Le modèle sera entièrement écrasé si vous continuez de l'annoter après l'avoir importé. Si vous planifiez d'importer un modèle dans une nouvelle collection, il est recommandé de créer une nouvelle collection qui contient un seul document, d'importer le modèle puis de télécharger le reste de vos documents.

## Meilleures pratiques pour annoter des documents et des tables
{: #bestpractices}

L'annotation de table est en version bêta. Une instruction décrivant les fonctions bêta est disponible [ici](/docs/services/discovery?topic=discovery-release-notes#beta-features).
{: important}

- Suivez toutes les instructions et utilisez un étiquetage cohérent sur l'ensemble des documents.
- Ne libellez pas de blanc.
- Utilisez les libellés `image` sur les images et les diagrammes
- Ne traitez pas différemment du texte en **gras**, _italique_ ou souligné. Le libellé dépend du contexte et non du style. 
- Lorsque vous libellez un document, allez de la première page à la dernière.
- Si vous avez libellé un élément de manière incorrecte, choisissez un autre libellé pour remplacer le premier.
- Les pages peuvent être soumises à tout moment. Assurez-vous que l'étiquetage approprié est terminé avant de soumettre.
- Documents et tables dans lesquels du texte chevauche un autre texte sont considérés comme “à double couche” et ne peuvent pas être annotés. Signalez ces documents à votre administrateur.
- Documents et tables comportant plusieurs colonnes de texte sur une seule page ne peuvent pas être annotés. Signalez ces documents à votre administrateur.
- Les notes de bas de page doivent être libellées uniquement lorsqu'elles figurent au bas de la page et sont référencées dans le corps de texte principal du document.
- Les notes/remarques figurant dans des sections ou des listes (c'est-à-dire explicitement appelées notes ou remarques), doivent être libellées `text`.
- Si vous n'êtes pas certain que la table a été correctement libellée et si le panneau de prévisualisation ne répond pas, la page doit être rechargée dans votre navigateur et la table re-libellée afin de garantir son exactitude.

