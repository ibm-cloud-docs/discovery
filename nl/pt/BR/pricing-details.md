---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-02-28"

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

# Planos de precificação do Discovery
{: #discovery-pricing-plans}

O serviço {{site.data.keyword.discoveryfull}} oferece três planos -- **Lite**, **Avançado** e **Premium** -- que fornecem diferentes níveis de recursos e capacidades para adequar às suas necessidades.
{: shortdesc}

Os **Casos de uso de dados privados** têm os recursos, limites e preços a seguir:

## Lite
{: #lite}

Tamanho | Limite de Armazenamento do Documento | Número de Docs\* | Preço 
------ | ------ | ------ | ------  
N/A | 50 MB | 1.000 por mês | Livre 

O plano Lite é um plano iniciador e não deve ser usado para produção. Quando você faz upgrade para um plano pago, é possível manter todos os documentos alimentados.  As instâncias do plano Lite são excluídas após 30 dias de inatividade. 

Atributos:
- 1 ambiente
- Até duas coleções
- Enriquecimentos de NLU Livres\*\*

Opções adicionais:<br> [ Modelos customizados ](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-your-custom-model):<br>
Um modelo do Watson Knowledge Studio incluído. Modelos adicionais: não disponível<br>[Classificação de elementos](/docs/services/discovery?topic=discovery-element-classification#element-classification)\*\*\*:
500 páginas incluídas por mês. Páginas adicionais: não disponível <br>[Consultas de notícias](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news):
200 consultas de Notícias incluídas por mês. Consultas adicionais: não disponível<br>[Expansões de consulta](/docs/services/discovery?topic=discovery-query-concepts#query-expansion):
500 expansões de consulta com um total de 1.000 termos. Expansões adicionais: Não disponível

Para obter informações sobre como fazer upgrade de Lite para Avançado, veja [Fazendo upgrade de seu serviço ](/docs/services/discovery?topic=discovery-upgrading-your-plan#service)

Para obter informações de desempenho da consulta, consulte [Desempenho da consulta](/docs/services/discovery?topic=discovery-qp#qp). Consultas são limitadas com base no plano. Taxas médias estimadas de consulta pelos planos **Lite** e **Standard**: 1 QPS para consultas classificadas novamente com dois campos de texto de nível superior.

## Avançado
{: #advanced}

Ao escolher um tamanho de plano Advanced, observe que os recursos são necessários para o armazenamento e a consulta de documento. Portanto, será possível requerer um ambiente maior se você estiver próximo do limite máximo de documento para um tamanho de plano e também tiver os requisitos a seguir: 

-  Requisitos de desempenho de consulta mais altos (por exemplo, usando treinamento de relevância)
-  Você prevê um grande número de usuários simultâneos
-  Necessidades de consulta complexas 

Para obter detalhes adicionais sobre fatores que influenciam o desempenho da consulta, consulte [Desempenho da consulta](/docs/services/discovery?topic=discovery-qp#qp). Consultas são limitadas com base no plano. Taxas médias estimadas de consulta pelos planos **Advanced** (S, MS): 10 QPS para consultas classificadas novamente com dois campos de texto de nível superior.

Tamanho | Limite de Armazenamento do Documento | Número de Docs\* | Preço 
------ | ------ | ------ | ------ 
Extra-Pequeno \ * \ * \ * \ * | 40 GB | Até 50.000 docs por mês | A partir de $500 por mês  
Pequeno | 160 GB | Até 1M docs por mês | A partir de $1.500 por mês  
Médio-Pequeno | 320 GB | Até 2M docs por mês | Começando com $3.000 por mês 
Médio| 640 GB | Até 4M docs por mês | Iniciando com $5.000 por mês 
Médio-Grande | 1.2 TB | Até 8M docs por mês | Começando com $10.000 por mês 
Grande| 2,4 TB | Até 16M docs por mês | A partir de $15.000 por mês 
Extra-Grande| 4 TB | Até 32M docs por mês | A partir de $20.000 por mês 
XX-Grande | 5,5 TB | Até 64M docs por mês | A partir de $35,000 por mês 
XXX-Grande | 12 TB | Até 100M docs por mês | Iniciando com $45.000 por mês 

O X-Small é o menor ambiente disponível e é recomendado apenas para desenvolvimento e teste. \ * \ * \ * \ *

Mover de um nível de Avançado para outro não requer a criação de novas instâncias. Novas instâncias serão necessárias se alternar de um plano Avançado para Premium. Para obter informações sobre como fazer upgrade de uma camada de Avançado para outra, veja [Movendo de uma camada de Avançado para outra](/docs/services/discovery?topic=discovery-upgrading-your-plan#upgrading-your-plan).

\ * \ * \ * \ *Atributos de X-Small: 
- 1 ambiente
- Até 4 coleções
- Enriquecimentos de NLU Livres\*\*

Atributos de todos os outros planos avançados:
- 1 ambiente
- Até 100 coleções
- Enriquecimentos de NLU Livres\*\*

Opções adicionais:<br> [Modelos customizados](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-your-custom-model):<br>
Um modelo do Watson Knowledge Studio incluído. Modelos adicionais: $800 cada<br>[Classificação de elementos](/docs/services/discovery?topic=discovery-element-classification#element-classification)\*\*\*:
500 páginas incluídas por mês. Páginas adicionais: $0.40 cada<br>[Consultas de notícias](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news):
200 consultas de Notícias incluídas por mês  
10.000 consultas adicionais (por mês): $0,10 por consulta<br>
10.001 - 100.000 consultas adicionais (por mês): $0,05 por consulta<br>
Mais de 100.000 consultas (por mês): $0,03 por consulta<br>
[Expansões de consulta](/docs/services/discovery?topic=discovery-query-concepts#query-expansion):
5.000 expansões de consulta com um total de 25.000 termos

`-----`
<br>
\* O limite do documento supõe um tamanho médio do documento de 100 KB no disco. O tamanho do documento é calculado depois que ele passou por conversão e enriquecimento, portanto, o tamanho do documento pode mudar significativamente da entrada original. É possível visualizar o número de documentos armazenados e a quantia total de uso de armazenamento usando a API [Ambientes](https://{DomainName}/apidocs/discovery#get-environment-info) ou [Coleções](https://{DomainName}/apidocs/discovery#get-collection-details) ou usando o conjunto de ferramentas. Se seus documentos forem em média maiores que 100 KB no disco, você atingirá o limite de armazenamento de um plano antes do limite máximo de documentos. Se você executar [segmentação de documento](/docs/services/discovery?topic=discovery-configservice#doc-segmentation) em seus documentos, cada segmento será contado como um documento separado.

\*\* Os [enriquecimentos do Natural Language Understanding (NLU)](/docs/services/discovery?topic=discovery-configservice#adding-enrichments) são: Extração de entidade, Análise de sentimentos, Classificação de categoria, Identificação de conceito, Extração de palavra-chave, Extração de relação, Análise de emoção, Classificação de elementos e Extração de função semântica.  Somente os primeiros 50.000 caracteres de cada documento são enriquecidos. 

\*\*\* A Classificação de elementos é um enriquecimento que analisa por meio do controle de documentos para converter, identificar e classificar elementos de importância. Ela usa o Processamento de Linguagem Natural para extrair os elementos a seguir de documentos PDF: parte (a quem se refere), natureza (tipo de elemento) e categoria (classe específica).

Para aproveitar as novas opções de dimensionamento de ambiente (`LT`, `XS`, `S`, `MS`, `M`, `ML`, `L`, `XL`, `XXL`, `XXXL`), deve-se usar a data de versão da API de `2018-08-01` ou mais recente ao criar ambientes com a API. Os tamanhos de ambiente agora têm o tipo de `string` (anteriormente, o tipo era `integer`.)
{: note}

## Premium
{: #premiumplan}
   
Os planos Premium oferecem aos desenvolvedores e organizações uma única instância de locatário de um ou mais serviços do Watson para melhor isolamento e segurança. Esses planos oferecem isolamento a nível de cálculo na plataforma compartilhada existente, bem como dados criptografados de ponta a ponta enquanto em trânsito e em repouso. 

Para obter mais informações ou para comprar um plano Premium, entre em contato com [Vendas](https://ibm.biz/contact-wdc-premium). 

## Informações adicionais
{: #pricingadd}

Para obter informações sobre o cálculo de custos, veja o [IBM Cloud Pricing Calculator ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/pricing/platform/watson){: new_window}.

Para obter informações sobre a segurança do IBM Cloud, veja [Segurança e privacidade de dados dos serviços de nuvem ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/software/sla/sladb.nsf/sla/csdsp?OpenDocument){: new_window}.

Para obter informações de precificação adicionais, consulte o [ catálogo do {{site.data.keyword.discoveryshort}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/catalog/services/discovery){: new_window}.

## Notas para Clientes com Planos Existentes
{: #pricingnotes}

- Iniciando em **1º de agosto de 2018**, seu faturamento e uso serão baseados neste plano de precificação.
- O plano Lite foi reduzido de 2.000 documentos/400 consultas do {{site.data.keyword.discoverynewsshort}} por mês para 1.000 documentos/200 consultas do {{site.data.keyword.discoverynewsshort}} por mês.  Se você já excedeu os novos limites do plano Lite, não será possível incluir mais nenhum documento. No entanto, é possível continuar usando-o ou fazer upgrade dele para um plano Avançado ou Premium.
- O plano Padrão tornou-se obsoleto e não estará mais disponível para novos usuários. Se você está atualmente em um plano Padrão existente, é possível continuar usando-o ou fazer upgrade dele para um plano Avançado ou Premium.
- Os planos Avançado e Premium são agora baseados em camadas de documentos, eles não são mais baseados nas horas de documento. Sua fatura mensal não flutuará com base no número de documentos, a menos que você alterne entre as camadas.
- Clientes Premium, entre em contato com [Vendas ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://ibm.biz/contact-wdc-premium){: new_window} para obter detalhes sobre mudanças de faturamento.	
