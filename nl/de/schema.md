---

copyright:
years: 2018, 2019
lastupdated: "2019-01-15"

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

# Informationen zum Ausgabeschema
{: #output_schema}

Nachdem ein Dokument mit der Elementklassifizierung eingepflegt wurde, stellt der Service eine JSON-Ausgabe in dem folgenden Schema für das Versionsdatum `2018-10-15` oder höher bereit. Die Ausgabe wird in das Objekt `enriched_html_elements` aufgenommen. 

```json
{
  "document": {
    "title": string,
    "html": string,
    "hash": string
  },
  "model_id" : string,
  "model_version" : string,  
  "elements": [
    {
      "location": { 
        "begin": int,
        "end": int
      },
      "text": string,
      "types": [
        {
          "label": { "nature": string, "party": string },
          "provenance_ids": [string, string, ...]
            ...
          ]
        }
        ...
      ],
      "categories": [
        {
          "label": string,
          "provenance_ids": [string, string, ...]
        }
        ...
      ],
      "attributes": [
        {
      	  "type": string,
          "text": string,
          "location": { "begin": int, "end": int }
         }
      ]
    }
    ...
  ],
  "tables": [
    {
      "location" : {
        "begin" : int,
        "end" : int
      },
      "text": string,
      "section_title": {
        "text": string,
        "location": {
          "begin" : int,
          "end" : int
        }
      },
      "table_headers" : [
        {
          "cell_id" : string,
          "location" : {
            "begin" : int,
            "end" : int
          },
          "text" : string,
          "row_index_begin" : int,
          "row_index_end" : int,
          "column_index_begin" : int,
          "column_index_end" : int
        },
        ...
      ],
      "column_headers" : [
        {
          "cell_id" : string,
          "location" : {
            "begin" : int,
            "end" : int
          },
          "text" : string,
          "text_normalized" : string,
          "row_index_begin" : int,
          "row_index_end" : int,
          "column_index_begin" : int,
          "column_index_end" : int
        },
        ...
      ],
      "row_headers" : [
        {
          "cell_id" : string,
          "location" : {
            "begin" : int,
            "end" : int
          },
          "text" : string,
          "text_normalized" : string,
          "row_index_begin" : int,
          "row_index_end" : int,
          "column_index_begin" : int,
          "column_index_end" : int
        },
        ...
      ],
      "body_cells" : [
        {
          "cell_id" : string,
          "location" : {
            "begin" : int,
            "end" : int
          },
          "text" : string,
          "row_index_begin" : int,
          "row_index_end" : int,
          "column_index_begin" : int,
          "column_index_end" : int,
          "row_header_ids": [ string ],
          "row_header_texts": [ string ],
          "row_header_texts_normalized": [ string ],
          "column_header_ids": [ string ],
          "column_header_texts": [ string ],
          "column_header_texts_normalized": [ string ],
          "attributes" : [
             {
               "type" : string,
               "text" : string,
               "location" : {
                 "begin" : int,
          "end" : int
        }
             },
             ...
           ]
        },
        ...
      ]
    },
    ...
  ],
  "document_structure": {
    "section_titles": [
      {
        "text": string,
        "location": {
          "begin": int,
          "end": int
        },
        "level": int,
        "element_locations": [
          {
            "begin": int,
            "end": int
          },
          ...
        ]
      },
      ...
    ],
    "leading_sentences": [
      {
        "text": string,
        "location": {
          "begin": int,
          "end": int
        },
        "element_locations": [
          {
            "begin": int,
            "end": int
          },
          ...
        ]
      },
      ...
    ]
  },
  "parties": [
    {
      "party": string,
      "role": string,
      "importance": string,
      "addresses": [
        {
          "text": string,
          "location": {
            "begin": int,
            "end": int
          }
        },
        ...
      ],
      "contacts": [
        {
          "name": string,
          "role": string 
        },
        ...
      ]
    },
    ...
  ],
  "effective_dates": [
    {
      "text": string,
      "confidence_level": string,
      "location": { "begin": int, "end": int }
     },
     ...
  ],
  "contract_amounts": [
    {
      "text": string,
      "confidence_level": string,      
      "location": { "begin": int, "end": int }
    },
    ...
  ],
  "termination_dates": [
    {
      "text": string,
      "confidence_level": string,      
      "location": { "begin": int, "end": int }
    },
    ...
  ]
}
```
{: codeblock}

Das Schema ist wie folgt angeordnet.

  - `document`: Ein Objekt, in dem grundlegende Informationen zum Dokument aufgelistet sind, darunter:
    - `title`: Der Dokumenttitel, falls gefunden.
    - `html`: Der vollständige Text des Eingabedokuments im HTML-Format.
    - `hash`: Der MD5-Hashwert für das Eingabedokument.
  - `model_id`: Das Analysemodell, das vom Service verwendet werden soll. Für die Methoden `/v1/element_classification` und `/v1/comparison` ist der Standardwert `contracts`. Für die Methode `/v1/tables` ist der Standardwert `tables`. Diese Standardwerte gelten für die eigenständigen Methoden und ihre Verwendung in Anforderungen zur Stapelverarbeitung.
  - `model_version`: Die Version des Analysemodells, die durch den Wert des Parameters `modell_id` angegeben wird.
  - `elements`: Ein Array mit den Dokumentelementen, die vom Service erkannt wurden.
    - `location`: Die Position des Elements, die durch die Indizes `begin` und `end` definiert wird.
    - `text`: Der Text des Elements.
    - `types`: Ein Array, das die Art des Elements und dessen Auswirkungen beschreibt.
      - `label`: Ein Objekt, dass den Typ anhand eines Paares definiert, das sich aus den folgenden Elementen zusammensetzen kann:
        - `nature`: Der Typ der Aktion, der für den Satz erforderlich ist. Die aktuellen Werte sind `Definition`, `Haftungsausschluss`, `Ausschluss`, `Verpflichtung` und `Recht`.
        - `party`: Eine Zeichenfolge, die die Partei angibt, auf die der Satz anwendbar ist.
      - `provenance_ids`: Ein Array aus einem oder mehreren Hashwerten, die Sie an IBM senden können, um Feedback zu geben oder Unterstützung zu erhalten.
    - `categories`: Ein Array, in dem die funktionalen Kategorien aufgelistet sind, in die das Element fällt; in anderen Worten, der Inhalt des Elements.
      - `label`: Eine Zeichenfolge, die die angegebene Kategorie auflistet. Eine Liste der [Kategorien](/docs/services/discovery?topic=discovery-contract_parsing#contract_categories) finden Sie im Abschnitt mit den [Informationen zum Parsen von Verträgen](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing).
      - `provenance_ids`: Ein Array aus einem oder mehreren Hashwerten, die Sie an IBM senden können, um Feedback zu geben oder Unterstützung zu erhalten.
    - `Attribute`: Ein Array, das Dokumentattribute angibt. Jedes Objekt in dem Array besteht aus drei Elementen:
      - `type`: Der Typ des Attributs. Mögliche Werte sind `Address`, `Currency`, `DateTime`, `Location`, `Organization` und `Person`.
      - `text`: Der Text, der dem Attribut zugeordnet ist.
      - `location`: Die Position des Attributs, die durch die Indizes `begin` und `end` definiert wird.
  - `tables`\*: Ein Array, das die Tabellen definiert, die im Eingabedokument angegeben sind.
    - `location`: Die Position der aktuellen Tabelle, die durch die Indizes `begin` und `end` im Eingabedokument definiert wird.
    - `text`: Der textuelle Inhalt der aktuellen Tabelle aus dem Eingabedokument ohne zugeordneten Markup-Inhalt.
    - `section_title`: Falls angegeben, die Position eines Abschnittstitels, der in der aktuellen Tabelle enthalten ist. Leer, wenn kein Abschnittstitel angegeben ist.
      - `text`: Der Text für den angegebenen Abschnittstitel.
      - `location`: Die Position des Abschnittstitels im Eingabedokument, die durch die Indizes `begin` und `end` definiert wird.
    - `table_headers`: Ein Array von Zellen auf Tabellenebene, die als Überschriften auf alle anderen Zellen der aktuellen Tabelle angewendet werden können. Jede Tabellenüberschrift ist als Sammlung der folgenden Elemente definiert:
      - `cell_id`: Zeichenfolgewert im Format `tableHeader-x-y`. Dabei stehen `x` und `y` für den Anfang und das Ende der Offsets des Zellenwerts im ursprünglichen Eingabedokument.
      - `location`: Die Position der Zelle im Eingabedokument, die durch die Indizes `begin` und `end` definiert wird.
      - `text`: Der textuelle Inhalt der Zelle aus dem Eingabedokument ohne zugeordneten Markup-Inhalt.
      - `row_index_begin`: Der Index `begin` der Position von `row` der Zelle in der aktuellen Tabelle.
      - `row_index_end`: Der Index `end` der Position von `row` der Zelle in der aktuellen Tabelle.
      - `column_index_begin`: Der Index `begin` der Position von `column` der Zelle in der aktuellen Tabelle.
      - `column_index_end`: Der Index `end` der Position von `column` der Zelle in der aktuellen Tabelle.
    - `column_headers`: Ein Array von Zellen auf Spaltenebene, wobei jede dieser Zellen als Überschrift für andere Zellen in der selben Spalte der aktuellen Tabelle angewendet werden kann. Jede Spaltenüberschrift ist als Sammlung der folgenden Elemente definiert:
      - `cell_id`: Ein Zeichenfolgewert im Format `columnHeader-x-y`. Dabei stehen `x` und `y` für den Anfang und das Ende der Offsets dieser Zelle für Spaltenüberschriften im Eingabedokument.
      - `location`: Die Position der Zelle im Eingabedokument, die durch die Indizes `begin` und `end` definiert wird.
      - `text`: Der textuelle Inhalt der Zelle aus dem Eingabedokument ohne zugeordneten Markup-Inhalt.
      - `text_normalized`: Wenn Sie eine Anpassungseingabe bereitstellen, ist dies die normalisierte Version des Zellentexts entsprechend der Anpassung; andernfalls ist dies der gleiche Wert wie für `text`. 
      - `row_index_begin`: Der Index `begin` der Position von `row` der Zelle in der aktuellen Tabelle.
      - `row_index_end`: Der Index `end` der Position von `row` der Zelle in der aktuellen Tabelle.
      - `column_index_begin`: Der Index `begin` der Position von `column` der Zelle in der aktuellen Tabelle.
      - `column_index_end`: Der Index `end` der Position von `column` der Zelle in der aktuellen Tabelle.
    - `row_headers`: Ein Array von Zellen auf Zeilenebene, wobei jede dieser Zellen als Überschrift für andere Zellen in der selben Zeile der aktuellen Tabelle angewendet werden kann. Jede Zeilenüberschrift ist als Sammlung der folgenden Elemente definiert:
      - `cell_id`: Ein Zeichenfolgewert im Format `rowHeader-x-y`. Dabei stehen `x` und `y` für den Anfang und das Ende der Offsets dieser Zelle für Zeilenüberschriften im Eingabedokument.
      - `location`: Die Position der Zelle im Eingabedokument, die durch die Indizes `begin` und `end` definiert wird.
      - `text`: Der textuelle Inhalt der Zelle aus dem Eingabedokument ohne zugeordneten Markup-Inhalt.
      - `text_normalized`: Wenn Sie eine Anpassungseingabe bereitstellen, ist dies die normalisierte Version des Zellentexts entsprechend der Anpassung; andernfalls ist dies der gleiche Wert wie für `text`. 
      - `row_index_begin`: Der Index `begin` der Position von `row` der Zelle in der aktuellen Tabelle.
      - `row_index_end`: Der Index `end` der Position von `row` der Zelle in der aktuellen Tabelle.
      - `column_index_begin`: Der Index `begin` der Position von `column` der Zelle in der aktuellen Tabelle.
      - `column_index_end`: Der Index `end` der Position von `column` der Zelle in der aktuellen Tabelle.
    - `body_cells`: Ein Array von Zellen der aktuellen Tabelle, die weder Zellen für Tabellenüberschriften noch Zellen für Spalten- oder Zeilenüberschriften sind, mit entsprechenden Zuordnungen für die Zeilen- und Spaltenüberschriften. Jede Textzelle ist als Sammlung der folgenden Elemente definiert:
      - `cell_id`: Ein Zeichenfolgewert im Format `bodyCell-x-y`. Dabei stehen `x` und `y` für den Anfang und das Ende der Offsets dieser Textzelle im Eingabedokument.
      - `location`: Die Position der Zelle im Eingabedokument, die durch die Indizes `begin` und `end` definiert wird.
      - `text`: Der textuelle Inhalt der Zelle aus dem Eingabedokument ohne zugeordneten Markup-Inhalt.
      - `row_index_begin`: Der Index `begin` der Position von `row` der Zelle in der aktuellen Tabelle.
      - `row_index_end`: Der Index `end` der Position von `row` der Zelle in der aktuellen Tabelle.
      - `column_index_begin`: Der Index `begin` der Position von `column` der Zelle in der aktuellen Tabelle.
      - `column_index_end`: Der Index `end` der Position von `column` der Zelle in der aktuellen Tabelle.
      - `row_header_ids`: Ein Array mit Werten, wobei jeder Wert der Wert `cell_id` einer Zeilenüberschrift ist, der auf diese Textzelle anwendbar ist.
      - `row_header_texts`: Ein Array mit Werten, wobei jeder Wert der Wert `text` einer Zeilenüberschrift ist, der auf diese Textzelle anwendbar ist.
      - `row_header_texts_normalized`: Wenn Sie eine Anpassungseingabe bereitstellen, ist dies die normalisierte Version des Text der Zeilenüberschrift entsprechend der Anpassung; andernfalls ist dies der gleiche Wert wie für `row_header_texts`. 
      - `column_header_ids`: Ein Array mit Werten, wobei jeder Wert der Wert `cell_id` einer Spaltenüberschrift ist, der auf diese Textzelle anwendbar ist.
      - `column_header_texts`: Ein Array mit Werten, wobei jeder Wert der Wert `text` einer Spaltenüberschrift ist, der auf diese Textzelle anwendbar ist.
      - `column_header_texts_normalized`: Wenn Sie eine Anpassungseingabe bereitstellen, ist dies die normalisierte Version des Text der Spaltenüberschrift entsprechend der Anpassung; andernfalls ist dies der gleiche Wert wie für `column_header_texts`.
      - `Attribute`: Ein Array, das Dokumentattribute angibt. Jedes Objekt in dem Array besteht aus drei Elementen:
        - `type`: Der Typ des Attributs. Mögliche Werte sind `Address`, `Currency`, `DateTime`, `Location`, `Organization` und `Person`.
        - `text`: Der Text, der dem Attribut zugeordnet ist.
        - `location`: Die Position des Attributs, die durch die Indizes `begin` und `end` definiert wird.
  - `document_structure`: Ein Objekt, das die Struktur des Eingabedokuments beschreibt.
    - `section_titles`: Ein Array, das ein Objekt pro Abschnitt oder Unterabschnitt enthält, der im Eingabedokument erkannt wurde. Schnitte und Unterabschnitte sind nicht ineinander verschachtelt. Sie sind flach angeordnet und können mit den Werten für `begin` und `end` des Elements und dem Wert für `level` des Abschnitts wieder zurück in die richtige Reihenfolge gebracht werden.
      - `text`: Eine Zeichenfolge, die den Abschnittstitel auflistet (falls gefunden).
      - `location`: Die Position des Titels im Eingabedokument, die durch die Indizes `begin` und `end` definiert wird.
      - `level`: Eine ganze Zahl, die die Ebene angibt, auf der sich der Abschnitt im Eingabedokument befindet. Sie stellt z. B. einen Abschnitt der höchsten Ebene oder einen Unterabschnitt innerhalb des Abschnitts 'level' dar.
      - `element_locations`: Ein Array, das die Werte für `begin` und `end` der Sätze im Abschnitt angibt.
    - `leading_sentences`: Ein Array, das ein Objekt pro Abschnitt oder Unterabschnitt enthält (parallel zum Array `section_titles`) und das die führenden Sätze im entsprechenden Abschnitt oder Unterabschnitt detailliert beschreibt. Wie im Array `section_titles` sind die Objekte nicht verschachtelt; stattdessen sind sie flach angeordnet und können mit den Werten für `begin` und `end` des Elements oder eine Ebenenmarke im Eingabedokument wieder in eine gewünschte Reihenfolge gebracht werden.
      - `text`: Eine Zeichenfolge, die den führenden Satz auflistet (falls gefunden).
      - `location`: Die Position des führenden Satzes im Eingabedokument, die durch die Indizes `begin` und `end` definiert wird.
      - `element_locations`: Ein Array, das die Werte für `begin` und `end` der führenden Sätze im Abschnitt angibt.
  - `parties`: Ein Array, das die vom Service angegebenen Parteien definiert.
    - `party`: Ein Zeichenfolgewert, der die Partei angibt.
    - `role`: Ein Zeichenfolgewert, der die Rolle der Partei angibt.
    - `importance`: Ein Zeichenfolgewert, der die Wichtigkeit der Partei angibt. Mögliche Werte sind `Primary` für eine Primärpartei oder `Unknown` für eine Nicht-Primärpartei.
    - `addresses`: Ein Array von Objekten, die Adressen angeben.
      - `text`: Eine Zeichenfolge, die die Adresse enthält.
      - `location`: Die Position der Adresse, die durch die Indizes `begin` und `end` definiert wird.
    - `contacts`: Ein Array, das den Namen und die Rolle von Kontakten definiert, die im Eingabedokument angegeben sind.
      - `name`: Eine Zeichenfolge, die den Namen eines angegebenen Kontakts auflistet.
      - `role`: Eine Zeichenfolge, die die Rolle des angegebenen Kontakts auflistet.  
  - `effective_dates`: Ein Array, das die Gültigkeitsdaten des Dokuments angibt.
    - `text`: Ein Gültigkeitsdatum, das als Zeichenfolge aufgelistet ist.
    - `confidence_level`: Das Konfidenzniveau für die Angabe des Gültigkeitsdatums. Mögliche Werte sind `High`, `Medium` und `Low`.
    - `location`: Die Position des Datums, die durch die Indizes `begin` und `end` definiert ist.
  - `contract_amounts`: Ein Array, das die im Dokument identifizierten Geldbeträge angibt.
    - `text`: Ein Vertragsbetrag, der als Zeichenfolge aufgelistet ist.
    - `confidence_level`: Das Konfidenzniveau für die Angabe des Vertragsbetrags. Mögliche Werte sind `High`, `Medium` und `Low`.    
    - `location`: Die Position des Betrags oder der Beträge, die durch die Indizes `begin` und `end` definiert wird.
  - `termination_dates`: Ein Array, das die Datumsangaben für die Beendigung des Dokuments angibt.
    - `text`: Ein Beendigungsdatum, das als Zeichenfolge aufgelistet ist.
    - `confidence_level`: Das Konfidenzniveau für die Angabe des Beendigungsdatums. Mögliche Werte sind `High`, `Medium` und `Low`.    
    - `location`: Die Position des Datums, die durch die Indizes `begin` und `end` definiert ist.

**\*Hinweise zu Tabellen:**
  - Zeilen- und Spaltenindexwerte pro Zelle sind auf null gesetzt und beginnen daher mit `0`.
  - Mehrere Werte in Arrays der Elemente `row_header_ids` und `row_header_texts` zeigen eine mögliche Hierarchie von Zeilenüberschriften an.
  - Mehrere Werte in Arrays der Elemente `column_header_ids` und `column_header_texts` zeigen eine mögliche Hierarchie von Spaltenüberschriften an.
