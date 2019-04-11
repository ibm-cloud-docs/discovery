---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-01-10"

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

# Sécurité de l'information
{: #information-security}

IBM se donne pour mission de fournir à ses clients et partenaires des solutions innovantes de confidentialité, de sécurité et de gouvernance des données.
{: shortdesc}

**Remarque :**
Il appartient à chaque entreprise de se conformer aux lois et réglementations, notamment relatives à la protection des données personnelles. Il relève de la seule responsabilité du client de consulter les services juridiques compétents aussi bien pour identifier et interpréter les lois et règlements susceptibles d’affecter son activité, que pour toute action à entreprendre pour se mettre en conformité avec ces lois et réglementations.

Les produits, services et autres fonctionnalités décrits ici ne sont pas adaptés à toutes les situations client et ne pourront être proposés que sous réserve de disponibilité. IBM ne donne aucun avis juridique, comptable ou d'audit et ne garantit pas que ses produits ou services permettent aux clients de se conformer aux lois ou réglementations applicables.

Si vous avez besoin d'une assistance RGPD pour les ressources {{site.data.keyword.cloud}} {{site.data.keyword.watson}} qui sont créées

-   Dans l'Union européenne (EU), voir [Demande de support pour des ressources IBM Cloud Watson créées dans l'Union européenne](/docs/services/watson/getting-started-gdpr-sar.html#request-EU).
-   Hors UE, voir [Demande de support pour des ressources hors Union européenne](/docs/services/watson/getting-started-gdpr-sar.html#request-non-EU).

## Règlement général sur la protection des données (RGPD) de l'Union Européenne
{: #gdpr}

IBM se donne pour mission de fournir à ses clients et partenaires des solutions innovantes de confidentialité, de sécurité et de gouvernance des données pour les accompagner dans leur mise en conformité au RGPD.

Pour en savoir plus sur le parcours préparatoire au RGPD d'IBM ainsi que sur nos session proposées et offres liées au RGPD pour la prise en charge de votre parcours de conformité, cliquez [ici ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/gdpr){: new_window}.

## Etiquetage et suppression de données dans {{site.data.keyword.discoveryshort}}
{: #gdpr-discovery}

Le service {{site.data.keyword.discoveryshort}} inclut une API permettant de libeller les données par appel.

Cette API vous permet de :

- Libeller vos données avec un ID client.
- Supprimer toutes les données d'un ID client spécifique, y compris les avis connexes.

Les données sont libellées en ajoutant l'`customer_id` de votre choix (voir les restrictions dans [Comment libeller des données](/docs/services/discovery?topic=discovery-information-security#labeling)) à l'en-tête facultatif `X-Watson-Metadata`. {{site.data.keyword.discoveryshort}} peut ensuite les supprimer par `customer_id`.

Dans tout appel REST, un en-tête facultatif `X-Watson-Metadata` peut être envoyé avec des paires `field=value` séparées par des points-virgules, où un seul `customer_id` est actuellement conservé. En ajoutant cet `customer_id` à l'en-tête `X-Watson-Metadata`, la demande indique qu'elle contient des données appartenant à cet `customer_id`.

Les `customer_id` sont uniques au sein d'une même instance de service {{site.data.keyword.discoveryshort}}. Ils ne sont PAS uniques par environnement ou collection. Ils ne doivent pas comporter de données personnelles.

**Remarque :** Les fonctions expérimentales et bêta ne sont pas destinées à un usage en environnement de production. Il n'est donc pas garanti qu'elles fonctionnent comme prévu lors de l'utilisation de l'étiquetage et de la suppression de données. Les fonctions expérimentales et bêta ne doivent pas être utilisées lors de l'implémentation d'une solution nécessitant l'étiquetage et la suppression de données.

## Méthodes prenant en charge l'étiquetage des données
{: #pi_methods}

Les informations stockées suivantes peuvent être supprimées en utilisant un `customer_id` si ce `customer_id` a été spécifié lors de l'ajout original d'informations à l'aide de la méthode associée :

- requêtes (`/v1/environments/{environment_id}/collections/{collection_id}/query`) Uniquement avec les paramètres `passages` ou `natural_language_query`
- événements (`/v1/events`)
- documents (`/v1/environments/{environment_id}/collections/{collection_id}/documents`)
- avis (`/v1/environments/{environment_id}/collections/{collection_id}/notices`) Seuls les `notices` d'ingestion sont libellés.
- entités Knowledge Graph (`/v1/environments/{environment_id}/collections/{collection_id}/query_entities`)
- relations Knowledge Graph (`/v1/environments/{environment_id}/collections/{collection_id}/query_relations`)
- données d'apprentissage (`/v1/environments/{environment_id}/collections/{collection_id}/training_data`)

Les informations stockées suivantes ne sont pas explicitement libellées et ne peuvent pas être supprimées en spécifiant un `customer_id`. Les données personnelles ne sont pas prises en charge dans ces zones.

Toute zone de chaîne (y compris, mais non limité à `name` et `description`) des éléments stockés suivants :
- configurations
- collections
- environnements

## Etiquetage des données
{: #labeling}

Lors de l'ingestion de documents, incluez l'en-tête `X-Watson-Metadata` à l'aide d'opérations `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` ou `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/ID`. La zone `customer_id` est ajoutée aux `extracted_metadata` des documents. Votre application doit être configurée pour fournir un `customer_id` dans l'en-tête `X-Watson-Metadata` lors de l'exécution d'une opération.

Vous avez la possibilité d'inclure la zone `customer_id` avec la portion de formulaire à plusieurs parties `metadata` plutôt que d'utiliser l'en-tête `X-Watson-Metadata`.

**Remarque :** Si vos documents ont déjà été ingérés, vous devrez à nouveau les verser pour ajouter l'en-tête `X-Watson-Metadata` et le `customer_id`.

**Remarque :** Si vous spécifiez `customer_id` dans le formulaire à plusieurs parties `metadata` ET l'en-tête `X-Watson-Metadata` pour le même document, le `customer_id` de l'en-tête `X-Watson-Metadata` sera utilisé.

Restrictions :

- La valeur de l'en-tête `X-Watson-Metadata` ne doit pas dépasser 4 kilooctets de texte.
- L'en-tête `X-Watson-Metadata` doit comporter une liste de paires `field=value` séparées par des points-virgules. `field` et `value` ne doivent pas contenir de point-virgule (`;`) ni de signe égal (`=`).
- Les `customer_id` sont uniques au sein de chaque instance {{site.data.keyword.discoveryshort}}. Ils ne sont PAS uniques par environnement ou collection.
- La longueur d'un `customer_id` ne doit pas dépasser 256 caractères.
- Si un `customer_id` contient uniquement un blanc ou est totalement vide, il sera traité comme si le `customer_id` n'avait pas été fourni et aucun message d'erreur ne sera renvoyé.

### Etiquetage de données à l'aide des outils Discovery
{: #labelingtooling}

Les données peuvent être libellées avec une zone `customer_id` lors de l'utilisation des outils {{site.data.keyword.discoveryshort}}. Cliquez sur l'icône ![Environment details](images/env_icon.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> et entrez l'élément `customer_id` dans la zone **GDPR Data Label**. Une fois cette zone définie, toutes les données téléchargées durant cette session de navigation seront libellées avec le `customer_id` spécifié. Cette zone doit être changée manuellement si l'ID client associé change.

L'ajout d'un `customer_id` via la zone **GDPR Data Label** permet de libeller les documents, notices/avis, entités Knowledge Graph, relations Knowledge Graph et données d'apprentissage de ce domaine d'URL à partir de maintenant, y compris chaque instance sous ce domaine. Tout action (chargements de document inclus) qui s'est produite dans les outils {{site.data.keyword.discoveryshort}} avant l'ajout de la zone **GDPR Data Label** ne sera pas libellée.

**Remarque :** Si vous changez de domaine, de navigateur, videz le cache du navigateur ou démarrez une session en mode navigation privée après avoir spécifié votre `customer_id` via la zone **GDPR Data Label** des outils {{site.data.keyword.discoveryshort}}, le `customer_id` ne sera pas conservé et vos données ne seront pas libellées. Si vous devez changer de domaine ou de navigateur, entrez à nouveau le `customer_id` dans la zone **GDPR Data Label**.

### Etiquetage de documents à l'aide de Data Crawler
{: #labelingdc}

Si des documents ont déjà été explorés à l'aide de Data Crawler, vous devrez les réexplorer pour ajouter l'en-tête `X-Watson-Metadata` et le `customer_id`.

1. Mettez à jour votre configuration d'adaptateur de sortie {{site.data.keyword.discoveryshort}} Data Crawler afin d'inclure le `customer_id`. Voir [Configuration de l'adaptateur de sortie](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#output-adapter).
1. Planifiez une exploration. Les documents sont soumis à {{site.data.keyword.discoveryshort}} à l'aide de l'en-tête `X-Watson-Metadata`, et ils seront libellés avec le `customer_id` configuré.

## Suppression de données libellées
{: #deletingdata}

Les données doivent être libellées avec un `customer_id` pour pouvoir être supprimées ultérieurement.

1. Utilisez l'opération `DELETE /v1/user_data` et indiquez le `customer_id` des données que vous souhaitez supprimer. `DELETE /v1/user_data` supprime toutes les données associées à un `customer_id` particulier au sein de cette instance de service, comme spécifié dans les [méthodes prenant en charge l'étiquetage des données](/docs/services/discovery?topic=discovery-information-security#pi_methods). Voir également [API reference ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery#delete-labeled-data){: new_window}

Les suppressions sont effectuées de manière asynchrone. Vous ne pouvez pas suivre la progression des suppressions.

Pour vérifier que l'ensemble du contenu libellé a été correctement retiré, `user_delete` doit être exécuté une fois que le nombre indiqué pour les éléments `processing` et `pending` pour toutes les collections de votre environnement est égal à la valeur `0`.

Si un `customer_id` inexistant est fourni, rien n'est supprimé, mais une réponse `200 - OK` est renvoyée.

Les environnements et collections ne sont pas libellés avec un `customer_id`, même si un en-tête `X-Watson-Metadata` est inclus dans la demande de création de l'environnement ou de la collection. Seuls les documents individuels d'une collection au sein d'un environnement sont libellés. C'est pourquoi, lorsque des données sont supprimées, les environnements et collections individuels ne sont PAS supprimés.

Vous ne pouvez pas supprimer de données libellées à l'aide des outils {{site.data.keyword.discoveryshort}}.
