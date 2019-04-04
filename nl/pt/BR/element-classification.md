---

copyright:
  years: 2015, 2018, 2019
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

# Classificação de elementos
{: #element-classification}

A Classificação de Elementos permite analisar rapidamente os documentos de controle para converter,
identificar e classificar elementos de importância. Usando o estado da arte Processamento de Linguagem Natural,
a parte (a quem ele se refere), a natureza (o tipo de elemento) e a categoria (classe específica) são extraídos
dos elementos de um documento.

A Classificação de Elementos é projetada para fornecer:

-  Entendimento de língua natural de contratos com ênfase nos Contratos de Compras de Software
-  A capacidade de converter PDF programático em JSON anotado
-  Identificação de Entidades e Categorias legais que se alinham ao conhecimento do assunto

A Classificação de Elementos reúne um conjunto funcionalmente completo de APIs do Watson integradas e
automatizada para inserir um PDF programático para identificação: seções, listas (numeradas e com marcadores),
notas de rodapé e tabelas que convertem esses itens em um formato HTML estruturado. Além disso, a
classificação desse formato estruturado é anotada e gerada como JSON com elementos, tipos e
categorias rotulados.

A Classificação de elementos transmite de forma segura seus dados que executam a criptografia em andamento e em repouso. Para obter informações sobre a segurança do IBM Cloud, veja a [Descrição do serviço do {{site.data.keyword.Bluemix_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=%28IBM+Cloud+Service+description%29){: new_window}

A Classificação de elementos retorna um objeto JSON que contém:

-  Um objeto `documents` que inclui o título do documento de entrada, uma versão HTML do documento de entrada e o hash MD5 do documento de entrada.
-  Informações sobre o modelo usado para classificar o documento de entrada.  
-  Uma matriz `elements` que detalha os elementos semânticos identificados no documento de entrada.
-  Uma matriz `tables` que divide as tabelas identificadas no documento de entrada.
-  Um objeto `document_structure` que lista títulos de seção e sentenças iniciais identificadas no documento de entrada.
-  Uma matriz `parties` que lista as partes, funções, endereços e contatos de partes identificadas no documento de entrada.
-  As matrizes que definem  ` effective_dates `, ` contract_quantias ` e  ` termination_dates `.

Esse recurso é suportado atualmente somente em inglês, veja [Suporte ao idioma](/docs/services/discovery?topic=discovery-language-support#feature-support) para obter detalhes.


## Requisitos de classificação
{: #element-class}

Para classificar documentos usando a Classificação de Elementos, seus documentos de configuração e de origem devem atender aos requisitos a seguir:

-  Os arquivos a serem analisados estão no formato PDF.
-  O conteúdo do PDF está no formato de texto. Documentos que foram varridos não podem ser analisados, mesmo que eles tenham sido reconhecidos por OCR.
   **Nota:** é possível identificar um PDF de texto abrindo o documento em
um visualizador de PDF e usando a ferramenta **Seleção de texto** para selecionar
uma única palavra. Se não for possível selecionar uma única palavra no documento, o arquivo não poderá ser
analisado.
-  Arquivos não são maiores que 50 MB em tamanho.
-  PDFs protegidos (com uma senha para abrir) e PDFs de edição restrita (com uma senha para edição) não podem ser analisados.
-  O conjunto de ferramentas do {{site.data.keyword.discoveryshort}} inclui uma configuração denominada **Configuração de contrato padrão** que pode ser usada para enriquecer sua coleção de documentos PDF. Você também tem a opção de criar uma configuração customizada que inclui o enriquecimento `elements`. Consulte  [ Requisitos de coleção ](/docs/services/discovery?topic=discovery-element-classification#element-collection)  para obter detalhes.
-  Os planos **Lite** podem processar um máximo de 500 páginas por mês.
-  Não disponível em ambientes **Dedicado**.
-  A normalização de pós-enriquecimento não pode ser executada ao usar a Classificação de elementos.

**Nota:** o arquivo de **Configuração de contrato padrão** foi atualizado em 25 de setembro de 2018. Se você aplicou essa configuração a uma coleção antes dessa data, veja as [notas sobre a liberação](/docs/services/discovery?topic=discovery-release-notes#25sept) para obter informações sobre como atualizar sua coleção.

## Requisitos de coleção
{: #element-collection}

Para usar a Classificação de elementos, sua coleção deve ser configurada para atender a requisitos específicos.

O conjunto de ferramentas do {{site.data.keyword.discoveryshort}} inclui uma configuração denominada **Configuração de contrato padrão** que foi pré-configurada para enriquecer documentos PDF com o enriquecimento **Classificação de elementos** e outras opções necessárias. É possível escolher essa configuração ao criar sua coleção. O JSON para esta configuração é:

```json
 {
   "name": "Default Contract Configuration",
   "description": "Extract party, nature, and category from elements in PDFs.",
  "conversions": {
     "html": {
       "exclude_tags_completely": [],
       "exclude_tags_keep_content": []
     }
   },
   "enrichments": [
     {
       "source_field": "html",
       "destination_field": "enriched_html_elements",
       "enrichment": "elements",
       "options": {
         "model": "contract" }
     }
   ]
 }
```
{: codeblock}

Se você deseja criar um arquivo de configuração customizado, configure sua coleção para atender aos requisitos a seguir:  

-  Configurações de conversão `PDF` serão ignoradas se especificadas.
-  As configurações de conversão `WORD` que podem ser omitidas como arquivos do
Microsoft Word não podem ser alimentadas quando a Classificação de Elementos é especificada.
-  As configurações de normalização `html` são ignoradas se especificadas.
-  A segmentação de documento não é suportada quando o enriquecimento `elements` é especificado.
-  Na configuração do {{site.data.keyword.discoveryshort}}, o campo `html`
deve ser aprimorado pelo enriquecimento `elements` e o
`model` especificado como `contract`. No exemplo a seguir, o `destination_field` é `enriched_html`, mas qualquer
nome válido pode ser usado:

```json
 "enrichments": [ {
     "source_field": "html",
    "destination_field": "enriched_html",
    "enrichment": "elements",
    "options": {
       "model": "contract" }
   }
 ]
```
{: codeblock}

Após selecionar `Default Contract Configuration` no conjunto de ferramentas, é possível fazer upload de seus documentos. Se
você não estiver familiarizado com a criação de coleções e com o upload de documentos, consulte
[Introdução ao conjunto de ferramentas](/docs/services/discovery?topic=discovery-getting-started#getting-started).

## Elementos classificados
{: #classified-elements}

Depois que um documento é indexado com Classificação de Elementos, ele é retornado com uma matriz `elements` como parte do documento pesquisável.

Cada objeto na matriz de `elements` descreve um elemento do contrato que o
{{site.data.keyword.discoveryshort}} identificou. O código a seguir representa um elemento típico:

```json
 {
    "location": {
     "begin" : 134323,
     "end" : 135109
    },
    "text" : "9. In the event that the Participant's total vested account balance is determined to be less than or equal to $2,000.00 as of the date that the Order is received, the parties will be informed in writing that the QDRO determination fee may potentially liquidate the account.",
   "types" : [ {
      "label" : {
        "nature" : "Obligation",
        "party" : "All Parties"
      },
      "provenance_ids" : ["Nlu0ogWAEGms4vjhhzpMv3iXhm8b8fBqMBNtT/bXH8JI=", "PlyERkjg5is36RpFjVUFXp69eDmGmCxLCXRs1sDMDUCo="
      ]
    } ],
   "categories" : [ {
      "label" : "Communication",
      "provenance_ids" : [ "Cs38YyU6VBFtJK1/bgtEJBlqqWmX5F6OYUciRxQXf7HrN5TOCPuI7QXbkbj4LRXoxVuB3/i9H15q5TU+vFxorhUBeWFfF998OYQiPYViD2yI="
      ]
    } ],
    "attributes" : [ {
      "type" : "Currency",
      "text" : "$2,000.00",
      "location" : {
        "begin" : 134780,
        "end" : 134789
      }
    } ]
 }
 ```
{: codeblock}

Cada elemento possui cinco seções importantes:
-  `location`: os índices `begin` e `end` que indicam o local do elemento no documento de entrada.
-  `text`: o texto do elemento classificado.
-  `types`: uma matriz que inclui zero ou mais objetos `label`. Cada objeto `label` inclui um campo `nature` que lista o efeito do elemento na parte identificada (por exemplo, `Right` ou `Exclusion`) e um campo `party` que identifica a parte ou as partes afetadas pelo elemento. Veja [Tipos](/docs/services/discovery?topic=discovery-contract_parsing#contract_types) em [Entendendo a análise sintática do contrato](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing) para obter informações adicionais.
-  `categories`: uma matriz que contém zero ou mais objetos `label`. O valor de cada objeto `label` lista uma categoria funcional na qual o elemento identificado cai. Veja [Categorias](/docs/services/discovery?topic=discovery-contract_parsing#contract_categories) em [Entendendo a análise sintática do contrato](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing) para obter informações adicionais.
-  `attributes`: uma matriz que lista zero ou mais objetos que definem os atributos do elemento. Os tipos de atributos atualmente suportados incluem `Location` (local geográfico mencionado pelo elemento), `DateTime` (data, hora, intervalo de data ou intervalo de tempo especificado pelo elemento) e `Currency` (unidades e valores monetários). Cada objeto na matriz `attributes` também inclui o texto e o local do elemento identificado; o local é definido pelos índices `begin` e `end` do texto no documento de entrada. Consulte [Atributos](/docs/services/discovery?topic=discovery-contract_parsing#attributes) em [Contratos de análise sintática](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing) para obter informações adicionais.

Além disso, cada objeto nas matrizes `types` e `categories` inclui uma matriz `provenance_ids`. Os valores listados na matriz `provenance_ids` são valores em hash que é possível enviar à IBM para fornecer feedback ou receber suporte sobre a parte da análise associada ao elemento. 

Algumas sentenças não se encaixam em nenhum tipo ou categoria. Nesse caso, o serviço retorna as matrizes `types` e `categories` como objetos vazios.
{: note}

Algumas sentenças abrangem múltiplos tópicos. Nesse caso, o serviço retorna múltiplos conjuntos de objetos `types` e `categories`.
{: note}

Algumas sentenças não contêm nenhum atributo identificável. Nesse caso, o serviço retorna a matriz `attributes` como objetos vazios.
{: note}
