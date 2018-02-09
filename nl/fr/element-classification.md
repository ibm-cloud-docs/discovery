---

copyright:
  years: 2015, 2017
lastupdated: "2017-12-15"

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

# Element Classification
{: #element-classification}

L'enrichissement Element Classification permet d'effectuer rapidement une analyse syntaxique de documents constitutifs afin de convertir, d'identifier et de classifier des éléments importants. A l'aide de la technique de pointe de traitement automatique du langage naturel, la partie prenante (la personne référencée), la nature (type d'élément) et la catégorie (classe spécifique) sont extraites des éléments d'un document. 

L'enrichissement Element Classification a été conçu pour :

- La compréhension en langage naturel de contrats, plus spécifiquement les contrats d'achat de logiciels et les documents de réglementation
- La possibilité de convertir un PDF de programmation dans un format JSON annoté
- L'identification d'entités et de catégories légales qui cadrent avec une expertise en la matière

Element Classification regroupe un ensemble fonctionnellement riche d'API Watson automatisées intégrées permettant d'entrer un PDF de programmation afin d'identifier des sections, des listes (numérotées et à puces), des notes de bas de page et des tables en convertissant ces éléments dans un format HTML structuré. De plus, la classification de ce format structuré est annotée et présentée sous la forme d'un document JSON avec des éléments, des types et des catégories libellés. 

Element Classification transmet vos données de manière sécurisée en effectuant un chiffrement en cours et au repos. Pour plus d'informations sur la sécurité IBM Cloud, voir la [description du service IBM Cloud![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=IBM+Bluemix+Service+Description){: new_window}.

## Exigences relatives à la classification

Pour que la classification de documents à l'aide d'Element Classification soit possible, votre configuration et vos documents source doivent respecter les conditions suivantes :

- Les fichiers à analyser doivent être au format PDF. 
- Le contenu PDF doit être dans un formulaire texte (les documents qui ont été scannés, mais dont les caractères n'ont pas fait l'objet d'une reconnaissance optique ne peuvent pas être analysés).

  **Remarque :** vous pouvez identifier un PDF qui se trouve dans un texte en ouvrant le document dans un afficheur de PDF et en utilisant l'outil **Text select** pour sélectionner un seul mot. Si vous ne pouvez pas sélectionner un seul mot dans le document, le fichier ne peut pas être analysé. 

- La taille des fichiers ne doit pas dépasser 50 Mo. 
- Les PDF sécurisés (mot de passe requis pour les ouvrir) et les PDF dont l'édition est restreinte (mot de passe requis pour les éditer) ne peuvent pas être analysés.
- Une configuration {{site.data.keyword.discoveryshort}} personnalisée incluant l'enrichissement `elements` doit être créée. Cette configuration ne peut être utilisée que pour ingérer des documents PDF.
- Les plans **Lite** et **Standard** peuvent traiter un maximum de 500 pages par mois. 
- Non disponible pour les instances de service abonnées au plan **Premium**. 

## Exigences relatives aux collections

Pour que l'enrichissement Element Classification puisse être utilisé sur votre collection, la configuration de cette dernière doit répondre aux exigences spécifiques suivantes :

- Les paramètres de conversion `PDF` sont ignorés si l'enrichissement Element Classification est spécifié. 
- Les paramètres de conversion `WORD` peuvent être omis car les fichiers Microsoft Word ne peuvent pas être ingérés lorsque l'enrichissement Element Classification est spécifié. 
- Les paramètres de normalisation `html` sont ignorés si l'enrichissement Element Classification est spécifié. 
- Le fractionnement de document n'est pas pris en charge lorsque l'enrichissement `elements` est spécifié. 
- Dans la configuration {{site.data.keyword.discoveryshort}}, la zone `html` doit être enrichie avec l'enrichissement `elements` et l'élément `model` doit avoir pour valeur `contract`. Dans l'exemple suivant, la zone `destination_field` a pour valeur `enriched_html`, mais n'importe quel nom valide peut être utilisé :

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

Ces options ne peuvent pas être ajoutées à l'aide des outils {{site.data.keyword.discoveryshort}}. Créez une configuration personnalisée et ajoutez l'enrichissement **Element Classification** à la zone `html`. 

**Remarque :** lorsque l'enrichissement **Element Classification** est ajouté à l'aide des outils, la zone `destination_field` prend la valeur `enriched_html_elements`.

Une fois la configuration personnalisée créée, elle peut être utilisée dans n'importe quelle collection. N'importe quelle méthode de téléchargement de documents peut être utilisée tant que la configuration personnalisée est spécifiée. Si vous ne savez pas comment créer des collections et télécharger des documents, voir [Initiation aux outils](/docs/services/discovery/getting-started-tool.html).

## Eléments classifiés

Dès lors qu'un document a été indexé avec Element Classification, il est renvoyé avec un tableau `elements` dans le cadre du document consultable. 

Chaque objet du tableau `elements` décrit un élément du contrat que l'enrichissement Element Classification a identifié. Le code suivant représente un élément typique :

```
{
   "sentence" : {
     "begin" : 34941,
     "end" : 35307
   },
   "sentence_text" : "A buyer must buy from the supplier.",
   "types" : [ {
     "label" : {
       "nature" : "Obligation",
       "party" : "Supplier"
     },
     "assurance" : "High"
   } ],
   "categories" : [ {
     "label : "Responsibilities",
     "assurance : "High"
     }
   ]
}
```

Il existe quatre sections importantes pour l'élément :

- `sentence_text` – Texte qui a été analysé. 
- `sentence` – Cet objet décrit à quel endroit l'élément a été trouvé dans le document HTML converti. Il contient une valeur de caractère de début et une valeur de caractère de fin. 
- `types` – Ce tableau décrit l'élément et à qui il s'applique. Il comporte un ou plusieurs ensembles composés d'un objet `party` (personne concernée par la phase) et d'un objet `nature` (impact de la phrase sur la partie prenante identifiée). 
- `categories` – Ce tableau affiche la liste des catégories fonctionnelles correspondant à la phrase identifiée. Il s'agit du thème abordé dans la phrase. 

**Remarque** : certaines phrases ne correspondent à aucun type et à aucune catégorie et, dans ce cas, les tableaux `types` et `categories` sont renvoyés vides. 

**Remarque :** certaines phrases couvrent plusieurs sujets et, par conséquent, elles seront renvoyées avec plusieurs éléments `types` et`categories`. 

De plus, les parties prenantes identifiées sont également définies dans le tableau parties :

```
  "parties" : [ {
    "party" : "Customer",
    "role" : "Buyer"
  } ]
```

Il existe deux sections importantes pour chaque élément du tableau parties :

- `party` – Texte qui a été identifié en tant que partie prenante dans le document. 
- `role` – Rôle de la partie prenante qui a été identifiée. Les rôles varient en fonction des sous-domaines. Pour obtenir la liste des rôles possibles, voir les informations relatives au sous-domaine spécifié. Les parties prenantes qui ne peuvent pas être identifiées pour un rôle spécifique sont libellées comme telles. 


## Compréhension des éléments de contrat

Les contrats analysés à partir de l'enrichissement Element Classification sont renvoyés avec chaque élément identifié analysé.

Les sections suivantes expliquent de quelle façon le document JSON renvoyé décrit l'analyse. 

### Type

L'élément `types` est un tableau d'objets contenant chacun une nature (élément nature) et une partie prenante (élément party) ayant été identifiées comme une strophe pour cet élément. Le tableau suivant décrit les éléments `nature` et `party` possibles pouvant être identifiés :

Les natures correspondent aux types d'action requis par la phrase. 

| **Nature** | **Description** |
| --- | --- |
| Definition | Cet élément ajoute de la clarté à un terme/une relation/etc. Aucune action n'est requise pour cet élément et aucune partie prenante n'est concernée. |
| Disclaimer | La partie prenante définie dans l'élément n'est pas tenue d'honorer les conditions spécifiques définies dans l'élément, mais il ne lui est pas interdit de le faire. |
| Exclusion | La partie prenante définie dans l'élément n'honorera pas les conditions spécifiques définies dans l'élément. |
| Obligation | La partie prenante définie dans l'élément est tenue d'honorer les conditions définies dans l'élément. |
| Right | La partie prenante définie dans l'élément est assurée de recevoir les conditions définies dans l'élément. |

### Parties

Pour chaque clause identifiée, des parties prenantes sont identifiées par leur nom. Chaque partie prenante identifiée est ensuite classifiée par `role`. Les parties prenantes sont les participants du contrat. Les rôles pouvant être identifiés pour un contrat sont les suivants :

| **Rôle** | **Description** |
| --- | --- |
| `Buyer` | Partie prenante chargée de régler les marchandises/services. |
| `End User` | Partie prenante qui va interagir avec les marchandises/services réels, ce qui la différencie explicitement du rôle Buyer. |
| `None` | Aucune partie prenante n'a été identifiée pour cet élément, toujours apparié avec la nature Definition. |
| `Supplier` | Partie prenante chargée de fournir les marchandises/services. |

### Categories

Il s'agit du thème abordé dans la phrase. Les catégories suivantes peuvent être identifiées.

| **Catégories** | **Description** |
| --- | --- |
| `Amendments` | Modification du contrat d'origine qui stipule les conditions relatives au changement des conditions. |
| `Asset Use` | Détails relatifs aux actifs du contrat qui seront utilisés par l'une ou l'autre des parties prenantes. |
| `Assignments` | Englobe le transfert des droits détenus par l'une des parties prenantes vers l'autre partie prenante. |
| `Audits` | Cette clause permet à l'acheter d'examiner ou d'inspecter le fournisseur des services fournis. |
| `Communication` | Décrit les méthodes de communication acceptables et les informations de contact. |
| `Confidentiality` | Décrit de quelle façon les informations confidentielles ou privées seront traitées, par exemple, qui peut partager quoi et comment. |
| `Business Continuity` | Décrit de quelle façon une organisation continuera de fournir un travail à des niveaux prédéfinis, en cas d'incident entraînant une interruption de l'activité. |
| `Definitions` | Section qui définit une condition utilisée dans le document. |
| `Deliverables` | Articles ou services à fournir à la fin d'un travail. |
| `Delivery` | Planification ou processus spécifique relatifs à la réalisation d'un projet. |
| `Dispute Resolution` | Prévoit un éventuel différend entre les parties prenante du contrat et la façon dont il sera géré. |
| `Force Majeure` | Clause qui libère les deux parties prenantes de toute responsabilité en cas d'événement perturbateur. |
| `Indemnification` | Décrit les solutions ou les conséquences si des conditions ne sont pas respectées. |
| `Insurance` | Décrit le niveau de couverture d'assurance qui doit être associée à un fournisseur. |
| `Intellectual Property` | Clause qui concerne les brevets, les droits d'auteur et les marques. Plus généralement, cette clause peut concerner les inventions, la création ou le savoir-faire. |
| `Liability` | Décrit les obligations et les limitations concernant la responsabilité de chaque partie prenante. |
| `Miscellaneous` | Sections d'intérêt qui ne s'intègrent dans aucune autre catégorie. |
| `Payment Terms & Billing` | Décrit les paiements dus et la planification correspondante. |
| `Pricing & Taxes` | Explique comment les prix sont calculés et comment les taxes doivent s'appliquer. |
| `Privacy` | Décrit la réglementation en matière de confidentialité qui s'applique. |
| `Responsibilities` | Décrit les responsabilités de chaque partie prenante. |
| `Safety and Security` | Explique comment éviter les dommages à une partie prenante. Comprend la sécurité des biens personnels et physiques. |
| `Scope of Work` | Décrit ce qui sera réalisé par les parties prenantes de manière détaillée dans le description du travail. |
| `Subcontracts` | Concerne les parties prenantes devant satisfaire à une obligation. |
| `Term & Termination` | Durée pendant laquelle quelque chose se produit, et conditions selon lesquelles cela peut s'arrêter. |
| `Warranties` | Garantie par un fournisseur du bon fonctionnement d'un produit. |

### Assurance

Chaque élément (type ou category) identifié par Element Classification se voit attribuer une évaluation `assurance`. Les  valeurs possibles pour l'élément assurance sont les suivantes : 

| **Assurance** | **Description** |
| --- | --- |
| `High` | Il est indéniable que la classification fournie est représentative du contenu. |
| `Low` | Il semblerait que la classification soit justifiée, mais des examens supplémentaires peuvent être nécessaires pour la confirmer. |
