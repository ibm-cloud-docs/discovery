---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-18"

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
{:download: .download}

# Initiation
{: #getting-started}

Dans ce bref tutoriel, nous allons vous présenter les outils {{site.data.keyword.discoveryshort}} et vous montrer comment créer une collection de données privées et comment effectuer des recherches dans cette dernière.
{: shortdesc}

Si vous préférez travailler dans l'API, voir [Initiation à l'API](/docs/services/discovery/getting-started.html).
{: tip}

## Avant de commencer
{: #before-you-begin}

Vous aurez besoin d'une instance de service pour commencer.

<!-- Remove the text marked `download` after there's no g-s tab in the catalog dashboard -->


Vous avez créé votre instance de service. Cliquez sur **Manage**, puis sur **Open tool**. Accédez à l'[étape 2](/docs/services/discovery/getting-started-tooling.html#create-a-collection).
{: download tip}

Si vous avez créé une instance de service {{site.data.keyword.discoveryshort}}, vous êtes prêt. Accédez à l'[étape 1](/docs/services/discovery/getting-started-tool.html#launch-the-tooling).

1.  Accédez à la page [{{site.data.keyword.discoveryshort}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.{DomainName}/catalog/services/discovery){: new_window} du catalogue {{site.data.keyword.Bluemix_notm}}.
1.  Inscrivez-vous pour un compte {{site.data.keyword.Bluemix_notm}} gratuite ou connectez-vous.
1.  Cliquez sur **Create**.


## Etape 1 : Lancement des outils
{: #launch-the-tooling}

Après que vous avez créé une instance du service {{site.data.keyword.discoveryshort}}, vous accédez au [tableau de bord {{site.data.keyword.Bluemix_notm}}](https://console.{DomainName}/dashboard). Cliquez sur votre instance de service {{site.data.keyword.discoveryshort}} pour accéder au tableau de bord du service {{site.data.keyword.discoveryshort}}.

Sur la page **Manage**, cliquez sur **Open tool**.

<!-- To do: Add screenshot for developer console -->

Si vous êtes invité à vous connecter aux outils, entrez vos données d'identification {{site.data.keyword.Bluemix_notm}}.

Si vous ne vous trouvez pas sur la page contenant les détails d'un projet pour le service {{site.data.keyword.discoveryshort}}, accédez à la page {{site.data.keyword.watson}} Developer Console [Projects ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.{DomainName}/developer/watson/projects) et sélectionnez le projet.
{: tip}

<!-- Remove this text after dedicated instances have the Developer Console: begin -->

{{site.data.keyword.Bluemix_dedicated_notm}} : sélectionnez votre instance de service dans le tableau de bord pour lancer les outils.

<!-- Remove this text after dedicated instances have the Developer Console: end -->

## Etape 2 : Création d'une collection
{: #create-a-collection}

Votre première étape dans les outils {{site.data.keyword.discoveryshort}} consiste à créer une collection de données.

Une collection regroupe certains de vos documents. *Pourquoi devrais-je avoir besoin de plusieurs collections ?* Il existe plusieurs raisons :

- Vous pouvez être amené à vouloir posséder plusieurs collections afin de séparer les résultats pour différents publics.
- Il peut arriver que les données soient très différentes, et dans ce cas, il ne serait pas logique qu'elles soient toutes ciblées par une requête.

Vous pouvez également utiliser la collection de données {{site.data.keyword.discoverynewsshort}} préenrichie publique qui est à votre disposition. Elle est prête à faire l'objet d'une requête et vous pouvez dès maintenant commencer à l'utiliser comme cible pour vos requêtes. Vous ne pouvez pas ajuster sa configuration ni ajouter de documents à{{site.data.keyword.discoverynewsshort}}.

1.  Cliquez sur ![Cog](images/icon_settings.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> et choisissez **Create environment**.
1.  Lorsque votre environnement est prêt, cliquez sur le bouton **Upload your own data**, puis vous pouvez donner un nom à votre nouvelle collection (**Name your new collection**).Entrez un nom pour votre collection et choisissez **Default Configuration** dans la liste **Select a configuration to apply** (vous pourrez changer de configuration ultérieurement).

Il existe une autre configuration disponible, nommée **Default Contract Configuration**, qui prend en charge Element Classification, et qui peut être utilisée pour extraire la partie prenante, la nature et la catégorie d'éléments dans des fichiers PDF. Voir [Element Classification](/docs/services/discovery/element-classification.html#element-collection) pour plus de détails. 

Vous pouvez également explorer des sources de données Box, Salesforce et Microsoft SharePoint Online avec les outils {{site.data.keyword.discoveryshort}}. Cliquez sur le bouton **Connect a data source** et consultez [Connexion à des sources de données](/docs/services/discovery/connect.html) pour plus d'informations.
{: tip}

## Etape 3 : Création d'une configuration personnalisée
{: create-custom-configuration}

Une fois votre collection créée, vous pourriez commencer tout de suite à télécharger du contenu à l'aide de la zone de téléchargement, mais nous souhaitons créer et tester une configuration personnalisée.

1.  Cliquez sur **Switch** en regard du nom de collection et choisissez **Create a new configuration**. Entrez un nom pour votre configuration et cliquez sur **Create**.
1.  Après avoir créé votre configuration, vous pouvez la personnaliser :
    1.  Téléchargez l'exemple de document <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe" class="style-scope doc-content"></a>.
    1.  Utilisez le panneau **Upload Sample Documents** pour télécharger l'exemple de document. Une fois l'exemple de document téléchargé, vous pouvez cliquer sur le lien correspondant au nom du document pour afficher la transformation.
1.  A présent, il est temps d'ajuster la configuration. Pour cette tâche, vous modifiez les enrichissements appliqués à chaque document :
    1.  Cliquez sur la section **Enrich** de la configuration. Examinez la sortie JSON générée qui figure sur la droite de l'écran. Faites défiler l'écran jusqu'à la section *enriched_text* ; vous constaterez qu'elle contient un grand nombre de *concepts*.
    1.  Ensuite, retirez l'enrichissement de texte nommé *concepts* en cliquant sur la lettre **X** qui le précède, puis cliquez sur **Apply & Save**.
    1.  Enfin, consultez à nouveau la sortie JSON. Vous constaterez qu'elle a changé et qu'elle ne contient plus *concepts*.

## Etape 4 : Téléchargement de vos documents
{: #upload-your-documents}

Lorsque vous êtes satisfait de la conversion personnalisée de votre exemple de document, il est temps de verser le contenu réel dans votre collection.

1. Téléchargez les trois exemples de document suivants :<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe" class="style-scope doc-content"></a>.
1.  Cliquez sur ![icône de fichier](images/icon_yourData.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> et sélectionnez votre collection.
1.  Assurez-vous que la configuration personnalisée que vous avez créée est répertoriée sous **Configuration**. Si tel n'est pas le cas, cliquez sur   **Switch** en regard du nom de configuration et sélectionnez-le.
1.  Cliquez sur le bouton **Upload documents** et commencez le téléchargement des quatre exemples de document test-doc1.html, test-doc2.html, test-doc3.html et test-doc4.html.
1.  Attendez que les documents soient tous téléchargés. Le statut de vos documents apparaît dans la section **Overview**.

## Etape 5 : Création d'une requête
{: #build-a-query}

1.  Cliquez sur l'![icône de requête](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> pour ouvrir la page de requête. Sélectionnez votre collection et cliquez sur **Get started**.
1.  Sur l'écran **Build queries**, cliquez sur **Search for documents**, puis sur **Use the {{site.data.keyword.discoveryshort}} Query Language** :
    - Pour rechercher les résultats comportant des entités nommées "IBM" :
        1.  Cliquez sur **Field** et sélectionnez `enriched_text.entities.text`. Sélectionnez `contains` pour **Operator** et `IBM` pour **Value**. La requête `enriched_text.entities.text:IBM` s'affiche dans le **générateur de requête visuelle**.
        1.  Cliquez sur **Run Query**. La requête renvoie 4 résultats.
    - Pour rechercher les résultats comportant des entités nommées "Watson" :
        1.  Cliquez sur **Field** et sélectionnez `enriched_text.entities.text`. Sélectionnez `contains` pour **Operator** et `watson` pour **Value**. La requête `enriched_text.entities.text:watson` s'affiche dans le **générateur de requête visuelle**.
        1.  Cliquez sur **Run Query**. La requête renvoie 2 résultats.
    - Pour rechercher les résultats comportant à la fois des entités "Watson" et des entités "Slack" :
        1.  Cliquez sur **Field** et sélectionnez `enriched_text.entities.text`. Sélectionnez `contains` pour **Operator** et `watson` pour **Value**. Cliquez sur **Add rule**, puis répétez vos sélections, mais choisissez `Slack` pour **Value**. La requête `enriched_text.entities.text:watson,enriched_text.entities.text:Slack` s'affiche dans le **générateur de requête visuelle**.
        1.  Cliquez sur **Run Query**. La requête renvoie 1 résultat.

    Cliquez sur **Edit in query language** pour créer des requêtes à l'aide du langage de requête {{site.data.keyword.discoveryshort}}. Pour en savoir plus sur le langage de requête {{site.data.keyword.discoveryshort}}, voir les rubriques [Référence de requête](/docs/services/discovery/query-reference.html) et [Concepts de requête](/docs/services/discovery/using.html).
1.  Les résultats de votre requête s'affichent dans la section **Results** :
    - L'onglet **Summary** fournit une présentation générale des résultats de la requête.
    - L'onglet **JSON** affiche les résultats JSON complets.

    Pour les requêtes affichées, l'onglet **Summary** affiche les passages de document (par ordre de pertinence), les noms des documents trouvés, puis les résultats par enrichissement. Les **passages** sont des extraits pertinents et courts issus des documents entiers renvoyés par votre requête.

    Le lien **Query URL** fourni sous les onglets **JSON** et **Summary** est prêt à être utilisé dans votre application.

    Vous pouvez également cliquer sur **Use natural language** et écrire une requête en langage naturel, telle que "IBM Watson partnerships". Pour en savoir plus sur les requêtes en langage naturel, voir [Requête en langage naturel](/docs/services/discovery/query-parameters.html#nlq).

    Watson peut être formé afin d'améliorer les résultats des requêtes en langage naturel. Voir [Amélioration de la pertinence des résultats à l'aide des outils](/docs/services/discovery/train-tooling.html).

    Ressources supplémentaires :
    - Pour en savoir plus sur le schéma de données de vos documents, cliquez sur l'icône **View Data Schema** ou sur l'onglet **JSON**. Pour plus d'informations, voir [Schéma de données Discovery](/docs/services/discovery/using.html#discovery-schema).
    - Si utilisez le langage de requête {{site.data.keyword.discoveryshort}} pour effectuer des modifications, cliquez sur les icônes **?** en regard de n'importe quelle zone **Enter query here** afin d'obtenir d'autres exemples.

## Etapes suivantes
{: #next-steps}

Vous disposez à présent d'une instance de service {{site.data.keyword.discoveryshort}} opérationnelle et remplie. Vous pouvez maintenant commencer à personnaliser votre collection en ajoutant d'autres documents et enrichissements et en personnalisant les paramètres de conversion.
