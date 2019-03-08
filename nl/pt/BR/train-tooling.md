---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-06"

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

# Melhorando a relevância do resultado com o conjunto de ferramentas
{: #improving-result-relevance-with-the-tooling}

A relevância de resultados da consulta de linguagem natural pode ser melhorada no serviço do {{site.data.keyword.discoveryfull}} com treinamento. É possível treinar suas coleções privadas usando o conjunto de ferramentas do {{site.data.keyword.discoveryshort}} ou as APIs do {{site.data.keyword.discoveryshort}}. Consulte [Melhorando a relevância dos resultados de sua consulta com a API](/docs/services/discovery/train.html) se preferir usar as APIs.
{: shortdesc}

O treinamento de relevância é opcional; se os resultados das suas consultas atendem às suas necessidades, não é necessário treinamento adicional. Para obter uma visão geral dos casos de uso de construção, consulte a postagem do blog[Como aproveitar ao máximo o treinamento de relevância ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.ibm.com/dwblog/2017/get-relevancy-training/){: new_window}.

Para treinar o Watson, é necessário:

  -   Fornecer consultas de exemplo que representem as consultas que seus usuários inserem e
  -   Fornecer classificação para dizer quais resultados para cada consulta são relevantes ou não

Quando o Watson possui entrada de treinamento suficiente, as informações fornecidas sobre quais resultados são bons e ruins para cada consulta são usadas para aprender sobre sua coleção. O Watson não apenas memoriza, mas também aprende com as informações específicas sobre consultas individuais e aplica os padrões que ele detecta a todas as novas consultas. Ele faz isso com suas próprias técnicas Watson de aprendizado de máquina que localizam sinais em seu conteúdo e em suas perguntas. Após o treinamento ser aplicado, o {{site.data.keyword.discoveryshort}} reordena os resultados da consulta para exibir os resultados mais relevantes na parte superior. Conforme você inclui mais e mais dados de treinamento, o {{site.data.keyword.discoveryshort}} deve tornar-se mais preciso na ordenação dos resultados da consulta.

**Observação:** o treinamento de relevância atualmente se aplica apenas a consultas de linguagem natural em coleções particulares. Ele não se destina a ser usado com consultas estruturadas da linguagem de consulta do {{site.data.keyword.discoveryshort}}. Para saber mais sobre a linguagem de consulta do {{site.data.keyword.discoveryshort}}, consulte [Conceitos da consulta](/docs/services/discovery/using.html).

Coleções treinadas retornarão uma pontuação de `confidence` no resultado de uma consulta de linguagem natural. Consulte [Pontuações de confiança](/docs/services/discovery/train-tooling.html#confidence) para obter detalhes.

Consulte [Requisitos de dados de treinamento](/docs/services/discovery/train.html#reqs) para obter os requisitos mínimos para treinamento, bem como os limites de treinamento.

Consulte [Monitoramento de uso](/docs/services/discovery/feedback.html) para obter detalhes sobre o uso de rastreamento e usando esses dados para ajudá-lo a entender e melhorar os seus aplicativos.

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

Se desejar excluir todos os dados de treinamento em sua coleção de uma vez, isso deverá ser feito por meio da API. Consulte [Excluir todos os dados de treinamento para uma coleção](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-all-training-data) para obter mais informações. Para obter mais informações sobre treinamento por meio da API, consulte [Melhorando a relevância dos seus resultados da consulta com a API](/docs/services/discovery/train.html).

## Testando e iterando na relevância dos resultados

Depois de concluir os resultados de classificação e que o Watson aplicar o treinamento, será necessário testar para ver se seus resultados da consulta melhoraram. Para isso, execute consultas de teste que estejam relacionadas (mas não idênticas) às suas consultas de treinamento. Verifique se os resultados de suas consultas de teste melhoraram.

Se desejar melhorar ainda mais os resultados após o teste, é possível:
- Incluir mais documentos em sua coleção.
- Incluir mais consultas de treinamento.
- Classificar mais resultados, certificando-se de utilizar as classificações `Relevant` e `Not relevant`.

Para obter orientação de treinamento adicional, consulte [Dicas de treinamento de relevância](/docs/services/discovery/train-tips.html#relevancy-tips).

## Pontuações de confiança
{: #confidence}

Coleções treinadas retornarão uma pontuação de `confidence` no resultado de uma consulta de linguagem natural. Este número de `confidence` é calculado com base no grau de relevância do resultado estimado, em comparação com o modelo treinado. A pontuação de `confidence` **não** é a mesma que a `score`. Para obter mais informações sobre como determinar limites para as pontuações de confiança, consulte [Como selecionar um limite para atuar usando pontuações de confianças ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.ibm.com/watson/blog/2016/06/23/how-to-select-a-threshold-for-acting-using-confidence-scores/). O `score` não deve ser usado para configurar limites absolutos, já que ele é um cálculo relativo.

A `confidence` pode variar de 0,0 a 1,0. Quanto maior o número, mais relevante é o documento.

A pontuação de `confidence` pode ser localizada nos resultados da consulta, sob o `result_metadata` para cada documento, por exemplo:

```json
    "results": [
        {
            "id": "eea16dfd5fe6139a25324e7481a32f89_13",
            "result_metadata": {
                "confidence": 0.5893963975910735,
                "score": 0.5006834
            },
```

**Nota:** o campo `confidence` será retornado somente quando o treinamento de relevância tiver sido concluído com êxito. Também pode haver casos em que o modelo treinado não está disponível e o campo `confidence` não será retornado. 

Por exemplo, o modelo treinado se tornará temporariamente inválido se novos campos de nível superior forem introduzidos ou o esquema da coleção tiver sido mudado de outra forma porque novos documentos com um esquema diferente foram alimentados. Nesse cenário, `confidence` não será retornado com os resultados e os resultados serão provenientes da procura não treinada padrão até que o modelo seja automaticamente reciclado e esteja novamente disponível. Durante a reciclagem, `confidence` não será retornado.

Os aplicativos que usam `confidence` como um limite devem assegurar que eles possam manipular esses cenários. Como a `score` é relativa à consulta, ela não é recomendada para uso como um limite fixo. Em vez disso, recomendamos que os aplicativos sempre executem o mesmo comportamento para todos os resultados que não incluem o campo `confidence`. Por exemplo, um aplicativo pode mostrar todos os resultados sem o campo `confidence` ou ocultar todos os resultados sem o campo `confidence`, mas não deve usar o valor de `score` para mostrar alguns e ocultar outros.
