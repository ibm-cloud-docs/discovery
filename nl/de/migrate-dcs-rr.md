---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-03"

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


# Von Watson Document Conversion und Retrieve and Rank migrieren
{: #migrate-dcs-rr}

{{site.data.keyword.documentconversionfull}} und {{site.data.keyword.retrieveandrankfull}} werden nicht mehr unterstützt und wurden durch {{site.data.keyword.discoveryfull}} ersetzt. Normalerweise werden diese beiden Services zusammen eingesetzt, um Daten einzupflegen sowie einzustufen sowie anschließend Ergebnisse an Ihre Anwendungen zu liefern. Dieses Dokument führt Sie durch die Migration von {{site.data.keyword.documentconversionshort}} und {{site.data.keyword.retrieveandrankshort}} auf {{site.data.keyword.discoveryshort}}.

{{site.data.keyword.discoveryfull}} bietet eine leistungsfähigere Abfrageschnittstelle, eine vereinfachte Dateneinpflegung, ein verbessertes Trainingsmanagement sowie eine größere Skalierung. {{site.data.keyword.discoveryshort}} deckt viele der Hauptanwendungsfälle wie {{site.data.keyword.retrieveandrankshort}} ab, zu denen die Agentenunterstützung, die Suche in unternehmenseigenen Wissensdatenbanken und die Recherchenunterstützung gehören. Bei der Konzeption wurden viele Herausforderungen bedacht, die sich für Benutzer von {{site.data.keyword.retrieveandrankshort}} ergaben, und viele dieser Probleme gelöst. {{site.data.keyword.discoveryshort}} bietet außerdem neue Funktionen für den Informationsabruf, die in {{site.data.keyword.retrieveandrankshort}} nicht verfügbar waren, beispielsweise der Passagenabruf und verbesserte Suchalgorithmen zur Ermittlung relevanterer Ergebnisse.

**Featurevergleich**

| Feature | {{site.data.keyword.retrieveandrankshort}} | {{site.data.keyword.discoveryshort}} |
|:-------------|:--------------------:|:-------------:|
| Suche in natürlicher Sprache | Ja | Ja |
| Relevanztraining durch maschinelles Lernen | Ja | Ja |
| Benutzerschnittstellentools für Training | Ja | Ja |
| JSON-Antworteinheiteneingabe | Ja | Ja |
| Dokumentaufteilung | Ja | Ja |
| Passagenabruf |   | Ja |
| CRUD für Dokumente | Ja | Ja |
| JSON-Upload im Stapelbetrieb | Ja |   |
| Automatische NLP-Dokumentaufbereitung |   | Ja |
| Integration von angepassten NLP-Modellen für Aufbereitung |   | Ja |
| Trainingsdatenspeicherung im Service |   | Ja |
| Automatisiertes Modelllebensyklusmanagement |   | Ja |
| Semantische Ähnlichkeit zur Relevanzverbesserung ohne Training |   | Ja |
| Genauigkeitsmessung in Tools basierend auf Testset | Ja |   |
| Angepasste Featurevektorunterstützung | Ja |   |
| Angepasste Analysefunktionskonfiguration | Ja | Vorkonfiguriert |
| Angepasste Stoppwörter | Ja | Vorkonfiguriert |
| Angepasste Sprachwörterbücher | Ja | Vorkonfiguriert |
| Angepasste Synonyme | Ja | Ja |
**Hinweis:** Diese Tabelle wird aktualisiert, sobald neue {{site.data.keyword.discoveryshort}}-Funktionalitäten hinzugefügt werden.

Bevor Sie mit der Migration beginnen, müssen Sie zunächst die Daten [evaluieren](#evaluate), die in Ihrem {{site.data.keyword.retrieveandrankshort}}-Service gespeichert sind, und sich darüber informieren, wie Sie die verschiedenen Komponenten umstellen, aus denen Ihre Lösung besteht.

Viele Kunden verwenden {{site.data.keyword.documentconversionshort}} in Kombination mit {{site.data.keyword.retrieveandrankshort}}. Falls Sie {{site.data.keyword.documentconversionshort}} nicht zum Konvertieren von Inhalt verwendet, damit er in einem durchsuchbaren Index gespeichert werden kann, fahren Sie mit der Prüfung der [Migrationsoptionen für eigenständige {{site.data.keyword.documentconversionshort}}-Instanzen](#dcs) fort.

Falls Sie anfangs das Lernprogramm für {{site.data.keyword.retrieveandrankshort}} verwendet haben und Ihre eigene Instanz auf dem Service in diesem Lernprogramm basiert, finden Sie [hier](/docs/services/discovery/migrate-rnr-tut.html) eine Erweiterung des Lernprogramms, mit der dieselben Daten in {{site.data.keyword.discoveryshort}} eingepflegt werden.

**Hinweis:** Die Konvertierungs- und Aufbereitungsfunktionalität ist in {{site.data.keyword.discoveryshort}} enthalten. Falls Sie {{site.data.keyword.documentconversionshort}} und/oder {{site.data.keyword.nlushort}} verwendet haben, um HTML-, PDF- oder Microsoft Word-Quellendokumente zu konvertieren und aufzubereiten, werden diese Services durch Features im {{site.data.keyword.discoveryshort}}-Service ersetzt.

## Pfad der Migration auf Watson Discovery-Service bewerten
{: #evaluate}

Zur Migration von {{site.data.keyword.retrieveandrankshort}} gibt es zwei praktische Möglichkeiten, denn Sie können die Migration entweder ausgehend vom Quelleninhalt oder ausgehend vom indexierten Inhalt vornehmen. Bewerten Sie beide Optionen, bevor Sie sich für die zu verwendende Option entscheiden.

### Aus Quelleninhalt migrieren
{: #source}

Eine vom Quelleninhalt ausgehende Migration setzt Folgendes voraus:

-  Sie müssen auf die ursprünglichen Dateien zugreifen können, aus denen der Inhalt eingepflegt wurde.
-  Sie müssen die ID für jedes Dokument programmgestützt extrahieren (das Ergebnis besitzt bereits eine ID, bevor es indexiert wird).

Falls Sie alle Migrationsbedingungen erfüllen, empfiehlt sich die Verwendung dieses Verfahrens für die Umstellung auf den {{site.data.keyword.discoveryshort}}-Service.

Zur Migration des Quelleninhalts ändern Sie die im [Migrationslernprogramm](/docs/services/discovery/migrate-rnr-tut.html) beschriebene Prozedur so, dass die Spezifikationen Ihrer Quellendaten erfüllt werden.

#### Antworteinheiten migrieren

Falls Sie mit {{site.data.keyword.documentconversionshort}} Antworteinheiten erstellt haben, verwenden Sie zur Migration dieses Inhalts eine der folgenden Optionen:

-  Falls Sie eine Einstufungskomponente trainiert haben und die Einstufung migrieren müssen, sollten Sie den von {{site.data.keyword.documentconversionshort}} zurückgegebenen Inhalt in {{site.data.keyword.discoveryshort}} einpflegen.
-  Falls keine Trainingsdaten migriert werden müssen, pflegen Sie die Originalquellendokumente in {{site.data.keyword.discoveryshort}} mit dem [Feature für die Dokumentsegmentierung](/docs/services/discovery/building.html#doc-segmentation) ein.

### Aus indexiertem Inhalt migrieren
{: #indexed}

Sie sollten die Migration ausgehend vom indexierten Inhalt in {{site.data.keyword.retrieveandrankshort}} ausführen, falls Sie nicht auf die Originalquellendokumente zugreifen können oder Folgendes zutrifft:

- Sie haben die automatische Generierung von Dokument-IDs verwendet und eine Einstufungskomponente trainiert.
- Sie haben Antworteinheiten in {{site.data.keyword.documentconversionshort}} erstellt und sie eingestuft, jedoch nicht die vom {{site.data.keyword.documentconversionshort}}-Service generierten Antworteinheiten beibehalten.

**Hinweis:** Dieses Verfahren ist nur dann möglich, wenn sich der gesamte benötigte Inhalt in gespeicherten Feldern in {{site.data.keyword.retrieveandrankshort}} befindet. Falls der Inhalt lediglich indexiert, jedoch nicht gespeichert wurde, kann der Inhalt außerhalb des Service nicht abgefragt werden; die Daten müssen in diesem Fall erneut aus der Quelle konvertiert und aufgeteilt werden.

Dokumente werden aus dem Service mit der Methode [/v1/solr_clusters/{solr-cluster-id}/solr/\{sammlungsname\}/select ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/watson/developercloud/retrieve-and-rank/api/v1/#index_doc){: new_window} unter Verwendung einer leeren Abfrage `q=*:*` extrahiert. Die Anzahl der zurückgegebenen Dokumente kann größer als die maximale Rückgabeanzahl in der Praxis sein (bei den meisten Sammlungen `200`). Wenn dies der Fall ist, sollten mehrere Aufrufe mit einer entsprechenden [Seitenaufteilung ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://lucene.apache.org/solr/guide/6_6/pagination-of-results.html){: new_window} erfolgen, um alle Dokumente zu erfassen.

Dokumente mit angegebenen **IDs** werden in den {{site.data.keyword.discoveryshort}}-Service mit der Methode [/v1/environments/\{umgebungs-id\}/collections/\{sammlungs-id\}/documents/\{dokument-id\} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#update-doc){: new_window} hochgeladen. Jeder Dokumentupload ist ein separater API-Aufruf.

## Trainingsdaten migrieren

Nachdem Sie Ihre Ergebnisse migriert haben, müssen Sie als Nächstes alle Trainingsdaten migrieren, die für den Inhalt erstellt wurden. Zur Migration von Trainingsdaten gibt es zwei Möglichkeiten, nämlich die Migration aus der Quelle (`csv`) und die Migration aus dem Service. Falls Sie Trainingsdaten aus einer `CSV`-Datei hochgeladen haben und noch auf diese Datei zugreifen können, sollten Sie diese Quelle für die Migration verwenden. Falls Sie die {{site.data.keyword.retrieveandrankshort}}-Tools verwendet haben oder nicht mehr auf die ursprüngliche `CSV`-Datei zugreifen können, sollten Sie die Migration ausgehend vom Service durchführen.

### Trainingsdaten aus Quelleninhalt migrieren
{: #csv}

Eine vom Einstufungsquelleninhalt ausgehende Migration setzt Folgendes voraus:

- Sie müssen auf die ursprünglichen `CSV`-Quellendateien zugreifen können, mit denen die Trainingsinformationen ursprünglich hochgeladen wurden.
- Sie müssen sicherstellen, dass die IDs der trainierten Dokumente bei ihrer Indexierung mit den IDs der trainierten Dokumente bei ihrer Indexierung in {{site.data.keyword.retrieveandrankshort}} identisch sind.

Falls Sie alle Migrationsbedingungen erfüllen, empfiehlt sich die Verwendung dieses Verfahrens für die Umstellung des Trainings auf den {{site.data.keyword.discoveryshort}}-Service.

Zur Migration der Trainingsdaten ändern Sie die im [Migrationslernprogramm](/docs/services/discovery/migrate-rnr-tut.html) beschriebene Prozedur so, dass die Spezifikationen Ihrer Quellendaten erfüllt werden.

### Trainingsdaten aus dem Service migrieren
{: #extract-train}

Zur Migration von Trainingsdaten aus dem {{site.data.keyword.retrieveandrankshort}}-Service müssen Sie die Trainingsdaten mit den APIs von {{site.data.keyword.retrieveandrankshort}} extrahieren, die JSON-Ausgabe von {{site.data.keyword.retrieveandrankshort}} für das Training in ein Format konvertieren, das von {{site.data.keyword.discoveryshort}} verwendet werden kann, und zum Schluss die Trainingsdaten mithilfe der API in {{site.data.keyword.discoveryshort}} einpflegen.

Zum Extrahieren von Trainingsdaten aus {{site.data.keyword.retrieveandrankshort}} verwenden Sie die `Exportfunktion` in den Tools von {{site.data.keyword.retrieveandrankshort}}. Nachdem ein vollständiger Export erfolgreich heruntergeladen wurde, extrahieren Sie die gespeicherte Datei `.zip`. Das Archiv enthält zwei Dateien. Die Trainingsdaten sind in der Datei namens `export-questions.json` gespeichert. Diese Datei enthält ein Array von JSON-Trainingsobjekten.

Jedes Trainingsergebnis im Array wird im folgenden Format dargestellt:

**Beispiel für Trainingsdaten aus {{site.data.keyword.retrieveandrankshort}}**
```json
{
    "text":"Who was the first royal to attend Wimbledon?",
    "cluster":{
        "id":"f62c11d3-30fa-11e7-8a0c-333f7f431ce8",
        "answers":{
            "f62c11d3-30fa-11e7-8a0c-33":[
                {
                    "id":"dac41335-0e96-40c9-983f-cc3f1c395782",
                    "ranking":1,
                    "source":{
                        "id":"e26a3d20-30fa-11e7-aa5e-d1632b06e0b1",
                        "file":"wimbledon-wikipedia.html",
                        "sequence":17,
                        "strategy":"retrieve"
                    }
                },
                {
                    "id":"661b4c9f-ecdb-4dad-aafc-6ae561a148c0",
                    "ranking":2,
                    "source":{
                        "id":"da1bc620-30fa-11e7-8f90-3305f35a93c9",
                        "file":"generated-otherFactsFigures.docx",
                        "sequence":67,
                        "strategy":"retrieve"
                    }
                },
                {
                    "id":"0053fdb8-c77e-4fcf-b0e0-6a4cd377266a",
                    "ranking":3,
                    "source":{
                        "id":"d9c0add0-30fa-11e7-aa5e-d1632b06e0b1",
                        "file":"generated-allEngland.docx",
                        "sequence":20,
                        "strategy":"retrieve"
                    }
                },
                {
                    "id":"506d3d50-19ed-49c8-b32f-65f848e60e86",
                    "ranking":4,
                    "source":{
                        "id":"da1bc620-30fa-11e7-8f90-3305f35a93c9",
                        "file":"generated-otherFactsFigures.docx",
                        "sequence":63,
                        "strategy":"retrieve"
                    }
                }
            ]
        },
        "flags":{

        }
    }
},
```
{: codeblock}

{{site.data.keyword.discoveryshort}} benötigt nicht alle Informationen, die aus {{site.data.keyword.retrieveandrankshort}} exportiert wurden. Das folgende Snippet zeigt die erforderliche Struktur eines {{site.data.keyword.discoveryshort}}-Trainingseintrags:

```json
{
  "natural_language_query": "{abfrage_in_natürlicher_sprache}",
  "examples": [
    {
      "document_id": "{dokument-id_1}",
      "relevance": 0
    },
    {
      "document_id": "{dokument-id_2}",
      "relevance": 10
    }
  ]
}
```
{: codeblock}

An dieser Stelle müssen Sie Ihre Trainingsinformationen aus {{site.data.keyword.retrieveandrankshort}} in {{site.data.keyword.discoveryshort}}-Trainingsinformationen umsetzen. Berücksichtigen Sie bei der Konvertierung die folgenden Punkte.

- **Nicht relevant** wird durch die Relevanzquote `0` (Feld `relevance`) in {{site.data.keyword.discoveryshort}} angegeben, jedoch durch die Einstufung (Feld `ranking`) `1` in {{site.data.keyword.retrieveandrankshort}}. Alle Einträge `"ranking": 1` müssen daher in `"relevance": 0` in {{site.data.keyword.discoveryshort}} konvertiert werden.
- Die {{site.data.keyword.discoveryshort}}-Tools verwenden eine Binärskala von `0` und `10`. Falls Sie mehr Ergebnisse einstufen und die {{site.data.keyword.discoveryshort}}-Tools verwenden wollen, müssen Sie alle Einträge `"ranking": 1` und `"ranking": 2` in `"relevance": 0` sowie alle Einträge `"ranking": 3` und `"ranking": 4` in `"relevance": 10` konvertieren. Falls Sie keine zusätzlichen Ergebnisse einstufen wollen oder nicht die {{site.data.keyword.discoveryshort}}-Tools verwenden, ist dies nicht erforderlich.
- Nicht beantwortete Fragen werden von {{site.data.keyword.discoveryshort}} nicht benötigt; die Gültigkeit des Relevanztrainings wird manuell überprüft.

![Migrationsablauf für Einstufungen](images/migrate-ranking.png)

Die oben aufgeführten **Beispieltrainingsdaten von {{site.data.keyword.retrieveandrankshort}}** würden zur Verwendung in den {{site.data.keyword.discoveryshort}}-Tools folgendermaßen konvertiert werden:

```json
{
  "natural_language_query": "Who was the first royal to attend Wimbledon?",
  "examples": [
    {
      "document_id": "e26a3d20-30fa-11e7-aa5e-d1632b06e0b1",
      "relevance": 0
    },
    {
      "document_id": "da1bc620-30fa-11e7-8f90-3305f35a93c9",
      "relevance": 0
    },
    {
      "document_id": "d9c0add0-30fa-11e7-aa5e-d1632b06e0b1",
      "relevance": 10
    },
    {
      "document_id": "da1bc620-30fa-11e7-8f90-3305f35a93c9",
      "relevance": 10
    }
  ]
}
```
{: codeblock}

## Sprachunterstützung
{: #language}

Entsprechende Informationen können Sie der [Sprachunterstützungstabelle für {{site.data.keyword.discoveryshort}}](/docs/services/discovery/language-support.html) entnehmen. Features von {{site.data.keyword.retrieveandrankshort}} werden primär durch die **Basissprachunterstützung** von {{site.data.keyword.discoveryshort}} unterstützt.

## Abfragen migrieren
{: #queries}

Die {{site.data.keyword.discoveryfull}}-Abfragesprache unterscheidet sich von der durch {{site.data.keyword.retrieveandrankshort}} verwendeten Solr-Abfragesprache. Vorhandene Abfragen sollten in eine der {{site.data.keyword.discoveryfull}}-Abfragemethoden umgestellt und in die Verwendung der {{site.data.keyword.discoveryfull}}-Abfragesprache konvertiert werden. In der folgenden Tabelle sind einige typische Operatoren beschrieben, die bei den meisten Abfragen verwendet werden:

**Migration von Solr-Abfrage zu {{site.data.keyword.discoveryshort}} - Typische Operatoren**

| Solr-Operator | Discovery-Operator | Beschreibung |
|:-------------:|--------------------|-------------|
| `.` | `.` | JSON-Begrenzer |
| `:` | `:` | Enthält |
|  | `::` | Exakte Übereinstimmung |
| `-{feldname}:` | `:!` | Enthält nicht |
|  | `::!` | Keine exakte Übereinstimmung |
| ``\` | ``\` | Escapezeichen |
| `""` | `""` | Ausdrucksabfrage |
| `()` | `()`, `[]` | Verschachtelte Gruppierung |
| `OR` | [<code>&#124;</code>] | oder |
| `AND` | [,] | und |
| `[* TO 100]` | `<=`, `>=`, `>`, `<` | Numerische Vergleiche |
| `^x` | `^x` | Bewertungsmultiplikator |
| `*` | `*` | Platzhalter |
| `~`(0 to 1) | [~n] | Zeichenfolgenvariante |

Unter [Abfragekonzepte](/docs/services/discovery/using.html) und [Abfragereferenz](/docs/services/discovery/query-reference.html) finden Sie ausführliche Informationen zur {{site.data.keyword.discoveryfull}}-Abfragesprache.


## Eigenständigen Watson Document Conversion-Service migrieren
{: #dcs}

Falls Sie {{site.data.keyword.documentconversionshort}} verwenden, um das Einpflegen von Inhalt in {{site.data.keyword.retrieveandrankshort}} zu unterstützen, wurde diese Funktionalität zu einem einzigen Service weiterentwickelt: {{site.data.keyword.discoveryshort}}. Mit {{site.data.keyword.discoveryshort}} können Sie Microsoft Word-, PDF-, HTML- und JSON-Dokumente ohne großen Aufwand konvertieren, aufbereiten und in einen trainierbaren und durchsuchbaren Index einpflegen. Dieser Abschnitt ist für Sie relevant, wenn Ihr Anwendungsfall keine Speicherung des konvertierten Inhalts in einem Index einbezieht. Falls Sie Dokumente in einen Index einpflegen, lesen Sie den Abschnitt [Daten in den {{site.data.keyword.discoveryshort}}-Service einpflegen](/docs/services/discovery/building.html).

IBM stellt keinen Service mehr bereit, der für die eigenständige Konvertierung von Microsoft Word-, PDF- und HTML-Dokumenten geeignet ist. Falls Sie gegenwärtig den {{site.data.keyword.documentconversionshort}}-Service verwenden und die Ausgabe nicht in einen online indexierten Service (z. B. {{site.data.keyword.discoveryshort}}) einpflegen, empfiehlt es sich, die Migration auf eine Open-Source-Alternative wie [Apache Tika ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://tika.apache.org/){: new_window} in Erwägung zu ziehen.
