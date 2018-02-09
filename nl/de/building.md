---

copyright:
  years: 2015, 2017
lastupdated: "2017-12-15"

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

# Service konfigurieren

Durch die Erstellung eines {{site.data.keyword.discoveryshort}}-Service können Sie nützliche Erkenntnisse erzielen, indem Sie Ihre eigenen Daten aufbereiten und anschließend in einem abfragefähigen Format übergeben.
{: shortdesc}

Bevor Sie eigenen Inhalt zum {{site.data.keyword.discoveryshort}}-Service hinzufügen, sollten Sie den Service konfigurieren, damit der Inhalt auf die von Ihnen gewünschte Weise verarbeitet wird.

Der erste Schritt besteht im Konfigurieren der Basisparameter für den Service ([Service für Dokumente vorbereiten](/docs/services/discovery/building.html#preparing-the-service-for-your-documents)). Dies umfasst die Erstellung einer Umgebung sowie einer oder mehrerer Sammlungen in dieser Umgebung. Beim Erstellen einer Sammlung wird automatisch eine Reihe von Standardwerten ([Standardkonfiguration](/docs/services/discovery/building.html#the-default-configuration)) bereitgestellt. Wenn diese Standardwerte Ihren Vorstellungen entsprechen, können Sie mit dem Hochladen Ihres Inhalts fortfahren ([Inhalt hinzufügen](/docs/services/discovery/adding-content.html)).

Höchstwahrscheinlich werden Sie jedoch eine oder mehrere angepasste Konfigurationen angeben wollen (siehe [Situationen, in denen eine angepasste Konfiguration erforderlich ist](/docs/services/discovery/building.html#when-you-need-a-custom-configuration)). In diesem Fall müssen Sie Folgendes ausführen:

-   Beispielinhalt ermitteln (also Dokumente, die für Ihre Dateien repräsentativ sind)
-   Inhalt hochladen ([Beispieldokumente hochladen](/docs/services/discovery/building.html#uploading-sample-documents))
-   Konvertierungsprozess anpassen ([Beispieldokumente konvertieren](/docs/services/discovery/building.html#converting-sample-documents))
-   Aufbereitungen definieren ([Aufbereitungen hinzufügen](/docs/services/discovery/building.html#adding-enrichments))
-   Ergebnisse normalisieren ([Daten normalisieren](/docs/services/discovery/building.html#normalizing-data))

    Nachdem Sie Ihre angepasste Konfiguration erstellt haben, können Sie Ihre Dokumente hochladen ([Inhalt hinzufügen](/docs/services/discovery/adding-content.html)).

## Service für Dokumente vorbereiten
{: #preparing-the-service-for-your-documents}

Im {{site.data.keyword.discoveryshort}}-Service wird der Inhalt, den Sie hochladen, in einer Sammlung gespeichert, die Bestandteil Ihrer Umgebung ist. Sie müssen die Umgebung und die Sammlung erstellen, bevor Sie Ihren Inhalt hochladen können.

-   **Umgebung**: Die Umgebung definiert den Umfang der Speicherkapazität, die Ihnen für Inhalt im {{site.data.keyword.discoveryshort}}-Service zur Verfügung steht. Für jede Instanz des {{site.data.keyword.discoveryshort}}-Service kann maximal eine Umgebung erstellt werden.

    Falls Sie unter mehreren Plänen auswählen können (Lite, Standard und Advanced), finden Sie im [{{site.data.keyword.discoveryshort}}-Katalog ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window} detaillierte Angaben. Ihre Quellendateien werden bei der Zählung für die Dateigrößenbegrenzung nicht berücksichtigt.

-   **Sammlung**: Eine Sammlung ist eine Gruppierung Ihres Inhalts in der Umgebung. Sie müssen mindestens eine Sammlung erstellen, damit Sie Ihren Inhalt hochladen können.

    Sammlungen bestehen aus Ihren privaten Daten, aber {{site.data.keyword.discoveryshort}} enthält ebenfalls den voraufbereiteten allgemein zugänglichen Datenbestand '{{site.data.keyword.discoverynewsshort}}'. Diesen Datenbestand können Sie zur Abfrage von Erkenntnissen verwenden (beispielsweise durch Alertausgabe für Nachrichten, Ereigniserkennung und Trendermittlung für Themen in den Nachrichten), die Sie in Ihre Anwendungen integrieren können.

    {{site.data.keyword.discoverynewsshort}}, ein allgemein zugänglicher Datenbestand, der vorab mit kognitiven Informationen aufbereitet wurde, ist ebenfalls in {{site.data.keyword.discoveryshort}} enthalten. Weitere Informationen finden Sie unter [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html#watson-discovery-news). Das Anpassen der {{site.data.keyword.discoverynewsshort}}-Konfiguration oder das Hinzufügen von Dokumenten zu dieser Sammlung ist nicht möglich. Was Sie mit {{site.data.keyword.discoverynewsshort}} erstellen können, ist in einem [Demo ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://discovery-news-demo.mybluemix.net/){: new_window} gezeigt.

So erstellen Sie eine Umgebung und eine private Datensammlung mit den {{site.data.keyword.discoveryshort}}-Tools:

1.  Klicken Sie in der Anzeige **Daten verwalten** auf das Symbol ![Cog](images/icon_settings.png) und wählen Sie die Option **Umgebung erstellen** aus. Die Umgebung wird auf der Basis des zuvor von Ihnen ausgewählten {{site.data.keyword.Bluemix_notm}}-Plans erstellt. Mithilfe dieses Dropdown-Felds können Sie sich jederzeit über den Status Ihrer Umgebung informieren.

1.  Sobald Ihre Umgebung bereit ist, klicken Sie auf die Schaltfläche **Datensammlung erstellen**. Anschließend können Sie Ihre neue **Datensammlung benennen**.

    Als Konfigurationsdatei wird standardmäßig die **Standardkonfiguration** verwendet. Falls eine andere Konfigurationsdatei verfügbar ist, können Sie diese Datei auswählen oder auch später eine neue Datei erstellen und sie auf diese Sammlung anwenden. Außerdem können Sie die Sprache der Dokumente auswählen, die Sie zu dieser Sammlung hinzufügen (Englisch, Deutsch, Spanisch, Arabisch, Französisch, Italienisch, Koreanisch oder Portugiesisch (Brasilien)). Jede Ihrer Sammlungen sollte nur eine einzige Sprache beinhalten. Nachdem Sie auf **Erstellen** geklickt haben, wird Ihre Datensammlung als Kachel angezeigt.

Ihre Umgebung und Ihre Datensammlung sind jetzt bereit! Falls Sie die Standardkonfigurationsdatei verwenden wollen, können Sie sofort mit dem [Hinzufügen von Inhalt](/docs/services/discovery/adding-content.html) beginnen. Wenn Sie jedoch Ihre {{site.data.keyword.discoveryshort}}-Konfiguration mit zusätzlichen Aufbereitungen und Konvertierungseinstellungen anpassen möchten, sollten Sie jetzt noch keine Dokumente hinzufügen, sondern zunächst Ihre angepasste Konfigurationsdatei erstellen. Weitere Informationen enthält der Abschnitt [Service konfigurieren](/docs/services/discovery/building.html#custom-configuration).

**Hinweis:** Sobald Dokumente in eine Datensammlung hochgeladen werden, werden sie unter Verwendung der für diese Sammlung ausgewählten Konfigurationsdatei konvertiert und aufbereitet. Falls Sie später bei einer Sammlung zu einer anderen Konfigurationsdatei wechseln wollen, ist dies möglich. Die Dokumente, die bereits hochgeladen wurden, bleiben jedoch gemäß der ursprünglichen Konfigurationsdatei konvertiert. Alle Dokumente, die nach dem Wechsel der Konfigurationsdatei hochgeladen werden, verwenden die neue Konfigurationsdatei. Wenn Sie die neue Konfiguration für die **gesamte** Sammlung verwenden wollen, müssen Sie eine neue Sammlung erstellen, die neue Konfigurationsdatei auswählen und alle Dokumente erneut hochladen. Der {{site.data.keyword.discoveryshort}}-Service speichert den konvertierten Text der von Ihnen hochgeladenen Dokumente; eingebettete Images in **PDF**- und **Microsoft Word**-Dateien werden nicht gespeichert und nicht in Ergebnissen zurückgegeben.

### Standardkonfiguration
{: #the-default-configuration}

Der {{site.data.keyword.discoveryshort}}-Service beinhaltet eine Standardkonfigurationsdatei, die Ihre Daten konvertiert, aufbereitet und normalisiert, ohne dass Sie diese Optionen manuell konfigurieren müssen.

Diese Standardkonfigurationsdatei heißt **Standardkonfiguration**. Sie enthält Aufbereitungen sowie Standarddokumentkonvertierungen, die auf Schriftstilen und -größen basieren.

Zunächst nun einige Informationen zu den Standardaufbereitungen. {{site.data.keyword.discoveryshort}} bereitet das Textfeld Ihrer Dokumente mit semantischen Informationen auf (fügt dem Feld hierzu kognitive Metadaten hinzu), die durch vier {{site.data.keyword.watson}}-Aufbereitungen (Entitätsextraktion, Stimmungsanalyse, Kategorieklassifizierung und Konzepttagging) erfasst wurden (weitere Informationen zu diesen Aufbereitungen finden Sie [hier](/docs/services/discovery/building.html#adding-enrichments)).

**Hinweis:** Am **18. Juli 2017** wurde für {{site.data.keyword.discoveryfull}} eine neue Aufbereitungstechnologie namens {{site.data.keyword.nlushort}} (NLU) eingeführt. Details enthält der Abschnitt [Aufbereitungen hinzufügen](/docs/services/discovery/building.html#adding-enrichments). Falls Sie die **Standardkonfiguration** vor diesem Datum auf eine Sammlung angewendet haben, wurde diese Sammlung mit den {{site.data.keyword.alchemylanguageshort}}-Aufbereitungen aufbereitet. Falls Sie die **Standardkonfiguration** nach diesem Datum auf eine Sammlung angewendet haben, wurden die {{site.data.keyword.nlushort}}-Aufbereitungen verwendet.

-   [Microsoft Word-Konvertierung](/docs/services/discovery/building.html#microsoft-word-conversion)
-   [PDF-Konvertierung](/docs/services/discovery/building.html#pdf-conversion)
-   [HTML-Konvertierung](/docs/services/discovery/building.html#html-conversion)
-   [JSON-Konvertierung](/docs/services/discovery/building.html#json-conversion)

Wenn Sie eine angepasste Konfiguration erstellen möchten, finden Sie im Abschnitt [Angepasste Konfiguration](/docs/services/discovery/building.html#custom-configuration) entsprechende Informationen.

### Situationen, in denen eine angepasste Konfiguration erforderlich ist
{: #when-you-need-a-custom-configuration}

Die Zielsetzung des {{site.data.keyword.discoveryshort}}-Service ist das Abrufen der richtigen Informationen aus Ihrem Inhalt sowie deren Rückgabe an Ihre Benutzer. Die Konfiguration, die Sie zum Einpflegen des Inhalts verwenden, gibt an, um welche Informationen es sich hierbei handelt und wie sie in Ihrem Inhalt gespeichert sind. Die Inhaltstypen, die der {{site.data.keyword.discoveryshort}}-Service einpflegen kann, sind flexibel. Dies bedeutet, dass selbst bei Speicherung Ihres unstrukturierten Inhalts in einem bestimmten Format die Struktur dieses Inhalts nicht mit der Struktur von anderem Inhalt desselben Typs übereinstimmen muss.

-   **Ich habe verstanden, dass meine Dokumente unter Umständen nicht auf die von der Standardkonfiguration erwartete Weise strukturiert sind. *Wie kann ich ermitteln, ob die Standardeinstellungen in meinem Fall geeignet sind?***
    -   Ob die Standardeinstellung für Sie geeignet ist, können Sie am einfachsten dadurch ermitteln, dass Sie sie durch das [Hochladen von Beispieldokumenten](/docs/services/discovery/building.html#uploading-sample-documents) testen. Falls die JSON-Ergebnisse für das Beispiel Ihren Erwartungen entsprechen, ist keine zusätzliche Konfiguration erforderlich.
-   **Ich habe verstanden, dass Standardaufbereitungen zum Textfeld meiner Dokumente hinzugefügt werden. Kann ich zusätzliche Aufbereitungen zu anderen Feldern hinzufügen?**
    -   Natürlich. Sie können zusätzliche Aufbereitungen zu so vielen Feldern hinzufügen, wie Sie möchten. Details enthält der Abschnitt [Aufbereitungen hinzufügen](/docs/services/discovery/building.html#adding-enrichments). 

## Angepasste Konfiguration
{: #custom-configuration}

Um eine angepasste Konfiguration in den {{site.data.keyword.discoveryshort}}-Tools zu erstellen, öffnen Sie eine private Datensammlung und klicken Sie dann in der Anzeige **Daten verwalten** neben dem Namen Ihrer **Konfiguration** auf **Wechseln**. Klicken Sie im Dialogfeld **Konfiguration wechseln** auf **Neue Konfiguration erstellen**.

Nachdem Sie einen Namen für Ihre neue Konfigurationsdatei vergeben haben, wird der Name oben in der Konfigurationsanzeige angegeben. Diese neue Konfigurationsdatei enthält automatisch die Einstellungen und Aufbereitungen der [Standardkonfigurationsdatei](/docs/services/discovery/building.html#the-default-configuration), damit Sie eine Ausgangsbasis für Ihre Änderungen besitzen.

Die drei Schritte beim Anpassen einer Konfigurationsdatei sind das **Konvertieren**, das **Aufbereiten** und das **Normalisieren**.

1.  [Beispieldokumente konvertieren](/docs/services/discovery/building.html#converting-sample-documents)
1.  [Aufbereitungen hinzufügen](/docs/services/discovery/building.html#adding-enrichments)
1.  [Daten normalisieren](/docs/services/discovery/building.html#normalizing-data)

### Beispieldokumente hochladen
{: #uploading-sample-documents}

Um den Konfigurationsprozess effizienter zu machen, können Sie bis zu 10 Microsoft Word-, HTML-, JSON- oder PDF-Dateien hochladen, die für Ihre Dokumentgruppe repräsentativ sind. Diese Dateien werden **Beispieldokumente** genannt. Beispieldokumente werden nicht zu Ihrer Sammlung hinzugefügt, sondern lediglich zur Identifizierung der Felder, die Ihren Dokumenten gemein sind, und zum Anpassen dieser Felder an Ihre Anforderungen verwendet.

Beim Erstellen einer neuen Konfigurationsdatei mit den {{site.data.keyword.discoveryshort}}-Tools können Sie Beispieldokumente durch Ziehen und Ablegen oder durch Navigieren und Auswählen hochladen. Wenn Sie im Teilfenster **Beispieldokumente hochladen** auf einen Dateinamen klicken, wird eine Vorschau für die Datei angezeigt.

#### Denken Sie beim Hochladen von Beispieldokumenten an die folgenden Punkte:

-   Alle Ihre Dokumente werden vor der Aufbereitung und Indexierung in JSON konvertiert.
-   Microsoft Word- und PDF-Dokumente werden zunächst in HTML und dann in JSON konvertiert.
-   HTML-Dokumente werden direkt in JSON konvertiert.
-   Die maximale Dateigröße für ein Beispieldokument beträgt 5 MB. Beispieldokumente werden nach einem Monat automatisch gelöscht. Sie können die Beispieldokumente jedoch erneut hochladen, wenn Sie weitere Änderungen an Ihrer Konfiguration vornehmen möchten.

#### Richtlinien für die Auswahl geeigneter Beispieldokumente:

-   Sie sollten (mindestens) ein Beispieldokument für jeden Dateityp bereithalten, den Sie einpflegen wollen (Microsoft Word, PDF, HTML und JSON).
-   Falls eindeutige Dokumenttypen vorhanden sind (z. B. Rechnungsberichte oder Pressemitteilungen), beziehen Sie in Ihre Gruppe der Beispieldokumente ein Dokument des jeweiligen Typs ein.
-   Für HTML-Dokumente sollten Sie Dokumente auswählen, in denen HTML-Tags enthalten sind, die Sie ausschließen wollen, sowie Tagattribute, die Sie ein- oder ausschließen wollen.
-   JSON-Dokumente sollten alle Felder enthalten, die Sie entfernen oder zusammenführen wollen (z. B. 'zipCode' und 'postalCode').

### Beispieldokumente konvertieren
{: #converting-sample-documents}

Die Konvertierung Ihrer Beispieldokumente ist der Prozess, mit dem Sie definieren können, wie jeder Eingabetyp verarbeitet werden soll. Der Dateityp des von Ihnen hochgeladenen Inhalts gibt die Anzahl der Konvertierungsschritte vor, die Sie berücksichtigen müssen.

Zur Vorbereitung müssen Sie Ihre [Beispieldokumente hochladen](/docs/services/discovery/building.html#uploading-sample-documents) und im rechten Teilfenster ein Beispieldokument des Dateityps öffnen, den Sie konfigurieren wollen.

Klicken Sie zum Durcharbeiten der Konvertierungseinstellungen nacheinander auf die Dateitypen.

![Beispieldokument konvertieren](images/convert.png)

-   **Falls Sie Microsoft Word-Dateien konvertieren, müssen Sie Folgendes ausführen:**
    -   Konvertierungsoptionen für Microsoft Word festlegen
    -   Konvertierungsoptionen für HTML festlegen
    -   Konvertierungsoptionen für JSON festlegen
    -   Ergebnis prüfen

-   **Falls Sie PDF-Dateien konvertieren, müssen Sie Folgendes ausführen:**
    -   Konvertierungsoptionen für PDF festlegen
    -   Konvertierungsoptionen für HTML festlegen
    -   Konvertierungsoptionen für JSON festlegen
    -   Ergebnis prüfen

-   **Falls Sie HTML-Dateien konvertieren, müssen Sie Folgendes ausführen:**
    -   Konvertierungsoptionen für HTML festlegen
    -   Konvertierungsoptionen für JSON festlegen
    -   Ergebnis prüfen

-   **Falls Sie JSON-Dateien konvertieren**, müssen Sie die Konvertierungsoptionen für JSON festlegen und das Ergebnis prüfen.

Für jede Konfigurationsdatei, die Sie erstellen, gibt es bei jedem Schritt des Prozesses nur eine einzige Gruppe von Konvertierungsoptionen. Dies bedeutet, dass für PDF-Dateien, Word-Dateien und HTML-Dateien dieselben HTML-Konvertierungsoptionen verwendet werden. Falls Sie für jeden Inhaltstyp, den Sie einpflegen wollen, unterschiedliche Konvertierungsoptionen benötigen (oder falls für Dateien desselben Typs unterschiedliche Konvertierungstypen benötigt werden), müssen Sie Ihre Dateien in verschiedenen Sammlungen speichern und für jede Gruppe von Konvertierungseinstellungen separate Konfigurationsdateien erstellen.

#### Microsoft Word-Konvertierung
{: #microsoft-word-conversion}

Zur ordnungsgemäßen Konvertierung der Überschriften in Ihren Dokumenten in H1, H2 usw. werden die Schriftgrößen und Schriftstile von Microsoft Word verwendet. H1-Überschriften sind der Dokumenttitel; H2-Überschriften und alle ihnen untergeordneten Überschriften sind Unterüberschriften. Verwenden Sie die Textfelder und Optionsfelder, um die Standardeinstellungen bei Bedarf zu ändern. Sie können auch zusätzliche Überschriftsebenen und Word-Stile hinzufügen. Falls Ihre Word-Dokumente häufig eine bestimmte Schriftart oder einen bestimmten Stilnamen für Überschriften verwenden, achten Sie darauf, diese Informationen hinzuzufügen. Hierdurch wird die Konvertierung optimiert und Sie erzielen bessere Abfrageergebnisse.

**Beispiel:** Falls Ihre Word-Dokumente in der Regel für H2-Überschriften eine 20-Punkt-Kursivschrift verwenden, ändern Sie den **Schriftgrößenbereich** in **20** bis **23** und den **Schriftstil** in **Kursiv**.

Klicken Sie auf **Anwenden und speichern**, nachdem Sie Änderungen vorgenommen haben.

#### PDF-Konvertierung
{: #pdf-conversion}

Zur ordnungsgemäßen Konvertierung der Überschriften in Ihren Dokumenten in H1, H2 usw. werden die PDF-Schriftgrößen und Schriftartnamen verwendet. H1-Überschriften sind der Dokumenttitel; H2-Überschriften und alle ihnen untergeordneten Überschriften sind Unterüberschriften. Verwenden Sie die Textfelder und Optionsfelder, um die Standardeinstellungen bei Bedarf zu ändern. Sie können auch zusätzliche Überschriftsebenen hinzufügen. Falls Ihre PDF-Dokumente häufig eine bestimmte Schriftart für Überschriften verwenden, achten Sie darauf, diese Informationen hinzuzufügen. Hierdurch wird die Konvertierung optimiert und Sie erzielen bessere Abfrageergebnisse.

**Beispiel:** Falls Ihre PDF-Dokumente in der Regel für H1-Überschriften eine 20-Punkt-Fettschrift verwenden, ändern Sie den **Schriftgrößenbereich** in **20** bis **80** und den **Schriftstil** in **Fett**. Passen Sie die anderen Ebenen entsprechend an.

Klicken Sie auf **Anwenden und speichern**, nachdem Sie Änderungen vorgenommen haben.

#### HTML-Konvertierung
{: #html-conversion}

Mit diesem Schritt können Sie nicht benötigte Tags und andere Dokumentinformationen entfernen, damit ausschließlich diejenigen Informationen erhalten bleiben, die Sie für Ihre Abfragen benötigen.

HTML-Standardeinstellungen:

- Folgende Tags sowie deren Inhalt ausschließen: **`script`**, **`sup`**
- Folgende Tags ausschließen, aber Inhalt beibehalten: **`font`**, **`em`**, **`span`**
- Folgende Tagattribute beibehalten: Keine Standardeinstellung
- Folgende Tagattribute ausschließen: **`EVENT_ACTIONS`**
- Mit folgendem/n XPath-Code(s) übereinstimmenden Inhalt beibehalten: Keine Standardeinstellung
- Mit folgendem/n XPath-Code(s) übereinstimmenden Inhalt ausschließen: Keine Standardeinstellung

Klicken Sie auf **Anwenden und speichern**, nachdem Sie Änderungen vorgenommen haben.

#### JSON-Konvertierung
{: #json-conversion}

Mit dem letzten Schritt der Konvertierung wird sichergestellt, dass die konvertierten (oder hochgeladenen) JSON-Daten auf die erwartete Weise formatiert sind, bevor Aufbereitungen angewendet werden. Sie können Regeln erstellen, die {{site.data.keyword.watson}} zur Konvertierung von HTML in JSON verwendet.

-   Sie können Felder verschieben, zusammenführen, kopieren oder entfernen. Beispiel: Sie wollen die Felder **`zipCode`** und **`postalCode`** zusammenführen, weil es sich um ähnliche Begriffe für dasselbe Feld handelt.
-   Leere Felder (also Felder, die keine Informationen enthalten) werden standardmäßig gelöscht. Dies können Sie mit der Umschaltfunktion **Leere Felder entfernen** ändern.

Klicken Sie auf **Anwenden und speichern**, nachdem Sie Änderungen vorgenommen haben.

## Aufbereitungen hinzufügen
{: #adding-enrichments}

**Hinweis:** Am **18. Juli 2017** wurde für {{site.data.keyword.discoveryfull}} eine neue Aufbereitungstechnologie namens {{site.data.keyword.nlushort}} (NLU) eingeführt. Diese Aufbereitungen sind mit den bestehenden Aufbereitungen identisch, erfordern jedoch eine leicht abweichende Konfiguration und ein etwas anderes Schema. Die ursprünglichen Aufbereitungen (also {{site.data.keyword.alchemylanguageshort}}-Aufbereitungen) werden nicht mehr verwendet. Die Unterstützung für {{site.data.keyword.alchemylanguageshort}}-Aufbereitungen endet am **15. Januar 2018**. Neue Sammlungen sollten mit {{site.data.keyword.nlushort}} aufbereitet werden, bestehende Sammlungen mit möglichst zeitnah migrierten {{site.data.keyword.alchemylanguageshort}}-Konfigurationsdateien. Informationen zum Migrieren von Sammlungen und Konfigurationsdateien, die die {{site.data.keyword.alchemylanguageshort}}-Aufbereitungen verwenden, finden Sie unter [Aufbereitungen nach {{site.data.keyword.nlushort}} migrieren](/docs/services/discovery/migrate-nlu.html).

Die {{site.data.keyword.discoveryshort}}-[Standardkonfiguration](/docs/services/discovery/building.html#the-default-configuration) bereitet das Feld `text` Ihrer eingepflegten Dokumente mit semantischen Informationen auf (fügt dem Feld hierzu kognitive Metadaten hinzu), die durch die vier folgenden {{site.data.keyword.watson}}-Funktionen erfasst wurden: Entitätsextraktion, Stimmungsanalyse, Kategorieklassifizierung und Konzepttagging. (Insgesamt sind neun {{site.data.keyword.watson}}-Aufbereitungen verfügbar; die weiteren Aufbereitungen sind Schlüsselwortextraktion, Beziehungsextraktion, Emotionsanalyse, Elementklassifizierung und Semantikrollenextraktion.)

**Wichtig:** Nur die ersten 50.000 Zeichen jedes JSON-Feldes, das für die Aufbereitung ausgewählt ist, werden aufbereitet.

Sie können Ihre Dokumente zusätzlich erweitern, indem Sie weitere Aufbereitungen zum Feld `text` hinzufügen oder andere Felder aufbereiten. Hierzu müssen Sie mit den {{site.data.keyword.discoveryshort}}-Tools eine [angepasste Konfiguration erstellen](/docs/services/discovery/building.html#custom-configuration), das/die aufzubereitende(n) Feld(er) auswählen und eine Auswahl in der Liste der verfügbaren {{site.data.keyword.nlushort}}-Aufbereitungen treffen:

### Entitätsextraktion
{: #entity-extraction}

Gibt Elemente wie Personen, Orte und Organisationen zurück, die im Eingabetext vorhanden sind. Die Entitätsextraktion fügt semantisches Wissen zum Inhalt hinzu, mit dessen Hilfe das Subjekt und der Kontext des analysierten Textes ermittelt werden können. Die Verfahren für die Entitätsextraktion basieren auf hoch entwickelten Statistikalgorithmen und der Technologie zur Verarbeitung natürlicher Sprache und sind durch ihre Unterstützung von mehrsprachiger Analyse, kontextabhängiger Vereindeutigung und Zitatextraktion branchenweit singulär. Die vollständige Liste der Entitätstypen und Subtypen finden Sie [hier](/docs/services/discovery/entity-types.html). Sie können auch ein [angepasstes Entitätsmodell](/docs/services/discovery/building.html#custom-entity-model) mit {{site.data.keyword.knowledgestudiofull}} erstellen und hinzufügen.

Beispielabschnitt eines mit Entitätsextraktion aufbereiteten Dokuments:

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "entities": [
         {
           "count": 1,
           "sentiment": {
             "score": 0
           },
           "text": "Acme Corporation",
           "relevance": 0.98389,
           "type": "Company"
           },
           {
           "count": 1,
           "sentiment": {
             "score": 0
           },
           "text": "Atlanta",
           "relevance": 0.532754,
           "type": "Location",
           "disambiguation": {
             "subtype": [
               "AdministrativeDivision",
               "GovernmentalJurisdiction",
               "OlympicHostCity",
               "PlaceWithNeighborhoods",
               "City"
           ],
               "name": "Atlanta",
               "dbpedia_resource": "http://dbpedia.org/resource/Atlanta"
           }
           },
           {
           "count": 1,
           "sentiment": {
             "score": 0
           },
           "text": "Georgia",
           "relevance": 0.469643,
           "type": "Location",
           "disambiguation": {
             "subtype": [
               "StateOrCounty"
           ]
    }
  }
```
{: codeblock}

Im obigen Beispiel könnte der Entitätstyp durch Zugriff auf `enriched_text.entities.type` abgefragt werden.

Der Wert von `sentiment` (Stimmung) wird für Entitätstypen auch dann berechnet, falls die Aufbereitung für **sentiment** nicht ausgewählt ist. Weitere Informationen zur Stimmungsbewertung finden Sie unter [Stimmungsanalyse](/docs/services/discovery/building.html#sentiment-analysis).

Die Quote für die Relevanz (`relevance`) reicht von `0.0` bis `1.0`. Je höher die Quote, desto relevanter die Entität. Das Feld `disambiguation` enthält die Vereindeutigungsinformationen für die Entität. Hierzu gehören Informationen zum Subtyp der Entität (Feld `subtype`) und - sofern zutreffend - Links zu der/den Ressource(n). Das Feld `count` gibt an, wie häufig die Entität im Dokument erwähnt wird.

#### Angepasstes Entitätsmodell verwenden
{: #custom-entity-model}

Falls Sie ein angepasstes Aufbereitungsmodell erstellen möchten, können Sie hierzu {{site.data.keyword.knowledgestudiofull}} verwenden und das Modell in {{site.data.keyword.discoveryshort}} importieren, indem Sie die ID im Feld `ID des angepassten Modells` der {{site.data.keyword.discoveryshort}}-Tools hinzufügen. Weitere Informationen zur Integration mit {{site.data.keyword.knowledgestudiofull}} finden Sie unter [Integration mit {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery/integrate-wks.html#integrating-with-watson-knowledge-studio). Das angepasste {{site.data.keyword.knowledgestudiofull}}-Modell überschreibt die Standardaufbereitung mit Entitätsextraktion.

**Hinweis:** Einer Aufbereitung kann nur ein einziges {{site.data.keyword.knowledgestudiofull}}-Modell zugewiesen sein.

### Beziehungsextraktion
{: #relation-extraction}

Erkennt, ob zwei Entitäten miteinander in Beziehung stehen, und identifiziert den Typ der Beziehung. Sie können auch ein [angepasstes Beziehungsmodell](/docs/services/discovery/building.html#custom-relation-model) mit {{site.data.keyword.knowledgestudiofull}} erstellen und hinzufügen.

Die vollständige Liste der Beziehungstypen finden Sie [hier](/docs/services/discovery/relation-types.html).

Beispielabschnitt eines mit Beziehungsextraktion aufbereiteten Dokuments:

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
  "enriched_text": {
    "relations": [
      {
        "type": "locatedAt",
        "sentence": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
        "score": 0.989245,
        "arguments": [
         {
            "text": "Atlanta",
            "location": [
             94,
             101
            ],
            "entities": [
              {
                "type": "GeopoliticalEntity",
                "text": "Atlanta"
              }
            ]
         },
          {
            "text": "Georgia",
            "location": [
             103,
             110
            ],
            "entities": [
              {
                "type": "GeopoliticalEntity",
                "text": "Georgia"
              }
            ]
          }
        ]
      }
    ]
  }
}
```
{: codeblock}

Im obigen Beispiel könnte der Beziehungstyp durch Zugriff auf `enriched_text.relations.type` abgefragt werden.

Die zugehörigen Entitäten sind im Feld `arguments` aufgelistet. Die von der Beziehungsextraktion identifizierbaren Entitätstypen finden Sie [hier](/docs/services/discovery/relation-types.html#specific-entity-types).

Der Wert für `score` (Bewertung) reicht von `0.0` bis `1.0`. Je höher die Bewertung, desto relevanter die Beziehung. 

#### Angepasstes Beziehungsmodell verwenden
{: #custom-relation-model}

Falls Sie ein angepasstes Aufbereitungsmodell erstellen möchten, können Sie hierzu {{site.data.keyword.knowledgestudiofull}} verwenden und das Modell in {{site.data.keyword.discoveryshort}} importieren, indem Sie die ID im Feld `ID des angepassten Modells` der {{site.data.keyword.discoveryshort}}-Tools hinzufügen. Weitere Informationen zur Integration mit {{site.data.keyword.knowledgestudiofull}} finden Sie unter [Integration mit {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery/integrate-wks.html#integrating-with-watson-knowledge-studio). Das angepasste {{site.data.keyword.knowledgestudiofull}}-Modell überschreibt die Standardaufbereitung mit Beziehungsextraktion.

**Hinweis:** Einer Aufbereitung kann nur ein einziges {{site.data.keyword.knowledgestudiofull}}-Modell zugewiesen sein.

### Schlüsselwortextraktion
{: #keyword-extraction}

Extrahiert wichtige Themen in Ihrem Inhalt, die normalerweise bei der Datenindexierung, der Generierung von Tagwolken oder bei der Suche verwendet werden. Der {{site.data.keyword.discoveryshort}}-Service erkennt automatisch unterstützte Sprachen im eingegebenen Inhalt. Anschließend ermittelt er Schlüsselwörter in diesem Inhalt und erstellt für sie eine Rangfolge.

Beispielabschnitt eines mit Schlüsselwortextraktion aufbereiteten Dokuments:

```json
  {
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "keywords": [
        {
          "text": "Acme Corporation",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.985203
        },
        {
          "text": "new factory",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.821033
        },
        {
          "text": "stockholders",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.66497
        },
        {
          "text": "title",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.332438
        },
        {
          "text": "Atlanta",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.307723
        },
        {
          "text": "Georgia",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.306485
        }
      ]
    }
  }
```
{: codeblock}

Im obigen Beispiel könnte der Schlüsselworttext durch Zugriff auf `enriched_text.keywords.text` abgefragt werden.

Der Wert von `sentiment` (Stimmung) wird für Schlüsselwörter auch dann berechnet, falls die Aufbereitung für **sentiment** nicht ausgewählt ist. Weitere Informationen zur Stimmungsbewertung finden Sie unter [Stimmungsanalyse](/docs/services/discovery/building.html#sentiment-analysis).

Die Quote für die Relevanz (`relevance`) reicht von `0.0` bis `1.0`. Je höher die Quote, desto relevanter das Schlüsselwort.

### Kategorieklassifizierung

Kategorisiert Eingabetext, HTML oder webbasierten Inhalt in einer hierarchischen und bis zu fünf Ebenen umfassenden Taxonomie. Mithilfe von tieferen Ebenen können Sie Inhalt in präzisere und nützlichere Untersegmente klassifizieren. Die vollständige Liste der Kategorien finden Sie [hier](/docs/services/discovery/categories.html).

Beispielabschnitt eines mit Kategorieklassifizierung aufbereiteten Dokuments:

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "categories": [
        {
          "score": 0.361614,
          "label": "/business and industrial"
        },
        {
          "score": 0.329377,
          "label": "/business and industrial/company/merger and acquisition"
        },
        {
          "score": 0.154254,
          "label": "/business and industrial/business operations/business plans"
        }
      ]
```
{: codeblock}

Im obigen Beispiel könnte die Kategoriekennzeichnung durch Zugriff auf `enriched_text.categories.label` abgefragt werden.

Das Feld `label` gibt die erkannte Kategorie an. Die Hierarchieebenen sind durch Schrägstriche voneinander abgegrenzt. Die Bewertung (Feld `score`) für diese Kategorie reicht von `0.0` bis `1.0`. Je höher die Bewertung, desto größer die Konfidenz in dieser Kategorie.

### Konzepttagging
{: #concept-tagging}

Erkennt Konzepte, zu denen der Eingabetext gehört, auf der Basis anderer Konzepte und Entitäten, die in diesem Text vorhanden sind. Das Konzepttagging erkennt, wie Konzepte zueinander in Beziehung stehen, und ist in der Lage, Konzepte zu identifizieren, die im Text nicht direkt referenziert werden. Falls in einem Artikel beispielsweise die Begriffe 'CERN' und 'Higgs-Boson' erwähnt werden, erkennen die Funktionen der API für Konzepte selbst dann das neue Konzept 'Large Hadron Collider' (Großer Hadronen-Speicherring), wenn dieser Begriff auf der Seite nicht explizit erwähnt ist. Das Konzepttagging ermöglicht eine Analyse des Eingabeinhalts auf einer höheren Ebene als der reinen Schlüsselworterkennung.

Beispielabschnitt eines mit Konzepttagging aufbereiteten Dokuments:

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "concepts": [
        {
          "text": "Acme Corporation",
          "relevance": 0.91136,
          "dbpedia_resource": "http://dbpedia.org/resource/Acme_Corporation"
        },
        {
          "text": "Factory",
          "relevance": 0.886784,
          "dbpedia_resource": "http://dbpedia.org/resource/Factory"
        }
      ]
```
{: codeblock}

Im obigen Beispiel könnte der Konzepttexttyp durch Zugriff auf `enriched_text.concepts.text` abgefragt werden.

Die Quote für die Relevanz (`relevance`) reicht von `0.0` bis `1.0`. Je höher die Quote, desto relevanter das Konzept. Sofern zutreffend, werden Links zu der/den Ressource(n) bereitgestellt.

### Semantikrollenextraktion

Erkennt Subjekt-, Aktions- und Objektbeziehungen innerhalb von Sätzen im Eingabeinhalt. Mithilfe von Beziehungsinformationen können Kaufsignale, Schlüsselereignisse und andere wichtige Aktionen automatisch erkannt werden.

Beispielabschnitt eines mit Semantikrollenextraktion aufbereiteten Dokuments:

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
      "enriched_text": {
      "semantic_roles": [
        {
          "subject": {
            "text": "The stockholders",
            "keywords": [
              {
                "text": "stockholders"
              }
            ]
          },
          "sentence": " The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
          "object": {
            "text": "pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia",
            "keywords": [
              {
                "text": "Acme Corporation"
              },
              {
                "text": "new factory"
              },
              {
                "text": "Atlanta"
              },
              {
                "text": "Georgia"
              }
            ],
            "entities": [
              {
                "type": "Company",
                "text": "Acme Corporation"
              },
              {
                "type": "Location",
                "text": "Atlanta",
                "disambiguation": {
                  "subtype": [
                    "AdministrativeDivision",
                    "GovernmentalJurisdiction",
                    "OlympicHostCity",
                    "PlaceWithNeighborhoods",
                    "CityTown",
                    "City"
                  ],
                  "name": "Atlanta",
                  "dbpedia_resource": "http://dbpedia.org/resource/Atlanta"
                }
              },
              {
                "type": "Location",
                "text": "Georgia",
                "disambiguation": {
                  "subtype": [
                    "StateOrCounty"
                  ]
                }
              }
            ]
          },
          "action": {
            "verb": {
              "text": "be",
              "tense": "past"
            },
            "text": "were",
            "normalized": "be"
          }
        }
      ]
```
{: codeblock}

Im obigen Beispiel könnte der Text für das Subjekt der Beziehung durch Zugriff auf `enriched_text.relations.subject.text` abgefragt werden.

Der Wert von `sentiment` (Stimmung) wird für Beziehungen auch dann berechnet, falls die Aufbereitung für **sentiment** nicht ausgewählt ist. Weitere Informationen zur Stimmungsbewertung finden Sie unter [Stimmungsanalyse](/docs/services/discovery/building.html#sentiment-analysis). `Entitäten` oder `Schlüsselwörter` werden (wie im Beispiel gezeigt) nur dann extrahiert, wenn Sie die Aufbereitungen für **Entitäten** und **Schlüsselwörter** auswählen. Weitere Informationen zu diesen Aufbereitungen enthalten die Abschnitte [Entitätsextraktion](/docs/services/discovery/building.html#entity-extraction) und [Schlüsselwortextraktion](/docs/services/discovery/building.html#keyword-extraction).

Die Felder `subject`, `action` und `object` werden für jeden Satz extrahiert, der eine Beziehung enthält.

### Stimmungsanalyse
{: #sentiment-analysis}

Erkennt Grundhaltungen, Meinungen oder Emotionen im analysierten Inhalt. Der {{site.data.keyword.discoveryshort}}-Service kann die Gesamtstimmung innerhalb eines Dokuments, die Stimmung für benutzerdefinierte Ziele, die Stimmung auf Entitätsebene, die Stimmung auf Zitatebene, die Richtungsstimmung und die Stimmung auf Schlüsselwortebene berechnen. Die Kombination dieser Leistungsmerkmale unterstützt eine Vielzahl von Anwendungsfällen, die von der Überwachung sozialer Medien bis hin zur Trendanalyse reichen können.

Beispielabschnitt eines mit Stimmungsanalyse aufbereiteten Dokuments:

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "sentiment": {
        "document": {
        "score": 0.459813,
        "label": "positive"
  }
}
```
{: codeblock}

Im obigen Beispiel könnte die Stimmungskennzeichnung durch Zugriff auf `enriched_text.sentiment.document.label` abgefragt werden.

Das Feld `label` gibt die Gesamtstimmung des Dokuments an (`positive`, `negative` oder `neutral`). Der Wert von `label` für die Stimmung basiert auf der Bewertung (Feld `score`). Die Bewertung `0.0` gibt an, dass das Dokument `neutral` ist. Eine positive Zahl gibt an, dass das Dokument `positiv` ist, eine negative Zahl gibt an, dass das Dokument `negativ` ist.

### Emotionsanalyse
{: #emotion-analysis}

Erkennt Wut, Abscheu, Angst, Freude und Traurigkeit, die in einem Text in englischer Sprache zum Ausdruck kommt. Die Emotionsanalyse kann Emotionen erkennen, die zielgruppenspezifischen Ausdrücken, Entitäten oder Schlüsselwörtern zugeordnet sind. Sie kann auch die generelle emotionale Tendenz des Inhalts analysieren.

Beispielabschnitt eines mit Emotionsanalyse aufbereiteten Dokuments:

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "emotion": {
        "document": {
          "emotion": {
          "disgust": 0.102578,
          "joy": 0.626655,
          "anger": 0.02303,
          "fear": 0.018884,
          "sadness": 0.096802
    }
  }
}
```
{: codeblock}

Im obigen Beispiel könnte die Emotion `joy` (Freude) durch Zugriff auf `enriched_text.emotion.document.emotion.joy` abgefragt werden.

Die Emotionsanalyse analysiert den Text und berechnet für die Emotionen 'anger' (Wut), 'disgust' (Abscheu), 'fear' (Angst), 'joy' (Freude) und 'sadness' (Traurigkeit) eine Bewertung, die sich auf einer Skala von `0.0` bis `1.0` befindet. Ist die Bewertung für eine Emotion `0.5` oder höher, wurde diese Emotion erkannt (je höher die Bewertung über `0.5` liegt, desto höher ist die Relevanz). Im gezeigten Snippet hat `joy` eine Bewertung von über 0.5; {{site.data.keyword.watson}} hat also Freude erkannt.

**Hinweis:** Die Emotionsanalyse wird nur in Englisch unterstützt.

### Elementklassifizierung
{: #elements}

Analysiert Elemente (Sätze, Listen, Tabellen) in behördlichen Dokumenten, um wichtige Typen und Kategorien zu klassifizieren. Weitere Informationen finden Sie unter [Elementklassifizierung](/docs/services/discovery/element-classification.html).

#### Preisstruktur bei der Aufbereitung
{: #enrichment-pricing}

Preisinformationen für die Aufbereitung sind unter [{{site.data.keyword.Bluemix_notm}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window} verfügbar.

#### Sprachunterstützung für die Aufbereitung
{: #enrichment-language-support}

Informationen zur Sprachunterstützung für die Aufbereitung enthält der Abschnitt [Sprachunterstützung bei {{site.data.keyword.discoveryshort}}](/docs/services/discovery/language-support.html).

### Unterschiede zwischen Entitäten, Konzepten und Schlüsselwörtern
{: #udbeck}

Auf den ersten Blick scheint es sich bei der **Entitätsextraktion**, dem **Konzepttagging** und der **Schlüsselwortextraktion** um ähnliche Aufbereitungen zu handeln. Die Unterschiede zwischen diesen Aufbereitungen sollen daher jetzt am Text aus den Aufbereitungsbeispielen veranschaulicht werden.

```json
"text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia."
```
{: codeblock}

Da die Aufbereitung mit **Entitätsextraktion** Personen, Orte und Organisationen im Eingabetext extrahiert, gibt die **Entitätsextraktion** die folgenden Entitätstypen zurück:

```json
"type": "City"
"text": "Atlanta"

"type": "Company"
"text": "Acme"

"type": "StateOrCounty"
"text": "Georgia"
```
{: codeblock}

Da die Aufbereitung mit **Konzepttagging** erkennt, wie Konzepte zueinander in Beziehung stehen, kann sie Konzepte identifizieren, die im Text nicht direkt referenziert werden. Falls in einem Artikel beispielsweise die Begriffe 'CERN' und 'Higgs-Boson' erwähnt werden, erkennt sie selbst dann das Konzept 'Large Hadron Collider' (Großer Hadronen-Speicherring), wenn dieser Begriff nicht explizit erwähnt ist. Da unser Beispieldokumenttext nur einen einzigen Satz umfasst, gibt es keine zugehörigen Konzepte, weshalb das **Konzepttagging** die folgenden Konzepte zurückgibt:

```json
"text": "Acme Corporation"
"text": "factory"
```
{: codeblock}

Da die Aufbereitung mit **Schlüsselwortextraktion** Inhalt erkennt, der normalerweise bei der Datenindexierung, der Generierung von Tagwolken oder bei der Suche verwendet wird, gibt die **Schlüsselwortextraktion** die folgenden Schlüsselwörter zurück:

```json
"text": "Acme Corporation"
"text": "new factory"
"text": "stockholders"
"text": "Atlanta"
"text": "Georgia"
```
{: codeblock}

Durch eine Kombination dieser Aufbereitungen können Sie bessere Abfragen erstellen.

## Daten normalisieren
{: #normalizing-data}

Im letzten Schritt zur Anpassung Ihrer Konfigurationsdatei wird eine abschließende Bereinigung durchgeführt, die auch als 'Normalisierung' bezeichnet wird.

Im Abschnitt **Normalisieren** der {{site.data.keyword.discoveryshort}}-Tools können Sie Folgendes ausführen:

-   Sie können Felder verschieben, zusammenführen, kopieren oder entfernen. 
-   Leere Felder (also Felder, die keine Informationen enthalten) werden standardmäßig gelöscht. Dies können Sie mit der Umschaltfunktion **Leere Felder entfernen** ändern.

Klicken Sie auf **Anwenden und speichern**, nachdem Sie Änderungen vorgenommen haben, und dann auf **Fertig**. Sie werden daraufhin zur Anzeige **Daten verwalten** zurückgeführt, in der Sie diese Konfiguration auf die gewünschte Sammlung anwenden können.

## Entitäten normalisieren
{: #normalizing-entities}

### Felder mittels CSS-Selektoren extrahieren
{: #using-css}

Durch eine Verwendung von CSS-Selektoren können Sie über die Discovery-API eine zusätzliche Normalisierung durchführen.

Falls Sie korrekt formatiertes HTML einpflegen, können Sie es normalisieren, mit CSS-Selektoren JSON-Felder daraus extrahieren und anschließend Aufbereitungen auf die extrahierten Felder anwenden. Zur Aktivierung dieses Features müssen Sie Ihre Konfigurationsdatei bearbeiten. Geben Sie insbesondere ein Element `extracted_fields` für die Hierarchie `conversions/html` an. Geben Sie anschließend Feldnamen, CSS-Selektoren und Feldtypen wie folgt an:

```json
{
  "name": "JSON-Konfiguration extrahieren",
  "description": "Neue Konfiguration zur Extraktion von JSON-Feldern aus HTML",
  "conversions": {
    ...
    "html": {
      ...
      "extracted_fields": {
        "{feldname_1}": {
          "css_selector": "{css-selektorausdruck_1}",
          "type": "{feldtyp}"
        },
        ...
        "{feldname_N}": {
          "css_selector": "{css-selektorausdruck_N}",
          "type": "{feldtyp}"
        }
      }
    ...
    }
  }
}
```
{: codeblock}

Geben Sie die Werte für die neuen Felder wie folgt an:

-   `feldname`: Der Name des Feldes, das zur JSON-Ausgabe hinzugefügt wird.
-   `css-selektorausdruck`: Der CSS-Selektor, der für die HTML-Eingabe ausgeführt werden soll, um die Felder zu extrahieren. Für den Ausdruck kann es eine oder mehrere Übereinstimmungen geben.

    Gültige CSS-Selektoren sind im [JSoup-Parser ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://jsoup.org/apidocs/org/jsoup/select/Selector.html){: new_window} und seiner [Selektorsyntax ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://jsoup.org/cookbook/extracting-data/selector-syntax){: new_window} angegeben. Eine kurze Liste finden Sie unter [Gängige Selektoren](/docs/services/discovery/building.html#common-selectors).
-   `feldtyp`: Entweder `array` oder `string`. Falls der Feldtyp nicht angegeben ist, wird standardmäßig `array` verwendet. Bitte beachten Sie, dass beim Typ `string` eine Aufbereitung möglich ist, die Informationen in einem Feld des Typs `array` jedoch nur dann aufbereitet werden können, wenn zuvor die Elemente des Arrays in Felder extrahiert wurden.

**Achtung:** Falls ein CSS-Selektor sowohl mit einem übergeordneten Knoten als auch mit einem oder mehreren seiner untergeordneten Elemente übereinstimmt, wird der Textinhalt der Knoten in der JSON-Ausgabe dupliziert.

**Hinweis:** Feldnamen müssen die Rahmenbedingung erfüllen, die im Abschnitt [Anforderungen für Feldnamen](/docs/services/discovery/custom-config.html#field_reqs) definiert sind.

Die folgende JSON-Passage zeigt den relevanten Abschnitt der Standardkonfiguration, zu dem Sie CSS-Selektorinformationen hinzufügen.

```json
{
  "name": "Default Configuration",
  "description": "The configuration used by default when creating a new collection without specifying a configuration_id.",
  "conversions": {
    ...
    "html": {
      "exclude_tags_completely": [
        "script",
        "sup"
      ],
      "exclude_tags_keep_content": [
        "font",
        "em",
        "span"
      ],
      "exclude_content": {
        "xpaths": []
      },
      "keep_content": {
        "xpaths": []
      },
      "exclude_tag_attributes": [
        "EVENT_ACTIONS"
      ]
    }
    ...
  }
}
```
{: codeblock}

Die folgende Passage zeigt die Konfiguration mit einem neuen Namen und einer neuen Beschreibung sowie der Position, an der Sie Selektoren angeben können.

```json
{
  "name": "Extract JSON config",
  "description": "New configuration enabling extraction of JSON fields from HTML",
  "conversions": {
    ...
    "html": {
      "exclude_tags_completely": [
        "script",
        "sup"
      ],
      "exclude_tags_keep_content": [
        "font",
        "em",
        "span"
      ],
      "exclude_content": {
        "xpaths": []
      },
      "keep_content": {
        "xpaths": []
      },
      "exclude_tag_attributes": [
        "EVENT_ACTIONS"
      ],
      "extracted_fields": {
        "{feldname_1}": {
          "css_selector": "{css-selektorausdruck_1}",
          "type": "{feldtyp}"
        },
        ...
        "{feldname_N}": {
          "css_selector": "{css-selektorausdruck_N}",
          "type": "{feldtyp}"
        }
      }
    }
  }
  ...
}
```
{: codeblock}

Die folgende Passage schließlich zeigt die Konfiguration mit dem neuen Namen und der neuen Beschreibung sowie einigen CSS-Selektoren. Die Selektoren stimmen mit Elementen in einem HTML-Beispiel überein, das später in diesem Abschnitt noch beschrieben wird.

```json
{
  "name": "Extract JSON config",
  "description": "New configuration enabling extraction of JSON fields from HTML",
  "conversions": {
    ...
    "html": {
      "exclude_tags_completely": [
        "script",
        "sup"
      ],
      "exclude_tags_keep_content": [
        "font",
        "em",
        "span"
      ],
      "exclude_content": {
        "xpaths": []
      },
      "keep_content": {
        "xpaths": []
      },
      "exclude_tag_attributes": [
        "EVENT_ACTIONS"
      ],
      "extracted_fields": {
        "chapters": {
          "css_selector": ".chapter",
          "type": "array"
        },
        "authors": {
          "css_selector": ".author"
        },
        "authors_str": {
          "css_selector": ".author",
          "type": "string"
        },
        "comments": {
          "css_selector": "[^comments-content]"
        }
      }
    }
  }
  ...
}
```
{: codeblock}

Falls Sie das folgende HTML-Dokument in eine Sammlung hochladen, die eine aktualisierte Konfiguration verwendet, stimmen die CSS-Selektoren mit den entsprechenden Attributen und Werten im HTML-Dokument überein.

```html
<html>
  <body>
    <div id="authors">
      <div class="author"><span class="first_name">Jane</span> <span class="last_name">Rain</span></div>
      <div class="author">Joe Snow</div>
  </div>
  <div class="chapter"><h1>The Rain in Spain</h1><p>falls mainly on the plain.</p></div>
  <div class="chapter"><h1>How I Learned to Stop Worrying</h1><p>and love my snowblower.</p></div>
  <span id="comments-section">
    <h4>Comments:</h4>
    <span id="comments-content-1">Rain gives me pain.</span>
    <span id="comments-content-2">All snow must go!</span>
  </span>
</body></html>
```
{: codeblock}

Nachdem das obige HTML-Dokument eingepflegt und erweitert wurde, gibt der {{site.data.keyword.discoveryshort}}-Service die folgende JSON-Ausgabe zurück:

```json
{
  "extracted_metadata": { ... },
  "html": "...",
  "text": "...",
  "extracted_fields": {
    "authors": [ "Jane Rain", "Joe Snow" ],
    "authors_str": "Jane Rain\n\nJoe Snow",
    "chapters": [ "The Rain in Spain\n\nfalls mainly on the plain.", "How I Learned to Stop Worrying\n\nand love my snowblower." ],
    "comments": [ "Rain gives me pain.", "All snow must go!" ]
  }
}
```
{: codeblock}

Nachdem Sie festgelegt haben, welche HTML-Elemente extrahiert werden sollen, können Sie die Konfigurationsdatei weiter ändern und die Aufbereitungen angeben, die auf die Elemente angewendet werden sollen.

#### Gängige Selektoren

Nachfolgend sind einige häufig verwendet Selektoren aufgelistet:

  - `tag`: Gleicht den Namen von `tag` ab.
  - `.class`: Gleicht den Wert von `class` ab.
  - `#id`: Gleicht den Wert von `id` ab.
  - `[attribut]`: Gleicht einen beliebigen Tag mit dem angegebenen `Attribut` ungeachtet des Wertes ab.
  - `[attribut=wert]` oder `[attribut="wert"]`: Gleicht das angegebene `Attribut` und den angegebenen `Wert` ab.

## Dokumente mittels Dokumentsegmentierung teilen
{: #doc-segmentation}

Sie können Word-, PDF- und HTML-Dokumente basierend auf HTML-Überschriftentags in Segmente teilen. Nachdem ein Dokument geteilt wurde, wird jedes Segment als separates Dokument behandelt, das in JSON konvertiert und danach separat indexiert und aufbereitet wird. Da diese Segmente von Abfragen als separate Dokumente zurückgegeben werden, können Sie mit der Dokumentsegmentierung Folgendes erreichen:

  - Sie können Aggregationen für einzelne Segmente eines Dokuments durchführen. Eine Aggregation könnte beispielsweise jede Erwähnung einer bestimmten Entität in einem Segment zählen, statt dies lediglich für das gesamte Dokument vorzunehmen.
  - Sie können ein Relevanztraining für Segmente anstelle von Dokumenten durchführen, was die Neueinstufung des Ergebnisses verbessert.

Die Segmente werden erstellt, wenn die Dokumente in HTML konvertiert werden (Word- und PDF-Dokumente werden in HTML konvertiert, bevor die Konvertierung in JSON stattfindet). Dokumente können auf Grundlage der HTML-Tags `h1`, `h2`, `h3`, `h4`, `h5` und `h6` geteilt werden.

Hinweise:

  - Die Anzahl der Segmente pro Dokument ist auf `50` begrenzt. Der gesamte verbleibende Dokumentinhalt nach dem Erreichen von `49` Segmenten wird im Segment `50` gespeichert.

  - Jedes Segment wird bei der Zählung für den Dokumentgrenzwert Ihres Plans berücksichtigt.

  - Wenn Sie die Dokumentsegmentierung verwenden, können Sie weder Daten normalisieren (siehe [Daten normalisieren](/docs/services/discovery/building.html#normalizing-data)) noch Felder mithilfe von CSS-Selektoren extrahieren (siehe [Felder mittels CSS-Selektoren extrahieren](/docs/services/discovery/building.html#using-css)).

  - Falls ein Dokument aktualisiert wurde und erneut eingepflegt werden muss, sind gelöschte Segmente nach dem erneuten Einpflegen weiterhin vorhanden und müssen mithilfe der API (siehe [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/watson/developercloud/discovery/api/v1/?curl#delete-doc){: new_window}) manuell gelöscht werden. Außerdem wird jedem Abschnitt eine neue Dokument-ID (`document_id`) zugeordnet, falls bei der Dokumentaktualisierung Inhalt hinzugefügt wurde, der neue Segmente erstellt, oder Inhalt gelöscht wurde, der Segmente entfernt. Falls für diese Segmente bereits durch ein Relevanztraining eine Einstufung vorgenommen wurde, muss das Training erneut durchgeführt werden. In diesem Fall kann es sinnvoller sein, ein neues Dokument zu erstellen, das den neuen Inhalt enthält, und es separat einzupflegen, statt Inhalt zu einem bestehenden Dokument hinzuzufügen. Löschen Sie solche Segmente mithilfe der API, statt sie aus einem bestehenden Dokument zu löschen und erneut einzupflegen.

  - Dokumente werden bei jeder Erkennung des angegebenen HTML-Tags segmentiert. Die Segmentierung kann infolgedessen zu einem fehlerhaften HTML-Dokument führen, weil es sein könnte, dass die Dokumente vor Endtags und nach Anfangstags geteilt werden.

  - HTML-, PDF- und Word-Metadaten werden nicht extrahiert und nicht in den Index einbezogen. Auch angepasste Metadaten, die durch den Dokumentupload übergeben werden, werden nicht in den Index einbezogen.

### Segmentierung durchführen
{: #performing-segmentation}

Die Segmentierung wird über die API im Abschnitt `conversions` konfiguriert.

```json
{
  "configuration_id": "a23c467d-1212-4b3a-5555-93e788a3622a",
  "name": "Example configuration",
  "conversions": {
    "segment": {
      "enabled": true,
      "selector_tags": ["h1", "h2", "h3", "h4", "h5", "h6"]
    }
  }
}
```
{: codeblock}

Die Einstellung `enabled` = `true` aktiviert die Dokumentsegmentierung.

Der Wert für `selector_tags` ist ein Array, das die Überschriftentags angibt, nach denen Dokumente segmentiert werden können.

#### Beispiel

Konfiguration:

```json
"conversions": {
  "segment": {
    "enabled": true,
    "selector_tags": ["h1", "h2"]
```
{: codeblock}

Ursprüngliches HTML-Dokument:

```
<html>
 <head>
 </head>
 <body>
  first line
   <div name="section 1">
    <h1>heading 1</h1>
     <div name="section 2">This is the text that falls under <b>heading 1</b> and should be therefore split into its own segment.
      <h2>heading 2</h2>
      line under heading 2
     </div>
       <h3>heading 3</h3>
       line under heading 3
   </div>
  last line
 </body>
</html>
```
{: codeblock}

Das erste Dokumentsegment sieht wie folgt aus:

```json
{
  "id": "94c686c3-a790-4d8d-ba42-2bddf01b311c",
  "segment_metadata": {
    "parent_id": "94c686c3-a790-4d8d-ba42-2bddf01b311c",
    "segment": 1,
    "total_segments": 3
  },
  "extracted_metadata": {
    "title": "Heading 1",
    "sha1": "45ede479df67d78f2205ea7e714843375d3029c0",
    "filename": "doc-with-different-heading-levels.html",
    "file_type": "html"
  },
  "text": "This is the text that falls under heading 1 and should be therefore split into its own segment.",
  "html": "<div name=\"section 2\">This is the text that falls under <b>heading 1</b> and should be therefore split into its own segment."
}
```
{: codeblock}

Alle Segmente enthalten Folgendes:

  - `id`: Die `ID` dieses Segments.
  - Abschnitt `segment_metadata` mit folgendem Inhalt:
    - `parent_id`: Die `übergeordnete ID` ist die ID des Originaldokuments. Beim ersten Segment sind die Werte für `id` und `parent_id` identisch.
    - `segment`: Die Nummer dieses Segments.
    - `total_segments`: Die Gesamtzahl der Segmente, in die das Dokument aufgeteilt wurde.
  - Abschnitt `extracted_metadata` mit folgendem Inhalt:
    - `title`: Das Feld `title` wird aus dem Inhalt des Überschriftentags in diesem Segment extrahiert (z. B. `Chapter 1`). Falls das erste Segment keinen Überschriftentag enthält, wird für `title` der Wert `no-title` angegeben.
    - `sha1`: Entspricht dem Originaldokument.
    - `filename`: Entspricht dem Originaldokument.
    - `file_type`: Entspricht dem Originaldokument.
  - Feld `text`
  - Feld `html`
