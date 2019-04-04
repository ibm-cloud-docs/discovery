---

copyright:
  years: 2019
lastupdated: "2019-03-07"

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

# Alta disponibilidade e recuperação de desastre
{: #recovery}

O {{site.data.keyword.discoveryfull}} suporta alta disponibilidade sem nenhum ponto único de falha. Além disso, é responsabilidade do cliente fazer backup de seus dados do {{site.data.keyword.discoveryshort}} em suporte de seu próprio plano de recuperação de desastres para que você possa recriar seu serviço.
{: shortdesc}

O tráfego do {{site.data.keyword.discoveryshort}} tem a carga balanceada em múltiplas zonas em uma região. Cada zona é um data center na mesma região. Consulte [Como assegurar tempo de inatividade zero?![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/docs/overview?topic=overview-zero-downtime#zero-downtime){: new_window} para obter mais informações.

## Fazendo backup de seus dados no Watson Discovery
{: #backup}

Existem vários métodos para fazer backup dos dados armazenados no {{site.data.keyword.discoveryfull}}. Esses métodos devem ser incluídos em seu plano de recuperação de desastres. 

-  Dados dos quais você deve manter uma cópia, como documentos de origem
-  O Data {{site.data.keyword.discoveryshort}} armazena e é necessário extrair e fazer backup
  
Haverá dados que precisarão ser recriados do zero (por exemplo, dados que não podem passar por backup, tais como eventos de feedback). 

### Documentos Ingestionados
{: #backupdocs}

Seus documentos transferidos por upload são convertidos e enriquecidos e, em seguida, armazenados no índice de procura. O índice de procura não é recuperável no caso de um desastre e, portanto, é necessário armazenar um backup de todos os seus documentos de origem em um local seguro.

Se você também importar documentos executando crawls planejados de origens de dados externas, será necessário reter as credenciais de origem de dados externamente para que seja possível reestabelecer suas origens de dados rapidamente. Consulte [Conectando-se a origens de dados](/docs/services/discovery?topic=discovery-sources#sources) para obter a lista de origens disponíveis e as credenciais necessárias para cada uma delas.

### Configurações
{: #backupconfigs}

É necessário fazer backup de suas configurações de instância e armazená-las localmente no caso de um desastre. 

Para fazer backup dessas configurações, primeiro [liste suas configurações](https://cloud.ibm.com/apidocs/discovery#list-configurations) para cada instância. 

Depois de obter a lista de configurações, [obtenha os detalhes](https://cloud.ibm.com/apidocs/discovery#get-configuration-details) para cada configuração.

### Dados de treinamento
{: #backuptraining}

É necessário fazer backup de seus dados de treinamento para cada coleção treinada e armazená-los localmente no evento de um desastre.  

Dados de treinamento são usados para treinamento explícito de suas coleções e são armazenados em uma base por coleção. 

Para extrair os dados de treinamento, use a API para fazer download das consultas e das classificações por meio do {{site.data.keyword.discoveryshort}}. 

1.  [ Listar os dados de treinamento ](https://cloud.ibm.com/apidocs/discovery#list-training-data)
1.  [ Liste os exemplos ](https://cloud.ibm.com/apidocs/discovery#list-examples-for-a-training-data-query)  para cada consulta.
1.  [Obtenha os detalhes](https://cloud.ibm.com/apidocs/discovery#get-details-for-training-data-example) para exemplos de dados de treinamento. 

Os `document ids` que você usa em seu ponto de dados de treinamento para os documentos em sua coleção atual. DEVE-SE usar os mesmos `document ids` em suas novas coleções para assegurar que os IDs corretos sejam mencionados. Se você não fizer isso, seu treinamento de relevância restaurado NÃO FUNCIONARÁ.
{: important} 

### Consultas
{: #backupqueries}

Por padrão (a menos que você cancele), o {{site.data.keyword.discoveryshort}} armazenará as consultas que você enviar para ele. 

Se você desejar ser capaz de restaurá-los para [propósitos estatísticos](https://cloud.ibm.com/apidocs/discovery#number-of-queries-over-time), será necessário armazenar essas consultas separadamente. 

É possível [extrair consultas](https://cloud.ibm.com/apidocs/discovery#search-the-query-and-event-log) do {{site.data.keyword.discoveryshort}}, no entanto, um máximo de 10.000 consultas são armazenadas. Não há nenhuma API de paginação. As consultas de restauração não são recomendadas. Recomendamos iniciar do zero. 

### Feedback / cliques
{: #clicks}

Se você está armazenando cliques na forma de eventos de feedback, não há nenhuma maneira fácil atualmente de fazer backup e restaurar essas informações. A recomendação é iniciar do zero com a API do [cliques/dados de feedback](https://cloud.ibm.com/apidocs/discovery#create-event). 

### Listas de Expansão
{: #backupexpansions}

Se você estiver usando expansões para modificação de consulta, será necessário fazer backup de sua lista de expansão e armazená-la localmente. Para fazer isso, solicite a lista de expansão usando o comando da API [get expansion list](https://cloud.ibm.com/apidocs/discovery#get-the-expansion-list) e armazene-a localmente.

### Dicionários de tokenização ou interrupções
{: #backupstopwords}

Se você usar esses recursos, precisará fazer backup desses arquivos e armazená-los localmente. No caso de palavras vazias, faça backup do arquivo de texto e, no caso das tokenizações, é necessário fazer backup do arquivo JSON. Consulte [Criando dicionários de tokenização customizados](/docs/services/discovery?topic=discovery-query-concepts#tokenization) e [Definindo palavras vazias](/docs/services/discovery?topic=discovery-query-concepts#stopwords) para obter mais informações sobre cada tipo de arquivo.

### Informações de Coleta
{: #collectioninfo}

Isso não é necessário, mas é uma boa prática [recuperar o status](https://cloud.ibm.com/apidocs/discovery#get-collection-details) para cada coleção em uma base regular e armazenar as informações localmente. Ao reter essas estatísticas, será possível verificar posteriormente se os processos de restauração foram bem-sucedidos, se necessário.
{: tip} 


### Modelos do Smart Document Understanding
{: #backupsdu}

Se estiver usando o Smart Document Understanding (SDU), você terá modelos associados à sua configuração. Para evitar a perda dessas informações, é necessário [exportar seus modelos](/docs/services/discovery?topic=discovery-sdu#import), fazer backup deles e armazená-los localmente. Os modelos de SDU têm a extensão de arquivo de `.sdumodel`.


## Restaurando seus dados para uma nova instância do Watson Discovery
{: #restore}

Considere usar seus backups para restaurar para uma nova instância do {{site.data.keyword.discoveryshort}} em um data center diferente (também conhecido como região/localização. Por exemplo, Dallas, Houston, Washington, DC, Londres). 
{: note}

Para iniciar a restauração, primeiro comece revisando sua lista de coleções e origens de dados associadas, bem como os backups de arquivo.

-  Crie seu [ambiente](https://cloud.ibm.com/apidocs/discovery#create-an-environment) e [coleções](https://cloud.ibm.com/apidocs/discovery#create-a-collection) usando as informações de configuração salvas. Assegure-se de que a configuração apropriada esteja definida de forma adequada e de que o idioma para a coleção esteja configurado corretamente. A falha ao fazer isso atrasará o funcionamento de seu sistema.
-  Se você teve qualquer configuração customizada definida em {{site.data.keyword.discoveryshort}}, será necessário [recriar essas configurações customizadas](/docs/services/discovery?topic=discovery-configservice#when-you-need-a-custom-configuration). 
-  Inclua novamente os dicionários de tokenização ou palavras vazias nas coleções. Consulte [Criando dicionários de tokenização customizados](/docs/services/discovery?topic=discovery-query-concepts#tokenization) e [Definindo palavras vazias](/docs/services/discovery?topic=discovery-query-concepts#stopwords).  
-  Se você tiver uma expansão de consulta customizada, será necessário [incluir as expansões de consulta](https://cloud.ibm.com/apidocs/discovery#create-or-update-expansion-list) para cada coleção também. 
-  Se você estiver usando qualquer modelo de entidade customizado do Watson Knowledge Studio (WKS) para enriquecimento, será necessário [reimportar esse modelo](/docs/services/discovery?topic=discovery-configservice#custom-entity-model) em sua instância do {{site.data.keyword.discoveryshort}}. 

Depois de ter suas coleções configuradas como antes, será necessário iniciar a ingestão de seus documentos de origem. Dependendo de como você alimentou seus documentos anteriormente, é possível fazer isso usando:
-  A  [ API ](https://cloud.ibm.com/apidocs/discovery#add-a-document)
-  Um  [ conector ](/docs/services/discovery?topic=discovery-sources#sources) 
-  O  [ Crawler de Dados ](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler)
-  ou outro método

### Restaurando dados de treinamento
{: #restoretraining}

Após a restauração das coleções, é possível iniciar o processo de [recriação de seus modelos de treinamento de relevância](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api). 

Recupere os dados de treinamento dos quais você fez backup e, em seguida:

1. [ Fazer Upload de suas Consultas ](https://cloud.ibm.com/apidocs/discovery#add-query-to-training-data)
1. [Fazer upload dos documentos de exemplo](https://cloud.ibm.com/apidocs/discovery#add-example-to-training-data-query) para cada consulta.
1.  Depois que os dados de treinamento são transferidos por upload, revise essa [postagem do blog](https://developer.ibm.com/dwblog/2017/get-relevancy-training/) para assegurar que você atenda os números de precisão anteriores. Lembre-se de que os `document ids` antigos devem ser transferidos para os novos dados de treinamento ou atualizados para refletir os novos IDs de documento em sua nova coleção.


### Restaurando Conexões para Origens de Dados Externas
{: #restoreconnections}

No caso de uma perda de dados inesperada, é possível perder os crawls planejados de origens de dados externas. Consulte [Conectando-se a origens de dados](/docs/services/discovery?topic=discovery-sources#sources) para obter a lista de origens disponíveis.

Para restaurar seus dados externos, será necessário reestabelecer suas conexões com essas origens de dados e, em seguida, executar novo crawl nelas.

Localize as credenciais de origem de dados que você armazenou anteriormente e siga as instruções [aqui](/docs/services/discovery?topic=discovery-sources#sources). Isso permitirá que você se reconecte às suas origens de dados e importe seus dados no {{site.data.keyword.discoveryshort}}.


### Restaurando modelos do Smart Document Understanding
{: #restoresdu}

Para importar um modelo do Smart Document Understanding (SDU) exportado anteriormente, siga as instruções [aqui](/docs/services/discovery?topic=discovery-sdu#import). Os modelos de SDU têm a extensão de arquivo de `.sdumodel`.

Ao importar um modelo existente de SDU para uma nova coleção, é uma boa melhor prática criar a nova coleção e incluir um documento e, em seguida, importar o modelo e fazer upload do restante de seus documentos.
