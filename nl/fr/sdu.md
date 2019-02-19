---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-10"

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

# Smart Document Understanding

Smart Document Understanding (SDU, ou la "vision intelligente des documents") est une nouvelle façon d'annoter vos documents dans {{site.data.keyword.discoveryfull}}. 

L'éditeur simplifie l'apprentissage des modèles de conversion personnalisés. Personnaliser la façon dont vos documents sont indexés dans Discovery va améliorer les réponses renvoyées pour votre application.

SDU est une version bêta. Une instruction décrivant les fonctions bêta est disponible [ici](/docs/services/discovery/release-notes.html#beta-features).

## Navigateurs et types de document pris en charge
{: #doctypes}

Types de document pris en charge : PDF, Word, HTML. Les documents JSON sont pris en charge par {{site.data.keyword.discoveryfull}} mais ne s'ouvrent pas dans l'éditeur SDU car il s'agit de documents structurés. 

Navigateurs pris en charge pour cette version bêta : Chrome et Firefox

## Comment annoter vos documents
{: #annotate}

Pour ouvrir l'éditeur Smart Document Understanding :

1. Ouvrez {{site.data.keyword.discoveryfull}} à l'aide du lien bêta.
1. Ouvrez une collection de données privée, et dans l'écran **Manage Data**, cliquez sur **Go to Data Settings**. 
1. L'écran **Data Settings** comporte deux onglets : **Extract fields** et **Enrich fields**.

   - **Extract fields** contient l'éditeur SDU. Cet onglet remplace les onglets **Convert** et **Normalize** de votre écran {{site.data.keyword.discoveryshort}} d'origine. 
   - **Enrich fields** est identique à l'onglet **Enrich** de l'écran d'origine. Pour plus d'informations sur les enrichissements, voir [Ajout d'enrichissements](/docs/services/discovery/building.html#adding-enrichments). L'option **Upload sample documents** n'est pas disponible dans l'onglet **Enrich fields** car il n'est pas nécessaire.

1. Vingt (20) documents de votre collection sont automatiquement chargés sous l'onglet **Extract fields**, dans l'éditeur Smart Document Understanding.

La barre d'outils située en haut permet de : 
- Sélectionner un document
- Accéder au document affiché
- Ajuster la vue de page (`single page view`, `zoom in`, `zoom out`), `clear changes` et `export/import models`. Cliquez sur `single page view` pour basculer vers un écran affichant séparément vos annotations et votre document.  

### Annotation d'un document dans l'éditeur SDU 
{: #documents}

**Remarque :** Les tables sont annotées au cours d'une étape distincte.

Voir [Meilleures pratiques pour libeller des documents et tables](/docs/services/discovery/sdu.html#bestpractices) avant de commencer à annoter. 

1. Un ensemble de zones par défaut apparaît à droite de votre document. (Pour la version bêta, vous ne pouvez pas créer de zone de personnalisation, mais cette fonction sera disponible ultérieurement.) Zones disponibles : `answer`, `author`, `footer`, `header`, `question`, `subtitle`, `table_of_contents`, `text` et `title`.
1. Cliquez sur un nom de zone à droite pour activer la zone. 
1. Cliquez sur le contenu représentant cette zone dans l'éditeur SDU. Le contenu est mis en évidence. 
   - Ou bien, vous pouvez sélectionner un nom de zone sur la droite, puis le faire glisser vers le contenu dans l'éditeur SDU. 
   - Pour effacer une modification, cliquez sur le bouton **Clear change** dans la barre d'outils.
1. Cliquez sur **Submit**.
   **Remarque :** Lorsque vous annotez, Watson apprend et commence à prévoir des annotations. Continuez vos annotations jusqu'à ce que Watson identifie les zones correctement et de manière cohérente. 
1. Lorsque vous avez fini d'annoter, cliquez sur **Apply changes to collection**. L'écran **Upload your documents** s'affiche. (Ce comportement sera modifié après la version bêta.) Vous pouvez à présent télécharger vos documents afin que les paramètres mis à jour soient appliqués à la totalité de la collection. Une fois le téléchargement terminé, vous êtes redirigé vers l'écran **Manage Data**.


Zone | Définition  
------ | ------ 
answer | Dans une paire Q/R (souvent dans une FAQ), la réponse à la question.
author | Nom de l'auteur (ou des auteurs). 
footer | Utilisez cette balise pour désigner les méta-informations relatives au document (numéro de page ou références, par exemple), qui apparaissent au bas de la page.
header | Utilisez cette balise pour désigner les méta-informations relatives au document qui apparaissent en haut de la page.
question | Dans une paire Q/R (souvent dans une FAQ), la question.
subtitle | Titre secondaire du document en cours d'annotation. Utilisez ce libellé une seule fois par document.
table-of-contents | Utilisez cette balise sur les listes de la table des matières du document.
text | Utilisez cette balise pour le texte classique, incluant les paragraphes, définitions, ou tout ensemble de mots qui ne constitue pas un titre, une partie de table, réponse, sous-titre, en-tête ou pied de page. 
title | Titre principal du document en cours d'annotation. Utilisez ce libellé une seule fois par document.

### Annotation d'une table dans l'éditeur SDU 
{: #tables} 

1. Sélectionnez la zone `table` sur la droite, puis sélectionnez la table dans l'éditeur SDU. 
1. Survolez la table dans l'éditeur SDU pour afficher le bouton **Annotate table**. Cliquez sur le bouton pour ouvrir l'éditeur de table.
1. Pour commencer, délimitez la table :
   - Sélectionnez la zone `column`.
   - Cliquez sur une colonne de la table pour l'activer.
   - Sélectionnez la zone `row`.
   - Cliquez sur une ligne de la table pour l'activer.

   Le contour de la table apparaît dans l'aperçu sur la gauche. 

   **Remarque :** Vous pouvez cliquer sur **Predict** pour afficher une prévision du modèle de votre annotation de table.
1. Libellez ensuite le contenu de la table.
1. Quand vous avez fini d'annoter la table, cliquez sur **Done annotating**.
1. Cliquez sur **Apply changes to collection**. L'écran **Upload your documents** s'affiche. (Ce comportement sera modifié après la version bêta.) Une fois le téléchargement terminé, vous êtes redirigé vers l'écran **Manage Data**.

Zone | Définition  
------ | ------ 
table body | Toute cellule autre que d'en-tête qui contient des informations
column header | Cellule d'en-tête (le cas échéant) pour chaque colonne de la table 
multi-column header | Toute cellule d'en-tête qui s'étend sur plusieurs colonnes 
subsection title | En-tête de la colonne des en-têtes de ligne (le cas échéant)
row header | Libellé de ligne (le cas échéant) pour chaque ligne de la table
multi-row header | Tout libellé de ligne s'étendant sur plusieurs lignes

## Meilleures pratiques pour libeller des documents et tables
{: #bestpractices}

- Suivez toutes les instructions et utilisez un étiquetage cohérent sur l'ensemble des documents.
- Ne libellez pas de blanc.
- Ne libellez pas de diagramme ou d'image.
- Ne traitez pas du texte en **gras**, _italique_ ou souligné différemment, les libellés sont basés sur le contexte et non sur le style. 
- Lorsque vous libellez un document, allez de la première page à la dernière. Chaque page doit être soumise, même si vous n'avez pas indiqué de libellé. 
- Si vous avez libellé un élément de manière incorrecte, choisissez un autre libellé pour remplacer le premier.
- Les pages peuvent être soumises à tout moment. Assurez-vous que l'étiquetage approprié est terminé avant de soumettre.
- N'utilisez pas la fonction de zoom sur votre navigateur lorsque vous libellez des documents.
- Documents et tables dans lesquels du texte chevauche un autre texte sont considérés comme “à double couche” et ne peuvent pas être annotés. Signalez ces documents à votre administrateur.
- Documents et tables comportant plusieurs colonnes de texte sur une seule page ne peuvent pas être annotés. Signalez ces documents à votre administrateur.
- Les notes de bas de page doivent être marquées comme tel uniquement lorsqu'elles figurent au bas de la page et sont référencées dans le corps de texte principal du document.
- Les notes/remarques figurant dans des sections ou des listes (c'est-à-dire explicitement appelées notes ou remarques), doivent être libellées `text`.
- Si vous n'êtes pas certain que la table a été correctement libellée et si le panneau de prévisualisation ne répond pas, la page doit être rechargée dans votre navigateur et la table re-libellée afin de garantir son exactitude.

