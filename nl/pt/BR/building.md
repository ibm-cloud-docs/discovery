---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-03"

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

# Configurando seu serviço
{: #configservice}

A construção de um serviço do {{site.data.keyword.discoveryshort}} permite obter
insights úteis por enriquecer seus próprios dados e, em seguida, entregá-los em um formato de consulta.
{: shortdesc}

Antes de incluir seu próprio conteúdo no serviço do {{site.data.keyword.discoveryshort}},
é necessário configurar o serviço para processar o conteúdo da maneira que você deseja.

A primeira etapa é configurar os parâmetros básicos do serviço
([Preparando o
serviço para seus documentos](/docs/services/discovery/building.html#preparing-the-service-for-your-documents)), que inclui a criação de um ambiente e a criação de uma ou mais coleções
dentro desse ambiente. Quando uma coleção é criada, um conjunto de padrões
([A configuração padrão](/docs/services/discovery/building.html#the-default-configuration))
é fornecido automaticamente. Se você estiver satisfeito com esses padrões, será possível continuar com o
upload de seu conteúdo ([Incluindo conteúdo](/docs/services/discovery/adding-content.html)).

No entanto, você provavelmente desejará especificar uma ou mais configurações customizadas (consulte
[Quando
uma configuração customizada é necessária](/docs/services/discovery/building.html#when-you-need-a-custom-configuration)). Se esse for o caso, será necessário fazer o seguinte:

-   identifique algum conteúdo de amostra (documentos que representam seus arquivos)
-   faça upload do conteúdo
([Fazendo upload de documentos
de amostra](/docs/services/discovery/building.html#uploading-sample-documents))
-   ajuste o processo de conversão
([Convertendo documentos de
amostra](/docs/services/discovery/building.html#converting-sample-documents))
-   defina os enriquecimentos
([Incluindo
enriquecimentos](/docs/services/discovery/building.html#adding-enrichments))
-   normalize os resultados
([Normalizando dados](/docs/services/discovery/building.html#normalizing-data))

    Depois de criar a configuração customizada, é possível fazer upload de seus documentos
([Incluindo conteúdo](/docs/services/discovery/adding-content.html)).

## Preparando o serviço para seus documentos
{: #preparing-the-service-for-your-documents}

No serviço do {{site.data.keyword.discoveryshort}}, o conteúdo que você faz upload é
armazenado em uma coleção que faz parte de seu ambiente. Deve-se criar o ambiente e a coleção para poder
fazer upload de seu conteúdo.

-   **Ambiente** — o ambiente define a quantia de espaço de armazenamento que você
tem para o conteúdo no serviço do {{site.data.keyword.discoveryshort}}. Um máximo de um ambiente pode ser
criado para cada instância do serviço do {{site.data.keyword.discoveryshort}}.

    Você tem vários planos (Lite, Avançado, Premium) dentre os quais escolher, veja o [catálogo do {{site.data.keyword.discoveryshort}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window} e [Planos de precificação do {{site.data.keyword.discoveryshort}}](/docs/services/discovery/pricing-details.html) para obter detalhes. Seus arquivos de origem não contam com relação ao seu limite de tamanho do arquivo, somente o tamanho do JSON convertido que é indexado conta para o seu limite de tamanho.

-   **Coleção** - uma coleção é um agrupamento de seu conteúdo dentro do ambiente. Deve-se criar pelo menos uma coleção para poder fazer upload de seu conteúdo.

    As coleções são compostas de seus dados privados, mas
o {{site.data.keyword.discoveryshort}}
também inclui o {{site.data.keyword.discoverynewsshort}}, um conjunto de dados público previamente
enriquecido. Ele pode ser usado para consultar insights; por exemplo: alertas de notícias, detecção de
eventos e a tendência de tópicos nas notícias, que podem ser integrados em seus aplicativos.

    {{site.data.keyword.discoverynewsshort}}, um conjunto de dados públicos que foi pré-enriquecido com insights cognitivos, também está incluído com o {{site.data.keyword.discoveryshort}}. Consulte [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html#watson-discovery-news) para obter mais informações. Não é possível ajustar a configuração do {{site.data.keyword.discoverynewsshort}} nem incluir
documentos nessa coleção. Veja uma demonstração do que você pode construir com o {{site.data.keyword.discoverynewsshort}} [aqui ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://discovery-news-demo.ng.bluemix.net/){: new_window}.

Para criar um ambiente e a coleção de dados privados com o conjunto de ferramentas do
{{site.data.keyword.discoveryshort}}:

1.  Na tela **Gerenciar dados**, clique no ícone
![Cog](images/icon_settings.png) e escolha **Criar ambiente**. O
ambiente é criado com base no plano do {{site.data.keyword.Bluemix_notm}} que você selecionou anteriormente. O status de seu ambiente está sempre disponível nesta lista suspensa.

1.  Quando seu ambiente estiver pronto, clique no botão **Fazer upload de seus próprios dados** e, em seguida, é possível **Nomear sua nova coleção**.

    Por padrão, o arquivo de configuração será **Configuração padrão**. Se você
tiver outro arquivo de configuração disponível, será possível escolhê-lo ou criar um novo mais tarde e
aplicá-lo a esta coleção. Também é possível selecionar o idioma dos documentos que serão incluídos nesta coleção: inglês, alemão, espanhol, árabe, japonês, japonês, francês, italiano, coreano ou português do Brasil. Deve haver apenas
um idioma em cada uma das suas coleções. Depois de clicar em **Criar**, sua coleção de dados
aparecerá como um ladrilho.

Seu ambiente e a coleção de dados estão prontos! Se você desejar usar o arquivo de configuração padrão,
é possível iniciar com [Incluindo conteúdo](/docs/services/discovery/adding-content.html)
imediatamente. No entanto, se você deseja customizar sua configuração do {{site.data.keyword.discoveryshort}} com enriquecimentos adicionais e configurações de conversão, é necessário começar pela criação do arquivo de configuração customizado em vez de começar pela inclusão de documentos. Consulte
[Configurando o seu serviço](/docs/services/discovery/building.html#custom-configuration).

**Nota:** quando os documentos são transferidos por upload para uma coleção de dados,
eles são convertidos e enriquecidos usando o arquivo de configuração escolhido para essa coleção. Se você decidir mais tarde que deseja mudar uma coleção para um arquivo de configuração diferente, será possível fazer isso, mas os documentos que já foram transferidos por upload permanecerão convertidos pelo arquivo de configuração original. Todos os documentos transferidos por upload depois de mudar o arquivo de configuração usarão o novo arquivo de configuração. Se você deseja que a coleção **inteira** use a nova configuração, será necessário criar uma nova coleção, escolher esse novo arquivo de configuração e fazer um novo upload de todos os documentos. O serviço do {{site.data.keyword.discoveryshort}} armazena o texto convertido dos documentos que você
faz upload e as imagens integradas em arquivos **PDF** e **Microsoft Word**
não são armazenadas e não serão retornadas nos resultados.

É possível usar o conjunto de ferramentas do {{site.data.keyword.discoveryshort}} ou a API para efetuar crawl em origens de dados do Box, Salesforce e Microsoft SharePoint Online. Consulte [Conectando-se a origens de dados](/docs/services/discovery/connect.html) para obter mais informações.
{: tip}

### A configuração padrão
{: #the-default-configuration}

O serviço {{site.data.keyword.discoveryshort}} inclui uma configuração padrão converterá, enriquecerá e normalizará seus dados sem requerer que você configure manualmente essas opções.

A configuração padrão denominada **Configuração padrão** contém enriquecimentos, mais conversões de documentos padrão com base em estilos e tamanhos de fonte. O {{site.data.keyword.discoveryshort}} irá enriquecer
(incluir metadados cognitivos) o campo de texto de seus documentos com informações semânticas coletadas
por quatro enriquecimentos do {{site.data.keyword.watson}}, Extração de Entidade,
Análise de Sentimentos, Classificação de Categoria e Identificação de Conceito (aprender mais sobre eles
[aqui](/docs/services/discovery/building.html#adding-enrichments)).

-   [Conversão em Microsoft
Word](/docs/services/discovery/building.html#microsoft-word-conversion)
-   [Conversão em PDF](/docs/services/discovery/building.html#pdf-conversion)
-   [Conversão em HTML](/docs/services/discovery/building.html#html-conversion)
-   [Conversão em JSON](/docs/services/discovery/building.html#json-conversion)

Uma segunda configuração padrão denominada **Configuração de contrato padrão** está disponível no conjunto de ferramentas do {{site.data.keyword.discoveryshort}}. Ela é configurada para enriquecer com a Classificação de elementos, que pode ser usada para extrair a parte, a natureza e a categoria de elementos em PDFs. Consulte [ Classificação de Elementos ](/docs/services/discovery/element-classification.html#element-collection) para obter detalhes.

Se você deseja criar uma configuração customizada, consulte
[Configuração customizada](/docs/services/discovery/building.html#custom-configuration).

### Quando uma configuração customizada é necessária
{: #when-you-need-a-custom-configuration}

O serviço do {{site.data.keyword.discoveryshort}} tem como objetivo obter as informações
certas de seu conteúdo e retorná-las para seus usuários. A identificação de qual é a informação e de como ela é armazenada no seu conteúdo é definida pela
configuração que você usa para alimentar o conteúdo. Os tipos de conteúdo que o serviço do {{site.data.keyword.discoveryshort}} pode alimentar são
flexíveis, o que significa que mesmo que seu conteúdo não estruturado seja salvo em um formato específico, a
estrutura desse conteúdo não precisa corresponder à estrutura de outro conteúdo do mesmo tipo.

-   **Entendo que meus documentos podem não ser estruturados da maneira esperada pela
configuração padrão. *Como eu sei se as configurações padrão são as certas para mim?***
    -   A maneira mais fácil de ver se o padrão funciona para você é testá-lo por meio de
[Fazendo upload de documentos de
amostra](/docs/services/discovery/building.html#uploading-sample-documents). Se os resultados JSON de amostra atenderem às suas expectativas, então nenhuma configuração
adicional é necessária.
-   **Eu entendo que os enriquecimentos padrão são incluídos no campo de texto de meus
documentos. Posso incluir enriquecimentos adicionais em outros campos?**
    -   Sim, é possível incluir enriquecimentos adicionais em quantos campos desejar. Consulte [Incluindo enriquecimentos](/docs/services/discovery/building.html#adding-enrichments) para obter detalhes.

## Configuração customizada
{: #custom-configuration}

Para criar uma configuração customizada no conjunto de
ferramentas do {{site.data.keyword.discoveryshort}},
abra uma coleta de dados privados e, na tela **Gerenciar dados**, clique em
**Alternar** ao lado do nome de sua **Configuração**. No
diálogo **Alternar configuração**, clique em **Criar uma nova
configuração**.

Depois de nomear seu novo arquivo de configuração, esse nome será exibido na parte superior da
tela de configuração. Esse novo arquivo de configuração contém automaticamente as configurações e os
enriquecimentos do arquivo
[Configuração padrão](/docs/services/discovery/building.html#the-default-configuration) para
fornecer um local para iniciar.

As três etapas de customização de um arquivo de configuração são: **Converter**,
**Enriquecer** e **Normalizar**.

1.  [Convertendo
documentos de amostra](/docs/services/discovery/building.html#converting-sample-documents)
1.  [Incluindo
enriquecimentos](/docs/services/discovery/building.html#adding-enrichments)
1.  [Normalizando dados](/docs/services/discovery/building.html#normalizing-data)

Para obter informações detalhadas sobre configurações, veja a [Referência de configuração](/docs/services/discovery/custom-config.html).

### Fazendo upload de documentos de amostra
{: #uploading-sample-documents}

Para tornar o processo de configuração mais eficiente, é possível fazer upload até dez arquivos Microsoft
Word, HTML, JSON ou PDF que representam seu conjunto de documentos. Eles são chamados de **documentos de amostra**. Os documentos de amostra não são incluídos
em sua coleção, eles são usados apenas para identificar campos que são comuns aos seus documentos e para
customizar esses campos de acordo com seus requisitos.

Ao criar um novo arquivo de configuração no conjunto de ferramentas do
{{site.data.keyword.discoveryshort}},
é possível fazer upload de documentos de amostra por meio de arrastar e soltar ou navegar. Clique no nome do
arquivo na área de janela **Fazer upload de documentos de amostra** para visualizar cada
arquivo.

#### Lembre-se dos seguintes itens ao fazer upload de documentos de amostra:

-   Todos os seus documentos são convertidos em JSON antes de serem enriquecidos e indexados.
-   Documentos Microsoft Word e PDF são convertidos primeiramente em HTML e depois em JSON.
-   Documentos HTML são convertidos diretamente em JSON.
-   O tamanho máximo do arquivo para um documento de amostra é 1 MB. Os documentos de amostra são armazenados na pasta de dados de roaming local do navegador. Para excluir seus documentos de amostra, clique no ícone **Excluir**.

#### Diretrizes para escolha de bons documentos de amostra:

-   É necessário ter (no mínimo) um documento de amostra para cada tipo de arquivo que pretende
alimentar, Microsoft Word, PDF, HTML e JSON. (Não é possível visualizar documentos PDF enriquecidos com o enriquecimento de **Classificação de elementos**.)
-   Se você tiver quaisquer tipos de documento exclusivos (como relatórios financeiros ou press
releases), inclua cada um deles em seu conjunto de documentos de amostra.
-   Para documentos HTML, é necessário escolher documentos que incluam tags HTML que você deseja
excluir, bem como atributos de tag que você deseja incluir ou excluir.
-   Documentos JSON devem incluir quaisquer campos que deseja remover ou mesclar juntos (por
exemplo, zipCode e postalCode).

### Convertendo documentos de amostra
{: #converting-sample-documents}

A conversão de seus documentos de amostra é o processo que permite definir como cada tipo de
entrada é manipulado. O tipo de arquivo de conteúdo transferido por upload determina o número de etapas de
conversão que você terá que considerar.

Antes de iniciar, [faça
upload dos seus documentos de amostra](/docs/services/discovery/building.html#uploading-sample-documents) e abra um documento de amostra do tipo de arquivo que você deseja
configurar na área de janela à direita.

Para trabalhar com as configurações de Conversão, clique nos tipos de arquivos.

![Convertendo documento de amostra](images/convert.png)

-   **Se você estiver convertendo arquivos do Microsoft Word, deverá fazer o
seguinte:**
    -   Configure as opções de conversão do Microsoft Word
    -   Configure as opções de conversão em HTML
    -   Configure as opções de conversão em JSON
    -   Revise o resultado

-   **Se você estiver convertendo arquivos PDF, deverá fazer o seguinte:**
    -   Configure as opções de conversão em PDF
    -   Configure as opções de conversão em HTML
    -   Configure as opções de conversão em JSON
    -   Revise o resultado

-   **Se você estiver convertendo arquivos HTML, deverá fazer o seguinte:**
    -   Configure as opções de conversão em HTML
    -   Configure as opções de conversão em JSON
    -   Revise o resultado

-   **Se você estiver convertendo arquivos JSON**, deverá configurar as opções de
conversão JSON e revisar o resultado.

Para cada arquivo de configuração que você cria, há apenas um conjunto de opções de conversão para cada
etapa do processo. Isso significa que as opções de conversão HTML serão as mesmas para arquivos PDF, arquivos
do Word e arquivos HTML. Se você precisar de opções de conversão diferentes para cada tipo de conteúdo que você
está alimentando (ou se você tiver arquivos do mesmo tipo que exigirá diferentes tipos de conversão), será
necessário armazenar seus arquivos em diferentes coleções e criar arquivos de configuração separados para cada
conjunto de configurações de conversão.

#### Conversão do Microsoft Word
{: #microsoft-word-conversion}

Os tamanhos e estilos de fonte do Microsoft Word são usados para converter os títulos em seus
documentos corretamente em H1, H2 e assim por diante. Os títulos do H1 são o título do documento e os títulos
do H2 são subtítulos. Use as caixas de texto e os botões de opção para mudar as configurações padrão, se desejar. Também é possível incluir níveis de título e estilos do Word adicionais. Se os documentos do Word tendem a
usar um nome de fonte ou de estilo específico para títulos, inclua essas informações. Isso ajudará a melhorar sua conversão, o que produzirá melhores resultados de consulta.

**Exemplo:** se seus documentos do Word geralmente usam uma fonte 20 pt em itálico
para o título 2s, mude o **Intervalo de tamanho da fonte** de
**20** para **23** e o **Estilo de fonte** para
**itálico**.

Após fazer qualquer mudança, clique em **Aplicar e salvar**.

#### Conversão em PDF
{: #pdf-conversion}

Os tamanhos e os nomes de fonte em PDF são usados para converter os títulos em seus documentos
corretamente em H1, H2 e assim por diante. Os títulos H1 são o título do documento e os títulos H2 e abaixo são
subtítulos. Use as caixas de texto e os botões de opção para mudar as configurações padrão, se desejar. Também
é possível incluir níveis de título adicionais. Se seus documentos PDF tendem a usar uma fonte específica para
títulos, certifique-se de incluir essas informações. Isso ajudará a melhorar sua conversão, o que produzirá melhores resultados de consulta.

**Exemplo:** se seus documentos PDF geralmente usam uma fonte 20 pt em negrito
para títulos 1s, mude **Intervalo de tamanho da fonte** de
**20** para **80** e o **Estilo de fonte** para
**negrito**. Ajuste os outros níveis apropriadamente.

Após fazer qualquer mudança, clique em **Aplicar e salvar**.

#### Conversão em HTML
{: #html-conversion}

É possível usar esta etapa para remover tags desnecessárias e outras informações do documento para que
você retenha apenas as informações necessárias para suas consultas.

Configurações de HTML padrão:

- Excluir essas tags, bem como seu conteúdo: **`script`**,
**`sup`**
- Excluir essas tags, mas mantenha seu conteúdo: **`font`**,
**`em`**, **`span`**
- Manter esses atributos de tag: sem padrão
- Excluir esses atributos de tag: **`EVENT_ACTIONS`**
- Manter conteúdo que corresponde a esses XPaths: sem padrão
- Excluir conteúdo que corresponde a esses XPaths: sem padrão

Após fazer qualquer mudança, clique em **Aplicar e salvar**.

#### Conversão de JSON
{: #json-conversion}

A última etapa da conversão é assegurar que o documento convertido (ou JSON transferido por upload)
esteja formado da maneira que você esperava que fosse antes de os enriquecimentos serem aplicados ao
conteúdo. É possível criar regras que o {{site.data.keyword.watson}} usará para converter seu HTML em
JSON.

-   É possível mover, mesclar, copiar ou remover campos. Por exemplo: talvez você queira mesclar
**`zipCode`** e **`postalCode`**
porque são dois termos semelhantes para o mesmo campo.
-   Os campos vazios (campos que não contêm informações) serão excluídos pelo padrão. É possível mudar isso usando a alternância **Remover campos vazios**.

Após fazer qualquer mudança, clique em **Aplicar e salvar**.

## Incluindo enriquecimentos
{: #adding-enrichments}

A {{site.data.keyword.discoveryshort}}
[configuração padrão](/docs/services/discovery/building.html#the-default-configuration) irá
enriquecer (incluir metadados cognitivos) o campo `texto` de seus documentos alimentados
com informações semânticas coletados por essas quatro funções do {{site.data.keyword.watson}},
Extração de Entidade, Análise de Sentimentos, Classificação de Categoria e Identificação de Conceito. (Há um
total de nove enriquecimentos do {{site.data.keyword.watson}} disponíveis; os outros são
Extração de Palavra-chave, Extração de Relação, Análise de Emoção, Classificação de Elementos e Extração de
Função Semântica).

Alguns enriquecimentos do {{site.data.keyword.watson}} podem não estar disponíveis em determinados planos ou ambientes.

**Importante:** apenas os 50.000 primeiros caracteres de cada campo JSON selecionado
para enriquecimento serão aprimorados.

**Nota:** os enriquecimentos do {{site.data.keyword.alchemylanguageshort}} foram descontinuados em 1º de março de 2018. Se você tem quaisquer coleções existentes que estão usando os enriquecimentos do {{site.data.keyword.alchemylanguageshort}}, deve-se migrar para os enriquecimentos do {{site.data.keyword.nlushort}}. Para obter informações sobre a migração de coleções existentes e arquivos de configuração que utilizam os enriquecimentos do {{site.data.keyword.alchemylanguageshort}}, consulte [Migrando enriquecimentos para o {{site.data.keyword.nlushort}}](/docs/services/discovery/migrate-nlu.html).

Você pode aumentar ainda mais seus documentos incluindo mais enriquecimentos no campo
`text` ou enriquecer outros campos. Para fazer isso usando o conjunto de ferramentas do
{{site.data.keyword.discoveryshort}},
[crie uma configuração
customizada](/docs/services/discovery/building.html#custom-configuration), escolha um ou mais campos que deseja enriquecer e selecione na lista de
enriquecimentos do {{site.data.keyword.nlushort}} disponíveis:

### Extração de Entidade
{: #entity-extraction}

Retorna itens como pessoas, lugares e organizações presentes no texto de entrada. Extração de entidade inclui conhecimento semântico ao conteúdo para ajudar a entender o assunto e o contexto do texto que está sendo analisado. As técnicas de extração de entidade são baseadas em algoritmos estatísticos sofisticados e em tecnologia de processamento de linguagem natural e são exclusivas na indústria com seu suporte para análise multilíngue e desambiguação sensível ao contexto. Visualize a lista completa de tipos e subtipos de entidade
[aqui](/docs/services/discovery/entity-types.html). Também é possível criar e incluir um
[modelo de entidade customizado](/docs/services/discovery/building.html#custom-entity-model)
com o {{site.data.keyword.knowledgestudiofull}}.

Parte exemplo de um documento enriquecido com a Extração de entidade:

```json
{
  "text": "Os acionistas ficaram satisfeitos com o fato de a Acme Corporation planejar a construção de uma nova fábrica em Atlanta, Georgia.", "enriched_text": {
    "entities": [ {
        "count": 1, "sentiment": {
          "score": 0
        },
           "text": "Acme Corporation",
           "relevance": 0.98389,
           "type": "Company"
      },
      {
        "count": 1, "sentiment": {
          "score": 0
        },
           "text": "Atlanta",
           "relevance": 0.532754,
           "type": "Location",
           "disambiguation": {
          "subtype": [
            "AdministrativeDivision",
               "GovernmentalJurisdiction",
               "OlympicHostCity",
               "PlaceWithNeighborhoods",
               "City"
          ], "name": "Atlanta", "dbpedia_resource": "http://dbpedia.org/resource/Atlanta" }
      },
      {
        "count": 1, "sentiment": {
          "score": 0
        },
           "text": "Georgia",
           "relevance": 0.469643,
           "type": "Location",
           "disambiguation": {
          "subtype": [
            "StateOrCounty" ]
        }
      }
    ]
  }
}
```
{: codeblock}

No exemplo anterior, seria possível consultar o tipo de entidade, acessando `enriched_text.entities.type`

`sentiment` é calculado para tipos de entidade, mesmo que o enriquecimento **sentiment** não seja selecionado. Para saber mais sobre a análise de sentimentos, consulte [Análise de sentimentos](/docs/services/discovery/building.html#sentiment-analysis).

A pontuação de `relevance` é de `0.0` a `1.0`. Quanto maior a pontuação, mais relevante a entidade. O campo `desambiguation` contém as informações de desambiguação para a entidade, que inclui
as informações de `subtype` da entidade e links para um ou mais recursos, se aplicável. A `count` é o número de vezes que a entidade é mencionada no documento.

#### Usando um modelo de entidade customizado
{: #custom-entity-model}

Se você deseja criar um modelo de enriquecimento customizado, é possível fazê-lo em {{site.data.keyword.knowledgestudiofull}} e importá-lo para o {{site.data.keyword.discoveryshort}}, incluindo o ID na caixa`Custom Model ID` do conjunto de ferramentas do {{site.data.keyword.discoveryshort}}. Para obter mais informações sobre como integrar com o {{site.data.keyword.knowledgestudiofull}}, consulte [Integrando com o{{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery/integrate-wks.html#integrating-with-watson-knowledge-studio). O modelo do {{site.data.keyword.knowledgestudiofull}} customizado substituirá o enriquecimento
Extração de Entidade padrão.

**Observação:** somente um modelo do {{site.data.keyword.knowledgestudiofull}} pode ser designado a um enriquecimento.

### Extração de Relação
{: #relation-extraction}

Reconhece quando duas entidades estão relacionadas e identifica o tipo de relação. Também é possível
criar e incluir um [modelo de relação
customizado](/docs/services/discovery/building.html#custom-relation-model) com o {{site.data.keyword.knowledgestudiofull}}.

Visualize a lista completa de tipos de relacionamentos
[aqui](/docs/services/discovery/relation-types.html).

Parte exemplo de um documento enriquecido com a Extração de relação:

```json
{
  "text": "Os acionistas ficaram satisfeitos com o fato de a Acme Corporation planejar a construção de uma nova fábrica em Atlanta, Georgia.", "enriched_text": {
    "relations": [ {
        "type": "locatedAt",
        "sentence": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
        "score": 0.989245,
        "arguments": [
         {
            "text": "Atlanta",
            "location": [
             94,
             101
            ], "entities": [ {
                "type": "GeopoliticalEntity",
                "text": "Atlanta"
              }
            ]
         },
          {
            "text": "Georgia",
            "location": [
             103,
             110
            ], "entities": [ {
                "type": "GeopoliticalEntity",
                "text": "Georgia"
              }
            ]
          }
        ]
      }
    ]
  }
}
```
{: codeblock}

No exemplo anterior, é possível consultar o tipo de relação acessando
`enriched_text.relations.type`.

As entidades relacionadas são listadas nos `arguments`. Os tipos de entidade que podem
ser identificados pelo enriquecimento de Extração de Relação podem ser localizados
[aqui](/docs/services/discovery/relation-types.html#specific-entity-types).

O `score` varia de `0.0` a `1.0`. Quanto maior a
pontuação, mais relevante é a relação.

#### Usando um modelo de relação customizado
{: #custom-relation-model}

Se você deseja criar um modelo de enriquecimento customizado, é possível fazê-lo em {{site.data.keyword.knowledgestudiofull}} e importá-lo para o {{site.data.keyword.discoveryshort}}, incluindo o ID na caixa`Custom Model ID` do conjunto de ferramentas do {{site.data.keyword.discoveryshort}}. Para obter mais informações sobre como integrar com o {{site.data.keyword.knowledgestudiofull}}, consulte [Integrando com o{{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery/integrate-wks.html#integrating-with-watson-knowledge-studio). O modelo do {{site.data.keyword.knowledgestudiofull}} customizado substituirá o enriquecimento
Extração de Relação padrão.

**Observação:** somente um modelo do {{site.data.keyword.knowledgestudiofull}} pode ser designado a um enriquecimento.

### Extração de Palavra-chave
{: #keyword-extraction}

Tópicos importantes em seu conteúdo que são usados, geralmente, ao indexar dados, ao gerar nuvens de tags ou ao fazer uma procura. O serviço do {{site.data.keyword.discoveryshort}} identifica automaticamente idiomas suportados em seu conteúdo de entrada e, em seguida, identifica e classifica palavras-chave nesse conteúdo.

Parte exemplo de um documento com a Extração de palavra-chave:

```json
  {
  "text": "Os acionistas ficaram satisfeitos com o fato de a Acme Corporation planejar a construção de uma nova fábrica em Atlanta, Georgia.", "enriched_text": {
      "keywords": [
        {
          "text": "Acme Corporation",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.985203
        },
        {
          "text": "new factory",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.821033
        },
        {
          "text": "stockholders",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.66497
        },
        {
          "text": "title",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.332438
        },
        {
          "text": "Atlanta",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.307723
        },
        {
          "text": "Georgia",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.306485
        }
      ]
    }
  }
```
{: codeblock}

No exemplo anterior, seria possível consultar o texto de palavra-chave, acessando `enriched_text.keywords.text`

`sentiment` é calculado para palavras-chave, mesmo que o enriquecimento **sentiment** não seja selecionado. Para saber mais sobre a análise de sentimentos, consulte [Análise de sentimentos](/docs/services/discovery/building.html#sentiment-analysis).

A pontuação de `relevance` é de `0.0` a `1.0`. Quanto maior a pontuação, mais relevante a palavra-chave.

### Classificação de Categoria

Categoriza conteúdo de texto de entrada, HTML ou baseado na web em uma taxonomia hierárquica em até
cinco níveis de profundidade. Os níveis mais profundos permitem classificar o conteúdo em subsegmentos mais precisos e úteis. Visualize a lista completa de categorias [aqui](/docs/services/discovery/categories.html).

Exemplo de parte de um documento enriquecida com Classificação de Categoria:

```json
{
  "text": "Os acionistas ficaram satisfeitos com o fato de a Acme Corporation planejar a construção de uma nova fábrica em Atlanta, Georgia.", "enriched_text": {
      "categories": [
        {
          "score": 0.361614,
          "label": "/business and industrial"
        },
        {
          "score": 0.329377,
          "label": "/business and industrial/company/merger and acquisition"
        },
        {
          "score": 0.154254,
          "label": "/business and industrial/business operations/business plans"
        }
      ]
```
{: codeblock}

No exemplo anterior, é possível consultar o rótulo de categoria acessando
`enriched_text.categories.label`

O `label` é a categoria detectada. Os níveis de hierarquia são separados por barras. A `score` para essa categoria variará de `0.0` a `1.0`. Quanto maior a pontuação, maior a confiança nessa categoria.

### Identificação de Conceito
{: #concept-tagging}

Identifica conceitos com os quais o texto de entrada está associado, com base em outros conceitos e entidades presentes nesse texto. A identificação de conceitos compreende como os conceitos se relacionam e podem identificar conceitos que não são referenciados diretamente no texto. Por exemplo, se um artigo menciona CERN e o boson Higgs, as funções da API Concepts identificarão o Large Hadron Collider como o conceito, mesmo que o termo não seja mencionado explicitamente na página. A identificação de conceitos permite uma análise de nível superior de conteúdo de entrada do que apenas a identificação básica de palavras-chave.

Parte exemplo de um documento enriquecido com a Identificação de conceito:

```json
{
  "text": "Os acionistas ficaram satisfeitos com o fato de a Acme Corporation planejar a construção de uma nova fábrica em Atlanta, Georgia.", "enriched_text": {
      "concepts": [ {
          "text": "Acme Corporation",
          "relevance": 0.91136,
          "dbpedia_resource": "http://dbpedia.org/resource/Acme_Corporation"
        },
        {
          "text": "Factory",
          "relevance": 0.886784,
          "dbpedia_resource": "http://dbpedia.org/resource/Factory"
        }
      ]
```
{: codeblock}

No exemplo anterior, seria possível consultar o tipo de texto de conceito, acessando `enriched_text.concepts.text`

A pontuação de `relevance` é de `0.0` a `1.0`. Quanto maior a pontuação, mais relevante o conceito. Os links para os recursos são fornecidos, se aplicável.

### Extração de função de semântica

Identifica relações de assunto, de ação e de objeto dentro de sentenças no conteúdo de entrada. As informações de relação podem ser usadas para identificar automaticamente sinais de compra, eventos-chave e outras ações importantes.

Exemplo de parte de um documento enriquecida com Extração de Função de Semântica:

```json
{
  "text": "Os acionistas ficaram satisfeitos com o fato de a Acme Corporation planejar a construção de uma nova fábrica em Atlanta, Georgia.", "enriched_text": {
      "semantic_roles": [
        {
          "subject": {
            "text": "The stockholders", "keywords": [ {
                "text": "stockholders" }
            ]
          },
          "sentence": " The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
          "object": {
            "text": "pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia",
            "keywords": [
              {
                "text": "Acme Corporation"
              },
              {
                "text": "new factory"
              },
              {
                "text": "Atlanta"
              },
              {
                "text": "Georgia"
              }
            ], "entities": [ {
                "type": "Company", "text": "Acme Corporation"
              },
              {
                "type": "Location",
                "text": "Atlanta",
                "disambiguation": {
                  "subtype": [
                    "AdministrativeDivision",
                    "GovernmentalJurisdiction",
                    "OlympicHostCity",
                    "PlaceWithNeighborhoods",
                    "CityTown",
                    "City"
                  ], "name": "Atlanta", "dbpedia_resource": "http://dbpedia.org/resource/Atlanta" }
              },
              {
                "type": "Location",
                "text": "Georgia",
                "disambiguation": {
                  "subtype": [
                    "StateOrCounty" ]
                }
              }
            ]
          }, "action": {
            "verb": {
              "text": "be",
              "tense": "past"
            },
            "text": "were",
            "normalized": "be"
          }
        }
      ]
```
{: codeblock}

No exemplo anterior, seria possível consultar o texto do assunto de relação, acessando `enriched_text.relations.subject.text`

`sentiment` é calculado para relações, mesmo que o enriquecimento **sentiment** não seja relacionado. Para saber mais sobre a análise de sentimentos, consulte [Análise de sentimentos](/docs/services/discovery/building.html#sentiment-analysis). Ele não extrairá `entities` ou `keywords` (como mostrado no exemplo) a menos que você também selecione os enriquecimentos **entidade** e **palavra-chave**. Consulte [Extração de Entidade](/docs/services/discovery/building.html#entity-extraction) e
[Extração de Palavra-chave](/docs/services/discovery/building.html#keyword-extraction)
para obter mais informações sobre os enriquecimentos.

O `subject`, a `action` e o `object` são extraídos para cada sentença que contém uma relação.

### Análise de Sentimentos
{: #sentiment-analysis}

Identifica atitude, opiniões ou sentimentos no conteúdo que está sendo analisado. O serviço do {{site.data.keyword.discoveryshort}} pode calcular o sentimento geral dentro de um documento, o sentimento para objetivos especificados pelo usuário, o sentimento de nível de entidade, o sentimento de nível de cotação, o sentimento direcional e o sentimento de nível de palavra-chave. A combinação desses recursos suporta uma variedade de casos de uso que vão do monitoramento de mídia social à análise de tendências.

Parte exemplo de um documento enriquecido com a Análise de sentimentos:

```json
{
  "text": "Os acionistas ficaram satisfeitos com o fato de a Acme Corporation planejar a construção de uma nova fábrica em Atlanta, Georgia.", "enriched_text": {
      "sentiment": {
        "document": {
        "score": 0.459813,
        "label": "positive"
  }
}
```
{: codeblock}

No exemplo anterior, é possível consultar o rótulo de impressão acessando
`enriched_text.sentiment.document.label`

O `label` é a impressão geral do documento (`positive`,
`negative` ou `neutral`). A impressão `label` é baseada no
e `score`; uma pontuação de `0.0` indica que o documento é
`neutral`, um número positivo indica que o documento é `positive` e um
número negativo indica que o documento é `negative`.

### Análise de Emoção
{: #emotion-analysis}

Detecta raiva, nojo, medo, alegria e tristeza implícitas no texto em inglês. A Análise de emoção pode detectar emoções associadas a frases, entidades ou palavras-chave específicas ou pode analisar o tom emocional geral do seu conteúdo.

Parte exemplo de um documento enriquecido com a Análise de emoção:

```json
{
  "text": "Os acionistas ficaram satisfeitos com o fato de a Acme Corporation planejar a construção de uma nova fábrica em Atlanta, Georgia.", "enriched_text": {
      "emotion": {
        "document": {
          "emotion": {
          "disgust": 0.102578,
          "joy": 0.626655,
          "anger": 0.02303,
          "fear": 0.018884,
          "sadness": 0.096802
    }
  }
}
```
{: codeblock}

No exemplo anterior, é possível consultar a emoção `joy` acessando
`enriched_text.emotion.document.emotion.joy`

A Análise de emoção analisa seu texto e calcula uma pontuação para cada emoção (raiva, nojo, medo, alegria, tristeza) em uma escala de `0.0` a `1.0`. Se a pontuação de qualquer emoção for `0.5` ou superior, então essa emoção foi detectada (quanto maior a pontuação acima de `0.5`, maior a relevância). No fragmento exibido, `joy` possui uma pontuação acima de 0,5, então o {{site.data.keyword.watson}} detectou alegria.

**Nota:** a Análise de Emoção é suportada apenas em inglês.

### Classificação de Elementos
{: #elements}

Analisa documentos (sentenças, listas, tabelas) em documentos de controle para classificar tipos
e categorias importantes. Para obter mais informações, consulte
[Classificação de Elementos](/docs/services/discovery/element-classification.html).

#### Precificação de Enriquecimento
{: #enrichment-pricing}

As informações de precificação para enriquecimento estão disponíveis no
[{{site.data.keyword.Bluemix_notm}}
![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window}.

#### Suporte ao idioma para enriquecimento
{: #enrichment-language-support}

Para obter informações sobre suporte ao idioma para enriquecimento, consulte
[Suporte
ao idioma do {{site.data.keyword.discoveryshort}}](/docs/services/discovery/language-support.html).

### Entendendo a diferença entre Entidades, Conceitos e Palavras-chave
{: #udbeck}

À primeira vista, **Extração de Entidade**, **Identificação de
Conceito** e **Extração de Palavra-chave** parecem ser enriquecimentos
semelhantes. Usaremos o texto dos exemplos de enriquecimento para mostrar as diferenças entre eles.

```json
"text": "Os acionistas ficaram satisfeitos com o fato de a Acme Corporation planejar a construção de uma nova fábrica em Atlanta, Georgia."
```
{: codeblock}

Como o enriquecimento **Extração de Entidade** extrai pessoas,
lugares e organizações no texto de entrada, **Extração de Entidade** retorna os tipos de entidade a
seguir:

```json
"type": "City"
"text": "Atlanta"

"type": "Company"
"text": "Acme"

"type": "StateOrCounty"
"text": "Georgia"
```
{: codeblock}

Como o enriquecimento de **Identificação de Conceito** entende como os conceitos se
relacionam, ele pode identificar conceitos que não sejam referenciados diretamente no texto. Por exemplo, se
um artigo menciona CERN e o bóson de Higgs, ele identificará Grande Colisor de Hádrons como um conceito, mesmo
se esse termo não estiver mencionado explicitamente. Como o texto do documento de exemplo é apenas uma
sentença e não há conceitos relacionados, q **Identificação de Conceito** retorna
os conceitos a seguir:

```json
"text": "Acme Corporation"
"text": "factory"
```
{: codeblock}

Como o enriquecimento **Extração de Palavra-chave** identifica conteúdo
normalmente usado ao indexar dados, gerar nuvens de tags ou realizar procura, a **Extração de
Palavra-chave** retorna as seguintes palavras-chave:

```json
"text": "Acme Corporation"
"text": "new factory"
"text": "stockholders"
"text": "Atlanta"
"text": "Georgia"
```
{: codeblock}

Esses enriquecimentos funcionam juntos para ajudar a construir consultas melhores.

## Normalizando dados
{: #normalizing-data}

A última etapa na customização de seu arquivo de configuração é fazer uma limpeza final, também
conhecida como normalização.

Na seção **Normalizar** do conjunto de ferramentas do
{{site.data.keyword.discoveryshort}}:

-   É possível mover, mesclar, copiar ou remover campos.
-   Os campos vazios (campos que não contêm informações) serão excluídos pelo padrão. É possível mudar isso usando a alternância **Remover campos vazios**.

Após fazer quaisquer mudanças, clique em **Aplicar e salvar** e, em seguida,
**Concluído**. Você será retornado para a tela **Gerenciar dados**,
na qual é possível aplicar esta configuração à coleção de sua escolha.

**Nota:** não é possível especificar o `data type` (por exemplo: `text` ou `date`) de campos. Durante a ingestão do documento, se for detectado um campo que ainda não existe no índice, o {{site.data.keyword.discoveryshort}} detectará automaticamente o `data type` desse campo com base no valor do campo para o primeiro documento indexado.

Se estiver usando o enriquecimento de **Classificação de elementos**, não será possível executar a normalização pós-enriquecimento.

## Normalizando entidades
{: #normalizing-entities}

### Usando seletores CSS para extrair campos
{: #using-css}

É possível executar uma normalização adicional usando seletores CSS por meio da API do Discovery.

Se você estiver alimentando HTML bem formado, será possível normalizá-lo, use os seletores CSS para
extrair campos JSON dele e, em seguida, aplique os enriquecimentos nos campos extraídos. Edite seu arquivo de
configuração para ativar esse recurso. Especificamente, inclua um elemento `extracted_fields`
na hierarquia `conversions/html` e, em seguida, especifique nomes de campos, seletores CSS
e tipos de campo como segue:

```json
{
  "name": "Extract JSON config", "description": "New configuration enabling extraction of JSON fields from HTML", "conversions": {
    ...
    "html": {
      ...
      "extracted_fields": {
        "{field_name_1}": {
          "css_selector": "{CSS_selector_expression_1}", "type": "{field_type}"
        },
        ...
        "{field_name_N}": {
          "css_selector": "{CSS_selector_expression_N}", "type": "{field_type}" }
      }
    ...
    }
  }
}
```
{: codeblock}

Especifique valores para os novos campos como segue:

-   `field_name` - o nome do campo que será incluído na saída JSON.
-   `CSS_selector_expression` — o seletor CSS que deve ser executado com relação ao
HTML de entrada para extrair os campos. A expressão pode ter uma ou mais correspondências.

    Os seletores de CSS válidos são aqueles especificados pelo
[Analisador JSoup
![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://jsoup.org/apidocs/org/jsoup/select/Selector.html){: new_window} e pela sua
[sintaxe do seletor
![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://jsoup.org/cookbook/extracting-data/selector-syntax){: new_window}. Uma lista curta é fornecida em
[Seletores Comuns](/docs/services/discovery/building.html#common-selectors).
-   `field_type` — `array` ou `string`. Se o tipo de
campo não for especificado, ele será padronizado para `array`. Observe que o tipo
`string` pode ser enriquecido, mas as informações armazenadas em um `array`
não podem ser enriquecidas, a menos que os itens da matriz sejam primeiramente extraídos nos campos de texto.

**Aviso:** se um seletor CSS corresponder a um nó-pai e a um ou mais de seus
filhos, o conteúdo do texto dos nós será duplicado na saída JSON.

**Nota:** os nomes de campo devem atender às restrições definidas em
[Requisitos de nome de campo](/docs/services/discovery/custom-config.html#field_reqs).

A passagem JSON a seguir mostra a seção relevante da Configuração Padrão para na qual você inclui
informações do seletor CSS.

```json
{
  "name": "Default Configuration",
  "description": "The configuration used by default when creating a new collection without specifying a configuration_id.",
  "conversions": {
    ...
    "html": {
      "exclude_tags_completely": [
        "script", "sup"
      ], "exclude_tags_keep_content": [
        "font", "em", "span"
      ], "exclude_content": {
        "xpaths": []
      }, "keep_content": {
        "xpaths": []
      }, "exclude_tag_attributes": [
        "EVENT_ACTIONS"
      ]
    }
    ...
  }
}
```
{: codeblock}

A passagem a seguir mostra a configuração com um novo nome e descrição, bem como o local em que é
possível especificar os seletores CSS.

```json
{
  "name": "Extract JSON config", "description": "New configuration enabling extraction of JSON fields from HTML", "conversions": {
    ...
    "html": {
      "exclude_tags_completely": [
        "script", "sup"
      ], "exclude_tags_keep_content": [
        "font", "em", "span"
      ], "exclude_content": {
        "xpaths": []
      }, "keep_content": {
        "xpaths": []
      }, "exclude_tag_attributes": [
        "EVENT_ACTIONS"
      ], "extracted_fields": {
        "{field_name_1}": {
          "css_selector": "{CSS_selector_expression_1}", "type": "{field_type}"
        },
        ...
        "{field_name_N}": {
          "css_selector": "{CSS_selector_expression_N}", "type": "{field_type}" }
      }
    }
  }
  ...
}
```
{: codeblock}

Finalmente, a passagem a seguir mostra a configuração do novo nome e a descrição, assim como alguns
seletores CSS. Os seletores correspondem itens em um exemplo HTML que é descrito mais adiante nesta página.

```json
{
  "name": "Extract JSON config", "description": "New configuration enabling extraction of JSON fields from HTML", "conversions": {
    ...
    "html": {
      "exclude_tags_completely": [
        "script", "sup"
      ], "exclude_tags_keep_content": [
        "font", "em", "span"
      ], "exclude_content": {
        "xpaths": []
      }, "keep_content": {
        "xpaths": []
      }, "exclude_tag_attributes": [
        "EVENT_ACTIONS"
      ], "extracted_fields": {
        "chapters": {
          "css_selector": ".chapter",
          "type": "array"
        },
        "authors": {
          "css_selector": ".author"
        },
        "authors_str": {
          "css_selector": ".author",
          "type": "string"
        },
        "comments": {
          "css_selector": "[^comments-content]"
        }
      }
    }
  }
  ...
}
```
{: codeblock}

Se você carregar o documento HTML a seguir em uma coleção que utiliza uma configuração atualizada, os
seletores CSS corresponderão aos atributos e valores apropriados no HTML.

```html
<html>
  <body>
    <div id="authors">
      <div class="author"><span class="first_name">Jane</span> <span class="last_name">Rain</span></div>
      <div class="author">Joe Snow</div>
  </div>
  <div class="chapter"><h1>The Rain in Spain</h1><p>falls mainly on the plain.</p></div>
  <div class="chapter"><h1>How I Learned to Stop Worrying</h1><p>and love my snowblower.</p></div>
  <span id="comments-section">
    <h4>Comentários:</h4>
    <span id="comments-content-1">Rain gives me pain.</span>
    <span id="comments-content-2">All snow must go!</span>
  </span>
</body></html>
```
{: codeblock}

Após o HTML anterior ser alimentado e enriquecido, o
serviço do {{site.data.keyword.discoveryshort}} retorna o seguinte JSON:

```json
{
  "extracted_metadata": { ... },
  "html": "...",
  "text": "...",
  "extracted_fields": {
    "authors": [ "Jane Rain", "Joe Snow" ],
    "authors_str": "Jane Rain\n\nJoe Snow",
    "chapters": [ "The Rain in Spain\n\nfalls mainly on the plain.", "How I Learned to Stop Worrying\n\nand love my snowblower." ],
    "comments": [ "Rain gives me pain.", "All snow must go!" ]
  }
}
```
{: codeblock}

Depois de decidir quais elementos HTML que você deseja extrair, é possível, então, modificar adicionalmente
o arquivo de configuração para especificar os enriquecimentos que deseja aplicar a eles.

#### Seletores comuns

Alguns os seletores CSS comuns incluem o seguinte:

  - `tag` - corresponde o nome `tag`
  - `.class` - corresponde o valor de `class`
  - `#id` - corresponde o valor de `id`
  - `[attribute]` - corresponde a qualquer tag com o
`attribute` especificado, independentemente do valor
  - `[attribute=value]` ou `[attribute="value"]` — corresponde o
`attribute` e o `value` especificados

## Dividindo documentos com a segmentação de documentos
{: #doc-segmentation}

É possível dividir seus documentos Word, PDF e HTML em segmentos com base nas tags de título
HTML. Uma vez dividido, cada segmento é um documento separado que será enriquecido e indexado separadamente. Como as consultas retornarão esses segmentos como documentos separados, segmentação
de documento pode ser usada para:

  - Executar agregações em segmentos individuais de um documento. Por exemplo, sua agregação contaria
cada vez que um segmento menciona uma entidade específica, em vez de contar apenas uma vez para o documento
inteiro.
  - Executar relevância de treinamento em segmentos em vez de em documentos, que irá melhorar
a reclassificação do resultado.

Os segmentos são criados quando os documentos são convertidos em HTML (documentos Word e PDF são
convertidos em HTML antes de serem convertidos em JSON). Os documentos podem ser divididos com base nas
seguintes tags HTML: `h1` `h2` `h3` `h4`
`h5` e `h6`.

Considerações:

  - O número de segmentos por documento é limitado a `250`. Qualquer conteúdo do documento restante após `249` segmentos será armazenado no segmento `250`.

  - Cada segmento conta até o limite de documento de seu plano. O {{site.data.keyword.discoveryshort}} indexará segmentos até que o limite de plano seja atingido. Veja [Planos de precificação de descoberta](/docs/services/discovery/pricing-details.html) para obter os limites do documento.

  - Não é possível normalizar dados (consulte
[Normalizar dados](/docs/services/discovery/building.html#normalizing-data)) ou usar os
seletores CSS para extrair campos (consulte
[Usando seletores CSS para extrair campos](/docs/services/discovery/building.html#using-css))
ao usar segmentação de documento.

  - Os documentos serão segmentados cada vez que a tag HTML especificada é detectada. Consequentemente, a segmentação poderá levar a HTML malformado, já que os documentos podem ser divididos antes
das tags de fechamento e após as tags de abertura.

  - Metadados HTML, PDF e Word, assim como quaisquer metadados customizados, são extraídos e incluídos no índice com cada segmento. Cada segmento de um documento incluirá metadados idênticos.

  - A segmentação de documento não é suportada quando o enriquecimento de **Classificação de elementos** (`elements`) é especificado.

  - A nova ingestão de um documento segmentado tem considerações adicionais, veja [Atualizando um documento segmentado](/docs/services/discovery/building.html#update-seg).

### Executando segmentação
{: #performing-segmentation}

A segmentação é configurada por meio da API na seção `conversions`.

```json
{
  "configuration_id": "a23c467d-1212-4b3a-5555-93e788a3622a",
  "name": "Example configuration",
  "conversions": {
    "segment": {
      "enabled": true,
      "selector_tags": ["h1", "h2", "h3", "h4", "h5", "h6"]
    }
  }
}
```
{: codeblock}

`enabled` = `true` ativa a segmentação do documento.

`selector_tags` é uma matriz que especifica o título no qual os documentos de tags
podem ser segmentados.

#### Exemplo

Configuração:

```json
"conversions": {
  "segment": {
    "enabled": true,
    "selector_tags": ["h1", "h2"]
```
{: codeblock}

Documento HTML original:

```
<html>
 <head>
 </head>
 <body>
  primeira linha
   <div name="section 1">
    <h1>título 1</h1>
     <div name="section 2">Este é o texto que cai sob <b>Título 1</b> e que deve ser, portanto, dividido em
seu próprio segmento.
      <h2>título 2</h2>
      linha sob o título 2
     </div>
       <h3>título 3</h3>
       linha sob o título 3
   </div>
  última linha
 </body>
</html>
```
{: codeblock}

O primeiro segmento de documento será semelhante ao seguinte:

```json
{
  "id": "94c686c3-a790-4d8d-ba42-2bddf01b311c",
  "segment_metadata": {
    "parent_id": "94c686c3-a790-4d8d-ba42-2bddf01b311c",
    "segment": 1,
    "total_segments": 3
  },
  "extracted_metadata": {
    "title": "Heading 1",
    "sha1": "45ede479df67d78f2205ea7e714843375d3029c0",
    "filename": "doc-with-different-heading-levels.html",
    "file_type": "html"
  },
  "text": "This is the text that falls under heading 1 and should be therefore split into its own segment.",
  "html": "<div name=\"section 2\">This is the text that falls under <b>heading 1</b> and should be therefore split into its own segment."
}
```
{: codeblock}

Todos os segmentos incluirão um:

  - `id` - o `id` deste segmento.
  - Seção `segment_metadata` que contém:
    - `parent_id` - o `parent_id` é o ID do documento original. Para
o primeiro segmento, o `id` e o `parent_id` serão idênticos.
    - `segment` - o número deste segmento.
    - `total_segments` - o número total de segmentos em que o documento foi dividido.
  - Seção `extracted_metadata` que contém:
    - `title` - o campo `title` é extraído do conteúdo da tag
de título naquele segmento (por exemplo, `Chapter 1`). Se o primeiro segmento não incluir uma
tag de título, o `title` será `no-title`.
    - `sha1` - corresponde ao documento original.
    - `filename` - corresponde ao documento original.
    - `file_type`- corresponde ao documento original.
  - Campo `text`
  - Campo `html`

### Atualizando um documento segmentado
{: #update-seg}

Se um documento segmentado tiver sido atualizado e precisar ser alimentado novamente, ele poderá ser substituído usando o método [Atualizar documento ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#update-doc){: new_window}.

Ao atualizar um documento segmentado, o documento deve ser transferido por upload usando o método POST da API `/environments/{environment_id}/collections/{collection_id}/documents/{document_id}`, especificando os conteúdos do campo `parent_id` de um dos segmentos atuais como a variável de caminho `{document_id}`.

Ao atualizar, todos os segmentos serão sobrescritos, a menos que a versão atualizada do documento tenha menos seções totais do que o original. Esses segmentos mais antigos permanecerão no índice e poderão ser excluídos individualmente usando a API. Consulte a [Referência da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-doc){: new_window} para obter detalhes. É possível identificar quantos segmentos foram criados consultando os `notices`. A cada segmento é fornecido um campo `document_id` que é composto por um `{parent_id}`, seguido por um sublinhado, seguido pelo número do segmento.

Se qualquer um dos segmentos do documento que você pretende atualizar foi classificado para treinamento de relevância, deve-se primeiro excluir todos os segmentos desse documento e, em seguida, alimentar o documento atualizado como um novo documento. Isso resultará em um novo `document_id` para cada segmento e todos os segmentos treinados precisarão ser reciclados. O índice treinado se tornará inexato se você não excluir o conteúdo antigo primeiro.

Como alternativa, considere a criação de um novo documento que contenha somente o novo conteúdo e alimente-o separadamente.
