---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-04"

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

# Paramètres de requête
{: #query-parameters}

Le service {{site.data.keyword.discoveryfull}} offre des fonctions de recherche de contenu puissantes par l'intermédiaire de requêtes. Une fois votre contenu téléchargé et enrichi par le service {{site.data.keyword.discoveryshort}}, vous pouvez créer des requêtes, intégrer {{site.data.keyword.discoveryshort}} dans vos propres projets ou créer une application personnalisée en utilisant {{site.data.keyword.watson}} Explorer Application Builder. Pour vous initier à la création de requêtes, voir  [Concepts de requête](/docs/services/discovery?topic=discovery-query-concepts#query-concepts). Pour obtenir la liste complète des paramètres, voir [Référence de requête](/docs/services/discovery?topic=discovery-query-reference#parameter-descriptions).
{: shortdesc}

**Paramètres de recherche**

Les paramètres de recherche vous permettent d'effectuer des recherches dans votre collection, d'identifier un ensemble de résultats et d'analyser l'ensemble de résultats.

L'**ensemble de résultats** est le groupe de documents identifiés par les recherches combinées des paramètres de recherche. L'ensemble de résultats peut être beaucoup plus important que les résultats renvoyés. Si une requête vide est effectuée, l'ensemble de résultats est égal à tous les documents contenus dans la collection.

## query
{: #query}

Une recherche exécutée à l'aide d'un paramètre de requête renvoie tous les documents de votre fichier avec des enrichissements complets et un texte intégral par ordre de pertinence. Une requête exclut également les documents qui ne mentionnent pas le contenu de la requête. Ces requêtes sont écrites à l'aide du [langage de requête {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-query-operators#query-operators).

## filter
{: #filter}

Requête pouvant être mise en cache qui exclut les documents qui ne mentionnent pas le contenu de la requête. Les résultats d'une recherche exécutée à l'aide d'un paramètre de filtre ne sont **pas** renvoyés par ordre de pertinence. Ces requêtes sont écrites à l'aide du [langage de requête {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-query-operators#query-operators).

### Différences entre les paramètres de requête et de filtre
{: #filtervquery}

Si vous testez le même terme de recherche sur un petit ensemble de données, vous constaterez peut-être que les paramètres de filtre (`filter`) et de requête (`query`) renvoient des résultats très semblables (voire identiques). Cependant, il y a une différence entre les deux paramètres.

- Un paramètre de filtre utilisé seul renvoie des résultats de recherche dans un ordre spécifique.
- Un paramètre de requête utilisé seul renvoie des résultats des recherche par ordre de pertinence.

Avec des ensembles de données volumineux, si les résultats doivent être renvoyés par ordre de pertinence, vous devez combiner les paramètres `filter` et `query` car ainsi, vous améliorerez vos performances. En effet, le paramètre `filter` s'exécute en premier et met en cache les résultats, puis le paramètre `query` les classe. Pour visualiser un exemple d'utilisation conjointe des filtres et des requêtes, voir [Création de requêtes combinées](/docs/services/discovery?topic=discovery-query-concepts#building-combined-queries). Les filtres peuvent également être utilisés dans des agrégations.

Lorsque vous écrivez une requête incluant à la fois un paramètre `filter` et un paramètre `aggregation`, `query` ou `natural_language_query`, le paramètre `filter` est exécuté en premier, puis le paramètre `aggregation`, `query` ou `natural_language_query` s'exécute en parallèle.

Avec une requête simple, en particulier dans le cas d'un petit ensemble de données, les paramètres `filter` et `query` renvoient souvent des résultats absolument identiques ou similaires. Si les appels `filter` et `query` renvoient des résultats similaires, et que l'ordre de pertinence des réponses n'est pas requis, il est préférable d'utiliser un appel filter car ce type d'appel est plus rapide et il est mis en cache. Grâce à la mise en cache, la prochaine fois que vous effectuerez cet appel, vous obtiendrez une réponse beaucoup plus rapidement, en particulier dans un ensemble de données volumineux.

## aggregation
{: #aggregation}

Les requêtes d'agrégation renvoient un nombre de documents correspondant aux valeurs d'un ensemble de données. Par exemples, des mots clés supérieurs, un sentiment global d'entités, etc. Pour obtenir la liste complète des options d'agrégation, voir [Tableau d'agrégations](/docs/services/discovery?topic=discovery-query-aggregations#query-aggregations). Ces agrégations sont écrites à l'aide du [langage de requête {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-query-operators#query-operators). 

## natural_language_query
{: #nlq}

Une requête natural_language_query vous permet d'effectuer des requêtes exprimées en langage naturel, telles que celles pouvant être reçues de la part d'un utilisateur final dans une interface conversationnelle ou de texte libre. Par exemple, "IBM Watson in healthcare". Le paramètre utilise toute l'entrée en tant que texte de requête. Il ne reconnaît **pas** les opérateurs. Le paramètre `natural_language_query` active des fonctions, telles que la recherche de passage et la formation pour la pertinence. Toutes les collections privées renvoient dans la plupart des cas un score `confidence` dans les résultats de requête. Pour plus d'informations, voir [Scores de confiance](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence). La longueur maximale de chaîne de requête pour une requête en langage naturel est de `2048`.

**Paramètres de structure**

Les paramètres de structure définissent le contenu et l'organisation des documents dans l'objet JSON renvoyé. Cela inclut le nombre de résultats renvoyés, l'endroit à partir duquel les documents de l'ensemble de résultats doivent être renvoyés, le mode de tri de l'ensemble de résultats, les zones à renvoyer pour chaque document, le retrait ou non des documents en double et l'extraction ou non des passages pertinents de l'ensemble de résultats. Les paramètres de structure n'ont aucun impact sur les documents qui font partie de l'intégralité de l'ensemble de résultats.

## count
{: #count}

Nombre de documents qui doivent être renvoyés dans la réponse. La valeur par défaut est `10`. Le maximum pour les valeurs `count` et `offset` spécifiées conjointement dans une requête est `10000`.

## offset
{: #offset}

Nombre de résultats de requête qui doit être ignoré au début. Par exemple, si le nombre total de résultats renvoyés est 10, et que la valeur de décalage est 8, les deux derniers résultats sont renvoyés. La valeur par défaut est `0`. Le maximum pour les valeurs `count` et `offset` utilisées conjointement dans une requête est `10000`.

## return
{: #return}

Liste des parties de la hiérarchie de documents à renvoyer, séparées par des virgules. N'importe quelle hiérarchie de documents est une valeur valide.

## sort
{: #sort}

Liste des zones du document à trier, séparées par des virgules. Vous pouvez éventuellement spécifier un sens de tri en associant à la zone un préfixe `-` pour l'ordre décroissant ou un préfixe `+` pour l'ordre croissant. L'ordre croissant est le sens de tri par défaut.

Le paramètre `sort` est actuellement disponible pour être utilisé uniquement avec l'API ; il n'est pas disponible pour être utilisé avec les outils.

## bias
{: #bias}

Ajuste les résultats de recherche de façon à tendre vers certains résultats, par exemple les documents publiés le plus récemment. `bias` doit être défini sur une zone de type `date` ou de type `number`, par exemple `bias=publication_date` ou `bias=field_1`.  Quand une zone de type `date` est spécifiée, les résultats renvoyés pencheront vers des valeurs plus proches de la date en cours. Quand une zone de type `number` est spécifiée, les résultats renvoyés pencheront vers des valeurs de zone plus élevées. Ce paramètre ne peut pas être utilisé dans la même requête que le paramètre `sort`.

Le paramètre `bias` est actuellement disponible uniquement ou une utilisation avec l'API, il n'est pas disponible via les outils.

## passages
{: #passages}

Valeur booléen qui spécifie si le service renvoie un ensemble des passages les plus pertinents à partir des documents renvoyés par une requête qui utilise le paramètre `natural_language_query`. Les passages sont générés par des algorithmes Watson sophistiqués afin de déterminer les meilleurs passages de texte à partir de tous les documents renvoyés par la requête. La valeur par défaut est `false`.

Le paramètre `passages` ne peut être utilisé que sur des collections privées. Il ne peut pas être utilisé sur la collection {{site.data.keyword.discoverynewsfull}}.
{: tip}

{{site.data.keyword.discoveryshort}} tente de renvoyer des passages qui commencent et se terminent respectivement au début et à la fin d'une phrase, à l'aide de la détection des limites de phrase. Pour cela, il commence par rechercher des passages de longueur à peu près équivalente à celle spécifiée dans le paramètre [`passages.characters`](/docs/services/discovery?topic=discovery-query-parameters#passages_characters) (`400`, par défaut). Ensuite, il développe chaque passage jusqu'à deux fois la longueur spécifiée afin de renvoyer des phrases complètes. Si votre paramètre `passages.characters` est court et/ou les phrases de vos documents sont très longues, il se peut que les limites de phrase ne soient pas suffisamment proches pour qu'une phrase complète puisse être renvoyée sans parcourir deux fois la longueur demandée. Dans ce cas, {{site.data.keyword.discoveryshort}} reste dans la limite correspondant à deux fois la valeur du paramètre `passages.characters`, par conséquent, le passage renvoyé n'inclura pas les phrases complètes et ignorera le début et/ou la fin.

Etant donné que les ajustements des limites de phrase développent la taille des passages, vous constaterez une augmentation significative de la longueur moyenne des passages. Si l'espace sur l'écran de votre application est limité, vous souhaiterez peut-être définir une valeur plus petite pour le paramètre `passages.characters` et/ou tronquer les passages qui sont renvoyés par {{site.data.keyword.discoveryshort}}. La détection des limites de phrase fonctionne pour toutes les langues prises en charge et utilise une logique spécifique aux langues.

Le paramètre `passages` renvoie des passages correspondants (`passage_text`), la valeur `score`, la valeur `document_id`, le nom de la zone à partir de laquelle le passage a été extrait (`field`) et les caractères de début et de fin du texte du passage dans la zone (`start_offset` et `end_offset`), comme illustré dans l'exemple ci-après. La requête est affichée dans la partie supérieure de l'exemple.

```bash
 curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-06-25&natural_language_query='Hybrid%20cloud%20companies'&passages=true"
```
{: pre}

L'objet JSON renvoyé est au format suivant :

```json
 {
   "matching_results":2,
   "passages":[
     {
       "document_id":"ab7be56bcc9476493516b511169739f0",
       "passage_score":15.230205287402338,
       "passage_text":"a privately held company that provides hybrid cloud recovery, cloud migration and business continuity software for enterprise data centers and cloud infrastructure."
       "start_offset":120
       "end_offset":300
       "field":"text"       
     },
     {
       "passage_text":"Disaster Recovery Services for Hybrid Cloud</title></head>\n<body>\n\n\n<p>Published: Thu, 27 Oct 2016 07:01:21 GMT</p>\n"
       "passage_score":10.153470191601558,
       "document_id":"fbb5dcb4d8a6a29f572ebdeb6fbed20e",              
       "start_offset":70
       "end_offset":120
       "field":"html"
     },
  ...
```
{: codeblock}                        

### passages.fields
{: #passages_fields}

Liste des zones de l'index dont les passages seront tirés, séparées par des virgules. Si ce paramètre n'est pas spécifié, toutes les zones de niveau supérieur seront incluses.

### passages.count
{: #passages_count}

Nombre maximal de passages à renvoyer. La recherche peut renvoyer un nombre inférieur de passages en fonction du nombre total de passages trouvés. La valeur par défaut est `10`. La valeur maximale est `100`.

### passages.characters
{: #passages_characters}

Nombre approximatif de caractères qu'un passage doit comporter. La valeur par défaut est `400`. La valeur minimale est `50`. La valeur maximale est `2000`. La longueur des passages renvoyés peut être jusqu'à deux fois supérieure à la longueur demandée (si nécessaire) afin que les passages commencent et se terminent sur les limites de phrase.

## highlight
{: #highlight}

Valeur booléenne qui spécifie si la sortie renvoyée inclut un objet `highlight` dans lequel les clés sont des noms de zone et les valeurs sont des tableaux qui contiennent des segments de texte correspondant à une requête et mis en évidence par la balise `*` HTML.

La sortie spécifie l'objet `highlight` après l'objet `enriched_text`, comme illustré dans l'exemple suivant :

```bash
curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-06-25&natural_language_query=Hybrid%20cloud%20companies&highlight=true"
```
{: pre}

L'objet JSON renvoyé est au format suivant :

```json
{
   "highlight": {
     "extracted_metadata.title": [
       "IBM to Acquire Sanovi Technologies to Expand Disaster Recovery Services for <em>Hybrid</em> <em>Cloud</em>"
       ],
     "enriched_text.concepts.text": [
       "Privately held <em>company</em>",
       "<em>Cloud</em> computing"
       ],
     "text": [
       " Sanovi Technologies, a privately held <em>company</em> that provides <em>hybrid</em> <em>cloud</em> recovery, <em>cloud</em> migration",
       "IBM to Acquire Sanovi Technologies to Expand Disaster Recovery Services for <em>Hybrid</em> <em>Cloud</em>\n\nPublished",
       " undergoing digital and <em>hybrid</em> <em>cloud</em> transformation.\n\nURL: http://www.ibm.com/press/us/en/pressrelease/50837.wss",
       " and business continuity software for enterprise data centers and <em>cloud</em> infrastructure. Adding"
       ],
     "enriched_text.categories.label": [
       "/business and industrial/<em>company</em>/bankruptcy"
       ],
     "enriched_text.entities.type": [
       "<em>Company</em>"
       ],
     "html": [
       " Technologies, a privately held <em>company</em> that provides <em>hybrid</em> <em>cloud</em>\n recovery, <em>cloud</em> migration and business",
       " Disaster Recovery Services for <em>Hybrid</em> <em>Cloud</em></title></head>\n<body>\n\n\n<p>Published: Thu, 27 Oct 2016 07:01",
       " digital and <em>hybrid</em> <em>cloud</em> transformation.</p>\n<p>URL: http://www.ibm.com/press/us/en/pressrelease/50837.wss</p>\n\n\n\n</body></html>",
       " continuity software for \nenterprise data centers and <em>cloud</em> infrastructure. Adding these \ncapabilities"
       ]
   }
}
```
{: codeblock}

## deduplicate
{: #deduplicate}

 Fonctionnalité bêta qui exclut les documents en double des résultats d'une requête de collection {{site.data.keyword.discoverynewsfull}} en fonction de la zone `title`. Voir [Exclusion des documents en double dans les résultats de requête](/docs/services/discovery?topic=discovery-query-parameters#deduplication).

### deduplicate.field
{: #deduplicate_field}

Fonctionnalité bêta qui exclut les documents en double des résultats de votre requête en fonction de la zone `{field}` spécifiée. Voir [Exclusion des documents en double dans les résultats de requête](/docs/services/discovery?topic=discovery-query-parameters#deduplication).

### Exclusion des documents en double dans les résultats de requête
{: #deduplication}

Si vous exécutez une requête sur la collection {{site.data.keyword.discoverynewsfull}} ou si votre collection de données privées contient plusieurs documents identiques ou quasiment identiques, vous pouvez exclure la plupart de ces documents de vos résultats de requête en utilisant le dédoublonnage de document.

**Remarque :** pour l'instant, le dédoublonnage de document est pris en charge uniquement en tant que fonctionnalité bêta. Pour plus d'informations, voir la section [Fonctionnalités bêta](/docs/services/discovery?topic=discovery-release-notes#beta-features) dans la rubrique Notes sur l'édition. Cette fonction bêta est actuellement prise en charge uniquement en anglais ; voir [Support de langue](/docs/services/discovery?topic=discovery-language-support#feature-support) pour plus de détails.

**Remarque :** chaque requête est dédoublonnée de façon indépendante, car le dédoublonnage entre les décalages n'est pas pris en charge.

Le dédoublonnage est effectué après l'extraction des `passages` et le calcul des agrégations, par conséquent, si vous incluez le paramètre `passages` dans votre requête, les passages seront renvoyés de tous les documents dans les résultats de requête, avant le dédoublonnage. Si vous exécutez une agrégation et une requête en même temps, les résultats d'agrégation incluront des données provenant de tous les documents renvoyés, avant le dédoublonnage.

Le dédoublonnage est effectué uniquement sur les zones renvoyées. Si vous choisissez de spécifier `return=` dans votre requête, ajoutez la zone sur laquelle le dédoublonnage doit porter.

Pour appliquer le dédoublonnage, utilisez la syntaxe ci-après dans votre requête.  Remplacez `{field}` par le nom de la zone sur laquelle le dédoublonnage doit porter. La zone `{field}` spécifiée doit être une chaîne, telle que `title`.

```
&deduplicate.field={field}
```
{: codeblock}

Lors du dédoublonnage, la réponse JSON inclut `"duplicates_removed": x`, où `x` est le nombre de documents retirés des résultats.

#### Dédoublonnage de documents dans Watson Discovery News
{: #deduplicatewds}

Les articles de journal peuvent être syndiqués vers plusieurs organes de presse. {{site.data.keyword.discoverynewsfull}} sélectionnera chacun d'eux, générant ainsi des articles en double. Cela signifie qu'une requête sur {{site.data.keyword.discoverynewsfull}} peut potentiellement renvoyer plusieurs articles identiques ou quasiment identiques dans les résultats de requête. Le dédoublonnage permet de retirer la plupart des articles en double de vos requêtes de recherche.

{{site.data.keyword.discoveryshort}} effectue le dédoublonnage en utilisant une correspondance approximative sur la zone `title`, par conséquent, une zone n'a pas besoin d'être spécifiée.

Pour appliquer le dédoublonnage, utilisez le paramètre ci-après dans votre requête. Cette requête effectue automatiquement un dédoublonnage sur la zone `title` dans{{site.data.keyword.discoverynewsfull}}.

```bash
&deduplicate=true
```
{: codeblock}

Si vous préférez effectuer un dédoublonnage sur une zone autre que `title`, utilisez la syntaxe ci-après dans votre requête. Remplacez `{field}` par le nom de la zone sur laquelle le dédoublonnage doit porter. La zone `{field}` spécifiée doit être une chaîne.

```bash
&deduplicate.field={field}
```
{: codeblock}

## collection_ids
{: #collection_ids}

Liste des collections de l'environnement qui fera l'objet d'une requête, séparées par des virgules. Ce paramètre est valide uniquement avec la méthode`environments/{environment_id}/query?` . Pour plus d'informations, voir [Exécution d'une requête sur plusieurs collections](/docs/services/discovery?topic=discovery-query-concepts#multiple-collections).

```bash
&collection_ids={id1},{id2}
```
{: codeblock}

## similar
{: #similar}

La similarité de documents identifie les documents similaires aux documents répertoriés au paramètre `similar.document_ids`. Il est possible d'affiner encore davantage en spécifiant les zones à prendre en considération pour la comparaison à l'aide des paramètres `similar.fields`. La valeur par défaut est `false`. Pour plus d'informations, voir [Similarité de documents](/docs/services/discovery?topic=discovery-query-concepts#doc-similarity).

```bash
&similar=true
```
{: codeblock}

### similar.document_ids
{: #similar_document_ids}

Liste d'ID document séparés par des virgules, qui sera utilisée comme base à la recherche de documents similaires. Ce paramètre est obligatoire si le paramètre `similar` est défini sur `true`.

```bash
&similar.document_ids={id1},{id2}
```
{: codeblock}

### similar.fields
{: #similar_fields}

Liste facultative de zones séparées par des virgules, qui sera utilisée pour comparer des documents afin de trouver les documents similaires. Ce paramètre peut uniquement être utilisé conjointement avec le paramètre `similar.document_ids`.

```bash
&similar.fields={field1},{field2}
```
{: codeblock}
