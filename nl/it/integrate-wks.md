---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-08"

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

# Integrazione con Watson Knowledge Studio

Puoi integrare un modello personalizzato da {{site.data.keyword.knowledgestudiofull}} con il servizio {{site.data.keyword.discoveryshort}} per fornire arricchimenti di entità e relazioni.
{: shortdesc}

Questo ti fornisce la flessibilità di applicare alle funzionalità di miglioramento del documento del servizio {{site.data.keyword.discoveryshort}}, informazioni specifiche di aree di particolare attenzione, come le discipline scientifiche e industriali. Puoi utilizzare i dati pubblici e i dati di tua proprietà nel tuo modello di arricchimento.

Puoi utilizzare l'API del servizio o la strumentazione {{site.data.keyword.discoveryshort}} per integrare un modello {{site.data.keyword.knowledgestudioshort}} con il servizio {{site.data.keyword.discoveryshort}}.

## Prima di iniziare

Prima di poter integrare un modello personalizzato da {{site.data.keyword.knowledgestudioshort}} con il servizio {{site.data.keyword.discoveryshort}}, devi creare e distribuire il modello utilizzando {{site.data.keyword.knowledgestudioshort}}. Consulta la [Documentazione di {{site.data.keyword.knowledgestudioshort}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.bluemix.net/docs/services/knowledge-studio/tutorials-create-project.html#wks_tutintro){: new_window} per informazioni sulla creazione e la distribuzione dei modelli. Hai bisogno dell'ID univoco del modello distribuito per integrarlo con il servizio {{site.data.keyword.discoveryshort}}.

## Integrazione del tuo modello personalizzato con l'API

1.  Ottieni l'ID del tuo ambiente {{site.data.keyword.discoveryshort}} come descritto nell'[Elenco degli ambienti ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_environments){: new_window}. Prendi nota dell'ID ambiente.
1.  Elenca gli ID delle tue configurazioni {{site.data.keyword.discoveryshort}} correnti come descritto nell'[Elenco delle configurazioni ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_configurations){: new_window}. Prendi nota dell'ID della configurazione che vuoi integrare con il tuo modello personalizzato {{site.data.keyword.knowledgestudiofull}}.
1.  Scarica una copia della tua configurazione {{site.data.keyword.discoveryshort}} corrente immettendo i seguenti comandi in una shell bash o in qualcosa di equivalente come Cygwin per Windows. Sostituisci `{environment_id}` e `{configuration_id}` con gli ID di cui hai preso nota nei due passi precedenti.

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-11-07" > my_config.json
    ```
    {: pre}

    Questo comando elenca i contenuti del tuo file della raccolta e li inserisce in un file JSON denominato `my_config.json`.
1.  Apri il file `my_config.json` in un editor di testo e apporta le seguenti modifiche:
    1.  Modifica il valore del campo `"name"` con qualcosa che indica lo scopo della nuova configurazione. Puoi facoltativamente modificare anche il valore del campo `"description"`.

        ```json
        ...
        "name": "wks-config",
        "description": "This is a configuration to use with a WKS model",
        ...
        ```
        {: codeblock}

    1.  Aggiorna i campi di arricchimento con le informazioni del modello {{site.data.keyword.knowledgestudioshort}}. Presupponendo che i campi di arricchimento in origine leggono:

        ```json
        "enrichments": [
  {
            "source_field": "text",
            "destination_field": "enriched_text",
            "enrichment": "natural_language_understanding",
            "options": {
                "features": {
                    "entities": {
                        "sentiment": true,
          "emotion": false,
          "limit": 50
                    },
        "sentiment": {
                        "document": true
                    },
                    "categories": {},
                    "concepts": {
                        "limit": 8
                    },
                    "relations": {}
                }
            }
        }]
        ```
        {: codeblock}

    1.  Aggiorna il file nel seguente modo, sostituendo l'ID univoco del modello {{site.data.keyword.knowledgestudioshort}} descritto in "Prima di iniziare" per `{watson_knowledge_studio_model_ID}`.

        ```json
        "enrichments": [
  {
            "source_field": "text",
            "destination_field": "enriched_text",
            "enrichment": "natural_language_understanding",
            "options": {
                "features": {
                    "entities": {
                        "sentiment": true,
                        "emotion": false,
                        "limit": 50,
                        "model": "{watson_knowledge_studio_model_ID}"
                    },
        "sentiment": {
                        "document": true
                    },
                    "categories": {},
                    "concepts": {
                        "limit": 8
                    },
        "relations": {
                      "model": "{watson_knowledge_studio_model_ID}"
                    }
                }
            }
        }]
        ```
        {: codeblock}

1.  Salva il file `my_config.json`.
1.  Utilizza un validatore JSON, come ad esempio [JSLint ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://jslint.com){: new_window} per la convalida e, se necessario, correggi il tuo JSON modificato prima di eseguire i prossimi passi.
1.  Aggiorna la configurazione nel seguente modo. Hai di nuovo bisogno degli ID `{environment_id}` e `{configuration_id}` raccolti all'inizio di questa procedura.

    ```bash
    curl -X PUT -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d @my_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-11-07"
    ```
    {: pre}

    **Nota:** se stai creando una nuova configurazione o modificando la configurazione predefinita, dovrai creare una nuova configurazione invece di aggiornarne una esistente. Prima di creare una nuova configurazione, assicurati che il campo `"configuration_id":` venga rimosso dal tuo file `my_config.json` e quindi immetti il seguente comando:

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d @my_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07"
    ```
    {: pre}

    Entrambi i comandi restituiscono il contenuto del file di configurazione aggiornato.

## Integrazione del tuo modello personalizzato con la strumentazione Discovery

Puoi integrare un modello personalizzato da {{site.data.keyword.knowledgestudioshort}} negli arricchimenti [Entity Extraction](/docs/services/discovery/building.html#entity-extraction) o [Relation Extraction](/docs/services/discovery/building.html#relation-extraction) con la strumentazione {{site.data.keyword.discoveryshort}}.

1. Ottieni il `Model ID` del tuo modello {{site.data.keyword.knowledgestudioshort}}.
1. Nella strumentazione {{site.data.keyword.discoveryshort}}, fai clic sull'icona **Manage Data** in alto a sinistra per aprire la schermata **Manage data**, quindi crea o apri una raccolta. **Nota:** se scegli una raccolta esistente, dovrebbe essere vuota. In caso contrario, devi reinserire i documenti dopo aver creato il tuo nuovo file di configurazione.
1. Nella sezione **Configuration** della schermata **Manage Data** della tua raccolta, fai clic su **Switch** e quindi su **Create a New Configuration**. Fornisci un nome alla configurazione. 
1. Fai clic su **Add enrichments** e seleziona gli arricchimenti **Entity Extraction** o **Relation Extraction**.
1. Immetti il `Model ID` nella casella `Custom Model ID` dell'arricchimento selezionato. Il modello {{site.data.keyword.knowledgestudiofull}} personalizzato sovrascriverà il valore predefinito di tale arricchimento. 
1. Fai clic su **Apply** e quindi su **Done**.

Quando i documenti vengono caricati in una raccolta dati, vengono convertiti e arricchiti utilizzando il file di configurazione scelto per tale raccolta. Se cambi una raccolta esistente con un nuovo file di configurazione dopo che i documenti sono stati caricati, quei documenti caricati resteranno convertiti dal file di configurazione originale. Tutti i documenti caricati dopo il passaggio al file di configurazione utilizzeranno il nuovo file di configurazione. Se vuoi che la raccolta **completa** utilizzi la nuova configurazione, dovrai creare una nuova raccolta, scegliere il nuovo file di configurazione e ricaricare tutti i documenti.

**Nota:** può essere assegnato solo un modello {{site.data.keyword.knowledgestudiofull}} a un arricchimento.

## Passi successivi

Utilizza il servizio {{site.data.keyword.discoveryshort}} con la tua nuova configurazione per inserire i dati privati. I documenti che inserisci con la configurazione aggiornata vengono automaticamente arricchiti con i dati dal tuo modello personalizzato.
