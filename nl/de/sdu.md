---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-10"

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

# Smart Document Understanding

Smart Document Understanding (SDU) ist eine neue Methode, um Ihre Dokumente in {{site.data.keyword.discoveryfull}} zu annotieren. 

Der Editor vereinfacht das Training von angepassten Konvertierungsmodellen. Das Anpassen der Indexierung Ihrer Dokumente in Discovery verbessert die Antworten, die für Ihre Anwendung zurückgegeben werden.

SDU befindet sich in der Betaversion. Eine Aussage zu Features als Betaversion finden Sie [hier](/docs/services/discovery/release-notes.html#beta-features).

## Unterstützte Dokumenttypen und Browser
{: #doctypes}

Unterstützte Dokumenttypen: PDF, Word, HTML. JSON-Dokumente werden von {{site.data.keyword.discoveryfull}} unterstützt, werden jedoch im SDU-Editor nicht geöffnet, da es sich um strukturierte Dokumente handelt.

Unterstützte Browser für diese Betaversion: Chrome und Firefox

## Vorgehensweise zum Versehen von Dokumenten von Annotationen
{: #annotate}

Gehen Sie wie folgt vor, um den Editor für Smart Document Understanding zu öffnen:

1. Öffnen Sie {{site.data.keyword.discoveryfull}} über den Betalink.
1. Öffnen Sie eine private Datensammlung und klicken Sie in der Anzeige **Daten verwalten** auf **Zu Dateneinstellungen wechseln**. 
1. In der Anzeige **Dateneinstellungen** gibt es zwei Registerkarten: **Felder extrahieren** und **Felder aufbereiten**.

   - **Felder extrahieren** enthält den SDU-Editor. Diese Registerkarte ersetzt die Registerkarten **Konvertieren** und **Normalisieren** in der ursprünglichen {{site.data.keyword.discoveryshort}}-Anzeige. 
   - **Felder aufbereiten** ist identisch mit der Registerkarte **Aufbereiten** in der ursprünglichen Anzeige. Weitere Informationen zu Aufbereitungen finden Sie unter [Aufbereitungen hinzufügen](/docs/services/discovery/building.html#adding-enrichments). Die Option **Beispieldokumente hochladen** ist auf der Registerkarte **Felder aufbereiten** nicht verfügbar, da sie nicht erforderlich ist.

1. Zwanzig (20) Dokumente aus Ihrer Sammlung werden automatisch unter die Registerkarte **Felder extrahieren** im Editor für Smart Document Understanding geladen.

Über die Symbolleiste am oberen Rand können Sie folgende Aktionen durchführen:
- Ein Dokument auswählen
- In dem angezeigten Dokument navigieren
- Die Seitenansicht (`Einzelseitenansicht`, `Vergrößern`, `Verkleinern`), `Änderungen löschen` und `Modells importieren/exportieren`) anpassen. Klicken Sie auf `Einzelseitenansicht`, um zu einer Anzeige zu wechseln, in der Ihre Annotationen und Dokumente separat angezeigt werden. 

### Dokumente im SDU-Editor annotieren
{: #documents}

**Hinweis:** Tabellen werden in einem separaten Schritt annotiert.

Weitere Informationen finden Sie unter [Best Practices für das Beschriften von Dokumenten und Tabellen](/docs/services/discovery/sdu.html#bestpractices).

1. Rechts von Ihrem Dokument wird eine Standardgruppe von Feldern angezeigt. (Für die Betaversion können Sie keine angepassten Felder erstellen, diese Funktion wird jedoch in der Zukunft verfügbar sein.) Die verfügbaren Felder sind `answer`, `author`, `footer`, `header`, `question`, `subtitle`, `table_of_contents`, `text` und `title`.
1. Klicken Sie auf der rechten Seite auf einen Feldnamen, um ihn zu aktivieren.
1. Klicken Sie auf den Inhalt, der dieses Feld im SDU-Editor darstellt. Das Feld wird hervorgehoben. 
   - Alternativ können Sie einen Feldnamen rechts auswählen und ihn auf den Inhalt im SDU-Editor ziehen. 
   - Wenn Sie eine Änderung löschen möchten, klicken Sie in der Symbolleiste auf die Schaltfläche **Änderung löschen**.
1. Klicken Sie auf **Übergeben**.
   **Hinweis:** Wenn Sie annotieren, lernt Watson dabei und beginnt mit der Vorhersage von Annotationen. Fahren Sie mit dem Annotieren so lange fort, bis Watson Felder korrekt und konsistent angibt.
1. Wenn Sie mit dem Annotieren fertig sind, klicken Sie auf **Änderungen auf Sammlung anwenden**. Die Anzeige **Dokumente hochladen** wird geöffnet. (Dies wird sich nach der Betaversion ändern.) Sie können jetzt Ihre Dokumente hochladen, so dass die aktualisierten Einstellungen auf die gesamte Sammlung angewendet werden. Nachdem das Hochladen abgeschlossen ist, werden Sie zur Anzeige **Daten verwalten** weitergeleitet.


Feld | Definition  
------ | ------ 
answer | In einem Frage/Antwort-Paar (oft in einer häufig gestellten Frage) ist dies die Antwort auf die Frage.
author | Der Name des Autors (oder der Autoren).
footer | Verwenden Sie diesen Tag, um Metainformationen über das Dokument (z. B. die Seitenzahl oder die Verweise) zu bezeichnen, die am Ende der Seite angezeigt werden.
header | Verwenden Sie diesen Tag, um Metainformationen über das Dokument zu bezeichnen, das oben auf der Seite angezeigt wird.
question | In einem Frage/Antwort-Paar (oft in einer häufig gestellten Frage) ist dies die Frage.
subtitle | Der sekundäre Titel des Dokuments, das annotiert wird. Verwenden Sie diese Bezeichnung nur einmal pro Dokument.
table-of-contents | Verwenden Sie diesen Tag für Listen im Inhaltsverzeichnis des Dokuments.
text | Verwenden Sie diesen Tag für Standardkopiertexte, einschließlich Absätze, Definitionen oder eine Gruppe von Wörtern, die kein Titel, Teil einer Tabelle, eine Antwort, ein Autor, ein Untertitel, eine Kopfzeile oder eine Fußzeile ist. 
title | Der Haupttitel des Dokuments, das annotiert wird. Verwenden Sie diese Bezeichnung nur einmal pro Dokument.

### Tabellen im SDU-Editor annotieren
{: #tables} 

1. Wählen Sie das Feld `table` auf der rechten Seite und anschließend die Tabelle im SDU-Editor aus. 
1. Bewegen Sie den Mauszeiger über die Tabelle im SDU-Editor, um die Schaltfläche **Tabelle annotieren** anzuzeigen. Klicken Sie auf die Schaltfläche, um den Tabelleneditor zu öffnen.
1. Entwerfen Sie zunächst die Tabelle:
   - Wählen Sie das Feld `column` aus.
   - Klicken Sie auf eine Spalte in der Tabelle, um sie zu aktivieren.
   - Wählen Sie das Feld `row` aus.
   - Klicken Sie auf eine Zeile in der Tabelle, um sie zu aktivieren.

   Der Entwurf der Tabelle wird in der Tabellenvorschau auf der linken Seite angezeigt.

   **Hinweis:** Sie können auf **Vorhersagen** klicken, um eine Modellvorhersage für die Tabellenannotation anzuzeigen.
1. Kennzeichnen Sie als Nächstes den Inhalt in der Tabelle.
1. Nachdem Sie die Tabelle mit Annotationen versehen haben, klicken Sie auf **Fertig mit Annotieren**.
1. Klicken Sie auf **Änderungen auf Sammlung anwenden**. Die Anzeige **Dokumente hochladen** wird geöffnet. (Dies wird sich nach der Betaversion ändern.) Nachdem das Hochladen abgeschlossen ist, werden Sie zur Anzeige **Daten verwalten** weitergeleitet.

Feld | Definition  
------ | ------ 
table body | Eine Zelle, die keine Kopfzeile ist und Informationen enthält
column header | Die Kopfzeilenzelle (falls vorhanden) für jede Spalte in der Tabelle 
multi-column header | Alle Kopfzeilenzellen, die sich über mehr als eine Spalte erstrecken
subsection title | Die Spaltenüberschrift für die Spalte der Zeilenüberschriften (falls vorhanden)
row header | Die Zeilenbeschriftung (falls vorhanden) für jede Zeile in der Tabelle
multi-row header | Alle Zeilenbeschriftungen, die sich über mehr als eine Zeile erstrecken

## Best Practice für das Beschriften von Dokumenten und Tabellen
{: #bestpractices}

- Befolgen Sie alle Richtlinien und verwenden Sie konsistente Beschriftungen für alle Dokumente.
- Beschriften Sie keine Leerräume.
- Beschriften Sie keine Diagramme und Images.
- Behandeln Sie **fett** oder _kursiv_ formatierten oder unterstrichenen Text nicht anders; die Beschriftung basiert auf dem Kontext und nicht auf dem Stil. 
- Arbeiten Sie beim Beschriften eines Dokuments dieses von der ersten bis zur letzten Seite durch. Jede Seite muss übergeben werden, auch wenn nichts beschriftet wurde. 
- Wenn Sie ein Element fälschlicherweise beschriften, wählen Sie eine andere Beschriftung für das Element aus, um das erste Element zu überschreiben.
- Seiten können jederzeit übergeben werden. Stellen Sie sicher, dass alle erforderlichen Beschriftungen vor der Übergabe abgeschlossen sind.
- Verwenden Sie beim Beschriften von Dokumenten nicht die Zoomfunktion in Ihrem Browser.
- Dokumente und Tabellen, bei denen es so scheint, als ob Text anderen Text überlagert, gelten als 'doppelt überlagert' und können nicht annotiert werden. Melden Sie diese Dokumente Ihrem Administrator.
- Dokumente und Tabellen, die mehrere Spalten mit Text auf einer einzelnen Seite enthalten, können nicht annotiert werden. Melden Sie diese Dokumente Ihrem Administrator.
- Fußnoten sollten nur dann markiert sein, wenn sie am unteren Rand der Seite erscheinen und im Hauptteil des Textes im Dokument referenziert werden.
- Hinweise, die in Abschnitten oder Listen enthalten sind (z. B. explizit als 'Notizen' bezeichnet sind), sollten als `text` gekennzeichnet sein.
- Wenn Sie nicht sicher sind, dass die Tabelle korrekt bezeichnet wurde und das Vorschaufenster nicht mehr antwortet, sollte die Seite in Ihrem Browser neu geladen und die Tabelle erneut beschriftet werden, damit die Richtigkeit gewährleistet ist.

