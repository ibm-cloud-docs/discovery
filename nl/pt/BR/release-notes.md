---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-02-08"

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

# Notas sobre a liberação
{: #release-notes}

As notas sobre a liberação fornecem informações sobre mudanças no serviço do {{site.data.keyword.discoveryfull}} desde a liberação anterior.
{: shortdesc}

## Versão da API de Serviço
{: #apiversioning}

As solicitações de API requerem um parâmetro version que use uma data no formato `version=YYYY-MM-DD`. Sempre que mudamos a API de uma maneira incompatível com versões anteriores, lançamos uma nova versão secundária da API.

Envie o parâmetro version com cada solicitação de API. O serviço usa a versão da API para a data que você especificar ou a versão mais recente antes dessa data. Não padronize com a data atual. Em vez disso, especifique uma data que corresponda a uma versão que seja compatível com seu aplicativo e não a mude até que o aplicativo esteja pronto para uma versão mais recente.

A versão atual é  ` 2019-01-01 `.

## Recursos beta
{: #beta-features}

A IBM libera serviços, recursos e suporte ao idioma que são classificados como beta ou experimentais. Essas capacidades podem ser instáveis, mudar frequentemente e podem ser descontinuadas com curto prazo. Elas são fornecidas para poder avaliar sua funcionalidade. Uma capacidade beta ou experimental não fornece o mesmo nível de desempenho ou de compatibilidade que as capacidades geralmente liberadas fornecem. Essas capacidades não são projetadas para uso em um ambiente de produção e qualquer uso desse tipo é de sua responsabilidade.


## Mudanças
{: #change-log}

Os novos recursos e mudanças a seguir para o serviço estão disponíveis.

## 10 de fevereiro de 2019
{: #10feb19}

- Incluída a opção para se conectar e sincronizar com o IBM Cloud Object Storage. Essa origem de dados não está disponível em ambientes Dedicados. Consulte [IBM Cloud Object Storage](/docs/services/discovery?topic=discovery-sources#connectcos) para obter mais informações.

## 4 de fevereiro de 2019
{: #4feb19}

Atualizado para disponibilidade geral:

-  O [Smart Document Understanding (SDU)](/docs/services/discovery?topic=discovery-sdu#sdu) foi movido do status beta para o status GA.
   -  A anotação de tabela permanece no status beta. Um comunicado explicando os recursos beta pode ser localizado [aqui](/docs/services/discovery?topic=discovery-release-notes#beta-features).
   -  O botão `Data settings` na parte superior direita foi renomeado para `Configure data`.
   -  Fazer upload de um documento não é mais necessário para acessar o botão `Configure data` (anteriormente `Data settings`).

O beta do SDU foi anunciado em [22 de janeiro de 2019](/docs/services/discovery?topic=discovery-release-notes#22jan19).   
    
## 28 de janeiro de 2019
{: #28jan19}

A assistência não será mais fornecida para o Data Crawler se você estiver usando-o com uma origem de dados suportada pelos conectores do {{site.data.keyword.discoveryshort}}. Os conectores do {{site.data.keyword.discoveryshort}} suportam executar crawl do Box, SharePoint, Salesforce e mais. Veja [Conectando a origens de dados](/docs/services/discovery?topic=discovery-sources#sources) para obter detalhes. O Data Crawler deve ser usado apenas para executar crawl de compartilhamentos de arquivo ou bancos de dados. Em todos os outros casos, use o conector do {{site.data.keyword.discoveryshort}}. Outra opção para fazer upload de grandes números de arquivos no {{site.data.keyword.discoveryshort}} é [discovery-files ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/IBM/discovery-files){: new_window} no GitHub.

## 22 de janeiro de 2019
{: #22jan19}

- Liberada a versão beta do [Smart Document Understanding (SDU)](/docs/services/discovery?topic=discovery-sdu#sdu), uma nova maneira de treinar o {{site.data.keyword.discoveryfull}} para extrair campos customizados em seus documentos. Com o Smart Document Understanding, você anota campos em seus documentos para treinar modelos de conversão customizados. Um comunicado explicando os recursos beta pode ser localizado [aqui](/docs/services/discovery?topic=discovery-release-notes#beta-features).

O editor do SDU beta está disponível somente para novas coleções que contêm tipos de documento suportados e não têm o enriquecimento Classificação de elementos aplicado. As coleções privadas existentes usarão o método de configuração original.

Se você fizer parte do beta fechado para o Smart Document Understanding, não importe modelos criados nesse beta para essa versão. Atualmente, o Smart Document Understanding não está disponível em ambientes dedicados.

As funções do editor do SDU estão disponíveis apenas no conjunto de ferramentas do {{site.data.keyword.discoveryshort}}; elas não estão disponíveis na API.

## 15 de janeiro de 2019
{: #15jan19}

Atualizações de Classificação de Elemento:
-  O enriquecimento Classificação de elementos atualizou as partes, as categorias e os atributos na versão da API `2018-10-15` ou mais recente. Consulte  [ Contratos de análise ](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing)  para as atualizações.

- A saída do método `/v1/element_classification` agora inclui o seguinte:
    - A matriz `parties` agora inclui um campo `importance` que indica se a parte é uma parte `Primary` ou uma parte `Unknown` (não primária).
    - As matrizes `effective_dates`, `contract_amounts` e `termination_dates` agora incluem um campo `confidence_level` que indica um valor de `High`, `Medium` ou `Low`.
    Para obter mais informações, consulte [Classificando elementos](/docs/services/discovery?topic=discovery-output_schema#output_schema) e [Analisando contratos](/docs/services/discovery?topic=discovery-contract_parsing#contract_parsing).

    O conjunto de ferramentas do {{site.data.keyword.discoveryshort}} ainda não usa a versão da API atual: `2019-01-01` (ele usa atualmente a `2018-08-01`), portanto, você não verá esses novos campos na saída de Classificação de elementos no conjunto de ferramentas do {{site.data.keyword.discoveryshort}}.

## 10 de janeiro de 2019
{: #10jan19}

Problema conhecido:

-  Se você especificar um `customer-id` usando o método de normalização descrito em [Especificando um `customer_id`](/docs/services/discovery?topic=discovery-sources#source_customer_id) e, em seguida, tentar excluir documentos que contêm esse `customer_id` usando o método descrito aqui: [Excluindo dados rotulados](/docs/services/discovery?topic=discovery-information-security#deletingdata), o documento de origem associado não será excluído.

## 1 de janeiro de 2019
{: #1jan19}

- A sequência de versão para todas as chamadas API foi mudada para `2019-01-01` de `2018-12-03`. Essa versão introduz um novo status de ingestão de documento: `pending`. O status `pending` será retornado para documentos que foram aceitos, mas ainda não iniciaram o processamento. Previamente, esses documentos teriam o status de `processing`. O conjunto de ferramentas do {{site.data.keyword.discoveryshort}} ainda não usa essa versão da API (ele usa atualmente a `2018-08-01`), portanto, quando você verificar o status do documento no conjunto de ferramentas do {{site.data.keyword.discoveryshort}}, o status `pending` não será retornado.

## 21 de dezembro de 2018
{: #21dec18}

- Incluída a opção para se conectar e sincronizar com o Microsoft SharePoint 2016 On-Premise. Essa origem de dados não está disponível em ambientes Dedicados. Consulte [SharePoint 2016 On-Premise](/docs/services/discovery?topic=discovery-sources#connectsp_op) para obter mais informações.

- Incluída a versão beta do conector Web Crawl, que pode ser usado para se conectar, executar crawl e sincronizar com websites. Essa origem de dados não está disponível em ambientes Dedicados. Consulte  [ Crawl da web ](/docs/services/discovery?topic=discovery-sources#connectwebcrawl)  para obter mais informações. Um comunicado explicando os recursos beta pode ser localizado [aqui](/docs/services/discovery?topic=discovery-release-notes#beta-features).

- As origens de dados do Microsoft SharePoint Online, Salesforce e Box estão agora disponíveis em ambientes Premium. Eles não estão disponíveis em ambientes dedicados.

## 17 de dezembro de 2018
{: #17dec18}

- Incluído suporte integral para italiano. Para obter mais informações, consulte  [ Suporte ao idioma ](/docs/services/discovery?topic=discovery-language-support#language-support).

## 14 de dezembro de 2018
{: #14dec18}

Agora é possível criar as instâncias de serviço do {{site.data.keyword.discoveryshort}} que estão hospedadas no data center de Londres sem sindicância. Como todas as localizações, a localização Londres (eu-gb) do {{site.data.keyword.cloud}} usa a autenticação do Identity and Access Management (IAM) baseada em token. Todas as novas instâncias de serviço que você cria nessa localização usam a autenticação do IAM.

## 12 de dezembro de 2018
{: #12dec18}

- Incluída a capacidade de definir e fazer upload de uma lista de palavras vazias customizadas. As palavras vazias customizadas são implementadas com a API do {{site.data.keyword.discoveryshort}}. Consulte  [ Definindo as interrupções ](/docs/services/discovery?topic=discovery-query-concepts#stopwords)  para obter detalhes. 

## 3 de dezembro de 2018
{: #3dec18}

- Para todas as consultas (com exceção de consultas somente de filtro) gravadas usando a versão da API de `2018-12-03` ou mais recente, o {{site.data.keyword.discoveryshort}} retornará agora uma pontuação de `confidence` no conjunto de resultados da consulta, mesmo se a coleta não tiver sido treinada usando um método de treinamento supervisionado, como [Treinamento de relevância](//docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling) ou [Treinamento contínuo de relevância](/docs/services/discovery?topic=discovery-crt#crt). Além disso, o {{site.data.keyword.discoveryshort}} retornará um campo `document_retrieval_estrategy` que indica a origem da pontuação de `confidence` de `untrained`, `relevancy_training` ou `continuous_relevancy_training`. Para obter mais informações, consulte  [ Pontuações de confiança ](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence).

- A sequência de versão para todas as chamadas API foi mudada para `2018-12-03` de `2018-10-15`. O conjunto de ferramentas do {{site.data.keyword.discoveryshort}} ainda não usa essa versão da API (ele usa atualmente a `2018-08-01`), portanto, as consultas gravadas usando o conjunto de ferramentas do {{site.data.keyword.discoveryshort}} não retornarão uma pontuação de `confidence` para coleções não treinadas.

## 8 de novembro de 2018
{: #8nov18}

- {{site.data.keyword.discoveryshort}} ativado na localização `Tokyo` em 8 de novembro de 2018. Os ambientes dedicados e Premium não estão atualmente disponíveis em `Tokyo`.

## 30 de outubro de 2018
{: #30oct18}

- O serviço {{site.data.keyword.discoveryshort}} agora suporta autenticação do Identity and Access Management (IAM) baseada em token em todas as regiões. O IAM usa tokens de acesso em vez de credenciais de serviço para autenticação com um serviço. Para obter mais informações sobre como usar tokens do IAM com aplicativos novos e existentes, veja a atualização da liberação de [17 de maio de 2018](#17May18).

## 25 de outubro de 2018
{: #25oct18}

O esquema para o enriquecimento [Classificação de elemento](/docs/services/discovery?topic=discovery-element-classification#element-classification) foi mudado. Se você deseja usar o esquema atualizado, deve-se alimentar seus documentos com a API, usando a data da versão de `2018-10-15` ou mais recente. O conjunto de ferramentas do {{site.data.keyword.discoveryshort}} ainda não usa essa versão da API (ele usa atualmente a `2018-08-01`), portanto, os documentos alimentados usando o conjunto de ferramentas do {{site.data.keyword.discoveryshort}} serão enriquecidos com o esquema original.

## 24 de outubro de 2018
{: #24oct18}

- As consultas do {{site.data.keyword.discoverynewsfull}} exibem aproximadamente 50 palavras de cada artigo no campo de JSON `text`. Essas palavras serão agora extraídas dos destaques, em vez de simplesmente exibir as primeiras 50 palavras do artigo. Veja [highlight](/docs/services/discovery?topic=discovery-query-parameters#highlight) para obter uma explicação de highlights. Highlights não precisam ser incluídos explicitamente em sua consulta para ativar esse comportamento.

## 25 de setembro de 2018
{: #25sept18}

- Continuous Relevancy Training liberado, que usa interações de usuários para aprender como levantar os resultados mais relevantes. Ele pode aprender com o comportamento do usuário automaticamente, reduzindo significativamente o esforço necessário para melhorar a classificação por relevância dos resultados.  Consulte  [ Continuous Relevancy Training ](/docs/services/discovery?topic=discovery-crt#crt)  para obter detalhes.

- Incluído suporte de API para executar consultas mais longas. Isso aumenta o limite de caractere para 10.000 caracteres e torna possível aumentar o número de filtros em suas consultas e executar agregações mais complexas. Veja a Consulta de POST em [Referência da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#long-collection-queries){: new_window} e [Referência da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#long-environment-queries){: new_window} para obter detalhes.

- Agora é possível fazer upgrade de seu plano Avançado usando a API. Veja [Fazendo upgrade de seu plano](/docs/services/discovery?topic=discovery-upgrading-your-plan#switchadvanced) para obter detalhes. 

- O enriquecimento Classificação de elementos atualizou os elementos classificados, elementos do contrato e partes e tabelas identificadas. Consulte  [ Classificação de Elementos ](/docs/services/discovery?topic=discovery-element-classification#element-classification)  para obter as atualizações.

- Incluído suporte integral para português do Brasil. Para obter mais informações, consulte  [ Suporte ao idioma ](/docs/services/discovery?topic=discovery-language-support#language-support).

- A API de propensão (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`) agora suporta o parâmetro `bias`, que permite a propensão a determinados resultados, por exemplo, documentos que foram publicados mais recentemente. Consulte o método [Consultar a sua coleção ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#query-your-collection){: new_window} na referência de API para obter informações.

- Descobriu-se que o arquivo de **Configuração de contrato padrão** fornecido para enriquecer coleções para [Classificação de elementos](/docs/services/discovery?topic=discovery-element-classification#element-collection) teve um problema com normalizações HTML. Uma nova **Configuração de contrato padrão** foi incluída com esta liberação. Siga as etapas abaixo para aplicar a nova **Configuração de contrato padrão** às suas coleções.

     1. Determine quais de suas coleções estão usando o arquivo de configuração de **Configuração de contrato padrão** ou uma configuração customizada com base na **Configuração de contrato padrão**.
     1. Anote as mudanças feitas em quaisquer configurações customizadas com base na **Configuração de contrato padrão**.
     1. Como o antigo arquivo de **Configuração de contrato padrão** precisa ser excluído de seu ambiente antes que o novo seja usado, use a API [Excluir configuração ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#delete-a-configuration){: new_window} para excluir a **Configuração de contrato padrão** associada a qualquer uma de suas coleções. Exclua também quaisquer configurações com base na antiga **Configuração de contrato padrão**.
     1. Agora é possível usar o novo arquivo de **Configuração de contrato padrão**. Para cada coleção usando uma dessas configurações, crie uma nova coleção. Aplique a nova **Configuração de contrato padrão** ou crie uma nova configuração customizada com base na nova **Configuração de contrato padrão** usando as notas que você fez na etapa 2.
     1. Faça upload dos arquivos alimentados anteriormente para as coleções originais.
     1. Exclua as coleções antigas.

## 15 de agosto de 2018
{: #15aug18}

- Dois novos operadores de consulta estão disponíveis. `Exists` (`:*`) pode ser usado para retornar todos os resultados em que o `field` especificado existe. `Does not exist` (`!*`) pode ser usado para retornar todos os resultados que não incluem o `field` especificado. Consulte  [ Operadores de consulta ](/docs/services/discovery?topic=discovery-query-operators#query-operators)  para obter mais informações. 

## 2 de agosto de 2018
{: #2aug18}

- O {{site.data.keyword.discoveryfull}} agora suporta coleções nos idiomas inglês, espanhol, alemão, italiano, português, francês, árabe, coreano e japonês ao conectar e sincronizar com o Box, Salesforce e SharePoint Online com o conjunto de ferramentas do {{site.data.keyword.discoveryshort}}. 

## 31 de julho de 2018
{: #31jul18}
 
 - Iniciando em **1º de agosto de 2018**, o {{site.data.keyword.discoveryfull}} tem uma nova estrutura de precificação. Ele apresenta um modelo de precificação mais simples (as horas de documento não fazem mais parte do cálculo) e precificação em camadas para consultas do {{site.data.keyword.discoverynewsfull}}. Além disso, o plano Padrão tornou-se obsoleto e o plano Lite reduziu os limites de documento e de consulta do {{site.data.keyword.discoverynewsshort}}. As mudanças de precificação não requerem ação de usuários atuais do {{site.data.keyword.discoverynewsshort}}. Consulte  [ {{site.data.keyword.discoveryshort}}  Planos de Precificação ](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)  para obter detalhes.
 
**Nota:** a data de versão da API foi atualizada para `2018-08-01`. Para aproveitar as novas opções de dimensionamento de ambiente (`LT`, `XS`, `S`, `MS`, `M`, `ML`, `L`, `XL`, `XXL`, `XXXL`), deve-se usar essa data de versão ao criar ambientes com a API. Os tamanhos de ambiente agora têm o tipo de `string` (anteriormente, o tipo era `integer`.)

## 27 de julho de 2018
{: #27jul18}

- [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news) liberado em um idioma adicional: japonês (`collection_id`: `news-ja`). O {{site.data.keyword.discoverynewsfull}} também está disponível em inglês, espanhol, alemão e coreano.

## 25 de junho de 2018
{: #25jun18}

- Incluída a opção para se conectar e sincronizar com as origens de dados Salesforce, Microsoft SharePoint Online e Box. Essas origens de dados não estão disponíveis em ambientes Premium. Liberadas as APIs [Credencial de origem ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#list-credentials){: new_window} e [Configuração ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#add-configuration){: new_window} para essas origens de dados. 
  - O {{site.data.keyword.discoveryfull}} suporta somente coleções no idioma inglês ao conectar e sincronizar com o Box, Salesforce e SharePoint Online com o conjunto de ferramentas do {{site.data.keyword.discoveryshort}}. [ Resolvido ](/docs/services/discovery?topic=discovery-release-notes#2aug18)
  - O limite de tamanho do arquivo de documento individual para Box, Salesforce e SharePoint Online é de 10 MB.
- Incluído um novo Painel de Desempenho no conjunto de ferramentas do {{site.data.keyword.discoveryshort}}. Veja [Visualizando métricas e melhorando os resultados da consulta com o painel Desempenho](/docs/services/discovery?topic=discovery-performance-dashboard#performance-dashboard). O novo painel não está disponível nos ambientes Premium ou Dedicado.
- Incluído suporte integral para japonês. Para obter mais informações, consulte  [ Suporte ao idioma ](/docs/services/discovery?topic=discovery-language-support#language-support).

## 22 de junho de 2018
{: #22jun18}

- Liberada a API de Eventos e Feedback. Veja a [Referência da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#create-event){: new_window} para obter mais informações.

## 11 de junho de 2018
{: #11jun18}

-  Para aplicativos que estão hospedados em Washington, DC (Leste dos EUA), o serviço agora suporta a autenticação de Identity and Access Management (IAM) baseada em token. O IAM usa tokens de acesso em vez de credenciais de serviço para autenticação com um serviço. Para obter mais informações sobre como usar tokens do IAM com aplicativos novos e existentes, veja a atualização da liberação de [17 de maio de 2018](#17May18).
-  Um elemento do contrato adicional agora é suportado na Classificação de elementos: `Safety and Security`. Consulte  [ Entendendo Elementos do Contrato ](/docs/services/discovery?topic=discovery-element-classification#contract-elements)  para obter detalhes.

## 6 de junho de 2018
{: #6jun18}

- As consultas do {{site.data.keyword.discoverynewsfull}} agora exibem as primeiras 50 palavras de cada artigo no campo JSON `text`. [ Atualizar ](#24oct18)

## 5 de junho de 2018
{: #5jun18}

- A Classificação de elementos agora está disponível para aqueles inscritos nos planos Premium.
- A classificação `assurance` de `Low` não está mais disponível para Classificação de elementos.

## 31 de maio de 2018
{: #31may18}

- Incluído suporte integral para francês. Para obter mais informações, consulte  [ Suporte ao idioma ](/docs/services/discovery?topic=discovery-language-support#language-support).

## 30 de maio de 2018
{: #30may18}

- Corrigido um problema conhecido no  {{site.data.keyword.discoverynewsfull}}. Anteriormente, ao consultar o {{site.data.keyword.discoverynewsshort}}, era possível receber uma contagem de documentos incorreta porque os documentos em outros idiomas seriam contados junto com o idioma solicitado. Isso já não é mais o caso.
- Iniciando com as coleções criadas em e após `22 May 2018`, o {{site.data.keyword.discoveryshort}} agora retorna resultados da consulta que incluem caracteres especiais para os idiomas a seguir: inglês, alemão, francês, holandês, italiano e português. Por exemplo, se você consultar `aqui`, agora receberá os resultados para `aqui` e <code>aqu&iacute;</code>.

## 21 de maio de 2018
{: #21may18}

- [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news) liberado em um idioma adicional: alemão (`collection_id`: `news-de`). O {{site.data.keyword.discoverynewsfull}} também está disponível em inglês, espanhol e coreano.

## 17 de maio de 2018
{: #17May18}

- As consultas do {{site.data.keyword.discoverynewsfull}} agora exibem somente as primeiras 20 palavras de cada artigo no campo JSON `text`.

-   O serviço agora suporta um novo processo de autenticação de API para instâncias de serviço para aplicativos que são hospedados em Sydney (**au-syd**) a partir de 15 de maio de 2018. Elas serão ativadas para aplicativos que estão hospedados em outras regiões em breve. O {{site.data.keyword.Bluemix}} está no processo de migração para a autenticação de Identity and Access Management (IAM) baseada em token. O IAM usa tokens de acesso em vez de credenciais de serviço para autenticação com um serviço.

   Na localização Sydney, use tokens de acesso do IAM com o serviço {{site.data.keyword.discoveryshort}} para

    -   *Novas instâncias de serviço* que você cria depois de 15 de maio. Para obter mais informações, veja [Autenticando com tokens do IAM](/docs/services/watson/getting-started-iam.html).
    -   *Instâncias de serviço existentes* que você migra do Cloud Foundry para um grupo de recursos que é gerenciado pelo Resource Controller (RC). As instâncias de serviço que foram criadas antes de 15 de maio continuam a usar credenciais de serviço para autenticação até que você as migre. Para obter mais informações, veja [Migrando instâncias de serviço do Cloud Foundry para um grupo de recursos](/docs/resources/instance_migration.html).

    Todas as instâncias de serviço novas e existentes em outras regiões continuam a usar credenciais de serviço (`apikey:{apikey_value}`) para autenticação.

### Usando um token de acesso do IAM para autenticar
{: #iam-token}

Ao usar tokens de acesso do IAM, você se autentica antes de enviar uma solicitação ao serviço {{site.data.keyword.discoveryshort}}.

1.  Obtenha uma chave API do IBM Cloud. Use essa chave para gerar um token de acesso do IAM. Para obter mais informações, veja [Como obter um token do IAM usando uma chave API do serviço {{site.data.keyword.watson}}](/docs/services/watson/getting-started-iam.html#iamtoken).
1.  Passe o token de acesso do IAM para o serviço {{site.data.keyword.discoveryshort}} usando o cabeçalho `Authorization`. No cabeçalho, indique que o token de acesso é um token `Bearer` especificando `Authorization: Bearer {access_token}`.

    O exemplo de cURL simples a seguir usa um token de acesso:

    ```bash
    curl -X GET
    --header "Authorization: Bearer eyJhbGciOiJIUz......sgrKIi8hdFs"
    "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    Para obter mais informações, veja [Usando um token para autenticação](/docs/services/watson/getting-started-iam.html#use_token).

### Atualizando um token de acesso do IAM
{: #iam-refreshing}

Os tokens de acesso do IAM que são gerados tem a estrutura a seguir. Você usa o valor do campo `access_token` para fazer uma solicitação autenticada para o serviço.

```javascript
{
  "access_token": "eyJhbGciOiJIUz......sgrKIi8hdFs",
  "refresh_token": "SPrXw5tBE3......KBQ+luWQVY=",
  "token_type": "Bearer",
  "expires_in": 3600,
  "expiration": 1473188353
}
```
{: codeblock}

Os tokens de acesso têm um tempo limitado de vida. O campo `expires_in` indica a duração do token, neste caso, uma hora. O campo `expiration` mostra quando o token expira como um registro de data e hora do UNIX que especifica o número de segundos desde 1º de janeiro de 1970 (meia-noite UTC/GMT).

Em seu aplicativo, verifique o prazo de expiração do token de acesso antes de usá-lo para fazer uma solicitação autenticada. Se ele está expirado, deve-se atualizar o token de acesso antes de poder usá-lo. Você usa o valor do campo `refresh_token` para atualizar o token de acesso. Para obter mais informações, veja [Atualizando um token](/docs/services/watson/getting-started-iam.html#refresh_token).


## 11 de maio de 2018
{: #11may18}

- Detalhes sobre segurança de informações podem ser localizados aqui: [Segurança de informações](/docs/services/discovery?topic=discovery-information-security#information-security).
- O problema conhecido de `query_entities` do {{site.data.keyword.discoveryfull}} Knowledge Graph foi corrigido com a atualização da versão da API `2018-05-04`. Essa correção se aplicará somente se as entidades forem alimentadas ou substituídas após `2018-05-04`. As entidades podem ser substituídas realimentando os documentos antigos ou alimentando os novos documentos que contêm essas entidades. Se as entidades antigas não forem substituídas, o `query_entities` retornará tudo em maiúsculo com a versão da API `2018-05-04`.
  - Todos os nomes de entidade eram convertidos anteriormente em camel case no `query_entities`. Por exemplo, o nome da entidade "IBM Corporation" era convertido em "Ibm Corporation". Isso já não é mais o caso.

## 9 de maio de 2018
{: #9may18}

- Os documentos de amostra são agora armazenados localmente, na pasta de dados móveis locais de seu navegador. Para obter mais informações sobre documentos de amostra, veja [Fazendo upload de documentos de amostra](/docs/services/discovery?topic=discovery-configservice#uploading-sample-documents).

## 4 de maio de 2018
{: #4may18}

- Dois elementos de contrato adicionais agora são suportados na Classificação de elementos: atributos e proveniência. Consulte  [ Entendendo Elementos do Contrato ](/docs/services/discovery?topic=discovery-element-classification#contract-elements)  para obter detalhes.

## 26 de abril de 2018
{: #26apr18}

- O problema de ingestão a seguir foi corrigido: em alguns casos em que `json_normalizations` e/ou `normalizations` de pós-enriquecimento foram especificados, as normalizações podem ter sido aplicadas na ordem errada. Isso pode resultar em documentos que estão sendo indexados com valores de campo inesperados. Isso já não é mais o caso.
- O tamanho máximo do arquivo para um documento de amostra agora é 1 MB. O tamanho máximo do arquivo era anteriormente 5 MB.

## 12 de abril de 2018
{: #12apr18}

- Knowledge Graph: [Evidência](/docs/services/discovery?topic=discovery-kg#kg_evidence) e [Canonicalização e filtragem](/docs/services/discovery?topic=discovery-kg#kg_canonicalization) agora estão disponíveis em todas as coleções. Em quaisquer coleções criadas antes de `03-05-2018`, é necessário realimentar seus documentos para usar esses recursos. Anteriormente, você precisava criar uma nova coleção e realimentar seus documentos.

## 11 de abril de 2018
{: #11apr18}

- Duas categorias adicionais são agora suportadas na Classificação de elementos: `Asset Use` e `Communication`. Consulte  [ Entendendo Elementos do Contrato ](/docs/services/discovery?topic=discovery-element-classification#contract-elements)  para obter detalhes.

## 2 de abril de 2018
{: #2apr18}

- Os documentos de amostra agora são excluídos automaticamente após 24 horas, em vez de 1 mês.

## 16 de março de 2018
{: #16mar18}

- Incluído suporte integral para alemão. Para obter mais informações, consulte  [ Suporte ao idioma ](/docs/services/discovery?topic=discovery-language-support#language-support).

Conjunto de ferramentas do {{site.data.keyword.discoveryshort}}:
- Uma nova configuração denominada **Configuração de contrato padrão** foi incluída para suportar a Classificação de elementos, que pode ser usada para extrair a parte, a natureza e a categoria de elementos em PDFs. Consulte [ Classificação de Elementos ](/docs/services/discovery?topic=discovery-element-classification#element-collection) para obter detalhes.

Atualizado para disponibilidade geral:
- A segmentação de documentação foi movida do status beta para o status GA. O limite de segmentação foi aumentado para 250 segmentos. Ele não está mais limitado a 50 segmentos por documento. Consulte  [ Segmentação de documentação ](/docs/services/discovery?topic=discovery-configservice#doc-segmentation)  para obter detalhes.

Problema conhecido:
- Os curingas não funcionam com consultas que contêm letras maiúsculas. Por exemplo, dado o par chave/campo `{"borrower": "GOVERNMENT OF INDIA"}`, `query-borrower:*ndia` retornará resultados, mas `query-borrower:*NDIA` não os retornará.

## 8 de março de 2018
{: #8mar18}

- A versão beta do {{site.data.keyword.discoveryfull}} Knowledge Graph incluiu vários recursos. Durante a liberação beta, a funcionalidade [Knowledge Graph](/docs/services/discovery?topic=discovery-kg#kg) e os métodos associados a ela estão disponíveis somente para instâncias de serviço que estão inscritas nos planos **Avançado** e **Premium** e em todos os ambientes **dedicados**. Os novos recursos são:
  - [ Similaridade de Entidade ](/docs/services/discovery?topic=discovery-kg#kg_similarity)
  - [ Evidência ](/docs/services/discovery?topic=discovery-kg#kg_evidence)
  - [ Canonicalização e filtragem ](/docs/services/discovery?topic=discovery-kg#kg_canonicalization)

## 7 de março de 2018
{: #7mar18}

- O problema conhecido de ingestão foi corrigido: entre 28 de fevereiro e 6 de março, uma pequena porcentagem de documentos foi indexada com somente os campos `id` e `extracted_metadata` (outro conteúdo do documento não foi indexado). O problema subjacente foi corrigido, no entanto, será necessário reenviar quaisquer documentos afetados para ingestão. Não há uma maneira simples de identificar os documentos afetados.

## 5 de março de 2018
{: #5mar18}

- O problema conhecido do {{site.data.keyword.discoveryfull}} Knowledge Graph a seguir foi corrigido com a atualização da versão de API `2018-03-05`. Essa correção se aplica somente a coleções recém-criadas que usam a atualização de versão `2018-03-05`.  
  - Todos os nomes de tipo de entidade e nomes de tipo de relação foram convertidos anteriormente em maiúsculos durante a ingestão. Por exemplo, a entidade "GeoPoliticalEntity" foi convertida em "GEOPOLITICALENTITY" e a relação "partOf" foi convertida em "PARTOF." Isso já não é mais o caso.

## 1º de março de 2018
{: #1mar18}

- Os limites de [Expansão de consulta](/docs/services/discovery?topic=discovery-query-concepts#query-expansion) foram aumentados nos planos Avançado e Premium para 5.000 expansões de consulta e 25.000 termos no total. Consulte  [ Planos de precificação de descoberta ](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)  para obter detalhes.

## 28 de fevereiro de 2018
{: #28feb18}

- Os enriquecimentos do {{site.data.keyword.alchemylanguageshort}} foram descontinuados efetivamente em **1º de março de 2018**. Para obter informações sobre a migração de coleções existentes e arquivos de configuração que utilizam os enriquecimentos do {{site.data.keyword.alchemylanguageshort}}, consulte [Migrando enriquecimentos para o {{site.data.keyword.nlushort}}](/docs/services/discovery?topic=discovery-migrate-nlu#migrate-nlu).

## 23 de fevereiro de 2018
{: #23feb18}

- Incluída a capacidade de consultar por similaridade de documento. É possível consultar documentos semelhantes por IDs de documento e, opcionalmente, refinar ainda mais a similaridade especificando campos. Consulte  [ Similaridade do documento ](/docs/services/discovery?topic=discovery-query-concepts#doc-similarity)  para obter mais informações.

- O [parâmetro `highlight`](/docs/services/discovery?topic=discovery-query-parameters#highlight) nos resultados da consulta foi aprimorado. Os resultados da consulta retornarão sentenças completas, ordenadas por sua `score`.

## 21 de fevereiro de 2018
{: #21feb18}

- Anteriormente, ao alimentar documentos PDF, o `file_type` retornado quando avisos de ingestão eram consultados, no objeto `extracted_metadata` e na API de detalhes do documento, era `html`. Isso já não é mais o caso. O `file_type` retornado agora será `pdf`. 

## 26 de janeiro de 2018
{: #26jan18}

Conjunto de ferramentas do {{site.data.keyword.discoveryshort}}:

- Incluída a capacidade de acessar coleções coreanas e espanholas para o tile do [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news) no conjunto de ferramentas. Anteriormente, essas coleções podiam ser consultadas somente por meio da API.

## 23 de janeiro de 2018
{: #23jan18}

- Incluída a capacidade de expandir o escopo de uma consulta, por exemplo, é possível expandir uma consulta para "carro" para incluir "automóvel" e "veículo motorizado". Além disso, é possível substituir termos normalmente digitados incorretamente, por exemplo, substituir as consultas por "seabizcuit" por "seabiscuit". A expansão de consulta é implementada com a API do {{site.data.keyword.discoveryshort}}. Consulte  [ Expansão de consulta ](/docs/services/discovery?topic=discovery-query-concepts#query-expansion)  para obter detalhes.  

## 15 de janeiro de 2018
{: #15jan18}

- O {{site.data.keyword.discoverynewsfull}} Original foi retirado de serviço. Ele foi substituído em 31 de julho de 2017 por uma nova versão, denominada {{site.data.keyword.discoverynewsfull}}. Para obter instruções sobre como migrar do {{site.data.keyword.discoverynewsfull}} Original para a nova versão, veja [Migrando do Watson Discovery News Original](/docs/services/discovery?topic=discovery-migrate-bwdn#migrate-bwdn).

## 11 de janeiro de 2018
{: #11jan18}

- Incluído suporte integral para coreano. Para obter mais informações, consulte  [ Suporte ao idioma ](/docs/services/discovery?topic=discovery-language-support#language-support).

## 15 de dezembro de 2017
{: #15dec17}

- Liberado o enriquecimento **Classificação de Elementos**, que analisa elementos (sentenças, listas, tabelas) em documentos de controle para classificar categorias e tipos importantes. Consulte [Classificação de elementos](/docs/services/discovery?topic=discovery-element-classification#element-classification) para obter mais informações. A Classificação de Elementos não está disponível para instâncias de serviço que estejam inscritas no plano **Premium**. [ Resolvido ](/docs/services/discovery?topic=discovery-release-notes#5jun18)
- Incluído suporte ao idioma básico para chinês simplificado e holandês. Consulte [Suporte ao idioma](/docs/services/discovery?topic=discovery-language-support#language-support) para obter mais informações. Atualmente, as coleções em chinês simplificado e em holandês devem ser criadas com a API.
- Incluídos dois novos parâmetros para o Data Crawler: `proxy_host_port` e `read-timeout`. Consulte [Configurando o Data Crawler](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-the-data-crawler) para obter detalhes.
- Os problemas a seguir podem ser vistos ao alimentar documentos PDF: [Resolvido](/docs/services/discovery?topic=discovery-release-notes#21feb18)
  - Quando avisos de ingestão são consultados, o campo `file_type` para documentos PDF é retornado como `html`.
  - O campo `file_type` no objeto `extracted_metadata` de resultados para documentos PDF é configurado como `html`.
  - A API de detalhes de documento também retorna o campo `file_type` para documentos PDF como `html`.
- Se você estiver alimentando JSON, as matrizes de tipo misto não serão suportadas.  

Conjunto de ferramentas do {{site.data.keyword.discoveryshort}}:

- Incluído um gerador de consultas visual para a versão beta do {{site.data.keyword.discoveryfull}} Knowledge Graph. Consulte [Consultando o Knowledge Graph usando o conjunto de ferramentas do {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-kg#querying-kg)

## 30 de novembro de 2017
{: #30nov17}

- Liberada a versão beta do {{site.data.keyword.discoveryfull}} Knowledge Graph, que fornece novos terminais para consulta de entidades e de relações em documentos. Isso inclui buscas baseadas em contexto e classificação de relevância. Este recurso beta está disponível somente para usuários do plano **Avançado**. Ele não está disponível em ambientes **Dedicados**. [Resolvido](/docs/services/discovery?topic=discovery-release-notes#8mar18) Veja [{{site.data.keyword.discoveryfull}} Knowledge Graph](/docs/services/discovery?topic=discovery-kg#kg) para obter mais informações.  Um comunicado explicando os recursos beta pode ser localizado [aqui](/docs/services/discovery?topic=discovery-release-notes#beta-features).
  - Problema conhecido no {{site.data.keyword.discoveryfull}} Knowledge Graph: todos os nomes de tipo de entidade e nomes de tipo de relação são convertidos em maiúsculas durante a ingestão. Por exemplo, a entidade "GeoPoliticalEntity" é convertida em "GEOPOLITICALENTITY" e a relação "partOf" é convertida em "PARTOF." [ Resolvido ](/docs/services/discovery?topic=discovery-release-notes#5mar18)
- Liberado o [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news) em dois idiomas adicionais: coreano (`collection_id`: `news-ko`) e espanhol (`collection_id`: `news-s`). O {{site.data.keyword.discoverynewsfull}} em coreano e em espanhol está disponível para uso por meio da API apenas. Para obter informações sobre a consulta de uma coleção por meio da API, consulte [Referência de API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#query-your-collection){: new_window} [Resolvido](/docs/services/discovery?topic=discovery-release-notes#26jan18). O {{site.data.keyword.discoverynewsfull}} em inglês agora possui o `collection_id` de `news-en`. Anteriormente, o `collection_id` era `news` - se você estiver usando o `collection_id` anterior, ele continuará funcionando, no entanto, será possível mudar para o novo, `collection_id` para novos projetos.
- Os resultados da consulta retornam um valor de `score`, que indica a relevância relativa entre os resultados da consulta. A partir de 30 de novembro de 2017, a maneira com que o `score` é calculado mudou. O valor de `score` deve ser usado somente para classificar documentos em uma procura única, não em procuras ou sessões. Se você tiver treinado uma coleção, um valor de `score` será retornado nos resultados de uma consulta de linguagem natural. Como o `score` indica a relevância relativa entre os resultados da consulta, ele não deve ser usado como um limite. Em vez disso, use o `confidence`, que indica a relevância do resultado quando comparado com o modelo treinado, para configurar limites. Consulte [Pontuações de confiança](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence) para obter mais informações sobre configuração de limites.
- Iniciando com esta liberação, a recuperação de passagem detecta limites de sentença, que tenta retornar passagens que começam no início de uma frase e que param no término. Anteriormente, muitas passagens iniciariam ou terminariam em algum lugar no meio da sentença. Consulte [Passagens](/docs/services/discovery?topic=discovery-query-parameters#passages) para obter mais informações sobre a recuperação de Passagem.

## 15 de novembro de 2017
{: #15nov17}

Conjunto de ferramentas do {{site.data.keyword.discoveryshort}}:

- Incluído o enriquecimento [Extração de relação](/docs/services/discovery?topic=discovery-configservice#relation-extraction), que inclui a opção para incorporar um modelo de relação customizado criado com o {{site.data.keyword.knowledgestudiofull}}.
- O conjunto de ferramentas {{site.data.keyword.discoveryshort}} do enriquecimento [Extração de Entidade](/docs/services/discovery?topic=discovery-configservice#entity-extraction) agora inclui a opção para incorporar um modelo de entidade customizado criado com o {{site.data.keyword.knowledgestudiofull}}.
- A opção para criar uma coleção em japonês foi removida do conjunto do conjunto de ferramentas do {{site.data.keyword.discoveryshort}}, no entanto, a opção para criar uma coleção em japonês usando a API do {{site.data.keyword.discoveryshort}} permanece.
- O {{site.data.keyword.discoveryshort}} Tooling agora suporta ambientes organizados.

## 10 de novembro de 2017
{: #10nov17}

Conjunto de ferramentas do {{site.data.keyword.discoveryshort}}:

- Incluídas opções adicionais para recuperação de Passagem no conjunto de ferramentas do {{site.data.keyword.discoveryshort}}. Durante a consulta, agora é possível especificar os campos dos quais você deseja que as passagens sejam retornadas, o número de passagens a serem retornadas e a contagem máxima de caracteres para cada passagem. Consulte [Passagens](/docs/services/discovery?topic=discovery-query-parameters#passages) para obter os limites mínimos e máximos.

## 8 de novembro de 2017
{: #8nov17}

A sequência de versão para todas as chamadas API mudou de `2017-10-16` para `2017-11-07`. Esta versão:
- Moveu a `score` em cada resultado da consulta para um novo objeto denominado `result_metadata`.
- Se a coleção consultada foi treinada e a consulta for uma consulta de língua natural, `result_metadata` incluirá um campo `confidence` que exibe a pontuação de confiança para esse resultado. Consulte [Pontuações de confiança](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence) para obter detalhes.
- Os campos que incluem espaços em branco (por exemplo: `body.additional read`) serão filtrados durante a ingestão. A descrição `notices` lerá `O campo 'leitura adicional' é inválido: espaço em branco, '.', '#' e ',' são inválidos em um nome de campo`.
- O campo `result_metadata` será filtrado durante a ingestão.

## 16 de outubro de 2017
{: #16oct17}

- A sequência de versão para todas as chamadas API mudou de `2017-09-01` para `2017-10-16`. Esta versão descontinua o suporte para upload de novos documentos em coleções existentes aprimoradas com enriquecimentos do {{site.data.keyword.alchemylanguageshort}} e para a criação de novas coleções e aprimoramento delas com os enriquecimentos do {{site.data.keyword.alchemylanguageshort}}. As coleções existentes enriquecidas com o {{site.data.keyword.alchemylanguageshort}} devem ser migradas para os enriquecimentos do {{site.data.keyword.nlushort}} assim que possível. Consulte [Migrando enriquecimentos para {{site.data.keyword.nlushort}}](/docs/services/discovery?topic=discovery-migrate-nlu#migrate-nlu) para obter detalhes. O conjunto de ferramentas do {{site.data.keyword.discoveryshort}} também usa a versão `2017-10-16`, consulte abaixo para obter mais informações.

Conjunto de ferramentas do {{site.data.keyword.discoveryshort}}:

- O conjunto de ferramentas do {{site.data.keyword.discoveryshort}} usa a sequência de versão da API `2017-10-16`, portanto, se você estiver usando o conjunto de ferramentas, não será mais possível fazer upload de documentos para as coleções existentes do {{site.data.keyword.alchemylanguageshort}} ou criar novas coleções aprimoradas com enriquecimentos do {{site.data.keyword.alchemylanguageshort}} após a versão `2017-10-16`.  Se você deseja continuar o uso do conjunto de ferramentas do {{site.data.keyword.discoveryshort}} para enriquecer coleções, primeiramente migre suas coleções para o {{site.data.keyword.nlushort}}. Consulte [Migrando enriquecimentos para {{site.data.keyword.nlushort}}](/docs/services/discovery?topic=discovery-migrate-nlu#migrate-nlu) para obter detalhes.
- O **Data Schema Explorer** exibe consultas de amostra para vários enriquecimentos na coleção do {{site.data.keyword.discoverynewsfull}}. Agora ele também tem um link **Mostrar mais valores** que exibirá valores de exemplo adicionais para esse enriquecimento no {{site.data.keyword.discoverynewsfull}}.
- Múltiplos aprimoramentos de produtividade, incluindo uma combinação de estatísticas de coleção, erros e avisos e dados de insights na tela **Gerenciar dados**.
- Uma mensagem foi incluída que exibe um alerta quando o processamento dos documentos é concluído.

## 9 de outubro de 2017
{: #9oct17}

- Uma nova métrica de agregação `unique_count` está disponível na API. Ela retorna uma contagem de instâncias exclusivas do campo especificado em uma coleção. Consulte [unique_count](/docs/services/discovery?topic=discovery-query-aggregations#unique_count) para obter mais informações.

Conjunto de ferramentas do {{site.data.keyword.discoveryshort}}:

- As agregações Histograma e Fatia de tempo agora são suportadas no **Visual Query Builder**. Também há a opção para ativar a detecção de anomalias para consultas de Fatia de tempo.
- O **Data Schema Explorer** exibe consultas de amostra para o enriquecimento escolhido. Agora ele também possui um link **Mostrar mais valores" que exibe valores de exemplo adicionais para esse enriquecimento.
- Um menu de hambúrguer foi incluído para agilizar a navegação nas telas **Gerenciar dados**, **Visualizar dados do esquema** e **Construir consultas**.

### 3 de outubro de 2017
{: #3oct17}

- A segmentação de documento agora está disponível. Consulte [Dividindo documentos com segmentação de documento](/docs/services/discovery?topic=discovery-configservice#doc-segmentation).

### 29 de setembro de 2017
{: #29sept17}

- {{site.data.keyword.discoveryshort}} ativado na localização `Germany` em 29 de setembro de 2017. Para conformidade com as regulamentações de dados da UE, os enriquecimentos AlchemyLanguage não são suportados nessa localização.
- Problema conhecido: os campos de consulta não podem conter espaços em branco.  Ao gravar uma consulta no {{site.data.keyword.discoveryshort}}, se qualquer campo de consulta contiver espaço em branco (por exemplo, `body.additional read`), você receberá um `Erro 400: sintaxe de consulta inválida`. [ Resolvido ](/docs/services/discovery?topic=discovery-release-notes#8nov17)

### 25 de setembro de 2017
{: #25sept17}

- Um plano de precificação Premium agora está disponível. Para obter mais informações, consulte  [ Planos de precificação do {{site.data.keyword.discoveryshort}}  ](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans).
- As capacidades de consultar, listar campos e consultar avisos entre as coleções no mesmo ambiente foram incluídas. Consulte [Consultando múltiplas coleções](/docs/services/discovery?topic=discovery-query-concepts#multiple-collections) para obter detalhes.
- Informações de suporte ao idioma para o {{site.data.keyword.discoveryshort}} estão disponíveis em [Suporte ao idioma](/docs/services/discovery?topic=discovery-language-support#language-support)

Conjunto de ferramentas do {{site.data.keyword.discoveryshort}}:
- O Visual Query Builder mudou do status beta para o status GA. As agregações Filtro, Fatia de tempo e Histograma não são suportadas atualmente com o Visual Query Builder. Clique em **Incluir análise de seus resultados** e depois em **Editar no Query Language** na tela **Construir consultas** para gravar essas agregações.
- Incluído o recurso beta para deduplicação em consultas do {{site.data.keyword.discoverynewsfull}}.
- Além das coleções de idiomas inglês, alemão e espanhol, agora é possível criar coleções em árabe, francês, italiano, coreano, japonês e português do Brasil.
- Problema conhecido: o {{site.data.keyword.discoveryshort}} Tooling não suporta ambientes organizados. [ Resolvido ](/docs/services/discovery?topic=discovery-release-notes#15nov17)

### 14 de setembro de 2017
{: #14sept17}

Conjunto de ferramentas do {{site.data.keyword.discoveryshort}}:

- Incluído o Data Schema Explorer, que exibe os campos e os valores em seus documentos transformados. Essas informações podem ser usadas para entender a estrutura de dados de sua coleção antes de construir consultas usando o Discovery Query Language. O esquema de dados pode ser visualizado de duas maneiras: pelo documento (visualização Documento) ou pelo campo (visualização Coleção). Para acessar o Data Schema Explorer: na tela **Meus insights de dados**, clique no botão **Visualizar esquema de dados** ou clique no ícone **Visualizar esquema de dados** à esquerda.

### 6 de setembro de 2017
{: #6sept17}

- Incluída a capacidade beta para deduplicar documentos retornados de sua consulta. Esse recurso beta funciona para coleções privadas e do Watson Discovery News. Consulte [Excluindo documentos duplicados dos resultados da consulta](/docs/services/discovery?topic=discovery-query-parameters#deduplication) para obter detalhes.

A deduplicação de documento é atualmente suportada somente como um recurso beta. Consulte a instrução sobre betas no topo deste documento para obter mais informações

### 31 de agosto de 2017
{: #31aug17}

- A sequência de versão para todas as chamadas API mudou de `2017-08-01` para `2017-09-01`. Essa versão inclui atualizações que filtram os campos JSON inválidos a seguir durante a visualização e a ingestão, para que somente os campos JSON válidos sejam alimentados. Atualize sua sequência de versão para `2017-09-01` para evitar conflitos e possíveis erros.

   - `id`, `score` e `highlight` no nível superior (é possível continuar a incluir documentos em sua coleção usando os IDs de documento com a função `include a document`. Consulte a [Referência da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#add-a-document){: new_window} para obter detalhes.
   - `_` como prefixo de nomes de campo no nível superior (como resultado, ao consultar um documento por ID, é possível consultar para `id` em vez de `_id`).
   - `#` e `,` no nome do campo
   - `+` e `-` como prefixo de nomes de campo
   - `"` `"` representando valores vazios para um nome de campo

**Nota:** se seus documentos JSON incluírem estes caracteres nos nomes de campos ou `id`, `score` e `highlight` no nível superior, será necessário removê-los antes de incluir os documentos em sua coleção ou os campos ficarão vazios. É possível criar uma configuração customizada e normalizar o JSON antes de incluir documentos em sua coleção para evitar esse problema. Consulte [Configuração customizada](/docs/services/discovery?topic=discovery-configservice#custom-configuration).  Além disso, os documentos que incluem os caracteres de pontuação `?`, `:` ou `#` no nome do arquivo causam erros no momento da ingestão. Renomeie quaisquer documentos que incluam estes caracteres antes de alimentá-los.

- Os métodos de recuperação para `natural_language_query` foram atualizados para melhorar a relevância dos resultados correspondendo palavras com semântica relacionada. Essa atualização afeta apenas as coleções que não tiveram treinamento de relevância. Se você estiver usando `natural_language_query` e não tiver realizado o treinamento de relevância, talvez veja uma melhora na ordem dos resultados retornados.

Conjunto de ferramentas do {{site.data.keyword.discoveryshort}}:

- Mudanças no gerador de consultas para facilitar a alternância entre as opções de consulta do Discovery Query Language e do Natural Language, bem como entre a consulta, o filtro e a agregação.


### 25 de agosto de 2017
{: #25aug17}

- A matriz `passages` agora inclui `field`, `start_offset` e `end_offset`. `field` é o nome do campo do qual a passagem foi extraída. `start_offset` é o caractere inicial do texto de passagem dentro do campo. `end_offset` é o caractere de finalização do texto de passagem dentro do campo.

Conjunto de ferramentas do {{site.data.keyword.discoveryshort}}: esse aprimoramento de construção de consulta pode ser localizado na tela **Construir consultas**.

-  Incluída a habilidade beta de gravar consultas no {{site.data.keyword.discoveryshort}} Query Language com um construtor visual. Clique em **Construir no modo visual** nas seções **Procurar por documentos** e **Limitar quais documentos serão consultados** para experimentar.  Conforme você constrói sua consulta visualmente, ela é exibida no **{{site.data.keyword.discoveryshort}} Query Language** abaixo dela.

   O gerador de consultas visual é atualmente suportado apenas como um recurso beta. Consulte a instrução sobre betas no topo deste documento para obter mais informações

### 18 de agosto de 2017
{: #18aug17}

Conjunto de ferramentas do {{site.data.keyword.discoveryshort}}:

- Incluído suporte para agregações e condições aninhadas para o construtor de agregação visual beta introduzido em [11 de agosto de 2017](/docs/services/discovery?topic=discovery-release-notes#11aug17). Há um limite de 3 condições por linha de agregação.

   O construtor de agregação visual atualmente é suportado apenas como um recurso beta. Consulte a instrução sobre betas no topo deste documento para obter mais informações

### 11 de agosto de 2017
{: #11aug17}

Conjunto de ferramentas do {{site.data.keyword.discoveryshort}}:

Ambos os recursos são aprimoramentos de construção de consulta e podem ser localizados na tela **Construir consultas**.

- Incluída a opção para selecionar uma consulta de um conjunto de consultas e de agregações de amostra pré-construídas. Clique em **Usar uma consulta de amostra** na parte superior direita para acessar a lista. Se você estiver consultando uma coleção de dados privados, as amostras usarão `top entities`, `categories`, etc., localizados em sua coleção. Essas consultas podem ser usadas como ponto inicial para gravação de suas próprias consultas. As consultas de amostra estão disponíveis para coleções do {{site.data.keyword.discoverynewsfull}} e privadas.

-  Incluída a capacidade beta para gravar agregações com um construtor visual. Clique em **Construir no modo visual** acima do campo **Gravar uma consulta de agregação usando o {{site.data.keyword.discoveryshort}} Query Language** para experimentar.  Conforme você constrói sua agregação visualmente, a consulta é exibida no **{{site.data.keyword.discoveryshort}} Query Language** abaixo dela.  

   O construtor de agregação visual atualmente é suportado apenas como um recurso beta. Consulte a instrução sobre betas no topo deste documento para obter mais informações

### 31 de julho de 2017
{: #31jul17}

- Uma nova versão do {{site.data.keyword.discoverynewsfull}} foi liberada. A versão original foi renomeada {{site.data.keyword.discoverynewsfull}} Original e foi retirada com uma remoção da data de serviço de **15 de janeiro de 2018**. Consulte [Migrando do Watson Discovery News Original](/docs/services/discovery?topic=discovery-migrate-bwdn#migrate-bwdn) para obter instruções de migração.   **Nota:** se você tiver criado uma nova instância do {{site.data.keyword.discoveryshort}}, você terá acesso somente à nova versão do {{site.data.keyword.discoverynewsfull}}.

- Um novo plano de precificação para o {{site.data.keyword.discoveryfull}} foi liberado. Consulte  [ Planos de precificação do {{site.data.keyword.discoveryshort}}  ](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)  para obter detalhes.

- A sequência de versão para todas as chamadas de API mudou de `2017-07-19` para `2017-08-01`. Essa versão inclui atualizações para o novo plano de precificação e a nova versão do Watson Discovery News. Atualize a sequência de versão para evitar conflitos e possíveis erros.

### 19 de julho de 2017
{: #19jul17}

 - Como parte da mudança de precificação que foi anunciada para 1º de agosto de 2017, os usuários que estão atualmente no plano de **30 dias de avaliação grátis** descontinuado serão migrados automaticamente para o plano **Lite**. Como resultado dessa transição, os usuários existentes podem ter cumprido ou excedido o limite do plano Lite em documentos _(2000)_, armazenamento _(200Mb)_ ou número de coleções _(2)_. Se você exceder o limite do plano **Lite**, não poderá incluir nenhum conteúdo adicional no serviço, mas ainda poderá consultar coleções. É possível visualizar o status atual de todos esses limites usando o conjunto de ferramentas do {{site.data.keyword.discoveryshort}} ou a API. Para ser capaz de continuar incluindo conteúdo na instância do {{site.data.keyword.discoveryshort}}, deve-se fazer um dos seguintes:
   - remova coleções e/ou documentos para que os limites do plano **Lite** não seja excedido.
     Os documentos podem ser excluídos individualmente por meio da API usando o método [delete-doc](https://{DomainName}/apidocs/discovery#delete-a-document) ou coleções inteiras podem ser excluídas usando o Tooling ou a API por meio do método [delete-collection](https://{DomainName}/apidocs/discovery#delete-a-collection)
   - Faça upgrade de seu plano para um nível que atenda às suas necessidades de armazenamento.
 - Os clientes com ambientes de tamanho **`1`**, **`2`** ou **`3`** serão migrados automaticamente para o plano **Avançado**.

### 17 de julho de 2017
{: #17jul17}

 - Os recursos a seguir foram movidos do status beta para o status GA:

   - Treinamento de relevância
   - Consulta de linguagem natural
   - Destaque

 - Desta liberação em diante, o {{site.data.keyword.discoveryfull}} está mudando seu mecanismo de enriquecimento do {{site.data.keyword.alchemylanguageshort}} para o {{site.data.keyword.nlushort}}. Como o {{site.data.keyword.alchemylanguageshort}} está no processo de descontinuação, é necessário iniciar o uso do {{site.data.keyword.nlushort}} o mais breve possível.  Consulte [Migrando de enriquecimentos {{site.data.keyword.alchemylanguageshort}} para enriquecimentos {{site.data.keyword.nlushort}}](/docs/services/discovery?topic=discovery-migrate-nlu#migrate-nlu) para obter detalhes.
   **Nota:** ao integrar-se com o Watson Knowledge Studio, a configuração de enriquecimento do {{site.data.keyword.alchemylanguageshort}} ainda deve ser usada. Consulte [Integrando-se com o {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-with-wks) para obter detalhes.

 - A sequência de versão para todas as chamadas API mudou de `2017-06-25` para `2017-07-19`. Essa versão permite uma configuração padrão de NLU na criação da coleção. Você ainda deve ser capaz de enriquecer com o {{site.data.keyword.alchemylanguageshort}} em versões anteriores.

    A configuração padrão foi atualizada para usar o {{site.data.keyword.nlushort}}. É necessário atualizar a sequência de versões assim que possível para evitar conflitos e possíveis erros.

 - Conjunto de ferramentas de descoberta:

    Os Cartões de Insights para coleções aprimoradas com enriquecimentos do {{site.data.keyword.alchemylanguageshort}} não serão mais atualizados automaticamente. Deve-se migrar sua coleção para o {{site.data.keyword.nlushort}} Enrichments para que os cartões de insight sejam atualizados.

    Se você criou uma coleção antes de **18 de julho de 2017** e aplicou a **Configuração Padrão**, essa coleção foi aprimorada com enriquecimentos do {{site.data.keyword.alchemylanguageshort}}. Se você aplicar a **Configuração Padrão** a uma coleção após essa data, os enriquecimentos do {{site.data.keyword.nlushort}} serão usados (o nome da configuração alternará para **Configuração Padrão com o NLU** no conjunto de ferramentas). Como os enriquecimentos do {{site.data.keyword.alchemylanguageshort}} estão sendo descontinuados, eles não devem ser usados com novas coleções.

### 30 de junho de 2017
{: #30jun17}

 -  A capacidade de normalização de entidade introduzida como um recurso beta em 5 de maio de 2017 foi movida para o status GA. Consulte [Criando uma configuração customizada para normalizar entidades](/docs/services/discovery?topic=discovery-normalizing-entities-cc#normalizing-entities-cc) para obter detalhes.

### 23 de junho de 2017
{: #23jun17}

 - A sequência de versão para todas as chamadas API mudou de `2017-12-01` para `2016-06-25`. A nova sequência de versão ativará enriquecimentos em alemão (`de`) ou em espanhol (`es`) se o idioma de uma coleção estiver configurado para um desses idiomas. Anteriormente, todos os enriquecimentos eram executados em inglês, independentemente da configuração de idioma de uma coleção.

    Se você não usar enriquecimentos em idiomas diferentes do inglês, será possível continuar a usar a sequência de versão `2016-12-01`. No entanto, é necessário atualizar a sequência de versão assim que possível para evitar conflitos futuros em potencial.

 - A detecção de anomalia agora está disponível como parte das agregações de `timeslice` como um recurso GA. Consulte [Detecção de anomalias de fatia de tempo](/docs/services/discovery?topic=discovery-query-aggregations#anomaly-detection) para obter detalhes.

 - Conjunto de ferramentas de descoberta:

   - Incluída a capacidade beta para melhorar a relevância dos resultados da consulta usando o Discovery Tooling (conjunto de ferramentas de relevância). Consulte [Melhorando a relevância dos seus resultados da consulta com o Discovery Tooling](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling).

### 19 de junho de 2017
{: #19jun17}

  - Conjunto de ferramentas de descoberta:

    - Incluída opção para especificar o idioma dos documentos em uma nova coleção, como inglês, espanhol ou alemão. Para usá-la, escolha **Selecionar o idioma dos seus documentos** no diálogo **Nomear sua nova coleção**.

    - Incluída uma guia **Resumo** na tela **Construir consultas**. A guia **Resumo** exibe uma visão geral dos resultados da consulta completos fornecidos na guia **JSON** existente. A exibição **Resumo** varia com base em sua consulta e enriquecimentos. As informações que podem ser exibidas incluem: nome ou ID do documento, estatísticas de agregação, passagens documento em ordem de relevância e resultados por enriquecimento.

    - Incluída uma opção do Natural Language Query na tela **Construir consultas** tela. Para usá-la, clique em **Fazer uma pergunta em língua simples** na seção **Procurar por documentos** e um campo aparecerá no qual é possível inserir sua pergunta. O campo de consulta original (anteriormente intitulado **Insira uma consulta ou palavra-chave**) agora pode ser acessado clicando no botão **Usar o Discovery Query Language**.

    - A tela **Construir consultas** foi reprojetada, mas todos os campos e opções permanecem. A seguir estão os nomes antigos e novos dos campos.

| **Nome do campo antigo**                                           | **Nome do novo campo ou seção**                                                                                             |
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| Gravar e executar uma consulta                                    | Procurar por documentos                                                                                                  |
| Limitar seus resultados da consulta (filtro)                       | Limitar quais documentos serão consultados                                                                                       |
| Agrupar resultados da consulta (agregação)                        | Incluir análise de seus resultados                                                                                      |
| Campos para exibição                                        | O nome não mudou, mas foi movido para a nova seção **Customizar opções de exibição**.                                      |
| Número de documentos a serem retornados (contagem)                    | Número de documentos a serem retornados [esse campo foi movido para a seção **Customizar opções de exibição**].                    |
| Incluir passagens correspondentes                                | Incluir passagens relevantes [esse campo foi movido para a seção **Customizar opções de exibição**].                        |
| Número de campos de consulta a serem ignorados no início (compensação) | Número de resultados da consulta a serem ignorados no início [esse campo foi movido para a seção **Customizar opções de exibição**]. |

### 5 de junho de 2017
{: #5jun17}

 - As consultas do Watson Discovery News agora exibem apenas as primeiras 150 palavras de cada artigo nos campos JSON `text` e `alchemyapi_text`. O campo `blekko.snippet` exibe apenas a primeira sentença da matriz de fragmento.

### 30 de maio de 2017
{: #30may17}

 - O parâmetro `passages` na consulta da API foi movido do status beta para GA.

### 25 de maio de 2017
{: #25may17}

 - Discovery Tooling: o destaque do campo de consulta foi incluído nesta liberação. Este recurso inclui destaque amarelo nos nomes de campos no JSON da área de janela Resultados. Todos os campos que são consultados ou filtrados são destacados para cada resultado, mesmo se o conteúdo do campo não corresponde à consulta. Quaisquer campos usados em agregações também são destacados nos resultados da consulta, mas apenas a primeira operação de agregação é destacada.

### 10 de maio de 2017
{: #10may17}

 - Os métodos `query` e `notices` agora suportam o parâmetro `highlight`. O parâmetro é um booleano. Ao executar uma consulta e especificar `highlight` como `true`, o serviço retorna a saída que inclui um novo campo `highlight` no qual palavras que correspondem à consulta são agrupadas em tags `*` (ênfase) HTML. Consulte os [Parâmetros de consulta](/docs/services/discovery?topic=discovery-query-parameters#highlight) para obter detalhes.

 - É possível concluir a exclusão de um ambiente apenas parcialmente, resultando em uma situação na qual um novo ambiente não pode ser criado, porque somente um único ambiente por instância de serviço é permitido. Se você tentar excluir e, em seguida, criar um ambiente e alguma operação estiver paralisada no estado `pending`, provavelmente você encontrou esse problema. Como uma solução alternativa, execute novamente a operação de exclusão para concluí-la e, em seguida, crie o novo ambiente.

### 8 de maio de 2017
{: #8may17}

 - Atualizado o modelo de pontuação de sinal de emoção para melhorar a precisão nos enriquecimentos de análise de emoção (`docEmotion`). O conjunto de dados de treinamento foi expandido e a engenharia de recurso foi mudada e, como resultado, o modelo possui maior precisão no conjunto dados de referência.

### 5 de maio de 2017
{: #5may17}

 - A normalização da entidade está agora disponível para uso com o serviço do Discovery que usa um modelo customizado gerado pelo Watson Knowledge Studio. A normalização da entidade insere nomes normalizados (canônicos) para referências diferentes para a mesma pessoa ou objeto no documento de origem. Consulte [Criando uma configuração customizada para normalizar entidades](/docs/services/discovery?topic=discovery-normalizing-entities-cc#normalizing-entities-cc) para obter detalhes.

     **Nota:** a normalização de entidade é suportada atualmente apenas como um recurso beta. Consulte a instrução sobre betas no topo deste documento para obter mais informações [ Resolvido ](/docs/services/discovery?topic=discovery-release-notes#30jun17)

Conjunto de ferramentas do {{site.data.keyword.discoveryshort}}:

 - O log de erro do Tooling não está mais limitado a um máximo de 8 (oito) páginas de resultados. O log de erros ainda exibe o ID do documento se o nome do documento não está disponível.

 - Os nomes de configuração são limitados a 50 caracteres e devem consistir nos caracteres `[a-zA-Z0-9-_]`. 

 - O parâmetro `passages` disponível anteriormente somente por meio da API agora está disponível também por meio do Tooling.

### 25 de abril de 2017
{: #25apr17}

  - O serviço agora permite que você forneça *dados de treinamento* para melhorar a precisão dos seus resultados da consulta. Ao fornecer uma instância do Discovery com dados de treinamento, o serviço usa os algoritmos avançados do Watson para determinar os resultados mais relevantes. À medida que você inclui mais dados de treinamento, a instância do serviço se torna mais precisa e sofisticada nos resultados retornados. Consulte [Melhorando a relevância dos seus resultados da consulta](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api) e a [Referência da API](https://{DomainName}/apidocs/discovery#list-training-data) para obter informações.

  - A API agora suporta o parâmetro `natural_language_query` como uma liberação beta. Este parâmetro permite especificar uma consulta em linguagem natural, não na linguagem de consulta do serviço do Discovery. Consulte o método [Consulte sua coleção](https://{DomainName}/apidocs/discovery#query-your-collection) na referência de API para informações.

  - Atualizações de documentação e correções de erratas.

### 14 de abril de 2017
{: #14apr17}

Aprimoramentos foram incluídos na API de consulta (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`). Consulte o método [Consulte sua coleção](https://{DomainName}/apidocs/discovery#query-your-collection) na referência de API para informações.

  - A consulta de API agora suporta o parâmetro `passages`. Se o parâmetro for configurado como `true`, a consulta retornará um conjunto de passagens mais relevantes dos documentos em sua coleção. As passagens são geradas por algoritmos Watson sofisticados para determinar as melhores passagens de texto de todos os documentos retornados pela consulta. Isso permite localizar informações e contexto com mais precisão. Consulte o método [Consulte sua coleção](https://{DomainName}/apidocs/discovery#query-your-collection) na referência de API para informações.

    - A especificação de `passages=true` em sua consulta pode reduzir o desempenho como resultado do aumento de processamento para extrair passagens. Em ambientes maiores, o impacto no desempenho pode ser reduzido.

    - O parâmetro `passages` é suportado apenas em coleções privadas. Ele não é suportado na coleção do Watson Discovery News.

    - O parâmetro `passages` atualmente retorna um máximo de 10 resultados. O número de resultados retornados não pode ser mudado. [ Atualizar ](/docs/services/discovery?topic=discovery-query-parameters#passages_count)

    - O parâmetro `passages` retorna um máximo de 3 (três) passagens de qualquer documento especificado na coleção. Se um documento contiver mais de três passagens relevantes adicionais, o parâmetro não as retornará.

### 7 de abril de 2017
{: #7apr17}

- A API de consulta (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`) agora suporta o parâmetro `sort`, que permite especificar uma lista separada por vírgula de campos no documento para classificação. Consulte o método [Consultar a sua coleção ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#query-your-collection){: new_window} na referência de API para obter informações.
- O parâmetro `timeslice` para agregações de consulta agora manipula corretamente datas no formato de época do UNIX. Consulte [Referência de consulta](/docs/services/discovery?topic=discovery-query-reference#aggregations) para obter informações sobre agregações e o parâmetro `timeslice`.
- Aprimoramentos para mensagens de erro.
- Atualizações para o SDK Java de serviço. Consulte a [Referência da API](https://{DomainName}/apidocs/discovery?language=java) para obter detalhes.
- As limitações a seguir para o uso de curingas em consultas estão agora corrigidas e funcionando corretamente:

  - Somente um curinga funcionava em qualquer consulta especificada. Por exemplo, `query-month:*ctober` funcionava, mas `query-month:*ctobe*` gerava um erro de análise.
  - Curingas não funcionavam com consultas que continham letras maiúsculas. Por exemplo, dado o par chave/campo `{"borrower": "GOVERNMENT OF INDIA"}`, `query-borrower:*ndia` retornava resultados, mas `query-borrower:*NDIA` não retornava.

**Nota:** curingas não são necessários em frases em consultas. Por exemplo, dado o par chave/campo `{"borrower": "GOVERNMENT OF TIMOR"}`, `query-borrower:"GOVERNMENT OF TIMOR"` retorna resultados, mas `query-borrower:"GOVERNMENT OF TI*OR"` não retorna. O uso de um curinga não é aplicável dentro de frases, porque todos os caracteres dentro das aspas (`"`) de uma frase são escapados.

### 24 de março de 2017
{: #24mar17}

- Incluída a filtragem na tela "Meus insights de dados" no Discovery Tooling

### 15 de março de 2017
{: #15mar17}

Os problemas conhecidos a seguir foram descobertos.

-  Todos os campos que são alimentados com documentos HTML, PDF e Word são digitados como **sequência**. Campos JSON e campos calculados, como pontuação de confiança, são do tipo conforme definido. [ Atualizar ](/docs/services/discovery?topic=discovery-addcontent#adding-content-with-the-api-or-tooling)
- A operação `preview` não verifica atualmente as matrizes JSON aninhadas dentro de um documento JSON enviado. Como o serviço não suporta atualmente matrizes JSON aninhadas, um documento com matrizes aninhadas pode passar com sucesso na operação `preview`, mas falha em uma tentativa de ingestão. Consulte  [ Posso fazer upload de matrizes JSON? ](/docs/services/discovery?topic=discovery-faqs#array)
- Se você encontrar erros de ingestão com a mensagem `idioma de texto não suportado`, atualize sua configuração com a opção de enriquecimento `"language": "english"` para forçar todo o texto a ser interpretado como inglês, conforme mostrado no exemplo a seguir. 
[ Atualizar ](/docs/services/discovery?topic=discovery-migrate-nlu#migrate-nlu)
```json
"enrichments": [ {
     "enrichment": "alchemy_language",
     "source_field": "author.label",
     "options": {
       "extract": "taxonomy,entity,relation,doc-emotion,doc-sentiment,concept,keyword",
       "sentiment": true,
       "quotations": true,
       "language": "english"
     }
   }
 ]
```
{: codeblock}

Os erros a seguir foram corrigidos.

- Desempenho e estabilidade melhorados do serviço.

### 8 de março de 2017
{: #8mar17}

 - Otimizado o backend, incluindo a adição de novos tempos limites, para melhorar o desempenho geral.
 - Corrigido um erro que fazia com que o status de ambientes livres (dimensão `0`) relatasse um status de `pending`, independentemente do status real.
 - O único idioma nacional suportado atualmente pelo {{site.data.keyword.discoveryshort}} é inglês dos EUA (`en_US`). [ Atualizar ](/docs/services/discovery?topic=discovery-language-support#language-support)

### 3 de março de 2017
{: #3mar17}

- Incluída a tela "Meus insights de dados" no Discovery Tooling.

### 26 de fevereiro de 2017
{: #26feb17}

-     O desempenho do ambiente do {{site.data.keyword.discoverynewsshort}} foi melhorado.
-  O serviço do {{site.data.keyword.discoverynewsshort}} retorna somente 50 resultados por vez. Como uma solução alternativa, use o parâmetro `offset` em sua consulta para percorrer os resultados.
-  É possível enviar uma nova configuração com um documento individual usando o comando a seguir:

```bash
curl -X POST -u apikey:{apikey_value} -F "file=@wikipedia-sample.html" -F "configuration=$(cat config.json)" "https://gateway.watsonplatform.net/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2016-12-01"
```
{: pre}
-  Os conversores PDF e Word do serviço criam HTML como uma etapa intermediária. O serviço pode aplicar transformações e normalizações adicionais no HTML intermediário antes da transformação final ao JSON normalizado.

Os erros a seguir foram corrigidos.

-  Códigos de erro melhorados.
-  Corrigidas várias erratas de documentação.

### 16 de fevereiro de 2017
{: #16feb17}

-  Agora é possível usar seletores CSS para selecionar campos JSON nos quais é possível, então, aplicar enriquecimentos. Consulte [Usando seletores CSS para extrair campos](/docs/services/discovery?topic=discovery-configservice#using-css) para obter informações.
-  Agora é possível aumentar o tamanho de um ambiente transmitindo um novo parâmetro `size: X` para o [método update-environment](https://{DomainName}/apidocs/discovery#update-an-environment), em que `X` é um número inteiro entre 0 e 3. Consulte o [método create-environment](https://{DomainName}/apidocs/discovery#create-an-environment) para obter informações sobre os tamanhos e atributos de ambientes. [ Atualizar ](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)

    **Nota:** não é possível reduzir o tamanho de um ambiente existente. Se você deseja reduzir o tamanho de seu ambiente, entre em contato com o suporte da {{site.data.keyword.IBM}} para obter assistência.

-  Um novo operador de consulta está disponível. O operador `::!` foi incluído como um operador não igual unário. Por exemplo, agora é possível executar `query=field::!value` (não igual). Anteriormente, o único operador de exclusão era `:!` para o operador não contém (por exemplo, `query=field:!value`).

Os erros a seguir foram corrigidos.

-  Atualizações de segurança aplicadas.
-  Mensagens de status aprimoradas para alertas de procura.

### 1 de fevereiro de 2017
{: #1feb17}

As notas a seguir se aplicam especificamente à liberação do Data Crawler 1.3.0.
[ Atualizar ](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler)

-   O Data Crawler registra os valores de `document_id` usados para fazer upload de documentos e o status do upload. Os avisos de conversão não são persistidos fora do log. Atualmente não há uma ferramenta para interagir com esses dados, mas tais ferramentas devem ser desenvolvidas de modo oportuno. Os dados são acessíveis por meio do banco de dados H2, que pode ser configurado para usar um DBMS remoto.

### 16 de janeiro de 2017
{: #16jan17}

As notas a seguir se aplicam especificamente à liberação do Data Crawler 1.2.5.
[ Atualizar ](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler)

-  Opcionalmente, o Data Crawler pode pesquisar o status do documento imediatamente após o upload de um arquivo. Essa verificação faz parte do conceito do Crawler de "upload de um documento", portanto, quando essa verificação é ativada, o Crawler é praticamente incapaz de fazer upload de mais documentos simultaneamente do que o serviço do {{site.data.keyword.discoveryshort}} pode processar ao mesmo tempo para o usuário.

    Um efeito colateral do recurso `check_for_completion` é que o Crawler também pode expor para o usuário por que um documento falhou e quando ele falhou. Quaisquer avisos anexados a um documento que foi transferido por upload com sucesso, mas que falhou ao processar, são exibidos no log Crawler. Os avisos não são exportados em um arquivo processado, mas a IBM recebe com prazer uma sugestão de recurso para isso.

### 5 de janeiro de 2017
{: #5jan17}

As notas a seguir descrevem problemas que foram identificados após a liberação de GA em 15 de dezembro de 2016.

[Atualização: referência de API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery){: new_window}

-   Se você incluir um documento usando a chamada `POST /v1/environments/{environment_id}/collections/{collection_id}/documents`
    ou `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]`, a chamada retornará um ID de documento e o status **processando**. Em seguida, se você consultar o documento usando a chamada `GET /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]`, o status permanecerá em **processando** até que a ingestão seja concluída, ponto no qual o status muda para **disponível**.

    Se você **atualizar** um documento existente usando a chamada `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]`, a chamada **GET** correspondente retornará o status `available`, mesmo se o serviço ainda não tiver processado completamente o documento atualizado. O status `available` pode consultar o documento original ou o documento atualizado. A menos que a operação de atualização retorne um erro, atualmente não é possível determinar o status do documento atualizado.

    Uma solução alternativa é aguardar até 10 minutos após o envio de uma atualização de documento antes de tentar consultar o conteúdo atualizado.

### Liberação Disponibilidade Geral, 15 de dezembro de 2016
{: #15dec16}

As notas a seguir se aplicam à liberação de Disponibilidade Geral (GA) do serviço do {{site.data.keyword.discoveryfull}}.

#### Notas gerais
{: #rn-general-notes}

[ Atualizar: Incluindo conteúdo ](/docs/services/discovery?topic=discovery-addcontent#addcontent)

Veja [Referência da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery){: new_window} para a versão da API atual.

[ Atualização: Integrando com o  {{site.data.keyword.knowledgestudiofull}} ](/docs/services/discovery?topic=discovery-integrating-with-wks#integrating-with-wks).

-   Atualmente não é possível especificar o tipo de dados dos campos. Todos os campos são indexados como texto (tipo de dados **sequência**). 
-   Se você usar a API para trabalhar com o serviço, deverá especificar a versão da API com cada chamada. A versão da API atual é **2016-12-01**. 

    **Nota:** a versão específica não é aplicada na liberação GA, mas ainda deve ser listada para ativar a compatibilidade com liberações futuras.

-   É possível usar o serviço com um modelo customizado criado com o {{site.data.keyword.knowledgestudiofull}}. O modelo customizado pode ser usado para enriquecer documentos alimentados. Deve-se usar a API para integrar o modelo customizado com o serviço do {{site.data.keyword.discoveryshort}}; não é possível executar a integração usando o conjunto de ferramentas.

#### Gerenciamento de dados
{: #rn-data}

[ Atualizar ](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)

-   Os índices de procura não são criptografados.
-   As funções de backup e de restauração não são controláveis pelo usuário.

#### Ambientes
{: #rn-environments}

[ Atualizar ](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)

-   É possível criar apenas um ambiente por instância de serviço para fazer upload de seus próprios dados.
-   O serviço do {{site.data.keyword.discoveryshort}} está localizado em uma zona de disponibilidade única (sul dos EUA).
-   Os planos dedicados e Premium não estão disponíveis no momento atual.

#### Dimensionamento de ambiente
{: #rn-sizing}

[ Atualizar ](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)

-   É possível escolher um tamanho de ambiente somente ao criar um novo ambiente. A capacidade de redimensionar um ambiente não está disponível atualmente para os usuários.
-   A escolha de um tamanho de ambiente com mais RAM aumenta o desempenho.
-   Atualmente não há nenhuma recomendação prescritiva de dimensionamento disponível para casos de uso específicos.
-   O dimensionamento customizado para modelos do {{site.data.keyword.knowledgestudiofull}} não é de autoatendimento. Entre em contato com seu representante {{site.data.keyword.IBM}} para obter mais informações.

#### Limitações de ingestão
{: #rn-ingestion}

[ Atualizar ](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans)

-   A taxa de ingestão está atualmente limitada a 100 operações de ingestão de documentos simultâneas. Um aplicativo que envia documentos para o serviço para ingestão precisa respeitar os erros HTTP 429 e regular as solicitações de ingestão apropriadamente.
-   Os enriquecimentos do {{site.data.keyword.alchemylanguageshort}} são limitados aos primeiros 50 KB por campo.
-   Enriquecimentos de modelos customizados do {{site.data.keyword.knowledgestudiofull}} não são limitados, mas os documentos de divisão são limitados em chunks de 10 KB. Nenhum relacionamento é anotado entre os limites de chunk.

#### Limitações de consulta
{: #rn-query}

[ Atualizar ](/docs/services/discovery?topic=discovery-query-concepts#query-concepts)

-   Um carregamento de consulta excessivo pode fazer com que o processo de índice de procura reinicie automaticamente.
-   Os aplicativos que emitem consultas devem aplicar limites razoáveis sobre o número de consultas simultâneas.

### Problemas conhecidos
{: #rn-issues}

[Atualização: referência de API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery){: new_window}

[ Update: tooling ](/docs/services/discovery?topic=discovery-getting-started#getting-started)

[ Atualização: Data Crawler ](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler)

[ Atualização: Enriquecimentos ](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)

[ Atualizar: Incluindo conteúdo ](/docs/services/discovery?topic=discovery-addcontent#addcontent)

-   Não é possível excluir um documento usando o conjunto de ferramentas. Se você precisar excluir um documento, deverá usar o método [Excluir um documento](https://{DomainName}/apidocs/discovery#delete-a-document) da API conforme descrito na referência de API.

-   A API não suporta atualmente o recebimento de uma lista de avisos (avisos e erro) que são gerados durante a ingestão do documento. Portanto, o conjunto de ferramentas é incapaz de mostrar uma lista de avisos de ingestão e não há nenhuma maneira fácil de determinar quais documentos submetidos a crawl pelo Data Crawler falharam ao serem alimentados, se houver. 
-   As informações de status do documento nem sempre são precisas.
    -   Se uma operação de ingestão demorar mais do que o tempo limite configurado de 10 minutos, o serviço relatará que o documento não será reconhecido pelo serviço até que a operação de ingestão seja concluída. Após a operação ser concluída, o status do documento estará disponível e será preciso.
    -   Os documentos que são indexados com sucesso, mas que geraram erros, poderão ter um status **com falha** por um curto período de tempo até que o documento tenha sido totalmente confirmado no índice. Depois que o documento é confirmado no índice, o status listado é preciso.
-   Não é possível usar o conjunto de ferramentas para substituir um documento específico. Se você tentar fazer isso, o segundo documento será transferido por upload como um documento separado. Se você estiver usando a API e souber o ID do documento que deseja substituir, poderá fazer isso; consulte [Atualizar um documento](https://{DomainName}/apidocs/discovery#update-a-document) na referência de API. Se você estiver usando o Data Crawler, o upload de um documento atualizado por meio da mesma URL como um documento anterior substitui o documento original.
-   Se você estiver usando o conjunto de ferramentas para editar os enriquecimentos em sua configuração, será possível editar apenas os enriquecimentos usados para extração. Se você deseja incluir ou editar os outros enriquecimentos (por exemplo, enriquecimentos customizados de um modelo do {{site.data.keyword.knowledgestudiofull}}), deve-se usar a API. Consulte o método [Atualizar uma Configuração](https://{DomainName}/apidocs/discovery#update-a-configuration) na referência de API para obter informações.
-   As notas a seguir se aplicam especificamente ao Data Crawler. 
    -   O Data Crawler tenta fazer upload novamente se ele encontra uma falha de upload.
    -   O Data Crawler é incapaz de tentar novamente documentos que foram transferidos por upload com sucesso, mas que falharam ao serem convertidos ou indexados.
    -   O Data Crawler não possui uma função para verificar o status de recebimento de dados e de tentar refazer o upload de URLs que falharam no recebimento de dados.
    -   Não há nenhuma maneira fácil de determinar quais documentos foram alimentados pelo Data Crawler. Por exemplo, se você executar o Data Crawler com relação a um conjunto de 500 documentos, o Data Crawler poderá relatar falhas enviando 65 documentos com uma coleção total de 212 documentos. O status dos 223 documentos restantes é indeterminado.

        Uma solução alternativa está disponível, mas ela é complicada e envolve chamada da API diretamente. Entre em contato com o suporte {{site.data.keyword.IBM}} para obter assistência.
-   Os SDKs Java, Python e Node.js para o {{site.data.keyword.discoveryshort}} não oferecem toda a funcionalidade fornecida pela API de REST (cURL) padrão. Nem todos os métodos cURL possuem um método equivalente nos SDKs não cURL e nem todos os métodos não cURL fornecem todos os mesmos recursos que seus cURLs equivalentes possuem. Em outras palavras, os SDK Java, Python e Node.js fornecem atualmente apenas um subconjunto de recursos da API do cURL.
-   Se você usa o conversor Word, a correspondência nos títulos usando a chave `style` é muito mais precisa e eficiente do que usando a chave `level`.
