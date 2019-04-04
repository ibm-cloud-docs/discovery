---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-02-06"

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

# Introdução a consultas
{: #getting-started-with-querying}

Neste tutorial, aprenderemos como gravar alguns tipos diferentes de consultas no {{site.data.keyword.discoveryshort}} Query Language.
{: shortdesc}

Para obter informações sobre como criar consultas, consulte:
- [Conceitos de consulta](/docs/services/discovery?topic=discovery-query-concepts#query-concepts)
- [Referência de consulta](/docs/services/discovery?topic=discovery-query-reference#query-reference) (inclui a lista de parâmetros, de operadores e de agregados disponíveis na linguagem de consulta do {{site.data.keyword.discoveryshort}})

Essas consultas de exemplo são construídas utilizando o
conjunto de ferramentas do {{site.data.keyword.discoveryshort}}. Se desejar usar a API, inclua os parâmetros de consulta em sua chamada API. Para obter mais
informações e exemplos, consulte a seção Consultas da
[Referência da API
![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#query-your-collection){: new_window}.

Também é possível gravar consultas de linguagem natural (como "Parcerias do IBM Watson")
usando o conjunto de ferramentas do {{site.data.keyword.discoveryshort}}. Esse tutorial foca principalmente no modo
como as consultas são gravadas com o {{site.data.keyword.discoveryshort}} Query Language, já que seus
requisitos podem exigir uma consulta estruturada e os filtros e agregações devem ser gravados no
{{site.data.keyword.discoveryshort}} Query Language.
{: tip}

## Antes de Começar
{: #querying-before-you-begin}

Acesse a tela **Gerenciar dados** e crie uma nova coleção denominada {{site.data.keyword.IBM_notm}} Press Releases e inclua estes quatro documentos nela: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo"></a>

Em alguns navegadores, o link se abre em uma nova janela em vez de salvar localmente. Se isso ocorrer, selecione `Save as` no menu `File` de seu navegador para salvar uma cópia do arquivo.
{: tip}

## Etapa 1: Tour rápido do esquema de dados do Discovery
{: #querying-step1}

Vamos iniciar conhecendo o {{site.data.keyword.discoveryshort}} JSON. Para entender como construir uma consulta usando o {{site.data.keyword.discoveryshort}} Query Language, ele ajuda familiarizar-se com o JSON produzido pelo {{site.data.keyword.discoveryshort}} depois que enriquece os documentos em sua coleção.

1.  [ Ative o conjunto de ferramentas do  {{site.data.keyword.discoveryshort}}  ](/docs/services/discovery?topic=discovery-getting-started#launch-the-tooling). Na tela **Gerenciar dados**, escolha a coleção Press Release do {{site.data.keyword.IBM_notm}}.

1.  Revise os insights descobertos pelo Watson em seus documentos enriquecidos.

    -  **Análise de sentimentos** exibe a porcentagem de detalhamento de documentos identificados como positivos, neutros e negativos descobertos pelo enriquecimento Análise de sentimentos.
    -  A **Extração de entidade** exibe pessoas, lugares e organizações descobertos em seus documentos pelo enriquecimento Extração de entidade.
    -  A **Classificação de categoria** exibe as taxonomias hierárquicas descobertas em seus documentos pelo enriquecimento Classificação de categoria.
    -  **Identificação de conceito** exibe os conceitos descobertos em seus documentos pelo enriquecimento Identificação de conceito.

1.  Para familiarizar-se com o esquema de dados de seus documentos, observe a tela **Visualizar esquema de dados**. Ela exibe os campos e os valores em seus documentos transformados em duas maneiras: por documento (**Visualização de documento**) ou por campo (**Visualização de coleção**). A **Visualização de coleção** exibe todos os campos em sua coleção.

    Clique no ícone **Visualizar esquema de dados** à esquerda. Na **Visualização de coleção**, em `enriched_text`, é possível examinar os enriquecimentos aplicados à sua coleção. Clique em `categories`, `concepts`, `entities` e `sentiment` para ver como sua coleção foi enriquecida com o Watson Insights.

Se sua consulta não retornar nenhum resultado correspondente e você achar que deveria, tente trocar o campo/valor que sua consulta está utilizando para um que possa ser verificado no esquema de dados.
{: tip}    

## Etapa 2: Construir uma consulta básica
{: #querying-step2}

Vamos começar gravando uma consulta que localizará o conceito `Cloud computing` em sua coleção:

1.  Clique no ícone **Construir consultas** ![Ícone de consulta](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> para abrir a página de consulta. Selecione a coleção que contém os Press Releases da {{site.data.keyword.IBM_notm}} e clique em **Introdução**.
1.  Na tela **Construir consultas**, clique em **Procurar por documentos**, depois em **Usar o {{site.data.keyword.discoveryshort}} Query Language** e, em seguida:
    - Clique no menu suspenso **Campo** e escolha `enriched_text.concepts.text` e para o **Operador**, escolha `contains` e, em seguida, insira o **Valor** de `Cloud computing`. A consulta `enriched_text.concepts.text:Cloud computing` será exibida no **Visual Query Builder**.

    - Como alternativa, é possível clicar em **Editar na linguagem de consulta** e depois em **Usar o {{site.data.keyword.discoveryshort}} Query Language**. Insira `enriched_text.concepts.text:"Cloud computing"` no campo **Inserir consulta aqui**.

1.  Clique em **Executar consulta**. Deve haver uma correspondência (`"matching_results": 1`). Copie a **URL de consulta** na parte superior da guia **Resumo** ou **JSON** para usar em seu aplicativo.

**Bônus:** em **Mais opções**, você tem a opção para ativar a recuperação de passagem com o botão de opções **Incluir passagens relevantes**. As passagens são curtas, excertos relevantes extraídos dos documentos completos retornados pela sua consulta. Essas passagens direcionadas são extraídas dos campos `text` dos documentos em sua coleção. Consulte [Passages](/docs/services/discovery?topic=discovery-query-parameters#passages) para obter mais informações. A recuperação de passagem não está disponível para a coleção Notícias do {{site.data.keyword.discoveryshort}}.

Se desejar conferir algumas consultas pré-construídas, clique no botão **Usar uma consulta de amostra**.
{: tip}

## Etapa 3: Experimentar com diferentes consultas
{: #querying-step3}

Experimente estas consultas:

Para retornar todos os documentos que possuem uma impressão `positive`: clique em **Procurar por documentos**, **Usar o {{site.data.keyword.discoveryshort}} Query Language** e, em seguida:
-  Clique na lista suspensa **Campo** e escolha `enriched_text.sentiment.document.label` e para o **Operador**, escolha `contains` e, em seguida, insira o **Valor** de `positive`.  

   A consulta `enriched_text.sentiment.document.label:positive` será exibida no **Visual Query Builder**.

Para retornar todos os documentos na categoria `health and fitness`: clique em **Procurar por documentos**, **Usar o {{site.data.keyword.discoveryshort}} Query Language** e, em seguida:
-  Clique no menu suspenso **Campo** e escolha `enriched_text.categories.label` e para o **Operador**, escolha `is` e, em seguida, insira o **Valor** de `"health and fitness"`.

   A consulta `enriched_text.categories.label::"health and fitness"` será exibida no **Visual Query Builder**. O operador `::` especifica uma correspondência exata.

Para retornar todos os documentos que contêm a entidade `IBM`, mas não a entidade `Watson`: clique em **Procurar por documentos**, **Usar o {{site.data.keyword.discoveryshort}} Query Language** e, em seguida:
-  Clique no menu suspenso **Campo** e escolha `enriched_text.entities.text`, para o **Operador**, escolha `contains`, em seguida, insira o **Valor** de `IBM`. Clique em **Incluir regra** e, em seguida, para o **Campo**, escolha `enriched_text.entities.text` e para o **Operador**, escolha `does not contains` e, em seguida, insira o **Valor** de `Watson`.

   A consulta `enriched_text.entities.text:IBM,enriched_text.entities.text:!Watson` será exibida no **Visual Query Builder**. O operador `:!` especifica "não
contém".

## Etapa 4: Construir uma consulta combinada
{: #querying-step4}

É possível combinar parâmetros de consulta para construir mais consultas direcionadas. Vamos tentar usar os parâmetros `filter` e `query` para retornar documentos sobre aquisições da {{site.data.keyword.IBM_notm}}. O parâmetro de filtro limitará os resultados para somente os documentos que mencionam `IBM` e, em seguida, o parâmetro de consulta retornará
todos os resultados sobre `aquisições`, em ordem de relevância.

1.  Clique no ícone de construção de consultas ![Ícone de consulta](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> para abrir a página de consulta. Selecione a coleção que contém os Press Releases da {{site.data.keyword.IBM_notm}} e clique em **Introdução**.

1.  Em **Filtrar quais documentos serão consultados**:
    -  Clique no menu suspenso **Campo** e escolha `enriched_text.entities.text`, para o **Operador**, escolha `contains`, em seguida, insira o **Valor** de `IBM`.

       A consulta `enriched_text.entities.text:IBM` limitará os documentos para somente aqueles que mencionam a entidade `IBM`.

1.  Em **Procurar por documentos**, clique em **Usar o {{site.data.keyword.discoveryshort}} Query Language** e, em seguida:
    -  Clique no menu suspenso **Campo** e escolha `enriched_text.concepts.text` e para o **Operador**, escolha `contains` e, em seguida, insira o **Valor** de `world wide web`.

       A consulta `enriched_text.concepts.text: "world wide web"` retornará todos os documentos que incluem o conceito de `world wide web` e esses documentos serão classificados em ordem de relevância.

1.  Clique em **Mais opções** e, em seguida, **Campos a serem retornados** e escolha **Especificar**. Selecione `text`. Isso limitará a resposta para o texto dos artigos relevantes e exclui o restante.

1.  Clique em **Executar consulta**. Haverá um documento correspondente: `"matching_results": 1`

## Etapa 5: Construindo uma agregação
{: #querying-step5}

As agregações retornam um conjunto de valores de dados; por exemplo, palavra-chaves principais, impressão geral de entidades e mais.

Tente construir esta agregação, que retornará os 10 principais conceitos na coleção Press Release da {{site.data.keyword.IBM_notm}}.

1.  Clique no ícone **Construir consultas** ![Ícone de consulta](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> para abrir a página de consulta. Selecione a coleção que contém os Press Releases da {{site.data.keyword.IBM_notm}} e clique em **Introdução**.

1.  Em **Incluir análise de seus resultados**:
    -  Clique no menu suspenso **Saída** e escolha `Principais valores` e para o **Campo**, escolha `enriched_text.concepts.text` e, em seguida, insira a **Contagem** de `10`.

       `Term` retornará os valores mais comuns para o campo `concepts` `text`. **Contagem** especifica o número de resultados que você deseja retornar. A consulta `term(enriched_text.concepts.text,count:10)` será
exibida no **Visual Query Builder**.   

1.  Clique em **Mais opções**, em seguida, insira `0` no campo **Número de documentos a serem retornados**.

1.  Clique em **Executar consulta**. Os 10 principais conceitos serão exibidos nas guias **Resumo** e **JSON**. Aqui está um exemplo do Resumo:

## Etapa 6: Construir uma consulta no Watson Discovery News
{: #querying-step6}

O {{site.data.keyword.discoverynewsshort}} é um conjunto de dados públicos que foi previamente enriquecido com insights cognitivos. Ele é está incluído com o {{site.data.keyword.discoveryshort}}. Consulte [Watson Discovery News](/docs/services/discovery?topic=discovery-watson-discovery-news#watson-discovery-news) para obter mais informações sobre esta coleção.

Não é possível ajustar a configuração do {{site.data.keyword.discoverynewsshort}}, treinar ou incluir documentos na coleção do {{site.data.keyword.discoverynewsshort}}. Veja uma demonstração do que você pode construir com o {{site.data.keyword.discoverynewsshort}} [aqui ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://discovery-news-demo.ng.bluemix.net/){: new_window}.

A consulta de exemplo a seguir retorna os 10 principais artigos no {{site.data.keyword.discoverynewsfull}} sobre os Pittsburgh Steelers que têm uma impressão positiva.

1.  Clique no ícone **Construir consultas** ![Ícone de consulta](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> para abrir a página de consulta. Selecione a coleção {{site.data.keyword.discoverynewsshort}} e
clique em **Introdução**. (Para consultar as coleções espanholas, alemãs ou coreanas do {{site.data.keyword.discoverynewsshort}}, deve-se primeiro clicar no ícone ![Gerenciar dados](/images/icon_yourData.png), em seguida, escolher o idioma apropriado na lista suspensa.)

1.  Em **Procurar por documentos**, clique em **Usar o {{site.data.keyword.discoveryshort}} Query Language** e, em seguida:
    -  Clique no menu suspenso **Campo** e escolha `text` e para o **Operador**, escolha `contains` e, em seguida, insira o **Valor** de `Pittsburgh Steelers`. Clique em **Incluir regra**, em seguida, clique no menu suspenso **Campo** e escolha `enriched_text.sentiment.document.label` e para o **Operator**, escolha `contains` e, em seguida, insira o **Valor** de `positive.`

       A consulta `text:"Pittsburgh Steelers",enriched_text.sentiment.document.label:"positive"` será exibida no **Visual Query Builder**.

1.  Clique em **Mais opções** e, em seguida, insira `10` (esse é o padrão) no campo **Número de documentos a serem retornados**.

1.  Clique em **Executar consulta**. Os 10 principais artigos sobre o Pittsburgh Steelers com uma impressão positiva serão exibidos.

**Observação:** o número máximo de resultados retornados para uma consulta do Watson Discovery News é `50`.

Os artigos de notícias podem ser organizados em vários meios de comunicação e {{site.data.keyword.discoverynewsfull}} escolherá cada um deles, resultando em artigos duplicados. Isso significa que uma consulta ao {{site.data.keyword.discoverynewsfull}} pode retornar potencialmente vários artigos idênticos ou quase idênticos nos resultados da consulta. Para ativar a deduplicação, em **Mais opções**, escolha **Excluir resultados duplicados**. Para saber mais sobre o recurso beta, consulte [Excluindo documentos beta de resultados da consulta](/docs/services/discovery?topic=discovery-query-parameters#deduplication).
