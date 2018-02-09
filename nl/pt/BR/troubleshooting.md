---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-18"

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

# Resolução de problemas

Dicas de resolução de problemas para uso do serviço do {{site.data.keyword.discoveryshort}}.

Se você encontrar problemas ao usar o serviço do {{site.data.keyword.discoveryshort}},
tente uma ou mais das seguintes dicas de resolução de problemas.

-   Um documento pode falhar ao ser alimentado devido a uma incompatibilidade de tipo
entre os dados no documento atual e os dados semelhantes em um documento alimentado anteriormente.
Por exemplo, um campo pode ser digitado como uma **data** em um documento e como uma
**sequência** em um documento subsequente, impedindo que o documento subsequente seja
indexado corretamente.

    A operação de visualização não prevê incompatibilidades de tipo porque ela testa apenas um único
documento e não mantém um registro dos resultados da conversão.
-   Às vezes, uma indexação rápida ou de larga escala de documentos pode resultar no reinício
do serviço de procura de backend. Se isso ocorrer, entre em contato com suporte {{site.data.keyword.IBM}} para
obter assistência.
