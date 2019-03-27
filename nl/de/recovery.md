---

copyright:
  years: 2019
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

# Hochverfügbarkeit und Disaster Recovery
{: #recovery}

{{site.data.keyword.discoveryfull}} unterstützt Hochverfügbarkeit ohne Single Point of Failure. Darüber hinaus liegt es in Ihrer Verantwortung, Ihre {{site.data.keyword.discoveryshort}}-Daten im Rahmen Ihres eigenen Disaster-Recovery-Plans zu sichern, damit Sie Ihren Service erneut erstellen können.{: shortdesc}

Der {{site.data.keyword.discoveryshort}}-Datenverkehr ist innerhalb einer Region über mehrere Zonen verteilt. Jede Zone ist ein Datenzentrum in derselben Region. Weitere Informationen finden Sie unter [Wie sorge ich für null Ausfallzeit? ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/docs/overview?topic=overview-zero-downtime#zero-downtime){: new_window}.

## Daten in Watson Discovery sichern
{: #backup}

Es gibt verschiedene Methoden, um die in {{site.data.keyword.discoveryfull}} gespeicherten Daten zu sichern. Diese Methoden sollten in Ihrem Disaster-Recovery-Plan enthalten sein.

-  Daten, für die Sie eine Kopie beibehalten sollten, z. B. Quellendokumente
-  Daten, die {{site.data.keyword.discoveryshort}} speichert und die Sie extrahieren und sichern sollten
  
Es wird Daten geben, die von Grund auf neu erstellt werden müssen (z. B. Daten, die nicht gesichert werden können, wie Feedbackereignisse.) 

### Eingepflegte Dokumente
{: #backupdocs}

Ihre hochgeladenen Dokumente werden konvertiert und aufbereitet und anschließend im Suchindex gespeichert. Der Suchindex ist nach einem Notfall nicht wiederherstellbar, daher sollten Sie eine Sicherung aller Quellendokumente an einem sicheren Ort speichern.

Wenn Sie Dokumente auch importieren, indem Sie geplante Crawlersuchen für externe Datenquellen ausführen, sollten Sie Ihre Datenquellenberechtigungsnachweise extern verwahren, damit Sie Ihre Datenquellen schnell wiederherstellen können. Eine Liste der verfügbaren Quellen und der für die einzelnen Quellen erforderlichen Berechtigungsnachweise finden Sie unter [Verbindung zu Datenquellen herstellen](/docs/services/discovery?topic=discovery-sources#sources).

### Konfigurationen
{: #backupconfigs}

Sie sollten Ihre Instanzkonfigurationen sichern und für einen Notfall lokal speichern. 

Zum Sichern dieser Konfigurationen [listen Sie zunächst für jede Instanz Ihre Konfigurationen auf](https://cloud.ibm.com/apidocs/discovery#list-configurations). 

Nach dem Abrufen der Liste von Konfigurationen [rufen Sie für jede Konfiguration die Details ab](https://cloud.ibm.com/apidocs/discovery#get-configuration-details).

### Trainingsdaten
{: #backuptraining}

Sie sollten Ihre Trainingsdaten für jede trainierte Sammlung sichern und für einen Notfall lokal speichern. 

Trainingsdaten werden für das explizite Training Ihrer Sammlungen verwendet und nach Sammlung gespeichert. 

Zum Extrahieren der Trainingsdaten laden Sie über die API die Abfragen und Einstufungen von {{site.data.keyword.discoveryshort}} herunter. 

1.  [Trainingsdaten auflisten](https://cloud.ibm.com/apidocs/discovery#list-training-data)
1.  [Listen Sie die Beispiele für jede Abfrage auf](https://cloud.ibm.com/apidocs/discovery#list-examples-for-a-training-data-query).
1.  [Rufen Sie die Details für Trainingsdatenbeispiele ab](https://cloud.ibm.com/apidocs/discovery#get-details-for-training-data-example). 

Die `Dokument-IDs`, die Sie in Ihrem Trainingsdatenpunkt verwenden, verweisen auf die Dokumente in Ihrer aktuellen Sammlung. Sie MÜSSEN dieselben `Dokument-IDs` in Ihren neuen Sammlungen verwenden, um sicherzustellen, dass auf die richtigen IDs verwiesen wird. Wenn dies nicht der Fall ist, wird das wiederhergestellte Relevanztraining NICHT FUNKTIONIEREN.{: important} 

### Abfragen
{: #backupqueries}

Standardmäßig werden von {{site.data.keyword.discoveryshort}} die Abfragen gespeichert, die Sie dorthin senden, sofern Sie diese Option nicht abwählen. 

Wenn Sie sie für [statische Zwecke](https://cloud.ibm.com/apidocs/discovery#number-of-queries-over-time) wiederherstellen können möchten, sollten diese Abfragen separat gespeichert werden. 

Sie können aus {{site.data.keyword.discoveryshort}} [Abfragen extrahieren](https://cloud.ibm.com/apidocs/discovery#search-the-query-and-event-log); es werden jedoch maximal 10.000 Abfragen gespeichert. Es gibt keine Paging-API. Das Wiederherstellen von Abfragen wird nicht empfohlen; vielmehr sollte von Grund auf neu begonnen werden.

### Feedback/Klicks
{: #clicks}

Wenn Sie Klicks in Form von Feedbackereignissen speichern, gibt es derzeit keine einfache Möglichkeit, diese Informationen zu sichern und wiederherzustellen. Die Empfehlung ist, mit der API für [Klicks/Feedbackdaten](https://cloud.ibm.com/apidocs/discovery#create-event) von Grund auf neu zu beginnen.

### Erweiterungslisten
{: #backupexpansions}

Wenn Sie Erweiterungen für Abfragemodifikationen verwenden, sollten Sie Ihre Erweiterungslisten sichern und lokal speichern. Dazu fordern Sie mit dem API-Befehl [get expansion list](https://cloud.ibm.com/apidocs/discovery#get-the-expansion-list) die Erweiterungsliste an und speichern sie lokal.

### Angepasste Wörterverzeichnisse für die Zerlegung in Tokens oder Stoppwörter
{: #backupstopwords}

Wenn Sie diese Funktionen verwenden, müssen Sie diese Dateien sichern und lokal speichern. Bei Stoppwörtern sichern Sie die Textdatei. Bei Zerlegungen in Tokens sollten Sie die JSON-Datei sichern. Weitere Informationen zu den einzelnen Dateitypen finden Sie unter [Angepasste Wörterverzeichnisse für die Zerlegung in Tokens erstellen](/docs/services/discovery?topic=discovery-query-concepts#tokenization) und [Stoppwörter definieren](/docs/services/discovery?topic=discovery-query-concepts#stopwords).

### Sammlungsinformationen
{: #collectioninfo}

Es ist zwar nicht erforderlich, aber ein bewährtes Verfahren, [den Status für jede Sammlung regelmäßig abzurufen](https://cloud.ibm.com/apidocs/discovery#get-collection-details) und die Informationen lokal zu speichern. Das Beibehalten dieser Statistikdaten ermöglicht Ihnen später bei Bedarf die Überprüfung, ob Ihre Wiederherstellungsprozesse erfolgreich waren.
{: tip} 


### Smart Document Understanding-Modelle
{: #backupsdu}

Wenn Sie Smart Document Understanding (SDU) verwenden, werden Ihrer Konfiguration Modelle zugeordnet. Um einen Verlust dieser Informationen zu vermeiden, sollten Sie [Ihre Modelle exportieren](/docs/services/discovery?topic=discovery-sdu#import), sie sichern und lokal speichern. SDU-Modelle haben die Dateierweiterung `.sdumodel`.


## Daten in einer neuen Watson Discovery-Instanz wiederherstellen
{: #restore}

Mit Ihren Sicherungen können Sie Ihre Daten in einer neuen {{site.data.keyword.discoveryshort}}-Instanz in einem anderen Rechenzentrum wiederherstellen (auch als Region oder Standort bezeichnet, z. B. Dallas, Houston, Washington, DC, oder London). 
{: note}

Zu Beginn der Wiederherstellung überprüfen Sie erst Ihre Liste von Sammlungen und zugehörigen Datenquellen sowie Ihre Dateisicherungen.

-  Erstellen Sie Ihre [Umgebung](https://cloud.ibm.com/apidocs/discovery#create-an-environment) und [Sammlungen](https://cloud.ibm.com/apidocs/discovery#create-a-collection) anhand der gespeicherten Konfigurationsinformationen. Stellen Sie sicher, dass die entsprechende Konfiguration ordnungsgemäß definiert und die Sprache für die Sammlung ordnungsgemäß festgelegt ist. Wenn Sie dies nicht tun, wird die Sicherung und Ausführung Ihres Systems verzögert.
-  Falls Sie in {{site.data.keyword.discoveryshort}} angepasste Konfigurationen eingerichtet haben, müssen Sie diese [angepassten Konfigurationen erneut erstellen](/docs/services/discovery?topic=discovery-configservice#when-you-need-a-custom-configuration). 
-  Fügen Sie angepasste Wörterverzeichnisse für die Zerlegung in Tokens oder Stoppwörter wieder in die Sammlungen ein. Siehe hierzu [>Angepasste Wörterverzeichnisse für die Zerlegung in Tokens erstellen](/docs/services/discovery?topic=discovery-query-concepts#tokenization) und [Stoppwörter definieren](/docs/services/discovery?topic=discovery-query-concepts#stopwords). 
-  Wenn Sie eine angepasste Abfrageerweiterung ausgeführt haben, müssen Sie für jede Sammlung auch [Ihre Abfrageerweiterungen hinzufügen](https://cloud.ibm.com/apidocs/discovery#create-or-update-expansion-list). 
-  Falls Sie angepasste Entitätsmodelle aus Watson Knowledge Studio (WKS) für die Aufbereitung verwendet haben, müssen Sie in Ihre {{site.data.keyword.discoveryshort}}-Instanz [dieses Modell erneut importieren](/docs/services/discovery?topic=discovery-configservice#custom-entity-model).

Nachdem Sie Ihre Sammlungskonfiguration wie zuvor eingerichtet haben, müssen Sie zunächst mit dem Einpflegen Ihrer Quellendokumente beginnen. Je nachdem, wie Sie Ihre Dokumente zuvor eingepflegt haben, können Sie Folgendes verwenden:
-  Die [-API](https://cloud.ibm.com/apidocs/discovery#add-a-document)
-  Einen [-Connector](/docs/services/discovery?topic=discovery-sources#sources) 
-  Den [Data Crawler](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler)
-  oder andere Methoden

### Trainingsdaten wiederherstellen
{: #restoretraining}

Nachdem die Sammlungen wiederhergestellt wurden, können Sie mit dem Prozess der [Neuerstellung von Modellen für das Relevanztraining](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api) beginnen. 

Rufen Sie die Trainingsdaten ab, die Sie gesichert haben, und führen Sie anschließend Folgendes aus:

1. [Abfragen hochladen](https://cloud.ibm.com/apidocs/discovery#add-query-to-training-data)
1. [Beispieldokumente für jede Abfrage hochladen](https://cloud.ibm.com/apidocs/discovery#add-example-to-training-data-query).
1.  Nachdem die Trainingsdaten hochgeladen wurden, lesen Sie diesen [Blogbeitrag](https://developer.ibm.com/dwblog/2017/get-relevancy-training/), um sicherzustellen, dass Sie die vorherigen Genauigkeitszahlen erfüllen. Denken Sie daran, dass alte `Dokument-IDs` an die neuen Trainingsdaten übertragen oder aktualisiert werden müssen, um die neuen Dokument-IDs in Ihrer neuen Sammlung wiederzugeben.


### Verbindungen zu externen Datenquellen wiederherstellen
{: #restoreconnections}

Im Falle eines unerwarteten Datenverlusts können Sie auch Ihre geplanten Crawlersuchen für externe Datenquellen verlieren. Eine Liste der verfügbaren Quellen finden Sie unter [Verbindung zu Datenquellen herstellen](/docs/services/discovery?topic=discovery-sources#sources).

Zum Wiederherstellen Ihrer externen Daten müssen Sie die Verbindungen zu diesen Datenquellen wieder herstellen und diese anschließend erneut durchsuchen.

Suchen Sie die zuvor von Ihnen gespeicherten Datenquellenberechtigungsnachweise und folgen Sie den Anweisungen [in diesem Abschnitt](/docs/services/discovery?topic=discovery-sources#sources). Dadurch können Sie eine erneute Verbindung zu Ihren Datenquellen herstellen und die Daten abrufen, die in {{site.data.keyword.discoveryshort}} importiert wurden.


### Smart Document Understanding-Modelle wiederherstellen
{: #restoresdu}

Führen Sie die Anweisungen [in diesem Abschnitt](/docs/services/discovery?topic=discovery-sdu#import) aus, um ein zuvor exportiertes Smart Document Understanding-Modell (SDU-Modell) zu importieren. SDU-Modelle haben die Dateierweiterung `.sdumodel`.

Wenn Sie ein vorhandenes SDU-Modell in eine neue Sammlung importieren, ist es ein bewährtes Verfahren, die neue Sammlung zu erstellen und ein einziges Dokument hinzuzufügen, anschließend das Modell zu importieren und danach die restlichen Dokumente hochzuladen.
