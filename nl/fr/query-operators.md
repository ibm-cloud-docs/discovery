---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-09"

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

# Opérateurs de requête
{: #query-operators}

Les opérateurs sont les séparateurs entre les différentes parties d'une requête. Pour obtenir la liste complète des opérateurs disponibles, voir la rubrique [Référence de requête](/docs/services/discovery/query-reference.html#operators).

## . \[Délimiteur JSON\]
{: #delimiter}

Ce délimiteur sépare les niveaux de hiérarchie dans le schéma JSON. 

Par exemple :
```bash
enriched_text.concepts.text
```
{: codeblock}

## : \[Inclut\]
{: #includes}

Cet opérateur indique une correspondance pour le terme de requête. 

Par exemple :
```bash
enriched_text.concepts.text:cloud computing
```
{: codeblock}

## :: \[Correspondance exacte\]
{: #match}

Cet opérateur indique une correspondance exacte pour le terme de requête. 

Par exemple :
```bash
enriched_text.concepts.text::cloud computing
```
{: codeblock}

## :! \[N'inclut pas\]
{: #notinclude}

Cet opérateur indique que les résultats ne contiennent pas de correspondance pour le terme de requête. 

Par exemple :
```bash
enriched_text.concepts.text:!cloud computing
```
{: codeblock}

## ::! \[N'est pas une correspondance exacte\]
{: #notamatch}

Cet opérateur indique que les résultats ne correspondent pas exactement au terme de requête. 

Par exemple :
```bash
enriched_text.concepts.text::!cloud computing
```
{: codeblock}

## \\ \[Caractère d'échappement\]
{: #escape}

Utilisé pour les requêtes nécessitant des littéraux chaîne contenant des caractères de contrôle. 

Par exemple :
```bash
enriched_text.concepts.text:\!cloud computing
```
{: codeblock}

## "" \[Requête de phrase\]
{: #phrase}

L'intégralité du contenu d'une requête de phrase est traitée avec des caractères d'échappement. Par conséquent, aucun caractère spécial présent dans une requête de phrase n'est analysé, à l'exception des guillemets (`"`) qui eux, doivent être spécifiés avec un caractère d'échappement (`\"`). Utilisez des requêtes de phrase avec des requêtes basées sur le classement et contenant un texte intégral et non avec des opérations de filtre booléen. N'utilisez pas de caractères génériques (`*`) dans les requêtes de phrase. **Remarque**: les apostrophes (`'`) ne sont pas prises en charge. 

Par exemple :
```bash
enriched_text.concepts.text:"IBM watson"
```
{: codeblock}

## (), \[\] \[Regroupement imbriqué\]
{: #nestedquery}

Des groupements logiques peuvent être constitués pour spécifier des informations plus spécifiques. 

Par exemple :
```bash
enriched_text.entities:(text:IBM,type:Company)
```
{: codeblock}

## \| \[ou\]
{: #or}

Opérateur booléen pour "ou".

Par exemple :
```bash
enriched_text.entities.text:Google|IBM
```
{: codeblock}

## , \[et\]
{: #and}

Opérateur booléen pour "et".

Par exemple :
```bash
enriched_text.entities.text:Google,IBM
```
{: codeblock}

## <=, >=, >, < \[Comparaisons numériques\]
{: #comparisons}

Crée les comparaisons numériques suivantes : inférieur ou égal à, supérieur ou égal à, supérieur à, inférieur à.

Par exemple :
```bash
enriched_text.sentiment.document.score>0.679
```
{: codeblock}

## ^x \[Multiplicateur de score\]
{: #multiplier}

Augmente la valeur de score d'un terme de recherche. 

Par exemple :
```bash
enriched_text.concepts.text:IBM^3
```
{: codeblock}

## * \[Caractère générique\]
{: #Wildcard}

Etablit des correspondances pour des caractères inconnus dans une expression de recherche. 

Par exemple :
```bash
enriched_text.concepts.text:IBM*
```
{: codeblock}

## ~n \[Variation de chaîne\]
{: #variation}

Nombre de changements d'un caractère qui doivent être apportés à une chaîne pour la rendre identique à une autre chaîne. Par exemple, `car~1` correspondra à `car`, `cap`, `cat`, `can`, etc..

Par exemple :
```bash
enriched_text.concepts.text:Watson~3
```
{: codeblock}
