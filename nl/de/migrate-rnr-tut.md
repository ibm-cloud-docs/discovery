---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-09"

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


# Lernprogramm: Aus Retrieve and Rank migrieren

Hier erfahren Sie, wie Sie aus {{site.data.keyword.retrieveandrankshort}} auf den {{site.data.keyword.discoveryfull}}-Service migrieren. Dieses Lernprogramm ist eine Fortsetzung des Lernprogramms für die Einführung in Cranfield.

## Übersicht
{: #overview}
Dieses Lernprogramm führt Sie durch die Erstellung und das Training eines {{site.data.keyword.discoveryfull}}-Service mit Beispieldaten. Es verwendet denselben Datenbestand wie das [Lernprogramm für die Einführung in {{site.data.keyword.retrieveandrankshort}}](/docs/services/retrieve-and-rank/getting-started.html); mit demselben Verfahren können Sie aber auch eine Serviceinstanz erstellen, die Ihre eigenen Daten verwendet.

Der Prozess, mit dem Benutzer Daten aus {{site.data.keyword.retrieveandrankshort}} nach {{site.data.keyword.discoveryshort}} migrieren, besteht aus zwei Hauptschritten.

1. Sammlungsdaten migrieren
2. Trainingsdaten migrieren

Wenn Sie Ihre trainierten Sammlungsdaten migrieren, ist es **am wichtigsten**, dass die _Dokument-IDs identisch bleiben_. Dies liegt daran, dass Ihre Trainingsdaten diese IDs zur Referenzierung von Ground Truth verwenden. Falls die IDs bei der Migration von {{site.data.keyword.retrieveandrankshort}} auf {{site.data.keyword.discoveryshort}} geändert werden, ist eine erneute Einstufung völlig unmöglich (oder das Training selbst wird nicht einmal gestartet). Bei {{site.data.keyword.discoveryshort}} können Sie die Dokument-ID im API-Uploadprozess angeben, so dass Sie dieses Problem anhand der Anweisungen in diesem Dokument vermeiden können.  Die Trainingsdaten von {{site.data.keyword.retrieveandrankshort}} sind normalerweise in einer `CSV`-Datei gespeichert. In diesem Lernprogramm wird diese `CSV`-Datei verwendet, um dieselben Trainingsdaten in {{site.data.keyword.discoveryshort}} hochzuladen.  Die Migration von Trainingsdaten, die aus den Tools von {{site.data.keyword.retrieveandrankshort}} exportiert wurden, ist detailliert im Abschnitt [Trainingsdaten aus dem Service migrieren](/docs/services/discovery/migrate-dcs-rr.html#extract-train) erläutert.

Dieses Lernprogramm setzt voraus, dass {{site.data.keyword.retrieveandrankshort}} ähnlich wie im [Lernprogramm für die Einführung in {{site.data.keyword.retrieveandrankshort}}](/docs/services/retrieve-and-rank/getting-started.html) konfiguriert wurde, und verwendet für die Migration den [hier](/docs/services/discovery/migrate-dcs-rr.html#source) beschriebenen Quellenpfad. Weitere Migrationsoptionen sind unter [Pfad zur Migration auf Watson Discovery-Service bewerten](/docs/services/discovery/migrate-dcs-rr.html#evaluate) beschrieben.

Zur Durcharbeitung des Lernprogramms benötigen Sie Folgendes:

-  **cURL.**  Sie können die cURL-Version für Ihr Betriebssystem installieren, die auf der Seite [haxx.se ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://curl.haxx.se/){: new_window} verfügbar ist. Sie müssen die Version installieren, die das Protokoll 'Secure Sockets Layer' (SSL) unterstützt. Denken Sie daran, die installierte Binärdatei in Ihre Umgebungsvariable PATH aufzunehmen.
-  Cranfield-Beispieldaten. Dieses Lernprogramm verwendet dieselben Sammlungsdaten wie das Lernprogramm für die Einführung in {{site.data.keyword.retrieveandrankshort}} (verfügbar auf der Seite mit den [Cranfield-JSON-Daten ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-data.json){: new_window}).
-  **Ground Truth für Beispieldaten**. Dieses Lernprogramm verwendet das Cranfield-Beispiel für Ground Truth aus dem Lernprogramm für die Einführung in {{site.data.keyword.retrieveandrankshort}} (verfügbar auf der Seite mit der [CSV-Datei für Ground Truth von Cranfield ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-gt.csv){: new_window}).
-  **Python Version 2.**  Um festzustellen, ob Python installiert ist, geben Sie `python --version` an einer Eingabeaufforderung ein und vergewissern Sie sich, dass die Versionsnummer mit 2 beginnt. Falls Sie Python installieren müssen, finden Sie auf der Seite [Downloading Python ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://wiki.python.org/moin/BeginnersGuide/Download){: new_window} weiterführende Informationen.
-  Script für Datenupload (verfügbar auf der Seite mit dem [Discovery-Dokumentuploader ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-upload.py){: new_window}).
-  Script für Trainingsdatenupload (verfügbar auf der Seite mit dem [Discovery-Trainingsuploader ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-train.py){: new_window}).

Bevor Sie mit diesem Lernprogramm beginnen, müssen die folgenden Voraussetzungen erfüllt sein:

-  Dieses Lernprogramm geht davon aus, dass Sie bereits eine {{site.data.keyword.discoveryshort}}-Instanz erstellt haben. Anweisungen zur Erstellung einer {{site.data.keyword.discoveryshort}}-Instanz enthält ein [weiteres Lernprogramm](/docs/services/discovery/getting-started.html).

-  Dieses Lernprogramm geht davon aus, dass Sie Ihre Serviceberechtigungsnachweise kennen.
   -  Klicken Sie im Watson {{site.data.keyword.discoveryshort}}-Service von {{site.data.keyword.Bluemix_notm}} auf **Serviceberechtigungsnachweise**.
   -  Klicken Sie unter 'Aktionen' auf **Berechtigungsnachweise anzeigen**.
   -  Kopieren Sie den Wert für `apikey` und stellen Sie sicher, dass der Wert für `url` mit dem Wert in den nachfolgenden Beispielen übereinstimmt. Falls nicht, ersetzen Sie ihn ebenfalls.

## Cranfield-Daten zu Discovery hinzufügen

1.  Erstellen Sie eine Umgebung.

    ```bash
    curl -X POST -u "apikey":"{wert_des_api-schlüssels}" -H "Content-Type: application/json" -d '{ "name": "my_environment", "description": "My environment" }' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    Kopieren Sie den Wert für `environment_id`, der in der JSON-Rückgabe angegeben ist.

1. Erstellen Sie eine Sammlung.

    ```bash
    curl -X POST -u "apikey":"{wert_des_api-schlüssels}" -H "Content-Type: application/json" -d '{ "name": "test_collection", "description": "My test collection", "configuration_id": "{konfigurations-id}", "language_code": "en" }' "https://gateway.watsonplatform.net/discovery/api/v1/environments/{umgebungs-id}/collections?version=2017-11-07"
    ```
    {: pre}

    Kopieren Sie die `sammlungs-id`, die in der JSON-Rückgabe angegeben ist.

1.  Fügen Sie die Dokumente hinzu, die durchsucht werden sollen.
    1.  Laden Sie die Datei [cranfield-data.json ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-data.json){: new_window} herunter, wenn Sie dies noch nicht getan haben. Dies ist die Quelle der Dokumente, die in {{site.data.keyword.retrieveandrankshort}} verwendet werden. Die Dokumente der Cranfield-Sammlung besitzen das JSON-Format, also das von {{site.data.keyword.retrieveandrankshort}} akzeptierte Format, das auch für Watson {{site.data.keyword.discoveryshort}} gut geeignet ist.
        **Hinweis:** Das Solr-Schema muss für {{site.data.keyword.discoveryshort}} nicht hochgeladen werden. Dies liegt daran, dass {{site.data.keyword.discoveryshort}} das Schema automatisch aus der JSON-Struktur übernimmt.
    1.  Laden Sie das Script für den Datenupload [hier ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-upload.py){: new_window} herunter. Dieses Script lädt das Cranfield-JSON in {{site.data.keyword.discoveryshort}} hoch.
        Das Script liest die JSON-Datei durch und sendet jedes einzelne JSON-Dokument an den {{site.data.keyword.discoveryshort}}-Service; hierbei wird eine Standardkonfiguration in {{site.data.keyword.discoveryshort}} verwendet.
        **Hinweis:** Die Standardkonfiguration in {{site.data.keyword.discoveryshort}} stellt ähnliche Einstellungen wie die Solr-Standardkonfiguration in {{site.data.keyword.retrieveandrankshort}} bereit.
    1.  Geben Sie den folgenden Befehl aus, um die Daten von `cranfield-data-json` in die Sammlung `cranfield_collection` hochzuladen. Ersetzen Sie `{wert_des_api-schlüssels}`, `{pfad_zur_datei}`, `{umgebungs-id}` und `{sammlungs-id}` durch Ihre Informationen. Bitte beachten Sie, dass es weitere Optionen gibt (-d für das Debug und –v für eine ausführliche Ausgabe von curl).

        ```bash
        python ./disco-upload.py -u apikey:{wert_des_api-schlüssels} -i {pfad_zur_datei}/cranfield-data.json -e {umgebungs-id} -c {sammlungs-id}
        ```
        {: pre}

1.  Nachdem der Uploadprozess abgeschlossen ist, können Sie überprüfen, ob die Dokumente vorhanden sind, indem Sie den folgenden Befehl zum Anzeigen der Sammlungsdetails ausgeben:

    ```bash
    curl -u "apikey":"{wert_des_api-schlüssels}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{umgebungs-id}/collections/{sammlungs-id}?version=2017-11-07"
    ```
    {: pre}

    Die Ausgabe sieht in etwa folgendermaßen aus:

    ```json
    {
      "collection_id": "f1360220-ea2d-4271-9d62-89a910b13c37",
      "name": "democollection",
      "configuration_id": "6963be41-2dea-4f79-8f52-127c63c479b0",
      "language": "en",
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
        "used_bytes": 260
      },
      "training_status": {
        "data_updated": null,
        "total_examples": 0,
        "sufficient_label_diversity": false,
        "processing": false,
        "minimum_examples_added": true,
        "successfully_trained": null,
        "available": false,
        "notices": 0,
        "minimum_queries_added": false        
      }
    }
    ```
    {: codeblock}

Stellen Sie im Abschnitt `document_counts` fest, wie viele Dokumente erfolgreich hochgeladen wurden. Bei diesem Beispieldatenbestand sollten eigentlich keine Dokumentfehler auftreten. Bei anderen Datenbeständen wird jedoch möglicherweise eine Zahl für fehlgeschlagene Dokumente angegeben. In einem solchen Fall können Sie die APIs für Hinweise aufrufen, um die Fehlernachrichten anzuzeigen. Den Befehl für die API für Hinweise finden Sie [hier ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-notices){: new_window}.

Der Abschnitt `training` der Rückgabe vermittelt Ihnen Informationen zu Ihrem  Training. Auf diesen Abschnitt kommen wird zurück, nachdem Sie die Trainingsdaten hochgeladen haben.

## Trainingsdaten in Discovery hinzufügen

Der Watson {{site.data.keyword.discoveryshort}}-Service verwendet ein Modell für maschinelles Lernen, um Dokumente erneut einzustufen. Dazu müssen Sie ein Modell trainieren. Das Training findet statt, nachdem Sie genügend Abfragen mit den zugehörigen eingestuften Dokumenten geladen haben. Indem Sie genügend Beispiele mit ausreichender Varianz für Watson {{site.data.keyword.discoveryshort}} laden, vermitteln Sie, was ein 'geeignetes' Dokument ist. In diesem Schritt wird der vorhandene Ground Truth von Cranfield aus {{site.data.keyword.retrieveandrankshort}} verwendet, um Watson {{site.data.keyword.discoveryshort}} zu trainieren.

1.  Laden Sie die [CSV-Beispieldatei für Ground Truth von Cranfield ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-gt.csv){: new_window} aus dem Lernprogramm für {{site.data.keyword.retrieveandrankshort}} herunter, wenn Sie dies noch nicht getan haben.

   Die Datei enthält eine Reihe von Fragen, die ein Benutzer zu den Dokumenten stellen könnte. Sie stellt die Beispielinformationen für das Training der Einstufungskomponte (Ranker) in {{site.data.keyword.retrieveandrankshort}} und das Relevanztraining in {{site.data.keyword.discoveryshort}} über Fragen und relevante Antworten bereit.

   Für jede Frage gibt es mindestens eine ID für eine Antwort (die Dokument-ID). Jede Dokument-ID bezieht eine Zahl ein, die Aufschluss darüber gibt, wie relevant die Antwort für die Frage ist. Die Dokument-ID zeigt auf die Antwort in der Datei `cranfield-data.json`, die Sie mit dem vorherigen Schritt in {{site.data.keyword.discoveryshort}} hochgeladen haben.

1.  Laden Sie das Script für den Trainingsdatenupload herunter. Dieses Script verwenden Sie, um die Trainingsdaten in {{site.data.keyword.discoveryshort}} hochzuladen. Das Script wandelt die `CSV`-Datei in eine Reihe von JSON-Abfragen und -Beispiele um und sendet diese an den {{site.data.keyword.discoveryshort}}-Service (mithilfe der [APIs für Trainingsdaten ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#training-data){: new_window}.
    **Hinweis:** {{site.data.keyword.discoveryshort}} verwaltet Trainingsdaten innerhalb des Service, so dass neu generierte Beispiele und Trainingsabfragen in {{site.data.keyword.discoveryshort}} selbst gespeichert werden können, statt hierzu eine separate CSV-Datei zu verwenden, die verwaltet werden muss.
1.  Führen Sie das Script für den Trainingsdatenupload aus, um die Trainingsdaten in {{site.data.keyword.discoveryshort}} hochzuladen. Ersetzen Sie `{wert_des_api-schlüssels}`, `{pfad_zur_datei}`, `{umgebungs-id}` und `{sammlungs-id}` durch Ihre Informationen. Bitte beachten Sie, dass es weitere Optionen gibt (`-d` für das Debug und `–v` für eine ausführliche Ausgabe von curl).

    ```bash
    python ./disco-train.py -u apikey:{wert_des_api-schlüssels} -i {pfad_zur_datei}/cranfield-gt.csv –e {umgebungs-id} -c {sammlungs-id}
    ```
    {: pre}

1.  Nachdem die Daten geladen wurden, können Sie den Status des Trainings mithilfe des Befehls für die Sammlungsdetails überprüfen, der im vorherigen Abschnitt angegeben ist. {{site.data.keyword.discoveryshort}} überprüft ungefähr einmal stündlich, ob neue Daten vorhanden sind. Wenn dies der Fall ist, beginnt der Service mit ihrer Verarbeitung und nimmt sie in ein Modell für maschinelles Lernen auf. Wenn ein Modell trainiert wird, ändert sich der Status des Trainingsabschnitts von `"processing": false` in `"processing": true`. Nachdem das Modell trainiert wurde, ändert sich der Status im Trainingsabschnitt von `"available": false` in `"available": true`. Außerdem wird das Datum für den Wert `"successfully_trained"` geändert.  Falls Fehler aufgetreten sind, können Sie diese in der **API für Hinweise** anzeigen (siehe vorheriger Abschnitt).

## Nach Dokumenten suchen
{: search}

Der {{site.data.keyword.discoveryshort}}-Service verwendet ein trainiertes Modell automatisch, um Suchergebnisse erneut einzustufen, wenn ein solches Modell verfügbar ist. Wenn ein [API-Aufruf ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection){: new_window} mit `natural_language_query` anstelle von `query` erfolgt, wird geprüft, ob ein Modell verfügbar ist. Ist ein Modell verfügbar, verwendet {{site.data.keyword.discoveryshort}} dieses Modell, um die Ergebnisse erneut einzustufen. Zunächst werden Sie nun eine Suche unter nicht eingestuften Dokumenten ausführen. Anschließend erfolgt eine Suche unter Verwendung des Einstufungsmodells.

1.  Mit einem cURL-Befehl können Sie in Ihrer Sammlung nach Dokumenten suchen. Führen Sie eine Abfrage mit einem Aufruf der Abfrage-API aus, um nicht eingestufte Ergebnisse anzuzeigen. Ersetzen Sie `{wert_des_api-schlüssels}`, `{umgebungs-id}` und `{sammlungs-id}` durch Ihre eigenen Werte. Die zurückgegebenen Ergebnisse sind nicht eingestuft und verwenden die {{site.data.keyword.discoveryshort}}-Standardeinstufungsformeln. Sie können weitere Abfragen ausprobieren, indem Sie die `CSV`-Datei mit den Trainingsdaten öffnen und den Wert der ersten Spalte in den Abfrageparameter kopieren.

    ```bash
    curl -u "apikey":"{wert_des_api-schlüssels}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{umgebungs-id}/collections/{sammlungs-id}/query?version=2017-11-07&query=what is the basic mechanism of the transonic aileron buzz"
    ```
    {: pre}

1.  Nun führen Sie eine Suche unter Verwendung des Modells aus, indem Sie den Parameter `natural_language_query` angeben. Vergewissern Sie sich zuvor, dass ein trainiertes Modell wie im vorherigen Abschnitt beschrieben verfügbar ist.  Fügen Sie den folgenden Code in Ihre Konsole ein und ersetzen Sie dabei den Wert für `{wert_des_api-schlüssels}`, `{umgebungs-id}` und `{sammmlungs-id}` durch Ihre Werte.

    ```bash
    curl -u "apikey":"{wert_des_api-schlüssels}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{umgebungs-id}/collections/{sammlungs-id}/query?version=2017-11-07&natural_language_query=what is the basic mechanism of the transonic aileron buzz"
    ```
    {: pre}

    Dieser Befehl gibt Ergebnisse zurück, die mit dem zuvor trainierten Modell erneut eingestuft wurden. Vergleichen Sie die Ergebnisse dieser Suche mit den Ergebnissen einiger anderer Suche, die Sie zuvor ausprobiert haben. Möglicherweise stellen Sie im Vergleich zur Darstellung in {{site.data.keyword.retrieveandrankshort}} einige Unterschiede bei den Ergebnissen fest. Dies liegt daran, dass die verwendeten Suchverfahren geändert wurden, um den Prozess zu vereinfachen und die Ergebnisse zu verbessern. Die Gesamtqualität der Ergebnisse ist jedoch ähnlich.

Nachdem Sie die erneut eingestuften Suchergebnisse ausgewertet haben, können Sie sie in {{site.data.keyword.discoveryshort}} optimieren, indem Sie das Hochladen von Trainingsdaten mit zusätzlichen Trainingsabfragen und Beispielen wiederholen und anschließend die Suchergebnisse anzeigen.  Sie können auch, wie im ersten Schritt beschrieben, neue Dokumente hinzufügen, um den Umfang der Suche zu vergrößern. Ähnlich wie bei {{site.data.keyword.retrieveandrankshort}} ist die Verbesserung von Ergebnissen durch das Training ein wiederholt auszuführender Prozess.
