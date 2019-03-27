---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-02-06"

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

# Einführung in die Ausführung von Abfragen
{: #getting-started-with-querying}

In diesem Lernprogramm erfahren Sie, wie Sie einige unterschiedliche Abfragetypen in der {{site.data.keyword.discoveryshort}}-Abfragesprache schreiben.
{: shortdesc}

Weitere Informationen zum Schreiben von Abfragen enthalten die folgenden Abschnitte:
- [Abfragekonzepte](/docs/services/discovery?topic=discovery-query-concepts#query-concepts)
- [Abfragereferenz](/docs/services/discovery?topic=discovery-query-reference#query-reference) (enthält eine Liste der in der {{site.data.keyword.discoveryshort}}-Abfragesprache verfügbaren Parameter, Operatoren und Aggregationen)

Die hier verwendeten Beispielabfragen wurden mit den {{site.data.keyword.discoveryshort}}-Tools erstellt. Wenn Sie stattdessen die API verwenden möchten, fügen Sie die Abfrageparameter zu Ihrem API-Aufruf hinzu. Weitere Informationen und Beispiele enthält der Abschnitt 'Abfragen' der [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/discovery#query-your-collection){: new_window}.

Sie können auch Abfragen in natürlicher Sprache (z. B. 'Partnerschaften von IBM Watson') mit den {{site.data.keyword.discoveryshort}}-Tools schreiben. Dieses Lernprogramm beschäftigt sich jedoch vorrangig mit dem Schreiben von Abfragen in der {{site.data.keyword.discoveryshort}}-Abfragesprache, da Ihre Anforderungen möglicherweise eine strukturierte Abfrage erforderlich machen können und Filter sowie Aggregationen in der {{site.data.keyword.discoveryshort}}-Abfragesprache geschrieben sein müssen.
{: tip}

## Vorbereitende Schritte
{: #querying-before-you-begin}

Wechseln Sie zur Anzeige **Daten verwalten**, erstellen Sie eine neue Sammlung namens '{{site.data.keyword.IBM_notm}} Press Releases' und fügen Sie ihnen die folgenden vier Dokumente hinzu: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link" title="Symbol für externen Link"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link" title="Symbol für externen Link"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link" title="Symbol für externen Link"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link" title="Symbol für externen Link"></a>

In einigen Browsern wird der Link in einem neuen Fenster geöffnet, anstatt lokal gespeichert zu werden. Falls dies der Fall ist, wählen Sie im Menü `Datei` des Browsers die Option `Speichern unter` aus, um eine Kopie der Datei zu speichern.
{: tip}

## Schritt 1: Schnelleinführung in das Discovery-Datenschema
{: #querying-step1}

Als Erstes lernen Sie die JSON-Ausgabe von {{site.data.keyword.discoveryshort}} kennen. Wenn Sie in der {{site.data.keyword.discoveryshort}}-Abfragesprache eine Abfrage erstellen, ist es hilfreich, wenn Sie mit der JSON-Ausgabe vertraut sind, die von {{site.data.keyword.discoveryshort}} erzeugt wird, nachdem die Dokumente in Ihrer Sammlung aufbereitet wurden.

1.  [Starten Sie die {{site.data.keyword.discoveryshort}}-Tools](/docs/services/discovery?topic=discovery-getting-started#launch-the-tooling). Wählen Sie in der Anzeige **Daten verwalten** die Sammlung '{{site.data.keyword.IBM_notm}} Press Releases' aus.

1.  Prüfen Sie die Informationen, die Watson in Ihren aufbereiteten Dokumenten ermittelt hat.

    -  Bei **Stimmungsanalyse** wird die prozentuale Aufschlüsselung der als positiv, neutral oder negativ gekennzeichneten Dokumente angezeigt, die von der Aufbereitung 'Stimmungsanalyse' erkannt wurden.
    -  Bei **Entitätsextraktion** werden Personen, Orte und Organisationen angezeigt, die durch die Aufbereitung 'Entitätsextraktion' in Ihren Dokumenten erkannt wurden.
    -  Bei **Kategorieklassifizierung** werden die hierarchischen Taxonomien angezeigt, die von der Aufbereitung 'Kategorieklassifizierung' in Ihren Dokumenten erkannt wurden.
    -  Bei **Konzepttagging** werden die Konzepte angezeigt, die von der Aufbereitung 'Konzepttagging' in Ihren Dokumenten erkannt wurden.

1.  Machen Sie sich mit dem Datenschema Ihrer Dokumente vertraut, indem Sie die Anzeige **Datenschema anzeigen** ansehen. Hier werden die Felder und Werte in Ihren konvertierten Dokumenten auf zwei Arten angezeigt, nämlich nach Dokument (**Dokumentansicht**) oder nach Feld (**Sammlungsansicht**). In der **Sammlungsansicht** werden alle Felder Ihrer Sammlung angezeigt.

    Klicken Sie auf das Symbol **Datenschema anzeigen** auf der linken Seite. In der **Sammlungsansicht** können Sie unter `enriched_text` die Aufbereitungen untersuchen, die Sie auf Ihre Sammlung angewendet haben. Klicken Sie auf `categories`, `concepts`, `entities` und `sentiment`, um festzustellen, wie Ihre Sammlung mit Watson-Informationen aufbereitet wurde.

Falls Ihre Abfrage keine passenden Ergebnisse zurückgibt, Sie jedoch der Ansicht sind, dass dies der Fall sein sollte, versuchen Sie, das Feld bzw. den Wert, das/den Ihre Abfrage verwendet, gegen etwas auszutauschen, das Sie im Datenschema überprüfen können.
{: tip}    

## Schritt 2: Basisabfrage erstellen
{: #querying-step2}

Zunächst schreiben Sie eine Abfrage, die das Konzept `Cloud computing` in Ihrer Sammlung sucht:

1.  Klicken Sie auf das Symbol **Abfragen erstellen** ![Abfragesymbol](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->, um die Abfrageseite zu öffnen. Wählen Sie die Sammlung aus, die '{{site.data.keyword.IBM_notm}} Press Releases' enthält, und klicken Sie auf **Lost geht's!**
1.  Klicken Sie in der Anzeige **Abfragen erstellen** auf **Dokumente suchen** und dann auf **{{site.data.keyword.discoveryshort}}-Abfragesprache verwenden**. Führen Sie anschließend Folgendes aus:
    - Klicken Sie auf die Dropdown-Liste **Feld** und wählen Sie den Eintrag `enriched_text.concepts.text` aus. Wählen Sie bei **Operator** die Einstellung `enthält` aus und geben Sie dann bei **Wert** die Zeichenfolge `Cloud computing` ein. Die Abfrage `enriched_text.concepts.text:Cloud computing` wird unter **Visual Query Builder** angezeigt.

    - Alternativ können Sie auf **In Abfragesprache bearbeiten** und dann auf **{{site.data.keyword.discoveryshort}}-Abfragesprache verwenden** klicken. Geben Sie `enriched_text.concepts.text:"Cloud computing"` im Feld **Abfrage hier eingeben** ein.

1.  Klicken Sie auf **Abfrage ausführen**. Es sollte eine Übereinstimmung (`"matching_results": 1`) erzielt werden. Kopieren Sie die **Abfrage-URL**, die oben auf der Registerkarte **Zusammenfassung** oder **JSON** angezeigt wird, um sie in Ihrer Anwendung zu verwenden.

**Bonus:** Unter **Weitere Optionen** haben Sie die Möglichkeit, den Abruf von Passagen durch Auswahl des Optionsfeldees **Relevante Passagen einbeziehen** zu aktivieren. Passagen sind kurze, relevante und aus den vollständigen Dokumenten, die von Ihrer Abfrage zurückgegeben wurden, extrahierte Auszüge. Diese gewünschten Passagen werden aus den Feldern `text` der Dokumente in Ihrer Sammlung extrahiert. Weitere Informationen enthält der Abschnitt [Passagen](/docs/services/discovery?topic=discovery-query-parameters#passages). Für die Sammlung '{{site.data.keyword.discoveryshort}} News' ist der Abruf von Passagen nicht verfügbar.

Falls Sie ein paar vordefinierte Abfragen ausprobieren möchten, klicken Sie auf die Schaltfläche **Beispielabfrage verwenden**.
{: tip}

## Schritt 3: Mit verschiedenen Abfragen experimentieren
{: #querying-step3}

Probieren Sie die folgenden Abfragen aus:

Um alle Dokumente mit einer `positiven` Stimmung zurückgeben zu lassen, klicken Sie auf **Dokumente suchen**, **{{site.data.keyword.discoveryshort}}-Abfragesprache verwenden** und führen Sie dann Folgendes aus:
-  Klicken Sie auf die Dropdown-Liste **Feld** und wählen Sie den Eintrag `enriched_text.sentiment.document.label` aus. Wählen Sie bei **Operator** die Einstellung `enthält` aus und geben Sie dann bei **Wert** die Zeichenfolge `positive` ein.  

   Die Abfrage `enriched_text.sentiment.document.label:positive` wird unter **Visual Query Builder** angezeigt.

Um alle Dokumente in der Kategorie `health and fitness` zurückgeben zu lassen, klicken Sie auf **Dokumente suchen**, **{{site.data.keyword.discoveryshort}}-Abfragesprache verwenden** und führen Sie dann Folgendes aus:
-  Klicken Sie auf die Dropdown-Liste **Feld** und wählen Sie den Eintrag `enriched_text.categories.label` aus. Wählen Sie bei **Operator** die Einstellung `ist` aus und geben Sie dann bei **Wert** die Zeichenfolge `"health and fitness"` ein.

   Die Abfrage `enriched_text.categories.label::"health and fitness"` wird unter **Visual Query Builder** angezeigt. Der Operator `::` gibt eine exakte Übereinstimmung an.

Um alle Dokumente zurückgeben zu lassen, die die Entität `IBM`, jedoch nicht die Entität `Watson` enthalten, klicken Sie auf **Dokumente suchen**, **{{site.data.keyword.discoveryshort}}-Abfragesprache verwenden** und führen Sie dann Folgendes aus:
-  Klicken Sie auf die Dropdown-Liste **Feld** und wählen Sie den Eintrag `enriched_text.entities.text` aus. Wählen Sie bei **Operator** die Einstellung `enthält` aus und geben Sie dann bei **Wert** die Zeichenfolge `IBM` ein. Klicken Sie auf **Regel hinzufügen**, wählen Sie dann für **Feld** den Eintrag `enriched_text.entities.text` aus, wählen Sie als **Operator** den Eintrag `enthält nicht` aus und geben Sie dann als **Wert** die Zeichenfolge `Watson` ein.

   Die Abfrage `enriched_text.entities.text:IBM,enriched_text.entities.text:!Watson` wird unter **Visual Query Builder** angezeigt. Der Operator `:!` steht für 'enthält nicht'.

## Schritt 4: Kombinierte Abfrage erstellen
{: #querying-step4}

Sie können Abfrageparameter kombinieren, um zielgerichtetere Abfragen zu erstellen. Sie verwenden jetzt die beiden Parameter `filter` und `query`, um Dokumente über {{site.data.keyword.IBM_notm}} Akquisitionen zurückgeben zu lassen. Der Parameter 'filter' grenzt die Ergebnisse auf Dokumente ein, die `IBM` enthalten; anschließend gibt der Parameter 'query' alle Ergebnisse über `acquisitions` in der Reihenfolge ihrer Relevanz zurück.

1.  Klicken Sie auf das Symbol 'Abfragen erstellen' ![Abfragesymbol](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->, um die Abfrageseite zu öffnen. Wählen Sie die Sammlung aus, die '{{site.data.keyword.IBM_notm}} Press Releases' enthält, und klicken Sie auf **Lost geht's!**

1.  Führen Sie unter **Abzufragende Dokumente filtern** Folgendes aus:
    -  Klicken Sie auf die Dropdown-Liste **Feld** und wählen Sie den Eintrag `enriched_text.entities.text` aus. Wählen Sie bei **Operator** die Einstellung `enthält` aus und geben Sie dann bei **Wert** die Zeichenfolge `IBM` ein.

       Die Abfrage `enriched_text.entities.text:IBM` grenzt die Dokumente auf diejenigen ein, in denen die Entität `IBM` erwähnt ist.

1.  Klicken Sie unter **Dokumente suchen** auf **{{site.data.keyword.discoveryshort}}-Abfragesprache verwenden** und führen Sie dann Folgendes aus:
    -  Klicken Sie auf die Dropdown-Liste **Feld** und wählen Sie den Eintrag `enriched_text.concepts.text` aus. Wählen Sie bei **Operator** die Einstellung `enthält` aus und geben Sie dann bei **Wert** die Zeichenfolge `world wide web` ein.

       Die Abfrage `enriched_text.concepts.text:"world wide web"` gibt alle Dokumente zurück, die das Konzept `world wide web` enthalten; die Dokumente werden in der Reihenfolge ihrer Relevanz aufgelistet.

1.  Klicken Sie auf **Weitere Optionen**, klicken Sie anschließend auf **Zurückzugebende Felder** und wählen Sie **Angeben** aus. Wählen Sie `text` aus. Dies beschränkt die Antwort auf den Text der relevanten Artikel und schließt alle anderen Angaben aus.

1.  Klicken Sie auf **Abfrage ausführen**. Es gibt ein übereinstimmendes Dokument: `"matching_results": 1`.

## Schritt 5: Aggregation erstellen
{: #querying-step5}

Aggregationen geben eine Gruppe von Datenwerten zurück, beispielsweise wichtige Schlüsselwörter, Gesamtstimmung von Entitäten und anderes.

Sie erstellen jetzt eine Aggregation, die die wichtigsten 10 Konzepte in der Sammlung '{{site.data.keyword.IBM_notm}} Press Releases' zurückgibt.

1.  Klicken Sie auf das Symbol **Abfragen erstellen** ![Abfragesymbol](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->, um die Abfrageseite zu öffnen. Wählen Sie die Sammlung aus, die '{{site.data.keyword.IBM_notm}} Press Releases' enthält, und klicken Sie auf **Lost geht's!**

1.  Führen Sie unter **Analyse der Ergebnisse einbeziehen** Folgendes aus:
    -  Klicken Sie auf die Dropdown-Liste **Ausgabe** und wählen Sie `Höchste Werte` aus. Wählen Sie bei **Feld** den Eintrag `enriched_text.concepts.text` aus und geben Sie dann für **Anzahl** den Wert `10` ein.

       Die Option `term` gibt die häufigsten Werte für das Feld `text` von `concepts` zurück. Die **Anzahl** gibt die Anzahl der Ergebnisse an, die zurückgegeben werden sollen. Die Abfrage `term(enriched_text.concepts.text,count:10)` wird unter **Visual Query Builder** angezeigt.   

1.  Klicken Sie auf **Weitere Optionen** und geben Sie dann den Wert `0` im Feld **Anzahl zurückzugebender Dokumente** ein.

1.  Klicken Sie auf **Abfrage ausführen**. Die häufigsten 10 Konzepte werden auf beiden Registerkarten **Zusammenfassung** und **JSON** angezeigt. Nachfolgend sehen Sie ein Beispiel für die Zusammenfassung:

## Schritt 6: Abfrage in Watson Discovery News erstellen
{: #querying-step6}

Die Sammlung '{{site.data.keyword.discoverynewsshort}}' ist ein allgemein zugänglicher Datenbestand, der vorab mit kognitiven Informationen aufbereitet wurde. Die Sammlung ist in {{site.data.keyword.discoveryshort}} enthalten. Weitere Informationen zu dieser Sammlung finden Sie unter [Watson Discovery News](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news).

Das Anpassen der {{site.data.keyword.discoverynewsshort}}-Konfiguration, das Durchführen eines Trainings oder das Hinzufügen von Dokumenten zur Sammlung '{{site.data.keyword.discoverynewsshort}}' ist nicht möglich. Was Sie mit {{site.data.keyword.discoverynewsshort}} erstellen können, wird in einer [Demo ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://discovery-news-demo.ng.bluemix.net/){: new_window} gezeigt.

Die folgende Beispielabfrage gibt die wichtigsten 10 Artikel in {{site.data.keyword.discoverynewsfull}} über die Pittsburgh Steelers mit einer positiven Stimmung zurück.

1.  Klicken Sie auf das Symbol **Abfragen erstellen** ![Abfragesymbol](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->, um die Abfrageseite zu öffnen. Wählen Sie die Sammlung '{{site.data.keyword.discoverynewsshort}}' aus und klicken Sie auf **Los geht's!** (Um die {{site.data.keyword.discoverynewsshort}}-Sammlungen für Spanisch, Deutsch oder Koreanisch abzufragen, müssen Sie zunächst auf das Symbol ![Daten verwalten](/images/icon_yourData.png) klicken und dann die entsprechende Sprache aus der Dropdown-Liste auswählen.)

1.  Klicken Sie unter **Dokumente suchen** auf **{{site.data.keyword.discoveryshort}}-Abfragesprache verwenden** und führen Sie dann Folgendes aus:
    -  Klicken Sie auf die Dropdown-Liste **Feld** und wählen Sie den Eintrag `text` aus. Wählen Sie bei **Operator** die Einstellung `enthält` aus und geben Sie dann bei **Wert** die Zeichenfolge `Pittsburgh Steelers` ein. Klicken Sie auf **Regel hinzufügen**, klicken Sie dann auf die Dropdown-Liste **Feld** und wählen Sie `enriched_text.sentiment.document.label` aus, wählen Sie als **Operator** den Eintrag `enthält` aus und geben Sie dann als **Wert** die Zeichenfolge `positive` ein.

       Die Abfrage `text:"Pittsburgh Steelers",enriched_text.sentiment.document.label:"positive"` wird unter **Visual Query Builder** angezeigt.

1.  Klicken Sie auf **Weitere Optionen** und geben Sie dann den Wert `10` (dies ist der Standardwert) im Feld **Anzahl zurückzugebender Dokumente** ein.

1.  Klicken Sie auf **Abfrage ausführen**. Die wichtigsten 10 Artikel über die Pittsburgh Steelers mit einer positiven Stimmung werden angezeigt.

**Hinweis:** Die maximale Anzahl der zurückgegebenen Ergebnisse für eine Abfrage von Watson Discovery News ist `50`.

Neue Artikel können für mehrere Nachrichtenausgaben syndiziert werden. {{site.data.keyword.discoverynewsfull}} nimmt alle diese Artikel auf, was zu doppelten Artikeln führt. Dies bedeutet, dass eine Abfrage von {{site.data.keyword.discoverynewsfull}} potenziell identische oder nahezu identische Artikel in Abfrageergebnissen zurückgibt. Unter **Weitere Optionen** können Sie durch Auswahl von **Doppelte Ergebnisse ausschließen** die Deduplizierung aktivieren. Mehr über diese Betafunktionalität enthält der Abschnitt [Doppelte Dokumente aus Abfrageergebnissen ausschließen](/docs/services/discovery?topic=discovery-query-parameters#deduplication).
