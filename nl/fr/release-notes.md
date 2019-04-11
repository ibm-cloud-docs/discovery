---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-02-08"

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

# Notes sur l'édition
{: #release-notes}

Les notes sur l'édition fournissent des informations relatives aux modifications apportées au service {{site.data.keyword.discoveryfull}} depuis l'édition précédente.
{: shortdesc}

## Gestion des versions d'API du service
{: #apiversioning}

Les demandes d'API nécessitent un paramètre de version qui prend une date au format `version=AAAA-MM-JJ`. Chaque fois que nous modifions l'API de manière irréversible, nous publions une nouvelle version mineure de l'API.

Envoyez le paramètre de version avec chaque demande d'API. Le service utilise la version d'API correspondant à la date que vous spécifiez ou la toute dernière version avant cette date. Ne laissez pas la date du jour par défaut. A la place, spécifiez une date correspondant à une version qui est compatible avec votre application et ne la changez pas tant que votre application n'est pas prête pour une version ultérieure.

Version en cours : `2019-01-01`.

## Fonctions bêta
{: #beta-features}

IBM va publier des services, des dispositifs et un support de langue classifiés en tant que fonctions bêta ou expérimentales. Ces fonctions peuvent être instables, ce qui signifie qu'elles peuvent être instables, qu'elle peuvent changer fréquemment et que leur commercialisation peut être arrêtée dans des délais rapides. Elles sont fournies afin de vous permettre d'évaluer leur fonctionnalité. Leur niveau de performance ou de compatibilité peut être différent de celui offert par les fonctions commercialisées partout. Elles n'ont pas été conçues pour être utilisées dans un environnement de production, et si vous passez outre cette recommandation, vous le faites à vos risques et périls.


## Modifications
{: #change-log}

Les nouvelles fonctions et modifications apportées au service et décrites ci-après sont disponibles.

## 10 février 2019
{: #10feb19}

- Ajout de l'option de connexion et de synchronisation avec IBM Cloud Object Storage. Cette source de données n'est pas disponible dans les environnements dédiés. Pour plus d'informations, voir [IBM Cloud Object Storage](/docs/services/discovery?topic=discovery-sources#connectcos).

## 4 février 2019
{: #4feb19}

Mise à jour de la disponibilité générale :

-  [Smart Document Understanding (SDU)](/docs/services/discovery?topic=discovery-sdu#sdu) est passé du statut bêta au statut de disponibilité générale (GA).
   -  L'annotation de table reste au statut bêta. Une instruction décrivant les fonctions bêta est disponible [ici](/docs/services/discovery?topic=discovery-release-notes#beta-features).
   -  Le bouton `Data settings` dans la partie supérieure droite de la fenêtre s'appelle désormais `Configure data`.
   -  Il n'est plus nécessaire de télécharger de document pour accéder au bouton `Configure data` (auparavant appelé `Data settings`).

La version bêta de SDU a été annoncée le [22 janvier 2019](/docs/services/discovery?topic=discovery-release-notes#22jan19).   
    
## 28 janvier 2019
{: #28jan19}

Plus aucune assistance n'est disponible pour Data Crawler si vous l'utilisez avec une source de données prise en charge par les connecteurs {{site.data.keyword.discoveryshort}}. Les connecteurs {{site.data.keyword.discoveryshort}} prennent en charge crawling Box, SharePoint, Salesforce, etc. Pour plus de détails, voir [Connexion à des sources de données](/docs/services/discovery?topic=discovery-sources#sources). Utilisez Data Crawler uniquement pour explorer les bases de données ou les partages de fichier. Dans tous les autres cas,  utilisez le connecteur {{site.data.keyword.discoveryshort}}. Pour télécharger un grand nombre de fichiers dans {{site.data.keyword.discoveryshort}}, vous pouvez utiliser [discovery-files ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/IBM/discovery-files){: new_window} sur GitHub.

## 22 janvier 2019
{: #22jan19}

- La version bêta de [Smart Document Understanding (SDU)](/docs/services/discovery?topic=discovery-sdu#sdu) constitue une nouvelle façon d'entraîner {{site.data.keyword.discoveryfull}} à extraire des zones personnalisées dans vos documents. Avec Smart Document Understanding, vous annotez les zones dans vos documents afin d'entraîner des modèles de conversion personnalisés. Une instruction décrivant les fonctions bêta est disponible [ici](/docs/services/discovery?topic=discovery-release-notes#beta-features).

L'éditeur SDU bêta est disponible uniquement pour les nouvelles collections qui contiennent des types de document pris en charge et auxquelles l'enrichissement Element Classification n'est pas appliqué. Les collections privées existantes utilisent la méthode de configuration d'origine.

Si vous utilisiez la version bêta fermée de Smart Document Understanding, n'importez pas de modèles créés au sein de cette dernière dans la version actuelle. Smart Document Understanding n'est pas actuellement disponible dans des environnements dédiés.

Les fonctions de l'éditeur SDU sont disponibles uniquement dans les outils {{site.data.keyword.discoveryshort}}, elles ne sont pas disponibles dans l'API.

## 15 janvier 2019
{: #15jan19}

Mises à jour d'Element Classification :
-  L'enrichissement Element Classification inclut des attributs, des catégories et des parties prenantes mis à jour dans la version d'API `2018-10-15` ou version ultérieure. Pour les mises à jour, voir [Analyse syntaxique de contrats](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing).

- La sortie de la méthode `/v1/element_classification` inclut désormais les éléments suivants :
    - Le tableau `parties` inclut désormais une zone `importance` qui indique si la partie prenante est une partie de type `Primary` ou `Unknown` (élément non principal).
    - Les tableaux `effective_dates`, `contract_amounts` et `termination_dates` incluent désormais chacun une zone `confidence_level` qui indique la valeur `High`, `Medium` ou `Low`.
    Pour plus d'informations, voir la rubrique présentant le [classification d'éléments](/docs/services/discovery?topic=discovery-output_schema#output_schema) ainsi que la rubrique [Analyse syntaxique de contrats](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing).

    Les outils {{site.data.keyword.discoveryshort}} n'utilisent pas encore la version d'API en cours, `2019-01-01` (ils utilisent actuellement `2018-08-01`). Vous ne verrez donc pas ces nouvelles zones dans la sortie Element Classification des outils {{site.data.keyword.discoveryshort}}.

## 10 janvier 2019
{: #10jan19}

Problème connu :

-  Si vous spécifiez un élément `customer-id` en utilisant la méthode de normalisation décrite dans [Spécification d'un `customer_id`](/docs/services/discovery?topic=discovery-sources#source_customer_id) et que vous tentez ensuite de supprimer des documents contenant cet élément `customer_id` en utilisant la méthode décrite dans [Suppression de données libellées](/docs/services/discovery?topic=discovery-information-security#deletingdata), le document source associé ne sera pas supprimé.

## 1 janvier 2019
{: #1jan19}

- La chaîne de version pour tous les appels d'API `2018-12-03` a été remplacée par `2019-01-01`. Cette version intègre désormais un nouveau statut d'ingestion de document, `pending`. Le statut `pending` sera renvoyé pour les documents ayant été acceptés mais dont le traitement n'a pas encore démarré. Auparavant, ces documents auraient eu le statut `processing`. Les outils {{site.data.keyword.discoveryshort}} n'utilisent pas encore cette version d'API (ils utilisent `2018-08-01`). Par conséquent, lorsque vous vérifiez le statut de document dans les outils {{site.data.keyword.discoveryshort}}, le statut `pending` ne sera pas renvoyé.

## 21 décembre 2018
{: #21dec18}

- Ajout de l'option de connexion et de synchronisation avec Microsoft SharePoint 2016 On-Premise. Cette source de données n'est pas disponible dans les environnements dédiés. Pour plus d'informations, voir [SharePoint 2016 On-Premise](/docs/services/discovery?topic=discovery-sources#connectsp_op).

- Ajout de la version bêta du connecteur Web Crawl, pouvant être utilisée pour la connexion, l'exploration et la synchronisation avec des sites Web. Cette source de données n'est pas disponible dans les environnements dédiés. Pour plus d'informations, voir [Web Crawl](/docs/services/discovery?topic=discovery-sources#connectwebcrawl). Une instruction décrivant les fonctions bêta est disponible [ici](/docs/services/discovery?topic=discovery-release-notes#beta-features).

- Les sources de données Microsoft SharePoint Online, Salesforce et Box sont désormais disponibles dans les environnements Premium. Elles ne sont pas disponibles dans les environnements dédiés.

## 17 décembre 2018
{: #17dec18}

- Ajout de la prise en charge complète pour l'italien. Pour plus d'informations, voir [Support de langue](/docs/services/discovery?topic=discovery-language-support#language-support).

## 14 décembre 2018
{: #14dec18}

Vous pouvez désormais créer des instances de service {{site.data.keyword.discoveryshort}} hébergées dans le centre de données de Londres sans syndication. Comme tous les emplacements, l'emplacement {{site.data.keyword.cloud}} de Londres (eu-gb) utilise l'authentification IAM (Identity and Access Management) à base de jetons. Toutes les nouvelles instances de service que vous créez à cet emplacement utilisent l'authentification IAM.

## 12 décembre 2018
{: #12dec18}

- Ajout de la possibilité de définir et de télécharger une liste de mots à exclure personnalisée. Les mots à exclure personnalisés sont implémentés avec l'API {{site.data.keyword.discoveryshort}}. Pour plus de détails, voir [Définition des mots à exclure](/docs/services/discovery?topic=discovery-query-concepts#stopwords). 

## 3 décembre 2018
{: #3dec18}

- Pour toutes les requêtes (à l'exception des requêtes de filtrage uniquement) écrites en utilisant la version d'API `2018-12-03` (ou une version ultérieure), {{site.data.keyword.discoveryshort}} renvoie désormais un score `confidence` dans l'ensemble de résultats de requête, même si la collection n'a pas été entraînée en utilisant une méthode de formation supervisée, comme [Formation de pertinence](//docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling) ou [Continuous Relevancy Training](/docs/services/discovery?topic=discovery-crt#crt). De plus, {{site.data.keyword.discoveryshort}} renvoie une zone `document_retrieval_strategy` qui indique la source du score `confidence` de `untrained`, `relevancy_training` ou `continuous_relevancy_training`. Pour plus d'informations, voir [Scores de confiance](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence).

- La chaîne de version pour tous les appels d'API `2018-10-15` a été remplacée par `2018-12-03`. Les outils {{site.data.keyword.discoveryshort}} n'utilisent pas encore cette version d'API (ils utilisent `2018-08-01`). Par conséquent, les requêtes créées en utilisant les outils {{site.data.keyword.discoveryshort}} ne renvoient pas de score `confidence` pour les collections non entraînées.

## 8 novembre 2018
{: #8nov18}

- {{site.data.keyword.discoveryshort}} a été lancé à l'emplacement `Tokyo` le 8 novembre 2018. Les environnements Premium et dédiés ne sont pas actuellement disponibles dans `Tokyo`.

## 30 octobre 2018
{: #30oct18}

- Le service {{site.data.keyword.discoveryshort}} prend désormais en charge l'authentification IAM à base de jetons dans toutes les régions. IAM utilise des jetons d'accès plutôt que les données d'identification du service pour l'authentification auprès d'un service. Pour plus d'informations sur l'utilisation de jetons IAM avec des applications nouvelles ou existantes, voir la mise à jour d'édition du [17 mai 2018](#17May18).

## 25 octobre 2018
{: #25oct18}

Le schéma de l'enrichissement [Element Classification](/docs/services/discovery?topic=discovery-element-classification#element-classification) a changé. Si vous souhaitez utiliser le schéma mis à jour, vous devez ingérer vos documents avec l'API, en utilisant la date de version `2018-10-15` ou ultérieure. Les outils {{site.data.keyword.discoveryshort}} n'utilisent pas encore cette version d'API (version actuellement utilisée : `2018-08-01`) ; aussi les documents ingérés à l'aide des outils {{site.data.keyword.discoveryshort}} seront-ils enrichis avec le schéma d'origine.

## 24 octobre 2018
{: #24oct18}

- Les requêtes {{site.data.keyword.discoverynewsfull}} affichent approximativement 50 mots de chaque article dans la zone JSON `text`. Ces mots seront désormais extraits des éléments mis en évidence alors qu'auparavant, les 50 premiers mots de l'article étaient affichés. Pour obtenir une explication des éléments mis en évidence, voir [highlight](/docs/services/discovery?topic=discovery-query-parameters#highlight). Il n'est pas nécessaire d'inclure explicitement les éléments mis en évidence dans votre requête pour activer ce comportement.

## 25 septembre 2018
{: #25sept18}

- Publication de Continuous Relevancy Training, qui utilise des interactions d'utilisateurs pour apprendre comment faire apparaître les résultats les plus pertinents. Est capable d'apprendre automatiquement à parti de comportement utilisateur, réduisant de manière significative l'effort requis pour améliorer le classement selon la pertinence des résultats.  Voir [Continuous Relevancy Training](/docs/services/discovery?topic=discovery-crt#crt) pour plus de détails.

- Ajout de la prise en charge d'API pour l'exécution de requêtes plus longues. Fait passer le nombre limite de caractères à 10 000, et permet d'augmenter le nombre de filtres dans les requêtes et d'effectuer des agrégations plus complexes. Voir la requête POST dans [API reference ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery#long-collection-queries){: new_window} et [API reference ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery#long-environment-queries){: new_window} pour plus de détails.

- Vous pouvez mettre à niveau votre plan Advanced à l'aide de l'API. Voir [Mise à niveau de votre plan](/docs/services/discovery?topic=discovery-upgrading-your-plan#switchadvanced) pour plus de détails. 

- L'enrichissement Element Classification a mis à jour les éléments classifiés, éléments de contrat, ainsi que les parties prenantes et tables identifiées. Voir [Element Classification](/docs/services/discovery?topic=discovery-element-classification#element-classification) pour les mises à jour.

- Ajout de la prise en charge complète pour le portugais brésilien. Pour plus d'informations, voir [Support de langue](/docs/services/discovery?topic=discovery-language-support#language-support).

- L'API de requête (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`) prend désormais en charge le paramètre `bias` qui permet de tendre vers certains résultats, par exemple les documents publiés le plus récemment. Pour plus d'informations, voir la méthode [Query your collection ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery#query-your-collection){: new_window} dans le document API Reference.

- Le fichier **Default Contract Configuration** fournit pour enrichir des collections pour [Element Classification](/docs/services/discovery?topic=discovery-element-classification#element-collection) présente un problème lié à la normalisation HTML. Une nouvelle configuration **Default Contract Configuration** est donc incluse dans la présente édition. Suivez la procédure ci-après pour appliquer la nouvelle **Default Contract Configuration** à vos collections.

     1. Déterminez quelles sont vos collections qui utilisent le fichier de configuration **Default Contract Configuration** ou une configuration personnalisée basée sur **Default Contract Configuration**.
     1. Notez les changements apportés aux configurations personnalisées basées sur **Default Contract Configuration**.
     1. Comme l'ancien fichier **Default Contract Configuration** doit être supprimé de votre environnement avant l'utilisation du nouveau, utilisez l'API [Delete configuration ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery#delete-a-configuration){: new_window} pour supprimer l'actuelle **Default Contract Configuration** associée à vos collections. Supprimez également toute configuration basée sur l'ancienne **Default Contract Configuration**.
     1. Vous pouvez à présent utiliser le nouveau fichier **Default Contract Configuration**. Pour chaque collection utilisant l'une de ces configuration, créez une nouvelle collection. Appliquez la nouvelle configuration **Default Contract Configuration** ou créez une nouvelle configuration personnalisée basée sur la nouvelle **Default Contract Configuration** à l'aide des notes que vous avez prises à l'étape 2.
     1. Téléchargez les fichiers précédemment ingérés dans les collections d'origine.
     1. Supprimez les anciennes collections.

## 15 août 2018
{: #15aug18}

- Deux nouveaux opérateurs de requête sont disponibles. `Exists` (`:*`) peut être utilisé pour renvoyer tous les résultats où la zone `field` spécifiée existe. `Does not exist` (`!*`) peut être utilisé pour renvoyer tous les résultats qui n'incluent pas la zone `field` spécifiée. Voir [Opérateurs de requête](/docs/services/discovery?topic=discovery-query-operators#query-operators) pour plus d'informations. 

## 2 août 2018
{: #2aug18}

- {{site.data.keyword.discoveryfull}} prend désormais en charge les collections en langue anglaise, espagnole, allemande, italienne, portugaise, française, arabe, coréenne et japonaise lors de la connexion et de la synchronisation de Box, Salesforce et SharePoint Online avec les outils {{site.data.keyword.discoveryshort}}. 

## 31 juillet 2018
{: #31jul18}
 
 - A compter du **1er août 2018**, {{site.data.keyword.discoveryfull}} possède une nouvelle structure de tarification. Il propose un modèle de tarification pus simple (les heures document ne font plus partie du calcul) et des tarifications à niveau pour les requêtes {{site.data.keyword.discoverynewsfull}}. En outre, le plan Standard a été retiré et le plan Lite a réduit les limites des requêtes de document et {{site.data.keyword.discoverynewsshort}}. Ces changements de tarification ne nécessitent aucune intervention de la part des utilisateurs {{site.data.keyword.discoverynewsshort}}. Pour plus de détails, voir [Plans de tarification {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans).
 
**Remarque :** La date de version de l'API a été mise à jour : `2018-08-01`. Pour bénéficier des nouvelles options de dimensionnement d'environnement (`LT`, `XS`, `S`, `MS`, `M`, `ML`, `L`, `XL`, `XXL`, `XXXL`), vous devez utiliser cette nouvelle date de version lors de la création d'environnements avec l'API. Les tailles d'environnement sont désormais de type `string` (précédemment le type était `integer`.)

## 27 juillet 2018
{: #27jul18}

- Publication de [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news) dans une langue supplémentaire : japonais (`collection_id`: `news-ja`). {{site.data.keyword.discoverynewsfull}} est également disponible en anglais, espagnol, allemand et coréen.

## 25 juin 2018
{: #25jun18}

- Ajout de l'option de connexion et de synchronisation avec des sources de données Salesforce, Microsoft SharePoint Online et Box. Ces sources de données ne sont pas disponibles dans les environnements Premium. Publication des API [Source Credential ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery#list-credentials){: new_window} et [Configuration ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery#add-configuration){: new_window} pour ces sources de données. 
  - {{site.data.keyword.discoveryfull}} prend en charge uniquement les collections en langue anglaise lors de la connexion et de la synchronisation de Box, Salesforce et SharePoint Online avec les outils {{site.data.keyword.discoveryshort}}. [Résolu](/docs/services/discovery?topic=discovery-release-notes#2aug18)
  - La taille limite du fichier document individuel pour Box, Salesforce et SharePoint Online est de 10 Mo.
- Ajout d'un nouveau tableau de bord Performance dans les outils {{site.data.keyword.discoveryshort}}. Voir [Affichage de métriques et amélioration des résultats de requête avec le tableau de bord Performance](/docs/services/discovery?topic=discovery-performance-dashboard#performance-dashboard). Le nouveau tableau de bord n'est pas disponible dans les environnements Premium ou Dedicated.
- Ajout de la prise en charge complète pour le japonais. Pour plus d'informations, voir [Support de langue](/docs/services/discovery?topic=discovery-language-support#language-support).

## 22 juin 2018
{: #22jun18}

- Publication de l'API Events and Feedback. Voir [API reference ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery#create-event){: new_window} pour plus d'informations.

## 11 juin 2018
{: #11jun18}

-  Pour les applications hébergées à Washington, DC (Est des Etats-Unis), le service prend désormais en charge l'authentification IAM (Identity and Access Management). IAM utilise des jetons d'accès plutôt que les données d'identification du service pour l'authentification auprès d'un service. Pour plus d'informations sur l'utilisation de jetons IAM avec des applications nouvelles ou existantes, voir la mise à jour d'édition du [17 mai 2018](#17May18).
-  Un élément de contrat supplémentaire est désormais pris en charge dans Element Classification : `Safety and Security`. Voir [Compréhension des éléments de contrat](/docs/services/discovery?topic=discovery-element-classification#contract-elements) pour plus de détails.

## 6 juin 2018
{: #6jun18}

- Les requêtes {{site.data.keyword.discoverynewsfull}} affichent désormais les 50 premiers mots de chaque article dans la zone JSON `text`. [Mise à jour](#24oct18)

## 5 juin 2018
{: #5jun18}

- Element Classification est désormais disponibles pour les abonnés à des plans Premium.
- L'évaluation `Low` pour `assurance` n'est plus disponible pour Element Classification.

## 31 mai 2018
{: #31may18}

- Ajout de la prise en charge complète pour le français. Pour plus d'informations, voir [Support de langue](/docs/services/discovery?topic=discovery-language-support#language-support).

## 30 mai 2018
{: #30may18}

- Correction d'un problème connu dans {{site.data.keyword.discoverynewsfull}}. Auparavant, il était possible lors de l'interrogation de {{site.data.keyword.discoverynewsshort}} de recevoir un nombre de documents incorrect car les documents dans d'autres langues étaient comptés avec ceux dans la langue demandée. Ce n'est plus le cas.
- Avec les collections créées à partir du `22 mai 2018`, {{site.data.keyword.discoveryshort}} renvoie désormais des résultats de requête incluant les caractères spéciaux pour les langues suivantes : anglais, allemand, français, néerlandais, italien et portugais. Si, par exemple, vous faites une requête pour `aqui`, vous recevrez à présent des résultats pour `aqui` et <code>aqu&iacute;</code>.

## 21 mai 2018
{: #21may18}

- Publication de [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news) dans une langue supplémentaire : allemand (`collection_id`: `news-de`). {{site.data.keyword.discoverynewsfull}} est également disponible en anglais, espagnol et coréen.

## 17 mai 2018
{: #17May18}

- Désormais, les requêtes {{site.data.keyword.discoverynewsfull}} affichent uniquement les 20 premiers mots de chaque article dans la zone JSON `text`.

-   Le service prend désormais en charge un nouveau processus d'authentification d'API pour les instances de service d'applications hébergées à Sydney (**au-syd**) à compter du 15 mai 2018. Les instances seront bientôt activées pour des applications hébergées dans d'autres régions. {{site.data.keyword.Bluemix}} est en cours de migration vers l'authentification IAM (Identity and Access Management) à base de jetons. IAM utilise des jetons d'accès plutôt que les données d'identification du service pour l'authentification auprès d'un service.

   A l'emplacement Sydney, vous utilisez des jetons d'accès IAM avec le service {{site.data.keyword.discoveryshort}} pour

    -   Les *nouvelles instances de service* créées après le 15 mai. Pour plus d'informations, voir [Authentification avec des jetons IAM](/docs/services/watson/getting-started-iam.html).
    -   Les *instances de service existantes* que vous migrez depuis Cloud Foundry vers un groupe de ressources géré par le contrôleur de ressources RC (Resource Controller). Les instances de service créées avant le 15 mai continuent à utiliser les données d'identification du service pour l'authentification tant que vous ne les migrez pas. Pour plus d'informations, voir [Migration des instances de service Cloud Foundry vers un groupe de ressources](/docs/resources/instance_migration.html).

    Toutes les instances de service nouvelles et existantes dans d'autres régions continuent d'utiliser les données d'identification du service (`apikey:{apikey_value}`) pour l'authentification.

### Utilisation d'un jeton d'accès IAM pour l'authentification
{: #iam-token}

Lorsque vous utilisez des jetons d'accès, vous vous authentifiez avant d'envoyer une demande au service {{site.data.keyword.discoveryshort}}.

1.  Procurez-vous une clé d'API sur IBM Cloud. Utilisez cette clé pour gérer un jeton d'accès IAM. Pour plus d'informations, voir [Comment obtenir un jeton IAM en utilisant une clé d'API de service {{site.data.keyword.watson}}](/docs/services/watson/getting-started-iam.html#iamtoken).
1.  Transmettez le jeton d'accès IAM au service {{site.data.keyword.discoveryshort}} en utilisant l'en-tête `Authorization`. Dans l'en-tête, indiquez que le jeton d'accès est un jeton `Bearer` en spécifiant `Authorization: Bearer {access_token}`.

    Le simple exemple cURL suivant utilise un jeton d'accès :

    ```bash
    curl -X GET
    --header "Authorization: Bearer eyJhbGciOiJIUz......sgrKIi8hdFs"
    "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    Pour plus d'informations, voir [Utilisation d'un jeton pour l'authentification](/docs/services/watson/getting-started-iam.html#use_token).

### Actualisation d'un jeton d'accès IAM
{: #iam-refreshing}

Les jetons d'accès IAM que vous générez possèdent la structure suivante. Vous utilisez la valeur de la zone `access_token` pour transmettre une demande authentifiée au service.

```javascript
{
  "access_token": "eyJhbGciOiJIUz......sgrKIi8hdFs",
  "refresh_token": "SPrXw5tBE3......KBQ+luWQVY=",
  "token_type": "Bearer",
  "expires_in": 3600,
  "expiration": 1473188353
}
```
{: codeblock}

La durée de vie des jetons d'accès est limitée. La zone `expires_in` indique la durée du jeton, dans le cas présent une heure. La zone `expiration` montre quand le jeton arrive à expiration sous la forme d'un horodatage UNIX indiquant le nombre de secondes depuis le 1er janvier 1970 (minuit UTC/GMT).

Dans votre application, vérifiez le délai d'expiration du jeton d'accès avant de l'utiliser pour faire votre demande authentifiée. S'il est arrivé à expiration, vous devez le régénérer avant de pouvoir l'utiliser. Vous utilisez la valeur de la zone `refresh_token` pour actualiser le jeton d'accès. Pour plus d'informations, voir [Actualisation d'un jeton](/docs/services/watson/getting-started-iam.html#refresh_token).


## 11 mai 2018
{: #11may18}

- Des détails concernant la sécurité des informations sont disponibles dans [Sécurité de l'information](/docs/services/discovery?topic=discovery-information-security#information-security).
- Le problème connu suivant concernant {{site.data.keyword.discoveryfull}} Knowledge Graph `query_entities` a été corrigé avec la mise à jour de version d'API `2018-05-04`. Ce correctif s'applique uniquement si des entités sont ingérées ou remplacées après la date du `2018-05-04`. Les entités peuvent être remplacées par réingestion des documents anciens ou par ingestion de nouveaux documents contenant ces entités. Si d'anciennes entités ne sont pas remplacées, `query_entities` renverra tout en majuscules avec la version d'API `2018-05-04`.
  - Tous les noms d'entité étaient précédemment convertis en casse mixte dans `query_entities`. Par exemple, le nom d'entité "IBM Corporation" était converti en "Ibm Corporation". Ce n'est plus le cas.

## 9 mai 2018
{: #9may18}

- Les exemples de document sont désormais stockés en local, dans le dossier local des données itinérantes de votre navigateur. Pour plus d'informations sur les exemples de document, voir [Téléchargement d'exemples de document](/docs/services/discovery?topic=discovery-configservice#uploading-sample-documents).

## 4 mai 2018
{: #4may18}

- Deux éléments de contrat supplémentaires sont désormais pris en charge dans Element Classification : Attributes et Provenance. Voir [Compréhension des éléments de contrat](/docs/services/discovery?topic=discovery-element-classification#contract-elements) pour plus de détails.

## 26 avril 2018
{: #26apr18}

- Le problème suivant d'ingestion a été corrigé : Dans certains cas où des `json_normalizations` et/ou `normalizations` post-enrichissement étaient spécifiées, il arrivait que les normalisations ne soient pas appliquées dans le bon ordre. Cela se traduisait par l'indexation des documents avec des valeurs de zone inattendues. Ce n'est plus le cas.
- La taille de fichier maximale pour un exemple de document est désormais de 1 Mo. La taille de fichier maximale était auparavant de 5 Mo.

## 12 avril 2018
{: #12apr18}

- Knowledge Graph : [Evidence](/docs/services/discovery?topic=discovery-kg#kg_evidence) et [Canonicalization and filtering](/docs/services/discovery?topic=discovery-kg#kg_canonicalization) (Canonisation et filtrage) sont désormais dans toutes les collections. Pour les collections créées avant `03-05-2018`, vous devrez réingérer vos documents pour utiliser ces fonctions. Auparavant, vous deviez créer une nouvelle collection et réingérer vos documents.

## 11 avril 2018
{: #11apr18}

- Deux catégories supplémentaires sont désormais prises en charge dans Element Classification : `Asset Use` et `Communication`. Voir [Compréhension des éléments de contrat](/docs/services/discovery?topic=discovery-element-classification#contract-elements) pour plus de détails.

## 2 avril 2018
{: #2apr18}

- Les exemples de document sont désormais supprimés automatiquement après 24 heures à la place d'un mois.

## 16 mars 2018
{: #16mar18}

- Ajout de la prise en charge complète pour l'allemand. Pour plus d'informations, voir [Support de langue](/docs/services/discovery?topic=discovery-language-support#language-support).

Outils {{site.data.keyword.discoveryshort}} :
- Une nouvelle configuration nommée **Default Contract Configuration** a été ajoutée pour la prise en charge d'Element Classification, et qui peut être utilisée pour extraire la partie prenante, la nature et la catégorie d'éléments dans des fichiers PDF. Voir [Element Classification](/docs/services/discovery?topic=discovery-element-classification#element-collection) pour plus de détails.

Mise à jour de la disponibilité générale :
- La segmentation de documentation est passée du statut bêta au statut GA. La limite de segmentation est passée à 250 segments. Elle n'est plus limitée à 50 segments par document. Voir [Segmentation de la documentation](/docs/services/discovery?topic=discovery-configservice#doc-segmentation) pour plus de détails.

Problème connu :
- Les caractères génériques ne fonctionnent pas dans les requêtes comportant des majuscules. Si, par exemple, vous indiquez la paire clé/zone `{"borrower": "GOVERNMENT OF INDIA"}`, `query-borrower:*ndia` renvoie des résultats mais `query-borrower:*NDIA` n'en renverra pas.

## 8 mars 2018
{: #8mar18}

- Ajout de plusieurs fonctions à la version bêta de {{site.data.keyword.discoveryfull}} Knowledge Graph. Dans la version bêta, la fonctionnalité [Knowledge Graph](/docs/services/discovery?topic=discovery-kg#kg) et les méthodes qui lui sont associées sont disponibles uniquement pour les instances de service abonnées aux plans **Advanced**, **Premium**, ainsi que tous les environnements **Dedicated**. Nouvelles fonctions :
  - [Entity similarity](/docs/services/discovery?topic=discovery-kg#kg_similarity) (Similarité d'entités)
  - [Evidence](/docs/services/discovery?topic=discovery-kg#kg_evidence)
  - [Canonicalization and filtering](/docs/services/discovery?topic=discovery-kg#kg_canonicalization) (Canonisation et filtrage)

## 7 mars 2018
{: #7mar18}

- Le problème connu suivant d'ingestion a été corrigé : entre le 28 février et le 6 mars, un faible pourcentage des documents ont été indexés avec uniquement les zones `id` et `extracted_metadata` (le reste du contenu des documents n'était pas indexé). Le problème sous-jacent a été corrigé ; néanmoins, vous devrez resoumettre pour ingestion tout document affecté. Il n'existe pas de moyen simple d'identifier les documents concernés.

## 5 mars 2018
{: #5mar18}

- Le problème connu suivant concernant {{site.data.keyword.discoveryfull}} Knowledge Graph a été corrigé avec la mise à jour de version d'API `2018-03-05`. Ce correctif s'applique uniquement aux collections nouvellement créées qui utilisent la mise à jour de version `2018-03-05`.  
  - Tous les noms de type d'entité et de type de relation étaient précédemment convertis en majuscules lors de l'ingestion. Par exemple, l'entité "GeoPoliticalEntity" était convertie en "GEOPOLITICALENTITY" et la relation "partOf" était convertie en "PARTOF". Ce n'est plus le cas.

## 1er mars 2018
{: #1mar18}

- Les limites d'[extension de requête](/docs/services/discovery?topic=discovery-query-concepts#query-expansion) ont été augmentées pour les plans Advanced et Premium (5 000 extensions de requête et 25 000 termes au total). Voir [Plans de tarification Discovery](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans) pour plus de détails.

## 28 février 2018
{: #28feb18}

- Les enrichissements {{site.data.keyword.alchemylanguageshort}} ont été dépréciés à la date du **1er mars 2018**. Pour plus d'informations sur la migration de collections et fichiers de configuration existants qui utilisent les enrichissements {{site.data.keyword.alchemylanguageshort}}, voir [Migration des enrichissements vers {{site.data.keyword.nlushort}}](/docs/services/discovery?topic=discovery-migrate-nlu#migrate-nlu).

## 23 février 2018
{: #23feb18}

- Ajout de la possibilité d'effectuer des requêtes par similarité de documents. Vous pouvez effectuer une requête pour des documents similaires par ID document, et éventuellement affiner les résultats de similarité en spécifiant des zones. Pour plus d'informations, voir [Similarité de documents](/docs/services/discovery?topic=discovery-query-concepts#doc-similarity).

- Le paramètre [`highlight`](/docs/services/discovery?topic=discovery-query-parameters#highlight) dans les résultats de requête a été étendu. Les résultats renverront des phrases complètes, classées en fonction de leur `score`.

## 21 février 2018
{: #21feb18}

- Auparavant, lors de l'ingestion de documents PDF, le `file_type` renvoyé lorsque des requêtes étaient exécutées sur des avis d'ingestion, dans l'objet `extracted_metadata` et depuis l'API de détails du document, était `html`. Ce n'est plus le cas. Le `file_type` renvoyé est désormais `pdf`. 

## 26 janvier 2018
{: #26jan18}

Outils {{site.data.keyword.discoveryshort}} :

- Ajout de la possibilité d'accès aux collections coréennes et espagnoles pour la pile [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news) dans les outils. Auparavant, ces collections pouvaient uniquement être interrogées via l'API.

## 23 janvier 2018
{: #23jan18}

- Ajout de la possibilité d'étendre la portée d'une requête - Vous pouvez, par exemple, étendre une requête "car" de façon à inclure "automobile" et "motor vehicle". En outre, vous pouvez remplacer les termes habituellement mal orthographiés, en remplaçant par exemple des requêtes pour "seabizcuit" par "seabiscuit." L'extension de requête est implémentée avec l'API {{site.data.keyword.discoveryshort}}. Voir [Extension de requête](/docs/services/discovery?topic=discovery-query-concepts#query-expansion) pour plus de détails.  

## 15 janvier 2018
{: #15jan18}

- {{site.data.keyword.discoverynewsfull}} Original a été retiré du service. Il a été remplacé le 31 juillet 2017 par une nouvelle version nommée {{site.data.keyword.discoverynewsfull}}. Pour des instructions sur la migration depuis {{site.data.keyword.discoverynewsfull}} Original vers la nouvelle version, voir [Migration à partir de Watson Discovery News Original](/docs/services/discovery?topic=discovery-migrate-bwdn#migrate-bwdn).

## 11 janvier 2018
{: #11jan18}

- Ajout de la prise en charge complète pour le coréen. Pour plus d'informations, voir [Support de langue](/docs/services/discovery?topic=discovery-language-support#language-support).

## 15 décembre 2017
{: #15dec17}

- L'enrichissement **Element Classification** a été publié. Il effectue l'analyse syntaxique d'éléments (phrases, listes, tables) contenus dans des documents constitutifs afin de classifier les catégories et les types importants. Pour plus d'informations, voir [Element Classification](/docs/services/discovery?topic=discovery-element-classification#element-classification). L'enrichissement Element Classification n'est pas disponible pour les instances de service abonnées au plan **Premium**. [Résolu](/docs/services/discovery?topic=discovery-release-notes#5jun18)
- Le support de langue de base pour le chinois simplifié et le néerlandais a été ajouté. Pour plus d'informations, voir [Support de langue](/docs/services/discovery?topic=discovery-language-support#language-support). Actuellement, les collections en chinois simplifié et en néerlandais doivent être créées à l'aide de l'API.
- Deux nouveaux paramètres relatifs à Data Crawler ont été ajoutés : `proxy_host_port` et `read-timeout`. Pour plus d'informations, voir [Configuration de Data Crawler](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-the-data-crawler).
- Les erreurs suivantes peuvent être générées lors de l'ingestion de documents PDF : [Résolu](/docs/services/discovery?topic=discovery-release-notes#21feb18)
  - Lorsqu'une requête est exécutée sur les avis d'ingestion, la valeur `html` est renvoyée pour la zone `file_type` relative aux documents PDF.
  - La zone `file_type` dans l'objet `extracted_metadata` de résultats pour les documents PDF a pour valeur `html`.
  - L'API des détails de document renvoie également la valeur `html` pour la zone `file_type` relative aux documents PDF.
- Si vous ingérez des données JSON, les tableaux de type mixte ne sont pas pris en charge.  

Outils {{site.data.keyword.discoveryshort}} :

- Un générateur de requête visuelle a été ajouté pour la version bêta de {{site.data.keyword.discoveryfull}} Knowledge Graph. Voir [Exécution de requêtes sur un graphique Knowledge Graph à l'aide des outils {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-kg#querying-kg). 

## 30 novembre 2017
{: #30nov17}

- La version bêta de {{site.data.keyword.discoveryfull}} Knowledge Graph a été publiée. Elle fournit des noeuds finaux permettant d'exécuter des requêtes sur des entités et des relations figurant dans des documents. Cela inclut des recherches contextuelles et un classement par pertinence. Cette fonction bêta est disponible uniquement pour les utilisateurs abonnés au plan **Advanced**. Elle n'est pas disponible dans les environnements **Dedicated**. [Résolu](/docs/services/discovery?topic=discovery-release-notes#8mar18) Voir [{{site.data.keyword.discoveryfull}} Knowledge Graph](/docs/services/discovery?topic=discovery-kg#kg) pour plus d'informations.  Une instruction décrivant les fonctions bêta est disponible [ici](/docs/services/discovery?topic=discovery-release-notes#beta-features).
  - Problème connu dans {{site.data.keyword.discoveryfull}} Knowledge Graph : tous les noms de type d'entité et de type de relation sont convertis en majuscules lors de l'opération d'ingestion. Par exemple, l'entité "GeoPoliticalEntity" est convertie en "GEOPOLITICALENTITY" et la relation "partOf" est convertie en "PARTOF". [Résolu](/docs/services/discovery?topic=discovery-release-notes#5mar18)
- [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news) a été publié dans deux langues supplémentaires : le coréen (`collection_id` : `news-ko`) et l'espagnol (`collection_id` : `news-es`). Les versions coréenne et espagnole de {{site.data.keyword.discoverynewsfull}} ne peuvent être utilisées que via l'API. Pour toute information sur l'exécution d'une requête sur une collection via l'API, voir la page [suivante ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery#query-your-collection){: new_window} [](/docs/services/discovery?topic=discovery-release-notes#26jan18). La référence `collection_id` de la version anglaise d'{{site.data.keyword.discoverynewsfull}} est désormais `news-en`. Anciennement, la référence `collection_id` était `news`. Si vous utilisiez l'ancienne référence `collection_id`, elle continuera de fonctionner, cela dit, vous souhaiterez peut-être utiliser la nouvelle référence `collection_id` pour vos nouveaux projets.
- Les résultats de requête renvoient une valeur `score`, qui indique la pertinence relative entre les résultats de requête. Depuis le 30 novembre 2017, la façon dont la valeur `score` est calculée a changé. La valeur `score` ne doit être utilisée que pour classer des documents dans une seule recherche et non entre plusieurs recherches ou sessions. Si vous avez formé une collection, une valeur `score` est renvoyée dans les résultats d'une requête en langage naturel. Dans la mesure où la valeur `score` indique la pertinence relative entre des résultats de requête, elle ne doit pas être utilisée en tant que seuil. En revanche, pour définir des seuils, vous pouvez utiliser la valeur `confidence`, qui indique la pertinence du résultat par rapport au modèle formé. Pour plus d'informations sur la définition de seuils, voir [Scores de confiance](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence).
- A partir de cette édition, la fonction d'extraction de passage détecte les limites de phrase. Elle tente de renvoyer des passages qui commencent et s'arrêtent respectivement au début et à la fin d'une phrase. Auparavant, de nombreux passages pouvaient commencer ou se terminer quelque part au milieu des phrases. Pour plus d'informations sur la fonction d'extraction de passage, voir [Passages](/docs/services/discovery?topic=discovery-query-parameters#passages).

## 15 novembre 2017
{: #15nov17}

Outils {{site.data.keyword.discoveryshort}} :

- L'enrichissement [Relation Extraction](/docs/services/discovery?topic=discovery-configservice#relation-extraction) a été ajouté. Il inclut une option permettant d'incorporer un modèle de relation personnalisé créé avec {{site.data.keyword.knowledgestudiofull}}.
- L'enrichissement [Entity Extraction](/docs/services/discovery?topic=discovery-configservice#entity-extraction) des outils {{site.data.keyword.discoveryshort}} inclut à présent une option permettant d'incorporer un modèle d'entité personnalisé créé avec {{site.data.keyword.knowledgestudiofull}}.
- L'option permettant de créer une collection en japonais à l'aide des outils {{site.data.keyword.discoveryshort}} a été retirée. En revanche, l'option permettant de créer une collection en japonais à l'aide de l'API {{site.data.keyword.discoveryshort}} a été conservée.
- Les outils {{site.data.keyword.discoveryshort}} prennent désormais en charge les environnements syndiqués.

## 10 novembre 2017
{: #10nov17}

Outils {{site.data.keyword.discoveryshort}} :

- Des options supplémentaires ont été ajoutées aux outils {{site.data.keyword.discoveryshort}} pour l'extraction de passage. Lorsque vous exécutez des requêtes, vous pouvez désormais spécifier les zones dont les passages doivent être renvoyés, le nombre de passages à renvoyer, ainsi que le nombre maximal de caractères pour chaque passage. Pour connaître les limites, les valeurs minimales et les valeurs maximales, voir la rubrique [Passages](/docs/services/discovery?topic=discovery-query-parameters#passages).

## 8 novembre 2017
{: #8nov17}

La chaîne de version pour tous les appels d'API, `2017-10-16`, a été remplacée par `2017-11-07`. Cette version :
- La valeur `score` dans chaque résultat de requête a été déplacée vers un nouvel objet nommé `result_metadata`.
- Si la collection ayant fait l'objet d'une requête a été formée et s'il s'agit d'une requête en langage naturel, l'objet `result_metadata` inclura une zone `confidence` qui affiche le score de confiance pour ce résultat. Pour plus d'informations, voir [Scores de confiance](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence).
- Les zones qui comportent des blancs (par exemple, `body.additional reading`) seront filtrées lors de l'opération d'ingestion. La description `notices` indiquera : `The field 'additional reading' is invalid: whitespace, '.', '#' and ',' are invalid in a field name`.
- La zone `result_metadata` sera filtrée lors de l'opération d'ingestion.

## 16 octobre 2017
{: #16oct17}

- La chaîne de version pour tous les appels d'API, `2017-09-01`, a été remplacée par `2017-10-16`. Cette version rend obsolète la prise en charge du téléchargement de nouveaux documents dans des collections existantes qui sont enrichies avec des enrichissements {{site.data.keyword.alchemylanguageshort}}, ainsi que la création de nouvelles collections et leur enrichissement avec les enrichissements {{site.data.keyword.alchemylanguageshort}}. Les collections existantes enrichies avec {{site.data.keyword.alchemylanguageshort}} doivent être migrées vers les enrichissements {{site.data.keyword.nlushort}} dès que possible. Pour plus d'informations, voir [Migration des enrichissements vers {{site.data.keyword.nlushort}}](/docs/services/discovery?topic=discovery-migrate-nlu#migrate-nlu). Les outils {{site.data.keyword.discoveryshort}} utilisent également la version `2017-10-16`. Pour plus d'informations, voir le paragraphe qui suit.

Outils {{site.data.keyword.discoveryshort}} :

- Les outils {{site.data.keyword.discoveryshort}} utilisent la chaîne de version d'API `2017-10-16`, par conséquent, si vous utilisez les outils, vous ne pourrez plus télécharger des documents dans des collections {{site.data.keyword.alchemylanguageshort}} existantes ni créer de nouvelles collections enrichies avec les enrichissements {{site.data.keyword.alchemylanguageshort}} après la version `2017-10-16`.  Si vous souhaitez continuer à utiliser les outils {{site.data.keyword.discoveryshort}} pour enrichir des collections, commencez par faire migrer ces dernières vers {{site.data.keyword.nlushort}}. Pour plus d'informations, voir [Migration des enrichissements vers {{site.data.keyword.nlushort}}](/docs/services/discovery?topic=discovery-migrate-nlu#migrate-nlu).
- L'**explorateur de schéma de données** affiche des exemples de requête pour plusieurs enrichissements dans la collection {{site.data.keyword.discoverynewsfull}}. De plus, il comporte à présent un lien **Show more values** qui permet d'afficher des valeurs d'exemple supplémentaires pour cet enrichissement dans {{site.data.keyword.discoverynewsfull}}.
- Plusieurs améliorations de productivité, y compris la combinaison de statistiques de collection, d'erreurs et d'avertissements et d'analyses de données sur l'écran **Manage data**.
- Un message affichant une alerte lorsque le traitement des documents est terminé, s'affiche.

## 9 octobre 2017
{: #9oct17}

- Une nouvelle métrique d'agrégation, `unique_count`, est disponible dans l'API. Elle renvoie un comptage des instances uniques de la zone spécifiée dans la collection. Pour plus d'informations, voir [unique_count](/docs/services/discovery?topic=discovery-query-aggregations#unique_count).

Outils {{site.data.keyword.discoveryshort}} :

- Les agrégations d'histogramme et d'intervalle de temps sont désormais prises en charge dans le **générateur de requête visuelle**. Vous avez également la possibilité d'activer la détection d'anomalies pour les requêtes d'intervalle de temps.
- L'**explorateur de schéma de données** affiche les exemples de requête pour l'enrichissement choisi. De plus, il comporte à présent un lien **Show more values" qui permet d'afficher des valeurs d'exemple supplémentaires pour cet enrichissement.
- Un menu Hamburger a été ajouté pour faciliter la navigation dans les écrans **Manage data**, **View data schema** et **Build queries**.

### 3 octobre 2017
{: #3oct17}

- La segmentation de document est à présent disponible. Voir [Fractionnement de documents avec segmentation de document](/docs/services/discovery?topic=discovery-configservice#doc-segmentation).

### 29 septembre 2017
{: #29sept17}

- {{site.data.keyword.discoveryshort}} a été lancé à l'emplacement `Germany` le 29 septembre 2017. Afin d'assurer la conformité avec la réglementation relative aux données de l'UE, les enrichissements AlchemyLanguage ne sont pas pris en charge à cet emplacement.
- Problème connu : les zones de requête ne peuvent pas contenir de blancs.  Lorsque vous écrivez une requête dans {{site.data.keyword.discoveryshort}}, si une zone de requête contient un espace (par exemple, `body.additional reading`), vous recevez le message `400: Invalid query syntax error`. [Résolu](/docs/services/discovery?topic=discovery-release-notes#8nov17)

### 25 septembre 2017
{: #25sept17}

- Un plan de tarification Premium est à présent disponible. Pour plus d'informations, voir [Plans de tarification {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans).
- L'option permettant d'exécuter des requêtes, de répertorier des zones et d'exécuter des requêtes sur des avis dans les collections d'un environnement a été ajoutée. Pour plus d'informations, voir [Exécution d'une requête sur plusieurs collections](/docs/services/discovery?topic=discovery-query-concepts#multiple-collections).
- Les informations de support de langue pour {{site.data.keyword.discoveryshort}} sont disponibles dans la rubrique [Support de langue](/docs/services/discovery?topic=discovery-language-support#language-support).

Outils {{site.data.keyword.discoveryshort}} :
- Le générateur de requête visuelle est passé du statut bêta au statut GA. Actuellement, les agrégations de filtre, d'intervalle de temps et d'histogramme ne sont pas prises en charge avec le générateur de requête visuelle. Cliquez sur **Include analysis of your results**, puis sur **Edit in Query Language** à l'écran **Build queries** pour écrire ces agrégations.
- Une fonction bêta permettant d'effectuer un dédoublonnage sur des requêtes {{site.data.keyword.discoverynewsfull}} a été ajoutée.
- Outre des collections en anglais, en allemand et en espagnol, vous pouvez désormais créer des collections en arabe, en français, en italien, en coréen, en japonais et en portugais brésilien.
- Problème connu : les outils {{site.data.keyword.discoveryshort}} ne prennent pas en charge les environnements syndiqués. [Résolu](/docs/services/discovery?topic=discovery-release-notes#15nov17)

### 14 septembre 2017
{: #14sept17}

Outils {{site.data.keyword.discoveryshort}} :

- L'explorateur de schéma de données a été ajouté. Il affiche les zones et les valeurs contenues dans vos documents transformés. Vous pouvez utiliser ces informations pour comprendre la structure de données de votre collection avant de créer des requêtes à l'aide du langage de requête Discovery. Le schéma de données peut être consulté de deux manières différentes : par document (vue de document) ou par zone (vue de collection). Pour accéder à l'explorateur de schéma de données, sur l'écran **My Data Insights**, cliquez sur le bouton **View data schema** ou sur l'icône **View Data Schema** située à gauche.

### 6 septembre 2017
{: #6sept17}

- Une option bêta permettant de dédoublonner les documents renvoyés par votre requête a été ajoutée. Cette fonction bêta est opérationnelle sur les collections privées et sur les collections Watson Discovery News. Pour plus d'informations, voir [Exclusion des documents en double dans les résultats de requête](/docs/services/discovery?topic=discovery-query-parameters#deduplication).

Pour l'instant, le dédoublonnage de document est pris en charge uniquement en tant que fonctionnalité bêta. Pour plus d'informations, voir l'instruction concernant les fonctions bêta au début du présent document.

### 31 août 2017
{: #31aug17}

- La chaîne de version pour tous les appels d'API, `2017-08-01`, a été remplacée par `2017-09-01`. Cette version inclut les mises à jour qui filtreront les zones JSON non valides suivantes lors de la prévisualisation et de l'ingestion de sorte que seules les zones JSON valides soient ingérées. Mettez à jour votre chaîne de version vers `2017-09-01` pour éviter les conflits et les erreurs.

   - Les zones `id`, `score` et `highlight` au niveau supérieur (vous pouvez continuer à ajouter des documents à votre collection à l'aide des ID de document avec la fonction `add a document`). Pour plus d'informations, voir le document [API Reference ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery#add-a-document){: new_window}.
   - Les noms de zone avec `_` comme préfixe au niveau supérieur (par conséquent, lorsque vous exécutez une requête portant sur un document en utilisant son ID, vous pouvez exécuter une requête sur `id` à la place de `_id`).
   - Les caractères `#` et `,` dans les noms de zone
   - Les caractères `+` et `-` dans les noms de zone préfixés
   - Les valeurs vides `"` `"` pour un nom de zone

**Remarque :** si dans vos documents JSON, les noms de zone comprennent ces caractères, ou si les zones `id`, `score` et `highlight` figurent au niveau supérieur, vous devez les retirer avant d'ajouter les documents à votre collection, sinon, ces zones seront vides. Vous pouvez créer une configuration personnalisée et normaliser vos documents JSON avant d'ajouter des documents à votre collection afin d'éviter ce problème. Voir[Configuration personnalisée](/docs/services/discovery?topic=discovery-configservice#custom-configuration).  De plus, les documents dont le nom de fichier comporte le caractère de ponctuation `?`, `:` ou `#` généreront des erreurs lors de l'ingestion. Renommez les documents dont le nom comporte ces caractères, avant de procéder à leur ingestion.

- Les méthodes d'extraction pour `natural_language_query` ont été mises à jour afin d'améliorer la pertinence des résultats en faisant correspondre des mots avec des sémantiques connexes. Cette mise à jour ne concerne que les collections qui n'ont pas fait l'objet d'une formation de pertinence. Si vous utilisez `natural_language_query` et n'avez effectué aucune formation de pertinence, il est probable que vous constatiez des améliorations au niveau de l'ordre des résultats renvoyés.

Outils {{site.data.keyword.discoveryshort}} :

- Les modifications apportées au générateur de requête facilitent le basculement entre les options de requête Discovery Query Language (langage de requête Discovery) et Natural Language (langage naturel), et entre les options query, filter et aggregation.


### 25 août 2017
{: #25aug17}

- Le tableau `passages` comprend désormais `field`, `start_offset` et `end _offset`. `field` est le nom de la zone dont le passage a été extrait. `start_offset` est le caractère de début du texte de passage dans la zone. `end_offset` est le caractère de fin du texte de passage dans la zone.

Outils {{site.data.keyword.discoveryshort}} :
Cette amélioration au niveau de la création de requête est disponible sur l'écran **Build queries**.

-  La fonction bêta permettant d'écrire des requêtes dans le langage de requête {{site.data.keyword.discoveryshort}} avec un générateur de requête visuelle a été ajoutée. Cliquez sur **Build in visual mode** dans les sections **Search for documents** et **Limit which documents you query** pour essayer cette fonction  A mesure que vous créez votre requête visuellement, elle s'affiche au-dessous dans le **langage de requête {{site.data.keyword.discoveryshort}}**.

   Pour l'instant, le générateur de requête visuelle est pris en charge uniquement en tant que fonctionnalité bêta. Pour plus d'informations, voir l'instruction concernant les fonctions bêta au début du présent document.

### 18 août 2017
{: #18aug17}

Outils {{site.data.keyword.discoveryshort}} :

- La prise en charge des agrégations et conditions imbriquées a été ajoutée au générateur d'agrégation visuelle bêta introduit le [11 août 2017](/docs/services/discovery?topic=discovery-release-notes#11aug17). Le nombre maximal de conditions par ligne d'agrégation a été fixé à 3.

   Pour l'instant, le générateur d'agrégation visuelle est pris en charge uniquement en tant que fonctionnalité bêta. Pour plus d'informations, voir l'instruction concernant les fonctions bêta au début du présent document.

### 11 août 2017
{: #11aug17}

Outils {{site.data.keyword.discoveryshort}} :

Deux fonctions sont des améliorations au niveau de la création de requête et sont disponibles sur l'écran **Build queries**.

- L'option permettant de sélectionner une requête dans un groupe d'exemples de requête et d'agrégation préconfigurés a été ajoutée. Cliquez sur **Use a sample query** dans l'angle supérieur droit pour accéder à la liste. Si vous exécutez une requête sur une collection de données privées, les exemples utilisent les `premières entités`, les `catégories`, etc. trouvées dans votre collection. Vous pouvez vous servir de ces requêtes comme point de départ pour écrire vos propres requêtes. Des exemples de requête sont disponibles pour les collections {{site.data.keyword.discoverynewsfull}} et pour les collections privées.

-  La fonction bêta permettant d'écrire des agrégations avec un générateur visuel a été ajoutée. Cliquez sur **Build in visual mode** au-dessus de la zone**Write an aggregation query using the {{site.data.keyword.discoveryshort}} Query Language** pour essayer cette fonction.  A mesure que vous créez votre agrégation visuellement, la requête apparaît au-dessous dans le **langage de requête {{site.data.keyword.discoveryshort}}**.  

   Pour l'instant, le générateur d'agrégation visuelle est pris en charge uniquement en tant que fonctionnalité bêta. Pour plus d'informations, voir l'instruction concernant les fonctions bêta au début du présent document.

### 31 juillet 2017
{: #31jul17}

- Une nouvelle version de {{site.data.keyword.discoverynewsfull}} a été publiée. La version d'origine a été renommée {{site.data.keyword.discoverynewsfull}} Original et son retrait est prévu le **15 janvier 2018**. Pour obtenir des instructions de migration, voir [Migration à partir de Watson Discovery News Original](/docs/services/discovery?topic=discovery-migrate-bwdn#migrate-bwdn).
  **Remarque :** si vous avez créé une nouvelle instance de service {{site.data.keyword.discoveryshort}}, vous ne pourrez accéder qu'à la nouvelle version de {{site.data.keyword.discoverynewsfull}}.

- Un nouveau plan de tarification pour {{site.data.keyword.discoveryfull}} a été publié. Pour plus de détails, voir [Plans de tarification {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans).

- La chaîne de version pour tous les appels d'API, `2017-07-19`, a été remplacée par `2017-08-01`. Cette version comprend des mises à jour pour le nouveau plan de tarification et la nouvelle version de Watson Discovery News. Mettez à jour la chaîne de version afin d'éviter les conflits et les erreurs.

### 19 juillet 2017
{: #19jul17}

 - Dans le cadre du changement de tarification annoncé pour le 1er août 2017, les utilisateurs qui utilisent actuellement le plan **d'essai gratuit de 30 jours** devenu obsolète seront automatiquement migrés vers le plan **Lite**. Suite à cette transition, il se peut que les utilisateurs aient atteint ou dépassé les limites du plan Lite relatives au nombre de documents (_2000_), à la capacité de stockage (_200 Mo_) ou au nombre de collections (_2_). Si vous atteint la limite du plan **Lite**, vous ne pouvez pas ajouter d'autre contenu dans le service, mais vous pouvez toujours exécuter des requêtes sur les collections. Vous pouvez afficher l'état en cours de toutes ces limites en utilisant les outils ou l'API {{site.data.keyword.discoveryshort}}. Pour pouvoir recommencer à ajouter du contenu à l'instance {{site.data.keyword.discoveryshort}}, vous devez exécuter l'une des actions suivantes :
   - Retirer des collections et/ou des documents de manière à ne dépasser les limites du plan **Lite**.
     Les documents peuvent être supprimés individuellement via l'API à l'aide de la méthode [delete-doc](https://{DomainName}/apidocs/discovery#delete-a-document), ou des collections entières peuvent être supprimées à l'aide des outils ou de l'API à l'aide de la méthode [delete-collection](https://{DomainName}/apidocs/discovery#delete-a-collection).
   - Effectuer une mise à niveau de votre plan vers un niveau qui répond à vos besoins en matière de stockage.
 - Les clients ayant des environnements dont la taille est **`1`** **`2`** ou**`3`** feront l'objet d'une migration automatique vers le plan **Advanced**.

### 17 juillet 2017
{: #17jul17}

 - Les fonctions suivantes sont passées du statut bêta au statut GA :

   - Formation de pertinence
   - Requête en langage naturel
   - Mise en évidence

 - Avec cette édition, le mécanisme d'enrichissement {{site.data.keyword.alchemylanguageshort}} de {{site.data.keyword.discoveryfull}} est remplacé par {{site.data.keyword.nlushort}}. {{site.data.keyword.alchemylanguageshort}} est en train de devenir obsolète et il est recommandé de commencer à utiliser {{site.data.keyword.nlushort}} dès que possible.  Pour plus de détails, voir [Migration des enrichissements {{site.data.keyword.alchemylanguageshort}} vers les enrichissements {{site.data.keyword.nlushort}}](/docs/services/discovery?topic=discovery-migrate-nlu#migrate-nlu).
   **Remarque :** lors de l'intégration à Watson Knowledge Studio, la configuration de l'enrichissement {{site.data.keyword.alchemylanguageshort}} doit encore être utilisé. Pour plus d'informations, voir [Intégration à {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-with-wks).

 - La chaîne de version pour tous les appels d'API, `2017-06-25` a été remplacée par `2017-07-19`. Cette version active une configuration par défaut NLU sur la création de collection. Vous devriez toujours être en mesure d'effectuer des enrichissements à l'aide de {{site.data.keyword.alchemylanguageshort}} dans les éditions précédentes.

    La configuration par défaut a été mise à jour pour utiliser {{site.data.keyword.nlushort}}. Il est recommandé de mettre à jour la chaîne de version dès que possible pour éviter les conflits et les erreurs.

 - Outils Discovery :

    Les fiches de connaissances pour collections enrichies avec {{site.data.keyword.alchemylanguageshort}} ne seront plus mises à jour automatiquement. Vous devez faire migrer votre collection vers les enrichissements {{site.data.keyword.nlushort}} pour que les fiches de connaissances soient mises à jour.

    Si vous avez créé une collection avant le **18 juillet 2017** et appliqué la **configuration par défaut**, cette collection a été enrichie à l'aide des enrichissements {{site.data.keyword.alchemylanguageshort}}. Si vous appliquez la **configuration par défaut** à une collection après cette date, les enrichissements {{site.data.keyword.nlushort}} seront utilisés (le nom de configuration deviendra **configuration par défaut avec NLU** dans les outils). Dans la mesure où les enrichissements {{site.data.keyword.alchemylanguageshort}} sont en passe de devenir obsolètes, il est recommandé de ne pas les utiliser avec les nouvelles collections.

### 30 juin 2017
{: #30jun17}

 -  La normalisation d'entité introduite en tant que fonction bêta le 5 mai 2017 est passée au statut GA. Pour plus d'informations, voir [Création d'une configuration personnalisée pour normaliser des entités](/docs/services/discovery?topic=discovery-normalizing-entities-cc#normalizing-entities-cc).

### 23 juin 2017
{: #23jun17}

 - La chaîne de version pour tous les appels d'API, `2016-12-01`, a été remplacée par `2017-06-25`. La nouvelle chaîne de version active les enrichissements en allemand (`de`) ou en espagnol (`es`) si la langue définie pour une collection correspond à l'une de ces langues. Auparavant, tous les enrichissements étaient effectués en anglais, quelque soit le paramètre linguistique d'une collection.

    Si vous n'utilisez pas d'enrichissements dans des langues autres que l'anglais, vous pouvez continuer à utiliser la chaîne de version `2016-12-01`. Toutefois, il est recommandé de mettre à jour la chaîne de version dès que possible pour éviter d'éventuels conflits.

 - La détection d'anomalies est désormais disponible dans le cadre des agrégations `timeslice` en tant que fonction GA. Pour plus d'informations, voir [Détection d'anomalies Timeslice](/docs/services/discovery?topic=discovery-query-aggregations#anomaly-detection).

 - Outils Discovery :

   - La fonction bêta permettant d'améliorer la pertinence des résultats de requête à l'aide des outils Discovery (outils de pertinence) a été ajoutée. Voir [Amélioration de la pertinence de vos résultats de requête à l'aide des outils Discovery ](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling).

### 19 juin 2017
{: #19jun17}

  - Outils Discovery :

    - Une option permettant d'ajouter la langue (Anglais, Espagnol ou Allemand) des documents dans une nouvelle collection a été ajoutée. Pour l'utiliser, choisissez  **Select the language of your documents** dans la boîte de dialogue **Name your new collection**.

    - Un onglet intitulé **Summary** a été ajouté à l'écran **Build queries**. L'onglet **Summary** affiche une présentation générale de l'ensemble des résultats de requête fournis sur l'onglet **JSON** existant. Le contenu affiché sur l'onglet **Summary** varie en fonction de votre requête et de vos enrichissements. Les informations pouvant être affichées sont notamment le nom ou l'ID de document, les statistiques d'agrégation, les passages de document par ordre de pertinence et les résultats par enrichissement.

    - Une option de requête en langage naturel a été ajoutée à l'écran **Build queries**. Pour l'utiliser, cliquez sur **Ask a question in plain language** dans la section **Search for documents** afin de faire apparaître une zone dans laquelle vous pouvez entrer votre question. La zone de requête d'origine (anciennement intitulée **Enter a query or keyword**) est désormais accessible en cliquant sur le bouton **Use the Discovery Query Language**.

    - L'écran **Build queries** a été remanié, mais toutes les zones et options ont été conservées. Les anciens noms et les nouveaux noms des zones sont présentés dans le tableau ci-dessous.

| **Ancien nom de zone**                                           | **Nouveau nom de zone ou de section**                                                                                             |
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| Write and run a query                                    | Search for documents                                                                                                  |
| Narrow your query results (Filter)                       | Limit which documents you query                                                                                       |
| Group query results (Aggregation)                        | Include analysis of your results                                                                                      |
| Fields to display                                        | Le nom n'a pas été modifié, mais la zone a été déplacée dans la nouvelle section **Customize display options**.                                      |
| Number of documents to return (Count)                    | Number of documents to return [Cette zone a été déplacée dans la section **Customize display options**.]                    |
| Include matching passages                                | Include relevant passages [Cette zone a été déplace dans la section **Customize display options**.]                        |
| Number of query fields to skip at the beginning (Offset) | Number of query results to skip at the beginning [Cette zone a été déplacée dans la section **Customize display options**.] |

### 5 juin 2017
{: #5jun17}

 - Désormais, les requêtes Watson Discovery News affichent uniquement les 150 premiers mots de chaque article dans les zones JSON `text` et `alchemyapi_text`. La zone `blekko.snippet` affichera uniquement la première phrase du tableau de fragments.

### 30 mai 2017
{: #30may17}

 - Le paramètre `passages` de l'API de requête est passé du statut bêta au statut GA.

### 25 mai 2017
{: #25may17}

 - Outils Discovery : la mise en évidence des zones de requête a été ajoutée dans cette édition. Cette fonction ajoute une mise en évidence de couleur jaune aux noms de zone dans l'objet JSON du panneau de résultats. Toutes les zones qui font l'objet d'une requête ou qui sont filtrées sont mises en évidence pour chaque résultat même si leur contenu ne correspond pas à la requête. Les zones utilisées dans des agrégations sont également mises en évidence dans les résultats de requête, mais seule la première opération d'agrégation est mise en évidence.

### 10 mai 2017
{: #10may17}

 - Désormais, les méthodes `query` et `notices` prennent en charge le paramètre `highlight`. Ce paramètre est une valeur booléenne. Lorsque vous exécutez une requête alors que vous avez affecté au paramètre `highlight` la valeur `true`, le service renvoie une sortie qui inclut une nouvelle zone `highlight` dans laquelle les mots qui correspondent à la requête sont encapsulés dans des balises `*` HTML (mise en évidence). Pour plus d'informations, voir[Paramètres de requête](/docs/services/discovery?topic=discovery-query-parameters#highlight).

 - Il peut arriver que la suppression d'un environnement n'aboutisse que partiellement, auquel cas, aucun nouvel environnement ne peut être créé car il ne peut exister qu'un seul environnement par instance de service. Si vous tentez de supprimer, puis de créer un environnement et vous constatez que l'une ou l'autre de ces opérations est bloquée à l'état `pending`, il est probable que ce problème se soit produit. Pour contourner ce problème, relancez l'opération de suppression afin de la terminer, puis créez le nouvel environnement.

### 8 mai 2017
{: #8may17}

 - Le modèle de score de tonalité affective a été mis à jour afin d'améliorer la précision des enrichissements d'analyse des émotions (`docEmotion`). Le jeu de données de formation a été développé et la conception de la fonction a été modifiée, par conséquent, le modèle est plus précis sur le jeu de données de test de performances.

### 5 mai 2017
{: #5may17}

 - Désormais, la normalisation d'entité est disponible avec le service Discovery qui utilise un modèle personnalisé généré par Watson Knowledge Studio. La normalisation d'entité insère des noms normalisés (canoniques) pour différentes références à la même personne ou au même objet dans le document source. Pour plus d'informations, voir [Création d'une configuration personnalisée pour normaliser des entités](/docs/services/discovery?topic=discovery-normalizing-entities-cc#normalizing-entities-cc).

     **Remarque :** actuellement, la normalisation d'entité est uniquement prise en charge en tant que fonction bêta. Pour plus d'informations, voir l'instruction concernant les fonctions bêta au début du présent document. [Résolu](/docs/services/discovery?topic=discovery-release-notes#30jun17)

Outils {{site.data.keyword.discoveryshort}} :

 - Le journal des erreurs des outils n'est plus limité à un maximum de 8 pages de résultats. Le journal des erreurs contient toujours l'ID du document si le nom du document n'est pas disponible.

 - Les noms de configuration sont limités à 50 caractères et doivent comporter les caractères `[a-zA-Z0-9-_]`. 

 - Le paramètre `passages`, précédemment accessible uniquement via l'API, est désormais également accessible via les outils.

### 25 avril 2017
{: #25apr17}

  - A présent, le service vous permet de fournir des *données de formation* destinées à améliorer la précision de vos résultats de requête. Lorsque vous fournissez des données de formation à une instance Discovery, le service utilise des algorithmes Watson avancés pour déterminer les résultats les plus pertinents. A mesure que vous ajoutez des données de formation, l'instance de service devient plus précise et plus sophistiquée par rapport aux résultats qu'elle renvoie. Pour plus d'informations, voir la rubrique [Amélioration de la pertinence de vos résultats de requête](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api) et le document [API Reference](https://{DomainName}/apidocs/discovery#list-training-data).

  - A présent, l'API prend en charge le paramètre `natural_language_query` en tant que version bêta. Ce paramètre vous permet de spécifier une requête en langage naturel au lieu du langage de requête du service Discovery. Pour plus d'informations, voir la méthode [Query your collection](https://{DomainName}/apidocs/discovery#query-your-collection) décrite dans le document API Reference.

  - Mises à jour et corrections d'erreurs apportées à la documentation

### 14 avril 2017
{: #14apr17}

Des améliorations ont été ajoutées à l'API de requête (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`). Pour plus d'informations, voir la méthode [Query your collection](https://{DomainName}/apidocs/discovery#query-your-collection) décrite dans le document API Reference.

  - Désormais, l'API de requête prend en charge le paramètre `passages`. Si le paramètre a pour valeur `true`, la requête renvoie un ensemble des passages les plus pertinents à partir des documents de votre collection. Les passages sont générés par des algorithmes Watson sophistiqués afin de déterminer les meilleurs passages de texte à partir de tous les documents renvoyés par la requête. Cela vous permet de trouver des informations et du contexte de manière plus précise. Pour plus d'informations, voir la méthode [Query your collection](https://{DomainName}/apidocs/discovery#query-your-collection) décrite dans le document API Reference.

    - Si vous spécifiez `passages=true` dans votre requête, vous risquez de réduire les performances car cela génère un traitement supplémentaire en raison de l'extraction des passages. Avec des environnements plus grands, l'impact sur les performances peuvent être moindre.

    - Le paramètre `passages` est pris en charge uniquement sur des collections privées. Il n'est pas pris en charge dans la collection Watson Discovery News.

    - Actuellement, le paramètre `passages` renvoie un maximum de 10 résultats. Le nombre de résultats renvoyés ne peut pas être modifié. [Mise à jour](/docs/services/discovery?topic=discovery-query-parameters#passages_count)

    - Le paramètre `passages` renvoie un maximum de trois (3) passages pour n'importe quel document contenu dans la collection. Si un document contient plus de trois passages pertinents supplémentaires, ils ne sont pas renvoyés par le paramètre.

### 7 avril 2017
{: #7apr17}

- A présent, l'API de requête (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`) prend en charge le paramètre `sort`, qui vous permet de spécifier une liste de zones du document sur lesquelles effectuer le tri, séparées par des virgules. Pour plus d'informations, voir la méthode [Query your collection ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery#query-your-collection){: new_window} dans le document API Reference.
- A présent, le paramètre `timeslice` pour les agrégations de requête traite correctement les dates au format époque UNIX. Pour plus d'informations sur les agrégations et le paramètre `timeslice`, voir la rubrique [Référence de requête](/docs/services/discovery?topic=discovery-query-reference#aggregations).
- Des améliorations ont été apportées aux messages d'erreur.
- Des mises à jour ont été apportées au logiciel SDK Java du service. Pour plus d'informations, voir le document [API Reference](https://{DomainName}/apidocs/discovery?language=java).
- Les limitations suivantes relatives à l'utilisation de caractères génériques dans les requêtes ont été résolues :

  - Auparavant, un seul caractère générique fonctionnait dans une requête. Par exemple, `query-month:*ctober` fonctionnait, mais`query-month:*ctobe*` a généré une erreur d'analyse syntaxique.
  - Les caractères génériques ne fonctionnaient pas avec des requêtes qui contenaient des majuscules. Par exemple, pour la paire clé/zone `{"borrower": "GOVERNMENT OF INDIA"}`, `query-borrower:*ndia` renvoyait des résultats, mais pas `query-borrower:*NDIA`.

**Remarque :** les caractères génériques ne sont pas nécessaires dans les phrases contenues dans des requêtes. Par exemple, pour la paire clé/zone   `{"borrower": "GOVERNMENT OF TIMOR"}`, `query-borrower:"GOVERNMENT OF TIMOR"` renvoie des résultats, mais pas `query-borrower:"GOVERNMENT OF TI*OR"`. L'utilisation d'un caractère générique n'est pas applicable dans des phrases car tous les caractères placés entre les guillemets (`"`) d'une phrase sont mis en échappement.

### 24 mars 2017
{: #24mar17}

- Une option de filtrage a été ajoutée à l'écran "My data insights" dans les outils Discovery

### 15 mars 2017
{: #15mar17}

Les problèmes connus suivants ont été découverts :

-  Toutes les zones qui sont ingérées à partir des documents HTML, PDF et Word sont de type **chaîne**. Les zones JSON et les zones calculées, telles que le score de sentiment, sont saisies comme définies. [Mise à jour](/docs/services/discovery?topic=discovery-addcontent#adding-content-with-the-api-or-tooling)
- Actuellement, l'opération `preview` ne recherche pas les tableaux JSON imbriqués dans un document JSON soumis. Actuellement, le service ne prend pas en charge les tableaux JSON imbriqués, par conséquent, un document qui comporte des tableaux imbriqués peut réussir l'opération `preview` mais échouer lors d'une tentative d'ingestion. Voir [Puis-je télécharger des tableaux JSON ?](/docs/services/discovery?topic=discovery-faqs#array)
- Si des erreurs d'ingestion se produisent et génèrent le message `unsupported text language`, mettez à jour votre configuration avec l'option d'enrichissement`"language": "english"` pour forcer tout le texte à être interprété en tant que texte en anglais, comme illustré dans l'exemple suivant : 
[Mise à jour](/docs/services/discovery?topic=discovery-migrate-nlu#migrate-nlu)
```json
"enrichments": [
        {
     "enrichment": "alchemy_language",
     "source_field": "author.label",
     "options": {
       "extract": "taxonomy,entity,relation,doc-emotion,doc-sentiment,concept,keyword",
       "sentiment": true,
       "quotations": true,
       "language": "english"
     }
   }
 ]
```
{: codeblock}

Les bogues suivants ont été résolus :

- Les performances et la stabilité du service ont été améliorées.

### 8 mars 2017
{: #8mar17}

 - Le système de back end a été optimisé, notamment par l'ajout de nouveaux délais d'attente, afin d'améliorer les performances globales.
 - Le bogue qui provoquait l'affichage du statut `pending` pour les environnements (`0`-sized) libres, quel que soit leur statut réel, a été résolu.
 - La seule langue nationale actuellement prise en charge par {{site.data.keyword.discoveryshort}} est l'anglais américain (`en_US`). [Mise à jour](/docs/services/discovery?topic=discovery-language-support#language-support)

### 3 mars 2017
{: #3mar17}

- L'écran "My data insights" a été ajouté aux outils Discovery.

### 26 février 2017
{: #26feb17}

-     Les performances de l'environnement {{site.data.keyword.discoverynewsshort}} ont été améliorées.
-  Le service {{site.data.keyword.discoverynewsshort}} ne renvoie que 50 résultats à la fois. Pour contourner ce problème, utilisez le paramètre `offset` dans votre requête afin d'activer la pagination des résultats.
-  Vous pouvez soumettre une nouvelle configuration avec un document individuel en utilisant la commande suivante :

```bash
curl -X POST -u apikey:{apikey_value} -F "file=@wikipedia-sample.html" -F "configuration=$(cat config.json)" "https://gateway.watsonplatform.net/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2016-12-01"
```
{: pre}
-  Les convertisseurs PDF et Word du service créent un document HTML en guise d'étape intermédiaire. Le service peut appliquer des transformations et des normalisations supplémentaires au document HTML intermédiaire avant la transformation finale en document JSON normalisé.

Les bogues suivants ont été résolus :

-  Des améliorations ont été apportées aux codes d'erreur.
-  Plusieurs erreurs de documentation ont été corrigées.

### 16 février 2017
{: #16feb17}

-  Vous pouvez désormais utiliser des sélecteurs CSS pour sélectionner des zones JSON auxquelles vous pouvez ensuite appliquer des enrichissements. Pour plus d'informations, voir [Utilisation de sélecteurs CSS pour extraire des zones](/docs/services/discovery?topic=discovery-configservice#using-css).
-  A présent, vous pouvez augmenter la taille d'un environnement en transmettant un nouveau paramètre `size: X` à la méthode [update-environment](https://{DomainName}/apidocs/discovery#update-an-environment), où `X` est un entier compris entre 0 et 3. Pour plus d'informations sur les tailles et les attributs d'environnement, voir [create-environment method](https://{DomainName}/apidocs/discovery#create-an-environment). [Mise à jour](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)

    **Remarque :** vous ne pouvez pas réduire la taille d'un environnement existant. Si vous souhaitez réduire la taille de votre environnement, contactez le support {{site.data.keyword.IBM}} pour obtenir de l'aide.

-  Un nouvelle opérateur de requête est disponible. L'opérateur `::!` a été ajouté en tant qu'opérateur not-equals unaire. Par exemple, vous pouvez désormais exécuter `query=field::!value` (différent de). Auparavant, le seul opérateur d'exclusion était `:!` pour l'opérateur not-contains (par exemple, `query=field:!value`).

Les bogues suivants ont été résolus :

-  Des mises à jour de sécurité ont été appliquées.
-  Les messages d'état des alertes de recherche ont été améliorés.

### 1er février 2017
{: #1feb17}

Les remarques suivantes s'appliquent spécifiquement à l'édition 1.3.0 de Data Crawler :
[Mise à jour](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler)

-   Data Crawler enregistre les valeurs `document_id` utilisées pour télécharger des documents, ainsi que le statut du téléchargement. Les avis de conversion ne sont pas conservés en dehors du journal. Actuellement, il n'existe aucun outil permettant d'interagir avec ces données, mais de tels outils devraient être développés dès que cela sera possible. Les données sont accessibles via la base de données H2, qui peut être configurée pour utiliser un système de gestion de base de données distant.

### 16 janvier 2017
{: #16jan17}

Les remarques suivantes s'appliquent spécifiquement à l'édition 1.2.5 de Data Crawler :
[Mise à jour](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler)

-  Data Crawler peut éventuellement sonder le statut d'un document juste après avoir téléchargé un fichier. Cette vérification fait partie du concept de "téléchargement d'un document" de Data Crawler, par conséquent, lorsque cette vérification est activée, il est virtuellement impossible pour Data Crawler de télécharger en une seule fois plus de documents que ce que le service {{site.data.keyword.discoveryshort}} peut traiter simultanément pour l'utilisateur.

    L'effet secondaire de la fonction `check_for_completion` est que Data Crawler peut également révéler à l'utilisateur pour quelle raison et quand un document a échoué. Les avis associés à un document qui a été téléchargé, mais dont le traitement a échoué, sont affichés dans le journal de Data Crawler. Les avis ne sont pas exportés dans un fichier pouvant être traité, mais IBM aimerait recevoir une suggestion de fonction pour gérer ce problème.

### 5 janvier 2017
{: #5jan17}

Les remarques suivantes décrivent les problèmes qui ont été identifiés après la disponibilité générale, le 15 décembre 2016 :

Mise à jour : [API reference ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery){: new_window}

-   Si vous ajoutez un document en utilisant l'appel `POST /v1/environments/{environment_id}/collections/{collection_id}/documents`
    ou `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]`, ce dernier renvoie un ID de document et le statut **processing**. Si vous exécutez ensuite une requête sur le document à l'aide de l'appel `GET /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]`, le statut demeure **processing** jusqu'à ce que l'ingestion soit terminée, après quoi, le statut devient **available**.

    Si vous **mettez à jour** un document existant en utilisant l'appel `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]`, l'appel **GET** correspondant renvoie le statut `available` même si le service n'a pas encore terminé le traitement du document mis à jour. Le statut `available` peut faire référence au document d'origine ou au document mis à jour. A moins que l'opération de mise à jour ne renvoie une erreur, il n'existe actuellement aucun moyen de déterminer le statut du document mis à jour.

    Vous pouvez contourner ce problème en attendant jusqu'à 10 minutes après avoir soumis une mise à jour de document avant de tenter d'exécuter une requête sur le contenu mis à jour.

### Disponibilité générale, le 15 décembre 2016
{: #15dec16}

Les remarques suivantes s'appliquent à la disponibilité générale du service {{site.data.keyword.discoveryfull}} :

#### Remarques générales
{: #rn-general-notes}

[Mise à jour : Ajout de contenu](/docs/services/discovery?topic=discovery-addcontent#addcontent)

Voir [API reference ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery){: new_window} pour la version d'API actuelle.

[Mise à jour : Intégration à {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-with-wks).

-   Actuellement, vous ne pouvez pas spécifier le type de données des zones. Toutes les zones sont indexées en tant que texte (type de données **chaîne**). 
-   Si vous utilisez l'API pour gérer le service, vous devez spécifier la version d'API avec chaque appel. La version d'API actuelle est **2016-12-01**. 

    **Remarque :** la version spécifique n'est pas imposée dans la disponibilité générale, mais elle doit tout de même être indiquée pour permettre la compatibilité avec les éditions ultérieures.

-   Vous pouvez utiliser le service avec un modèle personnalisé créé avec {{site.data.keyword.knowledgestudiofull}}. Le modèle personnalisé peut être utilisé pour enrichir les documents ingérés. Vous devez utiliser l'API pour intégrer le modèle personnalisé au service {{site.data.keyword.discoveryshort}} ; vous ne pouvez pas effectuer l'intégration à l'aide des outils.

#### Gestion des données
{: #rn-data}

[Mise à jour](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)

-   Les index de recherche ne sont pas chiffrés.
-   Les fonctions de sauvegarde et de restauration ne sont contrôlables par l'utilisateur.

#### Environnements
{: #rn-environments}

[Mise à jour](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)

-   Vous ne pouvez créer qu'un seul environnement par instance de service pour télécharger vos propres données.
-   Le service {{site.data.keyword.discoveryshort}} se trouve dans une seule zone de disponibilité (Sud des Etats-Unis).
-   Les plans Dedicated et Premium ne sont pas disponibles actuellement.

#### Dimensionnement d'environnement
{: #rn-sizing}

[Mise à jour](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)

-   Vous ne pouvez choisir une taille d'environnement que lorsque vous créez un nouvel environnement. La fonction permettant de redimensionner un environnement n'est pas disponible actuellement pour les utilisateurs.
-   Le choix d'une taille d'environnement avec davantage de mémoire vive permet d'augmenter les performances.
-   Il n'existe actuellement aucune recommandation de dimensionnement prescriptive disponible pour des cas d'utilisation spécifiques.
-   Le dimensionnement personnalisé pour les modèles {{site.data.keyword.knowledgestudiofull}} n'est pas disponible en libre-service. Pour plus d'informations, contactez votre représentant {{site.data.keyword.IBM}}.

#### Limitations affectant les opérations d'ingestion
{: #rn-ingestion}

[Mise à jour](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)

-   Le taux d'ingestion est actuellement limité à 100 opérations d'ingestion de document simultanées. Une application qui soumet des documents au service pour ingestion doit respecter les erreurs HTTP 429 et réduire les demandes d'ingestion en conséquence.
-   Les enrichissements {{site.data.keyword.alchemylanguageshort}} sont limités aux 50 premiers kilobits par zone.
-   Les enrichissements des modèles personnalisés {{site.data.keyword.knowledgestudiofull}} ne sont pas limités, mais fractionnement des documents en blocs de 10 kilobits. Aucune relation entre les limites de blocs n'est annotée.

#### Limitations affectant les requêtes
{: #rn-query}

[Mise à jour](/docs/services/discovery?topic=discovery-query-concepts#query-concepts)

-   Une charge de requête excessive peut entraîner le redémarrage automatique du processus d'index de recherche
-   Les applications qui émettent des requêtes doivent imposer des limites raisonnables au nombre de requêtes simultanées.

### Problèmes connus
{: #rn-issues}

Mise à jour : [API reference ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery){: new_window}

[Mise à jour : Outils](/docs/services/discovery?topic=discovery-getting-started#getting-started)

[Mise à jour : Data Crawler](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler)

[Mise à jour : Enrichissements](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)

[Mise à jour : Ajout de contenu](/docs/services/discovery?topic=discovery-addcontent#addcontent)

-   Vous ne pouvez pas supprimer un document à l'aide des outils. Si vous devez supprimer un document, vous devez utiliser la méthode [Delete a document](https://{DomainName}/apidocs/discovery#delete-a-document) de l'API, décrite dans le document API Reference.

-   Actuellement, l'API ne permet pas d'obtenir la liste des avis (avertissements et erreurs) qui sont générés durant l'ingestion de document. Par conséquent, les outils sont dans l'incapacité d'afficher une liste d'avis d'ingestion, et il n'existe aucun moyen de déterminer lequel des documents explorés par Data Crawler n'a pas pu être ingéré. 
-   Les informations de statut de document ne sont pas toujours précises.
    -   Si une opération d'ingestion dure plus longtemps que le délai de 10 minutes ayant été configuré, le service indique qu'il ne connaît pas le document jusqu'à la fin de l'opération d'ingestion. Une fois l'opération terminée, le statut du document est disponible et précis.
    -   Un document dont l'indexation a abouti mais qui a généré des erreurs peut prendre le statut **failed** pendant une courte période jusqu'à ce qu'il soit entièrement alloué à l'index. Une fois que le document est alloué à l'index, le statut affiché est exact.
-   Vous ne pouvez pas utiliser les outils pour remplacer un document spécifique. Si vous passez outre cette impossibilité, le second document est téléchargé en tant que document distinct. Si vous utilisez l'API et que vous connaissez l'ID du document à remplacer, vous pouvez le faire. Voir la section [Update a document](https://{DomainName}/apidocs/discovery#update-a-document) dans le document API Reference. Si vous utilisez Data Crawler, lorsque vous téléchargez un document mis à jour à partir de la même URL qu'un document précédent, le document d'origine est remplacé.
-   Si vous utilisez les outils pour éditer les enrichissements définis dans votre configuration, vous ne pouvez éditer que les enrichissements utilisés pour extraction. Si vous souhaitez ajouter ou éditer d'autres enrichissements (par exemple, des enrichissements personnalisés à partir d'un modèle {{site.data.keyword.knowledgestudiofull}}), vous devez utiliser l'API. Pour plus d'informations, voir la section [Update a configuration](https://{DomainName}/apidocs/discovery#update-a-configuration) dans le document API Reference.
-   Les remarques suivants s'appliquent spécifiquement à Data Crawler. 
    -   Data Crawler renouvelle les tentatives de téléchargement s'il détecte une erreur de téléchargement.
    -   Data Crawler ne peut pas renouveler le téléchargement de documents ayant été téléchargés mais dont la conversion ou l'indexation a échoué.
    -   Data Crawler ne dispose d'aucune fonction permettant de vérifier le statut en aval et d'essayer de renouveler le téléchargement des URL ayant échoué en aval.
    -   Il n'existe aucun moyen permettant de déterminer facilement lequel des documents a été ingéré par Data Crawler. Par exemple, si vous exécutez Data Crawler sur un groupe de 500 documents, il peut signaler des erreurs de soumission pour 65 documents sur une collection totale de 212 documents. Le statut des 223 documents restants est indéterminé.

        Une solution de contournement est disponible, mais elle est compliquée et implique d'appeler directement l'API. Contactez le support {{site.data.keyword.IBM}} pour obtenir de l'aide.
-   Les logiciels SDK Java, Python et Node.js pour {{site.data.keyword.discoveryshort}} ne fournissent pas toutes les fonctionnalités offertes par l'API REST par défaut (cURL). Les méthodes cURL n'ont pas toutes une méthode équivalente dans les logiciels SDK non-cURL, et toutes les méthodes non-cURL ne fournissent pas toutes les mêmes fonctions que leurs méthodes cURL équivalentes. En d'autres termes, actuellement, les logiciels SDK Java, Python et Node.js ne fournissent qu'un sous-ensemble des fonctions de l'API cURL.
-   Si vous utilisez le convertisseur Word, la mise en correspondance sur les en-têtes à l'aide de la clé `style` est beaucoup plus précise et efficace que celle effectuée avec la clé `level`.
