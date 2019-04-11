---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-02-05"

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

# Watson Discovery News
{: #watson-discovery-news}

{{site.data.keyword.discoverynewsfull}} est inclus dans {{site.data.keyword.discoveryshort}}. {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} est un fichier indexé qui est prédéfini avec les connaissances cognitives suivantes : **Keyword Extraction**, **Entity Extraction**, **Semantic Role Extraction**, **Sentiment Analysis**, **Relation Extraction** et **Category Classification**. (Pour en savoir plus sur les enrichissements, voir [Ajout d'enrichissements](/docs/services/discovery?topic=discovery-configservice#adding-enrichments).) Les métadonnées suivantes sont également ajoutées : date d'exploration et date de publication. Il est possible de rechercher dans l'historique des articles de nouvelles parus au cours des 60 derniers jours. Regardez une démonstration illustrant ce que vous pouvez créer avec {{site.data.keyword.discoverynewsfull}} [en cliquant ici ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://discovery-news-demo.ng.bluemix.net/){: new_window}.

{{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} est mis à jour en continu avec de nouveaux articles, et est disponible en anglais, espagnol, allemand, coréen et japonais. La version anglaise de {{site.data.keyword.discoverynewsshort}} est quotidiennement mise à jour avec environ 300 000 nouveaux articles. La version espagnole de {{site.data.keyword.discoverynewsshort}} est mise à jour avec environ 60 000 nouveaux articles par jour, la version allemande avec environ 15 000 nouveaux articles par jour et la version coréenne avec 10 000 nouveaux articles par jour. La version japonaise de {{site.data.keyword.discoverynewsshort}} est quotidiennement mise à jour avec environ 17 000 nouveaux articles. Les sources des nouvelles varient en fonction de la langue, c'est pourquoi les résultats de requête pour chaque collection ne sont pas identiques.

Cas d'utilisation pour {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} :

- Système d'alerte sur les actualités - Crée de nouvelles alertes en tirant parti du support des objets entities, keywords, categories et sentiment analysis pour lire les articles d'actualité et voir de quelle manière ils sont perçus.

- Détection d'événements - L'extraction de rôle sémantique sujet/action/objet recherche des termes/actions, tels que "acquisition", "election results" ou "IPO".

- Sujets tendance dans les articles d'actualités - Identifier les sujets populaires et surveiller l'augmentation et la réduction de la fréquence ils (ou les sujets liés) sont mentionnés.

Pour plus d'informations sur l'écriture de requêtes pour {{site.data.keyword.discoverynewsfull}}, voir :
- [Exécution de requêtes sur Watson Discovery News](/docs/services/discovery?topic=discovery-query-concepts#querying-news)
- [Concepts de requête](/docs/services/discovery?topic=discovery-query-concepts)
- [Référence de requête](/docs/services/discovery?topic=discovery-query-reference#query-reference).

Vous ne pouvez pas ajuster la configuration de {{site.data.keyword.discoverynewsfull}}, former, ou ajouter des documents à la collection {{site.data.keyword.discoverynewsfull}}.

Les requêtes {{site.data.keyword.discoverynewsfull}} affichent approximativement 50 mots de chaque article dans la zone JSON `text`. Ces mots sont extraits des éléments mis en évidence. Pour obtenir une explication des éléments mis en évidence, voir [highlight](/docs/services/discovery?topic=discovery-query-parameters#highlight). Il n'est pas nécessaire d'inclure explicitement les éléments mis en évidence dans votre requête pour activer ce comportement.

Le nombre maximal de résultats renvoyés pour une requête {{site.data.keyword.discoverynewsfull}} est de `50`. Utilisez d'autres requêtes ainsi  que le paramètre `offset` pour renvoyer plus de `50` résultats.

**Remarque :** cette version de {{site.data.keyword.discoverynewsfull}} a débuté le **31 juillet 2017**. {{site.data.keyword.discoverynewsfull}} Original a été retiré du service le **15 janvier 2018**. Pour plus d'informations sur la migration, voir [Migration à partir de Watson Discovery News Original](/docs/services/discovery?topic=discovery-migrate-bwdn#migrate-bwdn).
