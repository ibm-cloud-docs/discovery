---

copyright:
  years: 2015, 2018, 2019
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

# Elementklassifizierung
{: #element-classification}

Die Elementklassifizierung ermöglicht eine schnelle Analyse von maßgeblichen Dokumenten, um relevante Elemente zu konvertieren, zu identifizieren und zu klassifizieren. Mittels hochmoderner Verarbeitung natürlicher Sprache werden die Partei (der Bezug), die Gattung (der Typ des Elements) und die Kategorie (spezifische Klasse) aus Elementen eines Dokuments extrahiert.

Die Konzeption der Elementklassifzierung stellt die folgende Funktionalität bereit:

-  Interpretation natürlicher Sprache für Verträge mit Schwerpunkt auf Softwarebeschaffungsverträgen
-  Möglichkeit zur Konvertierung von programmorientiertem PDF-Format in annotiertes JSON-Format
-  Identifizierung von juristischen Personen und Kategorien in Ausrichtung an Expertenwissen

Die Elementklassifizierung verbindet eine funktionsreiche Gruppe von integrierten automatisierten Watson-APIs zur Eingabe einer programmorientierten PDF-Datei, zur Erkennung von Abschnitten, Listen (nummerierte Listen und Aufzählungen), Fußnoten und Tabellen und zur Konvertierung dieser Elemente in ein strukturiertes HTML-Format. Darüber hinaus wird die Klassifizierung dieses strukturierten Formats als JSON-Fomat mit gekennzeichneten Elementen, Typen und Kategorien annotiert und ausgegeben.

Die Elementklassifizierung überträgt Ihre Daten auf sichere Weise, da die Daten sowohl bei der Übertragung als auch im ruhenden Zustand verschlüsselt sind. Informationen zur Sicherheit bei IBM Cloud finden Sie in der [Servicebeschreibung zu {{site.data.keyword.Bluemix_notm}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=%28IBM+Cloud+Service+description%29){: new_window}

Die Elementklassifizierung gibt ein JSON-Objekt zurück, das Folgendes enthält:

-  Ein Objekt des Typs `documents`, das den Titel des Eingabedokuments, eine HTML-Version des Eingabedokuments und den MD5-Hashwert des Eingabedokuments enthält.
-  Informationen zu dem Modell, das zum Klassifizieren des Eingabedokuments verwendet wird.  
-  Ein Array des Typs `elements`, das im Eingabedokument angegebene semantische Elemente aufführt.
-  Ein Array des Typs `tables`, das die im Eingabedokument angegebenen Tabellen aufgliedert.
-  Ein Objekt des Typs `document_structure`, in dem Abschnittstitel und führende Sätze aufgelistet sind, die im Eingabedokument angegeben sind.
-  Ein Array des Typs `parties`, in dem die Parteien, Rollen, Adressen und Kontakte von Parteien aufgelistet sind, die im Eingabedokument angegeben sind.
-  Arrays, die `effective_dates`,`contract_amounts` und `termination_dates` definieren.

Dieses Beta-Feature wird derzeit nur in Englisch unterstützt. Details hierzu finden Sie unter [Sprachunterstützung](/docs/services/discovery?topic=discovery-language-support#feature-support).


## Voraussetzungen der Klassifizierung
{: #element-class}

Damit Dokumente mithilfe der Elementklassifizierung klassifiziert werden können, müssen Ihre Konfiguration und die Quellendokumente die folgenden Voraussetzungen erfüllen:

-  Die zu analysierenden Dateien müssen im PDF-Format vorliegen.
-  Der PDF-Inhalt liegt im Textformat vor. Dokumente, die gescannt wurden, können nicht geparst werden, selbst wenn sie mit OCR (einer automatisierten Texterkennung) verarbeitet wurden.
   **Hinweis:** Ob eine PDF-Datei im Textformat vorliegt, können Sie ermitteln, indem Sie das Dokument in einer PDF-Anzeigefunktion öffnen und mit dem Tool **Textauswahl** ein einzelnes Wort auswählen. Falls Sie kein einzelnes Wort im Dokument auswählen können, kann die Datei nicht analysiert werden.
-  Die Dateien sind nicht größer als 50 MB.
-  Geschützte (also nur mit einem Kennwort zu öffnende) PDF-Dateien sowie PDF-Dateien mit eingeschränkter Bearbeitung (bei denen zur Bearbeitung ein Kennwort erforderlich ist) können nicht analysiert werden.
-  Die {{site.data.keyword.discoveryshort}}-Tools enthalten eine Konfiguration mit dem Namen **Standardvertragskonfiguration**, die verwendet werden kann, um Ihre Sammlung von PDF-Dokumenten aufzubereiten. Sie haben auch die Möglichkeit, eine angepasste Konfiguration zu erstellen, die die Aufbereitung für `elements` enthält. Weitere Informationen finden Sie unter [Voraussetzungen für die Datensammlung](/docs/services/discovery?topic=discovery-element-classification#element-collection).
-  Bei **Lite**-Plänen können maximal 500 Seiten pro Monat verarbeitet werden.
-  Nicht verfügbar in **Dedicated**-Umgebungen.
-  Die Normalisierung nach der Aufbereitung kann bei Verwendung der Elementklassifizierung nicht ausgeführt werden.

**Hinweis:** Die Datei für die **Standardvertragskonfiguration** wurde am 25. September 2018 aktualisiert. Wenn Sie diese Konfiguration vor diesem Datum auf eine Sammlung angewendet haben, finden Sie in den [Releaseinformationen](/docs/services/discovery?topic=discovery-release-notes#25sept) die Informationen zum Aktualisieren Ihrer Sammlung.

## Voraussetzungen für die Datensammlung
{: #element-collection}

Damit die Elementklassifizierung verwendet werden kann, muss Ihre Sammlung so konfiguriert sein, dass sie bestimmten Anforderungen entspricht.

Die {{site.data.keyword.discoveryshort}}-Tools enthalten eine Konfiguration mit dem Namen **Standardvertragskonfiguration**, die vorkonfiguriert wurde, um PDF-Dokumente mit der Aufbereitung **Elementklassifizierung** und anderen erforderlichen Optionen aufzubereiten. Sie können diese Konfiguration auswählen, wenn Sie Ihre Sammlung erstellen. Das JSON für diese Konfiguration lautet:

```json
 {
   "name": "Standardvertragskonfiguration",
   "description": "Werte für 'party', 'nature' und 'category' aus Elementen in PDFs extrahieren.",
  "conversions": {
     "html": {
       "exclude_tags_completely": [],
       "exclude_tags_keep_content": []
     }
   },
   "enrichments": [
     {
       "source_field": "html",
       "destination_field": "enriched_html_elements",
       "enrichment": "elements",
       "options": {
         "model": "contract"
    }
     }
   ]
 }
```
{: codeblock}

Falls Sie eine angepasste Konfigurationsdatei erstellen möchten, konfigurieren Sie Ihre Sammlung so, dass sie die folgenden Anforderungen erfüllt:  

-  `PDF`-Konvertierungseinstellungen werden ignoriert, falls sie angegeben sind.
-  `WORD`-Konvertierungseinstellungen können übergangen werden, da Microsoft Word-Dateien nicht eingepflegt werden können, wenn die Elementklassifizierung angegeben ist.
-  `HTML`-Normalisierungseinstellungen werden ignoriert, falls sie angegeben sind.
-  Die Dokumentsegmentierung wird nicht unterstützt, wenn die Aufbereitung für Elemente (`elements`) angegeben ist.
-  In der {{site.data.keyword.discoveryshort}}-Konfiguration muss das Feld `html` durch die Aufbereitung `elements` aufbereitet werden und für `model` die Einstellung `contract` angegeben sein. Im folgenden Beispiel gilt für `destination_field` die Bezeichnung `enriched_html`; es kann jedoch jeder beliebige gültige Name verwendet werden:

```json
 "enrichments": [
   {
     "source_field": "html",
    "destination_field": "enriched_html",
    "enrichment": "elements",
    "options": {
       "model": "contract"
    }
   }
 ]
```
{: codeblock}

Nachdem Sie die `Standardvertragskonfiguration` in den Tools ausgewählt haben, können Sie Ihre Dokumente hochladen. Falls Sie keine Erfahrungen mit dem Erstellen von Sammlungen und dem Hochladen von Dokumenten besitzen, finden Sie unter [Einführung in die Tools](/docs/services/discovery?topic=discovery-getting-started#getting-started) entsprechende Informationen.

## Klassifizierte Elemente
{: #classified-elements}

Nachdem ein Dokument mit der Elementklassifizierung klassifiziert wurde, wird es mit einem Array `elements` als Teil des durchsuchbaren Dokuments zurückgegeben.

Jedes Objekt im Array `elements` beschreibt ein Element des Vertrages, das von {{site.data.keyword.discoveryshort}} erkannt wurde. Der folgende Code stellt ein typisches Element dar:

```json
 {
    "location" : {
     "begin" : 134323,
     "end" : 135109
    },
    "text" : "9. In the event that the Participant's total vested account balance is determined to be less than or equal to $2,000.00 as of the date that the Order is received, the parties will be informed in writing that the QDRO determination fee may potentially liquidate the account.",
   "types" : [ {
      "label" : {
        "nature" : "Obligation",
        "party" : "All Parties"
      },
      "provenance_ids" : ["Nlu0ogWAEGms4vjhhzpMv3iXhm8b8fBqMBNtT/bXH8JI=", "PlyERkjg5is36RpFjVUFXp69eDmGmCxLCXRs1sDMDUCo="
      ]
    } ],
   "categories" : [ {
      "label" : "Communication",
      "provenance_ids" : [ "Cs38YyU6VBFtJK1/bgtEJBlqqWmX5F6OYUciRxQXf7HrN5TOCPuI7QXbkbj4LRXoxVuB3/i9H15q5TU+vFxorhUBeWFfF998OYQiPYViD2yI="
      ]
    } ],
    "attributes" : [ {
      "type" : "Currency",
      "text" : "$2,000.00",
      "location" : {
        "begin" : 134780,
        "end" : 134789
      }
    } ]
 }
 ```
{: codeblock}

Jedes Element verfügt über fünf wichtige Abschnitte:
-  `location`: Die Indizes `begin` und `end`, die die Position des Elements im Eingabedokument angeben.
-  `text`: Der Text des klassifizierten Elements.
-  `types`: Ein Array, das null oder mehr Objekte des Typs `label` enthält. Jedes `label`-Objekt enthält ein Feld `nature`, das die Auswirkung des Elements auf die angegebene Partei (z. B. `Right` oder `Exclusion`) aufführt, und ein Feld `party`, das die vom Element betroffenen Parteien oder Parteien angibt. Weitere Informationen finden Sie unter [types](/docs/services/discovery?topic=discovery-contract_parsing#contract_types) im Abschnitt mit den [Informationen zum Parsing von Verträgen](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing).
-  `categories`: Ein Array, das null oder mehr Objekte des Typs `label` enthält. Der Wert jedes Objekts `label` gibt eine funktionale Kategorie an, in die das angegebene Element fällt. Weitere Informationen finden Sie unter [Kategorien](/docs/services/discovery?topic=discovery-contract_parsing#contract_categories) im Abschnitt mit den [Informationen zum Parsing von Verträgen](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing).
-  `attribute`: Ein Array, das null oder mehr Objekte auflistet, die Attribute des Elements definieren. Zu den gegenwärtig unterstützten Attributtypen zählen `Location` (geografische Position, auf die durch das Element verwiesen wird), `DateTime` (Datum, Uhrzeit, Datumsbereich oder Zeitbereich, der/die durch das Element angegeben wird) und `Currency` (Währungswerte und -einheiten). Jedes Objekt im Array `attributes` enthält auch den Text und die Position des identifizierten Elements. Die Position wird durch die Indizes `begin` und `end` des Texts im Eingabedokument definiert. Weitere Informationen finden Sie unter [Attribute](/docs/services/discovery?topic=discovery-contract_parsing#attributes) in [Parsing von Verträgen](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing).

Darüber hinaus enthält jedes Objekt in den Arrays `types` und `categories` ein Array des Typs `provenance_ids`. Die im Array `provenance_ids` aufgelisteten Werte sind Hashwerte, die Sie an IBM senden können, um Feedback zu geben oder Unterstützung für den Teil der Analyse zu erhalten, der sich auf das Element bezieht. 

Einige Sätze fallen unter keinen Typ und keine Kategorie. In diesem Fall werden die Arrays `types` und `categories` vom Service als leere Objekte zurückgegeben.
{: note}

Einige Sätze decken mehrere Themen ab. In diesem Fall gibt der Service mehrere Gruppen von Objekten der Typen `types` und `categories` zurück.
{: note}

Einige Sätze enthalten keine identifizierbaren Attribute. In diesem Fall gibt der Service das Array `attributes` als leeres Objekt zurück.
{: note}
