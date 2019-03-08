---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-06"

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

# Ergebnisrelevanz mithilfe der API verbessern
{: #improving-result-relevance-with-the-api}

Sie können den {{site.data.keyword.discoveryshort}}-Service trainieren, um die Relevanz von Abfrageergebnissen für Ihre jeweilige Organisation oder einen bestmmten Themenbereich zu verbessern. Wenn Sie eine {{site.data.keyword.discoveryshort}}-Instanz mit *Trainingsdaten* versorgen, verwendet der Service Watson-Verfahren für das maschinelle Lernen, um Signale im Inhalt und in Fragestellungen zu suchen. Anschließend ordnet der Service die Abfrageergebnisse neu an und zeigt die relevantesten Ergebnisse an erster Stelle an. Je mehr Trainingsdaten Sie hinzufügen, desto genauer und ausgereifter wird die Serviceinstanz bei der Sortierung der zurückgegebenen Ergebnisse.
{: shortdesc}

Das Relevanztraining ist optional. Falls die Ergebnisse Ihrer Abfragen Ihren Anfoderungen entsprechen, ist kein weiteres Training erforderlich. Eine Übersicht über den Aufbau von Anwendungsfällen für das Training enthält der Blogbeitrag [How to get the most out of Relevancy Training ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/dwblog/2017/get-relevancy-training/){: new_window}.

Umfassende Informationen zu den Trainings-APIs enthält die [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}.

Falls Sie lieber die {{site.data.keyword.discoveryshort}}-Tools für das Training von {{site.data.keyword.discoveryshort}} verwenden möchten, finden Sie im Abschnitt [Relevanz der Ergebnisse mithilfe der Tools verbessern](/docs/services/discovery/train-tooling.html) weiterführende Informationen.

**Hinweis:** Das Relevanztraining ist gegenwärtig nur auf Abfragen in natürlicher Sprache für private Sammlungen anwendbar. Es ist nicht für die Verwendung bei strukturierten Abfragen in der {{site.data.keyword.discoveryshort}}-Abfragesprache gedacht.  Weitere Informationen zur {{site.data.keyword.discoveryshort}}-Abfragesprache finden Sie unter [Abfragekonzepte](/docs/services/discovery/using.html).

Sammlungen, für die ein Training durchgeführt wurde, geben im Ergebnis für eine Abfrage in natürlicher Sprache eine Konfidenzbewertung (Feld `confidence`) zurück. Details enthält der Abschnitt [Konfidenzbewertung](/docs/services/discovery/train-tooling.html#confidence).

Unter [Anforderungen an Trainingsdaten](/docs/services/discovery/train.html#reqs) finden Sie die Mindestanforderungen für das Training sowie die Trainingsbegrenzungen.

Unter [Nutzungsüberwachung](/docs/services/discovery/feedback.html) finden Sie Details zur Nutzungsüberwachung und zur Verwendung der Daten, um Ihre Anwendungen besser verstehen und verbessern zu können.

<!-- A trained Discovery service instance is intended primarily for use with natural language queries, but it works equally well with queries that use structured syntax. -->  <!-- See [Query Concepts](/docs/services/discovery/using.html) and the [Query reference](/docs/services/discovery/query-reference.html) for information about structured queries and natural language queries. -->

Zum Trainieren einer Discovery-Instanz werden die folgenden Komponenten benötigt:

 - **Trainingsdaten**: Dies ist die Gruppe der *Abfragen* und *Beispiele*, die der Service zur Präzisierung der Abfrageergebnisse verwendet.
 - **Abfrage**: Eine Abfrage in natürlicher Sprache, die auf den Trainingsdatenbestand angewendet wird.
   Jeder Abfrage sind eines oder mehrere *Beispiele* zugeordnet (siehe nächster Listenpunkt).
   Jede Abfrage muss innerhalb des Trainingsdatenbestands eindeutig sein.
 - **Beispiel**: Dies ist ein in einer Discovery-Sammlung indexiertes Dokument, das als Referenz (**gut oder schlecht**) für die zugehörige Abfrage dient. Wenn Sie ein Beispiel zu einer Trainingsdatenabfrage hinzufügen, beziehen Sie eine Relevanzkennzeichnung ein, die die Relevanz (oder 'Güte' bzw. 'Unbrauchbarkeit') des Dokuments für die angegebene Abfrage angibt.

   Beispiele werden durch die ID des indexierten Dokuments angegeben. Jedes Beispiel muss eine Kennzeichnung einschließen, der die 'Güte' oder 'Unbrauchbarkeit' des Dokuments für die Abfrage angibt.

   Beispiele können optional eine Querverweisabfrage angeben. Die Querverweisabfrage muss nur das Beispieldokument zurückgeben und von der eindeutigen Dokument-ID in Watson Discovery unabhängig sein. Querverweisabfragen werden gegenwärtig nicht automatisch verwendet, können jedoch eingesetzt werden, um Trainingsdaten zu reparieren, falls während eines Einpflegeereignisses neue IDs zu Dokumenten zugeordnet werden.

## Anforderungen an Trainingsdaten
{: #reqs}

Trainingsdaten müssen die folgenden **Mindestqualitätskriterien** erfüllen, damit die Relevanz der vom Discovery-Service zurückgegebenen Antworten wirksam verbessert werden kann. Bitte beachten Sie, dass **Mindestkriterien** nicht gleichbedeutend mit **optimalen Kriterien** ist. Der Service überprüft die Trainingsdaten in regelmäßigen Abständen, um festzustellen, ob diese Anforderungen erfüllt sind, und aktualisiert sich aufgrund von Änderungen automatisch selbst.

- Die Trainingsdaten der Sammlung müssen mindestens 49 eindeutige Trainingsabfragen (also Gruppen aus Abfragen und Beispielen) enthalten. Abhängig von der Größe und der Komplexität Ihrer Sammlung muss Ihr Bestand möglicherweise mehr als 49 Trainingsabfragen enthalten, damit Watson in der Lage ist, das Relevanztraining auf die Sammlung anzuwenden. Watson gibt Ihnen eine Rückmeldung, falls weitere Abfragen für das Training benötigt werden.
- Beim Zuordnungen von Relevanzquoten über die API: Die Relevanzquote für jede Trainingsabfrage muss eine nicht negative ganze Zahl sein, z. B. `0` für *nicht relevant*, `1` für *etwas relevant* und `2` für *sehr relevant*. Um erfahrenen Benutzern beim Experimentieren mit unterschiedlichen Einstufungsschemas eine maximale Flexibilität zu bieten, akzeptiert der Service jedoch nicht negative ganze Zahlen zwischen `0` und `100`. Die größte ganze Zahl in der Gruppe der Trainingsfragen gibt jedoch immer die maximale Relevanz an, unabhängig davon, welchen Bereich Sie verwenden.
- Beim Zuordnen von Relevanzeinstufungen über die Tools: Die {{site.data.keyword.discoveryshort}}-Tools verwenden die Relevanzquoten `0` für *nicht relevant* und `10` für *relevant*. Sie sollten beide verfügbaren Einstufungen in Ihren Ergebnissen anwenden, also `Relevant` (= relevant) und `Not relevant` (= nicht relevant). Wenn Sie die Einstufung nur für `relevante` Dokumente vornehmen, erhalten Sie nicht die benötigten Daten.  Falls Sie Ihre Dokumente sowohl mit den {{site.data.keyword.discoveryshort}}-Tools als auch der API einstufen oder zunächst die API verwenden und später auf die Tools umsteigen wollen, verwenden Sie die Relevanzquoten `0` und `10`.
- Die Trainingsabfragen müssen einige Begriffsüberschneidungen zwischen der Abfrage und der gewünschten Antwort einbeziehen, damit diese bei der erstmaligen Suche durch den Discovery-Service abgerufen werden kann, die sich über einen großen Bereich erstreckt.

**Hinweis:** Watson verwendet Trainingsdaten, um Muster zu erlernen und Verallgemeinerungen vorzunehmen, und nicht, um einzelne Trainingsabfragen auswendig zu lernen. Daher reproduziert der Service möglicherweise für eine bestimmte Trainingsabfrage nicht immer identishce Relevanzergebnisse.

Das Training darf die folgenden **maximalen** Anforderungen nicht überschreiten:
  - Sie dürfen 24 trainierte Sammlungen pro Umgebung nicht überschreiten.
  - In einer einzigen Umgebung sind Sie auf 10.000 Trainingsabfragen begrenzt, wobei maximal 100 Beispiele pro Abfrage angegeben sind. 

## Abfrage zum Trainingsdatenbestand hinzufügen

Verwenden Sie die Methode `POST /v1/environments/{umgebungs-id}/collections/{erfassungs-id}/training_data`, um eine Abfrage zum Trainingsdatenbestand einer Sammlung hinzuzufügen. Die Abfrage wird als JSON-Objekt mit dem folgenden Format angegeben:

```json
{
  "query_id": "string",
  "natural_language_query": "string",
  "filter": "string",
  "examples": [
    {
      "document_id": "string",
      "cross_reference": "string",
      "relevance": 0
    }
  ]
}
```
{: codeblock}

Dieses Objekt enthält die folgenden Werte:

- `query_id`: Eine eindeutige ID für die Abfrage-ID. Wenn Sie dieses Feld nicht angeben, generiert der Service automatisch eine ID.
- `natural_language_query`: Eine Discovery-Abfrage in natürlicher Sprache, die auf den Trainingsbestand angewendet wird. <!-- The `natural_language_query` parameter is preferred. -->
- `filter`: Ein optionaler Filter für die Abfrage (eine Beschreibung finden Sie in der [Abfragereferenz](/docs/services/discovery/query-reference.html#parameter-descriptions)).

    **Hinweis:** Wenn Sie Filter in Ihre Trainingsdatenabfragen einbeziehen, achten Sie darauf, dieselben Filter für Abfragen in natürlicher Sprache in Ihrer trainierten Sammlung zu verwenden. Falls Sie die Sammlung mit gefilterten Daten trainieren, jedoch beim Abfragen der Sammlung nicht dieselben Filter verwenden, kann dies zu unvorhersehbaren Ergebnissen führen.

- `examples`: Ein Array mit den folgenden Werten:

   - `document_id`: Die eindeutige ID des Dokuments, das auf das Trainingsset angewendet wird. Dies ist das zuvor beschriebene *Beispiel*.
   - `cross_reference`: Eine optionale Kennung, die typischerweise aus einem Feld im referenzierten Dokument besteht und das Dokument sowie die vorhandenen Feldinformationen für den Fall 'festhält', dass sich die ID des Dokuments ändert, beispielsweise durch die Zuordnung derselben ID zu einem neu eingepflegten Dokument. Die Angabe eines Wertes für `cross-reference` bewirkt **nicht** die Verknüpfung eines Dokuments mit einem anderen Dokument, sondern stellt vielmehr sicher, dass der Service die relevanten Informationen des Dokuments aufbewahrt, falls das Dokument umbenannt oder überschrieben wird.
   - `relevance`: Eine ganze Zahl von `0` bis `100` (inklusive), mit der die relative Relevanz der Abfrage für die Trainingsdaten angegeben wird. Höhere Werte stehen für eine höhere Relevanz. Der Wert `0` gibt keine Relevanz für die Abfrage an, wohingegen der Wert `100` die absolute Relevanz für die Abfrage angibt.

   **Hinweis:** Obwohl sich der Bereich für den Parameter `relevance` zur Gewährleistung einer maximalen Flexibilität von `0` bis `100` erstreckt, können Sie einen kleineren Bereich verwenden, um die Einstufungsbeispiele zu vereinfachen. Ein Standardbereich könnte `0` bis `4` sein. Sie könnten aber auch den gesamten Bereich, jedoch hierbei nur Zwanzigerschritte verwenden (`0`,`20`,`40`,`60`,`80` und `100`). Die {{site.data.keyword.discoveryshort}}-Tools verwenden die Relevanzquoten `0` für *nicht relevant* und `10` für *relevant*. Falls Sie Ihre Dokumente sowohl mit den {{site.data.keyword.discoveryshort}}-Tools als auch der API einstufen oder zunächst die API verwenden und später auf die Tools umsteigen wollen, verwenden Sie die Relevanzquoten `0` und `10`.

Das folgende Beispiel zeigt eine mit Werten gefüllte Trainingsdatenabfrage:

```json
{
  "natural_language_query": "why is the sky blue",
  "filter": "text:meteorology",
  "examples": [
    {
      "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877",
      "relevance": 0
    },
    {
      "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81",
      "relevance": 1
    },
    {
      "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da",
      "cross_reference": "my_id_field:1463",
      "relevance": 4
    }
  ]
}
```
{: codeblock}

Der folgende Beispielbefehl fügt die obige Trainingsdatenabfrage zu einer Sammlung namens `99040100-fe6a-4782-a4f5-28f9eee30850` in einer Umgebung namens `a56dd9b4-040b-4ea3-a736-c1e7a467e191` hinzu:

```bash
curl -X POST -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" -H "Content-Type: application/json" -d
'{
  "natural_language_query": "why is the sky blue",
  "filter": "text:meteorology",
  "examples": [
    {
    "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877",
    "relevance": 0
    },
    {
      "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81",
      "relevance": 1
    },
    {
      "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da",
      "cross_reference": "my_id_field:1463",
      "relevance": 4
    }
  ]
}'
"https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data?version=2016-12-01"
```
{: pre}

## Beispiel zu einer Trainingsdatenabfrage hinzufügen

Nachdem Sie eine Trainingsdatenabfrage erstellt haben, können Sie laufend Beispiele zur Abfrage hinzufügen, um die Genauigkeit des Trainings zu verbessern. Verwenden Sie die Methode `POST /v1/environments/{umgebung-id}/collections/{sammlungs-id}/training_data/{abfrage-id}`, um ein Beispiel zu einer vorhandenen Trainingsdatenabfrage hinzuzufügen.

Führen Sie die folgenden Schritte aus, um ein Beispiel zu einer Trainingsdatenabfrage hinzuzufügen:

1. Ermitteln Sie die Abfrage-ID der Trainingsdatenabfrage, zu der Sie ein neues Beispiel hinzufügen wollen, indem Sie die [Trainingsdatenabfragen der Sammlung auflisten ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#get-training-data){: new_window}:

   ```bash
    curl -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" "https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data?version=2016-12-01"
   ```
   {: pre}

   Die JSON-Rückgabe besitzt das folgende Format:

   ```json
    {
      "query_id": "484baad4-d440-44b7-a0dd-70bb2ac77baa",
      "natural_language_query": "why is the sky blue",
      "filter": "text:meteorology",
      "examples": [
        {
          "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877",
          "relevance": 0
        },
        {
          "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81",
          "relevance": 1
        },
        {
          "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da",
          "cross_reference": "my_id_field:1463",
          "relevance": 4
        }
      ]
    }
   ```
   {: codeblock}

1. Fügen Sie das neue Beispiel unter Verwendung derselben Syntax hinzu, die Sie zum Definieren von Beispielen beim Erstellen einer neuen Trainingsdatenabfrage verwenden. Der folgende Beispielbefehl bezieht keinen Querverweis ein.

   ```bash
    curl -u -X POST -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" -H "Content-Type: application/json" -d
    '{
      "document_id": "46b52fdc-3a72-4700-9849-ac217532b373",
      "relevance": 3
    }' "https://gateway.watsonplatform.net/discovery/api/v1/environments//a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data/484baad4-d440-44b7-a0dd-70bb2ac77baa?version=2016-12-01"
   ```
   {: pre}

1. Prüfen Sie, ob das neue Beispiel zur Trainingsdatenabfage hinzugefügt wurde, indem Sie erneut die [Trainingsdatenabfragen der Sammlung auflisten ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#get-training-data){: new_window}:

   ```bash
    curl -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" "https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850/training_data?version=2016-12-01"
   ```
   {: pre}

   Die JSON-Rückgabe besitzt das folgende Format:

   ```json
    {
      "query_id": "484baad4-d440-44b7-a0dd-70bb2ac77baa",
      "natural_language_query": "why is the sky blue",
      "filter": "text:meteorology",
      "examples": [
        {
          "document_id": "9afcf06e-2ef7-438e-b2a5-e4d9432dc877",
          "relevance": 0
        },
        {
          "document_id": "54f95ac0-3e4f-4756-bea6-7a67b2713c81",
          "relevance": 1
        },
        {
          "document_id": "01bcca32-7300-4c9f-8d32-33ed7ea643da",
          "cross_reference": "my_id_field:1463",
          "relevance": 4
        },
        {
          "document_id": "46b52fdc-3a72-4700-9849-ac217532b373",
          "relevance": 3
        }
      ]
    }
   ```
   {: codeblock}

1. Überprüfen Sie den Status des Trainings, indem Sie die [Details der Sammlung auflisten ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#list-collection-details){: new_window}. Suchen Sie nach dem Wert des Feldes `"training"`/`"available"`. Wenn Sie genügend Abfragen und Beispiele hinzugefügt haben, damit die Trainingsanforderungen erfüllt sind, wird für das Feld der Wert `true` zurückgegeben und der Service beginnt automatisch mit der Verwendung der Trainingsdaten.

   ```bash
    curl -u "4ba1624f-48b6-484a-8e32-18d1c205c1fa":"qUy3B0CbGf9G" "https://gateway.watsonplatform.net/discovery/api/v1/environments/a56dd9b4-040b-4ea3-a736-c1e7a467e191/collections/99040100-fe6a-4782-a4f5-28f9eee30850?version=2016-12-01"
   ```
   {: pre}

   Die JSON-Rückgabe besitzt das folgende Format:

   ```json
    {
      "collection_id": "99040100-fe6a-4782-a4f5-28f9eee30850",
      "name": "democollection",
      "configuration_id": "def9bd08-8472-470f-ab5a-e377f77e9300",
      "language": "en_us",
      "status": "available",
      "description": "this is a demo collection",
      "created": "2015-08-24T18:42:25.324Z",
      "updated": "2015-08-24T18:42:25.324Z",
      "document_counts": {
        "available": 1000,
        "processing": 20,
        "failed": 180
      },
      "disk_usage": {
        "used_bytes": 895111
      },
      "training_status": {
        "data_updated": "2017-02-10T14:18:22.786Z",
        "total_examples": 54,
        "sufficient_label_diversity": false,
        "processing": false,
        "minimum_examples_added": true,
        "successfully_trained": "2017-02-08T14:18:22.786Z",
        "available": true,
        "notices": 13,
        "minimum_queries_added": true
      }
    }
   ```
   {: codeblock}

1. Wenn im vorherigen Schritt für alle folgenden Felder der Wert `true` zurückgegeben wird, geben Sie einige Beispielabfragen aus, um zu ermitteln, ob der Service relevantere Ergebnisse zurückgibt:

   - `minimum_queries_added`
   - `minimum_examples_added`
   - `sufficient_label_diversity`

   Falls sich die Relevanz der Ergebnisse nicht verbessert hat, fügen Sie weitere Trainingsabfragen hinzu, bis die Ergebnisse Ihren Anforderungen entsprechen.

Zusätzliche Anleitungen für das Training finden Sie unter [Tipps für das Relevanztraining](/docs/services/discovery/train-tips.html#relevancy-tips).   

## Andere Operationen für Trainingsdatenabfragen ausführen
{: #training-data-operations}

Sie können Trainingsdatenabfragen mit weiteren API-Methoden verwalten und pflegen, die in der [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window} beschrieben sind:

 - [Trainingsdaten für eine Sammlung auflisten ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#get-training-data){: new_window}
 - [Alle Trainingsdaten für eine Sammlung löschen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-all-training-data){: new_window}
 - [Inhalt einer bestimmten Trainingsdatenabfrage anzeigen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#show-td-query){: new_window}
 - [Trainingsdatenabfrage aus der Sammlung löschen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/watson/developercloud/discovery/api/v1#delete-td-query-example){: new_window}
 - [Relevanzkennung oder Querverweis eines Beispiels für eine Trainingsdatenabfrage ändern ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#update-example){: new_window}
 - [Beispieldokument aus einer Trainingsdatenabfrage löschen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-example){: new_window}

 **Fehlerüberwachung:** Fehler für Trainingsdaten werden in den Hinweisen angezeigt, die Sie mithilfe der [API für Abfragehinweise ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-notices){: new_window} überwachen können
 (`GET /v1/environments/{umgebungs-id}/collections/{sammlungs-id}/notices`).
