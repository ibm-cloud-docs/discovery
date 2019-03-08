---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-08"

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

# Integrando-se com o Watson Knowledge Studio
{: #integrating-with-wks}

É possível integrar um modelo customizado do {{site.data.keyword.knowledgestudiofull}} com o
serviço do {{site.data.keyword.discoveryshort}} para fornecer enriquecimentos customizados de entidade
e de relações.
{: shortdesc}

Isso fornece a flexibilidade para aplicar os recursos de aprimoramento de documento do serviço do {{site.data.keyword.discoveryshort}} com informações específicas para áreas de foco particular, como indústria ou disciplina científica. É possível usar dados públicos e seus próprios dados proprietários em seu modelo de enriquecimento.

É possível usar a API de serviço ou o conjunto de ferramentas do {{site.data.keyword.discoveryshort}} para integrar um modelo do {{site.data.keyword.knowledgestudioshort}} com o serviço do {{site.data.keyword.discoveryshort}}.

## Antes de Começar

Antes de ser possível integrar um modelo customizado de {{site.data.keyword.knowledgestudioshort}} com o serviço do {{site.data.keyword.discoveryshort}}, deve-se criar e implementar o modelo usando o{{site.data.keyword.knowledgestudioshort}}. Consulte a [Documentação do {{site.data.keyword.knowledgestudioshort}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.bluemix.net/docs/services/knowledge-studio/tutorials-create-project.html#wks_tutintro){: new_window} para obter informações sobre como criar e implementar modelos. É necessário ter o ID exclusivo do modelo implementado para integrá-lo com o serviço do {{site.data.keyword.discoveryshort}}.

## Integrando seu modelo customizado com a API

1.  Obtenha o ID de seu ambiente do {{site.data.keyword.discoveryshort}} conforme descrito em [Lista de ambientes![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_environments){: new_window}. Observe o ID de ambiente.
1.  Liste os IDs de sua configuração ou configurações atuais do {{site.data.keyword.discoveryshort}} conforme descrito em [Lista de configurações ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_configurations){: new_window} Observe o ID da configuração que você deseja integrar ao seu modelo customizado do {{site.data.keyword.knowledgestudiofull}}.
1.  Faça download de uma cópia de sua configuração atual do {{site.data.keyword.discoveryshort}} executando os comandos a seguir em um shell bash ou equivalente, tal como Cygwin for Windows. Substitua `{environment_id}` e `{configuration_id}` pelos IDs que você anotou nas duas etapas anteriores.

    ```bash
    curl -u "apikey": "{1}/environments/ {2}{0}{1}{7}-11-07" > my_config.json
    ```
    {: pre}

    Esse comando lista o conteúdo do seu arquivo de coleção e os coloca em um arquivo JSON chamado `my_config.json`.
1.  Abra o arquivo `my_config.json` em um editor de texto e faça as seguintes mudanças:
    1.  Mude o valor do campo `"name"` para algo que indica o propósito da nova configuração. É possível mudar opcionalmente o valor do campo `"description"` também.

        ```json
        ...
        "name": "wks-config", "description": "This is a configuration to use with a WKS model",
        ...
        ```
        {: codeblock}

    1.  Atualize os campos de enriquecimento com informações para o modelo do {{site.data.keyword.knowledgestudioshort}}. Assumindo que os campos de enriquecimento originalmente leram:

        ```json
        "enrichments": [ {
            "source_field": "text", "destination_field": "enriched_text", "enrichment": "natural_language_understanding", "options": {
                "features": {
                    "entities": {
                        "sentiment": true, "emotion": false, "limit": 50
                    }, "sentiment": {
                        "document": true }, "categories": {}, "concepts": {
                        "limit": 8
                    },
                    "relations": {}
                }
            }
        }]
        ```
        {: codeblock}

    1.  Atualize o arquivo da seguinte maneira, substituindo o ID exclusivo do modelo do {{site.data.keyword.knowledgestudioshort}} descrito em "Antes de iniciar" por `{watson_knowledge_studio_model_ID}`.

        ```json
        "enrichments": [ {
            "source_field": "text", "destination_field": "enriched_text", "enrichment": "natural_language_understanding", "options": {
                "features": {
                    "entities": {
                        "sentiment": true,
                        "emotion": false,
                        "limit": 50,
                        "model": "{watson_knowledge_studio_model_ID}"
                    }, "sentiment": {
                        "document": true }, "categories": {}, "concepts": {
                        "limit": 8
                    }, "relations": {
                      "model": "{watson_knowledge_studio_model_ID}"
                    }
                }
            }
        }]
        ```
        {: codeblock}

1.  Salve o arquivo `my_config.json`.
1.  Use um validador JSON, como [JSLint ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://jslint.com){: new_window} para validar e, se necessário, corrija seu JSON editado antes de executar as próximas etapas.
1.  Atualize a configuração conforme a seguir. Você precisa novamente dos IDs `{environment_id}` e `{configuration_id}` coletados no início deste procedimento.

    ```bash
    curl -X PUT -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d @my_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-11-07"
    ```
    {: pre}

    **Nota:** se você estiver criando uma nova configuração ou modificando a
configuração padrão, será necessário criar uma nova configuração customizada em vez de atualizar uma
configuração existente. Antes de criar uma nova configuração, certifique-se de que o
campo `"configuration_id":` foi removido do seu arquivo `my_config.json`
e, em seguida, execute o seguinte comando:

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d @my_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07"
    ```
    {: pre}

    Ambos os comandos retornam o conteúdo do arquivo de configuração atualizado.

## Integrando o seu modelo customizado com o conjunto de ferramentas do Discovery

É possível integrar um modelo customizado nos enriquecimentos
{{site.data.keyword.knowledgestudioshort}}
[Extração de Entidade](/docs/services/discovery/building.html#entity-extraction) ou
[Extração de Relação](/docs/services/discovery/building.html#relation-extraction)
com o conjunto de ferramentas do {{site.data.keyword.discoveryshort}}.

1. Obtenha o `ID do modelo` de seu
modelo do {{site.data.keyword.knowledgestudioshort}}.
1. No conjunto de ferramentas do {{site.data.keyword.discoveryshort}}, clique no ícone **Gerenciar dados** no canto superior esquerdo para abrir a tela **Gerenciar dados** e, em seguida, crie ou abra uma coleção. **Nota:** se você escolher uma coleção existente, ela deverá estar vazia. Se não, será necessário realimentar esses documentos após a criação de seu novo arquivo de configuração.
1. Na seção **Configuração** da tela **Gerenciar dados** para sua coleção, clique em **Alternar** e, em seguida, em **Criar uma nova configuração**. Nomeie a configuração. 
1. Clique em **Incluir enriquecimentos** e selecione os enriquecimentos
**Extração de Entidade** ou **Extração de Relação**.
1. Insira o `ID do modelo` na caixa `ID do modelo customizado`
do enriquecimento selecionado. O modelo {{site.data.keyword.knowledgestudiofull}} customizado
substituirá o padrão para esse enriquecimento. 
1. Clique em **Aplicar** e depois em
**Concluído**.

Quando os documentos são transferidos por upload para uma coleta de dados, eles são convertidos e enriquecidos usando o arquivo de configuração escolhido para essa coleção. Se você alternar uma coleção existente para um novo arquivo de configuração após os documentos terem sido
transferidos por upload, esses documentos transferidos por upload permanecerão convertidos pelo arquivo de
configuração original. Quaisquer documentos transferidos por upload depois de alternar o arquivo de
configuração usarão o novo arquivo de configuração. Se você deseja que a coleção **inteira** use a nova configuração, será necessário criar uma nova coleção, escolher esse novo arquivo de configuração e fazer um novo upload de todos os documentos.

**Observação:** somente um modelo do {{site.data.keyword.knowledgestudiofull}} pode ser designado a um enriquecimento.

## Próximas Etapas

Use o serviço do {{site.data.keyword.discoveryshort}} com sua nova configuração para alimentar
dados privados. Os documentos que você alimenta com a configuração atualizada são enriquecidos automaticamente com os dados do seu modelo customizado.
