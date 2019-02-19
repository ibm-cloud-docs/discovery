---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-26"

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

# Informationssicherheit
{: #information-security}

IBM ist bestrebt, unseren Kunden und Partnern innovative Datenschutz-, Sicherheits- und Governance-Lösungen zur Verfügung zu stellen.
{: shortdesc}

**Hinweis:**
Jeder Kunde ist für die Einhaltung der geltenden Gesetze und Vorschriften, einschließlich der Datenschutz-Grundverordnung (DSGVO) der Europäischen Union selbst verantwortlich. Es obliegt allein den Kunden, sich von kompetenter juristischer Stelle zu Inhalt und Auslegung aller relevanten Gesetze und Vorschriften beraten zu lassen, die ihre Geschäftstätigkeit und die von ihnen eventuell einzuleitenden Maßnahmen zur Einhaltung dieser Gesetze und Vorschriften betreffen.

Die hierin beschriebenen Produkte, Services und sonstigen Funktionen eignen sich nicht für alle Kundensituationen und sind möglicherweise nur eingeschränkt verfügbar. IBM erteilt keine Rechts- oder Steuerberatung und gibt keine Garantie bezüglich der Konformität von IBM Produkten oder Services mit den geltenden Gesetzen und Vorschriften.

Sie benötigen GDPR-Unterstützung für erstellte {{site.data.keyword.cloud}} {{site.data.keyword.watson}}-Ressourcen?

-   Innerhalb der Europäischen Union: Siehe [Unterstützung für in der Europäischen Union erstellte IBM Cloud Watson-Ressourcen anfordern](/docs/services/watson/getting-started-gdpr-sar.html#request-EU).
-   Außerhalb der Europäischen Union: Siehe [Unterstützung für Ressourcen außerhalb der Europäischen Region anfordern](/docs/services/watson/getting-started-gdpr-sar.html#request-non-EU).

## Datenschutz-Grundverordnung (DSGVO) der Europäischen Union
{: #gdpr}

IBM ist bestrebt, unseren Kunden und Partnern innovative Datenschutz-, Sicherheits- und Governance-Lösungen zur Verfügung zu stellen, um sie auf ihrem Weg zur Einhaltung der DSGVO zu unterstützen.

Erfahren Sie mehr zu den Bestrebungen von IBM zur Umsetzung der DSGVO und unseren eigenen DSGVO-Funktionen und -Angeboten für Ihre Compliance-Bemühungen, indem Sie [hier ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/gdpr){: new_window} klicken.

## Daten in {{site.data.keyword.discoveryshort}} kennzeichnen und löschen
{: #gdpr-discovery}

Der {{site.data.keyword.discoveryshort}}-Service enthält eine API, um Daten pro Aufruf zu kennzeichnen.

Mit dieser API können Sie:

- Ihre Daten mit einer Kunden-ID kennzeichnen.
- Alle Daten für eine bestimmte Kunden-ID, einschließlich der zugehörigen Hinweise, löschen.

Die Kennzeichnung der Daten erfolgt durch Hinzufügen einer Kunden-ID (`customer_id`) Ihrer Wahl (Einschränkungen hierzu unter [Vorgehensweise beim Kennzeichnen von Daten](/docs/services/discovery/information-security.html#labeling)) für den optionalen Header `X-Watson-Metadata`. {{site.data.keyword.discoveryshort}} kann die Daten dann nach `Kunden-ID` löschen.

Bei jedem REST-Aufruf kann ein optionaler Header `X-Watson-Metadata` mit durch Semikolon getrennte `field=value`-Paare gesendet werden, wobei gegenwärtig nur `customer_id` als persistent definiert wird. Durch das Hinzufügen des Werts für `customer_id` im Header `X-Watson-Metadata` zeigt die Anforderung an, dass sie Daten enthält, die zu dieser `Kunden-ID` gehören.

Die Werte für `customer_id` sind in einer {{site.data.keyword.discoveryshort}}-Serviceinstanz eindeutig. Sie sind NICHT eindeutig pro Umgebung oder Sammlung. Sie sollten keine personenbezogenen Daten enthalten.

**Hinweis:** Experimentelle und Beta-Features sind nicht für die Verwendung mit einer Produktionsumgebung gedacht. Es kann daher nicht garantiert werden, dass sie beim Kennzeichnen und Löschen von Daten wie erwartet funktionieren. Experimentelle und Beta-Features sollten bei der Implementierung einer Lösung, die die Kennzeichnung und Löschung von Daten erfordert, nicht verwendet werden.

## Methoden, die das Kennzeichnen von Daten unterstützen
{: #pi_methods}

Die folgenden gespeicherten Informationen können mit einer Kunden-ID (`customer_id`) gelöscht werden, falls der Wert für `customer_id` angegeben wurde, als die Informationen ursprünglich mit der zugehörigen Methode hinzugefügt wurde:

- Abfragen (`/v1/environments/{umgebungs-id}/collections/{sammlungs-id}/query`) Nur bei Verwendung der Parameter `passages` oder `natural_language_query`
- Ereignisse (`/v1/events`)
- Dokumente (`/v1/environments/{umgebungs-id}/collections/sammlungs-id}/documents`)
- Hinweise (`/v1/environments/{umgebungs-id}/collections/{sammlungs-id}/notices`) Nur `Hinweise` zum Einpflegen sind beschriftet.
- Knowledge Graph-Entitäten (`/v1/environments/{umgebungs-id}/collections/{sammlungs-id}/query_entities`)
- Knowledge Graph-Beziehungen (`/v1/environments/{umgebungs-id}/collections/{sammlungs-id}/query_relations`)
- Trainingsdaten (`/v1/environments/{umgebungs-id}/collections/{sammlungs-id}/training_data`)

Die folgenden gespeicherten Informationen sind nicht explizit gekennzeichnet und können nicht durch die Angabe der `customer_id` gelöscht werden. Persönliche Daten werden in diesen Feldern nicht unterstützt.

Zeichenfolgenfelder (einschließlich, jedoch nicht beschränkt auf `name` und `description`) der folgenden gespeicherten Elemente:
- configurations
- collections
- environments

## Daten kennzeichnen
{: #labeling}

Schließen Sie beim Einpflegen von Dokumenten den Header `X-Watson-Metadata` mithilfe der Operation `POST /v1/environments/{umgebungs-id}/collections/{sammlungs-id}/documents` oder `POST /v1/environments/{umgebungs-id}/collections/{sammlungs-id}/documents/ID` ein. Das Feld `customer_id` wird zu den extrahierten Metadaten (`extracted_metadata`) der Dokumente hinzugefügt. Ihre Anwendung sollte so konfiguriert sein, dass sie im Header `X-Watson-Metadata` eine Kunden-ID (`customer_id`) bereitstellt, wenn eine Operation ausgeführt wird.

Optional können Sie das Feld `customer_id` mit dem mehrteiligen Formularabschnitt `metadata` einbeziehen, anstatt den Header `X-Watson-Metadata` zu verwenden.

**Hinweis:** Falls Ihre Dokumente bereits eingepflegt wurden, müssen Sie sie erneut einpflegen, um den Header `X-Watson-Metadata` und `customer_id` hinzuzufügen.

**Hinweis:** Wenn Sie eine `customer_id` im mehrteiligen Formularabschnitt `metadata` und den Header `X-Watson-Metadata` für dasselbe Dokument angeben, wird die `customer_id` im Header `X-Watson-Metadata` verwendet.

Einschränkungen:

- Der Wert des Headers `X-Watson-Metadata` darf 4 Kilobyte Text nicht überschreiten.
- Der Header `X-Watson-Metadata` muss eine durch Semikolon getrennte Liste der Paare des Typs `field=value` enthalten. Dabei dürfen die Werte für `field` und `value` keine Semikolons (`;`) oder Gleichheitszeichen (`=`) enthalten.
- Die Werte für `customer_id` sind in jeder {{site.data.keyword.discoveryshort}}-Instanz eindeutig. Sie sind NICHT eindeutig pro Umgebung oder Sammlung.
- Eine `customer_id` darf nicht mehr als 256 Zeichen lang sein.
- Wenn eine `customer_id` nur Leerzeichen enthält oder komplett leer ist, wird sie so verarbeitet, als ob die `customer_id` nicht angegeben wurde und es werden keine Fehlernachrichten zurückgegeben.

### Daten mit den Discovery-Tools kennzeichnen
{: #labelingtooling}

Die Daten können bei der Verwendung der {{site.data.keyword.discoveryshort}}-Tools mit dem Feld `customer_id` gekennzeichnet werden. Klicken Sie auf ![Cog](images/icon_settings.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> und geben Sie die `Kunden-ID` im Feld für die **DSGVO-Datenkennzeichnung** ein. Sobald dieses Feld festgelegt wurde, werden alle mit dieser Browsersitzung hochgeladenen Daten mit dem angegebenen Wert für `customer_id` gekennzeichnet; dieses Feld muss manuell geändert werden, wenn die zugehörige Kunden-ID geändert wird.

Durch das Hinzufügen einer `Kunden-ID` für das Feld für die **DSGVO-Datenkennzeichnung** werden die Dokumente, Hinweise, Knowledge Graph-Entitäten, Knowledge Graph-Beziehungen und Trainingsdaten in dieser URL-Domäne von diesem Punkt ab gekennzeichnet, einschließlich der einzelnen Instanzen unter dieser Domäne. Alle Aktionen (einschließlich Dokumentuploads), die in den {{site.data.keyword.discoveryshort}}-Tools vor dem Hinzufügen des Feldes für die **GDPR-Datenkennzeichnung** durchgeführt wurden, werden nicht gekennzeichnet.

**Hinweis:** Wenn Sie Domänen wechseln, Browser wechseln, den Browsercache leeren oder eine anonyme Sitzung starten, nachdem Sie Ihre `Kunden-ID` im Feld für die **GDPR-Datenbezeichnung** der {{site.data.keyword.discoveryshort}}-Tools angegeben haben, wird die `Kunden-ID` nicht beibehalten und Ihre Daten werden nicht gekennzeichnet. Wenn Sie Domänen oder Browser wechseln müssen, geben Sie die `Kunden-ID` erneut im Feld für die **GDPR-Datenkennzeichnung** ein.

### Dokumente mit Data Crawler kennzeichnen
{: #labelingdc}

Wenn für Dokumente bereits eine Crawlersuche mit Data Crawler durchgeführt wurde, müssen Sie diese Dokumente erneut durchsuchen, um den Header `X-Watson-Metadata` und das Feld `customer_id` hinzuzufügen.

1. Aktualisieren Sie die {{site.data.keyword.discoveryshort}} Data Crawler-Ausgabeadapterkonfiguration so, dass sie die `Kunden-ID` enthält. Weitere Informationen finden Sie unter [Ausgabeadapter konfigurieren](/docs/services/discovery/data-crawler-discovery.html#output-adapter).
1. Planen Sie eine Crawlersuche. Die Dokumente werden unter Verwendung des Headers `X-Watson-Metadata` an {{site.data.keyword.discoveryshort}} übergeben und die Dokumente werden mit der konfigurierten `customer_id` gekennzeichnet.

## Gekennzeichnete Daten löschen
{: #deletingdata}

Die Daten müssen mit einer `customer_id` gekennzeichnet sein, damit sie später gelöscht werden können.

1. Verwenden Sie die Operation `DELETE /v1/user_data` und geben Sie die `customer_id` der Daten an, die Sie löschen wollen. Mit `DELETE /v1/user_data` werden alle Daten gelöscht, die einer bestimmten `customer_id` in dieser Serviceinstanz zugeordnet sind, wie unter [Methoden, die das Kennzeichnen von Daten unterstützen](/docs/services/discovery/information-security.html#pi_methods) angegeben. Weitere Informationen finden Sie auch in der [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html#delete-user-data){: new_window}.

Löschungen werden asynchron ausgeführt. Sie können den Fortschritt von Löschungen nicht verfolgen.

Wenn eine nicht vorhandene `customer_id` bereitgestellt wird, wird nichts gelöscht, es wird jedoch eine Antwort des Typs `200 - OK` zurückgegeben.

Umgebungen und Sammlungen sind nicht mit einer `customer_id` gekennzeichnet, auch wenn der Header `X-Watson-Metadata` in der Anforderung zum Erstellen der Umgebung oder Sammlung enthalten ist. Es werden nur die einzelnen Dokumente innerhalb einer Sammlung in einer Umgebung gekennzeichnet. Daher werden die einzelnen Umgebungen und Sammlungen beim Löschen von Daten NICHT gelöscht.

Gekennzeichnete Daten können mit den {{site.data.keyword.discoveryshort}}-Tools nicht gelöscht werden.
