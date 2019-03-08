---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-03"

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


# Migrando do Watson Document Conversion e do Retrieve and Rank
{: #migrate-dcs-rr}

O {{site.data.keyword.documentconversionfull}} e o
{{site.data.keyword.retrieveandrankfull}}
foram descontinuados e substituídos pelo {{site.data.keyword.discoveryfull}}. Geralmente, esses dois
serviços são usados juntos para alimentar, classificar e, em seguida, entregar resultados para seus aplicativos. Este documento é fornecido para guiá-lo pelo processo de migração por meio do
{{site.data.keyword.documentconversionshort}} e do {{site.data.keyword.retrieveandrankshort}}
para o {{site.data.keyword.discoveryshort}}.

O {{site.data.keyword.discoveryfull}} fornece uma interface de consulta mais robusta, ingestão de
dados simplificada, gerenciamento de treinamento melhorado e maior escala. O {{site.data.keyword.discoveryshort}} aborda muitos dos casos de uso principais que o
{{site.data.keyword.retrieveandrankshort}}, incluindo assistente de agente de suporte, procura de base
de conhecimento organizacional e assistência de pesquisa. Ele foi construído com muitos dos desafios
enfrentados pelos usuários do {{site.data.keyword.retrieveandrankshort}} em mente e resolve muitos desses
problemas. O {{site.data.keyword.discoveryshort}} também fornece novos recursos para recuperação
de informações não disponíveis no {{site.data.keyword.retrieveandrankshort}}, incluindo a recuperação
de passagem e melhores algoritmos de procura para localizar resultados mais relevantes.

**Comparação de recurso**

| Recurso | {{site.data.keyword.retrieveandrankshort}} | {{site.data.keyword.discoveryshort}} |
|:-------------|:--------------------:|:-------------:|
| Procura de linguagem natural | Sim | Sim |
| Treinamento de relevância de aprendizado de máquina | Sim | Sim |
| Ferramentas de UI para treinamento | Sim | Sim |
| Entrada de unidade de resposta JSON | Sim | Sim |
| Divisão de documento | Sim | Sim |
| Recuperação de passagem |   | Sim |
| Documento CRUD | Sim | Sim |
| Upload de JSON em lote | Sim |   |
| Enriquecimento NLP automático do documento |   | Sim |
| Integração de modelo NLP customizado para enriquecimento |   | Sim |
| Dados de treinamento armazenados no serviço |   | Sim |
| Gerenciamento de ciclo de vida de modelo automatizado |   | Sim |
| Similaridade de semântica para melhorar a relevância sem treinamento |   | Sim |
| Medida de precisão em conjunto de ferramentas com base no conjunto de testes | Sim |   |
| Suporte de vetor de recurso customizado | Sim |   |
| Configuração do analisador customizado | Sim | Pré-configurado |
| Palavras vazias customizadas | Sim | Pré-configurado |
| Dicionários de idiomas customizados | Sim | Pré-configurado |
| Sinônimos customizados | Sim | Sim |
**Nota:** essa tabela é atualizada conforme novos recursos do {{site.data.keyword.discoveryshort}} são incluídos.

Antes de iniciar a ação de migração, deve-se primeiramente [avaliar](#evaluate) os dados armazenados em seu serviço do {{site.data.keyword.retrieveandrankshort}} e entender como você moverá os diferentes componentes que compõem sus solução atual.

A maioria dos clientes usa o {{site.data.keyword.documentconversionshort}} em conjunto com o
{{site.data.keyword.retrieveandrankshort}}. Se você não estiver usando o {{site.data.keyword.documentconversionshort}} para converter conteúdo para que ele possa ser armazenado em um índice pesquisável, continue para revisar as [opções para migrar o {{site.data.keyword.documentconversionshort}}](#dcs) independente.

Se você originalmente usou o tutorial do {{site.data.keyword.retrieveandrankshort}} e teve como base sua própria instância do serviço nesse tutorial, uma extensão do tutorial que alimenta os mesmos dados no {{site.data.keyword.discoveryshort}} poderá ser localizada [aqui](/docs/services/discovery/migrate-rnr-tut.html).

**Nota:** as funcionalidades de conversão e de enriquecimento são incluídas com o {{site.data.keyword.discoveryshort}}. Se você tiver usado o {{site.data.keyword.documentconversionshort}} e/ou o {{site.data.keyword.nlushort}} para converter e enriquecer documentos HTML, PDF ou Microsoft Word de origem, esses serviços serão substituídos pelos recursos dentro do serviço do {{site.data.keyword.discoveryshort}}.

## Avalie o caminho de migração para o serviço do Watson Discovery
{: #evaluate}

Há duas opções práticas para migrar por meio do {{site.data.keyword.retrieveandrankshort}}: migração por meio do conteúdo de origem e migração por meio do conteúdo indexado. Avalie ambas as opções antes de decidir qual opção será utilizada.

### Migrando do conteúdo de origem
{: #source}

Para migrar por meio do conteúdo de origem, é necessário:

-  ter acesso aos arquivos de origem originais nos quais o conteúdo foi alimentado.
-  extrair programaticamente o ID de cada documento (o resultado já possui um ID antes de sua indexação)

Se você consegue atender a todos os critérios de migração, recomenda-se o uso deste método para mover para o serviço do {{site.data.keyword.discoveryshort}}.

Para migrar seu conteúdo de origem, modifique o procedimento descrito no [tutorial de migração](/docs/services/discovery/migrate-rnr-tut.html) para atender às especificações de seus dados de origem.

#### Migrando unidades de resposta

Se você criou unidades de resposta usando o {{site.data.keyword.documentconversionshort}}, escolha uma das opções a seguir para migrar esse conteúdo:

-  se você treinou um classificador e precisa migrar a classificação, é necessário selecionar o conteúdo que foi retornado do {{site.data.keyword.documentconversionshort}} e alimentá-lo no {{site.data.keyword.discoveryshort}}
-  se você não possui dados de treinamento para migrar, alimente os documentos de origem originais no {{site.data.keyword.discoveryshort}} usando o [recurso de segmentação de documento](/docs/services/discovery/building.html#doc-segmentation)

### Migrando do conteúdo indexado
{: #indexed}

Será necessário migrar por meio do conteúdo indexado no {{site.data.keyword.retrieveandrankshort}} se você não tiver acesso aos documentos de origem originais ou se:

- você usou a geração automática de ID do documento e treinou um classificador.
- criou unidades de resposta no {{site.data.keyword.documentconversionshort}} e as classificou, mas não reteve as unidades de resposta que foram geradas pelo serviço do {{site.data.keyword.documentconversionshort}}.

**Nota:** esse método será possível apenas se todo o conteúdo necessário estiver em campos armazenados no {{site.data.keyword.retrieveandrankshort}}. Se o conteúdo foi somente indexado, mas não armazenado, não será possível consultar o conteúdo fora do serviço e os dados deverão ser convertidos e divididos novamente na origem.

Os documentos são extraídos do serviço usando o método [/v1/solr_clusters/{solr_cluster_id}/solr/\{collection_name\}/select ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/watson/developercloud/retrieve-and-rank/api/v1/#index_doc){: new_window} usando uma consulta em branco `q=*:*`. O número de documentos retornados pode ser maior que a contagem máxima prática de retorno (`200` para a maioria das coleções). Se esse for o caso, múltiplas chamadas deverão ser feitas com a [paginação ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://lucene.apache.org/solr/guide/6_6/pagination-of-results.html){: new_window} apropriada para coletar todos os documentos.

Documentos com **IDs** especificados são transferidos por upload para o serviço do {{site.data.keyword.discoveryshort}} usando o método [/v1/environments/\{environment_id\}/collections/\{collection_id\}/documents/\{document_id\} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#update-doc){: new_window}. Cada upload do documento é uma chamada API separada.

## Migrando dados de treinamento

Depois de migrar seus resultados, a próxima etapa é migrar os dados de treinamento que foram criados para o conteúdo. Há duas opções para migrar os dados de treinamento: migrar por meio da origem (`csv`) e migrar por meio do serviço. Se você transferiu por upload os dados de treinamento de um arquivo `csv` e ainda tiver acesso a esse arquivo, deverá migrar por meio da origem. Se você usou o conjunto de ferramentas do {{site.data.keyword.retrieveandrankshort}} ou não tiver acesso ao arquivo `csv` original, será necessário migrar por meio do serviço.

### Migrando treinamento do conteúdo de origem
{: #csv}

Para migrar por meio do conteúdo de origem de classificação, é necessário:

- ter acesso aos arquivos `csv` de origem originais com os quais as informações de treinamento foram originalmente transferidas por upload.
- assegurar-se de que os IDs dos documentos treinados quando eles estão indexados correspondam aos IDs dos documentos treinados quando eles foram indexados no {{site.data.keyword.retrieveandrankshort}}.

Se você consegue atender a todos os critérios de migração, recomenda-se o uso deste método para mover o treinamento para o serviço do {{site.data.keyword.discoveryshort}}.

Para migrar seus dados de treinamento, modifique o procedimento descrito no [tutorial de migração](/docs/services/discovery/migrate-rnr-tut.html) para atender às especificações de sua origem de dados.

### Migrando dados de treinamento do serviço
{: #extract-train}

Para migrar dados de treinamento por meio do serviço do {{site.data.keyword.retrieveandrankshort}}, é necessário: extrair os dados de treinamento usando as APIs do {{site.data.keyword.retrieveandrankshort}}, converter o JSON de treinamento do {{site.data.keyword.retrieveandrankshort}} em um formato utilizável pelo {{site.data.keyword.discoveryshort}} e, finalmente, alimentar os dados de treinamento no {{site.data.keyword.discoveryshort}} usando a API.

Para extrair dados de treinamento do {{site.data.keyword.retrieveandrankshort}}, use a função `Export` dentro do conjunto de ferramentas do {{site.data.keyword.retrieveandrankshort}}. Após o download com sucesso de uma exportação completa, extraia o arquivo `.zip` salvo. O archive possui dois arquivos. Os dados de treinamento estão armazenados em um arquivo chamado
`export-questions.json`. Esse arquivo contém uma matriz de objetos de treinamento JSON.

Cada resultado de treinamento na matriz é apresentado no seguinte formato:

**Dados de treinamento de amostra do {{site.data.keyword.retrieveandrankshort}}**
```json
{
    "text":"Who was the first royal to attend Wimbledon?",
    "cluster":{
        "id":"f62c11d3-30fa-11e7-8a0c-333f7f431ce8",
        "answers":{
            "f62c11d3-30fa-11e7-8a0c-33":[
                {
                    "id":"dac41335-0e96-40c9-983f-cc3f1c395782",
                    "ranking":1,
                    "source":{
                        "id":"e26a3d20-30fa-11e7-aa5e-d1632b06e0b1",
                        "file":"wimbledon-wikipedia.html",
                        "sequence":17,
                        "strategy":"retrieve"
                    }
                },
                {
                    "id":"661b4c9f-ecdb-4dad-aafc-6ae561a148c0",
                    "ranking":2,
                    "source":{
                        "id":"da1bc620-30fa-11e7-8f90-3305f35a93c9",
                        "file":"generated-otherFactsFigures.docx",
                        "sequence":67,
                        "strategy":"retrieve"
                    }
                },
                {
                    "id":"0053fdb8-c77e-4fcf-b0e0-6a4cd377266a",
                    "ranking":3,
                    "source":{
                        "id":"d9c0add0-30fa-11e7-aa5e-d1632b06e0b1",
                        "file":"generated-allEngland.docx",
                        "sequence":20,
                        "strategy":"retrieve"
                    }
                },
                {
                    "id":"506d3d50-19ed-49c8-b32f-65f848e60e86",
                    "ranking":4,
                    "source":{
                        "id":"da1bc620-30fa-11e7-8f90-3305f35a93c9",
                        "file":"generated-otherFactsFigures.docx",
                        "sequence":63,
                        "strategy":"retrieve"
                    }
                }
            ]
        },
        "flags":{

        }
    }
},
```
{: codeblock}

O {{site.data.keyword.discoveryshort}} não requer todas as informações que são exportadas do {{site.data.keyword.retrieveandrankshort}}. O fragmento a seguir mostra a estrutura necessária de uma entrada de treinamento do {{site.data.keyword.discoveryshort}}.

```json
{
  "natural_language_query": "{natural_language_query}",
  "examples": [
    {
      "document_id": "{document_id_1}",
      "relevance": 0
    },
    {
      "document_id": "{document_id_2}",
      "relevance": 10
    }
  ]
}
```
{: codeblock}

Neste momento, é necessário converter suas informações de treinamento do {{site.data.keyword.retrieveandrankshort}} em informações de treinamento do {{site.data.keyword.discoveryshort}}. Considere os seguintes pontos durante a conversão.

- **Não relevante** é especificado por uma pontuação `relevance` de `0` no {{site.data.keyword.discoveryshort}}, mas é especificado por um `ranking` de `1` no {{site.data.keyword.retrieveandrankshort}} e todas as entradas `"ranking": 1` devem ser convertidas em `"relevance": 0` no {{site.data.keyword.discoveryshort}}
- O conjunto de ferramentas do {{site.data.keyword.discoveryshort}} usa uma escala binária de `0` e `10`. Se você deseja classificar mais resultados e usar o conjunto de ferramentas do {{site.data.keyword.discoveryshort}}, deve-se converter todas as entradas `"ranking": 1` e `"ranking": 2` em `"relevance": 0` e todas as entradas `"ranking": 3` e `"ranking": 4` em `"relevance": 10`. Isso não será necessário se você não estiver classificando resultados adicionais ou se não estiver usando o conjunto de ferramentas do {{site.data.keyword.discoveryshort}}.
- Perguntas não respondidas não são necessárias pelo {{site.data.keyword.discoveryshort}} e a verificação da validade do treinamento de relevância é executada manualmente.

![Fluxo de migração da classificação](images/migrate-ranking.png)

Como um exemplo, os **Dados de treinamento de amostra do {{site.data.keyword.retrieveandrankshort}}** listados acima são convertidos para serem usados no conjunto de ferramentas do {{site.data.keyword.discoveryshort}} a seguir:

```json
{
  "natural_language_query": "Who was the first royal to attend Wimbledon?",
  "examples": [
    {
      "document_id": "e26a3d20-30fa-11e7-aa5e-d1632b06e0b1",
      "relevance": 0
    },
    {
      "document_id": "da1bc620-30fa-11e7-8f90-3305f35a93c9",
      "relevance": 0
    },
    {
      "document_id": "d9c0add0-30fa-11e7-aa5e-d1632b06e0b1",
      "relevance": 10
    },
    {
      "document_id": "da1bc620-30fa-11e7-8f90-3305f35a93c9",
      "relevance": 10
    }
  ]
}
```
{: codeblock}

## Suporte ao idioma
{: #language}

Consulte a [tabela de suporte ao idioma para o {{site.data.keyword.discoveryshort}}](/docs/services/discovery/language-support.html). Os recursos do {{site.data.keyword.retrieveandrankshort}} são suportados principalmente pelo suporte ao idioma **Básico** do {{site.data.keyword.discoveryshort}}.

## Migrando consultas
{: #queries}

A linguagem de consulta do {{site.data.keyword.discoveryfull}} é diferente da linguagem de consulta do Solr usada pelo {{site.data.keyword.retrieveandrankshort}}. Consultas existentes devem ser roteadas novamente para um dos métodos de consulta do {{site.data.keyword.discoveryfull}} e convertidas para usar a linguagem de consulta do {{site.data.keyword.discoveryfull}}. A tabela a seguir descreve alguns dos operadores típicos que são usados na maioria das consultas:

**Migrando da consulta do Solr para o {{site.data.keyword.discoveryshort}} - operadores típicos**

| Operador do Solr | Operador do Discovery | Descrição |
|:-------------:|--------------------|-------------|
| `.` | `.` | delimitador JSON |
| `:` | `:` | Inclui |
|  | `::` | Correspondência exata |
| `-{fieldname}:` | `:!` | Não inclui |
|  | `::!` | Não é uma combinação exata |
| ``\` | ``\` | Caractere de escape |
| `""` | `""` | Consulta de frase |
| `()` | `()`, `[]` | Agrupamento aninhado |
| `OR` | [<code>&#124;</code>] | ou |
| `AND` | [,] | e |
| `[* TO 100]` | `<=`, `>=`, `>`, `<` | Comparações numéricas |
| `^x` | `^x` | Multiplicador de pontuação |
| `*` | `*` | Curinga |
| `~`(0 a 1) | [~n] | Variação de sequência |

Consulte os [Conceitos de consulta](/docs/services/discovery/using.html) e a documentação de [Referência de consulta](/docs/services/discovery/query-reference.html) para obter informações detalhadas sobre a linguagem de consulta do {{site.data.keyword.discoveryfull}}.


## Migração de serviço independente do Watson Document Conversion
{: #dcs}

Se você estiver usando {{site.data.keyword.documentconversionshort}} para ajudar alimentar conteúdo no {{site.data.keyword.retrieveandrankshort}}, então essa funcionalidade evoluiu para um único serviço, o {{site.data.keyword.discoveryshort}}. O {{site.data.keyword.discoveryshort}} permite converter, enriquecer e alimentar facilmente documentos Microsoft Word, PDF, HTML e JSON em um índice treinável e pesquisável. Esta seção será relevante se seu caso de uso não envolver armazenamento do conteúdo convertido em um índice. Se você estiver alimentando documentos em um índice, consulte [alimentando no serviço do {{site.data.keyword.discoveryshort}}](/docs/services/discovery/building.html).

A IBM não fornece mais um serviço que é projetado para conversão independente de documentos Microsoft Word, PDF e HTML. Se você estiver usando atualmente o serviço do {{site.data.keyword.documentconversionshort}} e não alimentar a saída em um serviço on-line indexado (como o {{site.data.keyword.discoveryshort}}), recomenda-se a migração para uma alternativa de software livre, como o [Apache Tika ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://tika.apache.org/){: new_window}.
