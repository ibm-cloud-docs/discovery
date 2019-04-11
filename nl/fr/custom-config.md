---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-01-22"

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

# Référence de configuration
{: #configref}

Vous pouvez créer votre propre configuration d'ingestion {{site.data.keyword.discoveryshort}} dans JSON si vos données ont des besoins [conversion](#conversion), [enrichment](#enrichment) ou [normalization](#normalization) spécifiques.
{: shortdesc}

Les sections suivantes décrivent en détail la structure de ce fichier JSON et de l'objet que vous pouvez définir dedans.

Si votre collection a été créée en utilisant [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu), les paramètres de conversion PDF et Word répertoriés ne seront pas utilisés. La modification de ces paramètres sera donc ignorée.
{: note}

## Structure de la configuration
{: #structure}

La structure d'une configuration {{site.data.keyword.discoveryshort}} se présente comme suit :

```json
{
  "name": "Configuration Name",
  "description": "Descriptive text about the configuration",
  "conversions": {
    "word": {},
    "pdf": {},
    "html": {},
    "segment": {},
    "json_normalizations": []
  },
  "enrichments": [],
  "normalizations": []
}
```
{: codeblock}

L'objet JSON de base contient les éléments suivants :

-  `"name": "Configuration Name"` - Nom de votre configuration.
-  `"description": "Descriptive text about the configuration"` - Description de votre configuration.

Les objets et tableaux suivants doivent être définis pour convertir, enrichir et normaliser les documents qui sont téléchargés dans votre collection :

- `"conversions": {}` - Décrit de quelle manière les documents sont transformés en objets JSON pouvant être enrichis.
- `"enrichments": []` - Indique quels enrichissements sont appliqués à quelles parties de l'objet JSON.
- `"normalizations": []` - Spécifie les ajustements d'enrichissement requis pour que le document puisse être stocké.

En outre, les éléments suivants sont ajoutés à l'objet de base par {{site.data.keyword.discoveryshort}} lorsque la configuration est créée/mise à jour :

```json
{
  "configuration_id": "4f5b7c7b-ebf4-4963-882e-27eff08f08e3",
  "created": "2017-09-13T14:45:03.575Z",
  "updated": "2017-09-13T14:45:03.575Z"
}
```
{: codeblock}

## Conversion
{: #conversion}

Lors de la conversion des documents, en une ou plusieurs étapes, le format source d'origine est transformé en un objet JSON qui peut être utilisé pour le restant du processus d'ingestion. Selon le type de fichier téléchargé, le processus se déroule comme suit :

- Les fichiers **PDF** sont convertis en un document HTML à l'aide des options `pdf`, le document **HTML** ainsi obtenu est ensuite converti en un objet JSON à l'aide des options `html` et, enfin, l'objet **JSON** ainsi obtenu est converti à l'aide des options `json`.

- Les fichiers **Microsoft Word** sont convertis en un document HTML à l'aide des options `word`, le document **HTML** ainsi obtenu est converti en objet JSON à l'aide des options `html` et, enfin, l'objet **JSON** ainsi obtenu est converti à l'aide des options `json`.

- Les fichiers **HTML** sont convertis en un objet JSON à l'aide des options `html` et l'objet **JSON** ainsi obtenu est converti à l'aide des options `json`.

- Les fichiers **JSON** sont convertis à l'aide des options `json`.

Si votre collection a été créée en utilisant [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu), les paramètres de conversion PDF et Word répertoriés ne seront pas utilisés. La modification de ces paramètres sera donc ignorée.
{: note}

Ces options sont décrites dans les sections ci-après. Une fois la conversion terminée, les actions [enrichment](#enrichment) et  [normalization](#normalization) sont effectuées avant le stockage du contenu.

### PDF
{: #pdf}

Si votre collection a été créée en utilisant [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu), les paramètres de conversion PDF et Word répertoriés ne seront pas utilisés. La modification de ces paramètres sera donc ignorée.
{: note}

L'objet de conversion `pdf` définit de quelle manière les documents PDF doivent être convertis en documents HTML. Sa structure se présente comme suit :

```json
"pdf": {
  "heading": {
    "fonts": [
      {
        "level": 1,
        "min_size": 24,
        "max_size": 80,
        "bold": false,
        "italic": true,
        "name": "arial"
      },
      {
        "level": 2,
        "min_size": 18,
        "max_size": 24,
        "bold": true,
        "italic": false,
        "name": "ariel"
      }
    ]
  }
},
```
{: codeblock}

L'identification de la taille, de la police et du style de chaque niveau d'en-tête permet de déterminer à quel moment les en-têtes des fichiers PDF doivent être convertis (et convertis dans une balise "`h`" HTML appropriée). Les niveaux d'en-tête peuvent être spécifiés plusieurs fois si besoin afin d'identifier correctement toutes les sections pertinentes. Les niveaux d'en-tête HTML sont essentiels pour déterminer si vous prévoyez d'extraire le contenu à l'aide de sélecteurs CSS ou si vous avez l'intention de fractionner le document à l'aide de la fonction de fractionnement de document. L'objet `heading` contient le tableau `fonts` ; chaque élément de ce tableau spécifie un niveau d'en-tête à l'aide des paramètres suivants :

- `"level": INT` - *Obligatoire* - Niveau `h` HTML dans lequel le texte identifié via ces paramètres sera converti.
- `"min_size": INT` - _Facultatif_ - Taille de police la plus petite identifiée comme ce niveau d'en-tête.
- `"max_size": INT` - _Facultatif_ - Taille de police la plus grande identifiée comme ce niveau d'en-tête.
- `"bold": boolean` - _Facultatif_ - Lorsque ce paramètre a pour valeur `true`, seules les polices en gras sont identifiées comme ce niveau d'en-tête.
- `"italic": boolean` - _Facultatif_ - Lorsque ce paramètre a pour valeur `true`, seules les polices en italique sont identifiées comme ce niveau d'en-tête.
- `"name": "string"` - _Facultatif_ - Nom de la police qui est identifiée comme ce niveau d'en-tête.

Pour qu'une zone de texte puisse être identifiée comme un en-tête, elle doit correspondre à tous les paramètres définis dans l'élément de tableau spécifique. Si les paramètres définis sont trop flexibles, il se peut que le nombre d'en-têtes identifiés soit supérieur à ce que vous aviez prévu. Vous obtiendrez de meilleurs résultats si vous définissez chaque niveau d'en-tête plusieurs fois, car ainsi toutes les variations de niveau d'en-tête seront incluses, sans les correspondances incorrectes.


### Word
{: #word}

Si votre collection a été créée en utilisant [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu), les paramètres de conversion PDF et Word répertoriés ne seront pas utilisés. La modification de ces paramètres sera donc ignorée.
{: note}

L'objet de conversion `word` définit de quelle manière les documents PDF doivent être convertis en documents HTML. Sa structure se présente comme suit :

```json
"word": {
  "heading": {
    "fonts": [
      {
        "level": 1,
        "min_size": 24,
        "bold": true,
        "italic": false,
        "name": "arial"
      },
      {
        "level": 2,
        "min_size": 18,
        "max_size": 23,
        "bold": true,
        "italic": false
      }
    ],
    "styles": [
      {
        "level": 1,
        "names": [
          "pullout heading",
          "pulloutheading",
          "header"
        ]
      },
      {
        "level": 2,
        "names": [
          "subtitle"
        ]
      }
    ]
  }
},
```
{: codeblock}

L'objet de conversion Microsoft Word fonctionne de la même manière que l'objet de conversion PDF. Toutefois, deux tableaux différents peuvent être spécifiés dans l'objet `heading` lors de l'extraction d'en-têtes à partir de documents Microsoft Word. Vous pouvez utiliser l'un et/ou l'autre de ces tableaux d'extraction d'en-tête pour extraire les éléments de niveau d'en-tête de vos documents Microsoft Word.

Chaque élément du tableau `fonts` spécifie un niveau d'en-tête à l'aide des paramètres de caractéristique de police suivants :

- `"level": INT` - *Obligatoire* - Niveau `h` HTML dans lequel le texte identifié via ces paramètres sera converti.
- `"min_size": INT` - _Facultatif_ - Taille de police la plus petite identifiée comme ce niveau d'en-tête.
- `"max_size": INT` - _Facultatif_ - Taille de police la plus grande identifiée comme ce niveau d'en-tête.
- `"bold": boolean` - _Facultatif_ - Lorsque ce paramètre a pour valeur `true`, seules les polices en gras sont identifiées comme ce niveau d'en-tête.
- `"italic": boolean` - _Facultatif_ - Lorsque ce paramètre a pour valeur `true`, seules les polices en italique sont identifiées comme ce niveau d'en-tête.
- `"name": "string"` - _Facultatif_ - Nom de la police qui est identifiée comme ce niveau d'en-tête.

Pour qu'une zone de texte puisse être identifiée comme un en-tête dans le tableau `font`, elle doit correspondre à tous les paramètres définis dans l'élément de tableau spécifique. Si les paramètres définis sont trop flexibles, il se peut que le nombre d'en-têtes identifiés soit supérieur à ce que vous aviez prévu. Vous obtiendrez de meilleurs résultats si vous définissez chaque niveau d'en-tête plusieurs fois, car ainsi toutes les variations de niveau d'en-tête seront incluses, sans les correspondances incorrectes.

Chaque élément du tableau `styles` spécifie un niveau d'en-tête à partir des styles Microsoft Word appliqués à ce paragraphe.

- `"level": INT` - *Obligatoire* - Niveau `h` HTML dans lequel le texte identifié via ces paramètres sera converti.
- `"names": array` - *Obligatoire* - Tableau de noms de style qui seront identifiés comme ce niveau d'en-tête, séparés par des virgules.

*Quand utiliser des polices et quand utiliser des styles* - Si vos documents Microsoft Word sont conformes à la feuille de style, chaque paragraphe étant correctement balisé avec le style approprié, il est recommandé d'utiliser `styles` pour extraire les en-têtes. Toutefois, il se peut que les styles de certains documents aient été remplacés manuellement par leur auteur. Ces documents sont davantage susceptibles de fournir une bonne conversion si la méthode d'extraction `fonts` est utilisée.
{: tip}


### HTML
{: #html}

```json
"html": {
  "exclude_tags_completely": [
    "script",
    "sup"
  ],
  "exclude_tags_keep_content": [
    "font",
    "em"
  ],
  "exclude_content": {
    "xpaths": [
      "//*[@id='list-old']",
      "//*[@id='unstable']"
    ]
  },
  "keep_content": {
    "xpaths": [
      "//*[@id='footer']",
      "//*[@id='header']"
    ]
  },
  "exclude_tag_attributes": [
    "EVENT_ACTIONS"
  ],
  "keep_tag_attributes": [
    "id"
  ],
  "extracted_fields": {
    "{field_name}": {
      "css_selector": "{CSS_selector_expression_1}",
      "type": "{field_type}"
    }
  }
},
```
{: codeblock}

#### exclude_tags_completely
{: #configref_exclude_completely}

`"exclude_tags_completely" : array` - Tableau de noms de balise HTML qui seront exclus. Cela inclut la balise, le contenu et les attributs de balise définis.

#### exclude_tags_keep_content
{: #configref_exclude_tags_keep_content}

`"exclude_tags_keep_content" : array` - Tableau de noms de balise HTML dans lesquels les informations de balise seront retirées. Cela inclut la balise HTML et les attributs de balise. Le contenu de la balise ne sera pas retirée sauf indication contraire. Par exemple, si vous spécifiez `exclude_tags_keep_content` pour la balise HTML `span`, `<span class="info">Some <strong>Information</strong></span>` sera réduit à : `Some <strong>Information</strong>`.

#### exclude_content
{: #configref_exclude_content}

`"xpaths" : array` - Tableau de XPaths qui identifient le contenu à retirer. Si cette valeur est définie, toutes les données qui correspondent à l'un des XPaths sont retirées de la sortie.

#### keep_content
{: #configref_keep_content}

`"xpaths" : array` - Tableau de XPaths qui identifient le contenu à convertir. Si cette valeur est définie, toutes les données qui correspondent à l'un des XPaths sont incluses dans la sortie. Les inclusions spécifiées par ce paramètre sont traitées après le traitement spécifié par `exclude_content`.

#### exclude_tag_attributes
{: #configref_exclude_tag_attributes}

`"exclude_tag_attributes" : array` - Tableau de noms d'attribut HTML qui sont retirés lors de la conversion, quelle que soit la balise HTML dans laquelle ils se trouvent. **Remarque :** Vous recevrez un message d'erreur si vous spécifiez à la fois `exclude_tag_attributes` et `keep_tag_attributes` dans une même configuration - un seul de ces éléments peut être spécifié par configuration. S'il est présent, `keep_tag_attributes` doit être entièrement retiré de la configuration ; il ne peut pas être présent en tant que tableau vide.

#### keep_tag_attributes
{: #configref_keep_tag_attributes}

`"keep_tag_attributes" : array` - Tableau de noms d'attribut HTML qui sont conservés lors de la conversion. **Remarque :** Vous recevrez un message d'erreur si vous spécifiez à la fois `keep_tag_attributes` et `exclude_tag_attributes` dans une même configuration - un seul de ces éléments peut être spécifié par configuration. S'il est présent, `exclude_tag_attributes` doit être entièrement retiré de la configuration ; il ne peut pas être présent en tant que tableau vide.

#### extracted_fields
{: #configref_extracted}

Cet objet définit n'importe quel contenu de la source HTML qui doit être extrait dans une zone JSON distincte dans le cadre de la conversion. Le contenu est identifié à l'aide de sélecteurs CSS.

Chaque zone que vous voulez créer est définie par un objet, comme suit :

```json
"{field_name}": {
  "css_selector": "{CSS_selector_expression_1}",
          "type": "{field_type}"
}
```
{: codeblock}

- `"{field_name}"` - Nom de la zone à créer.

**Remarque :** les noms de zone définis dans votre configuration doivent respecter les restrictions définies dans la rubrique [Exigences relatives aux noms de zone](#field_reqs).

- `"css_selector" : string` *Obligatoire* - Expression de sélecteur CSS qui définit la zone de contenu à stocker dans une zone.
- `"type" : string` *Obligatoire* - Type de zone à créer : `string` ou `date`.
Pour plus d'informations, voir [Utilisation de sélecteurs CSS pour extraire des zones](/docs/services/discovery?topic=discovery-configservice#using-css).

### Segment
{: #segment}

L'objet `segment` est un groupe d'options de configuration qui permettent de fractionner des documents ingérés en un ou plusieurs segments en fonction des en-têtes HTML identifiés (`h1`, `h2`).

```json
"segment": {
  "enabled": true,
      "selector_tags": ["h1", "h2", "h3", "h4", "h5", "h6"]
    }
```
{: codeblock}

- `"enabled": boolean` - *Obligatoire* - Doit avoir pour valeur `true` afin d'activer la segmentation de document.
- `"selector_tags": array` - *Obligatoire* - Tableau de balises `h` HTML utilisées pour le fractionnement des documents, séparées par des virgules.

De façon générale, lorsque la segmentation de document est activée, les éléments suivants ne peuvent pas être spécifiés :

-  `json_normalizations` ne peut pas être spécifié dans le cadre de la configuration.
-  `normalizations` ne peut pas être spécifié dans le cadre de la configuration.
-  L'option `extracted_fields` de la conversion `html` ne peut pas être spécifiée dans le cadre de la configuration.

Pour plus d'informations, voir [Exécution de la segmentation](/docs/services/discovery?topic=discovery-configservice#performing-segmentation).


### JSON
{: #json}

Vous pouvez effectuer une normalisation d'enrichissement préalable du document JSON ingéré en définissant des objets `operation` dans le tableau `json_normalizations`.

```json
"json_normalizations": [
  {
    "operation": "remove",
    "source_field": "header"
  },
  {
    "operation": "copy",
    "source_field": "title",
    "destination_field": "title_old"
  },
  {
    "operation": "move",
    "destination_field": "content",
    "source_field": "body"
  },
  {
    "operation": "merge",
    "source_field": "synopsis",
    "destination_field": "preamble"
  },
  {
    "operation": "remove_nulls"
  }
]
```
{: codeblock}

#### Objets operation
{: #operations}

- `"operation": string` - *Obligatoire* - L'opération qui sera exécutée sur le document JSON doit être l'une des suivantes :
  - `remove` - L'objet `source_field` spécifié sera retiré du document JSON.
  - `copy` - Le contenu de l'objet `source_field` spécifié sera copié vers une nouvelle instance de l'objet `destination_field`.
  - `move` - L'objet `source_field` spécifié sera renommé `destination_field`. Si `destination_field` existe déjà, une nouvelle instance de cet objet est créée.
  - `merge` - Le contenu des objets `source_field` et `destination_field` est fusionné dans l'objet `destination_field`.
  - `remove_nulls` - Les zones comportant un contenu `null` seront retirées.
- `"source_field": string` - _Facultatif_ - Zone sur laquelle l'opération sera exécutée.
- `"destination_field": string` - _Facultatif_ - Zone de destination dans laquelle l'opération sera restituée.  

  **Remarque :** les noms de zone définis dans votre configuration doivent respecter les restrictions définies dans la rubrique [Exigences relatives aux noms de zone](#field_reqs).


## Enrichissements
{: #enrichments}

```json
"enrichments": [
        {
    "enrichment": "elements",
    "source_field": "html",
    "destination_field": "enriched_html",
    "options": {
      "model": "contract"
    }
  },
  {
    "enrichment": "natural_language_understanding",
    "source_field": "title",
    "destination_field": "enriched_title",
    "options": {
      "features": {
        "keywords": {
          "sentiment": true,
                        "emotion": false,
                        "limit": 50
        },
        "entities": {
          "sentiment": true,
          "emotion": false,
          "limit": 50,
          "mentions": true,
          "mention_types": true,
          "sentence_locations": true,        
          "model": "WKS-model-id"
        },
                    "sentiment": {
          "document": true,
          "targets": [
            "IBM",
            "Watson"
          ]

        },
        "emotion": {
          "document": true,
          "targets": [
            "IBM",
            "Watson"
          ]
        },
        "categories": {},
        "concepts": {
          "limit": 8
        },
        "semantic_roles": {
          "entities": true,
          "keywords": true,
          "limit": 50
        },
                    "relations": {
          "model": "WKS-model-id"
        }
      }
    }
  }
]
```
{: codeblock}

{{site.data.keyword.discoveryshort}} prend en charge l'ajout des enrichissements {{site.data.keyword.nlushort}} et Element Classification. Chaque zone que vous souhaitez enrichir est définie par un objet dans le tableau `enrichments`. Un objet `source_field`, un objet `destination_field` et des enrichissements doivent être spécifiés pour chaque objet d'enrichissement.

- `"enrichment" : string` - *Obligatoire* - Type d'enrichissement à utiliser sur cette zone. Pour extraire des enrichissements{{site.data.keyword.nlushort}}, utilisez `natural_language_understanding`, pour exécuter un enrichissement Element Classification, utilisez `elements`.

  **Remarque :** lorsque vous utilisez l'enrichissement `elements`, vous devez suivez suivre les instructions spécifiées dans la documentation [Element Classification](/docs/services/discovery?topic=discovery-element-classification#element-classification). Plus spécifiquement, seuls les fichiers PDF peuvent être ingérés lorsque cet enrichissement est spécifié.

- `"source_field" : string` - *Obligatoire* - Zone source qui sera enrichie. Cette zone doit exister dans votre source une fois que l'opération `json_normalizations` est terminée.
- `"destination_field" : string` - *Obligatoire* - Nom de l'objet conteneur dans lequel les enrichissements seront créés.

  **Remarque :** les noms de zone définis dans votre configuration doivent respecter les restrictions définies dans la rubrique [Exigences relatives aux noms de zone](#field_reqs).

### Enrichissements Element Classification
{: #element_classification_enrichments}

Lorsque vous utilisez Element Classification, chaque objet d'enrichissement `elements` doit contenir un objet `"options": {}` pour lequel les paramètres suivants sont spécifiés :

- `"model" : string` - *Obligatoire* - Modèle d'extraction d'élément à utiliser sur ce document. Les modèles actuellement pris en charge sont les suivants :`contract`

**Remarque :** lorsque vous utilisez l'enrichissement `elements`, vous devez suivez suivre les instructions spécifiées dans la documentation [Element Classification](/docs/services/discovery?topic=discovery-element-classification#element-classification). Plus spécifiquement, seuls les fichiers PDF peuvent être ingérés lorsque cet enrichissement est spécifié.

### Enrichissements Natural Language Understanding
{: #nlu_enrichments}

Lorsque vous utilisez {{site.data.keyword.nlushort}}, chaque objet du tableau `enrichments` doit également contenir un objet`"options": { "features": { } }` comportant un ou plusieurs des enrichissements suivants :

### categories
{: #nlu_categories}

L'enrichissement `categories` identifie les catégories générales présentes dans le document ingéré. Aucune option n'est associée à cet enrichissement qui doit être spécifié comme un objet vide `"categories" : {}`.

### concepts
{: #nlu_concepts}

L'enrichissement `concepts` identifie les concepts auxquels le texte d'entrée est associé, en fonction d'autres concepts et entités présents dans ce texte.

- `"limit" : INT` - *Obligatoire* - Nombre maximal de concepts à extraire du document ingéré.

### emotion
{: #nlu_emotion}

L'enrichissement `emotion` évalue la tonalité affective globale (par exemple, `anger`) de l'ensemble du document ou les chaînes cible spécifiées dans l'ensemble du document. Cet enrichissement ne peut être utilisé qu'avec un contenu en anglais.

- `"document" : boolean ` _Facultatif_ - Lorsque ce paramètre a pour valeur `true`, la tonalité affective globale de l'ensemble du document est évaluée.
- `"targets" : array ` _Facultatif_ - Tableau de chaînes cible utilisées pour l'évaluation de l'état émotionnel du document, séparées par des virgules.

### entities
{: #nlu_entities}

L'enrichissement `entities` extrait des instances d'entités connues, telles que des personnes, des lieux et des organisations. Le cas échéant, un modèle personnalisé {{site.data.keyword.knowledgestudioshort}} peut être spécifié pour extraire des entités personnalisées.

- `"sentiment" : boolean` - _Facultatif_ - Lorsque ce paramètre a pour valeur `true`, une analyse des sentiments est effectuée sur l'entité extraite dans le contexte du contenu environnant.
- `"emotion" : boolean` - _Facultatif_ - Lorsque ce paramètre a pour valeur `true`, une analyse de la tonalité affective est effectuée sur l'entité extraire dans le contexte du contenu environnant.
- `"limit" : INT` - _Facultatif_ - Nombre maximal d'entités à extraire du document ingéré. La valeur par défaut est `50`.
- `"mentions": boolean` - _Facultatif_ - Lorsque ce paramètre a pour valeur `true`, le nombre de fois que cette entité est mentionnée est enregistré. La valeur par défaut est `false`.
- `"mention_types": boolean` - _Facultatif_ - Lorsque ce paramètre a pour valeur `true`, le type de chaque mention de cette entité est stocké. La valeur par défaut est `false`.
- `"sentence_location": boolean` - _Facultatif_ - Lorsque ce paramètre a pour valeur `true`, l'emplacement de la phrase contenant chaque mention d'entité est stocké. La valeur par défaut est `false`.
- `"model" : string` - _Facultatif_ - Lorsque ce paramètre est spécifié, le modèle personnalisé est utilisé pour extraire des entités au lieu du modèle public. Cette option requiert qu'un modèle personnalisé {{site.data.keyword.knowledgestudioshort}} soit associé à votre instance de {{site.data.keyword.discoveryshort}}. Pour plus d'informations, voir [Intégration à Watson Knowledge Studio](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-with-wks).

### keywords
{: #nlu_keywords}

L'enrichissement `keywords` extrait des instances de mots significatifs contenus dans le texte. Pour comprendre la différence entre les enrichissements keywords, concepts et entities, voir : [Compréhension de la différence entre Entities, Concepts et Keywords](/docs/services/discovery?topic=discovery-configservice#udbeck).

- `"sentiment" : boolean` - _Facultatif_ - Lorsque ce paramètre a pour valeur `true`, une analyse des sentiments est effectuée sur le mot clé extrait dans le contexte du contenu environnant.
- `"emotion" : boolean` - _Facultatif_ - Lorsque ce paramètre a pour valeur `true`, une analyse de la tonalité affective est effectuée sur le mot clé extrait dans le contexte du contenu environnant.
- `"limit" : INT` - _Facultatif_ - Nombre maximal de mots clés à extraire du document ingéré. La valeur par défaut est `50`.

### semantic_roles
{: #nlu_semantic_roles}

L'enrichissement `semantic_roles` identifie des composants de phrase, tels que le sujet, l'action et l'objet, dans le texte ingéré.

- `"entities" : boolean` - _Facultatif_ - Lorsque ce paramètre a pour valeur `true`, des entités sont extraites des composants de phrase.
- `"keywords" : boolean` - _Facultatif_ - Lorsque ce paramètre a pour valeur `true`, des mots clés sont extraits des composants de phrase.
- `"limit" : INT` - _Facultatif_ - Nombre maximal d'objets `semantic_roles` à extraire (phrases devant faire l'objet d'une analyse syntaxique) du document ingéré. La valeur par défaut est `50`.

### sentiment
{: #nlu_sentiment}

L'enrichissement `sentiment` évalue le niveau de sentiment global présent dans l'ensemble du document ou les chaînes cible spécifiées dans l'ensemble du document.

- `"document" : boolean ` _Facultatif_ - Lorsque ce paramètre a pour valeur `true`, le sentiment présent dans l'ensemble du document est évalué.
- `"targets" : array ` _Facultatif_ - Tableau de chaînes cible utilisées pour l'évaluation du sentiment présent dans le document, séparées par des virgules.

### relations
{: #nlu_relations}

L'enrichissement `relations` extrait des relations connues entre les entités identifiées dans le document. Le cas échéant, un modèle personnalisé {{site.data.keyword.knowledgestudioshort}} peut être spécifié pour extraire des relations personnalisées.

- `"model" : string` - _Facultatif_ - Lorsque ce paramètre est spécifié, le modèle personnalisé est utilisé pour extraire des relations au lieu du modèle public. Cette option requiert qu'un modèle personnalisé {{site.data.keyword.knowledgestudioshort}} soit associé à votre instance de {{site.data.keyword.discoveryshort}}. Pour plus d'informations, voir [Intégration à Watson Knowledge Studio](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-with-wks).

## Normalisation
{: #normalization}

Le tableau `normalizations` répertorie les objets `operation` JSON qui sont utilisés pour nettoyer le document JSON ingéré une fois que des `enrichissements` ont été appliqués et avant qu'il ne soit stocké.

```json
"normalizations": [
  {
    "operation": "remove",
    "source_field": "enriched_title.entities.text"
  },
  {
    "operation": "copy",
    "source_field": "enriched_title.sentiment.document.score",
    "destination_field": "titlescore"
  }
]
```
{:codeblock}

Les options d'objet `operation` sont répertoriées [ici](#operations)

## Exigences relatives aux noms de zone
{: #field_reqs}

Vous ne devez pas entrer d'espace dans les noms de zone. Les caractères et les chaînes ci-dessous sont réservés et ne peuvent pas être utilisés dans les noms de zone :


```
  .  ,  # ? :
  id
  score
  highlight
  result_metadata
```
{: pre}

Les caractères `_`, `+` et `-` ne peuvent pas être utilisés comme préfixe pour `field_name`.

Les caractères numériques `0 - 9` ne doivent pas être utilisés comme suffixe d'un nom de zone (par exemple, `extracted-content2`). Ces noms de zone seront indexés, mais ils ne pourront pas faire l'objet d'une requête.
