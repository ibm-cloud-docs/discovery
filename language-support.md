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

# Language support
{: #language-support}

The {{site.data.keyword.discoveryfull}} service offers two levels of language support, **Basic** and **Full**.
{: shortdesc}

| Language                         |  Support Level         |
|---------------------------------|------------------------|
| English (en)                    |  Full         |
| Arabic (ar)                     |  Basic         |
| Chinese, simplified (zh-CN)     |  Basic         |
| Dutch (nl)                     |  Basic         |
| French (fr)                     |  Full         |
| German (de)                     |  Full         |
| Italian (it)                    |  Full        |
| Japanese (ja)                  |  Full         |
| Korean (ko)                    |  Full         |
| Portuguese, Brazilian (pt-br)   |  Full         |
| Spanish (es)                    |  Full         |

## Basic support
{: #basic-support}

- {{site.data.keyword.discoveryshort}} support includes:
    - Document conversion
    - Orchestration
    - {{site.data.keyword.discoveryshort}} Tooling functionality
    - Front-end API (excluding Front-end Query API)
    - Language-optimized index
    - Relevancy training
    - Query expansion
    - Stopwords
    - Documentation in 9 languages: English, French, German, Japanese, Korean, Brazilian Portuguese, Spanish, Chinese Simplified, and Chinese Traditional. Scroll to the bottom of the {{site.data.keyword.Bluemix_notm}} documentation to select the language.
- Enrichments
    - Integration with {{site.data.keyword.knowledgestudiofull}} custom models
    - Language detection

## Full support
{: #full-support}

Full support includes basic support, plus:

- Passage retrieval
- Translated {{site.data.keyword.knowledgestudiofull}} interface
- All {{site.data.keyword.nlushort}} (NLU) enrichments, plus metadata extraction. NLU enrichments are:
    - Entity Extraction
    - Keyword Extraction
    - Category Classification
    - Concept Tagging
    - Semantic Role Extraction
    - Sentiment Analysis
    - Emotion Analysis (English only)

## English-only support
{: #feature-support}

The following features are currently supported in English only:

- Element Classification enrichment
- {{site.data.keyword.discoveryfull}} Knowledge Graph (beta)
- Document deduplication (beta)

## Japanese-only support
{: #japanese-support}

The following feature is currently supported in Japanese only:

- Custom tokenization dictionaries
