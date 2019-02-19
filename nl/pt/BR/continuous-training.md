---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-25"

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

# Continuous Relevancy Training
{: #crt}

O {{site.data.keyword.discoveryshort}} Continuous Relevancy Training pode aprender com o comportamento do usuário automaticamente, reduzindo significativamente o esforço necessário para melhorar a classificação de relevância dos resultados. Ele usa interações de usuários para aprender como levantar os resultados mais relevantes. Ele pode aprender por meio de interações como cliques para determinar quais resultados são mais valiosos para os usuários e descobrir os sinais mais importantes para as futuras consultas. O Continuous Relevancy Training reclassificará os documentos para levantar as informações mais relevantes na parte superior dos resultados. Ele pode ser usado para:

- Ajudar a melhorar a relevância dos resultados para agentes de suporte, com base nos resultados em que eles clicam
- Exibir resultados mais relevantes em um robô de bate-papo do cliente com base nos resultados de longo prazo selecionados 
- Fornecer aos especialistas respostas mais relevantes, com base nos resultados que eles exploram

Para configurar o Continuous Relevancy Training:

- O Continuous Relevancy Training pode ser ativado somente no nível de ambiente. As consultas devem usar os terminais `/api/v1/environment/{environment_id}/query` e `/api/v1/environments/{environment_id}/query` para consultar uma ou mais coleções.
- Como os `events` (cliques) do {{site.data.keyword.discoveryshort}} são usados para criar os dados de treinamento necessários, primeiro integre o rastreamento de eventos. Consulte  [ Monitoramento de uso ](/docs/services/discovery/feedback.html#usage)  para obter detalhes.
- É necessário um mínimo de 1000 consultas de língua natural com um evento de clique associado para que o Continuous Relevancy Training seja iniciado. Os eventos e logs são retidos por 30 dias em sua instância, portanto, os 1000 cliques devem ser coletados durante esse período.
- O Continuous Relevancy Training está disponível para o planos Avançados de tamanho `Small` ou maior e os planos Premium. Ele não está disponível para planos `Lite`.
- O número de coleções para o Continuous Relevancy Training é limitado a `5`. Como o Continuous Relevancy Training funciona em múltiplas coleções, os tempos de consulta e de treinamento podem ser estendidos.
- O Continuous Relevancy Training ocorre somente em campos de nível superior e há limites para quantos campos podem ser usados no processo de treinamento. Nos casos em que há mais de `10` campos de nível superior, o treinamento é mais provável de encontrar erros. 

Para usar o Continuous Relevancy Training:

Uma vez treinado, o Continuous Relevancy Training é usado para influenciar os resultados de uma `natural_language_query` ao usar uma consulta de nível de ambiente. 

O Continuous Relevancy Training pode ser usado no tempo de consulta executando uma `natural_language_query` de multicoleção em todas as coleções em seu ambiente. Consulte  [ Consultando múltiplas coleções ](/docs/services/discovery/using.html#multiple-collections)  para obter instruções. 

**Nota:** o Continuous Relevancy Training não afeta as consultas feitas em uma chamada de consulta no nível de coleção treinado ou não treinado (`/v1/environments/{environment_id}/collections/{collection_id}/query`). 

Status de rastreamento:

O status do Continuous Relevancy Training pode ser visualizado por meio do terminal `/api/v1/environments`. Veja a [Referência da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#environments-api){: new_window}. O `status` fornecerá informações sobre o estado das operações de treinamento e o informará se o Continuous Relevancy Training está ativo:

```
"search_status" : [
        {
            "scope" : "environment",
            "status" : "NO_DATA",
            "status_description" : "Discovery is employing a default strategy for document search natural_language_query. Enable query and event logging so we can initiate relevancy training to improve search accuracy.”
        }
    ]
```
