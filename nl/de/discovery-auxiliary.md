---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-31"

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

# Discovery-Archive

Dieser Abschnitt enthält Informationen zu {{site.data.keyword.discoveryshort}}-Features, die möglicherweise noch verfügbar sind, jedoch durch neuere Optionen ersetzt wurden.
{: tip}

## AlchemyLanguage-Aufbereitungen
{: #AlchemyLanguage-enrichments}

Am **18. Juli 2017** wurde für {{site.data.keyword.discoveryfull}} eine neue Aufbereitungstechnologie namens {{site.data.keyword.nlushort}} eingeführt. Diese Aufbereitungen sind mit den bestehenden Aufbereitungen identisch, erfordern jedoch eine leicht abweichende Konfiguration und ein etwas anderes Schema. Die ursprünglichen Aufbereitungen (also {{site.data.keyword.alchemylanguageshort}}-Aufbereitungen) werden ab dem **15. Januar 2018** nicht mehr verwendet und unterstützt.

Bei der API-Versionszeichenfolge `2017-10-16` wird das Hochladen neuer Dokumente in vorhandene Sammlungen, die mit {{site.data.keyword.alchemylanguageshort}} aufbereitet wurden, und das Erstellen neuer Sammlungen und deren Aufbereitung mit {{site.data.keyword.alchemylanguageshort}} nicht mehr unterstützt. Verwenden Sie eine frühere API-Versionszeichenfolge, wenn Sie {{site.data.keyword.alchemylanguageshort}} weiterhin verwenden wollen, bis die Unterstützung am **15. Januar 2018** endet.

Bestehende Sammlungen, die mit AlchemyLanguage aufbereitet wurden, sollten baldmöglichst nach Aufbereitungen mit Natural Language Understanding (NLU) migriert werden. Informationen zum Migrieren von Sammlungen und Konfigurationsdateien, die die {{site.data.keyword.alchemylanguageshort}}-Aufbereitungen verwenden, finden Sie unter [Aufbereitungnen nach {{site.data.keyword.nlushort}} migrieren](/docs/services/discovery/migrate-nlu.html).

**Hinweis:** Die {{site.data.keyword.discoveryshort}}-Tools verwenden immer die neueste API-Versionszeichenfolge. Ab der API-Versionszeichenfolge `2017-10-16` können Sie daher keine Dokumente mehr in vorhandene {{site.data.keyword.alchemylanguageshort}}-Sammlungen hochladen oder mit {{site.data.keyword.alchemylanguageshort}}-Aufbereitungen aufbereitete neue Sammlungen in den {{site.data.keyword.discoveryshort}}-Tools erstellen. Falls Sie weiterhin die Discovery-Tools für die Aufbereitung von Sammlungen verwenden wollen, migrieren Sie zuerst Ihre Sammlungen nach Natural Language Understanding. Details finden Sie unter [Aufbereitungen nach {{site.data.keyword.nlushort}} migrieren](/docs/services/discovery/migrate-nlu.html).

### Entitätsextraktion (AlchemyLanguage)
{: #entity-extraction-al}

Gibt Elemente wie Personen, Orte und Organisationen zurück, die im Eingabetext vorhanden sind. Die Entitätsextraktion fügt semantisches Wissen zum Inhalt hinzu, mit dessen Hilfe das Subjekt und der Kontext des analysierten Textes ermittelt werden können. Die Verfahren für die Entitätsextraktion basieren auf hoch entwickelten Statistikalgorithmen und der Technologie zur Verarbeitung natürlicher Sprache und sind durch ihre Unterstützung von mehrsprachiger Analyse, kontextabhängiger Vereindeutigung und Zitatextraktion branchenweit singulär. 

Beispielabschnitt eines mit Entitätsextraktion aufbereiteten Dokuments:

```json
{
      "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
      "enriched-text": {
        "status": "OK",
        "language": "english",
        "entities": [
          {
            "type": "City",
            "relevance": 0.532754,
            "sentiment": {
              "type": "positive",
              "score": 0.527541,
              "mixed": false
            },
            "count": 1,
            "text": "Atlanta",
            "disambiguated": {
              "subType": [
                "AdministrativeDivision",
                "GovernmentalJurisdiction",
                "OlympicHostCity",
                "PlaceWithNeighborhoods"
              ],
              "name": "Atlanta",
              "website": "http://www.atlantaga.gov/",
              "dbpedia": "http://dbpedia.org/resource/Atlanta",
              "freebase": "http://rdf.freebase.com/ns/m.013yq"
            }
          }
        ]
      }
    }
```
{: codeblock}
Im obigen Beispiel könnte der Entitätstyp durch Zugriff auf `enriched_text.entities.type` abgefragt werden.

Der Wert von `sentiment` (Stimmung) wird für Entitätstypen auch dann berechnet, falls die Aufbereitung für **sentiment** nicht ausgewählt ist. Weitere Informationen zur Stimmungsbewertung finden Sie unter [Stimmungsanalyse](/docs/services/discovery/discovery-auxiliary.html#sentiment-analysis-al).

Die Quote für die Relevanz (`relevance`) reicht von `0.0` bis `1.0`. Je höher die Quote, desto relevanter die Entität. Das Feld `disambiguated` enthält die Vereindeutigungsinformationen für die Entität. Hierzu gehören Informationen zum Subtyp der Entität (Feld `subType`) und - sofern zutreffend - Links zu der/den Ressource(n). Das Feld `count` gibt an, wie häufig die Entität im Dokument erwähnt wird.

### Schlüsselwortextraktion (AlchemyLanguage)
{: #keyword-extraction-al}

Extrahiert wichtige Themen in Ihrem Inhalt, die normalerweise bei der Datenindexierung, der Generierung von Tagwolken oder bei der Suche verwendet werden. Der {{site.data.keyword.discoveryshort}}-Service erkennt automatisch unterstützte Sprachen im eingegebenen Inhalt. Anschließend ermittelt er Schlüsselwörter in diesem Inhalt und erstellt für sie eine Rangfolge.

Beispielabschnitt eines mit Schlüsselwortextraktion aufbereiteten Dokuments:

```json
{
    "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched-text": {
        "status": "OK",
        "language": "english",
        "keywords": [
          {
            "relevance": 0.66497,
            "sentiment": {
              "score": 0.527541,
              "type": "positive",
              "mixed": false
            },
            "text": "stockholders"
          }
        ]
      }
    }
```
{: codeblock}

Im obigen Beispiel könnte der Schlüsselworttext durch Zugriff auf `enriched_text.keywords.text` abgefragt werden.

Der Wert von `sentiment` (Stimmung) wird für Schlüsselwörter auch dann berechnet, falls die Aufbereitung für **sentiment** nicht ausgewählt ist. Weitere Informationen zur Stimmungsbewertung finden Sie unter [Stimmungsanalyse](/docs/services/discovery/discovery-auxiliary.html#sentiment-analysis-al).

Die Quote für die Relevanz (`relevance`) reicht von `0.0` bis `1.0`. Je höher die Quote, desto relevanter das Schlüsselwort.

### Taxonomieklassifizierung (AlchemyLanguage)
{: #taxonomy-classification-al}

Kategorisiert Eingabetext, HTML oder webbasierten Inhalt in einer hierarchischen und bis zu fünf Ebenen umfassenden Taxonomie. Mithilfe von tieferen Ebenen können Sie Inhalt in präzisere und nützlichere Untersegmente klassifizieren. 

Beispielabschnitt eines mit Taxonomieklassifizierung aufbereiteten Dokuments:

```json
  {
    "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched-text": {
        "status": "OK",
        "language": "english",
        "taxonomy": [
          {
            "label": "/business and industrial/company/merger and acquisition",
            "score": 0.517533,
            "confident": false
          }
        ]
      }
    }
```
{: codeblock}

Im obigen Beispiel könnte die Taxonomiekennzeichnung durch Zugriff auf `enriched_text.taxonomy.label` abgefragt werden.

Das Feld `label` gibt die erkannte Taxonomiekategorie an. Die Hierarchieebenen sind durch Schrägstriche voneinander abgegrenzt. Die Bewertung (Feld `score`) für diese Kategorie reicht von `0.0` bis `1.0`. Je höher die Bewertung, desto größer die Konfidenz in dieser Kategorie.

### Konzepttagging (AlchemyLanguage)
{: #concept-tagging-al}

Erkennt Konzepte, zu denen der Eingabetext gehört, auf der Basis anderer Konzepte und Entitäten, die in diesem Text vorhanden sind. Das Konzepttagging erkennt, wie Konzepte zueinander in Beziehung stehen, und ist in der Lage, Konzepte zu identifizieren, die im Text nicht direkt referenziert werden. Falls in einem Artikel beispielsweise die Begriffe 'CERN' und 'Higgs-Boson' erwähnt werden, erkennen die Funktionen der API für Konzepte selbst dann das neue Konzept 'Large Hadron Collider' (Großer Hadronen-Speicherring), wenn dieser Begriff auf der Seite nicht explizit erwähnt ist. Das Konzepttagging ermöglicht eine Analyse des Eingabeinhalts auf einer höheren Ebene als der reinen Schlüsselworterkennung.

Beispielabschnitt eines mit Konzepttagging aufbereiteten Dokuments:

```json
{
    "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
        "status": "OK",
        "language": "english",
        "concepts": [
          {
            "text": "Acme Corporation",
            "relevance": 0.91136,
            "dbpedia": "http://dbpedia.org/resource/Acme_Corporation",
            "freebase": "http://rdf.freebase.com/ns/m.0dndy",
            "yago": "http://yago-knowledge.org/resource/Acme_Corporation"
          }
        ]
      }
    }
```
{: codeblock}

Im obigen Beispiel könnte der Konzepttexttyp durch Zugriff auf `enriched_text.concepts.text` abgefragt werden.

Die Quote für die Relevanz (`relevance`) reicht von `0.0` bis `1.0`. Je höher die Quote, desto relevanter das Konzept. Sofern zutreffend, werden Links zu der/den Ressource(n) bereitgestellt.

### Beziehungsextraktion (AlchemyLanguage)
{: #relation-extraction-al}

Erkennt Subjekt-, Aktions- und Objektbeziehungen innerhalb von Sätzen im Eingabeinhalt. Mithilfe von Beziehungsinformationen können Kaufsignale, Schlüsselereignisse und andere wichtige Aktionen automatisch erkannt werden.

Beispielabschnitt eines mit Beziehungsextraktion aufbereiteten Dokuments:

```json
{
      "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
      "enriched-text": {
        "status": "OK",
        "language": "english",
        "relations": [
          {
            "sentence": " The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, GA.",
            "subject": {
              "text": "The stockholders",
              "keywords": [
                {
                  "text": "stockholders"
                }
              ]
            },
            "action": {
              "text": "were",
              "lemmatized": "be",
              "verb": {
              "text": "be",
              "tense": "past"
            }
            },
            "object": {
              "text": "pleased that Acme Corporation plans to build a new factory in Atlanta, GA",
              "sentiment": {
                "type": "positive",
                "score": 0.834516,
                "mixed": false
              },
              "entities": [
                {
                  "type": "Company",
                  "text": "Acme Corporation"
                },
                {
                  "type": "City",
                  "text": "Atlanta",
                  "disambiguated": {
                    "subType": [
                      "AdministrativeDivision",
                      "GovernmentalJurisdiction",
                      "OlympicHostCity",
                      "PlaceWithNeighborhoods"
                    ],
                    "name": "Atlanta",
                    "website": "http://www.atlantaga.gov/",
                    "dbpedia": "http://dbpedia.org/resource/Atlanta",
                    "freebase": "http://rdf.freebase.com/ns/m.013yq"
                  }
                },
                {
                  "type": "StateOrCounty",
                  "text": "GA"
                }
              ],
              "keywords": [
                {
                  "text": "Acme Corporation"
                },
                {
                  "text": "new factory"
                },
                {
                  "text": "GA"
                },
                {
                "text": "Atlanta"
                }
              ]
            }
          }
        ]
      }
    }
```
{: codeblock}

Im obigen Beispiel könnte der Text für das Subjekt der Beziehung durch Zugriff auf `enriched_text.relations.subject.text` abgefragt werden.

Der Wert von `sentiment` (Stimmung) wird für Beziehungen auch dann berechnet, falls die Aufbereitung für **sentiment** nicht ausgewählt ist. Weitere Informationen zur Stimmungsbewertung finden Sie unter [Stimmungsanalyse](/docs/services/discovery/discovery-auxiliary.html#sentiment-analysis-al). `Entitäten` oder `Schlüsselwörter` werden (wie im Beispiel gezeigt) nur dann extrahiert, wenn Sie die Aufbereitungen für **Entitäten** und **Schlüsselwörter** auswählen. Weitere Informationen zu diesen Aufbereitungen enthalten die Abschnitte [Entitätsextraktion](/docs/services/discovery/discovery-auxiliary.html#entity-extraction-al) und [Schlüsselwortextraktion](/docs/services/discovery/discovery-auxiliary.html#keyword-extraction-al).

Die Felder `subject`, `action` und `object` werden für jeden Satz extrahiert, der eine Beziehung enthält.

### Stimmungsanalyse (AlchemyLanguage)
{: #sentiment-analysis-al}

Erkennt Grundhaltungen, Meinungen oder Emotionen im analysierten Inhalt. Der {{site.data.keyword.discoveryshort}}-Service kann die Gesamtstimmung innerhalb eines Dokuments, die Stimmung für benutzerdefinierte Ziele, die Stimmung auf Entitätsebene, die Stimmung auf Zitatebene, die Richtungsstimmung und die Stimmung auf Schlüsselwortebene berechnen. Die Kombination dieser Leistungsmerkmale unterstützt eine Vielzahl von Anwendungsfällen, die von der Überwachung sozialer Medien bis hin zur Trendanalyse reichen können.

Beispielabschnitt eines mit Stimmungsanalyse aufbereiteten Dokuments:

```json
{
      "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
      "enriched_text": {
        "status": "OK",
        "language": "english",
        "docSentiment": {
          "type": "positive",
          "score": 0.0966252,
          "mixed": true
        }
      }
    }
```
{: codeblock}

Im obigen Beispiel könnte der Typ der Stimmung für das Dokument (docSentiment) durch Zugriff auf `enriched_text.docSentiment.type` abgefragt werden.

Das Feld `type` gibt die Gesamtstimmung des Dokuments an (`positive`, `negative` oder `neutral`). Der Wert von `type` für die Stimmung basiert auf der Bewertung (Feld `score`). Die Bewertung `0.0` gibt an, dass das Dokument `neutral` ist. Eine positive Zahl gibt an, dass das Dokument `positiv` ist, eine negative Zahl gibt an, dass das Dokument `negativ` ist. Falls für `mixed` der Wert `true` angegeben ist, enthält das Dokument sowohl positive als auch negative Stimmungen (dieses Feld wird nicht durch die `Bewertung` bestimmt).

### Emotionsanalyse (AlchemyLanguage)
{: #emotion-analysis-al}

Erkennt Wut, Abscheu, Angst, Freude und Traurigkeit, die in einem Text in englischer Sprache zum Ausdruck kommt. Die Emotionsanalyse kann Emotionen erkennen, die zielgruppenspezifischen Ausdrücken, Entitäten oder Schlüsselwörtern zugeordnet sind. Sie kann auch die generelle emotionale Tendenz des Inhalts analysieren.

Beispielabschnitt eines mit Emotionsanalyse aufbereiteten Dokuments:

```json
{
      "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
      "enriched_text": {
        "status": "OK",
        "language": "english",
        "docEmotions": {
          "anger": "0.077394",
          "disgust": "0.044024",
          "fear": "0.092664",
          "joy": "0.553327",
          "sadness": "0.3969"
        }
      }
    }
```
{: codeblock}

Im obigen Beispiel könnte die Emotion des Dokuments (docEmotion) `joy` (Freude) durch Zugriff auf `enriched_text.docEmotions.joy` abgefragt werden.

Die Emotionsanalyse analysiert den Text und berechnet für die Emotionen 'anger' (Wut), 'disgust' (Abscheu), 'fear' (Angst), 'joy' (Freude) und 'sadness' (Traurigkeit) eine Bewertung, die sich auf einer Skala von `0.0` bis `1.0` befindet. Ist die Bewertung für eine Emotion `0.5` oder höher, wurde diese Emotion erkannt (je höher die Bewertung über `0.5` liegt, desto höher ist die Relevanz). Im gezeigten Snippet hat `joy` eine Bewertung von über 0.5; {{site.data.keyword.watson}} hat also Freude erkannt.


## Watson Discovery News Original

Eine neue Version von {{site.data.keyword.discoverynewsfull}} ist seit dem **31. Juli 2017** verfügbar. {{site.data.keyword.discoverynewsfull}} Original wurde mit dem Servicedatum **15. Januar 2018** zurückgezogen. Informationen zu dieser neuen Version finden Sie unter [Watson Discovery News](watson-discovery-news.html).

{{site.data.keyword.discoverynewsfull}} Original ist ein Datenbestand aus vorwiegend englischsprachigen Nachrichtenquellen, der laufend aktualisiert wird, wobei täglich ca. 300.000 neue Artikel und Blogbeiträge hinzugefügt werden. Dieser indexierte Datenbestand ist bereits mit den folgenden {{site.data.keyword.alchemylanguageshort}}-Aufbereitungen aufbereitet worden: **Schlüsselwortextraktion**, **Entitätsextraktion**, **Konzepttagging**, **Beziehungsextraktion**, **Stimmungsanalyse** und **Taxonomieklassifizierung**. Auch die folgenden zusätzlichen Metadaten werden hinzugefügt: Suchlaufdatum, Veröffentlichungsdatum, URL-Einstufung, Hosteinstufung und Ankertext. Eine Archivsuche ist für die Nachrichtendaten der letzten 60 Tage verfügbar. 

{{site.data.keyword.discoverynewsfull}} Original wird mit {{site.data.keyword.alchemylanguageshort}}-Aufbereitungen aufbereitet. Weitere Informationen zu diesen Aufbereitungen finden Sie unter [{{site.data.keyword.alchemylanguageshort}}-Aufbereitungen](discovery-auxiliary.html#AlchemyLanguage-enrichments).

### Watson Discovery News Original abfragen

Eine neue Version von {{site.data.keyword.discoverynewsfull}} ist seit dem **31. Juli 2017** verfügbar. {{site.data.keyword.discoverynewsfull}} Original wurde mit dem Servicedatum **15. Januar 2018** zurückgezogen. Informationen zu dieser neuen Version finden Sie unter [Watson Discovery News](watson-discovery-news.html).

**Hinweis:** Die maximale Anzahl der zurückgegebenen Ergebnisse für eine Abfrage von Watson Discovery News ist `50`. Verwenden Sie zusätzliche Abfragen und den Parameter `offset`, um mehr als `50` Ergebnisse zurückzugeben.

{{site.data.keyword.discoverynewsfull}} Original verwendet ein ähnliches, jedoch etwas anderes JSON-Schema als das für private Sammlungen verwendete Schema. Sie müssen `enriched_text` nicht in Ihre Abfragen aufnehmen. Beispiel:

**{{site.data.keyword.discoverynewsfull}} Original-Abfrage strukturieren**

![Beispiel für Struktur einer Watson Discovery News Original-Abfrage](images/news_query_structure.png)

Die folgende Beispielabfrage gibt die 10 relevantesten Artikel in {{site.data.keyword.discoverynewsfull}} Original über die Pittsburgh Steelers mit einer positiven Stimmung zurück.

1.  Wählen Sie in der Anzeige **Daten verwalten** die Sammlung '{{site.data.keyword.discoverynewsfull}}' aus.
1.  Klicken Sie auf **Datenschema anzeigen** und dann auf **Abfragen erstellen**.
1.  Klicken Sie unter **Dokumente suchen** auf **{{site.data.keyword.discoveryshort}}-Abfragesprache verwenden** und geben Sie dann `text:Pittsburgh Steelers, docSentiment.type:positive` im Feld **Abfrage hier eingeben** ein.
1.  Klicken Sie auf **Weitere Optionen** und geben Sie dann den Wert `10` (dies ist der Standardwert) im Feld `Anzahl zurückzugebender Dokumente` ein.
1.  Klicken Sie auf **Abfrage ausführen**. Die wichtigsten 10 Artikel über die Pittsburgh Steelers mit einer positiven Stimmung werden angezeigt.

**Zusätzliche Beispielabfragen für {{site.data.keyword.discoverynewsfull}} Original**

-  `concepts.text:"Health care"` - Klicken Sie unter **Dokumente suchen** auf **{{site.data.keyword.discoveryshort}}-Abfragesprache verwenden** und geben Sie dann diese Abfrage ein. Sie gibt alle Artikel zurück, die das Konzept `health care` enthalten. Falls Sie im Feld **Anzahl zurückzugebender Dokumente** eine Zahl angeben (z. B. 50), erhalten Sie nur die 50 relevantesten Artikel.

**{{site.data.keyword.discoverynewsfull}} Original-Aggregation strukturieren**

![Beispiel für die Struktur einer Watson Discovery News Original-Aggregationsabfrage](images/news_aggregation_structure.png)

Die folgende Beispielaggregation gibt für jede Stimmung die Anzahl der Artikel zurück, die in {{site.data.keyword.discoverynewsfull}} Original über die Pittsburgh Steelers gefunden wurden.

1.  Wählen Sie in der Anzeige **Daten verwalten** die Sammlung '{{site.data.keyword.discoverynewsfull}} Original' aus.
1.  Klicken Sie auf **Datenschema anzeigen** und dann auf **Abfragen erstellen**.
1.  Geben Sie unter **Analyse der Ergebnisse einbeziehen** die Zeichenfolge `filter(text:"Pittsburgh Steelers").term(docSentiment.type,count:3)` im Feld **Aggregationsabfrage mit {{site.data.keyword.discoveryshort}}-Abfragesprache schreiben** ein.
1.  Klicken Sie auf **Weitere Optionen** und geben Sie dann den Wert `0` im Feld **Anzahl zurückzugebender Dokumente** ein.
1.  Klicken Sie auf **Abfrage ausführen**. Die Ergebnisse geben die Anzahl der Dokumente über die Pittsburgh Steelers sowie die Anzahl der Ergebnisse mit dem Wert `positive`, `negative` oder `neutral` für 'docSentiment' an.

**Zusätzliche Beispielaggregation für {{site.data.keyword.discoverynewsfull}} Original**

-  `filter(entities.text:twitter).term(docSentiment.type,count:3)` - Wenn Sie diese Aggregationsabfrage im Feld **Aggregationsabfrage mit {{site.data.keyword.discoveryshort}}-Abfragesprache schreiben** eingeben, wird zunächst der Artikelbestand auf die Artikel eingegrenzt (gefiltert), die für 'entities' den Text 'twitter' enhalten. Anschließend werden diese Artikel nach dem Typ der Dokumentstimmung unterteilt. Nur die drei übergeordneten Stimmungstypen für Dokumente (`positive`, `negative`, `neutral`) werden zurückgegeben.

Die Angabe von `nested` vor einer Aggregationsabfrage beschränkt die Aggregation auf den Bereich der angegebenen Ergebnisse. Beispielsweise bedeutet `nested(text.entities)`, dass nur die Komponenten `text.entities` von Ergebnissen als Grundlage für die Aggregation verwendet werden. Diese Wirkung kann einfach anhand der Unterschiede zwischen den beiden folgenden Abfragen veranschaulicht werden.  Die Aggregation `filter(text.entities.type::City)` zählt die Anzahl der *Ergebnisse*, die eines oder mehrere Elemente `entity` mit dem Typ `City` enthalten. Die Aggregation `nested(text.entities).filter(text.entities.type::City)` zählt die Anzahl der Instanzen eines Elements `entity` mit dem Typ `City` in den Ergebnissen. Alle nachfolgenden Operationen grenzen die Ergebnismenge, für die eine Aggregation ausgeführt werden kann, weiter ein. Beispielsweise bedeutet `nested(text.entities).filter(text.entities.type::City)`, dass nur Entitäten mit `type::City` aggregiert werden. Beispiel: `nested(text.entities).filter(text.entities.type::City).term(text.entities.text,count:3)` aggregiert die drei relevantesten Entitäten des Typs `City`, wohingegen `filter(text.entities.type::City).term(text.entities.text,count:3)` die drei relevantesten Entitäten zurückgibt, wobei das Ergebnis mindestens eine Entität des Typs `City` zurückgibt.

**Hinweis:** Das Anpassen der {{site.data.keyword.discoverynewsfull}} Original-Konfiguration, das Durchführen eines Trainings oder das Hinzufügen von Dokumenten zu dieser Sammlung ist nicht möglich.

## Integration mit Watson Knowledge Studio bei Verwendung von AlchemyLanguage-Aufbereitungen

Sie können ein angepasstes Modell aus {{site.data.keyword.knowledgestudiofull}} mit dem {{site.data.keyword.discoveryshort}}-Service integrieren, um angepasste Aufbereitungen bereitzustellen.
{: shortdesc}

### Vorbereitende Schritte

Bevor Sie ein angepasstes Modell aus {{site.data.keyword.knowledgestudioshort}} mit dem {{site.data.keyword.discoveryshort}}-Service integrieren können, müssen Sie das Modell mithilfe von {{site.data.keyword.knowledgestudioshort}} erstellen und bereitstellen. Informationen zum Erstellen und Bereistellen von Modellen finden Sie in der Dokumentation von {{site.data.keyword.knowledgestudioshort}}. Sie benötigen die eindeutige ID des bereitgestellten Modells, um es mit dem {{site.data.keyword.discoveryshort}}-Service zu integrieren.

### Informationen zu diesem Vorgang

Mithilfe eines angepassten Modells, das in {{site.data.keyword.knowledgestudioshort}} entwickelt wurde, können Sie Dokumente im {{site.data.keyword.discoveryshort}}-Service aufbereiten. Dies gibt Ihnen die Flexibilität, die Dokumenterweiterungsfunktionen des {{site.data.keyword.discoveryshort}}-Service mit spezifischen Informationen zu besonders interessanten Bereichen (z. B. Branchen und wissenschaftliche Disziplinen) anzuwenden. In Ihrem Aufbereitungsmodell können Sie sowohl allgemein zugängliche als auch eigene proprietäre Daten verwenden.

Sie müssen die Service-API verwenden, um ein {{site.data.keyword.knowledgestudioshort}}-Modell mit dem {{site.data.keyword.discoveryshort}}-Service zu integrieren. Die Integration eines angepassten Modells mit den {{site.data.keyword.discoveryshort}}-Tools ist nicht möglich.

### Prozedur

1.  Ermitteln Sie die ID Ihrer {{site.data.keyword.discoveryshort}}-Umgebung (siehe [Umgebungen auflisten ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_environments){: new_window}). Notieren Sie sich die Umgebungs-ID.
1.  Listen Sie die IDs der aktuellen {{site.data.keyword.discoveryshort}}-Konfiguration(en) auf (siehe [Konfigurationen auflisten ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_configurations){: new_window}). Notieren Sie sich die ID der Konfiguration, die Sie mit Ihrem angepassten Modell von {{site.data.keyword.knowledgestudiofull}} integrieren wollen.
1.  Laden Sie mit dem folgenden Befehl in einer Bash-Shell oder funktional entsprechenden Shell wie Cygwin for Windows eine Kopie Ihrer aktuellen {{site.data.keyword.discoveryshort}}-Konfiguration herunter. Ersetzen Sie hierbei `{umgebungs-id}` und `{konfigurations-id}` durch die IDs, die Sie in den beiden vorherigen Schritten notiert haben.

    ```bash
    curl -u "{benutzername}":"{kennwort}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{umgebungs-id}/configurations/{konfigurations-id}?version=2017-09-01" > my_config.json
    ```
    {: pre}

    Dieser Befehl listet den Inhalt Ihrer Sammlungsdatei auf und speichert ihn in einer JSON-Datei namens `my_config.json`.
1.  Öffnen Sie die Datei `my_config.json` in einem Texteditor und nehmen Sie die folgenden Änderungen vor:
    1.  Ändern Sie den Wert des Feldes `"name"` in einen Wert, der den Zweck der neuen Konfiguration angibt. Optional können Sie auch den Wert des Feldes `"description"` ändern.

        ```json
        ...
        "name": "wks-config",
        "description": "This is a configuration to use with a WKS model",
        ...
        ```
        {: codeblock}

    1.  Aktualisieren Sie die Felder unter 'enrichments' für das {{site.data.keyword.knowledgestudioshort}}-Modell. Es wird davon ausgegangen, dass die Felder anfänglich wie folgt definiert sind:

        ```json
        "enrichments": [
          {
            "destination_field": "enriched_text",
            "source_field": "text",
            "enrichment": "alchemy_language",
            "options": {
              "extract": "keyword, entity, doc-sentiment, taxonomy, concept, relation",
              "sentiment": true,
              "quotations": true
            }
          }
        ]
        ```
        {: codeblock}

    1.  Aktualisieren Sie die Datei wie folgt, indem Sie die eindeutige ID des {{site.data.keyword.knowledgestudioshort}}-Modells anstelle von `{id_des_watson_knowledge_studio-modells}` angeben (siehe 'Vorbereitende Schritte').

        ```json
        "enrichments": [
          {
            "destination_field": "enriched_text",
            "source_field": "text",
            "enrichment": "alchemy_language",
            "options": {
              "extract": "keyword, entity, doc-sentiment, taxonomy, concept, relation, typed-rels",
              "sentiment": true,
              "quotations": true,
              "model": "{watson_knowledge_studio_model_ID}"
            }
          }
        ]
        ```
        {: codeblock}

1.  Aktivieren Sie optional die Entitätsnormalisierung (siehe [Angepasste Konfiguration zur Normalisierung von Entitäten erstellen](/docs/services/discovery/normalize-entities.html)).
1.  Speichern Sie die Datei `my_config.json`.
1.  Verwenden Sie ein JSON-Prüfprogramm (z. B. [JSLint ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://jslint.com){: new_window}, um die bearbeitete JSON-Datei zu prüfen und bei Bedarf zu korrigieren, bevor Sie die nächsten Schritte ausführen.
1.  Aktualisieren Sie die Konfiguration wie folgt. Sie benötigen wieder die `{umgebungs-id}` und die `{konfigurations-id}`, die Sie zu Beginn dieser Prozedur ermittelt haben.

    ```bash
    curl -X PUT -u "{benutzername}":"{kennwort}" -H "Content-Type: application/json" -d @my_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{umgebungs-id}/configurations/{konfigurations-id}?version=2017-09-01"
    ```
    {: pre}

    Der Befehl gibt den Inhalt der aktualisierten Konfigurationsdatei zurück.
1.  Verwenden Sie den {{site.data.keyword.discoveryshort}}-Service wie gewohnt. Dokumente, die Sie mit der aktualisierten Konfiguration einpflegen, werden automatisch mit den Daten aus dem angepassten Modell aufbereitet.

## Angepasste Konfiguration zum Normalisieren von AlchemyLanguage-Entitäten erstellen
{: #normalizing-entities}

Sie können den {{site.data.keyword.discoveryshort}}-Service so konfigurieren, dass in die Ausgabe Ihrer Abfragen *normalisierte Entitäten* einbezogen werden, die auch als *kanonische Namen* bezeichnet werden.
{: shortdesc}

**Hinweis:** Die Bearbeitung der Konfiguration zum Aktivieren normalisierter Entitäten ist eine manuelle Task, die mit einem Texteditor und API-Aufrufen ausgeführt werden muss. In den Tools wird sie gegenwärtig nicht unterstützt.

**Hinweis:** Die Entitätsnormalisierung ist nur dann verfügbar, wenn Sie den Discovery-Service mit einem von Watson Knowledge Studio generierten angepassten Modell verwenden (siehe [Integration mit {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery/integrate-wks.html)).

Die Entitätsnormalisierung fügt normalisierte (kanonische) Namen für verschiedene Verweise auf dieselbe Person oder dasselbe Objekt im Quellendokument ein. Falls Sie beispielsweise die Entitätsnormalisierung aktivieren und anschließend eines oder mehrere Dokumente einpflegen, die 'J.R. Cash' und 'John R. Cash' behandeln, enthält die verarbeitete Ausgabe im Feld `canonical_name` den kanonischen Namen 'Johnny Cash' zusammen mit jedem übereinstimmenden Begriff. Sie enthält außerdem relevante kanonische Namen für andere im Dokument gefundene Textentitäten. Eine Beispielausgabe finden Sie am Ende dieses Abschnitts.

Nachdem Sie ein Dokument mit kanonischen Namen aufbereitet haben, können Sie einfacher nach bestimmten Elementen mit demselben kanonischen Namen suchen.

Kanonische Namen werden aus einem allgemein zugänglichen Wörterverzeichnis abgeleitet. Falls im Wörterverzeichnis kein passender kanonischer Name zu finden ist, verwendet der Service die passendste Entitätsreferenz im Dokument als kanonischen Namen. Bevor Sie ein Dokument mit Entitätsnormalisierung nach einem kanonischen Namen abfragen, untersuchen Sie das aufbereitete JSON-Dokument und vergewissern Sie sich, dass der/die kanonische(n) Name(n), der/die vom Service generiert wurde(n), mit dem/den von Ihnen erwarteten Namen übereinstimmen.

### Prozedur

1.  Ermitteln Sie die ID Ihrer {{site.data.keyword.discoveryshort}}-Umgebung (siehe [Umgebungen auflisten ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_environments){: new_window}). Notieren Sie sich die Umgebungs-ID.
1.  Listen Sie die IDs der aktuellen {{site.data.keyword.discoveryshort}}-Konfiguration(en) auf (siehe [Konfigurationen auflisten ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_configurations){: new_window}).  Notieren Sie sich die ID der Konfiguration, die Sie aktualisieren wollen.
1.  Laden Sie mit dem folgenden Befehl in einer Bash-Shell oder funktional entsprechenden Shell wie Cygwin for Windows eine Kopie Ihrer aktuellen {{site.data.keyword.discoveryshort}}-Konfiguration herunter. Ersetzen Sie hierbei `{umgebungs-id}` und `{konfigurations-id}` durch die IDs, die Sie in den beiden vorherigen Schritten notiert haben.

    ```bash
    curl -u "{benutzername}":"{kennwort}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{umgebungs-id}/configurations/{konfigurations-id}?version=2017-09-01" > new_config.json
    ```
    {: pre}

    Dieser Befehl listet den Inhalt Ihrer Sammlungsdatei auf und speichert ihn in einer JSON-Datei namens `new_config.json`.

1.  Öffnen Sie die Datei `new_config.json` in einem Texteditor und nehmen Sie die folgenden Änderungen vor:
    1. Ändern Sie den Wert des Feldes `"name"` in einen Wert, der den Zweck der neuen Konfiguration angibt. Optional können Sie auch den Wert des Feldes `"description"` ändern.

       ```json
        ...
        "name": "normalize-entities-config",
        "description": "This configuration enables entity normalization",
        ...
       ```
       {: codeblock}

    1. Aktualisieren Sie die Felder unter 'enrichments' für das {{site.data.keyword.knowledgestudioshort}}-Modell. Es wird davon ausgegangen, dass die Felder anfänglich wie folgt definiert sind:

       ```json
       "enrichments": [
         {
           "destination_field": "enriched_text",
           "source_field": "text",
           "enrichment": "alchemy_language",
           "options": {
             "extract": "keyword, entity, doc-sentiment, taxonomy, concept, relation, typed-rels",
             "sentiment": true,
             "quotations": true,
             "model": "{watson_knowledge_studio_model_ID}"
           }
         }
       ]
       ```
       {: codeblock}

    1. Aktualisieren Sie die Datei wie folgt.

       ```json
       "enrichments": [
         {
           "destination_field": "enriched_text",
           "source_field": "text",
           "enrichment": "alchemy_language",
           "options": {
             "extract": "keyword, entity, doc-sentiment, taxonomy, concept, relation, typed-rels",
             "sentiment": true,
             "quotations": true,
             "model": "{watson_knowledge_studio_model_ID}"
             "normalizeEntities": 1
           }
         }
       ]
       ```
       {: codeblock}

    1. Speichern Sie die Datei `new_config.json`.

1.  Verwenden Sie ein JSON-Prüfprogramm (z. B. [JSLint ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://jslint.com){: new_window}, um die bearbeitete JSON-Datei zu prüfen, bevor Sie die nächsten Schritte ausführen.

1.  Aktualisieren Sie die Konfiguration wie folgt. Sie benötigen wieder die `{umgebungs-id}` und die `{konfigurations-id}`, die Sie zu Beginn dieser Prozedur ermittelt haben.

    ```bash
    curl -X PUT -u "{benutzername}":"{kennwort}" -H "Content-Type: application/json" -F configuration-@new_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{umgebungs-id}/configurations/{konfigurations-id}?version=2017-09-01"
    ```
    {: pre}

    Der Befehl gibt den Inhalt der aktualisierten Konfigurationsdatei zurück.

1.  Verwenden Sie den {{site.data.keyword.discoveryshort}}-Service wie gewohnt. Dokumente, die Sie mit der aktualisierten Konfiguration einpflegen, werden automatisch mit normalisierten Entitäten aufbereitet. Dies ist in den folgenden Auszügen dargestellt.

### Ausgabebeispiele

Ausgabesnippet **ohne** `"normalizeEntities": 1`:

```json
{
  "enriched_text": {
  ...
  ...
  ...
    "entity_relations": {
      "entities": {
        "entity": [
          {
            "class": "SPC",
            "eid": "-E0",
            "generic": false,
            "level": "NAM",
            "mentref": [
              {
                "mid": "-M0",
                "text": "J.R. Cash"
              },
              {
                "mid": "-M6",
                "text": "musician"
              },
              {
                "mid": "-M7",
                "text": "who"
              },
              {
                "mid": "-M13",
                "text": "He"
              },
              {
                "mid": "-M20",
                "text": "He"
              }
            ],
            "score": 0.7874817061794613,
            "subtype": "OTHER",
            "type": "PERSON"
          },
        ...
        ...
        ...
        ]
      },
      "relations": {
        "relation": [
          {
            "rel_entity_arg": [
              {
                "argnum": 1,
                "eid": "-E0"
              },
              {
                "argnum": 2,
                "eid": "-E1"
              }
            ],
            "relmentions": {
              "relmention": [
                {
                  "class": "SPECIFIC",
                  "modality": "ASSERTED",
                  "rel_mention_arg": [
                    {
                      "argnum": 1,
                      "mid": "-M0",
                      "text": "John R. Cash",
                    },
                    {
                      "argnum": 2,
                      "mid": "-M1",
                      "text": "country"
                    }
                  ],
                  "rmid": "-R1-1",
                  "score": 0.49918343781296,
                  "tense": "UNSPECIFIED"
                }
              ]
            },
            "rid": "-R1",
            "subtype": "OTHER",
            "type": "knownAs"
          },
          ...
          ...
          ...
        ]
      }
    }
  }
}
```
{: codeblock}

Ausgabesnippet **mit** `"normalizeEntities": 1`:

```json
{
  "enriched_text": {
  ...
  ...
  ...
    "entity_relations": {
      "entities": {
        "entity": [
          {
            "class": "SPC",
            "eid": "-E0",
            "generic": false,
            "level": "NAM",
            "mentref": [
              {
                "mid": "-M0",
                "text": "J.R. Cash"
              },
              {
                "mid": "-M6",
                "text": "musician"
              },
              {
                "mid": "-M7",
                "text": "who"
              },
              {
                "mid": "-M13",
                "text": "He"
              },
              {
                "mid": "-M20",
                "text": "He"
              }
            ],
            "score": 0.7874817061794613,
            "subtype": "OTHER",
            "type": "PERSON",
            "canonical_name": "Johnny Cash"
          },
        ...
        ...
        ...
        ]
      },
      "relations": {
        "relation": [
          {
            "rel_entity_arg": [
              {
                "argnum": 1,
                "eid": "-E0"
              },
              {
                "argnum": 2,
                "eid": "-E1"
              }
            ],
            "relmentions": {
              "relmention": [
                {
                  "class": "SPECIFIC",
                  "modality": "ASSERTED",
                  "rel_mention_arg": [
                    {
                      "argnum": 1,
                      "mid": "-M0",
                      "text": "John R. Cash",
                      "canonical_name": "Johnny Cash"
                    },
                    {
                      "argnum": 2,
                      "mid": "-M1",
                      "text": "country",
                      "canonical_name": "country music"
                    }
                  ],
                  "rmid": "-R1-1",
                  "score": 0.49918343781296,
                  "tense": "UNSPECIFIED"
                }
              ]
            },
            "rid": "-R1",
            "subtype": "OTHER",
            "type": "knownAs"
          },
          ...
          ...
          ...
        ]
      }
    }
  }
}
```
{: codeblock}
