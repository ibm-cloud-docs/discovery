---
copyright:
  years: 2015, 2018
lastupdated: "2018-12-19"

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

# Introduzione all'API
{: #gs-api}

In questa breve esercitazione, introdurremo l'API {{site.data.keyword.discoveryshort}} e illustreremo il processo di creazione di una raccolta dati privata e la sua ricerca.
{: shortdesc}

Se preferisci utilizzare la strumentazione {{site.data.keyword.discoveryshort}}, consulta l'[Introduzione](/docs/services/discovery?topic=discovery-getting-started#getting-started).
{: tip}

## Prima di iniziare
{: #before-you-begin-api}

- Crea un'istanza del servizio:
    1.  Vai alla pagina [{{site.data.keyword.discoveryshort}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/catalog/services/discovery) nel catalogo {{site.data.keyword.cloud_notm}}.
        L'istanza del servizio viene creata nel gruppo di risorse predefinito (**default**) se non ne scegli uno diverso e *non può* essere modificato in seguito. Questo gruppo è sufficiente per provare il servizio. Se stai creando un'istanza per un utilizzo più impegnativo, scopri di più sui [gruppi di risorse
![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/docs/resources/bestpractice_rgs.html#bp_resourcegroups){: new_window}.
    1.  Registrati per un account {{site.data.keyword.cloud_notm}} gratuito o accedi.
    1.  Fai clic su **Crea**. Dopo che hai creato un'istanza del servizio {{site.data.keyword.discoveryshort}}, vieni portato al tuo elenco di servizi.
- Copia le credenziali per autenticare la tua istanza del servizio:
    1.  Dall'[elenco risorse](https://{DomainName}/dashboard/), fai clic sulla tua istanza del servizio {{site.data.keyword.discoveryshort}} per andare alla pagina del dashboard del servizio {{site.data.keyword.discoveryshort}}.
    1.  Nella pagina **Gestisci**, fai clic su **Visualizza credenziali** per visualizzare le tue credenziali.
    1.  Copia i valori di `Chiave API` e `URL`.

        In alcune istanze, esegui l'autenticazione fornendo l'autenticazione di base. Se vedi `username` e `password` nelle credenziali, utilizza questi valori invece di `"apikey:{apikey}"` negli esempi in questa esercitazione.
        {: tip}

## Passo 1: Crea un ambiente
{: #create-an-environment}

In una shell bash o in un ambiente equivalente, come Cygwin con l'applicazione `curl` installata, utilizza il metodo `POST /v1/environments` per creare un ambiente. Pensa a un ambiente come al magazzino in cui stai archiviando tutte le tue scatole di documenti.

Questa esercitazione utilizza una chiave API per l'autenticazione. Per gli utilizzi di produzione, assicurati di riesaminare le [procedure ottimali](/docs/services/watson/apikey-bp.html#api-bp) della chiave API.
{: important}

1.  Immetti il seguente comando per creare un ambiente denominato `my-first-environment`. Sostituisci `{apikey}` e `{url}` con la chiave API e l'URL che hai copiato in precedenza:

    ```bash
    curl -X POST -u "apikey:{apikey}" -H "Content-Type: application/json" -d "{\"name\":\"my-first-environment\", \"description\":\"exploring environments\"}" "{url}/v1/environments?version=2018-12-03"
    ```
    {: pre}

    L'API restituisce informazioni come l'ID ambiente, lo stato dell'ambiente e la quantità di memoria che il tuo ambiente sta utilizzando.

1.  Controlla lo stato dell'ambiente periodicamente fino a quando non vedi uno stato di `active`.

    Immetti una chiamata al metodo `GET /v1/environments/{environment_id}` per richiamare lo stato del tuo ambiente. Sostituisci `{apikey}`, `{url}` e `{environment_id}` con le tue informazioni:

    ```bash
    curl -u "apikey:{apikey}" "{url}/v1/environments/{environment_id}?version=2018-12-03"
    ```
    {: pre}

    Lo stato deve essere `active` prima di poter creare una raccolta.

## Passo 2: Crea una raccolta
{: #create-a-collection-api}

Ora che l'ambiente è pronto, puoi creare una raccolta. Pensa a una raccolta come a una scatola in cui archivierai i tuoi documenti nel tuo ambiente.

1.  Hai bisogno dell'ID della tua prima configurazione predefinita. Per trovare il tuo valore predefinito per `configuration_id`, utilizza il metodo `GET /v1/environments/{environment_id}/configurations`. Sostituisci `{apikey}`, `{url}` e `{environment_id}` con le tue informazioni:
    ```bash
      curl -u "apikey:{apikey}" "{url}/v1/environments/{environment_id}/configurations?version=2018-12-03"
    ```
    {: pre}
1.  Utilizza il metodo `POST /v1/environments/{environment_id}/collections` per creare una raccolta denominata **my-first-collection**. Sostituisci `{apikey}`, `{url}`, `{environment_id}` e `{configuration_id}` con le tue informazioni:
    ```bash
    curl -X POST -u "apikey:{apikey}" -H "Content-Type: application/json" -d "{\"name\": \"my-first-collection\", \"description\": \"exploring collections\", \"configuration_id\":\"{configuration_id}\" , \"language": \"en_us\"}" "{url}/v1/environments/{environment_id}/collections?version=2018-12-03"
    ```
    {: pre}
    L'API restituisce informazioni come l'ID raccolta, lo stato della raccolta e la quantità di memoria che la tua raccolta sta utilizzando.
1.  Controlla lo stato della raccolta periodicamente fino a quando non vedi uno stato di `active`.

    Immetti una chiamata al metodo `GET /v1/environments/{environment_id}/collections/{collection_id}` per richiamare lo stato della tua raccolta.  Di nuovo, sostituisci `{apikey}`, `{url}`, `{environment_id}` e `{configuration_id}` con le tue informazioni:

    ```bash
    curl -u "apikey:{apikey}" "{url}/v1/environments/{environment_id}/collections/{collection_id}?version=2018-12-03"
    ```
    {: pre}

## Passo 3: Scarica i documenti di esempio
{: #download-sample-documents}

Scarica questi documenti di esempio: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="Icona link esterno" title="Icona link esterno"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="Icona link esterno" title="Icona link esterno"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="Icona link esterno" title="Icona link esterno"></a> e <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="Icona link esterno" title="Icona link esterno"></a>.

In alcuni browser, i precedenti link si apriranno in una nuova finestra invece di essere salvati localmente.Se questo si verifica, seleziona `Salva con nome` nel menu `File` del tuo browser per salvare una copia del file.
{: tip}

## Passo 4: Carica i documenti
{: #upload-the-documents}

1.  Adesso, aggiungi i documenti di esempio alla tua raccolta. Questo esempio carica il documento **test-doc1.html** nella tua raccolta. Sostituisci `{apikey}`, `{url}`, `{environment_id}` e `{collection_id}` con le tue informazioni. Modifica l'ubicazione del documento di esempio per puntare alla cartella in cui hai salvato il file `test-doc1.html`.
    - Utilizza il metodo `POST /v1/environments/{environment_id}/collections/{collection_id}/documents`:

        ```bash
        curl -X POST -u "apikey:{apikey}" -F "file=@test-doc1.html" "{url}/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2018-12-03"
        ```
        {: pre}

        In alternativa, utilizza uno degli SDK elencati nel [Riferimento API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/discovery){: new_window}:
    - Java:
      ```java
      Discovery discovery = new Discovery("2018-12-03");
      discovery.setEndPoint("{url}");

      IamOptions options = new IamOptions.Builder()
        .apiKey("{apikey}")
        .build();
      discovery.setIamCredentials(options);

      String environmentId = "{environment_id}";
      String collectionId = "{collection_id}";
      String documentJson = "{\"field\":\"value\"}";
      InputStream documentStream = new ByteArrayInputStream(documentJson.getBytes());

      CreateDocumentRequest.Builder builder = new CreateDocumentRequest.Builder(environmentId, collectionId);
      builder.inputStream(documentStream, HttpMediaType.APPLICATION_JSON);
      CreateDocumentResponse createResponse = discovery.createDocument(builder.build()).execute();
      ```
      {: codeblock}
    - Python:
      ```python
      import sys
      import os
      import json
      from watson_developer_cloud import DiscoveryV1

      discovery = DiscoveryV1(
          version='2018-12-03',
          iam_apikey='{apikey}',
          url='{url}'
      )
      with open((os.path.join(os.getcwd(), '{path_element}', '{filename}' as fileinfo:
        add_doc = discovery.add_document('{environment_id}', '{collection_id}', file_info=fileinfo)
      print(json.dumps(add_doc, indent=2))
      ```
      {: codeblock}

    - Node.js:
      ```javascript
      var DiscoveryV1 = require('watson-developer-cloud/discovery/v1');
      var fs = require('fs');

      var discovery = new DiscoveryV1({
        version_date: '2018-12-03',
        iam_apikey: '{apikey}',
        url: '{url}'
      });

      var file = fs.readFileSync('{/path/to/file}');

      discovery.addDocument({ environment_id: '{environment_id}', collection_id: '{collection_id}', file: file },
      function(error, data) {
        console.log(JSON.stringify(data, null, 2));
        }
      );
      ```
      {: codeblock}

1.  Ripeti questo processo per ognuno degli altri 3 file di esempio.

## Passo 5: Esegui la query della tua raccolta
{: #query-your-collection}

Infine, utilizza il metodo `GET /v1/environments/{environment_id}/collections/{collection_id}/query` per cercare la tua raccolta di documenti.

Il seguente esempio restituisce tutte le entità denominate **IBM**. Sostituisci `{apikey}`, `{environment_id}` e `{collection_id}` con le tue informazioni:

```bash
curl -u "apikey:{apikey}" "{url}/v1/environments/{environment_id}/collections/{collection_id}/query?version=2018-12-03&query=enriched_text.entities.text:IBM"
```
{: pre}

## Passi successivi
{: #next-steps-api}

Hai eseguito correttamente la query dei documenti nell'ambiente e nella raccolta che hai creato. Puoi ora iniziare a personalizzare la tua raccolta aggiungendo più documenti e arricchimenti e a personalizzare le impostazioni di conversione.

- Troverai ulteriori informazioni sull'API nel [Riferimento API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/discovery){: new_window}
- [Configura](/docs/services/discovery?topic=discovery-configservice#configservice) il tuo servizio
- Ulteriori informazioni sull'[autenticazione presso IAM ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/docs/services/watson/getting-started-iam.html#iam){: new_window}
