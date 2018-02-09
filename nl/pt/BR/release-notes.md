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

# Notas sobre a liberação

As notas sobre a liberação fornecem informações sobre mudanças no serviço do {{site.data.keyword.discoveryfull}} desde a liberação anterior.
{: shortdesc}

## Versão da API de Serviço
{: shortdesc}

As solicitações de API requerem um parâmetro version que use uma data no formato `version=YYYY-MM-DD`. Sempre que mudamos a API de uma maneira incompatível com versões anteriores, lançamos uma nova versão secundária da API.

Envie o parâmetro version com cada solicitação de API. O serviço usa a versão da API para a data que você especificar ou a versão mais recente antes dessa data. Não padronize com a data atual. Em vez disso, especifique uma data que corresponda a uma versão que seja compatível com seu aplicativo e não a mude até que o aplicativo esteja pronto para uma versão mais recente.

A versão atual é `2017-11-07`.

## Recursos beta
{: #beta-features}

A IBM libera serviços, recursos e suporte ao idioma que são classificados como beta ou experimentais. Essas capacidades podem ser instáveis, mudar frequentemente e podem ser descontinuadas com curto prazo. Elas são fornecidas para poder avaliar sua funcionalidade. Uma capacidade beta ou experimental não fornece o mesmo nível de desempenho ou de compatibilidade que as capacidades geralmente liberadas fornecem. Essas capacidades não são projetadas para uso em um ambiente de produção e qualquer uso desse tipo é de sua responsabilidade.


## Mudanças
{: #change-log}

Os novos recursos e mudanças a seguir para o serviço estão disponíveis.

## 15 de dezembro de 2017

- Liberado o enriquecimento **Classificação de Elementos**, que analisa elementos (sentenças, listas, tabelas) em documentos de controle para classificar categorias e tipos importantes. Consulte [Classificação de elementos](/docs/services/discovery/element-classification.html) para obter mais informações. A Classificação de Elementos não está disponível para instâncias de serviço que estejam inscritas no plano **Premium**.
- Incluído suporte ao idioma básico para chinês simplificado e holandês. Consulte [Suporte ao idioma](/docs/services/discovery/language-support.html) para obter mais informações. Atualmente, as coleções em chinês simplificado e em holandês devem ser criadas com a API.
- Incluídos dois novos parâmetros para o Data Crawler: `proxy_host_port` e `read-timeout`. Consulte [Configurando o Data Crawler](/docs/services/discovery/data-crawler-discovery.html) para obter detalhes.
- Os seguintes problemas podem ser vistos ao alimentar documentos PDF:
  - Quando avisos de ingestão são consultados, o campo `file_type` para documentos PDF é retornado como `html`.
  - O campo `file_type` no objeto `extracted_metadata` de resultados para documentos PDF é configurado como `html`.
  - A API de detalhes de documento também retorna o campo `file_type` para documentos PDF como `html`.

Conjunto de ferramentas do {{site.data.keyword.discoveryshort}}:

- Incluído um gerador de consultas visual para a versão beta do {{site.data.keyword.discoveryfull}} Knowledge Graph. Consulte [Consultando Knowledge Graph usando o conjunto de ferramentas do {{site.data.keyword.discoveryshort}}](/docs/services/discovery/building-kg.html#querying-kg)

## 30 de novembro de 2017

- Liberada a versão experimental do {{site.data.keyword.discoveryfull}} Visual Insights. O Visual Insights permite explorar visualmente as conexões identificadas pelo entendimento de elementos, relações, conceitos semânticos, etc. do {{site.data.keyword.discoveryshort}}. Consulte [Visual Insights](/docs/services/discovery/visual-insights.html) para obter informações adicionais. Um comunicado explicando os recursos experimentais/beta pode ser localizado [aqui](/docs/services/discovery/release-notes.html#beta-features).
- Liberada a versão beta do {{site.data.keyword.discoveryfull}} Knowledge Graph, que fornece novos terminais para consulta de entidades e de relações em documentos. Isso inclui buscas baseadas em contexto e classificação de relevância. Este recurso beta está disponível somente para usuários do plano **Avançado**. Ele não está disponível em ambientes **Dedicados**. Consulte [{{site.data.keyword.discoveryfull}} Gráfico de conhecimento](/docs/services/discovery/building-kg.html) para obter mais informações.  Um comunicado explicando os recursos beta pode ser localizado [aqui](/docs/services/discovery/release-notes.html#beta-features).
  - Problema conhecido no {{site.data.keyword.discoveryfull}} Knowledge Graph: todos os nomes de tipo de entidade e nomes de tipo de relação são convertidos em maiúsculas durante a ingestão. Por exemplo, a entidade "GeoPoliticalEntity" é convertida em "GEOPOLITICALENTITY" e a relação "partOf" é convertida em "PARTOF."
- Liberado o [{{site.data.keyword.discoverynewsfull}}](/docs/services/discovery/watson-discovery-news.html) em dois idiomas adicionais: coreano (`collection_id`: `news-ko`) e espanhol (`collection_id`: `news-s`). O {{site.data.keyword.discoverynewsfull}} em coreano e espanhol está disponível para uso somente por meio da API; para obter informações sobre como consultar uma coleção por meio da API, consulte [Referência da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection){: new_window}. O {{site.data.keyword.discoverynewsfull}} em inglês agora possui o `collection_id` de `news-en`. Anteriormente, o `collection_id` era `news` - se você estiver usando o `collection_id` anterior, ele continuará funcionando, no entanto, será possível mudar para o novo, `collection_id` para novos projetos.
- Os resultados da consulta retornam um valor de `score`, que indica a relevância relativa entre os resultados da consulta. A partir de 30 de novembro de 2017, a maneira com que o `score` é calculado mudou. O valor de `score` deve ser usado somente para classificar documentos em uma procura única, não em procuras ou sessões. Se você tiver treinado uma coleção, um valor de `score` será retornado nos resultados de uma consulta de linguagem natural. Como o `score` indica a relevância relativa entre os resultados da consulta, ele não deve ser usado como um limite. Em vez disso, use o `confidence`, que indica a relevância do resultado quando comparado com o modelo treinado, para configurar limites. Consulte [Pontuações de confiança](/docs/services/discovery/train-tooling.html#confidence) para obter mais informações sobre configuração de limites.
- Iniciando com esta liberação, a recuperação de passagem detecta limites de sentença, que tenta retornar passagens que começam no início de uma frase e que param no término. Anteriormente, muitas passagens iniciariam ou terminariam em algum lugar no meio da sentença. Consulte [Passagens](/docs/services/discovery/query-parameters.html#passages) para obter mais informações sobre a recuperação de Passagem.

## 15 de novembro de 2017

Conjunto de ferramentas do {{site.data.keyword.discoveryshort}}:

- Incluído o enriquecimento [Extração de relação](/docs/services/discovery/building.html#relation-extraction), que inclui a opção para incorporar um modelo de relação customizado criado com o {{site.data.keyword.knowledgestudiofull}}.
- O conjunto de ferramentas {{site.data.keyword.discoveryshort}} do enriquecimento [Extração de Entidade](/docs/services/discovery/building.html#entity-extraction) agora inclui a opção para incorporar um modelo de entidade customizado criado com o {{site.data.keyword.knowledgestudiofull}}.
- A opção para criar uma coleção em japonês foi removida do conjunto do conjunto de ferramentas do {{site.data.keyword.discoveryshort}}, no entanto, a opção para criar uma coleção em japonês usando a API do {{site.data.keyword.discoveryshort}} permanece.
- O {{site.data.keyword.discoveryshort}} Tooling agora suporta ambientes organizados.

## 10 de novembro de 2017

Conjunto de ferramentas do {{site.data.keyword.discoveryshort}}:

- Incluídas opções adicionais para recuperação de Passagem no conjunto de ferramentas do {{site.data.keyword.discoveryshort}}. Durante a consulta, agora é possível especificar os campos dos quais você deseja que as passagens sejam retornadas, o número de passagens a serem retornadas e a contagem máxima de caracteres para cada passagem. Consulte [Passagens](/docs/services/discovery/query-parameters.html#passages) para obter os limites mínimos e máximos.

## 8 de novembro de 2017

A sequência de versão para todas as chamadas API mudou de `2017-10-16` para `2017-11-07`. Esta versão:
- Moveu o `score` em cada resultado da consulta para um novo objeto chamado `results_metadata`.
- Se a coleção consultada foi treinada e a consulta for uma consulta de linguagem natural, os `results_metadata` incluirão um campo `confidence` que exibe a pontuação de confiança para esse resultado. Consulte [Pontuações de confiança](/docs/services/discovery/train-tooling.html#confidence) para obter detalhes.
- Os campos que incluem espaços em branco (por exemplo: `body.additional read`) serão filtrados durante a ingestão. A descrição `notices` lerá `O campo 'leitura adicional' é inválido: espaço em branco, '.', '#' e ',' são inválidos em um nome de campo`.
- O campo `result_metadata` será filtrado durante a ingestão.

## 16 de outubro de 2017

- A sequência de versão para todas as chamadas API mudou de `2017-09-01` para `2017-10-16`. Esta versão descontinua o suporte para upload de novos documentos em coleções existentes aprimoradas com enriquecimentos do {{site.data.keyword.alchemylanguageshort}} e para a criação de novas coleções e aprimoramento delas com os enriquecimentos do {{site.data.keyword.alchemylanguageshort}}. As coleções existentes enriquecidas com o {{site.data.keyword.alchemylanguageshort}} devem ser migradas para os enriquecimentos do {{site.data.keyword.nlushort}} assim que possível. Consulte [Migrando enriquecimentos para {{site.data.keyword.nlushort}}](/docs/services/discovery/migrate-nlu.html#migrating-enrichments-to-natural-language-understanding) para obter detalhes. O conjunto de ferramentas do {{site.data.keyword.discoveryshort}} também usa a versão `2017-10-16`, consulte abaixo para obter mais informações.

Conjunto de ferramentas do {{site.data.keyword.discoveryshort}}:

- O conjunto de ferramentas do {{site.data.keyword.discoveryshort}} usa a sequência de versão da API `2017-10-16`, portanto, se você estiver usando o conjunto de ferramentas, não será mais possível fazer upload de documentos para as coleções existentes do {{site.data.keyword.alchemylanguageshort}} ou criar novas coleções aprimoradas com enriquecimentos do {{site.data.keyword.alchemylanguageshort}} após a versão `2017-10-16`.  Se você deseja continuar o uso do conjunto de ferramentas do {{site.data.keyword.discoveryshort}} para enriquecer coleções, primeiramente migre suas coleções para o {{site.data.keyword.nlushort}}. Consulte [Migrando enriquecimentos para {{site.data.keyword.nlushort}}](/docs/services/discovery/migrate-nlu.html#migrating-enrichments-to-natural-language-understanding) para obter detalhes.
- O **Data Schema Explorer** exibe consultas de amostra para vários enriquecimentos na coleção do {{site.data.keyword.discoverynewsfull}}. Agora ele também possui um link **Mostrar mais valores" que exibe valores de exemplo adicionais para esse enriquecimento no {{site.data.keyword.discoverynewsfull}}.
- Múltiplos aprimoramentos de produtividade, incluindo uma combinação de estatísticas de coleção, erros e avisos e dados de insights na tela **Gerenciar dados**.
- Uma mensagem foi incluída que exibe um alerta quando o processamento dos documentos é concluído. 

## 9 de outubro de 2017

- Uma nova métrica de agregação `unique_count` está disponível na API. Ela retorna uma contagem de instâncias exclusivas do campo especificado em uma coleção. Consulte [unique_count](/docs/services/discovery/query-aggregations.html#unique_count) para obter mais informações.

Conjunto de ferramentas do {{site.data.keyword.discoveryshort}}:

- As agregações Histograma e Fatia de tempo agora são suportadas no **Visual Query Builder**. Também há a opção para ativar a detecção de anomalias para consultas de Fatia de tempo.
- O **Data Schema Explorer** exibe consultas de amostra para o enriquecimento escolhido. Agora ele também possui um link **Mostrar mais valores" que exibe valores de exemplo adicionais para esse enriquecimento.
- Um menu de hambúrguer foi incluído para agilizar a navegação nas telas **Gerenciar dados**, **Visualizar dados do esquema** e **Construir consultas**.

### 3 de outubro de 2017

- A segmentação de documento agora está disponível. Consulte [Dividindo documentos com segmentação de documento](/docs/services/discovery/building.html#doc-segmentation).

### 29 de setembro de 2017

- {{site.data.keyword.discoveryshort}} ativado na região `Germany` em 29 de setembro de 2017. Para estar em conformidade com os regulamentos de dados da EU, os enriquecimentos de AlchemyLanguage não são suportados nesta região.
- Problema conhecido: os campos de consulta não podem conter espaços em branco.  Ao gravar uma consulta no {{site.data.keyword.discoveryshort}}, se qualquer campo de consulta contiver espaço em branco (por exemplo, `body.additional read`), você receberá um `Erro 400: sintaxe de consulta inválida`.

### 25 de setembro de 2017

- Um plano de precificação Premium agora está disponível. Para obter mais informações, consulte [Planos de precificação do {{site.data.keyword.discoveryshort}}](/docs/services/discovery/pricing-details.html).
- As capacidades de consultar, listar campos e consultar avisos entre as coleções no mesmo ambiente foram incluídas. Consulte [Consultando múltiplas coleções](/docs/services/discovery/using.html#multiple-collections) para obter detalhes.
- Informações de suporte ao idioma para o {{site.data.keyword.discoveryshort}} estão disponíveis em [Suporte ao idioma](/docs/services/discovery/language-support.html)

Conjunto de ferramentas do {{site.data.keyword.discoveryshort}}:
- O Visual Query Builder mudou do status beta para o status GA. As agregações Filtro, Fatia de tempo e Histograma não são suportadas atualmente com o Visual Query Builder. Clique em **Incluir análise de seus resultados** e depois em **Editar no Query Language** na tela **Construir consultas** para gravar essas agregações.
- Incluído o recurso beta para deduplicação em consultas do {{site.data.keyword.discoverynewsfull}}.
- Além das coleções nos idiomas inglês, alemão e espanhol, agora é possível criar coleções em árabe, francês, italiano, coreano e português do Brasil.
- Problema conhecido: o {{site.data.keyword.discoveryshort}} Tooling não suporta ambientes organizados.

### 14 de setembro de 2017

Conjunto de ferramentas do {{site.data.keyword.discoveryshort}}:

- Incluído o Data Schema Explorer, que exibe os campos e os valores em seus documentos transformados. Essas informações podem ser usadas para entender a estrutura de dados de sua coleção antes de construir consultas usando o Discovery Query Language. O esquema de dados pode ser visualizado de duas maneiras: pelo documento (visualização Documento) ou pelo campo (visualização Coleção). Para acessar o Data Schema Explorer: na tela **Meus insights de dados**, clique no botão **Visualizar esquema de dados** ou clique no ícone **Visualizar esquema de dados** à esquerda.

### 6 de setembro de 2017

- Incluída a capacidade beta para deduplicar documentos retornados de sua consulta. Esse recurso beta funciona para coleções privadas e do Watson Discovery News. Consulte [Excluindo documentos duplicados dos resultados da consulta](/docs/services/discovery/query-parameters.html#deduplication) para obter detalhes.

A deduplicação de documento é atualmente suportada somente como um recurso beta. Consulte a instrução sobre betas no topo deste documento para obter mais informações

### 31 de agosto de 2017

- A sequência de versão para todas as chamadas API mudou de `2017-08-01` para `2017-09-01`. Essa versão inclui atualizações que filtram os campos JSON inválidos a seguir durante a visualização e a ingestão, para que somente os campos JSON válidos sejam alimentados. Atualize sua sequência de versão para `2017-09-01` para evitar conflitos e possíveis erros.

   - `id`, `score` e `highlight` no nível superior (é possível continuar a incluir documentos em sua coleção usando os IDs de documento com a função `include a document`. Consulte a [Referência da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#add-doc){: new_window} para obter detalhes.
   - `_` como prefixo de nomes de campo no nível superior (como resultado, ao consultar um documento por ID, é possível consultar para `id` em vez de `_id`).
   - `#` e `,` no nome do campo
   - `+` e `-` como prefixo de nomes de campo
   - `"` `"` representando valores vazios para um nome de campo

**Nota:** se seus documentos JSON incluírem estes caracteres nos nomes de campos ou `id`, `score` e `highlight` no nível superior, será necessário removê-los antes de incluir os documentos em sua coleção ou os campos ficarão vazios. É possível criar uma configuração customizada e normalizar o JSON antes de incluir documentos em sua coleção para evitar esse problema. Consulte [Configuração customizada](/docs/services/discovery/building.html#custom-configuration).  Além disso, os documentos que incluem os caracteres de pontuação `?`, `:` ou `#` no nome do arquivo causam erros no momento da ingestão. Renomeie quaisquer documentos que incluam estes caracteres antes de alimentá-los.

- Os métodos de recuperação para `natural_language_query` foram atualizados para melhorar a relevância dos resultados correspondendo palavras com semântica relacionada. Essa atualização afeta apenas as coleções que não tiveram treinamento de relevância. Se você estiver usando `natural_language_query` e não tiver realizado o treinamento de relevância, talvez veja uma melhora na ordem dos resultados retornados.

Conjunto de ferramentas do {{site.data.keyword.discoveryshort}}:

- Mudanças no gerador de consultas para facilitar a alternância entre as opções de consulta do Discovery Query Language e do Natural Language, bem como entre a consulta, o filtro e a agregação.


### 25 de agosto de 2017

- A matriz `passages` agora inclui `field`, `start_offset` e `end_offset`. `field` é o nome do campo do qual a passagem foi extraída. `start_offset` é o caractere inicial do texto de passagem dentro do campo. `end_offset` é o caractere de finalização do texto de passagem dentro do campo.

Conjunto de ferramentas do {{site.data.keyword.discoveryshort}}: esse aprimoramento de construção de consulta pode ser localizado na tela **Construir consultas**.

-  Incluída a habilidade beta de gravar consultas no {{site.data.keyword.discoveryshort}} Query Language com um construtor visual. Clique em **Construir no modo visual** nas seções **Procurar por documentos** e **Limitar quais documentos serão consultados** para experimentar.  Conforme você constrói sua consulta visualmente, ela é exibida no **{{site.data.keyword.discoveryshort}} Query Language** abaixo dela.

   O gerador de consultas visual é atualmente suportado apenas como um recurso beta. Consulte a instrução sobre betas no topo deste documento para obter mais informações

### 18 de agosto de 2017

Conjunto de ferramentas do {{site.data.keyword.discoveryshort}}:

- Incluído suporte para agregações e condições aninhadas para o construtor de agregação visual beta introduzido em [11 de agosto de 2017](/docs/services/discovery/release-notes.html#11aug). Há um limite de 3 condições por linha de agregação.

   O construtor de agregação visual atualmente é suportado apenas como um recurso beta. Consulte a instrução sobre betas no topo deste documento para obter mais informações

### 11 de agosto de 2017
{: #11aug}

Conjunto de ferramentas do {{site.data.keyword.discoveryshort}}:

Ambos os recursos são aprimoramentos de construção de consulta e podem ser localizados na tela **Construir consultas**.

- Incluída a opção para selecionar uma consulta de um conjunto de consultas e de agregações de amostra pré-construídas. Clique em **Usar uma consulta de amostra** na parte superior direita para acessar a lista. Se você estiver consultando uma coleção de dados privados, as amostras usarão `top entities`, `categories`, etc., localizados em sua coleção. Essas consultas podem ser usadas como ponto inicial para gravação de suas próprias consultas. As consultas de amostra estão disponíveis para coleções do {{site.data.keyword.discoverynewsfull}} e privadas.

-  Incluída a capacidade beta para gravar agregações com um construtor visual. Clique em **Construir no modo visual** acima do campo **Gravar uma consulta de agregação usando o {{site.data.keyword.discoveryshort}} Query Language** para experimentar.  Conforme você constrói sua agregação visualmente, a consulta é exibida no **{{site.data.keyword.discoveryshort}} Query Language** abaixo dela.  

   O construtor de agregação visual atualmente é suportado apenas como um recurso beta. Consulte a instrução sobre betas no topo deste documento para obter mais informações

### 31 de julho de 2017

- Uma nova versão do {{site.data.keyword.discoverynewsfull}} foi liberada. A versão original foi renomeada {{site.data.keyword.discoverynewsfull}} Original e foi retirada com uma remoção da data de serviço de **15 de janeiro de 2018**. Consulte [Migrando do Watson Discovery News Original](/docs/services/discovery/migrate-bwdn.html) para obter instruções de migração.   **Nota:** se você tiver criado uma nova instância do {{site.data.keyword.discoveryshort}}, você terá acesso somente à nova versão do {{site.data.keyword.discoverynewsfull}}.

- Um novo plano de precificação para o {{site.data.keyword.discoveryfull}} foi liberado. Consulte [Planos de precificação do {{site.data.keyword.discoveryshort}}](/docs/services/discovery/pricing-details.html) para obter detalhes.

- A sequência de versão para todas as chamadas de API mudou de `2017-07-19` para `2017-08-01`. Essa versão inclui atualizações para o novo plano de precificação e a nova versão do Watson Discovery News. Atualize a sequência de versão para evitar conflitos e possíveis erros.

### 19 de julho de 2017

 - Como parte da mudança de precificação que foi anunciada para 1º de agosto de 2017, os usuários que estão atualmente no plano de **30 dias de avaliação grátis** descontinuado serão migrados automaticamente para o plano **Lite**. Como resultado dessa transição, os usuários existentes podem ter cumprido ou excedido o limite do plano Lite em documentos _(2000)_, armazenamento _(200Mb)_ ou número de coleções _(2)_. Se você exceder o limite do plano **Lite**, não poderá incluir nenhum conteúdo adicional no serviço, mas ainda poderá consultar coleções. É possível visualizar o status atual de todos esses limites usando o conjunto de ferramentas do {{site.data.keyword.discoveryshort}} ou a API. Para ser capaz de continuar incluindo conteúdo na instância do {{site.data.keyword.discoveryshort}}, deve-se fazer um dos seguintes:
   - remova coleções e/ou documentos para que os limites do plano **Lite** não seja excedido.
     Os documentos podem ser excluídos individualmente por meio da API usando o método [delete-doc](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-doc) ou coleções inteiras podem ser excluídas usando o Tooling ou a API por meio do método [delete-collection](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-collection)
   - Faça upgrade de seu plano para um nível que atenda às suas necessidades de armazenamento.
 - Os clientes com ambientes de tamanho **`1`**, **`2`** ou **`3`** serão migrados automaticamente para o plano **Avançado**.

### 17 de julho de 2017

 - Os recursos a seguir foram movidos do status beta para o status GA:

   - Treinamento de relevância
   - Consulta de linguagem natural
   - Destaque

 - Desta liberação em diante, o {{site.data.keyword.discoveryfull}} está mudando seu mecanismo de enriquecimento do {{site.data.keyword.alchemylanguageshort}} para o {{site.data.keyword.nlushort}}. Como o {{site.data.keyword.alchemylanguageshort}} está no processo de descontinuação, é necessário iniciar o uso do {{site.data.keyword.nlushort}} o mais breve possível.  Consulte [Migrando de enriquecimentos do {{site.data.keyword.alchemylanguageshort}} para enriquecimentos do {{site.data.keyword.nlushort}}](/docs/services/discovery/migrate-nlu.html) para obter detalhes.
   **Nota:** ao integrar-se com o Watson Knowledge Studio, a configuração de enriquecimento do {{site.data.keyword.alchemylanguageshort}} ainda deve ser usada. Consulte [Integrando-se com o {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery/integrate-wks.html) para obter detalhes.

 - A sequência de versão para todas as chamadas API mudou de `2017-06-25` para `2017-07-19`. Essa versão permite uma configuração padrão de NLU na criação da coleção. Você ainda deve ser capaz de enriquecer com o {{site.data.keyword.alchemylanguageshort}} em versões anteriores.

    A configuração padrão foi atualizada para usar o {{site.data.keyword.nlushort}}. É necessário atualizar a sequência de versões assim que possível para evitar conflitos e possíveis erros.

 - Conjunto de ferramentas de descoberta:

    Os Cartões de Insights para coleções aprimoradas com enriquecimentos do {{site.data.keyword.alchemylanguageshort}} não serão mais atualizados automaticamente. Deve-se migrar sua coleção para o {{site.data.keyword.nlushort}} Enrichments para que os cartões de insight sejam atualizados.

    Se você criou uma coleção antes de **18 de julho de 2017** e aplicou a **Configuração Padrão**, essa coleção foi aprimorada com enriquecimentos do {{site.data.keyword.alchemylanguageshort}}. Se você aplicar a **Configuração Padrão** a uma coleção após essa data, os enriquecimentos do {{site.data.keyword.nlushort}} serão usados (o nome da configuração alternará para **Configuração Padrão com o NLU** no conjunto de ferramentas). Como os enriquecimentos do {{site.data.keyword.alchemylanguageshort}} estão sendo descontinuados, eles não devem ser usados com novas coleções.

### 30 de junho de 2017

 -  A capacidade de normalização de entidade introduzida como um recurso beta em 5 de maio de 2017 foi movida para o status GA. Consulte [Criando uma configuração customizada para normalizar entidades](/docs/services/discovery/normalize-entities.html) para obter detalhes.

### 23 de junho de 2017

 - A sequência de versão para todas as chamadas API mudou de `2017-12-01` para `2016-06-25`. A nova sequência de versão ativará enriquecimentos em alemão (`de`) ou em espanhol (`es`) se o idioma de uma coleção estiver configurado para um desses idiomas. Anteriormente, todos os enriquecimentos eram executados em inglês, independentemente da configuração de idioma de uma coleção.

    Se você não usar enriquecimentos em idiomas diferentes do inglês, será possível continuar a usar a sequência de versão `2016-12-01`. No entanto, é necessário atualizar a sequência de versão assim que possível para evitar conflitos futuros em potencial.

 - A detecção de anomalia agora está disponível como parte das agregações de `timeslice` como um recurso GA. Consulte [Detecção de anomalias de fatia de tempo](/docs/services/discovery/query-aggregations.html#anomaly-detection) para obter detalhes.

 - Conjunto de ferramentas de descoberta:

   - Incluída a capacidade beta para melhorar a relevância dos resultados da consulta usando o Discovery Tooling (conjunto de ferramentas de relevância). Consulte [Melhorando a relevância dos seus resultados da consulta com o Discovery Tooling](/docs/services/discovery/train-tooling.html).

### 19 de junho de 2017

  - Conjunto de ferramentas de descoberta:

    - Incluída opção para especificar o idioma dos documentos em uma nova coleção, como inglês, espanhol ou alemão. Para usá-la, escolha **Selecionar o idioma dos seus documentos** no diálogo **Nomear sua nova coleção**.

    - Incluída uma guia **Resumo** na tela **Construir consultas**. A guia **Resumo** exibe uma visão geral dos resultados da consulta completos fornecidos na guia **JSON** existente. A exibição **Resumo** varia com base em sua consulta e enriquecimentos. As informações que podem ser exibidas incluem: nome ou ID do documento, estatísticas de agregação, passagens documento em ordem de relevância e resultados por enriquecimento.

    - Incluída uma opção do Natural Language Query na tela **Construir consultas** tela. Para usá-la, clique em **Fazer uma pergunta em língua simples** na seção **Procurar por documentos** e um campo aparecerá no qual é possível inserir sua pergunta. O campo de consulta original (anteriormente intitulado **Insira uma consulta ou palavra-chave**) agora pode ser acessado clicando no botão **Usar o Discovery Query Language**.

    - A tela **Construir consultas** foi reprojetada, mas todos os campos e opções permanecem. A seguir estão os nomes antigos e novos dos campos.

| **Nome do campo antigo**              | **Nome do novo campo ou seção**
|
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| Gravar e executar uma consulta                           | Procurar por documentos  |
| Limitar seus resultados da consulta (filtro)           | Limitar quais documentos serão consultados  |
| Agrupar resultados da consulta (agregação)               | Incluir análise de seus resultados  |
| Campos para exibição                                     | O nome não mudou, mas foi movido para a nova seção **Customizar opções de exibição**.                                      |
| Número de documentos a serem retornados (contagem)       | Número de documentos a serem retornados [esse campo foi movido para a seção **Customizar opções de exibição**].
|
| Incluir passagens correspondentes                        | Incluir passagens relevantes [esse campo foi movido para a seção **Customizar opções de exibição**].                        |
| Número de campos de consulta a serem ignorados no início (compensação) | Número de resultados da consulta a serem ignorados no início [esse campo foi movido para a seção **Customizar opções de exibição**]. |

### 5 de junho de 2017

 - As consultas do Watson Discovery News agora exibem apenas as primeiras 150 palavras de cada artigo nos campos JSON `text` e `alchemyapi_text`. O campo `blekko.snippet` exibe apenas a primeira sentença da matriz de fragmento.

### 30 de maio de 2017

 - O parâmetro `passages` na consulta da API foi movido do status beta para GA.

### 25 de maio de 2017

 - Discovery Tooling: o destaque do campo de consulta foi incluído nesta liberação. Este recurso inclui destaque amarelo nos nomes de campos no JSON da área de janela Resultados. Todos os campos que são consultados ou filtrados são destacados para cada resultado, mesmo se o conteúdo do campo não corresponde à consulta. Quaisquer campos usados em agregações também são destacados nos resultados da consulta, mas apenas a primeira operação de agregação é destacada.

### 10 de maio de 2017

 - Os métodos `query` e `notices` agora suportam o parâmetro `highlight`. O parâmetro é um booleano. Ao executar uma consulta e especificar `highlight` como `true`, o serviço retorna a saída que inclui um novo campo `highlight` no qual palavras que correspondem à consulta são agrupadas em tags `*` (ênfase) HTML. Consulte os [Parâmetros de consulta](/docs/services/discovery/query-parameters.html#highlight) para obter detalhes.

 - É possível concluir a exclusão de um ambiente apenas parcialmente, resultando em uma situação na qual um novo ambiente não pode ser criado, porque somente um único ambiente por instância de serviço é permitido. Se você tentar excluir e, em seguida, criar um ambiente e alguma operação estiver paralisada no estado `pending`, provavelmente você encontrou esse problema. Como uma solução alternativa, execute novamente a operação de exclusão para concluí-la e, em seguida, crie o novo ambiente.

### 8 de maio de 2017

 - Atualizado o modelo de pontuação de sinal de emoção para melhorar a precisão nos enriquecimentos de análise de emoção (`docEmotion`). O conjunto de dados de treinamento foi expandido e a engenharia de recurso foi mudada e, como resultado, o modelo possui maior precisão no conjunto dados de referência.

### 5 de maio de 2017

 - A normalização da entidade está agora disponível para uso com o serviço do Discovery que usa um modelo customizado gerado pelo Watson Knowledge Studio. A normalização da entidade insere nomes normalizados (canônicos) para referências diferentes para a mesma pessoa ou objeto no documento de origem. Consulte [Criando uma configuração customizada para normalizar entidades](/docs/services/discovery/normalize-entities.html) para obter detalhes.

     **Nota:** a normalização de entidade é suportada atualmente apenas como um recurso beta. Consulte a instrução sobre betas no topo deste documento para obter mais informações

 - O log de erro do Tooling não está mais limitado a um máximo de 8 (oito) páginas de resultados. O log de erros ainda exibe o ID do documento se o nome do documento não está disponível.

 - Os nomes de configuração são limitados a 50 caracteres e devem consistir nos caracteres `[a-zA-Z0-9-_]`.

 - O parâmetro `passages` disponível anteriormente somente por meio da API agora está disponível também por meio do Tooling.

### 25 de abril de 2017

  - O serviço agora permite que você forneça *dados de treinamento* para melhorar a precisão dos seus resultados da consulta. Ao fornecer uma instância do Discovery com dados de treinamento, o serviço usa os algoritmos avançados do Watson para determinar os resultados mais relevantes. À medida que você inclui mais dados de treinamento, a instância do serviço se torna mais precisa e sofisticada nos resultados retornados. Consulte [Melhorando a relevância dos seus resultados da consulta](/docs/services/discovery/train.html) e a [Referência da API](http://www.ibm.com/watson/developercloud/discovery/api/v1/#training-data) para obter informações.

  - A API agora suporta o parâmetro `natural_language_query` como uma liberação beta. Este parâmetro permite especificar uma consulta em linguagem natural, não na linguagem de consulta do serviço do Discovery. Consulte o método [Consulte sua coleção](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection) na referência de API para informações.

  - Atualizações de documentação e correções de erratas.

### 14 de abril de 2017

Aprimoramentos foram incluídos na API de consulta (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`). Consulte o método [Consulte sua coleção](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection) na referência de API para informações.

  - A consulta de API agora suporta o parâmetro `passages`. Se o parâmetro for configurado como `true`, a consulta retornará um conjunto de passagens mais relevantes dos documentos em sua coleção. As passagens são geradas por algoritmos Watson sofisticados para determinar as melhores passagens de texto de todos os documentos retornados pela consulta. Isso permite localizar informações e contexto com mais precisão. Consulte o método [Consulte sua coleção](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection) na referência de API para informações.

    - A especificação de `passages=true` em sua consulta pode reduzir o desempenho como resultado do aumento de processamento para extrair passagens. Em ambientes maiores, o impacto no desempenho pode ser reduzido.

    - O parâmetro `passages` é suportado apenas em coleções privadas. Ele não é suportado na coleção do Watson Discovery News.

    - O parâmetro `passages` atualmente retorna um máximo de 10 resultados. O número de resultados retornados não pode ser mudado.

    - O parâmetro `passages` retorna um máximo de 3 (três) passagens de qualquer documento especificado na coleção. Se um documento contiver mais de três passagens relevantes adicionais, o parâmetro não as retornará.

### 7 de abril de 2017

- A API de consulta (`GET /v1/environments/{environment_id}/collections/{collection_id}/query`) agora suporta o parâmetro `sort`, que permite especificar uma lista separada por vírgula de campos no documento para classificação. Consulte o método [Consulte sua coleção](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection) na referência de API para informações.
- O parâmetro `timeslice` para agregações de consulta agora manipula corretamente datas no formato de época do UNIX. Consulte [Referência de consulta](/docs/services/discovery/query-reference.html#aggregations) para obter informações sobre agregações e o parâmetro `timeslice`.
- Aprimoramentos para mensagens de erro.
- Atualizações para o SDK Java de serviço. Consulte a [Referência da API](http://www.ibm.com/watson/developercloud/discovery/api/v1/?java) para obter detalhes.
- As limitações a seguir para o uso de curingas em consultas estão agora corrigidas e funcionando corretamente:

  - Somente um curinga funcionava em qualquer consulta especificada. Por exemplo, `query-month:*ctober` funcionava, mas `query-month:*ctobe*` gerava um erro de análise.
  - Curingas não funcionavam com consultas que continham letras maiúsculas. Por exemplo, dado o par chave/campo `{"borrower": "GOVERNMENT OF INDIA"}`, `query-borrower:*ndia` retornava resultados, mas `query-borrower:*NDIA` não retornava.

**Nota:** curingas não são necessários em frases em consultas. Por exemplo, dado o par chave/campo `{"borrower": "GOVERNMENT OF TIMOR"}`, `query-borrower:"GOVERNMENT OF TIMOR"` retorna resultados, mas `query-borrower:"GOVERNMENT OF TI*OR"` não retorna. O uso de um curinga não é aplicável dentro de frases, porque todos os caracteres dentro das aspas (`"`) de uma frase são escapados.

### 24 de março de 2017

- Incluída a filtragem na tela "Meus insights de dados" no Discovery Tooling

### 15 de março de 2017

Os problemas conhecidos a seguir foram descobertos.

-  Todos os campos que são alimentados com documentos HTML, PDF e Word são digitados como **sequência**. Campos JSON e campos calculados, como pontuação de confiança, são do tipo conforme definido.
- A operação `preview` não verifica atualmente as matrizes JSON aninhadas dentro de um documento JSON enviado. Como o serviço não suporta atualmente matrizes JSON aninhadas, um documento com matrizes aninhadas pode passar com sucesso na operação `preview`, mas falha em uma tentativa de ingestão.
- Se você encontrar erros de ingestão com a mensagem `idioma de texto não suportado`, atualize sua configuração com a opção de enriquecimento `"language": "english"` para forçar todo o texto a ser interpretado como inglês, conforme mostrado no exemplo a seguir.

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

 - Otimizado o backend, incluindo a adição de novos tempos limites, para melhorar o desempenho geral.
 - Corrigido um erro que fazia com que o status de ambientes livres (dimensão `0`) relatasse um status de `pending`, independentemente do status real.
 - O único idioma nacional suportado atualmente pelo {{site.data.keyword.discoveryshort}} é inglês dos EUA (`en_US`).

### 3 de março de 2017

- Incluída a tela "Meus insights de dados" no Discovery Tooling.

### 26 de fevereiro de 2017

-     O desempenho do ambiente do {{site.data.keyword.discoverynewsshort}} foi melhorado.
-  O serviço do {{site.data.keyword.discoverynewsshort}} retorna somente 50 resultados por vez. Como uma solução alternativa, use o parâmetro `offset` em sua consulta para percorrer os resultados.
-  É possível enviar uma nova configuração com um documento individual usando o comando a seguir:

```bash
curl -X POST -u {username}:{password} -F "file=@wikipedia-sample.html" -F "configuration=$(cat config.json)" "https://gateway.watsonplatform.net/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2016-12-01"
```
{: pre}
-  Os conversores PDF e Word do serviço criam HTML como uma etapa intermediária. O serviço pode aplicar transformações e normalizações adicionais no HTML intermediário antes da transformação final ao JSON normalizado. 

Os erros a seguir foram corrigidos.

-  Códigos de erro melhorados.
-  Corrigidas várias erratas de documentação.

### 16 de fevereiro de 2017

-  Agora é possível usar seletores CSS para selecionar campos JSON nos quais é possível, então, aplicar enriquecimentos. Consulte [Usando seletores CSS para extrair campos](/docs/services/discovery/building.html#using-css) para obter informações.
-  Agora é possível aumentar o tamanho de um ambiente transmitindo um novo parâmetro `size: X` para o [método update-environment](http://www.ibm.com/watson/developercloud/discovery/api/v1/#update_environment), em que `X` é um número inteiro entre 0 e 3. Consulte o [método create-environment](http://www.ibm.com/watson/developercloud/discovery/api/v1/#create_environment) para obter informações sobre os tamanhos e atributos de ambientes.

    **Nota:** não é possível reduzir o tamanho de um ambiente existente. Se você deseja reduzir o tamanho de seu ambiente, entre em contato com o suporte da {{site.data.keyword.IBM}} para obter assistência.

-  Um novo operador de consulta está disponível. O operador `::!` foi incluído como um operador não igual unário. Por exemplo, agora é possível executar `query=field::!value` (não igual). Anteriormente, o único operador de exclusão era `:!` para o operador não contém (por exemplo, `query=field:!value`). 

Os erros a seguir foram corrigidos.

-  Atualizações de segurança aplicadas.
-  Mensagens de status aprimoradas para alertas de procura.

### 1 de fevereiro de 2017

As notas a seguir se aplicam especificamente à liberação do Data Crawler 1.3.0.

-   O Data Crawler registra os valores de `document_id` usados para fazer upload de documentos e o status do upload. Os avisos de conversão não são persistidos fora do log. Atualmente não há uma ferramenta para interagir com esses dados, mas tais ferramentas devem ser desenvolvidas de modo oportuno. Os dados são acessíveis por meio do banco de dados H2, que pode ser configurado para usar um DBMS remoto.

### 16 de janeiro de 2017

As notas a seguir se aplicam especificamente à liberação do Data Crawler 1.2.5.

-  Opcionalmente, o Data Crawler pode pesquisar o status do documento imediatamente após o upload de um arquivo. Essa verificação faz parte do conceito do Crawler de "upload de um documento", portanto, quando essa verificação é ativada, o Crawler é praticamente incapaz de fazer upload de mais documentos simultaneamente do que o serviço do {{site.data.keyword.discoveryshort}} pode processar ao mesmo tempo para o usuário.

    Um efeito colateral do recurso `check_for_completion` é que o Crawler também pode expor para o usuário por que um documento falhou e quando ele falhou. Quaisquer avisos anexados a um documento que foi transferido por upload com sucesso, mas que falhou ao processar, são exibidos no log Crawler. Os avisos não são exportados em um arquivo processado, mas a IBM recebe com prazer uma sugestão de recurso para isso.

### 5 de janeiro de 2017

As notas a seguir descrevem problemas que foram identificados após a liberação de GA em 15 de dezembro de 2016.

-   Se você incluir um documento usando a chamada `POST /v1/environments/{environment_id}/collections/{collection_id}/documents`
    ou `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]`, a chamada retornará um ID de documento e o status **processando**. Em seguida, se você consultar o documento usando a chamada `GET /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]`, o status permanecerá em **processando** até que a ingestão seja concluída, ponto no qual o status muda para **disponível**.

    Se você **atualizar** um documento existente usando a chamada `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/[:{id}]`, a chamada **GET** correspondente retornará o status `available`, mesmo se o serviço ainda não tiver processado completamente o documento atualizado. O status `available` pode consultar o documento original ou o documento atualizado. A menos que a operação de atualização retorne um erro, atualmente não é possível determinar o status do documento atualizado.

    Uma solução alternativa é aguardar até 10 minutos após o envio de uma atualização de documento antes de tentar consultar o conteúdo atualizado.
-   Não é possível fazer upload de matrizes JSON. Para fazer upload de uma matriz JSON, deve-se fazer upload de cada seção individualmente. Por exemplo, o JSON a seguir não pode ser transferido por upload para o serviço:

    ```json
    [{
      "accepted": 1, "answer": "Não deve haver nenhum problema para mantê-lo ligado o tempo todo, no entanto, deve-se considerar qualquer contador que você possa ter como o uso do código millis. Dos documentos do Arduino em milis, este número voltará a ser zero após aproximadamente 50 dias. citação de bloco - Então, para projetos que estão ativos por longos períodos de tempo, talvez um problema não seja visto imediatamente, mas algo assim pode aparecer e causar erros no caminho. ", "answerScore": "49", "authorUserId": "3", "authorUsername": "Butzke", "downModVotes": 0, "id": 2, "subtitle": "Estou criando um servidor da web Arduino simples e quero mantê-lo ligado o tempo todo. Então, ele deve aguardar para continuar trabalhando continuamente. Estou usando um Arduino Uno com uma blindagem Ethernet. Ele é alimentado com uma fonte de alimentação de saída simples 5V 1A. Minhas perguntas - Tenho problemas para deixar o Arduino ligado o tempo todo? li - Existe alguma outra placa do Arduino melhor recomendada para isso? li - Existem precauções que devo ter em relação a isso? li ul ", "tags": "<arduino-uno><web-server><ethernet>", "title": "Um Arduino é capaz de ser executado 24 horas por dia, sete dias por semana?",
      "upModVotes": 49,
      "userId": "11",
      "userReputation": 4535,
      "username": "sachleen",
      "views": 3234
    }, {
      "accepted": 0, "answer": "Além da menção de Sachleen a Milli, que afirma que qualquer calor de eletroeletrônico pode ser perturbador. Não é provável que o micro controlador em si seja um problema enorme da perspectiva do calor, mas outros componentes, como a fonte de alimentação, podem causar problemas. li - Se o código usa EEPROMWrite, o EEPROM é classificado apenas para algo em torno de 100 mil gravações. li ul ", "answerScore": "24", "authorUserId": "3", "authorUsername": "Butzke", "downModVotes": 0, "id": 3, "subtitle": "Estou criando um servidor da web Arduino simples e quero mantê-lo ligado o tempo todo. Então, ele deve aguardar para continuar trabalhando continuamente. Estou usando um Arduino Uno com uma blindagem Ethernet. Ele é alimentado com uma fonte de alimentação de saída simples 5V 1A. Minhas perguntas - Tenho problemas para deixar o Arduino ligado o tempo todo? li - Existe alguma outra placa do Arduino melhor recomendada para isso? li - Existem precauções que devo ter em relação a isso? li ul ", "tags": "<arduino-uno><web-server><ethernet>", "title": "Um Arduino é capaz de ser executado 24 horas por dia, sete dias por semana?", "upModVotes": 24, "userId": "13", "userReputation": 489, "username": "Matthew G.",
      "views": 3234
    }]
    ```
    {: codeblock}

    Para fazer upload dessas informações para o serviço, divida a matriz e faça upload de cada seção
como segue:

    Seção 1:

    ```json
    {
      "accepted": 1, "answer": "Não deve haver nenhum problema para mantê-lo ligado o tempo todo, no entanto, deve-se considerar qualquer contador que você possa ter como o uso do código millis. Dos documentos do Arduino em milis, este número voltará a ser zero após aproximadamente 50 dias. citação de bloco - Então, para projetos que estão ativos por longos períodos de tempo, talvez um problema não seja visto imediatamente, mas algo assim pode aparecer e causar erros no caminho. ", "answerScore": "49", "authorUserId": "3", "authorUsername": "Butzke", "downModVotes": 0, "id": 2, "subtitle": "Estou criando um servidor da web Arduino simples e quero mantê-lo ligado o tempo todo. Então, ele deve aguardar para continuar trabalhando continuamente. Estou usando um Arduino Uno com uma blindagem Ethernet. Ele é alimentado com uma fonte de alimentação de saída simples 5V 1A. Minhas perguntas - Tenho problemas para deixar o Arduino ligado o tempo todo? li - Existe alguma outra placa do Arduino melhor recomendada para isso? li - Existem precauções que devo ter em relação a isso? li ul ", "tags": "<arduino-uno><web-server><ethernet>", "title": "Um Arduino é capaz de ser executado 24 horas por dia, sete dias por semana?",
      "upModVotes": 49,
      "userId": "11",
      "userReputation": 4535,
      "username": "sachleen",
      "views": 3234
    }
    ```
    {: codeblock}

    Seção 2:

    ```json
    {
      "accepted": 0, "answer": "Além da menção de Sachleen a Milli, que afirma que qualquer calor de eletroeletrônico pode ser perturbador. Não é provável que o micro controlador em si seja um problema enorme da perspectiva do calor, mas outros componentes, como a fonte de alimentação, podem causar problemas. li - Se o código usa EEPROMWrite, o EEPROM é classificado apenas para algo em torno de 100 mil gravações. li ul ", "answerScore": "24", "authorUserId": "3", "authorUsername": "Butzke", "downModVotes": 0, "id": 3, "subtitle": "Estou criando um servidor da web Arduino simples e quero mantê-lo ligado o tempo todo. Então, ele deve aguardar para continuar trabalhando continuamente. Estou usando um Arduino Uno com uma blindagem Ethernet. Ele é alimentado com uma fonte de alimentação de saída simples 5V 1A. Minhas perguntas - Tenho problemas para deixar o Arduino ligado o tempo todo? li - Existe alguma outra placa do Arduino melhor recomendada para isso? li - Existem precauções que devo ter em relação a isso? li ul ", "tags": "<arduino-uno><web-server><ethernet>", "title": "Um Arduino é capaz de ser executado 24 horas por dia, sete dias por semana?", "upModVotes": 24, "userId": "13", "userReputation": 489, "username": "Matthew G.",
      "views": 3234
    }
    ```
    {: codeblock}

### Liberação Disponibilidade Geral, 15 de dezembro de 2016

As notas a seguir se aplicam à liberação de Disponibilidade Geral (GA) do serviço do {{site.data.keyword.discoveryfull}}.

#### Notas gerais

-   Atualmente não é possível especificar o tipo de dados dos campos. Todos os campos são indexados como texto (tipo de dados **sequência**).
-   Se você usar a API para trabalhar com o serviço, deverá especificar a versão da API com cada chamada. A versão da API atual é **2016-12-01**.

    **Nota:** a versão específica não é aplicada na liberação GA, mas ainda deve ser listada para ativar a compatibilidade com liberações futuras.

-   É possível usar o serviço com um modelo customizado criado com o {{site.data.keyword.knowledgestudiofull}}. O modelo customizado pode ser usado para enriquecer documentos alimentados. Deve-se usar a API para integrar o modelo customizado com o serviço do {{site.data.keyword.discoveryshort}}; não é possível executar a integração usando o conjunto de ferramentas. Consulte [Integrando-se com o {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery/integrate-wks.html "É possível integrar um modelo customizado do {{site.data.keyword.knowledgestudiofull}} ao serviço do {{site.data.keyword.discoveryshort}} para fornecer enriquecimentos customizados.") para obter detalhes.

#### Gerenciamento de dados

-   Os índices de procura não são criptografados.
-   As funções de backup e de restauração não são controláveis pelo usuário.

#### Ambientes

-   É possível criar apenas um ambiente por instância de serviço para fazer upload de seus próprios dados.
-   O serviço do {{site.data.keyword.discoveryshort}} está localizado em uma zona de disponibilidade única (sul dos EUA).
-   Os planos dedicados e Premium não estão disponíveis no momento atual.

#### Dimensionamento de ambiente

-   É possível escolher um tamanho de ambiente somente ao criar um novo ambiente. A capacidade de redimensionar um ambiente não está disponível atualmente para os usuários.
-   A escolha de um tamanho de ambiente com mais RAM aumenta o desempenho.
-   Atualmente não há nenhuma recomendação prescritiva de dimensionamento disponível para casos de uso específicos.
-   O dimensionamento customizado para modelos do {{site.data.keyword.knowledgestudiofull}} não é de autoatendimento. Entre em contato com seu representante {{site.data.keyword.IBM}} para obter mais informações.

#### Limitações de ingestão

-   A taxa de ingestão está atualmente limitada a 100 operações de ingestão de documentos simultâneas. Um aplicativo que envia documentos para o serviço para ingestão precisa respeitar os erros HTTP 429 e regular as solicitações de ingestão apropriadamente.
-   Os enriquecimentos do {{site.data.keyword.alchemylanguageshort}} são limitados aos primeiros 50 KB por campo.
-   Enriquecimentos de modelos customizados do {{site.data.keyword.knowledgestudiofull}} não são limitados, mas os documentos de divisão são limitados em chunks de 10 KB. Nenhum relacionamento é anotado entre os limites de chunk.

#### Limitações de consulta

-   Um carregamento de consulta excessivo pode fazer com que o processo de índice de procura reinicie automaticamente.
-   Os aplicativos que emitem consultas devem aplicar limites razoáveis sobre o número de consultas simultâneas.

### Problemas conhecidos

-   Não é possível excluir um documento usando o conjunto de ferramentas. Se você precisar excluir um documento, deverá usar o método [Excluir um documento](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-doc) da API conforme descrito na referência de API.

-   A API não suporta atualmente o recebimento de uma lista de avisos (avisos e erro) que são gerados durante a ingestão do documento. Portanto, o conjunto de ferramentas é incapaz de mostrar uma lista de avisos de ingestão e não há nenhuma maneira fácil de determinar quais documentos submetidos a crawl pelo Data Crawler falharam ao serem alimentados, se houver. 
-   As informações de status do documento nem sempre são precisas.
    -   Se uma operação de ingestão demorar mais do que o tempo limite configurado de 10 minutos, o serviço relatará que o documento não será reconhecido pelo serviço até que a operação de ingestão seja concluída. Após a operação ser concluída, o status do documento estará disponível e será preciso.
    -   Os documentos que são indexados com sucesso, mas que geraram erros, poderão ter um status **com falha** por um curto período de tempo até que o documento tenha sido totalmente confirmado no índice. Depois que o documento é confirmado no índice, o status listado é preciso.
-   Não é possível usar o conjunto de ferramentas para substituir um documento específico. Se você tentar fazer isso, o segundo documento será transferido por upload como um documento separado. Se você estiver usando a API e souber o ID do documento que deseja substituir, poderá fazer isso; consulte [Atualizar um documento](http://www.ibm.com/watson/developercloud/discovery/api/v1/#update-doc) na referência de API. Se você estiver usando o Data Crawler, o upload de um documento atualizado por meio da mesma URL como um documento anterior substitui o documento original.
-   Se você estiver usando o conjunto de ferramentas para editar os enriquecimentos em sua configuração, será possível editar apenas os enriquecimentos usados para extração. Se você deseja incluir ou editar os outros enriquecimentos (por exemplo, enriquecimentos customizados de um modelo do {{site.data.keyword.knowledgestudiofull}}), deve-se usar a API. Consulte o método [Atualizar uma Configuração](http://www.ibm.com/watson/developercloud/discovery/api/v1/#replace_configuration) na referência de API para obter informações.
-   As notas a seguir se aplicam especificamente ao Data Crawler.
    -   O Data Crawler tenta fazer upload novamente se ele encontra uma falha de upload.
    -   O Data Crawler é incapaz de tentar novamente documentos que foram transferidos por upload com sucesso, mas que falharam ao serem convertidos ou indexados.
    -   O Data Crawler não possui uma função para verificar o status de recebimento de dados e de tentar refazer o upload de URLs que falharam no recebimento de dados.
    -   Não há nenhuma maneira fácil de determinar quais documentos foram alimentados pelo Data Crawler. Por exemplo, se você executar o Data Crawler com relação a um conjunto de 500 documentos, o Data Crawler poderá relatar falhas enviando 65 documentos com uma coleção total de 212 documentos. O status dos 223 documentos restantes é indeterminado.

        Uma solução alternativa está disponível, mas ela é complicada e envolve chamada da API diretamente. Entre em contato com o suporte {{site.data.keyword.IBM}} para obter assistência.
-   Os SDKs Java, Python e Node.js para o {{site.data.keyword.discoveryshort}} não oferecem toda a funcionalidade fornecida pela API de REST (cURL) padrão. Nem todos os métodos cURL possuem um método equivalente nos SDKs não cURL e nem todos os métodos não cURL fornecem todos os mesmos recursos que seus cURLs equivalentes possuem. Em outras palavras, os SDK Java, Python e Node.js fornecem atualmente apenas um subconjunto de recursos da API do cURL.
-   Se você usa o conversor Word, a correspondência nos títulos usando a chave `style` é muito mais precisa e eficiente do que usando a chave `level`.
