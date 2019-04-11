---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-03-07"

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

# Mise à niveau de votre plan
{: #upgrading-your-plan}

Le service {{site.data.keyword.discoveryfull}} offre trois plans qui fournissent différents niveaux de ressources et de fonctions adaptés à vos besoins.
{: shortdesc}

Pour plus de détails, voir [Plans de tarification {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans) et consultez le [catalogue {{site.data.keyword.discoveryshort}}![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/catalog/services/discovery){: new_window}.

## Mise à niveau de votre service
{: #service}

Pour passer votre plan de Lite à Advanced :

1. Ouvrez le tableau de bord [{{site.data.keyword.Bluemix_notm}}](https://{DomainName}/dashboard). 
1. Cliquez sur votre instance de service {{site.data.keyword.discoveryshort}} pour ouvrir le tableau de bord du service {{site.data.keyword.discoveryshort}}.
1. Sur la page **Manage** de votre service {{site.data.keyword.discoveryshort}}, cliquez sur **Upgrade** pour sélectionner le plan Advanced. La page **Plan** s'ouvre. Suivez les étapes pour procéder à la mise à niveau. 
1. Retournez à la page **Manage** et cliquez sur **Launch Tool** pour ouvrir les outils {{site.data.keyword.discoveryshort}}.
   - Si vous n'avez jamais créé d'environnement pour votre plan Lite avant la mise à niveau vers Advanced, cliquez sur l'icône ![Rouage](images/icon_settings.png) et sélectionnez **Create environment**. Un écran affiche les options pour votre plan Advanced. Choisissez celui qui répond à vos besoins.  (`X-Small`, `Small`, `Medium-Small`, `Medium`, `Medium-Large`, `Large`, `X-Large`, `XX-Large`).
   - Si vous avez créé un environnement pour votre plan Lite avant la mise à niveau vers Advanced, votre nouvel environnement de plan Advanced sera `Small` par défaut. 

## Passage d'un niveau Advanced à un autre
{: #switchadvanced} 

Si vous disposez déjà d'un plan Advanced et souhaitez passer à un plan de taille supérieure, vous pouvez le faire à l'aide de l'[API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/discovery#update-an-environment){: new_window}. 

Pour des informations détaillées sur les limites de stockage et la tarification des plans Advanced, voir [Plans de tarification Advanced](/docs/services/discovery?topic=discovery-discovery-pricing-plans#advanced).

Tailles de plan Advanced disponibles : 

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
- Si ultérieurement, vous estimez avoir besoin d'un plan de taille inférieure, vous devez configurer la taille de plan appropriée, migrer vos données puis annuler le plan de plus grande taille. 

## Mise à niveau vers un plan Premium
{: #premium}

Si vous êtes intéressé par un plan Premium, contactez le service des [ventes](https://ibm.biz/contact-wdc-premium).  
