---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-17"

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

# Monitoramento de uso
{: #usage}

É possível monitorar e controlar o uso de sua instância do {{site.data.keyword.discoveryshort}} e usar esses dados para ajudar a entender e melhorar seus aplicativos. A [API de eventos ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#create-event){: new_window} pode ser usada para criar entradas de log que estão associadas a consultas e ações de língua natural específicas. Por exemplo, é possível registrar quais documentos em um conjunto de resultados foram "clicados" por um usuário e quando esse clique ocorreu.

**Nota:** os logs e eventos são monitorados somente para consultas de língua natural em coletas de dados privados. Nenhum log é coletado no  {{site.data.keyword.discoverynewsfull}}.

O {{site.data.keyword.discoveryshort}}  pode registrar as seguintes informações:
- **Consultas** - consultas de língua natural são executadas com relação a coleções em seu ambiente 
- **Impressões** (ou **Resultados**) - os resultados retornados para uma consulta específica, geralmente documentos ou passagens 
- **Eventos** - interações que um usuário executa em um resultado ou conjunto de resultados no {{site.data.keyword.discoveryshort}} (por exemplo, um clique em um resultado de documento)

As **Consultas** e **Impressões** são registradas automaticamente; a criação de log de **Eventos** pode ser integrada a seu aplicativo por meio da API.

## Visualizando os logs
{: #viewlogs}

É possível procurar o log de consulta e de eventos para localizar sessões de consulta que correspondam aos critérios especificados. A procura do terminal `logs` usa a sintaxe da consulta padrão do {{site.data.keyword.discoveryshort}} para os parâmetros que são suportados. O terminal fornece a funcionalidade de consulta básica para visualizar e procurar por meio dos dados registrados.  

O terminal `/api/v1/logs` suporta os parâmetros de consulta do {{site.data.keyword.discoveryshort}} a seguir.
- query 
- filtro
- ordenação
- Nativa 
- Deslocamento
- versão

Para obter detalhes adicionais sobre a função e a sintaxe para os parâmetros, veja [Parâmetros de consulta](/docs/services/discovery?topic=discovery-query-parameters#query-parameters).

Exemplo de procura de logs para uma consulta de língua natural que contém o termo “train”:

` https://gateway.watsonplatform.net/discovery/api/v1/logs?version=2018-03-28&query=train `

A resposta de uma consulta de `logs` inclui resultados que parecem semelhantes aos resultados do documento do {{site.data.keyword.discoveryshort}}. Cada resultado será uma consulta ou um evento, especificado no campo `type` do documento.  

Exemplo de log de consulta:

```
{
            "customer_id": "",
            "environment_id": "252e6e82-c2d2-450e-9670-0008b0a3a99c",
            "natural_language_query": "how do i get from the airport to the city",
            "query_id": "_Qs35yOoa7",
            "document_results": {
                "count": 2,
                "results": [
                    {
                        "collection_id": "af9e1f41-6114-4d77-bca6-c9b99b2601b1",
                        "score": 6.724753491503856,
                        "position": 1,
                        "document_id": "4193eaa727d79b0f74597356dbcbb9a7"
                    },
                    {
                        "collection_id": "af9e1f41-6114-4d77-bca6-c9b99b2601b1",
                        "score": 5.791631414211986,
                        "position": 2,
                        "document_id": "bdcd6a9cc1438a3faa8c925f6a8d9429"
                    }
                ]
            },
            "event_type": "query",
            "session_token": "1_LKczxWGEWx5TJAi1_Qs35yOoa7",
            "created_timestamp": "2018-09-12T05:20:07.469Z"
        }
```

Com os logs de consulta, é possível investigar o tipo dos resultados retornados para seus usuários finais e investigar maneiras de melhorar a qualidade do resultado usando as abordagens disponíveis no {{site.data.keyword.discoveryshort}}. Por exemplo: 
- treinamento de relevância, veja [Melhorando a relevância de resultados com a API](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api) e [Melhorando a relevância de resultados com o conjunto de ferramentas](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling)
- [operadores de consulta](/docs/services/discovery?topic=discovery-query-operators#query-operators)
- [ expansão de consulta ](/docs/services/discovery?topic=discovery-query-concepts#query-expansion)
- configurações customizadas, consulte a  [ Referência de configuração ](/docs/services/discovery?topic=discovery-configref#configref)

## Criando logs de eventos
{: #eventlogs}

Os logs de eventos são usados para rastrear as interações de usuários dentro de seu aplicativo. Isso pode ajudá-lo a entender o quão bem o seu aplicativo está sendo executado, bem como as áreas de identificação que você pode precisar focar para melhorar os resultados. O {{site.data.keyword.discoveryshort}} fornece uma API que pode ser integrada a seu aplicativo para rastrear eventos. Chamar essa API com as informações apropriadas quando um usuário executa uma ação envia um sinal de volta para o {{site.data.keyword.discoveryshort}}, que pode então ser visualizado nos logs. 

Os eventos podem ajudar a reunir informações sobre métricas de computação (como taxa de clique) para medir o quanto o aplicativo é efetivo para ajudar os usuários finais a localizar informações relevantes ou podem ser usados para ajudar a fornecer treinamento, revisando as consultas e os cliques para começar a construir a verdade absoluta. 

É possível incluir essa API sempre que os usuários interagem com seus resultados. Por exemplo, em uma UI de procura, você talvez deseje incluí-la quando um usuário clicar em um link do documento ou, em uma interface de robô de bate-papo, talvez deseje usá-la para rastrear quando o usuário clicar em um botão **Expandir** ou **Mais detalhes**.

Os resultados do {{site.data.keyword.discoveryshort}} retornarão informações adicionais que podem ser usadas para rastreamento de eventos, incluindo um token de sessão. 

` "matching_results": 179, `  ` "session_token": "1_LKczxxxWGEWx59fYD0_VV8HFUpb6" `

Para registrar um evento, faça um POST para o terminal `/api/v1/events`. Veja a
[API de eventos ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#create-event){: new_window} para obter detalhes.

Quando um evento é registrado, ele pode ser lido de volta usando o terminal `/api/v1/logs`. Associe os eventos à consulta associada usando o `session_token`.
