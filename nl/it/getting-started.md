---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:curl: #curl .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}

# Introduzione all'API
{: #gs-api}

In questa breve esercitazione, introdurremo l'API {{site.data.keyword.discoveryshort}} e illustreremo il processo di creazione di una raccolta dati privata e la sua ricerca.
{: shortdesc}

Se preferisci utilizzare la strumentazione {{site.data.keyword.discoveryshort}}, consulta l'[Introduzione](/docs/services/discovery/getting-started-tool.html).
{: tip}

## Prima di iniziare
{: #before-you-begin}

- Crea un'istanza del servizio: 
    1.  Vai alla [pagina {{site.data.keyword.discoveryshort}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.{DomainName}/catalog/services/discovery){: new_window} nel catalogo {{site.data.keyword.Bluemix_notm}}.
    1.  Registrati per un account {{site.data.keyword.Bluemix_notm}} gratuito o accedi.
    1.  Fai clic su **Create**.
- Copia le credenziali per autenticare la tua istanza del servizio:
    1. Dal [dashboard {{site.data.keyword.Bluemix_notm}}](https://console.{DomainName}/dashboard/apps), fai clic sulla tua istanza del servizio {{site.data.keyword.discoveryshort}} per andare alla pagina del dashboard del servizio {{site.data.keyword.discoveryshort}}.
    1.  Nella pagina **Gestisci**, fai clic su **Mostra** per visualizzare le tue credenziali.
    1.  Copia i valori `apikey` e `url`.

    In alcune istanze, esegui l'autenticazione fornendo l'autenticazione di base. Se vedi `username` e `password` nelle credenziali, utilizza questi valori invece di `"apikey":"{apikey_value}"` negli esempi in questa esercitazione.
{: tip}

## Passo 1: Crea un ambiente
{: #create-an-environment}

In una shell bash o in un ambiente equivalente come Cygwin con l'applicazione `curl` installata, utilizza il metodo `POST /v1/Ambienti` per creare un ambiente. Pensa a un ambiente come al magazzino in cui stai archiviando tutte le tue scatole di documenti. 

Questa esercitazione utilizza una chiave API per l'autenticazione. Per gli utilizzi di produzione, assicurati di riesaminare le [procedure ottimali](/docs/services/watson/apikey-bp.html#api-bp) della chiave API.
{: tip}

1.  Immetti il seguente comando per creare un ambiente denominato `my-first-environment`. Sostituisci `{apikey_value}` con la chiave API che hai copiato in precedenza:

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    L'API restituisce informazioni come l'ID ambiente, lo stato dell'ambiente e la quantità di memoria che il tuo ambiente sta utilizzando. 

1.  Controlla lo stato dell'ambiente periodicamente fino a quando non vedi uno stato di `active`.
    - Immetti una chiamata al metodo `GET /v1/environments/{environment_id}` per richiamare lo stato del tuo ambiente. Sostituisci `{apikey_value}` e `{environment_id}` con le tue informazioni:

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}?version=2017-11-07"
    ```
    {: pre}

    Lo stato deve essere `active` prima di poter creare una raccolta.

## Passo 2: Crea una raccolta
{: #create-a-collection}

Ora che l'ambiente è pronto, puoi creare una raccolta. Pensa a una raccolta come a una scatola in cui archivierai i tuoi documenti nel tuo ambiente. 

1.  Hai bisogno dell'ID della tua prima configurazione predefinita. Per trovare il tuo valore predefinito per `configuration_id`, utilizza il metodo `GET /v1/environments/{environment_id}/configurations`. Sostituisci `{apikey_value}` e `{environment_id}` con le tue informazioni:

    ```bash
      curl -u "apikey":"{apikey_value}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07
    ```
    {: pre}
1.  Utilizza il metodo `POST /v1/environments/{environment_id}/collections` per creare una raccolta denominata **my-first-collection**. Sostituisci `{apikey_value}`, `{environment_id}` e `{configuration_id}` con le tue informazioni:

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d '{"name": "my-first-collection", "description": "exploring collections", "configuration_id":"{configuration_id}" , "language": "en_us"}' https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07
    ```
    {: pre}

    L'API restituisce informazioni come l'ID raccolta, lo stato della raccolta e la quantità di memoria che la tua raccolta sta utilizzando.
1.  Controlla lo stato della raccolta periodicamente fino a quando non vedi uno stato di `active`.
    - Immetti una chiamata al metodo `GET /v1/environments/{environment_id}/collections/{collection_id}` per richiamare lo stato della tua raccolta. Nuovamente, sostituisci `{apikey_value}`, `{environment_id}` e `{configuration_id}` con le tue informazioni:

    ```bash
    curl -u "apikey":"{apikey_value}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07
    ```
    {: pre}

## Passo 3: Scarica i documenti di esempio
{: #download-sample-documents}

Scarica questi documenti di esempio: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="Icona link esterno" title="Icona link esterno" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="Icona link esterno" title="Icona link esterno" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="Icona link esterno" title="Icona link esterno" class="style-scope doc-content"></a> e <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="Icona link esterno" title="Icona link esterno" class="style-scope doc-content"></a>.

**Nota:** in alcuni browser, i link precedenti si apriranno in una nuova finestra invece di essere salvati localmente. Se questo si verifica, seleziona `Salva con nome` nel menu `File` del tuo browser per salvare una copia del file.

## Passo 4: Carica i documenti
{: #upload-the-documents}

1.  Adesso, aggiungi i documenti di esempio alla tua raccolta. Questo esempio carica il documento **test-doc1.html** nella tua raccolta. Sostituisci `{apikey_value}`, `{environment_id}` e `{configuration_id}` con le tue informazioni. Modifica l'ubicazione del documento di esempio per puntare alla cartella in cui hai salvato il file `test-doc1.html`.
    - Utilizza il metodo `POST /v1/environments/{environment_id}/collections/{collection_id}/documents`:

        ```bash
        curl -X POST -u "apikey":"{apikey_value}" -F "file=@test-doc1.html" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2017-11-07
        ```
        {: pre}

    In alternativa, utilizza uno degli SDK elencati nel [Riferimento API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}:
    - Java:

      ```java
      Discovery discovery = new Discovery("2017-11-07");
      discovery.setEndPoint("https://gateway.watsonplatform.net/discovery/api/v1");
      IamOptions options = new IamOptions.Builder()
        .apiKey("{apikey_value}")
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
        version='2017-11-07',
        api_key='{apikey_value}'
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
        version_date: '2017-11-07',
        iam_apikey: '{apikey_value}',
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

Il seguente esempio restituisce tutte le entità denominate **IBM**. Sostituisci `{apikey_value}`, `{environment_id}` e `{configuration_id}` con le tue informazioni:

```bash
curl -u "apikey":"{apikey_value}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

## Passi successivi
{: #next-steps}

Hai eseguito correttamente la query dei documenti nell'ambiente e nella raccolta che hai creato. Puoi ora iniziare a personalizzare la tua raccolta aggiungendo più documenti e arricchimenti e a personalizzare le impostazioni di conversione.

- Troverai ulteriori informazioni sull'API nel [Riferimento API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}
- [Configura](/docs/services/discovery/building.html) il tuo servizio
- Informazioni sull'[autenticazione con IAM](/docs/services/watson/getting-started-iam.html)
