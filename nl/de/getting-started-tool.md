---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-02-08"

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

# Einführung
{: #getting-started}

In diesem kurzen Lernprogramm werden die {{site.data.keyword.discoveryshort}}-Tools vorgestellt. Sie werden durch den Prozess für die Erstellung einer privaten Datensammlung geführt und erfahren, wie Sie diese durchsuchen können.
{: shortdesc}

Wenn Sie lieber mit der API arbeiten, lesen Sie den Abschnitt [Einführung in die API](/docs/services/discovery?topic=discovery-gs-api#gs-api).
{: tip}

## Vorbereitende Schritte
{: #before-you-begin-tool}
{: hide-dashboard}

Für den Einstieg benötigen Sie eine Serviceinstanz.
{: hide-dashboard}

1.  {: hide-dashboard}Rufen Sie die [{{site.data.keyword.discoveryshort}}-Seite ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/catalog/services/discovery) im {{site.data.keyword.cloud_notm}}-Katalog auf.

    Die Serviceinstanz wird in der Ressourcengruppe **default** erstellt, wenn Sie keine andere auswählen, und kann später *nicht* mehr geändert werden. Diese Gruppe reicht aus, um den Service auszuprobieren.

    Wenn Sie eine Instanz für anspruchsvollere Anwendungen erstellen müssen, lesen Sie dazu die Informationen im Abschnitt [Ressourcengruppen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/docs/resources/bestpractice_rgs.html#bp_resourcegroups){: new_window}.
1.  {: hide-dashboard} Registrieren Sie sich entweder für ein kostenloses {{site.data.keyword.cloud_notm}}-Konto oder melden Sie sich an.
1.  {: hide-dashboard} Klicken Sie auf **Erstellen**.

## Schritt 1: Tools starten
{: #launch-the-tooling}

Nachdem Sie eine Instanz des {{site.data.keyword.discoveryshort}}-Service erstellt haben, werden Sie zu Ihrer Serviceliste geführt.
{: hide-dashboard}

1.  {: hide-dashboard} Klicken Sie auf die von Ihnen erstellte {{site.data.keyword.discoveryshort}}-Serviceinstanz, um zum Servicedashboard zu wechseln.
1.  Klicken Sie auf der Seite **Verwalten** auf **Tool starten**. Falls Sie aufgefordert werden, sich bei den Tools anzumelden, geben Sie Ihre {{site.data.keyword.cloud_notm}}-Berechtigungsnachweise an.

<!-- To do: Add screenshot for developer console -->

## Schritt 2: Sammlung erstellen
{: #create-a-collection-tool}

Ihr erster Schritt in den {{site.data.keyword.discoveryshort}}-Tools ist die Erstellung einer Datensammlung.

Eine Sammlung ist eine Gruppe von Dokumenten. *Es kann sinnvoll sein, mehrere Sammlungen zu verwenden.* Hierfür gibt es unter anderem die folgenden Gründe:

- Mit mehreren Sammlungen können Sie Ergebnisse für unterschiedliche Zielgruppen zusammenstellen.
- Die Daten sind unter Umständen so unterschiedlich, dass die gleichzeitige Abfrage aller Daten nicht zweckdienlich ist.

Die allgemein zugängliche und bereits aufbereitete {{site.data.keyword.discoverynewsshort}}-Datensammlung steht Ihnen ebenfalls zur Verfügung. Sie kann sofort abgefragt werden und Sie können umgehend mit der Erstellung von Abfragen für diese Sammlung beginnen. Ihre Konfiguration kann jedoch nicht angepasst werden; auch das Hinzufügen von Dokumenten zu {{site.data.keyword.discoverynewsshort}} ist nicht möglich.

1.  Klicken Sie auf ![Umgebungsdetails](images/env_icon.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> und wählen Sie **Umgebung erstellen** aus.
1.  Sobald Ihre Umgebung bereit ist, klicken Sie auf die Schaltfläche **Eigene Daten hochladen**. Anschließend können Sie Ihre neue **Datensammlung benennen**. Benennen Sie Ihre Sammlung mit **InstallDocs**.

    Beim Erstellen einer Sammlung im **Advanced**-Plan haben Sie die Option, eine Konfigurationsdatei mit dem Namen **Standardvertragskonfiguration** auszuwählen. Diese Konfiguration unterstützt nur die Aufbereitung 'Elementklassifizierung' zum Extrahieren von Partei-, Natur- und Kategorienelementen aus Elementen in PDFs. Details finden Sie unter [Elementklassifizierung](/docs/services/discovery?topic=discovery-element-classification#element-collection). Wählen Sie diese Option für dieses Lernprogramm nicht aus.

Sie können mit den {{site.data.keyword.discoveryshort}}-Tools auch Box-, Salesforce-, Microsoft SharePoint Online-, IBM Cloud Object Storage- und Microsoft SharePoint 2016-Datenquellen durchsuchen oder eine Web-Crawler-Suche durchführen. Klicken Sie auf die Schaltfläche **Datenquelle verbinden**; weitere Informationen hierzu finden Sie unter [Verbindung zu Datenquellen herstellen](/docs/services/discovery?topic=discovery-sources#sources).
{: tip}

## Schritt 3: Beispieldokument herunterladen und in die Sammlung hochladen
{: create-custom-configuration}

1.  Laden Sie dieses Beispiel-PDF-Dokument herunter: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/watsonexplorerinstall.pdf" download>Watson Explorer - Installationshandbuch<img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link" title="Symbol für externen Link"></a>. Eine vollständige Liste der Dokumenttypen, die in {{site.data.keyword.discoveryshort}} unterstützt werden, finden Sie unter [Unterstützte Dokumenttypen](/docs/services/discovery?topic=discovery-sdu#doctypes). 

    In einigen Browsern wird der Link in einem neuen Fenster geöffnet, anstatt lokal gespeichert zu werden. Falls dies der Fall ist, wählen Sie im Menü `Datei` des Browsers die Option `Speichern unter` aus, um eine Kopie der Datei zu speichern.
    {: tip}

1.  Laden Sie das Dokument in Ihre Sammlung hoch. Ziehen Sie es in Ihre Sammlung oder klicken Sie auf **Von Computer aus durchsuchen**, um Dokumente hochzuladen. Nachdem der Upload abgeschlossen ist, werden die folgenden Informationen angezeigt:
    -  Die Anzahl der Dokumente (1).
    -  Die Felder, die aus Ihrem Dokument identifiziert wurden. Es sollte ein Feld angegeben sein, `text`. Weitere Felder werden später identifiziert.
    -  Aufbereitungen, die auf Ihr Dokument angewendet wurden. Die Aufbereitungen Entitätsextraktion, Stimmungsanalyse, Kategorieklassifizierung und Konzepttagging werden von {{site.data.keyword.discoveryshort}} automatisch auf das Feld `text` angewendet. Weitere Informationen zu Aufbereitungen finden Sie [hier](/docs/services/discovery?topic=discovery-configservice#adding-enrichments). 
    -  Vordefinierte Abfragen können sofort ausgeführt werden.
1.  Probieren Sie eine schnelle Abfrage in natürlicher Sprache in der festgelegten Ebene. Klicken Sie auf die Schaltfläche **Eigene Abfrage erstellen** in der rechten unteren Ecke.
1.  Klicken Sie in der Anzeige **Abfragen erstellen** auf **Nach Dokumenten suchen** und dann auf **Natürliche Sprache verwenden**. Geben Sie die `Hardwaremindestvoraussetzungen` ein und klicken Sie auf die Schaltfläche **Abfrage ausführen**. Klicken Sie auf die Registerkarte **JSON** auf der rechten Seite. Das Ergebnis ist nicht so genau, wie es sein könnte, also verbessern Sie sie mittels Smart Document Understanding.
1.  Klicken Sie oben links auf den Namen der Sammlung (**InstallDocs**), um zur Anzeige **Übersicht** zurückzukehren.  
 
## Schritt 4: Dokument mit Annotationen versehen
{: #upload-your-documents}

Weitere Informationen zum Annotieren von Dokumenten finden Sie unter [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu).
{: tip}

1.  Klicken Sie auf die Schaltfläche **Daten konfigurieren** in der rechten oberen Ecke. 
1.  Die Anzeige **Daten konfigurieren** enthält drei Registerkarten: **Felder identifizieren**, **Felder verwalten** und **Felder aufbereiten**.
1.  Das `Watson Explorer - Installationshandbuch` wird auf der Registerkarte **Felder identifizieren** angezeigt und ist bereit für die Eingabe von Annotationen. Alle verfügbaren Felder (`answer`, `author`, `footer`, `header`, `question`, `subtitle`, `table_of_contents`, `text` und `title`) werden in der Liste **Feldbezeichnungen** auf der rechten Seite angezeigt. Wenn Sie einen Advanced- oder Premium-Plan erwerben, können Sie Ihre eigenen angepassten Bezeichnungen erstellen.

    Da das gesamte Dokument aktuell als `text` erkannt wird, sind die Marken auf der rechten Seite vollständig gelb dargestellt. Während Sie die Annotationen vornehmen (und das System mit der Vorhersage beginnt), werden die Farben aktualisiert.
    {: tip}

1.  Klicken Sie auf `title` und wählen Sie anschließend den Marker neben `Installations- und Integrationshandbuch` aus. Klicken Sie auf die Schaltfläche **Seite übergeben**.
1.  Klicken Sie in der Seitenvorschau auf der linken Seite auf Seite 3. Beachten Sie, dass `title` für diese Seite bereits vorhergesagt wurde. Klicken Sie auf die Schaltfläche **Seite übergeben**.
1.  Wählen Sie auf Seite 4 die Bezeichnung `footer` und den Marker neben der Fußzeile aus. Klicken Sie auf die Schaltfläche **Seite übergeben**.
1.  Auf den Seiten 5 und 6 können Sie die Fußzeilen mit der Bezeichnung `footer` annotieren. Übergeben Sie jede Seite. Klicken Sie auf mehrere weitere Seiten; Sie werden feststellen, dass die Fußzeile von {{site.data.keyword.discoveryshort}} korrekt vorhergesagt wurde. Annotieren Sie die Felder für `title` (bündig links) und `subtitle` (eingerückt) auf den Seiten 7, 9 und 10 und übergeben Sie jede Seite einzeln.
1.  Klicken Sie durch mehrere weitere Seiten und überprüfen Sie die vorhergesagten Titel und Untertitel. Wenn Änderungen erforderlich sind, müssen Sie diese Seiten annotieren und auf die Schaltfläche **Seite übergeben** klicken.
1.  Klicken Sie jetzt auf die Registerkarte **Felder verwalten** und teilen Sie unter **Verbessern der Abfrageergebnisse durch das Teilen Ihrer Dokumente** das Dokument nach `subtitle` auf. 
1.  Das genügt vorerst an Annotationen. Klicken Sie in der rechten oberen Ecke auf die Schaltfläche **Änderungen auf Sammlung anwenden**. Das Dialogfenster **Dokumente hochladen** wird angezeigt. Navigieren Sie zu der ursprünglichen Datei `watsonexplorerinstall.pdf` und laden Sie sie hoch. Dies gilt für alle Annotationen zu Ihrem Index. Nachdem die Indexierung abgeschlossen ist, wird die Anzeige **Übersicht** geöffnet. Es sollten jetzt mindestens 30 Dokumente sowie vier Felder angezeigt werden, die aus Ihren Daten identifiziert wurden: `footer`, `subtitle`, `text` und `title`. (Wenn die Änderungen nicht innerhalb weniger Minuten angezeigt werden, aktualisieren Sie das Browserfenster.)

    Sie können Felder (wie z. B. `footer`) aus der Indexierung ausschließen, indem Sie die Registerkarte **Felder verwalten** öffnen und dieses Feld mit der Umschaltfunktion `ausschalten`.
    {: tip}

## Schritt 5: Abfrage ausführen
{: #build-a-query}

1.  Klicken Sie in der rechten unteren Ecke auf **Eigene Abfrage erstellen**.
1.  Klicken Sie in der Anzeige **Abfragen erstellen** auf **Nach Dokumenten suchen** und dann auf **Natürliche Sprache verwenden**. Geben Sie die `Hardwaremindestvoraussetzungen` ein und klicken Sie auf die Schaltfläche **Abfrage ausführen**. 
1.  Klicken Sie auf die Registerkarte **JSON** auf der rechten Seite. Sehen Sie sich den `text` unter `results` an. Die Antworten, die für die Abfrage zurückgegeben werden, sind sehr viel präziser.

Zusätzliche Ressourcen:
-  Zusätzliche Informationen zum Datenschema Ihrer Dokumente erhalten Sie, wenn Sie ganz links auf das Symbol **Datenschema anzeigen** oder auf die Registerkarte **JSON** klicken. Details hierzu finden Sie unter [Discovery-Datenschema](/docs/services/discovery?topic=discovery-query-concepts#discovery-schema).
-  Klicken Sie auf die Schaltfläche **Beispielabfrage verwenden**, um Beispielabfragen in der {{site.data.keyword.discoveryshort}}-Abfragesprache zu testen.

## Nächste Schritte
{: #next-steps-tool}

Sie besitzen nun eine funktionsfähige und mit Daten bestückte {{site.data.keyword.discoveryshort}}-Serviceinstanz. Jetzt können Sie mit der Anpassung Ihrer Sammlung beginnen, indem Sie weitere Dokumente und Aufbereitungen hinzufügen sowie zusätzliche Dokumente mit Annotationen versehen. Weitere Informationen finden Sie unter [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu).
