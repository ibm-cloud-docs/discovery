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

# Plans de tarification Discovery

Le service {{site.data.keyword.discoveryfull}} offre trois plans qui fournissent différents niveaux de ressources et de fonctions adaptés à vos besoins.
{: shortdesc}

Les limites et les prix des **cas d'utilisation de données privées** sont les suivants :

| Lite                     |  Standard         | Advanced          | Premium          |
|--------------------------|-------------------|-------------------|-------------------|
| Jusqu'à 2 000 documents simultanés par mois\*   |Jusqu'à 10 000 documents simultanés par mois\*  <br/> 10 $ par tranche de 1 000 documents simultanés par mois ($0.0139USD/1000Doc/Hr)\*\*\*<br/> Gratuit pour 2 000 documents par mois\*\*\*\*  | **Environnement réservé**</br>Taux de base de 1 000 $/mois <br/> Jusqu'à 1,000 000 documents par mois\*<br/> 5 $ par tranche de 1 000 documents simultanés par mois ($0.00694 USD/1000Doc/Hr)\*\*\*<br/> 100 000 documents par mois inclus\*\*\*\*</br> Pour des environnements plus grands, contactez un [interlocuteur IBM ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/marketing/iwm/dre/signup?source=MAIL-watson){: new_window}.| Les **plans Premium** offrent aux développeurs et organisations une instance à service exclusif d'un ou de plusieurs services Watson pour un isolement et une sécurité accrus. Ces plans permettent un isolement au niveau ordinateur sur la plateforme partagée existante, ainsi que le chiffrement de bout en bout des données, que ces dernières soient en transit ou non. Pour plus d'informations, ou pour adhérer à un plan Premium, contactez un [interlocuteur IBM![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://ibm.biz/contact-wdc-premium){: new_window} |
| 200 Mo\*\*                  |10 Go\*\*  | 80 Go\*\* |-|
| Jusqu'à 2 collections      |Jusqu'à 4 collections | Jusqu'à 100 collections|-|
| Jusqu'à 1 modèle personnalisé {{site.data.keyword.knowledgestudiofull}} |Jusqu'à 1 modèle personnalisé {{site.data.keyword.knowledgestudioshort}} | Nombre illimité de modèles personnalisés {{site.data.keyword.knowledgestudioshort}} <br/>1 modèle personnalisé {{site.data.keyword.knowledgestudioshort}} inclus<br/>800 $ supplémentaires par modèle {{site.data.keyword.knowledgestudioshort}} chaque mois|-|

**Remarque :** dans tous les abonnements, les 1 000 premières requêtes {{site.data.keyword.discoverynewsshort}} par mois sont gratuites. Les requêtes {{site.data.keyword.discoverynewsshort}} sont facturées 0,10 $ par requête après les 1 000 premières requêtes. 

**Remarque :** les services du plan Lite sont supprimés au bout de 30 jours d'inactivité. Un environnement gratuit est alloué par organisation avec les plans Lite. 

 \* La limite du nombre de documents suppose une taille de document moyenne de 100 Ko sur disque. Il s'agit de la taille d'un document dans une collection après que celui-ci a été converti et enrichi, par conséquent, la taille peut être très différente de celle de l'entrée d'origine. Vous pouvez afficher le nombre de documents stockés et la quantité totale d'espace de stockage utilisée en vous servant de l'API `environments` ou `collections` ou des outils. 

 \*\* Si la taille moyenne de vos documents est supérieure à 100 Ko sur disque, vous atteindrez la limite de stockage d'un plan avant d'atteindre le nombre maximal limite de documents. 

 \*\*\* Le prix est basé sur le nombre d'heures de stockage d'un lot de 1 000 documents dans le service (nombre d'heures de stockage de 1 000 documents). Pour la calculatrice des prix, il s'agit du chiffre qui devrait être entré  (`nombre de documents * nombre d'heures de stockage de ces documents par mois / 1000`).

 \*\*\*\* La gratuité mensuelle est basée sur le nombre équivalent de documents stockés pendant un mois. Par exemple, dans le plan Standard, le montant de la gratuité est équivalent à 2 000 documents * 720 heures / lot de 1 000 documents = 1440 heures de stockage de 1 000 documents. 

**Exemple :** un utilisateur ayant souscrit au plan Standard stocke 4 000 documents pendant la totalité du mois. Il devrait être facturé comme suit :

- `4 000 documents * 720 heures (dans un mois) / 1 000 = 2 880` heures consommées pour 1 000 documents

- `2 880 - 1 440 (heures gratuites de document) = 1 440` heures facturables pour 1 000 documents

- `1 440 * 0,0139 $` (prix par heure de 1 000 documents) = `20 £` pour le mois

**Remarque :** lors du calcul du montant facturé chaque heure, le nombre total de documents stockés est arrondi au millier de documents le plus proche dans le cadre du calcul. Par exemple, si 4 678 documents sont stockés pour 1 heure, ce nombre est arrondi à 5 000 et par conséquent, 5 mille documents par heure seront facturés sur le compte. 

**Remarque :** il n'y a aucun frais supplémentaire pour les enrichissements. 

Pour plus d'informations sur la sécurité {{site.data.keyword.Bluemix_notm}}, voir la page [{{site.data.keyword.Bluemix_notm}} Service Description ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=IBM+Bluemix+Service+Description){: new_window}.

## Conversion à partir des plans de tarification précédents

Les clients ayant déjà souscrit à un plan avant le **1 août 2017** ont fait l'objet d'une migration vers les nouveaux plans. 

- Les clients qui bénéficiaient du plan d'essai gratuit de 30 jours ont fait l'objet d'une migration vers le plan **Lite**.
Suite à cette transition, il se peut que les utilisateurs aient atteint ou dépassé les limites du plan Lite relatives au nombre de documents (_2000_), à la capacité de stockage (_200 Mo_ ou au nombre de collections (_2_). Si vous atteint la limite du plan **Lite**, vous ne pouvez pas ajouter d'autre contenu dans le service, mais vous pouvez toujours exécuter des requêtes sur les collections. Vous pouvez afficher l'état en cours de toutes ces limites en utilisant les outils ou l'API {{site.data.keyword.discoveryshort}}. Pour pouvoir recommencer à ajouter du contenu à l'instance {{site.data.keyword.discoveryshort}}, vous devez exécuter l'une des actions suivantes : 
  - Retirer des collections et/ou des documents de manière à ne dépasser les limites du plan **Lite**.
Les documents peuvent être supprimés individuellement à l'aide de l'API via la méthode [delete-doc ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-doc){: new_window} ou des collections entières peuvent être supprimées à l'aide des outils ou de l'API via la méthode [delete-collection ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-collection){: new_window}. 
  - Effectuer une mise à niveau de votre plan vers un niveau qui répond à vos besoins en matière de stockage. 
- Les clients ayant des environnements dont la taille est **`1`**, **`2`** ou **`3`** ont fait l'objet d'une migration automatique vers le plan **Advanced**.
  Si vous avez fait l'objet d'une migration vers le niveau Advanced et que vous possédez moins de 100 000 documents et 4 collections, vous pouvez passer au niveau Standard afin de réduire vos coûts. Cela nécessite de créer une nouvelle instance Discovery dans le plan Standard et de reverser des données dans la nouvelle instance. Cette opération d'ingestion peut être réalisée à l'aide des outils, des API ou de Data Crawler.

Pour plus d'informations sur la tarification, voir le [catalogue {{site.data.keyword.discoveryshort}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window}. 
