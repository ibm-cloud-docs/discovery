---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-01-15"

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

# Element Classification
{: #element-classification}

L'enrichissement Element Classification permet d'effectuer rapidement une analyse syntaxique de documents constitutifs afin de convertir, d'identifier et de classifier des éléments importants. A l'aide de la technique de pointe de traitement automatique du langage naturel, la partie prenante (la personne référencée), la nature (type d'élément) et la catégorie (classe spécifique) sont extraites des éléments d'un document.

L'enrichissement Element Classification a été conçu pour :

-  La compréhension du langage naturel des contrats avec mise en évidence des contrats d'approvisionnement logiciel
-  La possibilité de convertir un PDF de programmation dans un format JSON annoté
-  L'identification d'entités et de catégories légales qui cadrent avec une expertise en la matière

Element Classification regroupe un ensemble fonctionnellement riche d'API Watson automatisées intégrées permettant d'entrer un PDF de programmation afin d'identifier des sections, des listes (numérotées et à puces), des notes de bas de page et des tables en convertissant ces éléments dans un format HTML structuré. De plus, la classification de ce format structuré est annotée et présentée sous la forme d'un document JSON avec des éléments, des types et des catégories libellés.

Element Classification transmet vos données de manière sécurisée en effectuant un chiffrement en cours et au repos. Pour des informations sur la sécurité IBM Cloud, voir la [description du service {{site.data.keyword.Bluemix_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=%28IBM+Cloud+Service+description%29){: new_window}

Element Classification renvoie un objet JSON qui contient :

-  Un objet `documents` incluant le titre du document d'entrée, une version HTML du document d'entrée, ainsi que le hachage MD5 du document d'entrée.
-  Des informations sur le modèle utilisé pour classifier le document d'entrée.  
-  Un tableau `elements` qui détaille les éléments sémantiques identifiés dans le document d'entrée.
-  Un tableau `tables` qui fractionne les tables identifiées dans le document d'entrée.
-  Un objet `document_structure` qui répertorie les titres de section et les phrases initiales identifiés dans le document d'entré.
-  Un tableau `parties` qui répertorie les parties prenantes, rôles, adresses et contacts des parties identifiées dans le document d'entrée.
-  Des tableaux définissant les éléments `effective_dates`,`contract_amounts` et `termination_dates`.

Cette fonction est actuellement prise en charge uniquement en anglais ; voir [Support de langue](/docs/services/discovery?topic=discovery-language-support#feature-support) pour plus de détails.


## Exigences relatives à la classification
{: #element-class}

Pour que la classification de documents à l'aide d'Element Classification soit possible, votre configuration et vos documents source doivent respecter les conditions suivantes :

-  Les fichiers à analyser doivent être au format PDF.
-  Le contenu PDF doit être sous forme de texte. Les documents numérisés ne peuvent pas être analysés même si la méthode OCR a été utilisée.
   **Remarque :** vous pouvez identifier un PDF qui se trouve dans un texte en ouvrant le document dans un afficheur de PDF et en utilisant l'outil **Text select** pour sélectionner un seul mot. Si vous ne pouvez pas sélectionner un seul mot dans le document, le fichier ne peut pas être analysé.
-  La taille des fichiers ne doit pas dépasser 50 Mo.
-  Les PDF sécurisés (mot de passe requis pour les ouvrir) et les PDF dont l'édition est restreinte (mot de passe requis pour les éditer) ne peuvent pas être analysés.
-  Les outils {{site.data.keyword.discoveryshort}} incluent une configuration nommée **Default Contract Configuration** (configuration de contrat par défaut) qui peut être utilisée pour enrichir votre collection de documents au format PDF. Vous avez également la possibilité de créer une configuration personnalisée incluant l'enrichissement `elements`. Voir [Exigences relatives aux collections](/docs/services/discovery?topic=discovery-element-classification#element-collection) pour plus de détails.
-  Les plans **Lite** permettent de traiter au maximum 500 pages par mois.
-  Non disponible dans les environnements de type dédié (**Dedicated**).
-  La normalisation post-enrichissement ne peut pas être effectuée lors de l'utilisation d'Element Classification.

**Remarque :** Le fichier **Default Contract Configuration** a été mis à jour le 25 septembre 2018. Si vous avez appliqué cette configuration à une collection avant cette date, consultez les [notes sur l'édition](/docs/services/discovery?topic=discovery-release-notes#25sept) pour des informations sur la mise à jour de votre collection.

## Exigences relatives aux collections
{: #element-collection}

Pour que l'enrichissement Element Classification puisse être utilisé sur votre collection, la configuration de cette dernière doit répondre à des exigences spécifiques.

Les outils {{site.data.keyword.discoveryshort}} incluent une configuration nommée **Default Contract Configuration** (configuration de contrat par défaut) qui a été préconfigurée pour enrichir des documents PDF avec l'enrichissement **Element Classification** et d'autres options requises. Vous pouvez choisir cette configuration lorsque vous créez votre collection. JSON pour cette configuration :

```json
 {
   "name": "Default Contract Configuration",
   "description": "Extract party, nature, and category from elements in PDFs.",
  "conversions": {
     "html": {
       "exclude_tags_completely": [],
       "exclude_tags_keep_content": []
     }
   },
   "enrichments": [
     {
       "source_field": "html",
       "destination_field": "enriched_html_elements",
       "enrichment": "elements",
       "options": {
         "model": "contract"
    }
     }
   ]
 }
```
{: codeblock}

Si vous souhaitez créer un fichier de configuration personnalisée, configurez votre collection pour répondre aux exigences suivantes :  

-  Les paramètres de conversion `PDF` sont ignorés si l'enrichissement Element Classification est spécifié.
-  Les paramètres de conversion `WORD` peuvent être omis car les fichiers Microsoft Word ne peuvent pas être ingérés lorsque l'enrichissement Element Classification est spécifié.
-  Les paramètres de normalisation `html` sont ignorés si l'enrichissement Element Classification est spécifié.
-  La segmentation de document n'est pas prise en charge lorsque l'enrichissement `elements` est spécifié.
-  Dans la configuration {{site.data.keyword.discoveryshort}}, la zone `html` doit être enrichie avec l'enrichissement `elements` et l'élément `model` doit avoir pour valeur `contract`. Dans l'exemple suivant, la zone `destination_field` a pour valeur `enriched_html`, mais n'importe quel nom valide peut être utilisé :

```json
 "enrichments": [
        {
     "source_field": "html",
    "destination_field": "enriched_html",
    "enrichment": "elements",
    "options": {
       "model": "contract"
    }
   }
 ]
```
{: codeblock}

Après avoir sélectionné la configuration `Default Contract Configuration` dans les outils, vous pouvez téléchargez vos documents. Si vous ne savez pas comment créer des collections et télécharger des documents, voir [Initiation aux outils](/docs/services/discovery?topic=discovery-getting-started#getting-started).

## Eléments classifiés
{: #classified-elements}

Dès lors qu'un document a été indexé avec Element Classification, il est renvoyé avec un tableau `elements` dans le cadre du document consultable.

Chaque objet du tableau `elements` décrit un élément du contrat ayant été identifié par {{site.data.keyword.discoveryshort}}. Le code suivant représente un élément typique :

```json
 {
    "location" : {
     "begin" : 134323,
     "end" : 135109
    },
    "text" : "9. In the event that the Participant's total vested account balance is determined to be less than or equal to $2,000.00 as of the date that the Order is received, the parties will be informed in writing that the QDRO determination fee may potentially liquidate the account.",
   "types" : [ {
      "label" : {
        "nature" : "Obligation",
        "party" : "All Parties"
      },
      "provenance_ids" : ["Nlu0ogWAEGms4vjhhzpMv3iXhm8b8fBqMBNtT/bXH8JI=", "PlyERkjg5is36RpFjVUFXp69eDmGmCxLCXRs1sDMDUCo="
      ]
    } ],
   "categories" : [ {
      "label" : "Communication",
      "provenance_ids" : [ "Cs38YyU6VBFtJK1/bgtEJBlqqWmX5F6OYUciRxQXf7HrN5TOCPuI7QXbkbj4LRXoxVuB3/i9H15q5TU+vFxorhUBeWFfF998OYQiPYViD2yI="
      ]
    } ],
    "attributes" : [ {
      "type" : "Currency",
      "text" : "$2,000.00",
      "location" : {
        "begin" : 134780,
        "end" : 134789
      }
    } ]
 }
 ```
{: codeblock}

Chaque élément comporte cinq sections importantes :
-  `location` : Index `begin` et `end` indiquant l'emplacement de l'élément dans le document d'entrée.
-  `text` : Texte de l'élément classifié.
-  `types` : Tableau qui comporte zéro objet `label` ou plus. Chaque objet `label` inclut une zone `nature` qui indique l'effet de l'élément sur la partie identifiée (par exemple, `Right` ou `Exclusion`) et une zone `party` qui identifie la ou les parties affectées par l'élément. Voir [Types](/docs/services/discovery?topic=discovery-contract_parsing#contract_types) dans [Maîtrise de l'analyse syntaxique de contrat](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing) pour des informations supplémentaires.
-  `categories` : Tableau qui contient zéro objet `label` ou plus. La valeur de chaque objet `label` correspond à une catégorie fonctionne dans laquelle tombe l'élément identifié. Voir [Catégories](/docs/services/discovery?topic=discovery-contract_parsing#contract_categories) dans [Maîtrise de l'analyse syntaxique de contrat](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing) pour des informations supplémentaires.
-  `attributes` : Tableau qui contient zéro objet ou plus définissant des attributs de l'élément. Types d'attribut actuellement pris en charge : `Location` (emplacement géographique référencé par l'élément), `DateTime` (date, heure, plage de dates ou plage d'heures spécifiée par l'élément) et `Currency` (valeurs et unités monétaires). Chaque objet du tableau `attributes` inclut également le texte et l'emplacement de l'élément identifié ; l'emplacement est défini par les index `begin` et `end` du texte dans le document d'entrée. Pour plus d'informations, voir [Attributes](/docs/services/discovery?topic=discovery-contract_parsing#attributes) dans la rubrique [Analyse syntaxique de contrats](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing).

En outre, chaque objet des tableaux `types` et `categories` inclut un tableau `provenance_ids`. Les valeurs répertoriées dans le tableau `provenance_ids` sont des valeurs hachées que vous pouvez envoyer à IBM pour fournir des commentaires ou recevoir du support sur la partie de l'analyse associée à l'élément. 

Certaines phrases ne sont associées à aucun type ou n'appartiennent à aucune catégorie. Dans ce cas, le service renvoie les tableaux `types` et `categories` sous forme d'objets vides.
{: note}

Certains phrases traitent de plusieurs sujets. Dans ce cas, le service renvoie plusieurs ensembles d'objets `types` et`categories`.
{: note}

Certaines phrases ne contiennent aucun attribut identifiable. Dans ce cas, le service renvoie le tableau `attributes` sous forme d'objets vides.
{: note}
