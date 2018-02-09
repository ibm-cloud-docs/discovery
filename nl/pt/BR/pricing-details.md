---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-09"

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

O serviço do {{site.data.keyword.discoveryfull}} oferece três planos que fornecem diferentes níveis de recursos e de capacidades para atender às suas necessidades.
{: shortdesc}

Os **casos de usos de dados privados** têm os limites e preços a seguir:

| Lite                     |  Padrão         | Avançado          | Premium          |
|--------------------------|-------------------|-------------------|-------------------|
| Até 2.000 documentos simultâneos por mês\*   |Até 100.000 documentos simultâneos por mês\*<br/> US$10 por 1.000 documentos simultâneos por mês (US$ 0,0139USD/1.000 doc./h)\*\*\*<br/> 2 mil documentos por mês gratuitos\*\*\*\*  | **Ambiente reservado**</br>US$1,000/taxa base mensal<br/> Até 1.000.000 documentos por mês\*<br/> US$5 por 1.000 documentos simultâneos por mês (US$ 0,00694/1.000 doc./h)\*\*\*<br/> 100 mil documentos por mês incluídos\*\*\*\*</br> Para ambientes maiores, entre em contato com [Vendas ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/marketing/iwm/dre/signup?source=MAIL-watson){: new_window}.| Os **Planos Premium** oferecem aos desenvolvedores e organizações uma única instância de locatário de um ou mais serviços Watson para um melhor isolamento e segurança. Esses planos oferecem isolamento a nível de cálculo na plataforma compartilhada existente, bem como dados criptografados de ponta a ponta enquanto em trânsito e em repouso. Para obter mais informações ou para comprar um plano Premium, entre em contato com a área de [Vendas ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://ibm.biz/contact-wdc-premium){: new_window} |
| 200 MB\*\*                  |10 GB\*\*  | 80 GB\*\* |-|
| Até duas coleções      |Até quatro coleções | Até 100 coleções|-|
| Até um modelo customizado do {{site.data.keyword.knowledgestudiofull}}     |Até um modelo customizado do {{site.data.keyword.knowledgestudioshort}} | Modelos customizados ilimitados do {{site.data.keyword.knowledgestudioshort}}<br/>1 {{site.data.keyword.knowledgestudioshort}} Custom Model incluído <br/>$ 800 adicionais por modelo do {{site.data.keyword.knowledgestudioshort}} por mês|-|

**Observação:** em todos os planos, as primeiras 1.000 consultas do {{site.data.keyword.discoverynewsshort}} por mês são grátis. As consultas do {{site.data.keyword.discoverynewsshort}} são cobradas em $ 0,10 por consulta após os primeiros 1.000.

**Observação:** os serviços de plano Lite são excluídos após 30 dias de inatividade. Um ambiente grátis é atribuído por organização nos planos Lite.

 \* O limite do documento supõe um tamanho médio de documento de 100 KB no disco. Este é o tamanho de um documento em uma coleção depois que ele passou por conversão e enriquecimento, de modo que o tamanho pode mudar significativamente da entrada original. É possível visualizar o número de documentos armazenados e a quantia total de armazenamento usada pela API `environments` ou `collections` ou usando o conjunto de ferramentas.

 \*\* Se seus documentos forem em média maiores que 100 KB no disco, você atingirá o limite de armazenamento de um plano antes do limite máximo de documento.

 \*\*\* O preço é baseado no número de horas em que um lote de 1.000 documentos é armazenado no serviço (referido como um Mil documentos/hora). Para o calculador de precificação, esse é o número que deve ser inserido (`número de documentos * número de horas em que esses documentos são armazenados em um mês/1000`).

 \*\*\*\* Quantias livres são baseadas no equivalente de documentos armazenados por um mês. Por exemplo, no plano Padrão, a quantia livre é equivalente a 2.000 documentos * 720 horas / 1.000 documentos em lote = 1.440 Mil documentos/hora.

**Exemplo:** um usuário no plano Padrão armazena 4.000 documentos no mês inteiro. Ele seria cobrado como segue:

- `4.000 documentos * 720 horas (em um mês) / 1.000 = 2.880` Mil documentos/hora

- `2.880 - 1.440 (horas de documento livre) = 1.440` Mil documentos/hora faturáveis

- `1.440 * $0,0139` (preço por Mil documentos/hora) = `$20.00` para o mês

**Nota:** ao calcular a quantia faturada cada hora, o número total de documentos armazenados é arredondado para o próximo 1.000 como parte do cálculo. Por exemplo, se você tiver 4.678 documentos armazenados por 1 hora, será arredondado para 5.000 e resultará em 5 mil documentos/hora sendo faturados para a conta.

**Nota:** não há encargos adicionais para enriquecimentos.

Para obter informações sobre a segurança do {{site.data.keyword.Bluemix_notm}}, consulte [Descrição do serviço do {{site.data.keyword.Bluemix_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=IBM+Bluemix+Service+Description){: new_window}.

## Convertendo de planos de precificação anteriores

Clientes que assinaram um plano antes de **1º de agosto de 2017** foram migrados para um dos novos planos.

- Os clientes que anteriormente estavam no plano de avaliação grátis de 30 dias foram migrados para o plano **Lite**.
  Como resultado dessa transição, os usuários existentes podem ter cumprido ou excedido o limite do plano Lite em documentos _(2000)_, armazenamento _(200Mb)_ ou número de coleções _(2)_. Se você exceder o limite do plano **Lite**, não poderá incluir nenhum conteúdo adicional no serviço, mas ainda poderá consultar coleções. É possível visualizar o status atual de todos esses limites usando o conjunto de ferramentas do {{site.data.keyword.discoveryshort}} ou a API. Para ser capaz de continuar incluindo conteúdo na instância do {{site.data.keyword.discoveryshort}}, deve-se fazer um dos seguintes:
  - remova coleções e/ou documentos para que os limites do plano **Lite** não seja excedido.
    Os documentos podem ser excluídos individualmente por meio da API usando o método [delete-doc ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-doc){: new_window} ou coleções inteiras podem ser excluídas usando o conjunto de ferramentas ou a API usando o método [delete-collection ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-collection){: new_window} 
  - Faça upgrade de seu plano para um nível que atenda às suas necessidades de armazenamento.
- Os clientes com ambientes de tamanho **`1`** **`2`** ou **`3`** foram migrados automaticamente para o plano **Avançado**.
  Se você foi movido para a camada Avançado e tiver menos de 100.000 documentos e 4 coleções, será possível mudar para a camada Padrão para reduzir custos. Isso requer a criação de uma nova instância do Discovery no plano Padrão e realimentação de dados na nova instância. A ingestão pode ser feita por meio do conjunto de ferramentas, das APIs ou do Data Crawler.

Consulte o [Catálogo do {{site.data.keyword.discoveryshort}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window} para obter informações de precificação adicionais.
