---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-17"

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

# Planos de precificação do Discovery

O serviço {{site.data.keyword.discoveryfull}} oferece três planos -- **Lite**, **Avançado** e **Premium** -- que fornecem diferentes níveis de recursos e capacidades para adequar às suas necessidades.
{: shortdesc}

Os **Casos de uso de dados privados** têm os recursos, limites e preços a seguir:

## Lite
{: #lite}

Tamanho | Limite de Armazenamento do Documento | Número de Docs\* | Preço 
------ | ------ | ------ | ------  
N/A | 50 MB | 1.000 por mês | Livre 

O plano Lite é um plano iniciador e não deve ser usado para produção. Quando você faz upgrade para um plano pago, é possível manter todos os documentos alimentados. As instâncias do plano Lite são excluídas após 30 dias de inatividade. 

Atributos:
- 1 ambiente
- Até duas coleções
- Enriquecimentos de NLU Livres\*\*
- 20 documentos em andamento\*\*\*\* 

Opções adicionais:<br> [ Modelos customizados ](/docs/services/discovery/integrate-wks.html#integrating-your-custom-model):<br>
Um modelo do Watson Knowledge Studio incluído. Modelos adicionais: não disponível<br>[Classificação de elementos](/docs/services/discovery/element-classification.html)\*\*\*:
500 páginas incluídas por mês. Páginas adicionais: não disponível <br>[Consultas de notícias](/docs/services/discovery/watson-discovery-news.html):
200 consultas de Notícias incluídas por mês. Consultas adicionais: não disponível<br>[Expansões de consulta](/docs/services/discovery/using.html#query-expansion):
500 expansões de consulta com um total de 1.000 termos. Expansões adicionais: Não disponível

Para obter informações sobre como fazer upgrade de Lite para Avançado, veja [Fazendo upgrade de seu serviço ](/docs/services/discovery/upgrading.html#service)

## Avançado
{: #advanced}

Tamanho | Limite de Armazenamento do Documento | Número de Docs\* | Preço 
------ | ------ | ------ | ------ 
Extra-Pequeno\*\*\*\*\* | 40 GB | Até 50.000 docs por mês | A partir de $500 por mês  
Pequeno | 160 GB | Até 1M docs por mês | A partir de $1.500 por mês  
Médio-Pequeno | 320 GB | Até 2M docs por mês | Começando com $3.000 por mês 
Médio| 640 GB | Até 4M docs por mês | Iniciando com $5.000 por mês 
Médio-Grande | 1.2 TB | Até 8M docs por mês | Começando com $10.000 por mês 
Grande| 2,4 TB | Até 16M docs por mês | A partir de $15.000 por mês 
Extra-Grande| 4 TB | Até 32M docs por mês | A partir de $20.000 por mês 
XX-Grande | 5,5 TB | Até 64M docs por mês | A partir de $35,000 por mês 
XXX-Grande | 12 TB | Até 100M docs por mês | Iniciando com $45.000 por mês 

O X-Small é o menor ambiente disponível e é recomendado somente para desenvolvimento e teste.\*\*\*\*\*

Mover de um nível de Avançado para outro não requer a criação de novas instâncias. Novas instâncias serão necessárias se alternar de um plano Avançado para Premium. Para obter informações sobre como fazer upgrade de uma camada de Avançado para outra, veja [Movendo de uma camada de Avançado para outra](/docs/services/discovery/upgrading.html#advanced).

\*\*\*\*\*Atributos de X-Small Planos: 
- 1 ambiente
- Até 4 coleções
- Enriquecimentos de NLU Livres\*\*
- 50 documentos em andamento\*\*\*\*

Atributos de todos os outros planos avançados:
- 1 ambiente
- Até 100 coleções
- Enriquecimentos de NLU Livres\*\*
- 105 documentos em andamento\*\*\*\*

Opções adicionais:<br> [Modelos customizados](/docs/services/discovery/integrate-wks.html#integrating-your-custom-model):<br>
Um modelo do Watson Knowledge Studio incluído. Modelos adicionais: $800 cada<br>[Classificação de elementos](/docs/services/discovery/element-classification.html)\*\*\*:
500 páginas incluídas por mês. Páginas adicionais: $0.40 cada<br>[Consultas de notícias](/docs/services/discovery/watson-discovery-news.html):
200 consultas de Notícias incluídas por mês  
10.000 consultas adicionais (por mês): $0,10 por consulta<br>
10.001 - 100.000 consultas adicionais (por mês): $0,05 por consulta<br>
Mais de 100.000 consultas (por mês): $0,03 por consulta<br>
[Expansões de consulta](/docs/services/discovery/using.html#query-expansion):
5.000 expansões de consulta com um total de 25.000 termos

## Premium
   
Os planos Premium oferecem aos desenvolvedores e organizações uma única instância de locatário de um ou mais serviços do Watson para melhor isolamento e segurança. Esses planos oferecem isolamento a nível de cálculo na plataforma compartilhada existente, bem como dados criptografados de ponta a ponta enquanto em trânsito e em repouso. 

Para obter mais informações ou para comprar um plano Premium, entre em contato com [Vendas](https://ibm.biz/contact-wdc-premium). 
<br>
<br> 

**Nota:** a data de versão da API foi atualizada para `2018-08-01`. Para tirar vantagem das novas opções de dimensionamento de ambiente (`LT`, `XS`, `S`, `MS`, `M`, `ML`, `L`, `XL`, `XXL`, `XXXL`), deve-se usar esta data de versão ao criar ambientes com a API. Os tamanhos de ambiente agora têm o tipo de `string` (anteriormente, o tipo era `integer`.)

\* O limite do documento supõe um tamanho médio do documento de 100 KB no disco. O tamanho do documento é calculado depois que ele passou por conversão e enriquecimento, portanto, o tamanho do documento pode mudar significativamente da entrada original. É possível visualizar o número de documentos armazenados e a quantia total de uso de armazenamento usando a API [Ambientes](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#environments-api) ou [Coleções](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#collections-api) ou usando o conjunto de ferramentas. Se seus documentos forem em média maiores que 100 KB no disco, você atingirá o limite de armazenamento de um plano antes do limite máximo de documentos. Se você executar [segmentação de documento](https://console.bluemix.net/docs/services/discovery/building.html#doc-segmentation) em seus documentos, cada segmento será contado como um documento separado.

\*\* Os [enriquecimentos do Natural Language Understanding (NLU)](https://console.bluemix.net/docs/services/discovery/building.html#adding-enrichments) são: Extração de entidade, Análise de sentimentos, Classificação de categoria, Identificação de conceito, Extração de palavra-chave, Extração de relação, Análise de emoção, Classificação de elementos e Extração de função semântica. Somente os primeiros 50.000 caracteres de cada documento são enriquecidos. 

\*\*\* A Classificação de elementos é um enriquecimento que analisa por meio do controle de documentos para converter, identificar e classificar elementos de importância. Ela usa o Processamento de Linguagem Natural para extrair os elementos a seguir de documentos PDF: parte (a quem se refere), natureza (tipo de elemento) e categoria (classe específica).

\*\*\*\* Se você atingir seu limite em andamento, será necessário desacelerar a taxa de sua ingestão. Ao usar o serviço Discovery, um documento está "em andamento" ao ser transferido por upload, enriquecido e processado antes de ser incluído em uma coleção.

Para obter informações sobre o cálculo de custos, veja o [IBM Cloud Pricing Calculator ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.bluemix.net/pricing/platform/watson){: new_window}.

Para obter informações sobre a segurança do IBM Cloud, veja [Segurança e privacidade de dados dos serviços de nuvem ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/software/sla/sladb.nsf/sla/csdsp?OpenDocument){: new_window}.

Para obter informações adicionais de precificação, veja o [Catálogo do {{site.data.keyword.discoveryshort}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.bluemix.net/catalog/services/discovery){: new_window}.

## Notas para Clientes com Planos Existentes

- Iniciando em **1º de agosto de 2018**, seu faturamento e uso serão baseados neste plano de precificação.
- O plano Lite foi reduzido de 2.000 documentos/400 consultas do {{site.data.keyword.discoverynewsshort}} por mês para 1.000 documentos/200 consultas do {{site.data.keyword.discoverynewsshort}} por mês. Se você já excedeu os novos limites do plano Lite, não será possível incluir mais nenhum documento. No entanto, é possível continuar usando-o ou fazer upgrade dele para um plano Avançado ou Premium.
- O plano Padrão tornou-se obsoleto e não estará mais disponível para novos usuários. Se você está atualmente em um plano Padrão existente, é possível continuar usando-o ou fazer upgrade dele para um plano Avançado ou Premium.
- Os planos Avançado e Premium são agora baseados em camadas de documentos, eles não são mais baseados nas horas de documento. Sua fatura mensal não flutuará com base no número de documentos, a menos que você alterne entre as camadas.
- Os clientes Premium devem entrar em contato com [Vendas](https://ibm.biz/contact-wdc-premium) para obter detalhes sobre mudanças de faturamento.	
