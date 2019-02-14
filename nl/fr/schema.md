---

copyright:
years: 2018
lastupdated: "2018-10-23"

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

# Compréhension du schéma de sortie
{: #output_schema}

Après qu'un document a été ingéré à l'aide de la classification d'éléments (Element Classification), le service fournit une sortie JSON dans le schéma suivant pour la date de version `2018-10-15` ou ultérieure. La sortie sera incluse dans l'objet `enriched_html_elements`.  

```
{
  "document": {
    "title": string,
    "html": string,
    "hash": string
  },
  "model_id" : string,
  "model_version" : string,  
  "elements": [
    {
      "location": { 
        "begin": int,
        "end": int
      },
      "text": string,
      "types": [
        {
          "label": { "nature": string, "party": string },
          "provenance_ids": [string, string, ...]
            ...
          ]
        }
        ...
      ],
      "categories": [
        {
          "label": string,
          "provenance_ids": [string, string, ...]
        }
        ...
      ],
      "attributes": [
        {
      	  "type": string,
          "text": string,
          "location": { "begin": int, "end": int }
         }
      ]
    }
    ...
  ],
  "tables": [
    {
      "location" : {
        "begin" : int,
        "end" : int
      },
      "text": string,
      "section_title": {
        "text": string,
        "location": {
          "begin" : int,
          "end" : int
        }
      },
      "table_headers" : [
        {
          "cell_id" : string,
          "location" : {
            "begin" : int,
            "end" : int
          },
          "text" : string,
          "row_index_begin" : int,
          "row_index_end" : int,
          "column_index_begin" : int,
          "column_index_end" : int
        },
        ...
      ],
      "column_headers" : [
        {
          "cell_id" : string,
          "location" : {
            "begin" : int,
            "end" : int
          },
          "text" : string,
          "text_normalized" : string,
          "row_index_begin" : int,
          "row_index_end" : int,
          "column_index_begin" : int,
          "column_index_end" : int
        },
        ...
      ],
      "row_headers" : [
        {
          "cell_id" : string,
          "location" : {
            "begin" : int,
            "end" : int
          },
          "text" : string,
          "text_normalized" : string,
          "row_index_begin" : int,
          "row_index_end" : int,
          "column_index_begin" : int,
          "column_index_end" : int
        },
        ...
      ],
      "body_cells" : [
        {
          "cell_id" : string,
          "location" : {
            "begin" : int,
            "end" : int
          },
          "text" : string,
          "row_index_begin" : int,
          "row_index_end" : int,
          "column_index_begin" : int,
          "column_index_end" : int,
          "row_header_ids": [ string ],
          "row_header_texts": [ string ],
          "row_header_texts_normalized": [ string ],
          "column_header_ids": [ string ],
          "column_header_texts": [ string ],
          "column_header_texts_normalized": [ string ]
        },
        ...
      ]
    },
    ...
  ],
  "document_structure": {
    "section_titles": [
      {
        "text": string,
        "location": {
          "begin": int,
          "end": int
        },
        "level": int
        "element_locations": [
          {
            "begin": int,
            "end": int
          },
          ...
        ]
      },
      ...
    ],
    "leading_sentences": [
      {
        "text": string,
        "location": {
          "begin": int,
          "end": int
        },
        "element_locations": [
          {
            "begin": int,
            "end": int
          },
          ...
        ]
      },
      ...
    ]
  },
  "parties": [
    {
      "party": string,
      "role": string,
      "addresses": [
        {
          "text": string,
          "location": {
            "begin": int,
            "end": int
          }
        },
        ...
      ],
      "contacts": [
        {
          "name": string,
          "role": string 
        },
        ...
      ]
    },
    ...
  ],
  "effective_dates": [
    {
      "text": string,
      "location": { "begin": int, "end": int }
     },
     ...
  ],
  "contract_amounts": [
    {
      "text": string,
      "location": { "begin": int, "end": int }
    },
    ...
  ]
}
```

Le schéma est organisée comme suit.

  - `document` : Objet répertoriant les informations de base relatives au document, notamment :
    - `title` : Titre du document, si détecté.
    - `html` : Texte intégral du document d'entrée au format HTML. 
    - `hash` : Hachage MD5 du document d'entrée.
  - `model_id` : Modèle d'analyse à utiliser pour classifier le document. La valeur par défaut est `contracts`.  
  - `model_version` : Version du modèle d'analyse spécifié par la valeur du paramètre `model_id`.
  - `elements` : Tableau des éléments du document détectés par le service.
    - `location` : Emplacement de l'élément tel que défini par ses index `begin` et `end`.
    - `text` : Texte de l'élément. 
    - `types` : Tableau qui décrit ce qu'est l'élément et les parties prenantes concernées.
      - `label` : Objet qui définit le type à l'aide d'une paire des éléments suivants : 
        - `nature` : Type d'action requis par la phrase. Valeur en cours : `Definition`, `Disclaimer`, `Exclusion`, `Obligation` et `Right`.
        - `party` : Chaîne qui identifie la partie prenante à qui la phrase s'applique.
      - `provenance_ids` : Tableau d'une ou plusieurs valeurs hachées que vous pouvez envoyer à IBM pour fournir des commentaires ou recevoir du support.
    - `categories` : Tableau qui répertorie les catégories fonctionnelles dans lesquelles tombe l'élément ; en d'autre termes, domaine de l'élément.
      - `label` : Chaîne indiquant la catégorie identifiée. Vous trouverez la liste des [catégories](/docs/services/discovery/parsing.html#contract_categories) dans [Maîtrise de l'analyse syntaxique de contrat](/docs/services/discovery/parsing.html#contract_parsing).
      - `provenance_ids` : Tableau d'une ou plusieurs valeurs hachées que vous pouvez envoyer à IBM pour fournir des commentaires ou recevoir du support.
    - `attributes` : Tableau identifiant des attributs de document. Chaque objet du tableau de compose de trois éléments : 
      - `type` : Type d'attribut. Les valeurs possibles sont `Location`, `DateTime` et `Currency`.
      - `text` : Texte associé à l'attribut.
      - `location` : Emplacement de l'attribut tel que défini par ses index `begin` et `end`.
  - `tables`\* : Tableau définissant les tables identifiées dans le document d'entrée. 
    - `location` : Emplacement de la table en cours telle que définie par ses index `begin` et `end` dans le document d'entrée. 
    - `text` : Contenu textuel de la table en cours provenant du document d'entrée et sans contenu de balisage associé. 
    - `section_title` : Si identifié, emplacement d'un titre de section contenant la table en cours. Vide si aucun titre de section n'est identifié.
      - `text` : Texte du titre de section identifié. 
      - `location` : Emplacement du titre de section dans le document d'entrée tel que défini par ses index `begin` et `end`. 
    - `table_headers` : Tableau de cellules de niveau table applicables en tant qu'en-tête à toutes les autres cellules de la table en cours. Chaque en-tête de table est défini en tant que collection des éléments suivants :
      - `cell_id` : Valeur de chaîne au format `tableHeader-x-y` où `x` et `y` correspondent aux décalages de début et de fin de la valeur de cellule dans le document d'entrée.
      - `location` : Emplacement de la cellule dans le document d'entrée tel que défini par ses index `begin` et `end`. 
      - `text` : Contenu textuel de la cellule provenant du document d'entrée et sans contenu de balisage associé. 
      - `row_index_begin` : Index `begin` de l'emplacement `row` de la cellule dans la table en cours. 
      - `row_index_end` : Index `end` de l'emplacement `row` de la cellule dans la table en cours. 
      - `column_index_begin` : Index `begin` de l'emplacement `column` de la cellule dans la table en cours. 
      - `column_index_end` : Index `end` de l'emplacement `column` de la cellule dans la table en cours. 
    - `column_headers` : Tableau de cellules de niveau colonne, toutes applicables en tant qu'en-tête à d'autres cellules de la même colonne, de la table en cours. Chaque en-tête de colonne est défini en tant que collection des éléments suivants :
      - `cell_id` : Valeur de chaîne au format `columnHeader-x-y` où `x` et `y` correspondent aux décalages de début et de fin de cette cellule d'en-tête de colonne dans le document d'entrée.
      - `location` : Emplacement de la cellule dans le document d'entrée tel que défini par ses index `begin` et `end`. 
      - `text` : Contenu textuel de la cellule provenant du document d'entrée et sans contenu de balisage associé. 
      - `text_normalized` : Si vous fournissez une entrée de personnalisation, version normalisée du texte de cellule en fonction de la personnalisation ; sinon, même valeur que `text`. 
      - `row_index_begin` : Index `begin` de l'emplacement `row` de la cellule dans la table en cours. 
      - `row_index_end` : Index `end` de l'emplacement `row` de la cellule dans la table en cours. 
      - `column_index_begin` : Index `begin` de l'emplacement `column` de la cellule dans la table en cours. 
      - `column_index_end` : Index `end` de l'emplacement `column` de la cellule dans la table en cours. 
    - `row_headers` : Tableau de cellules de niveau ligne, toutes applicables en tant qu'en-tête à d'autres cellules de la même ligne, de la table en cours. Chaque en-tête de ligne est défini en tant que collection des éléments suivants :
      - `cell_id` : Valeur de chaîne au format `rowHeader-x-y` où `x` et `y` correspondent aux décalages de début et de fin de cette cellule d'en-tête de ligne dans le document d'entrée.
      - `location` : Emplacement de la cellule dans le document d'entrée tel que défini par ses index `begin` et `end`. 
      - `text` : Contenu textuel de la cellule provenant du document d'entrée et sans contenu de balisage associé. 
      - `text_normalized` : Si vous fournissez une entrée de personnalisation, version normalisée du texte de cellule en fonction de la personnalisation ; sinon, même valeur que `text`. 
      - `row_index_begin` : Index `begin` de l'emplacement `row` de la cellule dans la table en cours. 
      - `row_index_end` : Index `end` de l'emplacement `row` de la cellule dans la table en cours. 
      - `column_index_begin` : Index `begin` de l'emplacement `column` de la cellule dans la table en cours. 
      - `column_index_end` : Index `end` de l'emplacement `column` de la cellule dans la table en cours. 
    - `body_cells` : Tableau de cellules qui ne sont ni des cellules d'en-tête de table, d'en-tête de colonne ou d'en-tête de ligne, de la en cours avec associations d'en-tête de colonne et de ligne correspondantes. Chaque cellule de corps est définie en tant que collection des éléments suivants :
      - `cell_id` : Valeur de chaîne au format `bodyCell-x-y` où `x` et `y` correspondent aux décalages de début et de fin de cette cellule de corps de texte dans le document d'entrée.
      - `location` : Emplacement de la cellule dans le document d'entrée tel que défini par ses index `begin` et `end`. 
      - `text` : Contenu textuel de la cellule provenant du document d'entrée et sans contenu de balisage associé. 
      - `row_index_begin` : Index `begin` de l'emplacement `row` de cette cellule dans la table en cours. 
      - `row_index_end` : Index `end` de l'emplacement `row` de cette cellule dans la table en cours. 
      - `column_index_begin` : Index `begin` de l'emplacement `column` de cette cellule dans la table en cours. 
      - `column_index_end` : Index `end` de l'emplacement `column` de cette cellule dans la table en cours. 
      - `row_header_ids` : Tableau de valeurs, chacune étant la valeur `cell_id` d'un en-tête de ligne applicable à cette cellule de corps de texte.
      - `row_header_texts` : Tableau de valeurs, chacune étant la valeur `text` d'un en-tête de ligne applicable à cette cellule de corps de texte.
      - `row_header_texts_normalized` : Si vous fournissez une entrée de personnalisation, version normalisée des textes d'en-tête de ligne en fonction de la personnalisation ; sinon, même valeur que `row_header_texts`. 
      - `column_header_ids` : Tableau de valeurs, chacune étant la valeur `cell_id` d'un en-tête de colonne applicable à cette cellule de corps de texte.
      - `column_header_texts` : Tableau de valeurs, chacune étant la valeur `text` d'un en-tête de colonne applicable à cette cellule de corps de texte.
      - `column_header_texts_normalized` : Si vous fournissez une entrée de personnalisation, version normalisée des textes d'en-tête de colonne en fonction de la personnalisation ; sinon, même valeur que `column_header_texts`.
  - `document_structure` : Objet décrivant la structure du document d'entrée.
    - `section_titles` : Tableau contenant un objet par section et sous-section détectées dans le document d'entrée. Les sections et sous-sections ne sont pas imbriquées ; en revanche, elles sont aplaties et peuvent être replacées dans l'ordre en utilisant les valeurs `begin` et `end` de l'élément et la valeur `level` de la section.
      - `text` : Chaîne indiquant le titre de section, si détecté. 
      - `location` : Emplacement du titre dans le document d'entrée tel que défini par ses index `begin` et `end`. 
      - `level` : Entier indiquant le niveau auquel se trouve la section dans le document d'entrée. Par exemple, `1` représente une section de niveau supérieur, `2` une sous-section de la section de niveau `1`, et ainsi de suite. 
      - `element_locations` : Tableau contenant des objets qui spécifient les valeurs `begin` et `end` des phrases de la section.
    - `leading_sentences` : Tableau contenant un objet par section ou sous-section, en parallèle avec le tableau `section_titles`, qui détaille les phrases initiales dans la section ou sous-section correspondante. Comme dans le tableau `section_titles`, les objets ne sont pas imbriqués ; en revanche, ils sont aplatis et peuvent être replacés dans l'ordre en utilisant les valeurs `begin` et `end` de l'élément ou des marqueurs de niveau du document d'entrée. 
      - `text` : Chaîne indiquant la phrase initiale, si détectée. 
      - `location` : Emplacement de la phrase initiale dans le document d'entrée tel que défini par ses index `begin` et `end`. 
      - `element_locations` : Tableau contenant des objets qui spécifient les valeurs `begin` et `end` des phrases initiales de la section.
  - `parties` : Tableau définissant les parties identifiées par le service.
    - `party` : Valeur de chaîne identifiant la partie prenante.
    - `role` : Valeur de chaîne identifiant le rôle de la partie prenante.
    - `addresses` : Tableau d'objets qui identifient des adresses.
      - `text` : Chaîne contenant l'adresse. 
      - `location` : Emplacement de l'adresse telles que définie par ses index `begin` et `end`.
    - `contacts` : Tableau définissant le nom et le rôle des contacts identifiés dans le document d'entrée. 
      - `name` : Chaîne indiquant le nom d'un contact identifié. 
      - `role` : Chaîne indiquant le rôle du contact identifié.   
  - `effective_dates` : Tableau identifiant les dates d'effet du document.
    - `text` : Dates d'effet, répertoriés sous la forme d'une chaîne. 
    - `location` : Emplacement de la ou des dates telles définies par les index `begin` et `end`.
  - `contract_amounts` : Tableau identifiant les montants monétaires identifiés dans le document.
    - `text` : Montants du contrat, répertoriés sous la forme d'une chaîne. 
    - `location` : Emplacement du ou des montants tels que définis par les index `begin` et `end`.

**\*Remarques sur les tables :**
  - Les valeurs d'index de ligne et de colonne sont à base zéro, de sorte qu'elles commencent à `0`.
  - Plusieurs valeurs des tableaux d'éléments `row_header_ids` et `row_header_texts` indiquent une hiérarchie des en-têtes de ligne.
  - Plusieurs valeurs des tableaux d'éléments `column_header_ids` et `column_header_texts` indiquent une hiérarchie des en-têtes de colonne.
