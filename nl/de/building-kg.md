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

# Watson Discovery Knowledge Graph

Wissensdiagramme bilden weitaus mehr als Daten und Informationen ab, denn sie stellen dokumentübergreifende Verbindungen in Ihren Daten her und generieren neue Erkenntnisse. Mithilfe der bereitgestellten AI-Technologie werden angepasste Wissensdiagramme automatisch aus unstrukturierten Daten erstellt. Hierzu werden Entitäten und Beziehungen extrahiert und vereindeutigt, die Beziehungen unter Verwendung von algorithmischen Verfahren aufbereitet und die Ergebnisse mithilfe von Relevanzalgorithmen in eine Rangordnung gebracht. Wissensdiagramme können als 'Wissenszentrum' für Ihr Unternehmen dienen und für Unternehmenssuche, Auswertung, Recommendation-Engines und andere Entscheidungsfindungsprozesse genutzt werden (z. B. Erkennung von Betrug, Verschwendung oder Missbrauch). Die Verwendung eines (in {{site.data.keyword.knowledgestudioshort}} erstellten) angepassten Modells beim Erstellungsprozess für das Wissensdiagramm kann für die Erstellung von domänenspezifischen Wissensdiagrammen hilfreich sein, die in Bereichen wie Finanzwesen, Technologie, Sicherheit, Informationsbeschaffung, Gesundheitswesen und vielen anderen anwendbar sind.

Zu {{site.data.keyword.discoveryfull}} wurden zwei neue Endpunkte hinzugefügt, die eine dokumentübergreifende Suche nach vereindeutigten Entitäten und aufbereiteten Beziehungen in unstrukturierten Dokumentsammlungen ermöglichen. Die Suchergebnisse können in eine nach Relevanz oder Beliebtheit aufgestellte Rangordnung gebracht werden. Neben einem Suchtoken können die APIs optional eines oder mehrere Kontextwörter bzw. Passagen verwenden, die das Auffinden von relevanteren Entitäten und Beziehungen innerhalb des automatisch erstellten umfangreichen Wissensdiagramms ermöglichen.

 Die folgende Abbildung zeigt, wie Knowledge Graph in die aktuelle Pipeline von {{site.data.keyword.discoveryfull}} eingebunden ist. {{site.data.keyword.nlushort}} bereitet Dokumente mit Entitäten und Dokumente auf der Einzeldokumentebene auf. Während der Erstellung des Wissensdiagramms werden Verfahren für die implizite (automatische) Entitätsauflösung und Diagrammerweiterung verwendet, um ein dokumentübergreifendes verbundenes Diagramm von Entitäten und Beziehungen zu erstellen. Neben dem erstellten Wissensdiagramm trägt der Knowledge Graph-Analyseservice Verfahren für die Relevanzeinstufung zur Rückgabe von Ergebnissen bei.

![Knowledge Graph-Prozess](images/knowledge-graph.png)

Dieses verbundene Diagramm aus Wissen und Einstufungsverfahren stellt Folgendes bereit:

-  Vereindeutigte Entitäten durch Verwendung eines Tokens für die unscharfe Suche sowie optional von Typinformationen und Kontext. Beispiel: Die Suche nach `Steve` im Kontext `Apple` gibt `Steve Jobs` als relevantestes Ergebnis zurück, während die Suche nach `Steve` im Kontext `Microsoft` als relevantestes Ergebnis `Steve Ballmer` zurückgibt.
-  Nach Relevanz angeordnete Beziehungen durch die Eingabe eines Tokens für die unscharfe Suche und von Kontext (optional). Die Relevanzeinstufung verwendet die globalen Eigenschaften des Diagramms, um spezifischere Informationen zutage zu fördern. Beispiel: Die Suche nach Beziehungen für `Obama` im Kontext `health` gibt `Affordable Care Act` und andere verwandte Entitäten zurück.
-  Dokumentübergreifende Inferenzen und Aggregationen durch die Abfrage von Entitäten und Beziehungen in einem verbundenen Wissensdiagramm. Beispiele für solche Abfragen: In welcher Verbindung steht Person X zu Person Y? Wie stark weichen die Datenzugriffsmuster des Mitarbeiters X von der Norm ab? Welchen Einflussbereich besitzt Person X?

## Voraussetzungen für den Service

In der Betaversion sind die Funktionalität der Komponente 'Knowledge Graph' für das Wissensdiagramm und die zugehörigen Methoden nur für Serviceinstanzen verfügbar, die den **Advanced**-Plan abonniert haben.

## Voraussetzungen für die Datensammlung

{{site.data.keyword.discoveryshort}} verwendet Entitäten und Beziehungen, die zur Bildung des Wissensdiagramms aus eingepflegten Dokumenten extrahiert werden und Entitäts- sowie Beziehungsabfragen ermöglichen.

**Hinweis:** Die Komponente 'Knowledge Graph' kann nur für private Datensammlungen verwendet werden; sie ist nicht zur Verwendung mit {{site.data.keyword.discoverynewsshort}} gedacht.

Damit Sie Knowledge Graph nutzen können, muss Ihre Sammlung so konfiguriert sein, dass sie die folgenden Anforderungen erfüllt:

-  Für die Felder, die Knowledge Graph verwenden, müssen beide Aufbereitungen für Entitäten (`entities`) und Beziehungen (`relations`) angegeben sein. Jede Aufbereitung muss hierbei dasselbe angepasste Modell verwenden. Falls das öffentliche Modell erforderlich ist, muss es im Format eines angepassten Modells angegeben sein (`model="en-news"`).

-  Die Aufbereitungen für `relations` müssen wie folgt angegeben werden:
   ```json
   "relations": {
     "model": "en-news"
   }
   ```
   {: codeblock}

-  Die Aufbereitung für `entities` muss wie folgt angegeben werden; zusätzlich müssen die Parameter `mentions`, `mentions_types` und `sentence_locations` angegeben sein:
   ```json
   "entities": {
     "mentions": true,
     "mention_types": true,
     "sentence_locations": true,
     "model": "en-news"
    }
    ```
    {: codeblock}

   Andere optionale Optionen für `enrichments` (z. B. `"sentiment": true`) können auf Wunsch ebenfalls angegeben werden.

Diese Optionen können nicht mit den {{site.data.keyword.discoveryshort}}-Tools hinzugefügt werden, stattdessen muss eine angepasste Konfiguration mithilfe der API hochgeladen werden. Eine zur Aufbereitung des Feldes `text` geänderte Standardkonfiguration, die die Verwendung der Sammlung mit dem Wissensdiagramm und dem öffentlichen Modell ermöglicht, ist [hier](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/discovery/config-default-kg.json) verfügbar.

Erstellen Sie nach der Erstellung einer {{site.data.keyword.discoveryshort}}-Serviceinstanz wie folgt eine angepasste Konfiguration:

1. Geben Sie den folgenden Befehl aus, um eine Umgebung namens `my-first-environment` zu erstellen. Ersetzen Sie hierbei `{benutzername}` und `{kennwort}` durch Ihre Serviceberechtigungsnachweise:

   ```bash
   curl -X POST -u "{benutzername}":"{kennwort}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "api/v1/environments?version=2017-11-07"
   ```
   {: pre}

   Die API gibt daraufhin Informationen wie Ihre Umgebungs-ID, den Umgebungsstatus und den Umfang des durch die Umgebung verwendeten Speichers zurück.

   Sie benötigen den für {umgebungs-id} zurückgegebenen Wert.

1. Erstellen Sie anschließend die angepasste Konfiguration. Diese Prozedur setzt voraus, dass Sie die unter (https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/discovery/config-default-kg.json) verfügbare Konfiguration hochgeladen haben. Falls Sie eine eigene angepasste Konfiguration erstellen wollen, finden Sie in der Konfigurationsreferenz (/docs/services/discovery/custom-config.html) weitere Informationen.

   ```bash
   curl -X PUT -u "{benutzername}":"{kennwort}" -H "Content-Type: application/json" -d config-default-kg.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{umgebungs-id}/configurations?version=2017-11-07"
   ```
   {: pre}

1. Nachdem die angepasste Konfiguration hochgeladen wurde, kann sie für jede von Ihnen erstellte Sammlung verwendet werden. Zum Hochladen von Dokumenten kann jede beliebige Methode eingesetzt werden, solange die angepasste Konfiguration angegeben ist. Falls Sie keine Erfahrungen mit dem Erstellen von Sammlungen und dem Hochladen von Dokumenten besitzen, finden Sie unter 'Einführung in die Tools' (/docs/services/discovery/getting-started-tool.html) weitere Informationen. Wenn Sie mit Schritt 3 (/docs/services/discovery/getting-started-tool.html#create-custom-configuration) fortfahren, wählen Sie 'Knowledge Graph-Konfiguration' aus, statt eine neue Konfiguration zu erstellen.

## Entitätsabfragen
{: #entities}

In der Betaversion von Knowledge Graph wird bei Entitätsabfragen die kontextbasierte Entitätsvereindeutigung unterstützt. Basierend auf dem bereitgestellten Entitätstext und optionalem Kontexttext identifiziert die Vereindeutigung eindeutige Entitäten und gibt eine Liste der Entitäten zurück, deren Rangordnung auf den Kontextinformationen basiert. Eine Knowledge Graph-Entitätsabfrage wird mit einer Anforderung POST für ein JSON-Objekt an den Endpunkt 'v1/environments/{umgebungs-id}/collections/{sammlungs-id}/query_entities' ausgeführt.

Zur Abfrage von Entitäten können Sie die APIs oder die {{site.data.keyword.discoveryshort}}-Tools verwenden. Der Abschnitt 'Knowledge Graph mit Discovery-Tools abfragen' (/docs/services/discovery/building-kg.html#querying-kg) enthält Informationen zu den Tools.

Das JSON-Objekt der Knowledge Graph-Entitätsabfrage verwendet das folgende Format:

```json
{
  "feature": "disambiguate",
  "entity": {
    "text": "Steve",
    "type": "Person"
  },
  "context": {
    "text": "iphone"
  },
  "count": 10
}
```
{: codeblock}

-  `"feature": Datentyp 'string' (erforderlich): Das zu verwendende Feature für die Entitätsabfrage, muss 'disambiguate' lauten.
-  `"entity": {} (erforderlich): ein Objekt, das die zu vereindeutigenden Entitätsinformationen enthält.
   -  `"text": Datentyp 'string' (erforderlich): Der Entitätstyp, der vereindeutigt wird.
   -  `"type": Datentyp 'string' (optional): Der optionale Entitätstyp, in Bezug auf den die Vereindeutigung erfolgen soll. Wenn dieser Parameter nicht angegeben ist, werden alle Typen einbezogen.
-  `"context": {} (optional): Ein optionales Objekt, das kontextbezogene Voraussetzungen für die Vereindeutigung enthält.
   -  `"text": Datentyp 'string' (optional): Der Entitätstext, der den Kontext für die abgefragte Entität und die auf dieser Zuordnung basierende Einstufung angibt. Beispiel: Falls Sie die Stadt London in England abfragen wollen, würde Ihre Abfrage nach 'London' mit dem Kontext 'England' suchen. Die Eingabe kann aus Namensteilen oder umfangreichen Passagen bestehen, die relevante Entitätsbegriffe enthalten. Mehrere Begriffe können gleichzeitig übergeben werden.
-  `"count": Datentyp INT (optional): Die Anzahl der zurückzugebenden vereindeutigten Entitäten. Der Standardwert ist 10. Der maximale Wert ist 1000.

Die Abfrage gibt Ergebnisse im folgenden Format zurück:

```json
{
  "entities": [
    {
      "text": "Steve Jobs",
      "type": "PERSON"
    },
    {
      "text": "Steve Wozniak",
      "type": "PERSON"
    }
  ]
}
```
{: codeblock}

Falls keine Übereinstimmung gefunden wird, wird das folgende JSON-Objekt zurückgegeben:

```json
{
  "entities": []
}
```
{: codeblock}

## Beziehungsabfragen
{: #relations}

Bei Knowledge Graph-Beziehungsabfragen wird die Suche nach den relevantesten Beziehungen basierend auf Eingabeentitäten unterstützt, wobei implizite Entitätsvereindeutigung, kontextbasierte Beziehungen, Sortierung nach Relevanzquote und Erwähnungsanzahl sowie Filterung nach Typen und Dokument-IDs verwendet werden können.

Zur Abfrage von Beziehungen können Sie die APIs oder die {{site.data.keyword.discoveryshort}}-Tools verwenden. Der Abschnitt 'Knowledge Graph mit Discovery-Tools abfragen' (/docs/services/discovery/building-kg.html#querying-kg) enthält Informationen zu den Tools.

Eine Knowledge Graph-Beziehungsabfrage wird mit einer Anforderung POST für ein JSON-Objekt an den Endpunkt 'v1/environments/{umgebungs-id}/collections/{sammlungs-id}/query_relations' ausgeführt.

Das JSON-Objekt der Knowledge Graph-Beziehungsabfrage verwendet das folgende Format:

```json
{
  "entities": [
    {
      "text": "Steve Jobs",
      "type": "PERSON",
      "exact": true
    }
  ],
  "context": {
    "text": "iphone"
  },
  "sort": "score",
  "filter": {
    "relation_types": {
      "exclude": ["colocation"],
      "include": ["locatedAt", "employedBy", "managerOf", "founderOf"]
    },
    "entity_types": {
      "exclude": ["EVENT"],
      "include": ["PERSON", "GPE", "ORGANIZATION"]
    },
    "document_ids": ["b95df4c1-d00f-4771-abb2-a52baea0444a", "ad340635-bf3e-47a5-bea5-5e778f600c32"]
  },
  "count": 10
}
```
{: codeblock}

-  `"entities": [] (erforderlich): Ein Array, das die Entitäten enthält, deren Beziehungen abgefragt werden. Falls nur ein einziges Entitätsobjekt definiert ist, werden alle Nachbarbeziehungen zurückgegeben. Sind mehrere Entitätsobjekte definiert, werden die wechselseitigen Beziehungen paarweise zurückgegeben. Wechselseitige paarweise Beziehungen geben die direkten Beziehungen zwischen den Eingabeentitäten und nicht die Beziehungen zu allen Nachbarn zurück. Jedes Entitätsobjekt enthält Folgendes:
   -  `"text": Datentyp 'string' (erforderlich): Der Entitätstext.
   -  `"type": Datentyp 'string' (optional): Der optionale Entitätstyp. Dieses Feld ist erforderlich, falls für 'exact' der Wert 'true' angegeben ist.
   -  `"exact": Datentyp 'boolean' (optional): Beim Wert 'false' wird die implizite Vereindeutigung ausgeführt. Die implizite Vereindeutigung verwendet für jedes Eingabeentitätsobjekt jeweils die vereindeutigte Entität mit der größten Relevanz. Der Standardwert ist 'false'.
-  `"context": {} (optional): Ein optionales Objekt, das kontextbezogene Voraussetzungen enthält.
   -  `"text": Datentyp 'string' (optional): Der Entitätstext, der den Kontext für die abgefragte Entität und die auf dieser Zuordnung basierende Einstufung angibt. Beispiel: Falls Sie die Stadt London in England abfragen wollen, würde Ihre Abfrage nach 'London' mit dem Kontext 'England' suchen. Die Eingabe kann aus Namensteilen oder umfangreichen Passagen bestehen, die relevante Entitätsbegriffe enthalten. Mehrere Begriffe können gleichzeitig übergeben werden.
-  `"sort": Datentyp 'string' (optional): Die Sortiermethode für die Beziehungen. Der Wert kann 'score' (Quote) oder 'frequency' (Häufigkeit) lauten. Der Standardwert ist 'score'. Die Quote basiert auf der Relevanz von Beziehungen und Nachbarn der Eingabeentität und auf der Relevanz für den Kontext, falls der Kontext angegeben ist. Die Häufigkeit gibt an, wie oft jede Beziehung eindeutig identifiziert wird.
-  `"filter": {} (optional): Ein Objekt, das die Beziehungstypen, Entitätstypen und speziellen Dokumente enthält, nach denen die Filterung für diese Abfrage erfolgen soll. Standardmäßig wird nichts ausgeschlossen.
   -  `"relation_types": {} (optional): Eine Liste der zu filternden Beziehungstypen.
      -  `"exclude": [] (optional): Eine durch Kommas getrennte Liste von Beziehungstypen, die aus der Abfrage gefiltert werden sollen.
      -  `"include": [] (optional): Eine durch Kommas getrennte Liste von Beziehungstypen, die explizit in die Abfrage einbezogen werden sollen. Wenn dieser Parameter angegeben ist, gelten alle anderen Typen als ausgeschlossen.
   -  `"entity_types": {} (optional): Eine Liste von Entitätstypen zum Filtern von Nachbarn. Ist bei einer Eingabe von mehreren Entitäten nicht anwendbar, da kein neuer Nachbar zurückgegeben wird.
      -  `"exclude": [] (optional): Eine durch Kommas getrennte Liste von Entitätstypen, die aus der Abfrage ausgeschlossen werden sollen.
      -  `"include": [] (optional): Eine durch Kommas getrennte Liste von Entitätstypen, die explizit in die Abfrage einbezogen werden sollen. Wenn dieser Parameter angegeben ist, gelten alle anderen Typen als ausgeschlossen.
   -  `"document_ids": [] (optional): Eine durch Kommas getrennte Liste von Dokumenten, für die die Beziehungsabfrage ausgeführt werden soll.
-  `"count": Datentyp INT (optional): Die zurückzugebende Anzahl von Beziehungen. Der Standardwert ist 10. Der maximale Wert ist 1000.

Die Abfrage gibt Ergebnisse im folgenden Format zurück:

```json
{
  "relations": [
    {
      "type": "FOUNDEROF",
      "frequency": 7,
      "arguments": [
        {
          "entities": [
            {
              "type": "PERSON",
              "text": "Steve Jobs"
            }
          ]
        },
        {
          "entities": [
            {
              "type": "ORGANIZATION",
              "text": "Apple"
            }
          ]
        }
      ]
    }
  ]
}
```
{: codeblock}

In jedem Objekt des Beziehungsarrays wird ein Array 'arguments' zurückgegeben, das ein Paar aus Entitätsarrays enthält. Das erste Array ist die Quelle oder das Subjekt der Beziehung, das zweite Array ist ihr Ziel oder Objekt.


Falls keine Übereinstimmung gefunden wird, wird das folgende JSON-Objekt zurückgegeben:

```json
{
  "relations": []
}
```
{: codeblock}

## Knowledge Graph mit den Discovery-Tools abfragen
{: #querying-kg}

Benutzer mit Serviceinstanzen, die den [**Advanced-Plan**] (/docs/services/discovery/building-kg.html#service-requirements) abonniert haben, können private Sammlungen mit Knowledge Graph unter Verwendung der {{site.data.keyword.discoveryshort}}-Tools abfragen.

So greifen Sie in den {{site.data.keyword.discoveryshort}}-Tools auf die Knowledge Graph-Abfrage zu:

1.  Klicken Sie auf das Symbol ! [Abfragesymbol] (images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->, um die Abfrageseite zu öffnen.
2.  Wählen Sie Ihre Sammlung aus und klicken Sie auf 'Los geht's!'.
3.  Wählen Sie in der Anzeige 'Abfragen erstellen' die Registerkarte 'Knowledge Graph' und anschließend 'Entitäten' oder 'Beziehungen' aus.
