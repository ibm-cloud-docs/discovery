---

copyright:
  years: 2015, 2017
lastupdated: "2017-12-05"

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

A relevância de resultados da consulta de linguagem natural pode ser melhorada no serviço do {{site.data.keyword.discoveryfull}} com treinamento. É possível treinar suas coleções privadas usando o conjunto de ferramentas do {{site.data.keyword.discoveryshort}} ou as APIs do {{site.data.keyword.discoveryshort}}. Consulte [Melhorando a relevância dos resultados de sua consulta com a API](/docs/services/discovery/train.html) se preferir usar as APIs.
{: shortdesc}

O treinamento de relevância é opcional; se os resultados das suas consultas atendem às suas necessidades, não é necessário treinamento adicional. Para obter uma visão geral dos casos de uso de construção, consulte a postagem do blog[Como aproveitar ao máximo o treinamento de relevância ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.ibm.com/dwblog/2017/get-relevancy-training/){: new_window}.

Para treinar o Watson, é necessário:

  -   Fornecer consultas de exemplo que representem as consultas que seus usuários inserem e 
  -   Fornecer classificação para dizer quais resultados para cada consulta são relevantes ou não 

Quando o Watson possui entrada de treinamento suficiente, as informações fornecidas sobre quais resultados são bons e ruins para cada consulta são usadas para aprender sobre sua coleção. O Watson não apenas memoriza, mas também aprende com as informações específicas sobre consultas individuais e aplica os padrões que ele detecta a todas as novas consultas. Ele faz isso com suas próprias técnicas Watson de aprendizado de máquina que localizam sinais em seu conteúdo e em suas perguntas. Após o treinamento ser aplicado, o {{site.data.keyword.discoveryshort}} reordena os resultados da consulta para exibir os resultados mais relevantes na parte superior. Conforme você inclui mais e mais dados de treinamento, o {{site.data.keyword.discoveryshort}} deve tornar-se mais preciso na ordenação dos resultados da consulta.

O treinamento deve atender aos seguintes requisitos **mínimos** para que o {{site.data.keyword.discoveryshort}} comece a aplicar suas classificações:

  - Deve-se treinar um mínimo de 49 consultas e possivelmente mais. O Watson fornecerá feedback se ele precisar de mais consultas para o treinamento.
  - É necessário aplicar ambas as classificações disponíveis aos seus resultados: `Relevant` e `Not relevant`. A classificação somente de documentos `Relevant` não fornece os dados necessários.

**Observação:** o treinamento de relevância precisa de certos requisitos de dados de treinamento antes que ele entre em vigor. O serviço verifica os dados de treinamento periodicamente para determinar se esses requisitos são atendidos e se atualiza automaticamente com base em qualquer mudança.

**Observação:** o treinamento de relevância atualmente se aplica apenas a consultas de linguagem natural em coleções particulares. Ele não se destina a ser usado com consultas estruturadas da linguagem de consulta do {{site.data.keyword.discoveryshort}}.  Para saber mais sobre a linguagem de consulta do {{site.data.keyword.discoveryshort}}, consulte [Conceitos da consulta](/docs/services/discovery/using.html).

**Observação:** há um máximo de 4 coleções treinadas por ambiente.  

## Incluindo consultas e classificando a relevância dos resultados

O treinamento consiste em três partes: uma consulta de linguagem natural, os resultados da consulta e as classificações que você aplica a esses resultados.

1.  No conjunto de ferramentas do {{site.data.keyword.discoveryshort}}, é possível acessar a página de treinamento de uma coleção na tela **Construir consultas**. Clique em **Treinar o Watson para melhorar os resultados** na parte superior direita. Não é necessário inserir uma consulta na tela **Construir consultas** para iniciar o treinamento.
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
