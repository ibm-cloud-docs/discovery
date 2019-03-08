---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-08"

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

# Integration mit Watson Knowledge Studio
{: #integrating-with-wks}

Sie können ein angepasstes Modell aus {{site.data.keyword.knowledgestudiofull}} mit dem {{site.data.keyword.discoveryshort}}-Service integrieren, um angepasste Aufbereitungen für Entitäten und Beziehungen bereitzustellen.
{: shortdesc}

Dies gibt Ihnen die Flexibilität, die Dokumenterweiterungsfunktionen des {{site.data.keyword.discoveryshort}}-Service mit spezifischen Informationen zu besonders interessanten Bereichen (z. B. Branchen und wissenschaftliche Disziplinen) anzuwenden. In Ihrem Aufbereitungsmodell können Sie sowohl allgemein zugängliche als auch eigene proprietäre Daten verwenden.

Sie können die Service-API oder die {{site.data.keyword.discoveryshort}}-Tools verwenden, um ein {{site.data.keyword.knowledgestudioshort}}-Modell mit dem {{site.data.keyword.discoveryshort}}-Service zu integrieren.

## Vorbereitende Schritte

Bevor Sie ein angepasstes Modell aus {{site.data.keyword.knowledgestudioshort}} mit dem {{site.data.keyword.discoveryshort}}-Service integrieren können, müssen Sie das Modell mithilfe von {{site.data.keyword.knowledgestudioshort}} erstellen und bereitstellen. Informationen zum Erstellen und Bereistellen von Modellen finden Sie in der [Dokumentation zu {{site.data.keyword.knowledgestudioshort}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.bluemix.net/docs/services/knowledge-studio/tutorials-create-project.html#wks_tutintro){: new_window}. Sie benötigen die eindeutige ID des bereitgestellten Modells, um es mit dem {{site.data.keyword.discoveryshort}}-Service zu integrieren.

## Angepasstes Modell mithilfe der API integrieren

1.  Ermitteln Sie die ID Ihrer {{site.data.keyword.discoveryshort}}-Umgebung (siehe [Umgebungen auflisten ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_environments){: new_window}). Notieren Sie sich die Umgebungs-ID.
1.  Listen Sie die IDs der aktuellen {{site.data.keyword.discoveryshort}}-Konfiguration(en) auf (siehe [Konfigurationen auflisten ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_configurations){: new_window}). Notieren Sie sich die ID der Konfiguration, die Sie mit Ihrem angepassten Modell von {{site.data.keyword.knowledgestudiofull}} integrieren wollen.
1.  Laden Sie mit dem folgenden Befehl in einer Bash-Shell oder funktional entsprechenden Shell wie Cygwin for Windows eine Kopie Ihrer aktuellen {{site.data.keyword.discoveryshort}}-Konfiguration herunter. Ersetzen Sie hierbei `{umgebungs-id}` und `{konfigurations-id}` durch die IDs, die Sie in den beiden vorherigen Schritten notiert haben.

    ```bash
    curl -u "apikey":"{wert_des_api-schlüssels}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{umgebungs-id}/configurations/{konfigurations-id}?version=2017-11-07" > my_config.json
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
            "source_field": "text",
            "destination_field": "enriched_text",
            "enrichment": "natural_language_understanding",
            "options": {
                "features": {
                    "entities": {
                        "sentiment": true,
                        "emotion": false,
                        "limit": 50
                    },
                    "sentiment": {
                        "document": true
                    },
                    "categories": {},
                    "concepts": {
                        "limit": 8
                    },
                    "relations": {}
                }
            }
        }]
        ```
        {: codeblock}

    1.  Aktualisieren Sie die Datei wie folgt, indem Sie die eindeutige ID des {{site.data.keyword.knowledgestudioshort}}-Modells anstelle von `{id_des_watson_knowledge_studio-modells}` angeben (siehe 'Vorbereitende Schritte').

        ```json
        "enrichments": [
   {
            "source_field": "text",
            "destination_field": "enriched_text",
            "enrichment": "natural_language_understanding",
            "options": {
                "features": {
                    "entities": {
                        "sentiment": true,
                        "emotion": false,
                        "limit": 50,
                        "model": "{id_des_watson_knowledge_studio-modells}"
                    },
                    "sentiment": {
                        "document": true
                    },
                    "categories": {},
                    "concepts": {
                        "limit": 8
                    },
                    "relations": {
                      "model": "{id_des_watson_knowledge_studio-modells}"
                    }
                }
            }
        }]
        ```
        {: codeblock}

1.  Speichern Sie die Datei `my_config.json`.
1.  Verwenden Sie ein JSON-Prüfprogramm (z. B. [JSLint ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://jslint.com){: new_window}, um die bearbeitete JSON-Datei zu prüfen und bei Bedarf zu korrigieren, bevor Sie die nächsten Schritte ausführen.
1.  Aktualisieren Sie die Konfiguration wie folgt. Sie benötigen wieder die `{umgebungs-id}` und die `{konfigurations-id}`, die Sie zu Beginn dieser Prozedur ermittelt haben.

    ```bash
    curl -X PUT -u "apikey":"{wert_des_api-schlüssels}" -H "Content-Type: application/json" -d @my_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{umgebungs-id}/configurations/{konfigurations-id}?version=2017-11-07"
    ```
    {: pre}

    **Hinweis:** Wenn Sie eine neue Konfiguration erstellen oder die Standardkonfiguration ändern, müssen Sie eine neue angepasste Konfiguration erstellen, statt eine vorhandene Konfiguration zu aktualisieren. Achten Sie vor dem Erstellen einer neuen Konfiguration darauf, das Feld `"configuration_id":` aus der Datei `my_config.json` zu entfernen, und führen Sie dann den folgenden Befehl aus:

    ```bash
    curl -X POST -u "apikey":"{wert_des_api-schlüssels}" -H "Content-Type: application/json" -d @my_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{umgebungs-id}/configurations?version=2017-11-07"
    ```
    {: pre}

    Beide Befehle geben den Inhalt der aktualisierten Konfigurationsdatei zurück.

## Angepasstes Modell mithilfe der Discovery-Tools integrieren

Sie können ein angepasstes {{site.data.keyword.knowledgestudioshort}}-Modell in die Aufbereitungen für die [Entitätsextraktion](/docs/services/discovery/building.html#entity-extraction) oder [Beziehungsextraktion](/docs/services/discovery/building.html#relation-extraction) mit den {{site.data.keyword.discoveryshort}}-Tools integrieren.

1. Ermitteln Sie die `Modell-ID` Ihres {{site.data.keyword.knowledgestudioshort}}-Modells.
1. Klicken Sie in den {{site.data.keyword.discoveryshort}}-Tools auf das Symbol **Daten verwalten** in der linken oberen Ecke, um die Anzeige **Daten verwalten** zu öffnen und eine Sammlung zu erstellen oder zu öffnen. **Hinweis:** Wenn Sie eine vorhandene Sammlung auswählen, sollte sie leer sein. Falls dies nicht der Fall ist, sollten Sie diese Dokumente nach dem Erstellen der neuen Konfigurationsdatei erneut einpflegen.
1. Klicken Sie im Abschnitt **Konfiguration** in der Anzeige **Daten verwalten** für Ihre Sammlung auf **Wechseln** und anschließend auf **Neue Konfiguration erstellen**. Geben Sie der Konfiguration einen Namen. 
1. Klicken Sie auf **Aufbereitungen hinzufügen** und wählen Sie entweder die Aufbereitung für die **Entitätsextraktion** oder die **Beziehungsextraktion** aus.
1. Geben Sie die `Modell-ID` im Feld `ID des angepassten Modells` für die ausgewählte Aufbereitung ein. Das angepasste {{site.data.keyword.knowledgestudiofull}}-Modell überschreibt die Standardeinstellung für diese Aufbereitung. 
1. Klicken Sie auf **Anwenden** und dann auf **Fertig**.

Sobald Dokumente in eine Datensammlung hochgeladen werden, werden sie unter Verwendung der für diese Sammlung ausgewählten Konfigurationsdatei konvertiert und aufbereitet. Falls Sie für eine bestehende Sammlung zu einer neuen Konfigurationsdatei wechseln, nachdem Dokumente hochgeladen wurden, bleiben diese hochgeladenen Dokumente gemäß der ursprünglichen Konfigurationsdatei konvertiert. Alle Dokumente, die nach dem Wechsel der Konfigurationsdatei hochgeladen werden, verwenden die neue Konfigurationsdatei. Wenn Sie die neue Konfiguration für die **gesamte** Sammlung verwenden wollen, müssen Sie eine neue Sammlung erstellen, die neue Konfigurationsdatei auswählen und alle Dokumente erneut hochladen.

**Hinweis:** Einer Aufbereitung kann nur ein einziges {{site.data.keyword.knowledgestudiofull}}-Modell zugewiesen sein.

## Nächste Schritte

Verwenden Sie die neue Konfiguration beim {{site.data.keyword.discoveryshort}}-Service, um private Daten einzupflegen. Dokumente, die Sie mit der aktualisierten Konfiguration einpflegen, werden automatisch mit den Daten aus dem angepassten Modell aufbereitet.
