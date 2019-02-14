---

copyright:
  years: 2015, 2018
lastupdated: "2018-01-23"

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

# Konfigurationsreferenz

Sie können in JSON eine eigene {{site.data.keyword.discoveryshort}}-Konfiguration für das Einpflegen erstellen, falls für Ihre Daten spezielle Anforderungen an die [Konvertierung](#conversion), [Aufbereitung](#enrichment) oder [Normalisierung](#normalization) gelten.
{: shortdesc}

 Die folgenden Abschnitte zeigen diese JSON-Konfiguration und das Objekt, das in ihr definiert werden kann, im Detail.

## Konfigurationsstruktur
{: #structure}

Eine {{site.data.keyword.discoveryshort}}-Konfiguration ist wie folgt strukturiert:

```json
{
  "name": "Configuration Name",
  "description": "Descriptive text about the configuration",
  "conversions": {
    "word": {},
    "pdf": {},
    "html": {},
    "segment": {},
    "json_normalizations": []
  },
  "enrichments": [],
  "normalizations": []
}
```
{: codeblock}

Das JSON-Basisobjekt enthält die folgenden Elemente:

-  `"name": "Configuration Name"`: Der Name Ihrer Konfiguration.
-  `"description": "Descriptive text about the configuration"`: Eine Beschreibung Ihrer Konfiguration.

Die folgenden Objekte und Arrays müssen definiert werden, um Dokumente zu konvertieren, aufzubereiten und zu normalisieren, die in Ihre Sammlung hochgeladen werden.

- `"conversions": {}`: Gibt an, wie Dokumente in das JSON-Format konvertiert werden, das aufbereitet werden kann.
- `"enrichments": []`: Gibt an, welche Aufbereitungen auf welche JSON-Teile angewendet werden.
- `"normalizations": []`: Hier sind alle Anpassungen angegeben, die nach der Aufbereitung vorzunehmen sind, bevor das Dokument gespeichert wird.

Außerdem werden die folgenden Elemente durch {{site.data.keyword.discoveryshort}} zum Basisobjekt hinzugefügt, wenn die Konfiguration erstellt/aktualisiert wird:

```json
{
  "configuration_id": "4f5b7c7b-ebf4-4963-882e-27eff08f08e3",
  "created": "2017-09-13T14:45:03.575Z",
  "updated": "2017-09-13T14:45:03.575Z"
}
```
{: codeblock}

## Konvertierung
{: #conversion}

Bei der Konvertierung von Dokumenten wird das ursprüngliche Quellenformat als Eingabe verwendet und mit einem oder mehreren Schritten in das JSON-Format umgewandelt, das im weiteren Verlauf des Einpflegeprozesses verwendet wird. Abhängig vom Typ der hochgeladenen Datei vollzieht sich der Prozess wie folgt:

- **PDF**-Dateien werden mit den Optionen von `pdf` in HTML konvertiert. Die resultierende **HTML**-Datei wird anschließend unter Verwendung der Optionen von `html` in JSON konvertiert. Die resultierende **JSON**-Datei wird schließlich unter Verwendung der Optionen von `json` konvertiert.

- **Microsoft Word**-Dateien werden mit den Optionen von `word` in HTML konvertiert. Die resultierende **HTML**-Datei wird anschließend unter Verwendung der Optionen von `html` in JSON konvertiert. Die resultierende **JSON**-Datei wird schließlich unter Verwendung der Optionen von `json` konvertiert.

- **HTML**-Dateien werden unter Verwendung der Optionen von `html` in JSON konvertiert. Die resultierende **JSON**-Datei wird unter Verwendung der Optionen von `json` konvertiert.

- **JSON**-Dateien werden unter Verwendung der Optionen von `json` konvertiert.

Diese Optionen sind in den nachfolgenden Abschnitten beschrieben. Nach Abschluss der Konvertierung werden die [Aufbereitung](#enrichment) und die [Normalisierung](#normalization) durchgeführt, bevor der Inhalt gespeichert wird.

### PDF
{: #pdf}

Das Konvertierungsobjekt `pdf` definiert, wie PDF-Dokumente in HTML konvertiert werden müssen, und besitzt die folgende Struktur:

```json
"pdf": {
  "heading": {
    "fonts": [
      {
        "level": 1,
        "min_size": 24,
        "max_size": 80,
        "bold": false,
        "italic": true,
        "name": "arial"
      },
      {
        "level": 2,
        "min_size": 18,
        "max_size": 24,
        "bold": true,
        "italic": false,
        "name": "ariel"
      }
    ]
  }
},
```
{: codeblock}

Bei der Konvertierung von PDF-Dateien können Überschriften in solchen Dateien erkannt (und in ein geeignetes HTML-Tag `h` konvertiert) werden, indem die Größe, die Schriftart und der Stil jeder Überschriftsebene ermittelt wird. Überschriftsebenen können mehrmals angegeben werden, wenn dies erforderlich ist, damit alle relevanten Abschnitte ordnungsgemäß erkannt werden. Die Erkennung der HTML-Überschriftsebenen ist wichtig, falls Sie später den Inhalt unter Verwendung von CSS-Selektoren extrahieren oder das Dokument aufteilen wollen. Das Objekt `heading` enthält das Array `fonts` und jedes Element in diesem Array gibt eine Überschriftsebene mit den folgenden Parametern an:

- `"level": INT` *(erforderlich)*: Die `h`-Ebene in HTML, in die mit diesen Parametern gekennzeichneter Text konvertiert wird.
- `"min_size": INT` _(optional)_: Die kleinste Schriftgröße, die als diese Überschriftsebene erkannt wird.
- `"max_size": INT` _(optional)_: Die größte Schriftgröße, die als diese Überschriftsebene erkannt wird.
- `"bold": boolean` _(optional)_: Beim Wert `true` werden nur Fettschriften als diese Überschriftsebene erkannt.
- `"italic": boolean` _(optional)_: Beim Wert `true` werden nur Kursivschriften als diese Überschriftsebene erkannt.
- `"name": "string"` _(optional)_: Der Name der Schriftart, die als diese Überschriftsebene erkannt wird.

Damit ein Textbereich als Überschrift erkannt wird, muss er allen Parametern entsprechen, die im jeweiligen Element des Arrays definiert sind. Falls die definierten Parameter zu uneindeutig sind, werden mehr Überschriften erkannt, als Sie erwartet haben. Sie erzielen bessere Ergebnisse, wenn Sie jede Überschriftsebene mehrmals genau definieren, um sicherzustellen, dass alle Überschriftsebenenvarianten ohne ungültige Übereinstimmungen abgedeckt sind.


### Word
{: #word}

Das Konvertierungsobjekt `word` definiert, wie Word-Dokumente in HTML konvertiert werden müssen, und besitzt die folgende Struktur:

```json
"word": {
  "heading": {
    "fonts": [
      {
        "level": 1,
        "min_size": 24,
        "bold": true,
        "italic": false,
        "name": "arial"
      },
      {
        "level": 2,
        "min_size": 18,
        "max_size": 23,
        "bold": true,
        "italic": false
      }
    ],
    "styles": [
      {
        "level": 1,
        "names": [
          "pullout heading",
          "pulloutheading",
          "header"
        ]
      },
      {
        "level": 2,
        "names": [
          "subtitle"
        ]
      }
    ]
  }
},
```
{: codeblock}

Das Konvertierungsobjekt für Microsoft Word funktioniert ähnlich wie das PDF-Konvertierungsobjekt. Es gibt jedoch zwei unterschiedliche Arrays, die im Objekt `heading` angegeben werden können, wenn Überschriften aus Microsoft Word-Dokumenten extrahiert werden. Sie können entweder eines oder beide Arrays für die Überschriftenextraktion verwenden, um Überschriftsebenenelemente aus Ihren Microsoft Word-Dokumenten zu extrahieren.

Jedes Element im Array `fonts` gibt mit den folgenden Parametern unter Verwendung von Schriftartkenndaten eine Überschriftsebene an:

- `"level": INT` *(erforderlich)*: Die `h`-Ebene in HTML, in die mit diesen Parametern gekennzeichneter Text konvertiert wird.
- `"min_size": INT` _(optional)_: Die kleinste Schriftgröße, die als diese Überschriftsebene erkannt wird.
- `"max_size": INT` _(optional)_: Die größte Schriftgröße, die als diese Überschriftsebene erkannt wird.
- `"bold": boolean` _(optional)_: Beim Wert `true` werden nur Fettschriften als diese Überschriftsebene erkannt.
- `"italic": boolean` _(optional)_: Beim Wert `true` werden nur Kursivschriften als diese Überschriftsebene erkannt.
- `"name": "string"` _(optional)_: Der Name der Schriftart, die als diese Überschriftsebene erkannt wird.

Damit ein Textbereich als Überschrift erkannt wird, muss er im Array `font` allen Parametern entsprechen, die im jeweiligen Element des Arrays definiert sind. Falls die definierten Parameter zu uneindeutig sind, werden mehr Überschriften erkannt, als Sie erwartet haben. Sie erzielen bessere Ergebnisse, wenn Sie jede Überschriftsebene mehrmals genau definieren, um sicherzustellen, dass alle Überschriftsebenenvarianten ohne ungültige Übereinstimmungen abgedeckt sind.

Jedes Element im Array `styles` gibt eine Überschriftsebene aus den Microsoft Word-Stilen an, die auf diesen Abschnitt angewendet werden.

- `"level": INT` *(erforderlich)*: Die `h`-Ebene in HTML, in die mit diesen Parametern gekennzeichneter Text konvertiert wird.
- `"names": array` *(erforderlich)*: Ein durch Kommas getrenntes Array von Stilnamen, die als diese Überschriftsebene erkannt werden.

*Situationen für die Verwendung von Schriftarten bzw. Stilen*: Falls Ihre Microsoft Word-Dokumente dem Style-Sheet ordnungsgemäß entsprechen, jeder Abschnitt also korrekt mit den entsprechenden Stil-Tags versehen ist, empfiehlt sich die Verwendung eines Arrays `styles` zum Extrahieren von Überschriften. Möglicherweise stellen Sie jedoch fest, dass einige Dokumente Stile verwenden, die vom Autor manuell überschrieben wurden. Solche Dokumente ergeben eher dann eine gute Konvertierung, wenn die Extraktionsmethode `fonts` verwendet wird.
{: tip}


### HTML
{: #html}

```json
"html": {
  "exclude_tags_completely": [
    "script",
    "sup"
  ],
  "exclude_tags_keep_content": [
    "font",
    "em"
  ],
  "exclude_content": {
    "xpaths": [
      "//*[@id='list-old']",
      "//*[@id='unstable']"
    ]
  },
  "keep_content": {
    "xpaths": [
      "//*[@id='footer']",
      "//*[@id='header']"
    ]
  },
  "exclude_tag_attributes": [
    "EVENT_ACTIONS"
  ],
  "keep_tag_attributes": [
    "id"
  ],
  "extracted_fields": {
    "{field_name}": {
      "css_selector": "{CSS_selector_expression_1}",
      "type": "{field_type}"
    }
  }
},
```
{: codeblock}

#### exclude_tags_completely

`"exclude_tags_completely" : array`: Ein Array der HTML-Tags, die ausgeschlossen werden. Es enthält den Tag, den Inhalt und alle definierten Tagattribute.

#### exclude_tags_keep_content

`"exclude_tags_keep_content" : array`: Ein Array von HTML-Tagnamen, in denen die Taginformationen entfernt werden. Dies führt dazu, dass der HTML-Tag und alle Tagattribute verkürzt werden. Der Inhalt des Tags wird nur dann weiter verkürzt, wenn dies angegeben wird. Falls Sie beispielsweise `exclude_tags_keep_content` für den HTML-Tag `span` angeben, wird `<span class="info">Einige <strong>Informationen</strong></span>` auf `Einige <strong>Informationen</strong>` gekürzt.

#### exclude_content

`"xpaths" : array`: Ein Array aus XPath-Angaben, die den entfernten Inhalt angeben. Wenn dieser Wert festgelegt ist, werden alle mit einer der XPath-Angaben übereinstimmenden Elemente aus der Ausgabe entfernt.

#### keep_content

`"xpaths" : array`: Ein Array aus XPath-Angaben, die den konvertierten Inhalt angeben. Wenn dieser Wert festgelegt ist, werden alle mit einer der XPath-Angaben übereinstimmenden Elemente in die Ausgabe einbezogen. Die durch diesen Parameter angegebenen Einschlüsse werden nach allen Verarbeitungen verarbeitet, die durch `exclude_content` angegeben sind.

#### exclude_tag_attributes

`"exclude_tag_attributes" : array`: Ein Array von HTML-Attributnamen, die durch die Konvertierung unabhängig davon entfernt werden, in welchem HTML-Tag sie vorhanden sind. **Hinweis:** Sie erhalten eine Fehlernachricht, wenn Sie sowohl `exclude_tag_attributes` als auch `keep_tag_attributes` in derselben Konfiguration angeben; es kann nur ein Attribut pro Konfiguration angegeben werden. Falls vorhanden, muss `keep_tag_attributes` vollständig aus der Konfiguration entfernt werden; das Attribut kann nicht als leeres Array vorhanden sein.

#### keep_tag_attributes

`"keep_tag_attributes" : array`: Ein Array von HTML-Attributnamen, die durch die Konvertierung beibehalten werden. **Hinweis:** Sie erhalten eine Fehlernachricht, wenn Sie sowohl `keep_tag_attributes` als auch `exclude_tag_attributes` in derselben Konfiguration angeben; es kann nur ein Attribut pro Konfiguration angegeben werden. Falls vorhanden, muss `exclude_tag_attributes` vollständig aus der Konfiguration entfernt werden; das Attribut kann nicht als leeres Array vorhanden sein.

#### extracted_fields

Dieses Objekt definiert Inhalt aus dem HTML-Quelltext, der bei der Konvertierung in ein separates JSON-Feld extrahiert werden soll. Der Inhalt wird mithilfe von CSS-Selektoren angegeben.

Jedes Feld, das Sie erstellen wollen, wird wie folgt durch ein Objekt definiert:

```json
"{field_name}": {
  "css_selector": "{CSS_selector_expression_1}",
  "type": "{field_type}"
}
```
{: codeblock}

- `"{field_name}"`: Der Name des zu erstellenden Feldes.

**Hinweis:** In Ihrer Konfiguration definierte Feldnamen müssen die Rahmenbedingung erfüllen, die im Abschnitt [Anforderungen für Feldnamen](#field_reqs) definiert sind.

- `"css_selector" : string` *(erforderlich)*: Ein CSS-Selektorausdruck, der den in einem Feld zu speichernden Bereich des Inhalts definiert.
- `"type" : string` *(erforderlich)*: Der Typ des zu erstellenden Feldes, möglich sind `string`, `date`.
Ausführliche Informationen finden Sie unter [Felder mittels CSS-Selektoren extrahieren](/docs/services/discovery/building.md#using-css).

### Segmentierung
{: #segment}

Das Objekt `segment` stellt eine Gruppe von Konfigurationsoptionen dar, die eingepflegte Dokumente in eines oder mehrere Segmente unterteilen. Grundlage hierfür sind die erkannten HTML-Überschriften (`h1`, `h2`).

```json
"segment": {
  "enabled": true,
  "selector_tags": ["h1", "h2", "h3", "h4", "h5", "h6"]
}
```
{: codeblock}

- `"enabled": boolean` *(erforderlich)*: Muss auf `true` gesetzt sein, damit die Dokumentsegmentierung aktiviert ist.
- `"selector_tags": array` *(erforderlich)*: Ein durch Kommas getrenntes Array von HMTL-Tags `h`, nach denen Dokumente segmentiert werden sollen.

Wenn die Dokumentsegmentierung aktiviert ist, kann generell Folgendes nicht angegeben werden:

-  `json_normalizations` kann nicht als Teil der Konfiguration angegeben werden.
-  `normalizations` kann nicht als Teil der Konfiguration angegeben werden.
-  Die Option `extracted_fields` der Konvertierung für `html` kann nicht als Teil der Konfiguration angegeben werden.

Ausführliche Informationen enthält der Abschnitt [Segmentierung ausführen](/docs/services/discovery/building.html#performing-segmentation).


### JSON
{: #json}

Vor der Aufbereitung können Sie eine Normalisierung der eingepflegten JSON-Daten ausführen, indem Sie Objekte des Typs `operation` im Array `json_normalizations` definieren.

```json
"json_normalizations": [
  {
    "operation": "remove",
    "source_field": "header"
  },
  {
    "operation": "copy",
    "source_field": "title",
    "destination_field": "title_old"
  },
  {
    "operation": "move",
    "destination_field": "content",
    "source_field": "body"
  },
  {
    "operation": "merge",
    "source_field": "synopsis",
    "destination_field": "preamble"
  },
  {
    "operation": "remove_nulls"
  }
]
```
{: codeblock}

#### Operationsobjekte
{: #operations}

- `"operation": string` *(erforderlich)*: Die Operation, die für die JSON-Daten ausgeführt werden soll; muss einer der folgenden Werte sein:
  - `remove`: Das angegebene Element des Typs `source_field` wird aus den JSON-Daten entfernt.
  - `copy`: Der angegebene Inhalt von `source_field` wird in eine neue Instanz von `destination_field` kopiert.
  - `move`: Das angegebene Element des Typs `source_field` wird in den Wert von `destination_field` umbenannt. Falls das Element des Typs `destination_field` bereits vorhanden ist, wird eine neue Instanz von `destination_field` erstellt.
  - `merge`: Der Inhalt von `source_field` und `destination_field` wird in `destination_field` zusammengeführt.
  - `remove_nulls`: Felder mit dem Inhalt `null` werden entfernt.
- `"source_field": string` _(optional)_: Das Feld, für das die Operation ausgeführt werden soll.
- `"destination_field": string` _(optional)_: Das Zielfeld, in das die Ausgabe der Operation gestellt werden soll.  

  **Hinweis:** In Ihrer Konfiguration definierte Feldnamen müssen die Rahmenbedingung erfüllen, die im Abschnitt [Anforderungen für Feldnamen](#field_reqs) definiert sind.


## Aufbereitungen
{: #enrichments}

```json
"enrichments": [
  {
    "enrichment": "elements",
    "source_field": "html",
    "destination_field": "enriched_html",
    "options": {
      "model": "contract"
    }
  },
  {
    "enrichment": "natural_language_understanding",
    "source_field": "title",
    "destination_field": "enriched_title",
    "options": {
      "features": {
        "keywords": {
          "sentiment": true,
          "emotion": false,
          "limit": 50
        },
        "entities": {
          "sentiment": true,
          "emotion": false,
          "limit": 50,
          "mentions": true,
          "mention_types": true,
          "sentence_locations": true,        
          "model": "WKS-model-id"
        },
        "sentiment": {
          "document": true,
          "targets": [
            "IBM",
            "Watson"
          ]

        },
        "emotion": {
          "document": true,
          "targets": [
            "IBM",
            "Watson"
          ]
        },
        "categories": {},
        "concepts": {
          "limit": 8
        },
        "semantic_roles": {
          "entities": true,
          "keywords": true,
          "limit": 50
        },
        "relations": {
          "model": "WKS-model-id"
        }
      }
    }
  }
]
```
{: codeblock}

{{site.data.keyword.discoveryshort}} unterstützt das Hinzufügen von {{site.data.keyword.nlushort}}-Aufbereitungen und von Aufbereitungen für die Elementklassifizierung. Jedes Feld, das Sie aufbereiten wollen, wird durch ein Objekt im Array `enrichments` definiert. Für jedes Aufbereitungsobjekt müssen die Elemente `source_field`, `destination_field` und Aufbereitungen angegeben werden.

- `"enrichment" : string` *(erforderlich)*: Der Typ der Aufbereitung, die für dieses Feld verwendet werden soll. Um {{site.data.keyword.nlushort}}-Aufbereitungen zu extrahieren, verwenden Sie `natural_language_understanding`, zur Ausführung der Elementklassifizierung verwenden Sie `elements`.

  **Hinweis:** Bei Verwendung der Aufbereitung `elements` müssen unbedingt die unter [Elementklassifizierung](/docs/services/discovery/element-classification.html) angegebenen Anleitungen befolgt werden. Insbesondere können nur PDF-Dateien eingepflegt werden, wenn diese Aufbereitung angegeben ist.

- `"source_field" : string` *(erforderlich)*: Das Quellenfeld, das aufbereitet wird. Dieses Feld muss in der Quelle vorhanden sein, nachdem die Operation `json_normalizations` abgeschlossen wurde.
- `"destination_field" : string` *(erforderlich)*: Der Name des Containerobjekts, in dem die Aufbereitungen erstellt werden.

  **Hinweis:** In Ihrer Konfiguration definierte Feldnamen müssen die Rahmenbedingung erfüllen, die im Abschnitt [Anforderungen für Feldnamen](#field_reqs) definiert sind.

### Aufbereitungen für die Elementklassifizierung

Bei Verwendung der Elementklassifizierung muss jedes Aufbereitungsobjekt `elements` ein Objekt `"options": {}` mit den folgenden angegebenen Parametern enthalten:

- `"model" : string` *(erforderlich)*: Das Elementextraktionsmodell, das bei diesem Dokument verwendet werden soll. Gegenwärtig wird das Modell `contract` unterstützt.

**Hinweis:** Bei Verwendung der Aufbereitung `elements` müssen unbedingt die unter [Elementklassifizierung](/docs/services/discovery/element-classification.html) angegebenen Anleitungen befolgt werden. Insbesondere können nur PDF-Dateien eingepflegt werden, wenn diese Aufbereitung angegeben ist.

### Aufbereitungen von Natural Language Understanding (NLU)

Bei Verwendung von {{site.data.keyword.nlushort}} muss jedes Objekt im Array `enrichments` ebenfalls ein Objekt `"options": { "features": { } }` enthalten, das eine oder mehrere der folgenden Aufbereitungen enthält:

### categories

Die Aufbereitung `categories` gibt alle allgemeinen Kategorien im eingepflegten Dokument an. Diese Aufbereitung besitzt keine Optionen und muss als leeres Objekt `"categories" : {}` angegeben werden.

### concepts

Die Aufbereitung `concepts` ermittelt anhand anderer im Text vorhandenen Konzepte und Entitäten diejenigen Konzepte, die dem Eingabetext zugeordnet sind.

- `"limit" : INT` *(erforderlich)*: Die maximale Anzahl von Konzepten, die aus dem eingepflegten Dokument extrahiert werden sollen.

### emotion

Die Aufbereitung `emotion` wertet die emotionale Gesamttendenz, z. B. `anger` (= Wut) eines vollständigen Dokuments oder angegebener Zielzeichenfolgen im gesamten Dokument aus. Diese Aufbereitung kann nur für Inhalt in englischer Sprache verwendet werden.

- `"document" : boolean ` _(optional)_: Beim Wert `true` wird die emotionale Tendenz des gesamten Dokuments ausgewertet.
- `"targets" : array ` _(optional)_: Eine durch Kommas getrennte Liste der Zielzeichenfolgen, deren emotionaler Zustand im Dokument ausgewertet werden soll.

### entities

Die Aufbereitung `entities` extrahiert Instanzen bekannter Entitäten wie Personen, Orte und Organisationen. Optional kann ein angepasstes {{site.data.keyword.knowledgestudioshort}}-Modell angegeben werden, um angepasste Entitäten zu extrahieren.

- `"sentiment" : boolean` _(optional)_: Beim Wert `true` wird für die extrahierte Entität im Kontext des sie umgebenden Inhalts eine Stimmungsanalyse ausgeführt.
- `"emotion" : boolean` _(optional)_: Beim Wert `true` wird eine Emotionstendenzanalyse für die extrahierte Entität im Kontext des sie umgebenden Inhalts ausgeführt.
- `"limit" : INT` _(optional)_: Die maximale Anzahl von Entitäten, die aus dem eingepflegten Dokument extrahiert werden sollen. Der Standardwert ist `50`.
- `"mentions": boolean` _(optional)_: Beim Wert `true` wird aufgezeichnet, wie häufig diese Entität erwähnt ist. Der Standardwert ist `false`.
- `"mention_types": boolean` _(optional)_: Beim Wert `true` wird der Typ der Erwähnung für jede Erwähnung dieser Entität gespeichert. Der Standardwert ist `false`.
- `"sentence_location": boolean` _(optional)_: Beim Wert `true` wird die Position des Satzes für jede Erwähnung der Entität gespeichert. Der Standardwert ist `false`.
- `"model" : string` _(optional)_: Wenn diese Option angegeben ist, wird das angepasste Modell anstelle des öffentlichen Modells verwendet, um Entitäten zu extrahieren. Diese Option macht die Zuordnung eines angepassten {{site.data.keyword.knowledgestudioshort}}-Modells zu Ihrer Instanz von {{site.data.keyword.discoveryshort}} erforderlich. Weitere Informationen finden Sie unter [Integration mit Watson Knowledge Studio](/docs/services/discovery/integrate-wks.html).

### keywords

Die Aufbereitung `keywords` extrahiert Vorkommen von signifikanten Wörtern im Text. Informationen zu den Unterschieden zwischen den Aufbereitungen 'keywords', 'concepts' und 'entities' enthält der Abschnitt [Unterschiede zwischen Entitäten, Konzepten und Schlüsselwörtern](/docs/services/discovery/building.html#udbeck).

- `"sentiment" : boolean` _(optional)_: Beim Wert `true` wird für das extrahierte Schlüsselwort im Kontext des es umgebenden Inhalts eine Stimmungsanalyse ausgeführt.
- `"emotion" : boolean` _(optional)_: Beim Wert `true` wird eine Emotionstendenzanalyse für das extrahierte Schlüsselwort im Kontext des es umgebenden Inhalts ausgeführt.
- `"limit" : INT` _(optional)_: Die maximale Anzahl von Schlüsselwörtern, die aus dem eingepflegten Dokument extrahiert werden sollen. Der Standardwert ist `50`.

### semantic_roles

Die Aufbereitung `semantic_roles` identifiziert Satzkomponenten wie Subjekt, Aktion und Objekt im eingepflegten Text.

- `"entities" : boolean` _(optional)_: Beim Wert `true` werden Entitäten aus den Satzkomponenten extrahiert.
- `"keywords" : boolean` _(optional)_: Beim Wert `true` werden Schlüsselwörter aus den Satzkomponenten extrahiert.
- `"limit" : INT` _(optional)_: Die maximale Anzahl von Objekten des Typs `semantic_roles`, die aus dem eingepflegten Dokument extrahiert werden sollen, also die maximale Anzahl der zu analysierenden Sätze. Der Standardwert ist `50`.

### sentiment

Die Aufbereitung `sentiment` wertet die Gesamtstimmung eines vollständigen Dokuments oder angegebener Zielzeichenfolgen im gesamten Dokument aus.

- `"document" : boolean ` _(optional)_: Beim Wert `true` wird die Stimmung des gesamten Dokuments ausgewertet.
- `"targets" : array ` _(optional)_: Eine durch Kommas getrennte Liste der Zielzeichenfolgen, deren Stimmung im Dokument ausgewertet werden soll.

### relations

Die Aufbereitung `relations` extrahiert bekannte Beziehungen zwischen identifizierten Entitäten im Dokument. Optional kann ein angepasstes {{site.data.keyword.knowledgestudioshort}}-Modell angegeben werden, um angepasste Beziehungen zu extrahieren.

- `"model" : string` _(optional)_: Wenn diese Option angegeben ist, wird das angepasste Modell anstelle des öffentlichen Modells verwendet, um Beziehungen zu extrahieren. Diese Option macht die Zuordnung eines angepassten {{site.data.keyword.knowledgestudioshort}}-Modells zu Ihrer Instanz von {{site.data.keyword.discoveryshort}} erforderlich. Weitere Informationen finden Sie unter [Integration mit Watson Knowledge Studio](/docs/services/discovery/integrate-wks.html).

## Normalisierung
{: #normalization}

Das Array `normalizations` enthält JSON-Objekte des Typs `operation`, die zur Bereinigung der eingepflegten JSON-Daten verwendet werden, nachdem die Aufbereitungen`` angewendet wurden und bevor das Dokument gespeichert wird.

```json
"normalizations": [
  {
    "operation": "remove",
    "source_field": "enriched_title.entities.text"
  },
  {
    "operation": "copy",
    "source_field": "enriched_title.sentiment.document.score",
    "destination_field": "titlescore"
  }
]
```
{:codeblock}

Die Optionen für das Objekt `operation` sind [hier](#operations) aufgelistet.

## Anforderungen an Feldnamen
{: #field_reqs}

Feldnamen dürfen keine Leerzeichen enthalten. Die folgenden Zeichen und Zeichenfolgen sind reserviert und dürfen in Feldnamen nicht verwendet werden:


```
  .  ,  # ? :
  id
  score
  highlight
  result_metadata
```
{: pre}

Die Zeichen `_`, `+` und `-` können nicht als Präfix für `field_name` verwendet werden.

Die numerischen Zeichen `0 - 9` sollten nicht als Suffix eines Feldnamens verwendet werden (z. B. `extracted-content2`). Derartige Feldnamen werden zwar indexiert, können jedoch nicht abgefragt werden.
