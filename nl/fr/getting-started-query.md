---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-02-06"

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

# Initiation à l'écriture de requêtes
{: #getting-started-with-querying}

Dans ce tutoriel, vous allez apprendre à écrire différents types de requête dans le langage de requête {{site.data.keyword.discoveryshort}}.
{: shortdesc}

Pour plus d'informations sur l'écriture de requêtes, voir :
- [Concepts de requête](/docs/services/discovery?topic=discovery-query-concepts#query-concepts)
- [Référence de requête](/docs/services/discovery?topic=discovery-query-reference#query-reference) (comprend la liste des paramètres, opérateurs et agrégations disponibles dans le langage de requête {{site.data.keyword.discoveryshort}})

Ces exemples de requête sont créés à l'aide des outils {{site.data.keyword.discoveryshort}}. Si vous souhaitez utiliser l'API à la place, ajoutez les paramètres de requête à votre appel d'API. Pour plus d'informations et pour visualiser des exemples, voir la section Queries du document[API Reference ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery#query-your-collection){: new_window}.

Vous pouvez également écrire des requêtes en langage naturel (par exemple, "IBM Watson partnerships") à l'aide des outils {{site.data.keyword.discoveryshort}}. Ce tutoriel se concentre principalement sur l'écriture des requêtes à l'aide du langage de requête {{site.data.keyword.discoveryshort}} car vous pouvez avoir besoin d'une requête structurée, et les filtres et les agrégations doivent être écrits en langage de requête {{site.data.keyword.discoveryshort}}.
{: tip}

## Avant de commencer
{: #querying-before-you-begin}

Accédez à l'écran **Manage data**, créez une collection nommée Communiqués de presse {{site.data.keyword.IBM_notm}} puis ajoutez-y quatre documents : <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download> test-doc2.html <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe"></a> et <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe"></a>

Dans certains navigateurs, les liens s'ouvrent dans une nouvelle fenêtre au lieu d'être sauvegardés localement. Dans ce cas, sélectionnez `Save As` dans le menu `File` de votre navigateur pour sauvegarder une copie du fichier.
{: tip}

## Etape 1 : Tour d'horizon du schéma de données Discovery
{: #querying-step1}

Commençons par découvrir l'objet JSON {{site.data.keyword.discoveryshort}}. Pour comprendre comment créer une requête à l'aide du langage de requête {{site.data.keyword.discoveryshort}}, il est utile de connaître l'objet JSON produit par {{site.data.keyword.discoveryshort}} après que celui-ci a enrichi les documents de votre collection.

1.  [Lancez les outils {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-getting-started#launch-the-tooling). Sur l'écran **Manage data**, choisissez la collection {{site.data.keyword.IBM_notm}} Press Releases.

1.  Passez en revue les renseignements découverts par Watson dans vos documents enrichis.

    -  **Sentiment Analysis** affiche la répartition en pourcentage des documents marqués comme positifs, neutres et négatifs découverts par l'enrichissement Sentiment Analysis.
    -  **Entity Extraction** affiche les personnes, les lieux et les organisations découverts dans vos documents par l'enrichissement Entity Extraction.
    -  **Category Classification** affiche les taxonomies hiérarchiques découvertes dans vos documents par l'enrichissement Category Classification.
    -  **Concept Tagging** affiche les concepts découverts dans vos documents par l'enrichissement Concept Tagging.

1.  Pour découvrir le schéma de données de vos documents, examinons l'écran **View data schema**. Cet écran affiche de deux manières différentes les zones et les valeurs contenues dans vos documents transformés : par document (**vue de document**) ou par zone (**vue de collection**). La **vue de collection** affiche toutes les zones de votre collection.

    Cliquez sur l'icône **View data schema** se trouvant à gauche. Dans la section **Collection view**, sous `enriched_text`, se trouvent les enrichissements que vous avez appliqués à votre collection. Cliquez sur `categories`, `concepts`, `entities` et `sentiment` pour voir de quelle façon votre collection a été enrichie avec des connaissances Watson.

Si votre requête ne renvoie aucun résultat et vous pensez qu'elle aurait dû produire des résultats, remplacez la zone/valeur de votre requête par une zone/valeur que vous pouvez vérifier dans le schéma de données.
{: tip}    

## Etape 2 : Création d'une requête de base
{: #querying-step2}

Commençons par écrire une requête qui permettra de trouver le concept `Cloud computing` dans votre collection :

1.  Cliquez sur l'icône **Build queries** ![Icône Query](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> pour ouvrir la page de requête. Sélectionnez la collection {{site.data.keyword.IBM_notm}} Press Releases, puis cliquez sur **Get started**.
1.  Sur l'écran **Build queries**, cliquez sur **Search for Documents**, puis sur **Use the {{site.data.keyword.discoveryshort}} Query Language**, puis :
    - Cliquez sur la liste déroulante **Field** et choisissez `enriched_text.concepts.text`, pour **Operator** choisissez `contains`, puis entrez `Cloud computing` dans **Value**. La requête `enriched_text.concepts.text:Cloud computing` s'affichera sous le **générateur de requête visuelle**.

    - Vous pouvez aussi cliquer sur **Edit in query language**, puis sur **Use the {{site.data.keyword.discoveryshort}} Query Language**. Entrez `enriched_text.concepts.text:"Cloud computing"` dans la zone **Enter query here**.

1.  Cliquez sur **Run query**. Un résultat devrait apparaître (`"matching_results": 1`). Copiez le contenu du lien **Query URL** situé en haut de l'onglet **Summary** ou **JSON** afin de l'utiliser dans votre application.

**Bonus :** sous **More options**, vous avez la possibilité d'activer l'extraction de passage avec le bouton d'option **Include relevant passages**. Les passages sont des extraits pertinents et courts issus des documents entiers renvoyés par votre requête. Ces passages ciblés sont extraits des zones `text` contenues dans les documents de votre collection. Pour plus d'informations, voir [Passages](/docs/services/discovery?topic=discovery-query-parameters#passages). L'extraction de passage n'est pas disponible pour la collection {{site.data.keyword.discoveryshort}} News.

Si vous souhaitez extraire un petit nombre de requêtes préconfigurées, cliquez sur le bouton **Use a sample query**.
{: tip}

## Etape 3 : Expérimentation de différentes requêtes
{: #querying-step3}

Essayez les requêtes suivantes :

Pour que tous les documents comportant un sentiment positif (`positive`) soient renvoyés, cliquez sur **Search for Documents**, **Use the {{site.data.keyword.discoveryshort}} Query Language**, puis :
-  Cliquez sur la liste déroulante **Field** et choisissez `enriched_text.sentiment.document.label`, pour **Operator**, choisissez `contains`, puis entrez `positive` dans **Value**.  

   La requête `enriched_text.sentiment.document.label:positive` s'affichera sous le **générateur de requête visuelle**.

Pour que tous les documents comportant la catégorie `health and fitness` soient renvoyés, cliquez sur **Search for Documents**, **Use the {{site.data.keyword.discoveryshort}} Query Language**, puis :
-  Cliquez sur la liste déroulante **Field** et choisissez `enriched_text.categories.label`, pour **Operator** choisissez `is`, puis entrez `"health and fitness"` dans **Value**.

   La requête `enriched_text.categories.label::"health and fitness"` s'affichera sous le **générateur de requête visuelle**. L'opérateur `::` indique une correspondance exacte.

Pour que tous les documents comportant l'entité `IBM`, mais pas l'entité `Watson`, soient renvoyés, cliquez sur **Search for Documents**, **Use the {{site.data.keyword.discoveryshort}} Query Language**, puis :
-  Cliquez sur la liste déroulante **Field** et choisissez `enriched_text.entities.text`, pour **Operator**, choisissez `contains`, puis entrez `IBM` dans **Value**. Cliquez sur **Add rule**, puis, pour **Field**, choisissez `enriched_text.entities.text`, pour **Operator**, choisissez `does not contain`, puis entrez `Watson` dans **Value**.

   La requête `enriched_text.entities.text:IBM,enriched_text.entities.text:!Watson` s'affichera sous le **générateur de requête visuelle**. L'opérateur  `:!` spécifie "ne contient pas".

## Etape 4 : Création d'une requête combinée
{: #querying-step4}

Vous pouvez combiner des paramètres de requête afin de créer des requêtes davantage ciblées. Essayons d'utiliser en même temps les paramètres `filter` et `query` pour renvoyer des documents concernant les acquisitions {{site.data.keyword.IBM_notm}}. Le paramètre filter permet de limiter les résultats aux documents qui mentionnent `IBM`, et le paramètre query permet de renvoyer tous les résultats relatifs à `acquisitions`, par ordre de pertinence.

1.  Cliquez sur l'icône de création de requêtes ![Icône de requête](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> pour ouvrir la page de requête. Sélectionnez la collection {{site.data.keyword.IBM_notm}} Press Releases, puis cliquez sur **Get started**.

1.  Sous **Filter which documents you query** :
    -  Cliquez sur la liste déroulante **Field** et choisissez `enriched_text.entities.text`, pour **Operator**, choisissez `contains`, puis entrez `IBM` dans **Value**.

       La requête `enriched_text.entities.text:IBM` permet de limiter les documents à ceux qui mentionnent l'entité `IBM`.

1.  Sous **Search for Documents**, cliquez sur **Use the {{site.data.keyword.discoveryshort}} Query Language**, puis :
    -  Cliquez sur la liste déroulante **Field** et choisissez `enriched_text.concepts.text`, pour **Operator**, choisissez `contains`, puis entrez `world wide web` dans **Value**.

       La requête `enriched_text.concepts.text:"world wide web"` renverra tous les documents qui comportent le concept `world wide web` et ces documents seront classés par ordre de pertinence.

1.  Cliquez sur **More options**, puis sur **Fields to return** et choisissez **Specify**. Sélectionnez `text`. De cette façon, la réponse sera limitée au texte des articles pertinents. Tout autre texte sera exclus.

1.  Cliquez sur **Run query**. Un seul document correspondant sera trouvé : `"matching_results": 1`

## Etape 5 : Création d'une agrégation
{: #querying-step5}

Les agrégations renvoient un groupe de valeurs de données. Par exemple, des mots clés principaux, des sentiments d'entités globaux, etc.

Essayez de créer cette agrégation. Elle renverra les 10 premiers concepts dans la collection {{site.data.keyword.IBM_notm}} Press Releases.

1.  Cliquez sur l'icône **Build queries** ![Icône Query](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> pour ouvrir la page de requête. Sélectionnez la collection {{site.data.keyword.IBM_notm}} Press Releases, puis cliquez sur **Get started**.

1.  Sous **Include analysis of your results** :
    -  Cliquez sur la liste déroulante **Output** et choisissez `Top values`, pour **Field**, choisissez `enriched_text.concepts.text`, puis entrez `10` dans **Count**.

       `Term` renverra les valeurs les plus courantes pour la zone `text` `concepts`. **Count** spécifie le nombre de résultats à renvoyer. La requête `term(enriched_text.concepts.text,count:10)` s'affichera sous le **générateur de requête visuelle**.   

1.  Cliquez sur **More options**, puis entrez `0` dans la zone **Number of documents to return**.

1.  Cliquez sur **Run query**. Les 10 premiers concepts s'afficheront dans les onglets **Summary** et **JSON**. Voici un exemple de l'onglet Summary :

## Etape 6 : Création d'une requête dans Watson Discovery News
{: #querying-step6}

{{site.data.keyword.discoverynewsshort}} est un fichier public qui a été pré-enrichi avec des renseignements cognitifs. Il est fourni avec {{site.data.keyword.discoveryshort}}. Pour plus d'informations sur cette collection, voir [Watson Discovery News](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news).

Vous ne pouvez pas ajuster la configuration de {{site.data.keyword.discoverynewsshort}}, former ou ajouter des documents à la collection {{site.data.keyword.discoverynewsshort}}. Regardez une démonstration illustrant ce que vous pouvez créer avec {{site.data.keyword.discoverynewsshort}} [en cliquant ici ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://discovery-news-demo.ng.bluemix.net/){: new_window}.

L'exemple de requête suivant renvoie les 10 premiers articles de {{site.data.keyword.discoverynewsfull}} concernant les Steelers de Pittsburgh et comportant un sentiment positif.

1.  Cliquez sur l'icône **Build queries** ![Icône Query](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> pour ouvrir la page de requête. Sélectionnez la collection {{site.data.keyword.discoverynewsshort}} et cliquez sur **Get started**. (Pour interroger les collections {{site.data.keyword.discoverynewsshort}} en espagnol, allemand ou coréen, vous devez d'abord cliquer sur l'icône ![Manage Data](/images/icon_yourData.png), puis sélectionner la langue appropriée dans la liste déroulante.)

1.  Sous **Search for documents**, cliquez sur **Use the {{site.data.keyword.discoveryshort}} Query Language**, puis :
    -  Cliquez sur la liste déroulante **Field** et choisissez `text`, pour **Operator**, choisissez `contains`, puis entrez `Pittsburgh Steelers` dans **Value**. Cliquez sur **Add rule**, puis cliquez sur la liste déroulante **Field** et choisissez `enriched_text.sentiment.document.label`, pour **Operator**, choisissez `contains`, puis entrez `positive` dans **Value**.

       La requête `text:"Pittsburgh Steelers",enriched_text.sentiment.document.label:"positive"` s'affichera sous le générateur **Visual Query Builder**.

1.  Cliquez sur **More options**, puis entrez `10` (valeur par défaut) dans la zone **Number of documents to return**.

1.  Cliquez sur **Run query**. Les 10 premiers articles concernant les Steelers de Pittsburgh et comportant un sentiment positif seront affichés.

**Remarque :** le nombre maximal de résultats pouvant être renvoyés pour une requête Watson Discovery News est `50`.

Les articles de journal peuvent être syndiqués vers plusieurs organes de presse. {{site.data.keyword.discoverynewsfull}} sélectionnera chacun d'eux, générant ainsi des articles en double. Cela signifie qu'une requête sur {{site.data.keyword.discoverynewsfull}} peut potentiellement renvoyer plusieurs articles identiques ou quasiment identiques dans les résultats de requête. Pour activer le dédoublonnage, sous **More options**, choisissez **Exclude duplicate results**. Pour en savoir plus sur cette fonction bêta, voir [Exclusion des documents en double dans les résultats de requête](/docs/services/discovery?topic=discovery-query-parameters#deduplication).
