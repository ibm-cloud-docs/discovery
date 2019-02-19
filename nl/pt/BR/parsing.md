---

copyright:
  years: 2017, 2018
lastupdated: "2018-10-23"

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

# Contratos de análise
{: #contract_parsing}

A Classificação de elementos retorna os contratos analisados com uma análise de cada elemento identificado.

As seções a seguir descrevem como o JSON retornado fornece a análise.

## Tipos
{: #contract_types}

A matriz `types` inclui uma série de objetos, cada um dos quais contendo chaves
`nature` e `party` cujos valores identificam um couplet para o elemento.

As
tabelas a seguir listam os valores possíveis das chaves `nature` e `party`.

| `nature`         |Descrição                                                |
|:----------------:|-----------------------------------------------------------|
|`Definition`      |Este elemento inclui clareza para um termo, relacionamento ou semelhante. Nenhuma ação é necessária para cumprir o elemento, nem qualquer parte afetada.|
|`Disclaimer`      |A `party` no elemento não é obrigada a cumprir os
termos especificados pelo elemento, mas não é proibida de fazê-lo.|
|`Exclusion`       |A `party` no elemento não cumprirá os termos
especificados pelo elemento.|
|`Obligation`      |A `party` no elemento é obrigada a cumprir os
termos especificados pelo elemento.|
|`Right`           |A `party` no elemento tem a garantia de que receberá os
termos especificados pelo elemento.|

Cada chave `nature` é emparelhada com uma chave `party`, que conterá o nome ou a função da parte ou partes que se aplicam à natureza (os exemplos incluem, mas não se limitam a, `Buyer`, `IBM` ou `All Parties`). Observe que para a natureza `Definition`, a parte é sempre `None`.

## Partes
{: #contract_parties}

A matriz `parties` separada especifica os participantes listados no contrato. Cada objeto `party` identificado lista a parte identificada por nome e é correspondido com uma `role` que classifica a função do objeto `party`. Os valores de `role` que podem ser retornados para contratos incluem, mas não estão limitados a:

| `role`           |Descrição                                                |
|:----------------:|-----------------------------------------------------------|
|`Buyer`           |A parte responsável pelo pagamento dos bens ou serviços listados no
contrato.|
|`End User`        |A parte que interagirá com os bens ou serviços fornecidos, distinguidos
explicitamente do `Buyer`.|
|`None`            |Nenhuma parte foi identificada para o elemento.|
|`Supplier`        |A parte responsável pelo fornecimento dos bens ou serviços listados no
contrato.|

## Categorias
{: #contract_categories}

A matriz `categories` define o assunto da sentença. As categorias atualmente suportadas incluem:

| `categories`     |Descrição                                                |
|:----------------:|-----------------------------------------------------------|
|`Amendments`      |Elementos que especificam mudanças no contrato após ele ter sido assinado
ou alterações em um contrato padrão. Inclui discussões sobre as condições para mudar os termos de um contrato.|
|`Asset Use`       |Elementos que se referem a como uma parte pode ou não usar os ativos de outra parte. Isso se aplica especificamente a uma parte que tenha acesso ou esteja usando ativos, como licenças, equipamento, ferramentas ou equipe, da outra parte enquanto está no processo de condução de suas obrigações sob o contrato, incluindo permissões e restrições sobre isso. Isso não se estende a especificações das obrigações ou direitos de uma parte em relação a quaisquer mercadorias compradas, serviços, licenças, etc., uma vez que estes são os próprios ativos da parte, em vez de ativos de outra parte.|
|`Assignments`     |Elementos que descrevem a transferência de direitos, obrigações ou
ambos para um terceiro.|
|`Audits`          |Elementos que se referem ao direito de uma parte para examinar ou revisar a conformidade ou os requisitos para que uma parte fique disponível para inspeção ou análise de conformidade. Isso inclui referências à manutenção de registros (principalmente quando se relaciona ao direito da inspeção) e à manutenção e retenção de registros de atividade que podem ser examinados.|
|` Business Continuity `|Elementos que se referem às consequências se o negócio inteiro de uma das partes for vendido.|
|`Communication`  |Elementos que se referem aos requisitos para comunicar, responder, notificar ou fornecer aviso, informações de contato ou informações relativas a mudanças no contrato. Também inclui referências a detalhes sobre métodos de comunicação, o ato ou o processo de troca de informações e os meios aceitáveis de troca de informações entre as partes (bem como outras que não são necessariamente partes diretas para o contrato).|
|`Confidentiality` |Elementos que descrevem como as partes podem ou não podem usar as informações aprendidas no curso da conclusão do contrato e em encaminhamento. Também inclui a discussão de informações que devem ser mantidas confidenciais, como a manutenção de segredos comerciais ou a não divulgação de informações de negócios.|
|`Deliverables`    |Elementos que especificam os itens, como mercadorias e serviços, que uma parte fornece à outra sob os termos do contrato, normalmente em troca de pagamento. Inclui a discussão da preparação de distribuíveis.|
|`Delivery`        |Elementos que especificam os meios ou modos de transferência de distribuíveis (coisas, em oposição a serviços pessoais) de uma parte para outra. Inclui discussões de características da entrega, como planejamento ou local.|
|`Dispute Resolution`|Elementos que discutem provisões para resolução de qualquer disputa (por exemplo, em relação à mão de obra, faturas ou faturamento) originada entre as partes contratantes. Os exemplos de provisão podem incluir a quitação por um procedimento definido, como um painel de arbitragem, um processo para obter uma liminar, renunciar a um direito a julgamento ou proibir a busca de uma ação de classe. Também incluem referências ao direito aplicável do contrato ou à escolha de lei, como um país ou jurisdição particular. |
|`Force Majeure`   |Elementos que se referem a eventos inesperados ou disruptivos fora do controle de uma parte que aliviariam a parte de executar sua obrigação contratual.|
|`Indemnification` |Elementos que especificam a correção de determinados passivos, quando uma parte do contrato se torna responsável por compensar outra parte como resultado da perda ou dano incorrido durante o termo ou proveniente das circunstâncias do contrato. Também inclui referências a quaisquer isenções legais de perda ou danos.|
|`Insurance`       |Elementos que se referem à cobertura de seguro ou aos termos de cobertura fornecidos por uma parte para outra parte (incluindo para terceiros, como subcontratados ou outros). Inclui uma variedade de seguros, incluindo, mas não se limitando a, seguro de saúde.|
|` Propriedade Intelectual `|Elementos que discutem a designação de direitos (tais como copyrights, patentes e segredos comerciais) para partes no contrato. Inclui referências a patentes, direitos de aplicação de patentes, marcas comerciais, nomes comerciais, marcas de serviço, nomes de domínio, copyrights e todos os aplicativos e registro de tais esquemas, modelos industriais, invenções, autoria, conhecimento comercial, programas de software de computador e outras informações protegidas por direitos autorais intangíveis. Também inclui a discussão sobre as consequências da violação dos direitos de propriedade intelectual.|
|`Liability`       |Elementos que descrevem o método para determinar quando e como a falha se
conecta a qualquer parte. Os exemplos podem incluir, mas não se limitam a, instruções relativas a limitações de responsabilidade, reclamações de terceiros e reparos, substituições ou reembolsos conforme requeridos da parte no caso de falha.|
|` Payment Terms & Billing `|Elementos que detalham como e quando uma parte deve pagar ou receber, bem como os itens ou taxas que as partes pagarão ou serão faturadas. Inclui referências a modos de pagamento ou mecanismos de pagamento.|
|`Pricing & Taxes` |Elementos que se referem a quantias ou valores específicos associados a distribuíveis individuais que são trocados (por exemplo, quanto algo custa) como parte do cumprimento dos termos do contrato. Inclui referências a figuras ou métodos específicos para calcular preços ou quantias de impostos.|
|`Privacy`         |Elementos que estão particularmente preocupados com o tratamento de informações pessoais sensíveis, geralmente em relação à sua proteção (por exemplo, para satisfazer regulamentações como GDPR).|
|` Responsabilidades `|Elementos que discutem as tarefas auxiliares ao contrato que estão no controle de somente uma parte, especificamente focadas na discussão de supervisão de funcionário.|
|` Segurança e Segurança `|Elementos que se referem à segurança física ou à proteção de segurança cibernética para pessoas, dados ou sistemas. Os exemplos incluem discussões de verificações de histórico, precauções de segurança, segurança do local de trabalho, protocolos de acesso seguro e defeitos do produto que podem representar um perigo.|
|`Scope of Work`   |Elementos que definem o que está no contrato versus o que não está no contrato; consequentemente, o que é prometido ser feito. Os exemplos incluem instruções que definem uma ordem específica ou que descrevem as metas ou os objetivos descritos no contrato.|
|`Subcontracts`    |Elementos que se referem à contratação de terceiros para executar
determinas obrigações sob o contrato e as permissões, os direitos, as restrições e as consequências inerentes
e decorrentes.|
|` Termo e Terminação `|Elementos que se referem à duração do contrato, ao planejamento e aos
termos da rescisão do contrato e às consequências da rescisão, incluindo quaisquer obrigações que se
apliquem à rescisão ou após ela.|
|`Warranties`      |Elementos que se referem a promessas e obrigações contínuas feitas no contrato que atualmente são verdade e continuarão a ser verdade no futuro. Além disso, os elementos que discutem as consequências de tais promessas ou obrigações que estão sendo quebradas e os direitos para remediar a situação (por exemplo, mas não limitado a, buscar danos). Esta categoria não se aplica a elementos que estejam simplesmente preocupados com declarações de representação (declarações de fato sobre o passado ou o presente) ou a elementos que definem suposições sobre coisas que ocorreram no passado.|

## Atributos
{: #attributes}

A matriz `attributes` especifica quaisquer atributos identificados na sentença. Cada objeto na matriz inclui três chaves: `type` (o tipo de atributo da tabela a seguir), `text` (o texto aplicável) e `local` (os índices `begin` e `end` do atributo no documento de entrada). Os atributos atualmente suportados incluem:

| `attributes`     |Descrição                                                |
|:----------------:|-----------------------------------------------------------|
|`Location`        |Uma localização geográfica ou região.                         |
|`DateTime`        |Uma data, hora, intervalo de data ou intervalo de tempo.                   |
|`Currency`        |Valor monetário e unidades.                                  |

## Provenance
{: #provenance}

Cada objeto nas matrizes `types` e `categories` inclui uma matriz `provenance_ids`. A matriz `provenance_ids` tem uma ou mais chaves. Cada chave é um valor em hash que é possível enviar à IBM para fornecer feedback ou receber suporte.

