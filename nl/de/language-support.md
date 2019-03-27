---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-18"

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

# Sprachunterstützung
{: #language-support}

Der {{site.data.keyword.discoveryfull}}-Service bietet zwei Stufen der Sprachunterstützung, nämlich eine **Basisunterstützung** und eine **vollständige Unterstützung**.
{: shortdesc}

| Sprache                         |  Unterstützungsstufe         |
|---------------------------------|------------------------|
| Englisch (en)                    |  Vollständig         |
| Arabisch (ar)                     |  Basis         |
| Vereinfachtes Chinesisch (zh-CN)     |  Basis         |
| Niederländisch (nl)                     |  Basis         |
| Französisch (fr)                     |  Vollständig         |
| Deutsch (de)                     |  Vollständig         |
| Italienisch (it)                    |  Vollständig        |
| Japanisch (ja)                  |  Vollständig         |
| Koreanisch (ko)                    |  Vollständig         |
| Portugisisch (Brasil.) (pt-br)   |  Vollständig         |
| Spanisch (es)                    |  Vollständig         |

## Basisunterstützung
{: #basic-support}

- Die {{site.data.keyword.discoveryshort}}-Unterstützung umfasst Folgendes:
    - Dokumentkonvertierung
    - Orchestrierung
    - Funktionalität der {{site.data.keyword.discoveryshort}}-Tools
    - Front-End-API (ohne Front-End-API für Abfragen)
    - Sprachoptimierter Index
    - Relevanztraining
    - Abfrageerweiterung
    - Stoppwörter
    - Dokumentation in 9 Sprachen: Englisch, Französisch, Deutsch, Japanisch, Koreanisch, Portugiesisch (Brasilien), Spanisch, Chinesisch (vereinfacht) und Chinesisch (traditionell). Blättern Sie bis zum Ende der {{site.data.keyword.Bluemix_notm}}-Dokumentation, um die Sprache auszuwählen.
- Aufbereitungen
    - Integration mit angepassten {{site.data.keyword.knowledgestudiofull}}-Modellen
    - Spracherkennung

## Vollständige Unterstützung
{: #full-support}

Die vollständige Unterstützung umfasst die Basisunterstützung zuzüglich Folgendem:

- Passagenabruf
- Übersetzte {{site.data.keyword.knowledgestudiofull}}-Schnittstelle
- Alle Aufbereitungen in {{site.data.keyword.nlushort}} (NLU) plus Metadatenextraktion. NLU-Aufbereitungen sind Folgende:
    - Entitätsextraktion
    - Schlüsselwortextraktion
    - Kategorieklassifizierung
    - Konzepttagging
    - Semantikrollenextraktion
    - Stimmungsanalyse
    - Emotionsanalyse (nur Englisch)

## Ausschließliche Unterstützung in Englisch
{: #feature-support}

Die folgenden Features werden gegenwärtig nur in Englisch unterstützt:

- Aufbereitung 'Elementklassifizierung'
- {{site.data.keyword.discoveryfull}} Knowledge Graph (Betaversion)
- Dokumentdeduplizierung (Betaversion)

## Unterstützung nur für Japanisch
{: #japanese-support}

Das folgende Feature wird gegenwärtig nur auf Japanisch unterstützt:

- Angepasste Wörterverzeichnisse für die Zerlegung in Tokens
