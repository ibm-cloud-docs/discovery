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

# Sicurezza delle informazioni
{: #information-security}

IBM si impegna a fornire ai nostri clienti e partner soluzioni innovative per la privacy, la sicurezza e la governance dei dati.
{: shortdesc}

**Avviso:**
I clienti sono responsabili per la garanzia della propria conformità alle varie leggi e normative, incluso il Regolamento generale sulla protezione dei dati dell'Unione Europea. È responsabilità esclusiva dei clienti richiedere una consulenza legale qualificata per identificare e interpretare normative e regolamenti importanti che potrebbero influenzare le attività di business dei clienti ed eventuali azioni che i clienti dovranno intraprendere per rispettare la conformità a tali normative e regolamenti.

I prodotti, i servizi e le altre funzionalità qui descritti non sono adatti per tutte le situazioni dei clienti e potrebbero avere una disponibilità limitata. IBM non fornisce consulenza legale, contabile o di controllo né dichiara o garantisce che i propri servizi o prodotti assicureranno che i clienti siano conformi ad eventuali norme di legge o regolamentari.

Se hai bisogno di richiedere il supporto GDPR per le risorse {{site.data.keyword.cloud}} {{site.data.keyword.watson}} che vengono create

-   Nell'Unione Europea (EU), consulta [Requesting support for IBM Cloud Watson resources created in the European Union](/docs/services/watson/getting-started-gdpr-sar.html#request-EU).
-   Al di fuori dell'Unione Europea (EU), consulta [Requesting support for resources outside the European Union](/docs/services/watson/getting-started-gdpr-sar.html#request-non-EU).

## Regolamento generale sulla protezione dei dati dell'Unione europea (GDPR)
{: #gdpr}

IBM si impegna a offrire ai nostri clienti e partner soluzioni innovative per la privacy, la sicurezza e la governance dei dati per assisterli nel loro percorso verso la conformità GDPR.

È possibile trovare ulteriori informazioni sul percorso di preparazione verso la disponibilità GDPR e sulle nostre funzionalità e offerte GDPR che supportano il tuo percorso di conformità [qui ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](../../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/gdpr){: new_window}.

## Etichettatura ed eliminazione dei dati in {{site.data.keyword.discoveryshort}}
{: #gdpr-discovery}

Il servizio {{site.data.keyword.discoveryshort}} include un'API per etichettare i dati per chiamata.

Con questa API puoi:

- Etichettare i tuoi dati con un ID cliente.
- Eliminare tutti i dati per un ID cliente specifico, inclusi gli avvisi correlati.

I dati vengono etichettati aggiungendo un `customer_id` di tua scelta (vedi le limitazioni in [Come etichettare i dati](/docs/services/discovery?topic=discovery-information-security#labeling)) all'intestazione `X-Watson-Metadata` facoltativa. {{site.data.keyword.discoveryshort}} può quindi eliminarli per il `customer_id`.

Su qualsiasi chiamata REST, può essere inviata un'intestazione facoltativa `X-Watson-Metadata` con le coppie `field=value` separate da punti e virgola, dove al momento viene conservato solo il `customer_id`. Aggiungendo tale `customer_id` nell'intestazione `X-Watson-Metadata`, la richiesta indica che contiene i dati che appartengono a questo `customer_id`.

I `customer_id` sono univoci in una sola istanza del servizio {{site.data.keyword.discoveryshort}}. NON sono univoci per l'ambiente o la raccolta. Non dovrebbero includere dati personali.

**Nota:** le funzioni sperimentale e beta non sono destinate per essere utilizzate con un ambiente di produzione e quindi non è garantito che funzionino come previsto quando si etichettano ed eliminano i dati. Le funzioni sperimentale e beta non dovrebbero essere utilizzate durante l'implementazione di una soluzione che richiede l'etichettatura e l'eliminazione dei dati.

## Metodi che supportano l'etichettatura dei dati
{: #pi_methods}

Le seguenti informazioni archiviate possono essere eliminate utilizzando un `customer_id` se è stato specificato il `customer_id` quando le informazioni sono state originariamente aggiunte utilizzando il metodo associato:

- query (`/v1/environments/{environment_id}/collections/{collection_id}/query`) solo quando utilizzate con i parametri `passages` o `natural_language_query`
- eventi (`/v1/events`)
- documenti (`/v1/environments/{environment_id}/collections/{collection_id}/documents`)
- avvisi (`/v1/environments/{environment_id}/collections/{collection_id}/notices`) vengono etichettati solo gli inserimenti di avvisi (`notices`).
- entità Knowledge Graph (`/v1/environments/{environment_id}/collections/{collection_id}/query_entities`)
- relazioni Knowledge Graph (`/v1/environments/{environment_id}/collections/{collection_id}/query_relations`)
- dati di formazione (`/v1/environments/{environment_id}/collections/{collection_id}/training_data`)

Le seguenti informazioni archiviate non vengono etichettate esplicitamente e non possono essere eliminate specificando il `customer_id`. I dati personali non sono supportati in questi campi.

Tutti i campi stringa (inclusi ma non limitati a `name` e `description`) dei seguenti elementi archiviati:
- configurazioni
- raccolte
- ambienti

## Etichettatura dei dati
{: #labeling}

Quando vengono inseriti i documenti, includi l'intestazione `X-Watson-Metadata` utilizzando le operazioni `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` o `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/ID`. Il campo `customer_id` viene aggiunto ai metadati estratti (`extracted_metadata`) dei documenti. La tua applicazione dovrebbe essere configurata per fornire un `customer_id` nell'intestazione `X-Watson-Metadata` durante l'esecuzione di tutte le operazioni.

Facoltativamente, puoi includere il campo `customer_id` con la parte del modulo a più parti `metadata` invece di utilizzare l'intestazione `X-Watson-Metadata`.

**Nota:** se i tuoi documenti sono già stati inseriti, dovrai reinserirli per aggiungere l'intestazione `X-Watson-Metadata` e il `customer_id`.

**Nota:** se si specifica un `customer_id` nella parte del modulo a più parti `metadata` E l'intestazione `X-Watson-Metadata` per lo stesso documento, sarà utilizzato il `customer_id` nell'intestazione `X-Watson-Metadata`.

Limitazioni:

- Il valore dell'intestazione `X-Watson-Metadata` non può superare i 4 kilobyte di testo.
- L'intestazione `X-Watson-Metadata` deve contenere un elenco separato da punti e virgola di coppie `field=valore`. `field` e `value` non devono contenere punti e virgola (`;`) o segni uguale (`=`).
- I `customer_id` sono univoci all'interno di ogni istanza di {{site.data.keyword.discoveryshort}}. NON sono univoci per l'ambiente o la raccolta.
- Un `customer_id` non può superare i 256 caratteri in lunghezza.
- Se un `customer_id` contiene solo spazi vuoti o è completamente vuoto, si tratterà questo caso come se il `customer_id` non fosse stato fornito affatto e non verrà restituito alcun messaggio di errore.

### Etichettatura dei dati con la strumentazione Discovery
{: #labelingtooling}

I dati possono essere etichettati con il campo `customer_id` quando si utilizza la strumentazione {{site.data.keyword.discoveryshort}}. Fai clic su ![Environment details](images/env_icon.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> e immetti il `customer_id` nel campo **GDPR Data Label**. Una volta che questo campo è stato impostato per tutti i dati caricati utilizzando questo browser, la sessione sarà etichettata con il `customer_id` specificato, questo campo deve essere modificato manualmente se viene modificato l'ID cliente associato.

Aggiungendo un `customer_id` al campo **GDPR Data Label** si etichetteranno i documenti, gli avvisi, le entità Knowledge Graph, le relazioni Knowledge Graph e i dati di formazione all'interno di tale dominio URL da quel punto in avanti, inclusa ogni istanza in tale dominio. Tutte le azioni (inclusi i caricamenti dei documenti) che si sono verificate nella strumentazione {{site.data.keyword.discoveryshort}} prima dell'aggiunta del campo **GDPR Data Label** non verranno etichettate.

**Nota:** se cambi i domini, i browser, svuoti la cache del browser o avvii una sessione in incognito dopo aver specificato il tuo `customer_id` utilizzando il campo **GDPR Data Label** della strumentazione {{site.data.keyword.discoveryshort}}, il `customer_id` non verrà conservato e i tuoi dati non saranno etichettati. Se devi cambiare dominio o browser, reinserisci il `customer_id` nel campo **GDPR Data Label**.

### Etichettatura dei documenti utilizzando il data crawler
{: #labelingdc}

Se il Data Crawler ha già eseguito la ricerca per l'indicizzazione di qualche documento, dovrai rieseguirne la ricerca per l'indicizzazione per aggiungere l'intestazione `X-Watson-Metadata` e il `customer_id`.

1. Aggiorna la tua configurazione dell'adattatore di output del Data Crawler {{site.data.keyword.discoveryshort}} per includere il `customer_id `. Consulta [Configurazione dell'adattatore di output](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#output-adapter).
1. Pianifica una ricerca per l'indicizzazione. I documenti vengono inoltrati a {{site.data.keyword.discoveryshort}} utilizzando l'intestazione `X-Watson-Metadata` e verranno etichettati con il `customer_id` configurato.

## Eliminazione dei dati etichettati
{: #deletingdata}

I dati devono essere etichettati con un `customer_id` per poterli eliminare successivamente.

1. Utilizza l'operazione `DELETE /v1/user_data` e fornisci il `customer_id` dei dati che vuoi eliminare. `DELETE /v1/user_data` elimina tutti i dati associati a un particolare `customer_id` all'interno di tale istanza del servizio, come specificato in [Metodi che supportano l'etichettatura dei dati](/docs/services/discovery?topic=discovery-information-security#pi_methods). Consulta anche il [Riferimento API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/discovery#delete-labeled-data){: new_window}

Le eliminazioni vengono eseguite in modo asincrono. Non puoi tenere traccia dello stato di avanzamento delle eliminazioni.

Per garantire che tutto il contenuto etichettato venga rimosso correttamente, non eseguire `user_delete` finché i conteggi `processing` e `pending` per tutte le raccolte nel tuo ambiente non restituiscono `0`.

Se viene fornito un `customer_id` non esistente, non verrà eliminato alcunché, ma sarà restituita una risposta `200 - OK`.

Gli ambienti e le raccolte non vengono etichettati con un `customer_id`, anche se viene inclusa un'intestazione `X-Watson-Metadata` nella richiesta di creazione dell'ambiente o della raccolta. Vengono etichettati solo i singoli documenti all'interno di una raccolta all'interno di un ambiente. Pertanto, quando i dati vengono eliminati, le raccolte e gli ambienti individuali NON vengono eliminati.

Non puoi eliminare i dati etichettati utilizzando la strumentazione {{site.data.keyword.discoveryshort}}.
