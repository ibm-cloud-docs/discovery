---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-09"

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


# Tutorial: Migrando do Retrieve and Rank

Migrando do {{site.data.keyword.retrieveandrankshort}} para o serviço do {{site.data.keyword.discoveryfull}}. Uma continuação do Tutorial de Introdução ao Cranfield

## Visão geral
{: #overview}
Este tutorial orienta o processo de criação e treinamento de um serviço do {{site.data.keyword.discoveryfull}} com dados de amostra. Este tutorial usa o mesmo conjunto de dados usado no [Tutorial de Introdução ao {{site.data.keyword.retrieveandrankshort}}](/docs/services/retrieve-and-rank/getting-started.html), mas é possível usar a mesma abordagem para criar uma instância de serviço que use seus próprios dados.

O processo para usuários que migram dados do {{site.data.keyword.retrieveandrankshort}} para o {{site.data.keyword.discoveryshort}} consiste em duas etapas principais.

1. Migrar os dados de coleção.
2. Migrar os dados de treinamento.

Ao migrar seus dados de coleção treinados, o **mais importante** é _manter os IDs do documento os mesmos_. Isso ocorre porque seus dados de treinamento usam esses IDs para referenciar a verdade absoluta e, se os IDs forem mudados durante a movimentação do {{site.data.keyword.retrieveandrankshort}} para o {{site.data.keyword.discoveryshort}}, a reclassificação será completamente desativada (ou o treinamento poderá nem mesmo iniciar). Como o {{site.data.keyword.discoveryshort}} permite especificar o ID do documento no processo de upload da API, esse problema pode ser evitado seguindo as diretrizes neste documento.  Os dados de treinamento do {{site.data.keyword.retrieveandrankshort}} são geralmente armazenados em um arquivo `csv`. Neste tutorial, esse arquivo `csv` é usado para fazer upload dos dados de treinamento de amostra no {{site.data.keyword.discoveryshort}}.  A migração de dados de treinamento exportados por meio do conjunto de ferramentas do {{site.data.keyword.retrieveandrankshort}} é detalhada em [Migrando dados de treinamento por meio do serviço](/docs/services/discovery/migrate-dcs-rr.html#extract-train).

Este tutorial supõe que o {{site.data.keyword.retrieveandrankshort}} foi configurado de modo semelhante ao [Tutorial de Introdução do {{site.data.keyword.retrieveandrankshort}} ](/docs/services/retrieve-and-rank/getting-started.html) e usa a migração do caminho de origem descrito [aqui](/docs/services/discovery/migrate-dcs-rr.html#source). Consulte [Avalie seu caminho de migração para o serviço Watson Discovery](/docs/services/discovery/migrate-dcs-rr.html#evaluate) para obter outras opções de migração.

Para concluir o tutorial, é necessário o seguinte:

-  **cURL.**  É possível instalar a versão do cURL para seu sistema operacional por meio do [haxx.se ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://curl.haxx.se/){: new_window}. Deve-se instalar a versão que suporta o protocolo Secure Sockets Layer (SSL). Inclua o arquivo binário instalado em sua variável de ambiente PATH.
-  Dados de amostra do Cranfield. Este tutorial usa os dados de coleção de amostra do Tutorial de Introdução ao {{site.data.keyword.retrieveandrankshort}}. [Dados JSON do Cranfield ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-data.json){: new_window}
-  **Verdade absoluta de dados de amostra** Este tutorial usa verdade absoluta de Cranfield de amostra do Tutorial de Introdução ao {{site.data.keyword.retrieveandrankshort}}. [CSV de verdade absoluta do Cranfield![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-gt.csv){: new_window}
-  **Python versão 2.**  Para verificar se o Python está instalado, insira `python -- version` em um prompt de comandos e assegure-se de que o número da versão inicia com 2. Se precisar instalar o Python, consulte [Fazendo download do Python ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://wiki.python.org/moin/BeginnersGuide/Download){: new_window}.
-  Script de upload de dados: [Carregador do documento de descoberta ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-upload.py){: new_window}
-  Script de upload de dados de treinamento: [Carregador de treinamento de descoberta ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-train.py){: new_window}

Os pré-requisitos a seguir são necessários antes de iniciar este tutorial:

-  Este tutorial supõe que você já criou um tutorial do {{site.data.keyword.discoveryshort}} e, se precisar de instruções sobre como criar uma instância do {{site.data.keyword.discoveryshort}}, consulte o [tutorial a seguir](/docs/services/discovery/getting-started.html).

-  Este tutorial supõe que você possui suas credenciais de serviço.
   -  Quando estiver no serviço do Watson {{site.data.keyword.discoveryshort}} no {{site.data.keyword.Bluemix_notm}}, clique em **Credenciais de serviço**.
   -  Clique em **Visualizar credenciais** em Ações.
   -  Copie o valor de `apikey` e certifique-se de que o valor de `url` corresponda ao que está nos exemplos abaixo, se não, substitua-o também.

## Incluindo dados do Cranfield no Discovery

1.  Crie um Ambiente.

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d '{ "name": "my_environment", "description": "My environment" }' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    Copie o `environment-id` que está listado no JSON retornado.

1. Crie uma Coleção.

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d '{ "name": "test_collection", "description": "My test collection", "configuration_id": "{configuration_id}", "language_code": "en" }' "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07"
    ```
    {: pre}

    Copie o `collection-id` que está listado no JSON retornado.

1.  Inclua os documentos que devem ser procurados.
    1.  Faça download do arquivo [cranfield-data.json ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-data.json){: new_window} se você ainda não fez isso. Essa é a origem de documentos que são usados em {{site.data.keyword.retrieveandrankshort}}. Os documentos de coleção do Cranfield estão no formato JSON, que é o formato do {{site.data.keyword.retrieveandrankshort}} aceito e que também funciona corretamente para o Watson {{site.data.keyword.discoveryshort}}.
        **Nota:** o {{site.data.keyword.discoveryshort}} não requer upload do esquema Solr. Isso ocorre porque o {{site.data.keyword.discoveryshort}} infere o esquema da estrutura JSON automaticamente.
    1.  Faça download do script de upload de dados [aqui ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/disco-upload.py){: new_window}. Esse script fará upload do json Cranfield no {{site.data.keyword.discoveryshort}}.
        O script lê o arquivo JSON e envia cada documento JSON individual para o serviço do {{site.data.keyword.discoveryshort}} usando uma configuração padrão no {{site.data.keyword.discoveryshort}}.
        **Nota:** a configuração padrão no {{site.data.keyword.discoveryshort}} fornece configurações semelhantes à configuração Solr padrão no {{site.data.keyword.retrieveandrankshort}}.
    1.  Emita o comando a seguir para fazer upload dos dados `cranfield-data-json` para a coleção `cranfield_collection`. Substitua `{apikey_value}`, `{path_to_file}`, `{environment_id}`, `{collection_id}` por suas informações. Observe que há opções adicionais, como -d para depuração e –v para a saída detalhada por meio do curl.

        ```bash
        python ./disco-upload.py -u apikey:{apikey_value} -i {path_to_file}/cranfield-data.json -e {environment_id} -c {collection_id}
        ```
        {: pre}

1.  Quando o processo de upload é concluído, é possível verificar se os documentos estão lá emitindo o comando a seguir para visualizar os detalhes da coleção:

    ```bash
    curl -u "apikey": "{1}/environments/ {2}{0}{1}{7}-11-07"
    ```
    {: pre}

    A saída será algo semelhante a esta:

    ```json
    {
      "collection_id": "f1360220-ea2d-4271-9d62-89a910b13c37",
      "name": "democollection",
      "configuration_id": "6963be41-2dea-4f79-8f52-127c63c479b0",
      "language": "en",
      "status": "available",
      "description": "this is a demo collection",
      "created": "2015-08-24T18:42:25.324Z",
      "updated": "2015-08-24T18:42:25.324Z",      
      "document_counts": {
        "available": 1000, "processing": 20, "failed": 180
      },
      "disk_usage": {
        "used_bytes": 260
      }, "training_status": {
        "data_updated": null,
        "total_examples": 0,
        "sufficient_label_diversity": false,
        "processing": false,
        "minimum_examples_added": true,
        "successfully_trained": null,
        "available": false,
        "notices": 0,
        "minimum_queries_added": false        
      }
    }
    ```
    {: codeblock}

Consulte a seção `document_counts` para ver quantos documentos foram transferidos por upload com sucesso. Nenhuma falha de documento é esperada com este conjunto de dados de amostra. No entanto, com outros conjuntos de dados, poderá haver falha nas contagens do documento. Se você tiver alguma contagem de documento com falha, será possível visualizar a API de avisos para ver as mensagens de erro. Consulte a seção [aqui ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-notices){: new_window} para revisar o comando da API de avisos.

A seção `training` do retorno fornece informações sobre seu treinamento. Revisaremos essa seção após o upload de seus dados de treinamento.

## Incluindo dados de treinamento no Discovery

O Watson {{site.data.keyword.discoveryshort}} Service usa um modelo de aprendizado de máquina para reclassificação de documentos. Para fazer isso, é necessário treinar um modelo. O treinamento ocorre depois que você carrega consultas suficientes junto dos documentos classificados apropriados. Ao carregar exemplos suficientes com variação suficiente para o Watson {{site.data.keyword.discoveryshort}}, você está ensinando a ele o que é um documento "bom". Nesta etapa, usaremos a "verdade absoluta" Cranfield existente que é usada no {{site.data.keyword.retrieveandrankshort}} para treinar o Watson {{site.data.keyword.discoveryshort}}.

1.  Faça download da amostra [Arquivo csv de verdade absoluta do Cranfield ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://watson-developer-cloud.github.io/doc-tutorial-downloads/retrieve-and-rank/cranfield-gt.csv){: new_window} no tutorial do {{site.data.keyword.retrieveandrankshort}}, caso ainda não tenha feito.

   O arquivo é um conjunto de perguntas que um usuário pode fazer sobre os documentos. O arquivo fornece as informações de exemplo para treinar o classificador no {{site.data.keyword.retrieveandrankshort}} e treinamento de relevância no {{site.data.keyword.discoveryshort}} sobre perguntas e respostas relevantes.

   Para cada pergunta, há pelo menos um identificador para uma resposta (o ID do documento). Cada ID de documento inclui um número para indicar o quão relevante a resposta é para a pergunta. O ID do documento aponta para a resposta no arquivo `cranfield-data.json` que você transferiu por upload para o {{site.data.keyword.discoveryshort}} na etapa anterior.

1.  Faça download do script de upload de dados de treinamento. Esse script será usado para fazer upload dos dados de treinamento para o {{site.data.keyword.discoveryshort}}. O script transforma o arquivo `csv` em um conjunto de consultas e de exemplos JSON e os envia para o serviço do {{site.data.keyword.discoveryshort}} usando as [APIs de dados de treinamento![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#training-data){: new_window}
    **Nota:** o {{site.data.keyword.discoveryshort}} gerencia dados de treinamento dentro do serviço, portanto, ao gerar novos exemplos e consultas de treinamento, eles podem ser armazenados no próprio {{site.data.keyword.discoveryshort}}, não como parte de um arquivo CSV separado que precisa ser mantido.
1.  Execute o script de upload de treinamento para fazer upload dos dados de treinamento para o {{site.data.keyword.discoveryshort}}. Substitua `{apikey_value}`, `{path_to_file}`, `{environment_id}`, `{collection_id}` por suas informações. Observe que há opções adicionais, como `-d` para depuração e `-v` para saída detalhada por meio do curl.

    ```bash
    python ./disco-train.py -u apikey:{apikey_value} -i {path_to_file}/cranfield-gt.csv –e {environment_id} -c {collection_id}
    ```
    {: pre}

1.  Quando os dados são carregados, é possível verificar o status de treinamento usando o comando de detalhes da coleção que vimos na seção anterior. O {{site.data.keyword.discoveryshort}} verifica uma vez por hora se há quaisquer novos dados e, se houver, começará a processá-los e os transformará em um modelo de aprendizado de máquina. Quando um modelo está sob treinamento, é exibido o estado da mudança de seção de treinamento de `"processing": false` para `"processing": true`. Quando o modelo tiver sido treinado, você verá o estado na seção de treinamento mudar de `"available": false` para `"available": true`. Você também verá a mudança de data para o valor `"successfully_trained"`.  Se houver erros, será possível visualizá-los consultando a **API de avisos**, conforme descrito na seção anterior.

## Procurar por documentos
{: search}

O serviço do {{site.data.keyword.discoveryshort}} usará automaticamente um modelo treinado para reclassificar os resultados da procura, se disponível. Quando [uma chamada API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#query-collection){: new_window} é feita com `natural_language_query` em vez de `query`, uma verificação é feita para ver se há um modelo disponível. Se um modelo estiver disponível, então o {{site.data.keyword.discoveryshort}} usará esse modelo para reclassificar os resultados. Primeiramente, faremos uma procura pelos documentos não classificados e depois faremos uma procura usando o modelo de classificação.

1.  É possível procurar por documentos em sua coleção usando um comando cURL. Execute uma consulta usando a chamada API de consulta para ver os resultados não classificados. Substitua `{apikey_value}`, `{environment_id}`, `{collection_id}` por seus próprios valores. Os resultados retornados serão resultados não classificados e usarão as fórmulas de classificação padrão do {{site.data.keyword.discoveryshort}}. É possível tentar outras consultas abrindo o arquivo `csv` de dados de treinamento e copiando o valor da primeira coluna para o parâmetro de consulta.

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&query=what is the basic mechanism of the transonic aileron buzz"
    ```
    {: pre}

1.  Agora, execute uma procura usando o modelo configurando o parâmetro `natural_language_query`. Antes de fazer isso, verifique se você tem um modelo treinado, conforme descrito na seção anterior.  Cole o código a seguir em seu console, substituindo `{apikey_value}`, `{environment_id}`, `{collection_id}` por seus valores.

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&natural_language_query=what is the basic mechanism of the transonic aileron buzz"
    ```
    {: pre}

    Esse comando retornará resultados reclassificados usando o modelo treinado anteriormente. Compare os resultados dessa procura, bem como os resultados de algumas das outras procuras que você tentou anteriormente. Podem ser exibidas algumas diferenças nos resultados em comparação ao que é visto na {{site.data.keyword.retrieveandrankshort}}. Isso ocorre porque algumas das técnicas utilizadas para procura foram mudadas para simplificar a experiência e melhorar os resultados, no entanto, em geral a qualidade dos resultados será semelhante.

Após avaliar os resultados da procura reclassificados, é possível refiná-los no {{site.data.keyword.discoveryshort}} repetindo a etapa de upload de dados de treinamento com consultas e exemplos de treinamento tradicionais e visualizando os resultados da procura.  Também é possível incluir novos documentos, conforme descrito na primeira etapa, para ampliar o escopo da procura. Semelhante ao {{site.data.keyword.retrieveandrankshort}}, a melhora dos resultados com treinamento é um processo iterativo.
