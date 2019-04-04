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

# Upgrade del tuo piano
{: #upgrading-your-plan}

Il servizio {{site.data.keyword.discoveryfull}} offre tre piani che forniscono diversi livelli di risorse e funzionalità per soddisfare i tuoi bisogni.
{: shortdesc}

Vedi [Piani dei prezzi di {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans) e il [catalogo {{site.data.keyword.discoveryshort}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/catalog/services/discovery){: new_window} per i dettagli.

## Upgrade del tuo servizio
{: #service}

Per ridimensionare il tuo piano da Lite ad Advanced:

1. Apri il [dashboard {{site.data.keyword.Bluemix_notm}}](https://{DomainName}/dashboard). 
1. Fai clic sulla tua istanza del servizio {{site.data.keyword.discoveryshort}} per aprire il dashboard del servizio {{site.data.keyword.discoveryshort}}.
1. Dalla pagina **Manage** del tuo servizio {{site.data.keyword.discoveryshort}}, fai clic su **Upgrade** per scegliere il piano Advanced. Questo aprirà la pagina **Plan**. Attieniti alla procedura per completare il tuo upgrade. 
1. Ritorna alla pagina **Manage** e fai clic su **Launch Tool** per aprire la strumentazione {{site.data.keyword.discoveryshort}}.
   - Se non avevi mai creato un ambiente per il tuo piano Lite prima dell'esecuzione dell'upgrade ad Advanced, fai clic sull'icona ![Cog](images/icon_settings.png) e scegli **Create environment**. Una schermata visualizzerà le opzioni per il tuo piano Advanced. Scegli quello adatto alle tue esigenze.  (`X-Small`, `Small`, `Medium-Small`, `Medium`, `Medium-Large`, `Large`, `X-Large`, `XX-Large`).
   - Se avevi creato un ambiente per il tuo piano Lite prima dell'esecuzione dell'upgrade ad Advanced, il tuo nuovo ambiente del piano Advanced sarà `Small` per impostazione predefinita. 

## Passaggio da un livello Advanced a un altro
{: #switchadvanced} 

Se già hai un piano Advanced, e vuoi eseguirne l'upgrade a una dimensione del piano più grande, puoi farlo utilizzando l'API [ ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/discovery#update-an-environment){: new_window}. 

Per informazioni dettagliate sui limiti di archiviazione e i prezzi del piano Advanced, vedi [Piani dei prezzi Advanced](/docs/services/discovery?topic=discovery-discovery-pricing-plans#advanced).

Le dimensioni del piano Advanced disponibili sono: 

Dimensione del piano | Etichetta  
--------- | ------ 
X-Small | XS 
Small | S 
Medium-Small | MS 
Medium | M 
Medium-Large | ML 
Large | L
X-Large | XL 
XX-Large | XXL 

- L'esecuzione delle query e quella dell'indicizzazione possono procedere durante l'upgrade. Il tempo richiesto per eseguire l'upgrade dipende da diversi fattori. Puoi eseguire il polling del tuo ambiente utilizzando l'API mentre l'upgrade viene completato.
- Il passaggio da un livello Advanced a un altro non richiede la creazione di nuove istanze. 
- Una volta completato l'upgrade, la fatturazione a tuo carico sarà basata sulla tariffa del nuovo piano.
- Se successivamente ti rendi conto che hai bisogno di una dimensione del piano più piccola, devi configurare la dimensione del piano appropriata, migrare i tuoi dati ed annullare quindi il piano più grande. 

## Upgrade a un piano Premium
{: #premium}

Se sei interessato a un piano Premium, contatta il settore [Vendite](https://ibm.biz/contact-wdc-premium).  
