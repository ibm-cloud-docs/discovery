---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-25"

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

# Mise à niveau de votre plan

Le service {{site.data.keyword.discoveryfull}} offre trois plans qui fournissent différents niveaux de ressources et de fonctions adaptés à vos besoins.
{: shortdesc}

Voir [Plans de tarification {{site.data.keyword.discoveryshort}}](/docs/services/discovery/pricing-details.html) et [{{site.data.keyword.discoveryshort}} catalog ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window} pour plus de détails.

## Mise à niveau de votre service
{: #service} 

Pour passer votre plan de Lite à Advanced :

1. Ouvrez le [tableau de bord {{site.data.keyword.Bluemix_notm}}](https://console.{DomainName}/dashboard). 
1. Cliquez sur votre instance de service {{site.data.keyword.discoveryshort}} pour ouvrir le tableau de bord du service {{site.data.keyword.discoveryshort}}.
1. Sur la page **Manage** de votre service {{site.data.keyword.discoveryshort}}, cliquez sur **Upgrade** pour sélectionner le plan Advanced. La page **Plan** s'ouvre. Suivez les étapes pour procéder à la mise à niveau. 
1. Retournez à la page **Manage** et cliquez sur **Launch Tool** pour ouvrir les outils {{site.data.keyword.discoveryshort}}.
   - Si vous n'avez jamais créé d'environnement pour votre plan Lite avant la mise à niveau vers Advanced, cliquez sur l'icône ![Rouage](images/icon_settings.png) et sélectionnez **Create environment**. Un écran affiche les options pour votre plan Advanced. Choisissez celui qui répond à vos besoins. (`X-Small`, `Small`, `Medium-Small`, `Medium`, `Medium-Large`, `Large`, `X-Large`, `XX-Large`).
   - Si vous avez créé un environnement pour votre plan Lite avant la mise à niveau vers Advanced, votre nouvel environnement de plan Advanced sera `Small` par défaut. 

## Passage d'un niveau Advanced à un autre
{: #advanced} 

Si vous disposez déjà d'un plan Advanced et souhaitez passer à un plan de taille supérieure, vous pouvez le faire à l'aide de l'[API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#update-environment){: new_window}. 

Pour des informations détaillées sur les limites de stockage et la tarification des plans Advanced, voir [Plans de tarification Advanced](/docs/services/discovery/pricing-details.html#advanced).

Vous pouvez mettre à niveau votre taille de plan Advanced, mais vous ne pouvez pas passer à une taille inférieure. Tailles de plan Advanced disponibles :  

Taille de plan | Libellé  
--------- | ------ 
X-Small | XS 
Small | S 
Medium-Small | MS 
Medium | M 
Medium-Large | ML 
Large | L
X-Large | XL 
XX-Large | XXL 

- L'analyse et l'indexation peuvent se poursuivre durant la mise à niveau. Le temps nécessaire à la mise à niveau dépendent de plusieurs facteurs. Vous pouvez interroger votre environnement à l'aide de l'API pendant que la mise à niveau se déroule.
- Passer d'un niveau de la formule Advanced à un autre ne nécessite pas la création de nouvelles instances.  
- Une fois la mise à niveau terminée, vous êtes facturé selon les tarifs du nouveau plan.

## Mise à niveau vers un plan Premium
{: #premium}

Si vous êtes intéressé par un plan Premium, contactez le service des [ventes](https://ibm.biz/contact-wdc-premium).  
