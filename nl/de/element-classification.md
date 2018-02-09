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

# Elementklassifizierung
{: #element-classification}

Die Elementklassifizierung ermöglicht eine schnelle Analyse von maßgeblichen Dokumenten, um relevante Elemente zu konvertieren, zu identifizieren und zu klassifizieren. Mittels hochmoderner Verarbeitung natürlicher Sprache werden die Partei (der Bezug), die Gattung (der Typ des Elements) und die Kategorie (spezifische Klasse) aus Elementen eines Dokuments extrahiert.

Die Konzeption der Elementklassifzierung stellt die folgende Funktionalität bereit:

- Interpretation natürlicher Sprache für Verträge mit Schwerpunkt auf Softwarebeschaffungsverträgen und behördlichen Dokumenten
- Möglichkeit zur Konvertierung von programmorientiertem PDF-Format in annotiertes JSON-Format
- Identifizierung von juristischen Personen und Kategorien in Ausrichtung an Expertenwissen

Die Elementklassifizierung verbindet eine funktionsreiche Gruppe von integrierten automatisierten Watson-APIs zur Eingabe einer programmorientierten PDF-Datei, zur Erkennung von Abschnitten, Listen (nummerierte Listen und Aufzählungen), Fußnoten und Tabellen und zur Konvertierung dieser Elemente in ein strukturiertes HTML-Format. Darüber hinaus wird die Klassifizierung dieses strukturierten Formats als JSON-Fomat mit gekennzeichneten Elementen, Typen und Kategorien annotiert und ausgegeben.

Die Elementklassifizierung überträgt Ihre Daten auf sichere Weise, da die Daten sowohl bei der Übertragung als auch im ruhenden Zustand verschlüsselt sind. Informationen zur Sicherheit bei IBM Cloud finden Sie unter [IBM Cloud Service Description ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=IBM+Bluemix+Service+Description){: new_window}.

## Voraussetzungen der Klassifizierung

Damit Dokumente mithilfe der Elementklassifizierung klassifiziert werden können, müssen Ihre Konfiguration und die Quellendokumente die folgenden Voraussetzungen erfüllen:

- Die zu analysierenden Dateien müssen im PDF-Format vorliegen.
- Der PDF-Inhalt liegt im Textformat vor (gescannte, jedoch nicht mit OCR, also einer automatisierten Texterkennung, verarbeitete Dokumente können nicht analysiert werden).

  **Hinweis:** Ob eine PDF-Datei im Textformat vorliegt, können Sie ermitteln, indem Sie das Dokument in einer PDF-Anzeigefunktion öffnen und mit dem Tool **Textauswahl** ein einzelnes Wort auswählen. Falls Sie kein einzelnes Wort im Dokument auswählen können, kann die Datei nicht analysiert werden.

- Die Dateien sind nicht größer als 50 MB.
- Geschützte (also nur mit einem Kennwort zu öffnende) PDF-Dateien sowie PDF-Dateien mit eingeschränkter Bearbeitung (bei denen zur Bearbeitung ein Kennwort erforderlich ist) können nicht analysiert werden.
- Es muss eine angepasste {{site.data.keyword.discoveryshort}}-Konfiguration erstellt werden, die die Aufbereitung für Elemente (`elements`) enthält. Diese Konfiguration kann nur zum Einpflegen von PDF-Dokumenten verwendet werden.
- Bei **Lite**- und **Standard**-Plänen können maximal 500 Seiten pro Monat verarbeitet werden.
- Bei Serviceinstanzen, die den **Premium**-Plan abonniert haben, ist diese Funktionalität nicht verfügbar.

## Voraussetzungen für die Datensammlung

Damit die Elementklassifizierung verwendet werden kann, muss Ihre Datensammlung so konfiguriert sein, dass sie bestimmte Anforderungen erfüllt:

- `PDF`-Konvertierungseinstellungen werden ignoriert, falls sie angegeben sind.
- `WORD`-Konvertierungseinstellungen können übergangen werden, da Microsoft Word-Dateien nicht eingepflegt werden können, wenn die Elementklassifizierung angegeben ist.
- `HTML`-Normalisierungseinstellungen werden ignoriert, falls sie angegeben sind.
- Die Dokumentteilung wird nicht unterstützt, wenn die Aufbereitung für Elemente (`elements`) angegeben ist.
- In der {{site.data.keyword.discoveryshort}}-Konfiguration muss das Feld `html` durch die Aufbereitung `elements` aufbereitet werden und für `model` die Einstellung `contract` angegeben sein. Im folgenden Beispiel gilt für `destination_field` die Bezeichnung `enriched_html`; es kann jedoch jeder beliebige gültige Name verwendet werden:

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

Diese Optionen können mithilfe der {{site.data.keyword.discoveryshort}}-Tools hinzugefügt werden. Erstellen Sie eine angepasste Konfiguration und fügen Sie die Aufbereitung für die **Elementklassifizierung** zum Feld `html` hinzu.

**Hinweis:** Wenn die **Elementklassifizierung** mithilfe der Tools hinzugefügt wird, wird für `destination_field` der Wert `enriched_html_elements` festgelegt.

Nachdem die angepasste Konfiguration erstellt wurde, kann sie in jeder beliebigen Datensammlung verwendet werden. Zum Hochladen von Dokumenten kann eine beliebige Methode verwendet werden, solange die angepasste Konfiguration angegeben ist. Falls Sie keine Erfahrungen mit dem Erstellen von Sammlungen und dem Hochladen von Dokumenten besitzen, finden Sie unter [Einführung in die Tools](/docs/services/discovery/getting-started-tool.html) entsprechende Informationen.

## Klassifizierte Elemente

Nachdem ein Dokument mit der Elementklassifizierung klassifiziert wurde, wird es mit einem Array `elements` als Teil des durchsuchbaren Dokuments zurückgegeben.

Jedes Objekt im Array `elements` beschreibt ein Element des Vertrages, das von der Elementklassifizierung erkannt wurde. Der folgende Code stellt ein typisches Element dar:

```
{
   "sentence" : {
     "begin" : 34941,
     "end" : 35307
   },
   "sentence_text" : "A buyer must buy from the supplier.",
   "types" : [ {
     "label" : {
       "nature" : "Obligation",
       "party" : "Supplier"
     },
     "assurance" : "High"
   } ],
   "categories" : [ {
     "label : "Responsibilities",
     "assurance : "High"
     }
   ]
}
```

Für das Element gibt es vier wichtige Abschnitte:

- `sentence_text`: Der analysierte Text.
- `sentence`: Dieses Objekt beschreibt, wo das Element im konvertierten HTML-Dokument gefunden wurde. Es enthält einen Wert für das Anfangszeichen und einen Wert für das Endzeichen.
- `types`: Dieses Array beschreibt, worum es sich bei dem Element handelt und was von ihm beeinflusst wird. Es besteht aus einer oder mehreren Gruppen `party` (durch den Satz betroffen) und `nature` (Auswirkung des Satzes auf die erkannte Partei).
- `categories`: Dieses Array listet die funktionalen Kategorien auf, in die der erkannte Satz fällt. Es gibt den Inhalt des Satzes an.

**Hinweis**: Einige Sätze fallen unter keinen Typ oder unter keine Kategorie. In diesem Fall werden die Arrays `types` und `categories` leer zurückgegeben.

**Hinweis**: Einige Sätze decken mehrere Themen ab und werden daher mit mehreren aufgelisteten Elementen `types` und `categories` zurückgegeben.

Alle erkannten Parteien werden außerdem im Array 'parties' definiert:

```
  "parties" : [ {
    "party" : "Customer",
    "role" : "Buyer"
  } ]
```

Für jedes Element des Arrays 'parties' gibt es zwei wichtige Abschnitte:

- `party`: Der Text, der als Partei im Dokument identifiziert wurde.
- `role`: Die Rolle der Partei, die identifiziert wurde. Rollen ändern sich auf der Grundlage der Unterdomäne (eine Liste der möglichen Rollen finden Sie in den Informationen zur angegebenen Unterdomäne). Parteien, für die keine bestimmte Rolle identifiziert werden kann, werden wie folgt gekennzeichnet:


## Wissenswertes über Vertragselemente

Durch die Elementklassifizierung analysierte Verträge werden unter Angabe jedes identifizierten analysierten Elements zurückgegeben.

In den folgenden Abschnitten ist beschrieben, wie die Analyse in der JSON-Rückgabe beschrieben wird.

### Typ

Die Informationen zum Element `types` werden als Array von Objekten angegeben, wobei jedes Objekt eine Gattung (nature) und eine Partei (party) enthält, die als Paar für dieses Element identifiziert wurden. In der folgenden Tabelle sind die möglichen Werte für `natures` und `parties` aufgeführt, die identifiziert werden können.

Gattungen geben die Aktionstypen an, die der Satz erfordert.

| **Gattung** | **Beschreibung** |
| --- | --- |
| Definition | Dieses Element verdeutlicht einen Begriff/eine Beziehung usw. Zur Erfüllung dieses Elements ist keine Aktion erforderlich und keine Partei ist betroffen.|
| Haftungsausschluss | Die Partei im Element ist nicht verpflichtet, die speziellen Bedingungen im Element zu erfüllen, wird hieran jedoch nicht gehindert.|
| Ausschluss | Die Partei im Element erfüllt die speziellen Bedingungen nicht, die im Element dargelegt sind.  |
| Verpflichtung | Die Partei im Element muss die Bedingungen des Elements erfüllen.   |
| Recht | Der Partei im Element werden die Bedingungen des Elements zugesichert.  |

### Parteien

Für jede identifizierte Klausel werden die betroffenen Parteien namentlich angegeben. Jede identifizierte Partei wird dann nach ihrer Rolle (`role`) klassifiziert. Parteien sind die Beteiligten des Vertrags. Für einen Vertrag können die folgenden Rollen identifiziert werden:

| **Rolle** | **Beschreibung** |
| --- | --- |
| `Einkäufer` | Die Partei, die für die Bezahlung von Waren/Dienstleistungen verantwortlich ist. |
| `Endbenutzer` | Die Partei, die mit den eigentlichen Waren/Dienstleistungen interagiert. Sie wird ausdrücklich vom Einkäufer unterschieden. |
| `Keine` | Für dieses Element wurde keine Partei identifiziert. Diese Rolle ist immer mit der Gattung 'Definition' verbunden. |
| `Lieferant` | Die Partei, die für die Lieferung von Waren/Dienstleistungen verantwortlich ist. |

### Kategorien

Kategorien definieren den Inhalt des Satzes. Die folgenden Kategorien können identifiziert werden:

| **Kategorien** | **Beschreibung** |
| --- | --- |
| `Änderungen` | Eine Änderung des ursprünglichen Vertrages, die die Konditionen für die Änderung der Vertragsbedingungen festlegt. |
| `Assetverwendung` | Details aller Assets in der Vereinbarung, die von einer der Parteien genutzt werden. |
| `Abtretungen` | Umfasst die Übertragung von Rechten einer Partei an eine andere Partei.  |
| `Prüfungen` | Diese Klausel ermöglicht dem Einkäufer die Untersuchung oder Überprüfung des Lieferanten der bereitgestellten Dienstleistungen. |
| `Kommunikation` | Beschreibt zulässige Kommunikationsverfahren und Kontaktinformationen. |
| `Vertraulichkeit` | Beschreibt, wie vertrauliche oder persönliche Informationen behandelt werden, beispielsweise die Zugänglichkeit bestimmter Daten für bestimmte Personen und die Art des Zugriffs. |
| `Business-Continuity` | Beschreibt, wie ein Unternehmen im Fall einer unterbrechenden Störung die Bereitstellung von Arbeit auf vordefinierten Ebenen fortsetzt. |
| `Definitionen` | Ein Abschnitt, der einen im Dokument verwendeten Begriff definiert.  |
| `Liefergegenstände` | Die Artikel oder Dienstleistungen, die am Ende einer Arbeitseinheit zu liefern sind. |
| `Lieferung` | Der spezielle Zeitplan oder Prozess für den Abschluss eines Projekts. |
| `Schlichtung` | Gibt an, wie ein gegebenenfalls zwischen den Vertragsparteien entstehender Streitfall gehandhabt wird. |
| `Höhere Gewalt` | Eine Klausel, die beide Parteien im Fall eines Störereignisses von ihren Verpflichtungen entbindet. |
| `Freistellung` | Beschreibt den Rechtsbehelf oder die Folgen bei Verstößen gegen Bedingungen. |
| `Versicherung` | Beschreibt den Umfang des vom Lieferanten zu übernehmenden Versicherungsschutzes. |
| `Geistiges Eigentum` | Eine Klausel, die sich auf Patente, Copyrights oder Marken bezieht. Kann sich im allgemeineren Sinn auch auf Erfindungen, Autorenschaft oder Fachwissen beziehen. |
| `Haftung` | Beschreibt Verpflichtungen und Einschränkungen für die Zuständigkeit jeder Partei. |
| `Sonstiges` | Relevante Abschnitte, die nicht in andere Kategorien passen. |
| `Zahlungsbedingungen & Rechnungsstellung` | Beschreibt, welche Zahlungen fällig sind und wie der Zeitplan für die Zahlung lautet. |
| `Preisgestaltung & Steuern` | Beschreibt, wie sich die Preise zusammensetzen und wie Steuern anzuwenden sind. |
| `Datenschutz` | Beschreibt die geltenden Datenschutzregelungen. |
| `Zuständigkeiten` | Beschreibt die Zuständigkeiten der einzelnen Parteien. |
| `Sicherheit` | Beschreibt, wie Schädigungen einer Partei zu verhindern sind. Schließt die Sicherheit sowohl für das Personal als auch für physische Assets ein. |
| `Leistungsumfang` | Beschreibt in der Leistungsbeschreibung detailliert, was durch die Parteien geleistet werden soll. |
| `Unterauftragsvergabe` | Bezieht sich auf alle Drittparteien, die an die Erfüllung einer Anforderung beteiligt sind. |
| `Laufzeit & Kündigung` | Der Zeitraum, in dem etwas stattfindet, und die Bedingungen, unter denen der Vertrag beendet werden kann. |
| `Gewährleistung` | Die Garantie eines Lieferant für die Funktionsweise eines Produkts. |

### Zusicherung

Jedem Element (Typ oder Kategorie), das von der Elementklassifizierung identifiziert wird, wird eine Einstufung der Zusicherung (`assurance`) erteilt. Die möglichen Werte für die Zusicherung sind nachfolgend beschrieben:

| **Zusicherung** | **Beschreibung** |
| --- | --- |
| `Hoch` | Es gibt signifikante Anzeichen, dass die angegebene Klassifizierung repräsentativ für den Inhalt ist. |
| `Niedrig` | Es gibt einige Anzeichen für die Unterstützung der Klassifizierung, zur Bestätigung ist jedoch möglicherweise eine weitere Prüfung erforderlich. |
