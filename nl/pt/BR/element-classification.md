---

copyright:
  years: 2015, 2017
lastupdated: "2017-12-15"

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

# Classificação de elementos
{: #element-classification}

A Classificação de Elementos permite analisar rapidamente os documentos de controle para converter,
identificar e classificar elementos de importância. Usando o estado da arte Processamento de Linguagem Natural,
a parte (a quem ele se refere), a natureza (o tipo de elemento) e a categoria (classe específica) são extraídos
dos elementos de um documento.

A Classificação de Elementos é projetada para fornecer:

- Natural Language Understanding de Contratos com ênfase nos documentos de Contratos e Regulamentos de Compra de Software
- A capacidade de converter PDF programático em JSON anotado
- Identificação de Entidades e Categorias legais que se alinham ao conhecimento do assunto

A Classificação de Elementos reúne um conjunto funcionalmente completo de APIs do Watson integradas e
automatizada para inserir um PDF programático para identificação: seções, listas (numeradas e com marcadores),
notas de rodapé e tabelas que convertem esses itens em um formato HTML estruturado. Além disso, a
classificação desse formato estruturado é anotada e gerada como JSON com elementos, tipos e
categorias rotulados.

A Classificação de Elementos transmite seguramente seus dados executando criptografia em andamento e em repouso. Para obter informações sobre segurança do IBM Cloud, consulte o
[Descrição
do serviço do IBM Cloud ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link
externo")](http://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=IBM+Bluemix+Service+Description){: new_window}.

## Requisitos de classificação

Para classificar documentos usando a Classificação de Elementos, seus documentos de configuração e de origem devem atender aos requisitos a seguir:

- Os arquivos a serem analisados estão no formato PDF.
- O conteúdo PDF está em formato de texto (documentos que foram digitalizados, mas que não passaram por OCR, não podem ser analisados)

  **Nota:** é possível identificar um PDF de texto abrindo o documento em
um visualizador de PDF e usando a ferramenta **Seleção de texto** para selecionar
uma única palavra. Se não for possível selecionar uma única palavra no documento, o arquivo não poderá ser
analisado.

- Arquivos não são maiores que 50 MB em tamanho.
- PDFs protegidos (com uma senha para abrir) e PDFs de edição restrita (com uma senha para edição) não podem ser analisados.
- Deve ser criada uma configuração customizada do {{site.data.keyword.discoveryshort}} que inclua o enriquecimento de `elements`. Essa configuração pode ser usada somente para alimentar documentos PDF.
- Planos **Lite** e **Padrão** podem processar um máximo de 500 páginas por mês.
- Não disponível para instâncias de serviço que estejam inscritas no plano **Premium**.

## Requisitos de coleção

Para usar a Classificação de Elementos, sua coleção deve ser configurada para atender a requisitos
específicos como segue:

- Configurações de conversão `PDF` serão ignoradas se especificadas. 
- As configurações de conversão `WORD` que podem ser omitidas como arquivos do
Microsoft Word não podem ser alimentadas quando a Classificação de Elementos é especificada.
- As configurações de normalização `html` são ignoradas se especificadas. 
- A divisão do documento não é suportada quando o enriquecimento de `elements`
é especificado.
- Na configuração do {{site.data.keyword.discoveryshort}}, o campo `html`
deve ser aprimorado pelo enriquecimento `elements` e o
`model` especificado como `contract`.
No exemplo a seguir, o `destination_field` é `enriched_html`, mas qualquer
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

Essas opções podem ser incluídas usando o conjunto de ferramentas {{site.data.keyword.discoveryshort}}, crie uma configuração customizada e inclua o enriquecimento **Classificação de Elementos** no campo `html`.

**Nota:** ao incluir **Classificação de Elementos** usando o
conjunto de ferramentas, o `destination_field` é configurado como
`enriched_html_elements`.

Após a configuração customizada ter sido criada, ela poderá ser usada em qualquer coleção e qualquer
método para fazer upload de documentos poderá ser usado enquanto a configuração customizada é especificada. Se
você não estiver familiarizado com a criação de coleções e com o upload de documentos, consulte
[Introdução ao conjunto de ferramentas](/docs/services/discovery/getting-started-tool.html).

## Elementos classificados

Depois que um documento é indexado com Classificação de Elementos, ele é retornado com uma matriz `elements` como parte do documento pesquisável.

Cada objeto na matriz `elements` descreve um elemento do contrato que a Classificação de Elementos identificou. O código a seguir representa um elemento típico:

```
{
   "sentence" : {
     "begin" : 34941,
     "end" : 35307
   },
   "sentence_text" : "A buyer must buy from the supplier.",
   "types" : [ {
     "label" : {
       "nature" : "Obligation",
       "party" : "Supplier"
     },
     "assurance" : "High"
   } ],
   "categories" : [ {
     "label : "Responsibilities",
     "assurance : "High"
     }
   ]
}
```

Há quatro seções importantes para o elemento:

- `sentence_text` – o texto que foi analisado.
- `sentence` - esse objeto descreve o local em que o elemento foi encontrado no HTML
convertido e contém um valor de caractere inicial e um valor de caractere final.
- `types` – essa matriz descreve o que é o elemento e quem o afeta consiste em um ou
mais conjuntos de `party` (quem está sendo afetado pela sentença) e `nature`
(o efeito da sentença na parte identificada)
- `categories` - essa matriz lista as categorias funcionais em que a sentença identificada se encaixa. O assunto da sentença.

**Nota**: algumas sentenças não se encaixam em nenhum tipo ou categoria e, nesse caso,
as matrizes de `types` e `categories` são retornadas vazias.

**Nota:** algumas sentenças cobrem múltiplos tópicos e, portanto, serão retornadas com múltiplos itens `types` e `categories` listados.

Além disso, quaisquer partes identificadas também são definidas na matriz de partes:

```
  "parties" : [ {
    "party" : "Customer",
    "role" : "Buyer"
  } ]
```

Há duas seções importantes para cada elemento da matriz de partes:

- `party` - o texto que foi identificado como uma parte dentro do documento.
- `role` - a função da parte que foi identificada. As funções mudam com base em subdomínio, consulte as informações sobre o subdomínio especificado para obter uma lista de funções possíveis. As partes que não podem ser identificadas para uma função específica são rotuladas como


## Entendendo os elementos do contrato

Os contratos analisados por meio da Classificação de Elementos são retornados com cada elemento identificado analisado.

As seções a seguir descrevem como o JSON retornado descreve a análise.

### Tipo

O elemento `types` de informações é uma matriz de objetos, em que cada objeto contém uma natureza e uma parte que foram identificadas como uma combinação para este elemento. As tabelas a seguir
descrevem as possíveis `natures` e `parties` que podem ser identificadas.

As naturezas são os tipos de ação que a sentença requer.

| **Natureza** | **Descrição** |
| --- | --- |
| Definição | Este elemento inclui clareza para um termo/relacionamento, etc. Uma ação não é necessária para cumprir este elemento e nenhuma parte é afetada. |
| Renúncia de Responsabilidade | A parte no elemento não é obrigada a cumprir os termos específicos no elemento, mas não está impedida de fazer isso.  |
| Exclusão | A parte no elemento não cumprirá os termos específicos dispostos no elemento.  |
| Obrigação | A parte no elemento é obrigada a cumprir os termos do elemento.   |
| Certo | É garantido que a parte no elemento receberá os termos do elemento.  |

### Partes

Para cada cláusula identificada, as partes afetadas são identificadas por nome. Cada parte identificada
é, então, classificada por `role`. As partes são os participantes no contrato. As funções que
podem ser identificadas para o contrato são as seguintes:

| **Função** | **Descrição** |
| --- | --- |
| `Buyer` | A parte responsável por pagar pelas mercadorias/serviços. |
| `End User` | A parte que irá interagir com as mercadorias/serviços reais, explicitamente
distintos do Buyer. |
| `None` | Nenhuma parte foi identificada para esse elemento, sempre emparelhado com a natureza Definição. |
| `Supplier` | A parte responsável por fornecer as mercadorias/serviços. |

### Categorias

As categorias definem o assunto da sentença. As categorias a seguir podem ser identificadas.

| **Categorias** | **Descrição** |
| --- | --- |
| `Amendments` | Uma modificação do contrato original que estipula as condições para mudança
dos termos. |
| `Asset Use` | Detalhes sobre quaisquer ativos no contrato que serão usados por qualquer uma
das partes. |
| `Assignments` | Inclui a transferência dos direitos mantidos por uma parte para outra.  |
| `Audits` | Essa cláusula permite que o comprador examine ou inspecione o fornecedor dos serviços que estão sendo fornecidos. |
| `Communication` | Descreve os métodos de comunicação e as informações de contato aceitáveis. |
| `Confidentiality` | Descreve como informações confidenciais ou privadas serão manipuladas, como quem pode compartilhar o que e como. |
| `Business Continuity` | Descreve como uma organização continuará a entrega de trabalho nos níveis predefinidos, no caso de um incidente disruptivo. |
| `Definitions` | Uma seção que define um termo usado no documento. |
| `Deliverables` | Os itens ou serviços a serem entregues no término de uma parte do trabalho. |
| `Delivery` | A programação ou o processo específico para concluir um projeto. |
| `Dispute Resolution` | Prepara-se para qualquer litígio que possa ocorrer entre as partes contratantes e como ele será resolvido. |
| `Force Majeure` | Uma cláusula que isenta ambas as partes de responsabilidade em caso de um evento disruptivo. |
| `Indemnification` | Descreve as soluções ou as consequências, caso os termos sejam violados. |
| `Insurance` | Descreve o nível de cobertura de seguro que um fornecedor deve conduzir. |
| `Intellectual Property` | Uma cláusula que está relacionada a patentes, direitos autorais e marcas comerciais. Mais geralmente pode relacionar-se à invenção, à autoria ou ao know-how.  |
| `Liability` | Descreve as obrigações e as limitações sobre a responsabilidade de cada parte. |
| `Miscellaneous` | Seções de interesse que não se encaixam em outras categorias. |
| `Payment Terms & Billing` | Descreve quais pagamentos são devidos e para que o pagamento está agendado. |
| `Pricing & Taxes` | Descreve como os preços são definidos e como os impostos devem ser aplicados |
| `Privacy` | Descreve os regulamentos de privacidade que se aplicam. |
| `Responsabilidades` | Descreve quais são as responsabilidades de cada parte. |
| `Safety and Security` | Descreve como evitar danos a uma parte. Inclui segurança para a equipe e para o ativo físico. |
| `Scope of Work` | Descreve detalhadamente o que as partes alcançarão de acordo com a descrição do trabalho. |
| `Subcontracts` | Relaciona quaisquer terceiros envolvidos para cumprir um requisito. |
| `Term & Termination` | O tempo durante o qual algo acontecerá e as condições sob as quais ele pode terminar.  |
| `Warranties` | Garantia por um fornecedor de como um produto funcionará. |

### Garantia

Cada item (tipo ou categoria) identificado pela Classificação de Elementos recebe uma classificação
`assurance`. Os valores de garantia possíveis são descritos abaixo:

| **Garantia** | **Descrição** |
| --- | --- |
| `High` | Há evidências consideráveis de que a classificação fornecida representa o conteúdo. |
| `Low` | Há alguma evidência para suportar a classificação, mas pode precisar de revisão adicional para confirmar. |
