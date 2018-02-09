---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-30"

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

# Watson Discovery News

{{site.data.keyword.discoverynewsfull}} est inclus dans {{site.data.keyword.discoveryshort}}. {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} est un fichier indexé qui est prédéfini avec les connaissances cognitives suivantes : **Keyword Extraction**, **Entity Extraction**, **Semantic Role Extraction**, **Sentiment Analysis**, **Relation Extraction** et **Category Classification**. (Pour en savoir plus sur les enrichissements, voir [Ajout d'enrichissements](building.html#adding-enrichments).) Les métadonnées suivantes sont également ajoutées : date d'exploration et date de publication. Il est possible de rechercher dans l'historique des articles de nouvelles parus au cours des 60 derniers jours. Regardez une démonstration illustrant ce que vous pouvez créer avec {{site.data.keyword.discoverynewsfull}} [en cliquant ici ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://discovery-news-demo.mybluemix.net/){: new_window}.

{{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} est continuellement mis à jour avec de nouveaux articles. La version anglaise de {{site.data.keyword.discoverynewsshort}} est quotidiennement mise à jour avec environ 300 000 nouveaux articles. La version espagnole de {{site.data.keyword.discoverynewsshort}} est quotidiennement mise à jour avec environ 60 000 nouveaux articles ; la version coréenne de {{site.data.keyword.discoverynewsshort}} est quotidiennement mise à jour avec 10 000 nouveaux articles.

Cas d'utilisation pour {{site.data.keyword.watson}} {{site.data.keyword.discoverynewsshort}} :

- Système d'alerte sur les actualités - Crée de nouvelles alertes en tirant parti du support des objets entities, keywords, categories et sentiment analysis pour lire les articles d'actualité et voir de quelle manière ils sont perçus. 

- Détection d'événements - L'extraction de rôle sémantique sujet/action/objet recherche des termes/actions, tels que "acquisition", "election results" ou "IPO".

- Sujets tendance dans les articles d'actualités - Identifier les sujets populaires et surveiller l'augmentation et la réduction de la fréquence ils (ou les sujets liés) sont mentionnés. 

Pour plus d'informations sur l'écriture de requêtes pour {{site.data.keyword.discoverynewsfull}}, voir [Concepts de requête](/docs/services/discovery/using.html) et [Référence de requête](/docs/services/discovery/query-reference.html).

Vous ne pouvez pas ajuster la configuration de {{site.data.keyword.discoverynewsfull}}, former, ou ajouter des documents à la collection {{site.data.keyword.discoverynewsfull}}. 

**Remarque :** le nombre maximal de résultats pouvant être renvoyés pour une requête Watson Discovery News est `50`. Utilisez d'autres requêtes ainsi  que le paramètre `offset` pour renvoyer plus de `50` résultats. 

**Remarque :** cette version de {{site.data.keyword.discoverynewsfull}} a débuté le **31 juillet 2017**. La version d'origine a été renommée {{site.data.keyword.discoverynewsfull}} Original et son retrait est prévu le **15 janvier 2018**. Pour plus d'informations sur la migration, voir [Migration à partir de Watson Discovery News Original](/docs/services/discovery/migrate-bwdn.html).
