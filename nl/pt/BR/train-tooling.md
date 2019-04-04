---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-11"

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

# Melhorando a relevância do resultado com o conjunto de ferramentas
{: #improving-result-relevance-with-the-tooling}

A relevância de resultados da consulta de linguagem natural pode ser melhorada no serviço do {{site.data.keyword.discoveryfull}} com treinamento. É possível treinar suas coleções privadas usando o conjunto de ferramentas do {{site.data.keyword.discoveryshort}} ou as APIs do {{site.data.keyword.discoveryshort}}. Consulte [Melhorando a relevância dos resultados de sua consulta com a API](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api) se preferir usar as APIs.
{: shortdesc}

O treinamento de relevância é opcional; se os resultados das suas consultas atendem às suas necessidades, não é necessário treinamento adicional. Para obter uma visão geral dos casos de uso de construção, consulte a postagem do blog[Como aproveitar ao máximo o treinamento de relevância ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.ibm.com/dwblog/2017/get-relevancy-training/){: new_window}.

Para treinar o Watson, é necessário:

  -   Fornecer consultas de exemplo que representem as consultas que seus usuários inserem e
  -   Fornecer classificação para dizer quais resultados para cada consulta são relevantes ou não

Quando o Watson possui entrada de treinamento suficiente, as informações fornecidas sobre quais resultados são bons e ruins para cada consulta são usadas para aprender sobre sua coleção. O Watson não apenas memoriza, mas também aprende com as informações específicas sobre consultas individuais e aplica os padrões que ele detecta a todas as novas consultas. Ele faz isso com suas próprias técnicas Watson de aprendizado de máquina que localizam sinais em seu conteúdo e em suas perguntas. Após o treinamento ser aplicado, o {{site.data.keyword.discoveryshort}} reordena os resultados da consulta para exibir os resultados mais relevantes na parte superior. Conforme você inclui mais e mais dados de treinamento, o {{site.data.keyword.discoveryshort}} deve tornar-se mais preciso na ordenação dos resultados da consulta.

**Observação:** o treinamento de relevância atualmente se aplica apenas a consultas de linguagem natural em coleções particulares. Ele não se destina a ser usado com consultas estruturadas da linguagem de consulta do {{site.data.keyword.discoveryshort}}. Para saber mais sobre a linguagem de consulta do {{site.data.keyword.discoveryshort}}, consulte [Conceitos da consulta](/docs/services/discovery?topic=discovery-query-concepts#query-concepts).

Todas as coleções privadas retornarão uma pontuação de `confidence` nos resultados da consulta na maioria dos casos. Consulte [Pontuações de confiança](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence) para obter detalhes.

A inclusão de uma lista de palavras vazias customizada pode melhorar a relevância dos resultados para consultas de língua natural. Consulte  [ Definindo as interrupções ](/docs/services/discovery?topic=discovery-query-concepts#stopwords)  para obter mais informações.

Consulte [Requisitos de dados de treinamento](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#reqs) para obter os requisitos mínimos para treinamento, bem como os limites de treinamento.

Consulte [Monitoramento de uso](/docs/services/discovery?topic=discovery-usage#usage) para obter detalhes sobre o uso de rastreamento e usando esses dados para ajudá-lo a entender e melhorar os seus aplicativos.

## Incluindo consultas e classificando a relevância dos resultados
{: #results}

O treinamento consiste em três partes: uma consulta de linguagem natural, os resultados da consulta e as classificações que você aplica a esses resultados.

1.  Há duas maneiras de acessar a página de treinamento no conjunto de ferramentas do {{site.data.keyword.discoveryshort}}:
    - Para uma coleção individual, na tela **Construir consultas**, clique em **Treinar o Watson para melhorar os resultados** na parte superior direita. Não é necessário inserir uma consulta na tela **Construir consultas** para iniciar o treinamento. 
    - A partir do painel Desempenho. Clique no ícone **Visualizar métricas de dados** à esquerda para abrir o painel. Você será solicitado a escolher uma coleção para treinar.
1.  Na tela **Treinar o Watson**, clique em **Incluir uma consulta de linguagem natural**, por exemplo: "IBM Watson em assistência médica" e inclua-a. Certifique-se de que suas consultas sejam gravadas na maneira com que seus usuários as perguntariam. Além disso, as consultas de treinamento devem ser gravadas com algum termo de sobreposição entre a consulta e a resposta desejada. Isso melhora os resultados iniciais quando a consulta de linguagem natural é executada. Como o treinamento de relevância usa somente consultas de linguagem natural, não insira consultas gravadas no {{site.data.keyword.discoveryshort}} Query Language.
1.  Para visualizar os resultados de sua consulta, clique no botão **Classificar resultados** ao lado dela. Se você achar que não há resultados suficientes, será possível tentar regravar a consulta ou incluir mais documentos nesta coleção por meio da tela **Gerenciar dados**.
1.  Inicie os resultados de classificação como `Relevant` ou `Not relevant`. Quando você estiver pronto, clique em **Voltar para consultas**. No conjunto de ferramentas do {{site.data.keyword.discoveryshort}}, `Relevant` possui uma pontuação de `10` e `Not relevant` possui uma pontuação de `0`. Se você já iniciou a classificação de resultados para esta coleção usando a API e está usando uma escala de pontuação diferente, um aviso será exibido, com opções para corrigir o problema.
    Na parte superior da tela, o Watson acompanha o status de treinamento para você e fornece dicas sobre o que pode ser feito para melhorar os resultados. "Inclua mais variedade em suas classificações" significa que é necessário usar as classificações `Relevant` e `Not relevant`. Quando você atende aos requisitos, o treinamento começa a atualização periodicamente. Após iniciada, a atualização leva menos de 30 minutos para ser concluída e é possível continuar trabalhando conforme o Watson atualiza.
1.  Continue incluindo resultados de consultas e de classificação.

Para retornar à tela principal **Construir consultas** a qualquer momento, clique em **Construir consultas** na parte superior esquerda.
{: tip}
Para retornar à tela **Gerenciar dados**, clique no nome da coleção na parte superior direita.
{: tip}

Se desejar excluir todos os dados de treinamento em sua coleção de uma vez, isso deverá ser feito por meio da API. Consulte [Excluir todos os dados de treinamento para uma coleção](https://{DomainName}/apidocs/discovery#delete-all-training-data) para obter mais informações. Para obter mais informações sobre treinamento por meio da API, consulte [Melhorando a relevância dos seus resultados da consulta com a API](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api).

## Testando e iterando na relevância dos resultados
{: #testing-results}

Depois de concluir os resultados de classificação e que o Watson aplicar o treinamento, será necessário testar para ver se seus resultados da consulta melhoraram. Para isso, execute consultas de teste que estejam relacionadas (mas não idênticas) às suas consultas de treinamento. Verifique se os resultados de suas consultas de teste melhoraram.

Se desejar melhorar ainda mais os resultados após o teste, é possível:
- Incluir mais documentos em sua coleção.
- Incluir mais consultas de treinamento.
- Classificar mais resultados, certificando-se de utilizar as classificações `Relevant` e `Not relevant`.

Para obter orientação de treinamento adicional, consulte [Dicas de treinamento de relevância](/docs/services/discovery?topic=discovery-relevancy-tips#relevancy-tips).

## Pontuações de confiança
{: #confidence}

O {{site.data.keyword.discoveryshort}} retorna uma pontuação de `confidence` para ambos, as consultas de língua natural e aquelas gravadas no {{site.data.keyword.discoveryshort}} Query Language.

A pontuação de `confidence` será retornada para coleções privadas treinadas e não treinadas (com a exceção de consultas somente de filtro de coleções não treinadas). Além disso, o {{site.data.keyword.discoveryshort}} retorna um campo `document_retrieval_strategy` que indica a origem da pontuação de `confidence`: 
-  ` sem treinamento `
-  ` relevancy_Training `, ou
-  ` continuous_relevancy_Training `

O `document_retrieval_strategy` pode ser usado junto com a pontuação de `confidence` para determinar como os resultados fornecidos devem ser usados. Nos casos em que o carregamento é alto, o `document_retrieval_strategy` retornado pode ser `untrained`, mesmo caso a coleção tenha sido treinada.

A `confidence` pode variar de 0,0 a 1,0. Quanto maior o número, mais relevante é o documento.

A pontuação de `confidence` pode ser localizada nos resultados da consulta em `result_metadata` para cada documento. O `document_retrieval_strategy` será listado sob o `retrieval_details`.

```json
{
  "matching_results": 4,
  "session_token": "1_2gYuWJyaWx792Ni4_DQ4C5cbnW",
  "retrieval_details" : {
    "document_retrieval_strategy" : "relevancy_training",
  },
  "results": [
    {
      "id": "eea16dfd5fe6139a25324e7481a32f89_13",
            "result_metadata": {
        "confidence": 0.5893963975910735,
        "score": 0.5006834
      }
    }
  ]
}
```
{: codeblock}

Para coleções treinadas, o número de `confidence` é calculado com base na estimativa de relevância do resultado, em comparação com o modelo treinado. As coleções treinadas calculam as pontuações de `confidence` somente para consultas de língua natural. Se você consultar uma coleção treinada usando o {{site.data.keyword.discoveryshort}} Query Language ou o modelo treinado estiver temporariamente indisponível, o número de `confidence` retornado terá um `document_retrieval_estrategy` de `untrained`. A pontuação de `confidence` para um resultado com o `document_retrieval_strategy` de `untrained` é uma estimativa não supervisionada da relevância dos resultados do documento para a consulta; ela não é intercambiável com a pontuação retornada para coleções treinadas. Uma coleção treinada pode fornecer respostas melhores para consultas de língua natural do que coleções não treinadas.

Observe que a pontuação de `confidence` **não** é a mesma que a `score`. Para obter mais informações sobre como determinar limites para as pontuações de confiança, consulte [Como selecionar um limite para atuar usando pontuações de confianças ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.ibm.com/watson/blog/2016/06/23/how-to-select-a-threshold-for-acting-using-confidence-scores/). O `score` não deve ser usado para configurar limites absolutos, já que ele é um cálculo relativo. Em vez disso, recomendamos que os aplicativos sempre executem o mesmo comportamento para todos os resultados que não incluem o campo `confidence`. Por exemplo, um aplicativo pode mostrar todos os resultados sem o campo `confidence` ou ocultar todos os resultados sem o campo `confidence`, mas não deve usar o valor de `score` para mostrar alguns e ocultar outros. Como a maneira que `confidence` é calculado varia entre os diferentes métodos de recuperação, é necessário considerar `document_retrieval_strategy` ao configurar um limite e revisar os valores antes e depois do treinamento.

Para obter mais informações sobre como consultar, consulte [Introdução à consulta](/docs/services/discovery?topic=discovery-getting-started-with-querying#getting-started-with-querying).

Para obter mais informações sobre métodos de treinamento supervisionados, consulte
-  [ Treinamento de Relevância ](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling)  e
-  [Continuous Relevancy Training](/docs/services/discovery?topic=discovery-crt#crt)
