---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-18"

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

# Crawlersuche für das Datenrepository durchführen
{: #crawling-your-data-repository}

Nachdem alle Crawleroptionen ordnungsgemäß konfiguriert worden sind, können Sie eine Crawlersuche für Ihr Datenrepository ausführen.
{: shortdesc}

Führen Sie den Crawler nur dann als Benutzer `root` aus, wenn Sie auf Dateien zugreifen müssen, die nur vom Benutzer `root` gelesen werden können.
{: tip}

Führen Sie den Befehl `crawler` aus.

Der Crawler gibt daraufhin eine Dokumentation aus, in der die möglichen Aktionen erläutert sind. Sie können eine Testcrawlersuche oder eine reguläre Crawlersuche ausführen. Außerdem stehen weitere Optionen für die Crawlersuche zur Verfügung.

## Testcrawlersuche ausführen

Führen Sie den Befehl `crawler testit` aus.

Dieser Befehl führt eine Testcrawlersuche aus, bei der lediglich die Seed-URL durchsucht wird und alle eingereihten URLs angezeigt werden. Falls die Seed-URL zu indexierbarem Inhalt führt (es sich also beispielsweise um ein Dokument handelt), wird dieser Inhalt an den Ausgabeadapter gesendet und in der Anzeige ausgegeben. Führt der Abruf der Seed-URL dazu, dass URLs eingereiht werden müssen, werden diese URLs angezeigt und es wird kein Inhalt an den Ausgabeadapter gesendet. Standardmäßig werden fünf eingereihte URLs angezeigt.

Sie können auch eine angepasste Konfigurationsdatei als Option für den Befehl 'crawl' angeben. Beispiel: `crawler testit --config [config/myconfigfile.conf]`.

Der Pfad zu der Konfigurationsdatei, der in der Option `--config` übergeben wird, muss ein qualifizierter Pfad sein. Er muss somit in relativen Formaten angegeben werden, z. B. `config/myconfigfile.conf` oder `./myconfigfile.conf`, bzw. als absoluter Pfad wie `/path/to/config/myconfigfile.conf`.

Des Weiteren können Sie als Option für den Befehl 'testit' die Anzahl der eingereihten URLs begrenzen, die angezeigt werden. Beispiel: `crawler testit --limit [anzahl]`.

## Crawlersuche ausführen

Führen Sie den Befehl `crawler crawl` aus.

Dieser Befehl führt eine Crawlersuche mit der Standardkonfigurationsdatei (`crawler.conf`) aus.

Sie können auch eine angepasste Konfigurationsdatei als Option für den Befehl 'crawl' angeben. Beispiel: `crawler crawl --config [config/myconfigfile.conf]`.

Der Pfad zu der Konfigurationsdatei, der in der Option `--config` übergeben wird, muss ein qualifizierter Pfad sein. Er muss somit in relativen Formaten angegeben werden, z. B. `config/myconfigfile.conf` oder `./myconfigfile.conf`, bzw. als absoluter Pfad wie `/path/to/config/myconfigfile.conf`.

## Crawlersuche erneut starten

Führen Sie den Befehl `crawler restart` aus.

Dieser Befehl führt einen Neustart der Crawlersuche aus, indem eine neue Crawlersuche mit der Standardkonfigurationsdatei (`crawler.conf`) gestartet wird.

Sie können auch eine angepasste Konfigurationsdatei als Option für den Befehl 'restart' angeben. Beispiel: `crawler restart --config [config/myconfigfile.conf]`.

Der Pfad zu der Konfigurationsdatei, der in der Option `--config` übergeben wird, muss ein qualifizierter Pfad sein. Er muss somit in relativen Formaten angegeben werden, z. B. `config/myconfigfile.conf` oder `./myconfigfile.conf`, bzw. als absoluter Pfad wie `/path/to/config/myconfigfile.conf`.

## Crawlersuche wiederaufnehmen

Führen Sie den Befehl `crawler resume` aus.

Dieser Befehl nimmt eine Crawlersuche mit der Standardkonfigurationsdatei (`crawler.conf`) an der Stelle wieder auf, an der sie gestoppt wurde.

Sie können auch eine angepasste Konfigurationsdatei als Option für den Befehl 'resume' angeben. Beispiel: `crawler resume --config [config/myconfigfile.conf]`.

Der Pfad zu der Konfigurationsdatei, der in der Option `--config` übergeben wird, muss ein qualifizierter Pfad sein. Er muss somit in relativen Formaten angegeben werden, z. B. `config/myconfigfile.conf` oder `./myconfigfile.conf`, bzw. als absoluter Pfad wie `/path/to/config/myconfigfile.conf`.

## Crawlersuche aktualisieren

Führen Sie den Befehl `crawler refresh` aus.

Dieser Befehl aktualisiert eine vorherige Crawlersuche mit der Standardkonfigurationsdatei (`crawler.conf`).

Sie können auch eine angepasste Konfigurationsdatei als Option für den Befehl 'refresh' angeben. Beispiel: `crawler refresh --config [config/myconfigfile.conf]`.

Der Pfad zu der Konfigurationsdatei, der in der Option `--config` übergeben wird, muss ein qualifizierter Pfad sein. Er muss somit in relativen Formaten angegeben werden, z. B. `config/myconfigfile.conf` oder `./myconfigfile.conf`, bzw. als absoluter Pfad wie `/path/to/config/myconfigfile.conf`.
