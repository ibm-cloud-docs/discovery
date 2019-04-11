---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-02-28"

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

# Plans de tarification Discovery
{: #discovery-pricing-plans}

Le service {{site.data.keyword.discoveryfull}} propose trois plans -- **Lite**, **Advanced** et **Premium** -- qui fournissent des niveaux différents de ressources et de fonctions adaptés à vos besoins.
{: shortdesc}

**Cas d'utilisation de données privées**  - Fonctions, limites et prix :

## Lite
{: #lite}

Taille | Limite de stockage de documents | Nombre de documents\* | Prix 
------ | ------ | ------ | ------  
N/A | 50 Mo | 1 000 par mois | Gratuit 

Le plan Lite est un plan de démarrage et ne doit pas être utilisé pour la production. Lorsque vous passez à un plan payant, vous pouvez conserver tous les documents ingérés.  Les instances de plan Lite sont supprimées après 30 jours d'inactivité. 

Attributs :
- 1 environnement
- Jusqu'à 2 collections
- Enrichissements NLU gratuits\*\*

Options supplémentaires :<br> [Modèles personnalisés](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-your-custom-model) :<br>
Un modèle Watson Knowledge Studio inclus. Modèles supplémentaires : Non disponible<br>[Element Classification](/docs/services/discovery?topic=discovery-element-classification#element-classification)\*\*\* :
500 pages incluses par mois. Pages supplémentaires : Non disponible <br>[Requêtes d'informations](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news) :
200 requêtes d'informations incluses par mois. Requêtes supplémentaires : Non disponible<br>[Extensions de requête](/docs/services/discovery?topic=discovery-query-concepts#query-expansion) :
500 extensions de requête avec un total de 1 000 termes. Extensions supplémentaires : Non disponible

Pour des informations sur la mise à niveau de la version Lite à Advanced, voir [Mise à niveau de votre service](/docs/services/discovery?topic=discovery-upgrading-your-plan#service)

Pour plus d'informations sur les performances des requêtes, voir [Performances des requêtes](/docs/services/discovery?topic=discovery-qp#qp). Les requêtes sont limitées en fonction du plan. Taux de requête moyen estimé pour les plans **Lite** et **Standard** : 1 QPS pour les requêtes reclassées avec deux zones de texte de niveau supérieur.

## Advanced
{: #advanced}

Lors du choix d'une taille de plan Advanced, notez que des ressources sont requises à la fois pour l'interrogation et le stockage de documents. C'est pourquoi, il est possible que vous ayez besoin d'un environnement de plus grande taille si vous approchez du nombre maximal de documents pour une taille de plan et que vous devez respecter les exigences suivantes : 

-  Exigences de performances des requêtes plus élevées (par exemple, entraînement visant à améliorer la pertinence)
-  Anticipation d'un grand nombre d'utilisateurs simultanés
-  Besoins de requête complexe 

Pour plus d'informations sur les facteurs qui influencent les performances des requêtes, voir [Performances des requêtes](/docs/services/discovery?topic=discovery-qp#qp). Les requêtes sont limitées en fonction du plan. Taux de requête moyen estimé pour les plans **Advanced** (S, MS) : 10 QPS pour les requêtes reclassées avec deux zones de texte de niveau supérieur.

Taille | Limite de stockage de documents | Nombre de documents\* | Prix 
------ | ------ | ------ | ------ 
X-Small\*\*\*\* | 40 Go | Jusqu'à 50 000 documents par mois | A partir de 500 $ par mois  
Small | 160 Go | Jusqu'à un million de documents par mois | A partir de 1 500 $ par mois  
Medium-Small | 320 Go | Jusqu'à deux millions de documents par mois | A partir de 3 000 $ par mois 
Medium| 640 Go | Jusqu'à quatre millions de documents par mois | A partir de 5 000 $ par mois 
Medium-Large | 1,2 To | Jusqu'à huit millions de documents par mois | A partir de 10 000 $ par mois 
Large| 2,4 To | Jusqu'à 16 millions de documents par mois | A partir de 15 000 $ par mois 
X-Large| 4 To | Jusqu'à 32 millions de documents par mois | A partir de 20 000 $ par mois 
XX-Large | 5,5 To | Jusqu'à 64 millions de documents par mois | A partir de 35 000 $ par mois 
XXX-Large | 12 To | Jusqu'à 100 millions de documents par mois | A partir de 45 000 $ par mois 

X-Small correspond au plus petit environnement disponible, recommandé pour le développement et le test uniquement.\*\*\*\*

Passer d'un niveau de la formule Advanced à un autre ne nécessite pas la création de nouvelles instances. De instances sont requises si vous passez d'un plan Advanced à un plan Premium. Pour des informations sur le passage d'un niveau Advanced à un autre, voir [Passage d'un niveau Advanced à un autre](/docs/services/discovery?topic=discovery-upgrading-your-plan#upgrading-your-plan).

\*\*\*\*Attributs des plans X-Small : 
- 1 environnement
- Jusqu'à 4 collections
- Enrichissements NLU gratuits\*\*

Attributs de tous les autres plans Advanced :
- 1 environnement
- Jusqu'à 100 collections
- Enrichissements NLU gratuits\*\*

Options supplémentaires :<br> [Modèles personnalisés](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-your-custom-model) :<br>
Un modèle Watson Knowledge Studio inclus. Modèles supplémentaires : 800 $ par modèle<br>[Element Classification](/docs/services/discovery?topic=discovery-element-classification#element-classification)\*\*\* :
500 pages incluses par mois. Pages supplémentaires : 0,40 $ par page<br>[Requêtes d'informations](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news) :
200 requêtes d'informations incluses par mois  
10 000 requêtes supplémentaires (par mois) : 0,10 $ la requête<br>
De 10 001 à 100 000 requêtes supplémentaires (par mois) : 0,05 $ la requête<br>
Au-delà de 100 000 requêtes (par mois) : 0,03 $ la requête<br>
[Extensions de requête](/docs/services/discovery?topic=discovery-query-concepts#query-expansion) :
5 000 extensions de requête avec un total de 25 000 termes

`-----`
<br>
\* La limite de document implique une taille moyenne de document de 100 ko sur disque. La taille d'un document est calculée après son passage par la conversion et l'enrichissement. Par conséquent, la taille peut être très différente de celle de l'entrée d'origine. Vous pouvez afficher le nombre de documents stockés et la quantité totale d'espace de stockage utilisée en vous servant de l'API [Environments](https://{DomainName}/apidocs/discovery#get-environment-info) ou [Collections](https://{DomainName}/apidocs/discovery#get-collection-details) ou des outils. Si la taille moyenne de vos documents dépasse les 100 ko sur disque, vous atteindrez la limite de stockage d'un plan avant la limite maximale du nombre de documents. Si vous effectuez une [segmentation de document](/docs/services/discovery?topic=discovery-configservice#doc-segmentation) sur vos documents, chaque segment compte comme un document distinct.

\*\* Les [enrichissements NLU (Natural Language Understanding)](/docs/services/discovery?topic=discovery-configservice#adding-enrichments) sont : Entity Extraction, Sentiment Analysis, Category Classification, Concept Tagging, Keyword Extraction, Relation Extraction, Emotion Analysis, Element Classification et Semantic Role Extraction.  Seuls les 50 000 premiers caractères de chaque document sont enrichis. 

\*\*\* Element Classification est un enrichissement qui permet d'effectuer rapidement une analyse syntaxique de documents constitutifs afin de convertir, d'identifier et de classifier des éléments importants. Il utilise le traitement automatique du langage naturel pour extraire les éléments suivants de documents PDF :  partie prenante (personne référencée), nature (type d'élément) et catégorie (classe spécifique).

Pour bénéficier des nouvelles options de dimensionnement d'environnement (`LT`, `XS`, `S`, `MS`, `M`, `ML`, `L`, `XL`, `XXL`, `XXXL`), vous devez utiliser la date de version de l'API `2018-08-01` ou une date ultérieure lors de la création d'environnements avec l'API. Les tailles d'environnement sont désormais de type `string` (précédemment le type était `integer`.)
{: note}

## Premium
{: #premiumplan}
   
Les plans Premium offrent aux développeurs et organisations une instance à service exclusif d'un ou de plusieurs services Watson pour un isolement et une sécurité accrus. Ces plans permettent un isolement au niveau ordinateur sur la plateforme partagée existante, ainsi que le chiffrement de bout en bout des données, que ces dernières soient en transit ou non. 

Pour plus d'informations, ou pour adhérer à un plan Premium, contactez le service des [ventes](https://ibm.biz/contact-wdc-premium). 

## Informations supplémentaires
{: #pricingadd}

Pour des informations sur le calcul des coûts, voir [IBM Cloud Pricing Calculator ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/pricing/platform/watson){: new_window}.

Pour des informations sur la sécurité d'IBM Cloud, voir [Cloud Services data security and privacy ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/software/sla/sladb.nsf/sla/csdsp?OpenDocument){: new_window}.

Pour obtenir des informations supplémentaires sur la tarification, voir le catalogue [{{site.data.keyword.discoveryshort}}![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/catalog/services/discovery){: new_window}.

## Remarques destinées aux clients possédant déjà des plans
{: #pricingnotes}

- A compter du **1er août 2018**, votre facturation et votre utilisation seront basées sur le plan de tarification ci-après.
- Le plan Lite a été réduit de 2 000 documents/400 requêtes {{site.data.keyword.discoverynewsshort}} par mois à 1 000 documents/200 requêtes {{site.data.keyword.discoverynewsshort}} par mois.  Si vous avez déjà dépassé les nouvelles limites du plan Lite, vous ne pourrez plus ajouter de document. Toutefois, vous pouvez continuer à l'utiliser ou effectuer une mise à niveau vers un plan Advanced ou Premium.
- Le plan Standard a été retiré et ne sera plus disponible pour les nouveaux utilisateurs. Si vous utilisez actuellement un plan Standard, vous pouvez continuer à l'utiliser ou effectuer une mise à niveau vers un plan Advanced ou Premium.
- Les plans Advanced et Premium sont désormais basés sur des niveaux de document et non plus des heures de document. Votre facture mensuelle ne changera pas à moins que vous ne changiez de niveau.
- Clients Premium, contactez le [service commercial ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://ibm.biz/contact-wdc-premium){: new_window} pour plus d'informations sur les changements de facturation.	
