---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-15"

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

# Operatori di query
{: #query-operators}

Gli operatori sono i separatori tra le diverse parti di una query. Per l'elenco completo degli operatori disponibili, consulta la [Guida di riferimento per le query](/docs/services/discovery?topic=discovery-query-reference#operators).

## . \[JSON delimiter\]
{: #delimiter}

Questo delimitatore separa i livelli di gerarchia nello schema JSON

Ad esempio:
```bash
enriched_text.concepts.text
```
{: codeblock}

## : \[Includes\]
{: #includes}

Questo operatore specifica una corrispondenza per il termine della query.

Ad esempio:
```bash
enriched_text.concepts.text:"cloud computing"
```
{: codeblock}

## :: \[Exact match\]
{: #match}

Questo operatore specifica una corrispondenza esatta per il termine della query.

Ad esempio:
```bash
enriched_text.concepts.text::"Cloud computing"
```
{: codeblock}

Le corrispondenze esatte sono sensibili a minuscole/maiuscole.

## :! \[Does not include\]
{: #notinclude}

Questo operatore specifica che i risultati non contengono una corrispondenza per il termine della query

Ad esempio:
```bash
enriched_text.concepts.text:!"cloud computing"
```
{: codeblock}

## ::! \[Not an exact match\]
{: #notamatch}

Questo operatore specifica che i risultati non corrispondono esattamente al termine della query

Ad esempio:
```bash
enriched_text.concepts.text::!"Cloud computing"
```
{: codeblock}

Le corrispondenze esatte sono sensibili a minuscole/maiuscole.

## \\ \[Escape character\]
{: #escape}

Carattere di escape per le query che richiedono la capacità di eseguire query dei termini utilizzando valori letterali di stringa che contengono caratteri di controllo.

Ad esempio:
```bash
title::"Dorothy said: \"There's no place like home\""
```
{: codeblock}

## "" \[Phrase query\]
{: #phrase}

Tutto i contenuti di una query di frase vengono elaborati come se ne fosse stato indicato l'escape. Quindi non viene analizzato alcun carattere speciale in una query di frase, fatta eccezione per le virgolette doppie (`"`) all'interno di una query di frase, di cui è necessario sia indicato l'escape (`\"`). Utilizza le query di frase con query full-text e basate sulla classificazione e non con operazioni di filtro booleano. Non utilizzare caratteri jolly (`*`) nelle query di frase. 

Le virgolette singole (`'`) non sono supportate.
{: note}

Ad esempio:
```bash
enriched_text.entities.text:"IBM watson"
```
{: codeblock}

## (), \[\] \[Nested grouping\]
{: #nestedquery}

I raggruppamenti logici possono essere formati per specificare informazioni più specifiche.

Ad esempio:
```bash
enriched_text.entities:(text:IBM,type:Company)
```
{: codeblock}

## \| \[or\]
{: #or}

Operatore booleano per "or".

Ad esempio:
```bash
enriched_text.entities.text:Google|IBM
```
{: codeblock}

## , \[and\]
{: #and}

Operatore booleano per "and".

Ad esempio:
```bash
enriched_text.entities.text:Google,IBM
```
{: codeblock}

## <=, >=, >, < \[Numerical comparisons\]
{: #comparisons}

Crea confronti numerici di meno di o uguale a, maggiore di o uguale a e maggiore di o meno di.

Ad esempio:
```bash
enriched_text.sentiment.document.score>0.679
```
{: codeblock}

## ^x \[Score multiplier\]
{: #multiplier}

Aumenta il valore di punteggio di un termine di ricerca.

Ad esempio:
```bash
enriched_text.concepts.text:IBM^3
```
{: codeblock}

## * \[Wildcard\]
{: #Wildcard}

Corrisponde a caratteri sconosciuti in un'espressione di ricerca. Non utilizzare lettere maiuscole con i caratteri jolly.

Ad esempio:
```bash
enriched_text.entities.text:ib*
```
{: codeblock}

## ~n \[String variation\]
{: #variation}

Il numero di cambiamenti di un singolo carattere che è necessario apportare a una stringa per renderla uguale a un'altra stringa. Ad esempio, `car~1` corrisponderà a `car`,`cap`,`cat`,`can`, ecc.

Ad esempio:
```bash
enriched_text.concepts.text:Watson~3
```
{: codeblock}

## :* \[Exists\]
{: #exists}

Utilizzato per restituire tutti i risultati dove esiste il `field` specificato.

Ad esempio:
```bash
title:*
```
{: codeblock}

## !* \[Does not exist\]
{: #dnexist}

Utilizzato per restituire tutti i risultati che non includono il `field` specificato.

Ad esempio:
```bash
title:!*
```
{: codeblock}
