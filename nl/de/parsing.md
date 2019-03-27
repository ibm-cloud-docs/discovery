---

copyright:
  years: 2017, 2018, 2019
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

# Parsing von Verträgen
{: #contract_parsing}

Die Elementklassifizierung gibt geparste Verträge mit einer Analyse für jedes identifizierte Element zurück.

In den folgenden Abschnitten ist beschrieben, wie die Analyse in der JSON-Rückgabe bereitgestellt wird.

## types
{: #contract_types}

Das Array `types` enthält eine Reihe von Objekten, die jeweils die Schlüssel `nature` und `party` enthalten, deren Werte ein Couplet für das Element angeben.

In den folgenden Tabellen sind die möglichen Werte für die Schlüssel `nature` und `party` aufgelistet.

| `Gattung`         |Beschreibung                                                |
|:----------------:|-----------------------------------------------------------|
|`Definition`      |Dieses Element verdeutlicht einen Begriff, eine Beziehung oder einen ähnlichen Begriff. Zur Erfüllung dieses Elements ist keine Aktion erforderlich und keine Partei ist betroffen.|
|`Haftungsausschluss`      |Die Partei (`party`) im Element ist nicht verpflichtet, die durch das Element angegebenen Bedingungen zu erfüllen, wird hieran jedoch nicht gehindert.|
|`Ausschluss`       |Die Partei (`party`) im Element erfüllt nicht die durch das Element angegebenen Bedingungen.|
|`Verpflichtung`      |Die Partei (`party`) im Element muss die durch das Element angegebenen Bedingungen erfüllen.|
|`Recht`           |Der Partei (`party`) im Element wird gewährleistet, dass sie die durch das Element angegebenen Bedingungen erhält.|

Jeder Schlüssel des Typs `nature` wird paarweise mit einem Schlüssel des Typs `party` verbunden, der entweder den Namen oder die Rolle der Partei oder Parteien enthält, die sich auf die Gattung beziehen (Beispiele sind unter anderem `Buyer`, `IBM` oder `All Parties`). Beachten Sie, dass für die Gattung `Definition` die Partei immer den Wert `None` hat.

## parties
{: #contract_parties}

Das Array `parties` gibt die Teilnehmer an, die im Vertrag aufgelistet sind. Jedes Objekt `party` ist anderen Objekten zugeordnet, die Details zu der Partei angeben, darunter:

  - `role`: Die Rolle der Partei. Die Werte sind in der Tabelle aufgeführt, die auf diese Liste folgt.
  - `importance`: Die Wichtigkeit der Partei. Mögliche Werte sind `Primary` für eine Primärpartei oder `Unknown` für eine Nicht-Primärpartei.
  - `addresses`: Ein Array, das Adressen identifiziert.
    - `text`: Eine Adresse.
    - `location`: Die Position der Adresse, die durch die Indizes `begin` und `end` definiert wird.
  - `contacts`: Ein Array, das die Namen und Rollen von Kontakten definiert, die im Eingabedokument angegeben sind.
    - `name`: Der Name eines Kontakts.
    - `role`: Die Rolle des Kontakts.

Zu den Werten von `role`, die für Verträge zurückgegeben werden können, zählen unter anderem:

| `Rolle`           |Beschreibung                                                |
|:----------------:|-----------------------------------------------------------|
|`Einkäufer`           |Die Partei, die für die Bezahlung der im Vertrag aufgeführten Waren oder Dienstleistungen verantwortlich ist.|
|`Endbenutzer`        |Die Partei, die mit den bereitgestellten Waren oder Services interagiert und die sich explizit vom `Einkäufer` unterscheidet.|
|`Keine`            |Es wurde keine Partei für das Element angegeben.|
|`Lieferant`        |Die Partei, die für die Lieferung der im Vertrag aufgeführten Waren oder Dienstleistungen verantwortlich ist.|

## categories
{: #contract_categories}

Das Array `categories` definiert den Inhalt des Satzes. 

Die Kategorien und Beschreibungen in dieser Tabelle basieren auf den Rechtsgrundlagen der Vereinigten Staaten und sind in Gerichtsbarkeiten außerhalb der Vereinigten Staaten möglicherweise nicht anwendbar.
{: important}

Zu den derzeit unterstützten Kategorien gehören:

| `Kategorien`     |Beschreibung                                                |
|:----------------:|-----------------------------------------------------------|
|`Änderungen`      |Elemente, die Änderungen an dem Vertrag angeben, nachdem dieser signiert wurde, oder Änderungen an einem Standardvertrag. Enthält die Diskussionen über die Bedingungen für die Änderung der Bedingungen eines Vertrags.|
|`Assetverwendung`       |Elemente, die darauf verweisen, wie eine Partei die Assets einer anderen Partei verwenden darf oder nicht. Dies gilt insbesondere für eine Partei, die berechtigt ist, Ressourcen wie Lizenzen, Geräte, Tools oder Personal der anderen Partei zu nutzen oder zu verwenden, während sie ihre Aufgaben im Rahmen des Abkommens, einschließlich der Berechtigungen und der Einschränkungen, in der Vereinbarung durchführen.  Dies umfasst jedoch nicht Spezifikationen zu den Verpflichtungen einer Partei oder Rechte bezüglich erworbener Waren, Dienstleistungen, Lizenzen usw., da es sich hierbei um die eigenen Assets einer Partei handelt und nicht um die Assets einer anderen Partei.|
|`Abtretungen`     |Elemente, die die Übertragung von Rechten, Pflichten oder beides an eine andere Partei beschreiben.|
|`Prüfungen`          |Elemente, die sich entweder auf das Recht einer Partei beziehen, die Konformität zu untersuchen oder zu überprüfen, oder Anforderungen, die eine Partei für die Überprüfung oder Konformitätsprüfung zur Verfügung stellt. Dies schließt Verweise auf die Aufbewahrung von Datensätzen ein (vor allem in Bezug auf das Prüfungsrecht) und die Pflege und Aufbewahrung von Aktivitätsdatensätzen, die untersucht werden können.|
|`Business-Continuity`|Elemente, die sich auf die Folgen beziehen, wenn das gesamte Geschäft einer der Parteien verkauft wird.|
|`Kommunikation`  |Elemente, die sich auf Anforderungen zur Kommunikation, zu Antworten oder Mitteilungen beziehen; Kontaktinformationen oder Informationen über Änderungen am Vertrag. Enthält außerdem Verweise auf Details über Kommunikationsverfahren, den Akt oder den Prozess des Austauschs von Informationen und annehmbare Mittel zum Austausch von Informationen zwischen Parteien (sowie anderen, die nicht unbedingt direkt Vertragsparteien des Vertrags sind).|
|`Vertraulichkeit` |Elemente, die beschreiben, wie Parteien im Verlauf des Vertragsablaufs und darüber hinaus Gelerntes verwenden oder nicht verwenden können. Enthält zudem eine Beschreibung der Informationen, die vertraulich behandelt werden müssen, wie das Wahren von Geschäftsgeheimnissen oder das Geheimhalten von Geschäftsinformationen.|
|`Liefergegenstände`    |Elemente, die die Elemente (z. B. Waren oder Dienstleistungen) angeben, die von einer Partei unter den Bedingungen des Vertrags, in der Regel im Austausch für die Zahlung, bereitgestellt werden. Enthält eine Beschreibung der Vorbereitung der Liefergegenstände.|
|`Lieferung`        |Elemente, die die Mittel oder Modi für die Übertragung von Liefergegenständen (Dinge, im Gegensatz zu persönlichen Services) von einer Partei zu einer anderen angeben. Enthält die Beschreibungen der Merkmale der Lieferung, z. B. die Zeitplanung oder den Standort.|
|`Schlichtung`|Elemente, die die Regelungen für das Beilegen von Rechtsstreitigkeiten (z. B. in Bezug auf Arbeit, Rechnungen oder Rechnungsstellung) zwischen Vertragsparteien diskutieren.  Zu diesen Regelungen können die Beilegung durch ein festgelegtes Verfahren, wie ein Schiedsgericht, ein Prozess für das Erteilen einer einstweiligen Verfügung, der Verzicht auf ein Verfahren oder das Verbot zum Einreichen einer Sammelklage. Enthält außerdem Verweise auf das geltende Recht des Vertrags oder die Rechtswahl, wie ein bestimmtes Land oder eine bestimmte Gerichtsbarkeit. |
|`Höhere Gewalt`   |Elemente, die sich auf unerwartete oder störende Ereignisse beziehen, die außerhalb der Kontrolle einer Partei liegen, die die Partei von der Erfüllung ihrer vertraglichen Verpflichtung befreien würden.|
|`Freistellung` |Elemente, die die Korrektur bestimmter Verbindlichkeiten angeben, wenn eine Partei des Vertrags für die Entschädigung einer anderen Partei infolge eines entstandenen Schadens oder Schadens während der Laufzeit des Vertrags verantwortlich ist oder der sich aus den Umständen des Vertrags ergibt. Enthält außerdem Verweise auf alle gesetztlichen Freistellungen von Verlust oder Schäden.|
|`Versicherung`       |Elemente, die sich auf den Versicherungsschutz oder die Bedingungen des Versicherungsschutzes beziehen, der/die von einer Partei für eine andere Partei (einschließlich Drittparteien, wie Subunternehmer oder andere) bereitgestellt wird/werden. Enthält eine Vielzahl von Versicherungen, einschließlich, aber nicht beschränkt auf, Krankenversicherungen.|
|`Geistiges Eigentum`|Elemente, die die Abtretung von Rechten (z. B. Copyrights, Patente und Geschäftsgeheimnisse) an Parteien des Vertrags diskutieren. Enthält Verweise auf Patente, Rechte auf Patente, Marken, Handelsnamen, Dienstleistungsmarken, Domänennamen, Copyrights und alle Anwendungen und die Registrierung solcher Schemas, Industriemodelle, Erfindungen, Urheberschaft, Know-how, Geschäftsgeheimnisse, Computersoftwareprogramme und andere immaterielle proprietäre Informationen. Enthält zudem Informationen über die Folgen von Verletzungen der geistigen Eigentumsrechte.|
|`Haftung`       |Elemente, die die Methode beschreiben, mit der ermittelt wird, wann und wie einer Partei eine Verschuldung angelastet werden kann. Beispiele hierfür sind u. a. Angaben zu Haftungsbeschränkungen, Ansprüchen Dritter und Reparaturen, Ersetzungen oder Erstattungen, die von der schuldigen Partei verlangt werden.|
|`Zahlungsbedingungen & Rechnungsstellung`|Elemente, die detailliert beschreiben, wie und wann eine Party bezahlen muss oder Zahlungen erhält, sowie die Artikel oder Gebühren aufführen, die die Parteien bezahlen müssen oder in Rechnung gestellt bekommen. Enthält Verweise auf Zahlungsarten oder Zahlungsmechanismen.|
|`Preisgestaltung & Steuern` |Elemente, die sich auf bestimmte Mengen oder Zahlen zu einzelnen Liefergegenständen beziehen, die als deren Bestandteil (z. B. Kosten eines Artikels) im Rahmen der Erfüllung der Bedingungen des Vertrags ausgetauscht werden. Enthält Verweise auf bestimmte Zahlen oder Methoden zur Berechnung von Preisen oder Steuerbeträgen.|
|`Datenschutz`         |Elemente, die sich insbesondere auf die Handhabung sensibler persönlicher Informationen beziehen, in der Regel in Bezug auf ihren Schutz (beispielsweise zum Einhalten von Verordnungen wie der DSGVO).|
|`Zuständigkeiten`|Elemente, die Aufgaben im Rahmen des Vertrags diskutieren, die nur der Kontrolle einer Partei unterliegen und die sich speziell auf die Diskussion der Mitarbeiteraufsicht konzentrieren.|
|`Sicherheit`|Elemente, die sich auf die physische Sicherheit oder die Cybersicherheit für Personen, Daten oder Systeme beziehen. Beispiele hierfür sind Diskussionen über Hintergrundprüfungen, Sicherheitsvorkehrungen, Arbeitsplatzsicherheit, sichere Zugriffsprotokolle und Produktmängel, die eine Gefahr darstellen könnten.|
|`Leistungsumfang`   |Elemente, die definieren, was im Vertrag steht und was nicht im Vertrag steht und infolgedessen das, was entsprechend getan werden muss. Beispiele sind Mitteilungen zu einer bestimmten Bestellung oder Beschreibungen der im Vertrag angegebenen Ziele.|
|`Unterauftragsvergabe`    |Elemente, die sich auf die Beauftragung von Dritten beziehen, um bestimmte Aufgaben im Rahmen des Vertrags zu erfüllen, sowie die Berechtigungen, Rechte, Einschränkungen und Auswirkungen darauf und die daraus resultierenden Konsequenzen.|
|`Laufzeit & Kündigung`|Elemente, die sich auf die Dauer des Vertrags, den Zeitplan und die Bedingungen für die Beendigung des Vertrags und alle Folgen der Beendigung beziehen, einschließlich aller Verpflichtungen, die bei oder nach der Beendigung gelten.|
|`Gewährleistung`      |Elemente, die sich auf fortlaufende Zusagen und Verpflichtungen im Vertrag beziehen, die derzeit wahr sind und in der Zukunft weiterhin wahr sein werden. Außerdem Elemente, die die Konsequenzen beschreiben, die aus der Nichteinhaltung solcher Versprechen oder Verpflichtungen resultieren, und die Rechte, dieser Situation Abhilfe zu schaffen (z. B., aber nicht beschränkt auf, Schadensersatzansprüche). Diese Kategorie gilt nicht für Elemente, die sich ausschließlich auf die Darstellung von Sachverhalten beziehen (Tatsachenaussagen zur Vergangenheit oder Gegenwart) oder auf Elemente, die Annahmen bezüglich von Vorkommnissen aus der Vergangenheit darlegen.|

## attributes
{: #attributes}

Das Array `attributes` gibt alle Attribute an, die im Satz angegeben sind. Jedes Objekt im Array enthält drei Schlüssel: `type` (der Typ des Attributs aus der folgenden Tabelle), `text`  (der entsprechende Text) und `location` (die Indizes `begin` und `end`des Attributs im Eingabedokument). Zu den derzeit unterstützten Attributen gehören:

| `Attribute`     |Beschreibung                                                |
|:----------------:|-----------------------------------------------------------|
|`Adresse`         |Eine Postadresse.                                          |
|`Währung`        |Währungswerte und -einheiten.                                  |
|`Datum/Zeit`        |Ein Datum, eine Uhrzeit, ein Datumsbereich oder ein Zeitbereich.                   |
|`Position`        |Eine geografische Position oder Region.                         |
|`Organisation`    |Eine Organisation.                                           |
|`Person`          |Eine Person.                                                  |

## Gültigkeitsdaten
{: #effective_dates}

Das Array `effective_dates` gibt die Datumsangaben für die Gültigkeitsdauer des Dokuments an.

| `effective_dates`|Beschreibung                                                |
|:----------------:|-----------------------------------------------------------|
|`text`            |Ein Gültigkeitsdatum, das als Zeichenfolge aufgelistet ist.                     |
|`confidence_level`|Das Konfidenzniveau für die Angabe des Gültigkeitsdatums. Mögliche Werte sind `High`, `Medium` und `Low`.|
|`location`        |Die Position des Datums, die durch die Indizes `begin` und `end` definiert ist.|

## Vertragsbeträge
{: #contract_amounts}

Das Array `contract_amounts` gibt die im Dokument angegebenen Geldbeträge an.

| `contract_amounts`|Beschreibung                                               |
|:----------------:|-----------------------------------------------------------|
|`text`            |Ein Vertragsbetrag, der als Zeichenfolge aufgelistet ist.                  |
|`confidence_level`|Das Konfidenzniveau für die Angabe des Vertragsbetrags. Mögliche Werte sind `High`, `Medium` und `Low`.|
|`location`        |Die Position des Vertragsbetrags, die durch die Indizes `begin` und `end` definiert ist.|

## Datumsangaben für die Beendigung
{: #termination_dates}

Das Array `termination_dates` gibt die Datumsangaben für die Beendigung des Dokuments an.

| `contract_amounts`|Beschreibung                                               |
|:----------------:|-----------------------------------------------------------|
|`text`            |Das Beendigungsdatum, das als Zeichenfolge aufgelistet ist.                  |
|`confidence_level`|Das Konfidenzniveau für die Angabe des Beendigungsdatums. Mögliche Werte sind `High`, `Medium` und `Low`.|
|`location`        |Die Position des Beendigungsdatums, die durch die Indizes `begin` und `end` definiert ist.|

## provenance_ids
{: #provenance}

Jedes Objekt in den Arrays `types` und `categories` enthält ein Array des Typs `provenance_ids`. Das Array `provenance_ids` verfügt über einen oder mehrere Schlüssel. Jeder Schlüssel ist ein Hashwert, den Sie an IBM senden können, um Feedback zu geben oder Unterstützung zu erhalten.
