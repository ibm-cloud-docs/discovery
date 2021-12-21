---

copyright:
  years: 2015, 2021
lastupdated: "2021-08-06"

subcollection: discovery

---

{{site.data.keyword.attribute-definition-list}}

# Language support
{: #language-support}

{{site.data.keyword.discoveryfull}} offers two levels of language support, **Basic** and **Full**.
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

To create a collection in Dutch or Chinese, you must use the API. For more information, see the [API reference](https://cloud.ibm.com/apidocs/discovery#createcollection){: external}.

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
- Document deduplication (beta)

The Element Classification enrichment is deprecated and will no longer be available, effective **10 July 2020**.
{: important}

## Japanese-only support
{: #japanese-support}

The following feature is currently supported in Japanese only:

- Custom tokenization dictionaries
