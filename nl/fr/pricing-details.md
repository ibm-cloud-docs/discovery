---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-17"

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

Le service {{site.data.keyword.discoveryfull}} propose trois plans -- **Lite**, **Advanced** et **Premium** -- qui fournissent des niveaux différents de ressources et de fonctions adaptés à vos besoins.
{: shortdesc}

**Cas d'utilisation de données privées**  - Fonctions, limites et prix : 

## Lite
{: #lite}

Taille | Limite de stockage de documents | Nombre de documents\* | Prix 
------ | ------ | ------ | ------  
N/A | 50 Mo | 1 000 par mois | Gratuit 

Le plan Lite est un plan de démarrage et ne doit pas être utilisé pour la production. Lorsque vous passez à un plan payant, vous pouvez conserver tous les documents ingérés. Les instances de plan Lite sont supprimées après 30 jours d'inactivité. 

Attributs :
- 1 environnement
- Jusqu'à 2 collections
- Enrichissements NLU gratuits\*\*
- 20 documents en cours\*\*\*\* 

Options supplémentaires :<br> [Modèles personnalisés](/docs/services/discovery/integrate-wks.html#integrating-your-custom-model) :<br>
Un modèle Watson Knowledge Studio inclus. Modèles supplémentaires : Non disponible<br>[Element Classification](/docs/services/discovery/element-classification.html)\*\*\* :
500 pages incluses par mois. Pages supplémentaires : Non disponible <br>[Requêtes d'informations](/docs/services/discovery/watson-discovery-news.html) :
200 requêtes d'informations incluses par mois. Requêtes supplémentaires : Non disponible <br>[Extensions de requête](/docs/services/discovery/using.html#query-expansion) :
500 extensions de requête avec un total de 1 000 termes. Extensions supplémentaires : Non disponible

Pour des informations sur la mise à niveau de la version Lite à Advanced, voir [Mise à niveau de votre service](/docs/services/discovery/upgrading.html#service)

## Advanced
{: #advanced}

Taille | Limite de stockage de documents | Nombre de documents\* | Prix 
------ | ------ | ------ | ------ 
X-Small\*\*\*\*\* | 40 Go | Jusqu'à 50 000 documents par mois | A partir de 500 $ par mois  
Small | 160 Go | Jusqu'à un million de documents par mois | A partir de 1 500 $ par mois  
Medium-Small | 320 Go | Jusqu'à deux millions de documents par mois | A partir de 3 000 $ par mois  
Medium| 640 Go | Jusqu'à quatre millions de documents par mois | A partir de 5 000 $ par mois  
Medium-Large | 1,2 To | Jusqu'à huit millions de documents par mois | A partir de 10 000 $ par mois  
Large| 2,4 To | Jusqu'à 16 millions de documents par mois | A partir de 15 000 $ par mois  
X-Large| 4 To | Jusqu'à 32 millions de documents par mois | A partir de 20 000 $ par mois  
XX-Large | 5,5 To | Jusqu'à 64 millions de documents par mois | A partir de 35 000 $ par mois  
XXX-Large | 12 To | Jusqu'à 100 millions de documents par mois | A partir de 45 000 $ par mois  

X-Small correspond au plus petit environnement disponible, recommandé pour le développement et le test uniquement.\*\*\*\*\*

Passer d'un niveau de la formule Advanced à un autre ne nécessite pas la création de nouvelles instances. De instances sont requises si vous passez d'un plan Advanced à un plan Premium. Pour des informations sur le passage d'un niveau Advanced à un autre, voir [Passage d'un niveau Advanced à un autre](/docs/services/discovery/upgrading.html#advanced).

\*\*\*\*\*Attributs des plans X-Small : 
- 1 environnement
- Jusqu'à 4 collections
- Enrichissements NLU gratuits\*\*
- 50 documents en cours\*\*\*\*

Attributs de tous les autres plans Advanced :
- 1 environnement
- Jusqu'à 100 collections
- Enrichissements NLU gratuits\*\*
- 105 documents en cours\*\*\*\*

Options supplémentaires :<br> [Modèles personnalisés](/docs/services/discovery/integrate-wks.html#integrating-your-custom-model) :<br>
Un modèle Watson Knowledge Studio inclus. Modèles supplémentaires : 800 $ par modèle<br>[Element Classification](/docs/services/discovery/element-classification.html)\*\*\* :
500 pages incluses par mois. Pages supplémentaires : 0,40 $ par page <br>[Requêtes d'informations](/docs/services/discovery/watson-discovery-news.html) :
200 requêtes d'informations incluses par mois   
10 000 requêtes supplémentaires (par mois) : 0,10 $ la requête<br>
De 10 001 à 100 000 requêtes supplémentaires (par mois) : 0,05 $ la requête<br>
Au-delà de 100 000 requêtes (par mois) : 0,03 $ la requête<br>
[Extensions de requête](/docs/services/discovery/using.html#query-expansion) :
5 000 extensions de requête avec un total de 25 000 termes 

## Premium
   
Les plans Premium offrent aux développeurs et organisations une instance à service exclusif d'un ou de plusieurs services Watson pour un isolement et une sécurité accrus. Ces plans permettent un isolement au niveau ordinateur sur la plateforme partagée existante, ainsi que le chiffrement de bout en bout des données, que ces dernières soient en transit ou non. 

Pour plus d'informations, ou pour adhérer à un plan Premium, contactez le service des [ventes](https://ibm.biz/contact-wdc-premium). 
<br>
<br> 

**Remarque :** La date de version de l'API a été mise à jour : `2018-08-01`. Pour bénéficier des nouvelles options de dimensionnement d'environnement (`LT`, `XS`, `S`, `MS`, `M`, `ML`, `L`, `XL`, `XXL`, `XXXL`), vous devez utiliser cette nouvelle date de version lors de la création d'environnements avec l'API. Les tailles d'environnement sont désormais de type `string` (précédemment le type était `integer`.)

\* La limite de document implique une taille moyenne de document de 100 ko sur disque. La taille d'un document est calculée après son passage par la conversion et l'enrichissement. Par conséquent, la taille peut être très différente de celle de l'entrée d'origine. Vous pouvez afficher le nombre de documents stockés et la quantité totale d'espace de stockage utilisée en vous servant de l'API [Environments](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#environments-api) ou [Collections](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#collections-api) ou des outils. Si la taille moyenne de vos documents dépasse les 100 ko sur disque, vous atteindrez la limite de stockage d'un plan avant la limite maximale du nombre de documents. Si vous effectuez une [segmentation de document](https://console.bluemix.net/docs/services/discovery/building.html#doc-segmentation) sur vos documents, chaque segment compte comme un document distinct.

\*\* Les [enrichissements NLU (Natural Language Understanding)](https://console.bluemix.net/docs/services/discovery/building.html#adding-enrichments) sont : Entity Extraction, Sentiment Analysis, Category Classification, Concept Tagging, Keyword Extraction, Relation Extraction, Emotion Analysis, Element Classification et Semantic Role Extraction. Seuls les 50 000 premiers caractères de chaque document sont enrichis.  

\*\*\* Element Classification est un enrichissement qui permet d'effectuer rapidement une analyse syntaxique de documents constitutifs afin de convertir, d'identifier et de classifier des éléments importants. Il utilise le traitement automatique du langage naturel pour extraire les éléments suivants de documents PDF :  partie prenante (personne référencée), nature (type d'élément) et catégorie (classe spécifique). 

\*\*\*\* Si vous atteignez la limite en cours, vous devrez ralentir votre taux d'ingestion. Lors de l'utilisation d'un service Discovery, un document est dit "en cours" lorsqu'il est téléchargé, enrichi puis traité avant d'être ajouté à une collection.

Pour des informations sur le calcul des coûts, voir [IBM Cloud Pricing Calculator ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.bluemix.net/pricing/platform/watson){: new_window}.

Pour des informations sur la sécurité d'IBM Cloud, voir [Cloud Services data security and privacy ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/software/sla/sladb.nsf/sla/csdsp?OpenDocument){: new_window}.

Pour des informations supplémentaires sur la tarification, voir le [catalogue {{site.data.keyword.discoveryshort}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.bluemix.net/catalog/services/discovery){: new_window}.

## Remarques destinées aux clients possédant déjà des plans

- A compter du **1er août 2018**, votre facturation et votre utilisation seront basées sur le plan de tarification ci-après.
- Le plan Lite a été réduit de 2 000 documents/400 requêtes {{site.data.keyword.discoverynewsshort}} par mois à 1 000 documents/200 requêtes {{site.data.keyword.discoverynewsshort}} par mois. Si vous avez déjà dépassé les nouvelles limites du plan Lite, vous ne pourrez plus ajouter de document. Toutefois, vous pouvez continuer à l'utiliser ou effectuer une mise à niveau vers un plan Advanced ou Premium.
- Le plan Standard a été retiré et ne sera plus disponible pour les nouveaux utilisateurs. Si vous utilisez actuellement un plan Standard, vous pouvez continuer à l'utiliser ou effectuer une mise à niveau vers un plan Advanced ou Premium. 
- Les plans Advanced et Premium sont désormais basés sur des niveaux de document et non plus des heures document. Votre facture mensuelle ne changera pas à moins que vous ne changiez de niveau. 
- Pour les clients Premium, contactez le service des [ventes](https://ibm.biz/contact-wdc-premium) pour connaître les détails des changements de facturation. 	
