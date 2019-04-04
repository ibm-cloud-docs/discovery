---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-02-28"

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

# Configurando o Data Crawler
{: #configuring-the-data-crawler}

Para configurar o Data Crawler para efetuar crawl em seu repositório, deve-se especificar o adaptador
de entrada apropriado no arquivo `crawler.conf` e, em seguida, configurar as
informações específicas do repositório nos arquivos de configuração do adaptador de entrada.
{: shortdesc}

O Data Crawler deve ser usado apenas para efetuar crawl de compartilhamentos de arquivo ou bancos de dados; em todos os outros casos, é necessário usar o conector apropriado do {{site.data.keyword.discoveryshort}}. Veja [Conectando a origens de dados](/docs/services/discovery?topic=discovery-sources#sources) para obter detalhes. A assistência não será mais fornecida para o Data Crawler se você estiver usando-o com uma origem de dados suportada pelos conectores do {{site.data.keyword.discoveryshort}}.
{: important}

Antes de fazer as mudanças listadas nessas etapas, certifique-se de que você criou o seu
diretório ativo copiando o conteúdo do diretório
`{installation_directory}/share/examples/config` para um
diretório ativo em seu sistema, por exemplo, `/home/config`.

**Importante:** não modifique os arquivos de exemplo de configuração fornecidos
diretamente. Copie-os e, em seguida, edite-os. Se você editar os arquivos de exemplo no local, sua configuração poderá ser substituída ao fazer upgrade do Data Crawler ou poderá ser removida ao desinstalá-lo.

**Observação:** as referências neste guia aos arquivos no diretório `config`, tal como `config/crawler.conf`, referem-se ao arquivo em seu diretório de trabalho e NÃO no diretório `{installation_directory}/share/examples/config` instalado.

Os valores especificados são os padrões em `config/crawler.conf` e configuram o
conector do sistema de arquivos:

1.  Abra o arquivo `config/crawler.conf` em um editor de texto.

    -   Configure a opção `crawl_config_file` para o arquivo `.conf`
que você modificou anteriormente, por exemplo: `connectors/filesystem.conf`.
    -   Configure a opção `crawl_seed_file` para o `-seed.conf` que
você modificou anteriormente, por exemplo: `seeds/filesystem-seed.conf`.
    -   Configure as opções `output_adapter` `class` e `config` para o serviço do {{site.data.keyword.discoveryshort}} como a seguir:

        ```
        classe - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

        configuração - "discovery_service"

        discovery_service {
          incluir "discovery/discovery_service.conf" }
        ```
        {: codeblock}

    Há outras configurações opcionais neste arquivo que podem ser definidas conforme apropriado para
seu ambiente, consulte:
[Configurando
opções de crawl](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-crawl-options),
[Configurando o adaptador de
entrada](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#input-adapter), [Configurando
o adaptador de saída](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#output-adapter) e
[Opções
adicionais de gerenciamento de crawl](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#additional-crawl-management-options) para obter informações detalhadas sobre como configurar esses
valores.

1.  Abra o arquivo `discovery/discovery_service.conf` em um editor de texto. Modifique
os valores a seguir que são específicos para o serviço do {{site.data.keyword.discoveryshort}}
que você criou anteriormente no {{site.data.keyword.Bluemix}}:

    -   `environment_id` - Seu ID de ambiente do serviço do {{site.data.keyword.discoveryshort}}.
    -   `collection_id` - Seu ID de coleção do serviço do {{site.data.keyword.discoveryshort}}.
    -   `configuration_id` - Seu ID de configuração do serviço do {{site.data.keyword.discoveryshort}}.
    -   `configuration` - O local do caminho completo deste arquivo `discovery_service.conf`, por exemplo, `/home/config/discovery/discovery_service.conf`.
    -   `username` - credencial de nome do usuário para seu serviço do {{site.data.keyword.discoveryshort}}.
    -   ` apikey ` -Credencial para seu serviço do  {{site.data.keyword.discoveryshort}} .

    Há outras configurações opcionais neste arquivo que podem ser definidas conforme apropriado para
seu ambiente. Consulte
[Configurando
opções de serviço](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#configuring-service-options) para obter informações detalhadas sobre como configurar esses valores.

1.  Após modificar esses arquivos, você está pronto para efetuar crawl em seus dados. Continue com
[Efetuando crawl de
seu repositório de dados](/docs/services/discovery?topic=discovery-crawling-your-data-repository#crawling-your-data-repository) para continuar.

## Configurando opções de crawl
{: #configuring-crawl-options}

O arquivo `config/crawler.conf` contém informações que avisam o Data Crawler
sobre quais arquivos serão usados para seu crawl (adaptador de entrada), o local para envia a coleção de
arquivos submetidos a crawl quando o crawl tiver sido concluído (adaptador de saída) e outras opções de
gerenciamento de crawl.

**Nota:** todos os caminhos de arquivo são relativos ao
diretório `config`, exceto o local indicado.

Para acessar o manual no produto no arquivo `crawler.conf`, com as informações mais
atualizadas, digite o comando a seguir no diretório de instalação do Crawler: `man
crawler.conf`
{: tip}

As opções que podem ser configuradas neste arquivo são:

### Adaptador de entrada
{: #input-adapter}

-   **`class`** - somente para uso interno; define a classe do
adaptador de entrada do Data Crawler. O valor padrão é:
`com.ibm.watson.crawler.connectorframeworkinputadapter.Crawl`
-   **`config`** - somente para uso interno; define a configuração da
estrutura do conector. A chave de configuração padrão dentro desse bloco a ser transmitida para o adaptador de
entrada escolhido é: `connector_framework`

    A estrutura do conector é o que permite conversar com seus dados. Ela pode representar dados internos
dentro da empresa ou pode representar dados externos na web ou na nuvem. Os conectores permitem acesso a
várias origens de dados diferentes, enquanto que a conexão é realmente controlada pelo processo de crawl.

    **Importante:** os dados recuperados pelo Connector Framework Input Adapter são
armazenados em cache localmente. Eles não são armazenados criptografados. Por padrão, os dados são armazenados
em cache em um diretório temporário que deve ser limpo na reinicialização e devem ser legíveis somente pelo
usuário que executou o comando do crawler.

    Há uma chance para esse diretório sobreviver ao crawler quando a estrutura do conector desaparecer antes que possa limpar a si mesmo. Considere cuidadosamente o local para seus dados em cache, é possível
colocá-los em um sistema de arquivos criptografados, mas esteja ciente das implicações de desempenho desde procedimento. Somente você pode decidir o equilíbrio apropriado entre a velocidade e a segurança dos seus crawls.
-   **`crawl_config_file`** - o arquivo de configuração a ser usado para o crawl. O valor padrão é: `connectors/filesystem.conf`
-   **`crawl_seed_file`** - o arquivo inicial de crawl a ser usado para o crawl. O valor padrão é: `seeds/filesystem-seed.conf`
-   **`id_vcrypt_file`** - arquivo-chave usado para criptografia de dados pelo crawler; a chave padrão incluída com o crawler é `id_vcrypt`. Use o script vcrypt na pasta `bin` se precisar gerar um novo arquivo `id_vcrypt`.
-   **`crawler_temp_dir`** - a pasta temporária do Crawler para logs do conector. O valor padrão, `tmp`, é fornecido. Se ele ainda não existir, a pasta `tmp` será criada no diretório atualmente em funcionamento.
-   **`extra_jars_dir`** - inclui um diretório de JARs extras no caminho de classe da estrutura do conector.

    **Nota:** relativo ao diretório `lib/java` da estrutura do conector.

    -   Este valor deve ser `database` ao usar o conector do banco de dados.

    É possível deixar esse valor vazio (ou seja, sequência vazia "") ao usar outros conectores.

-   **`urls_to_filter`** - lista de bloqueio de URLs que não devem ser submetidas a crawl, em formato de expressão regular. O Data Crawler não efetuará crawl de URLs que correspondam a qualquer uma das expressões regulares fornecidas.

    A `domain list` contém os domínios que não podem ser submetidos a crawl. Adicione-o, se necessário.

    A `filetype list` contém as extensões de arquivo que o Serviço de Orquestração não suporta.

    Remova quaisquer tipos de arquivos suportados das expressões regulares.

    Assegure-se de que o domínio da URL inicial seja permitido pelo filtro. Use um filtro vazio para o comportamento `allow everything`.

    Assegure-se de que a URL inicial não seja excluída por um filtro ou o Crawler poderá ser interrompido.

-   **`max_text_size`** - o tamanho máximo, em bytes, que um documento pode ter antes de ser gravado no disco pelo Connector Framework. Ajustar isso para um valor maior diminui a quantia de documentos gravados em disco, mas aumenta o requisito de memória. O valor padrão é
`1048576`
-   **`extra_vm_params`** - permite incluir parâmetros Java extras no comando usado para ativar o Connector Framework.

-   **`bootstrap_logging`** - grava o log de inicialização da estrutura do conector; útil somente para depuração avançada. Os valores possíveis são `true`
ou `false`. O arquivo de log será gravado em `crawler_temp_dir`

-   **`read-timeout`** - configura o tempo (em segundos) que o crawler aguardará por uma resposta da estrutura do conector. O valor padrão é 5 segundos.

### Adaptador de saída
{: #output-adapter}

-   **`class`** - define a classe do adaptador de saída do Data Crawler.
-   **`config`** - define qual chave de configuração será transmitida para o adaptador de saída. A sequência deve corresponder a uma chave dentro desse objeto de configuração. No exemplo de código a seguir:

    ```
    classe - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

    configuração - "discovery_service"

    discovery_service {
        incluir "discovery/discovery_service.conf" }
    ```
    {: codeblock}

    a chave de configuração é `discovery_service`.

Deve-se selecionar um adaptador de saída especificando seu parâmetro `class` e a chave `config`.

-   **{{site.data.keyword.discoveryshort}} Service Output Adapter** - faz upload de documentos submetidos a crawl para o {{site.data.keyword.discoveryfull}} Service. Selecione esse adaptador configurando o parâmetro `class` e a chave `config` como a seguir.

```
class - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

config - "discovery_service"

discovery_service {
            incluir "discovery/discovery_service.conf" }
```
{: codeblock}

-   **Test Output Adapter** - o Test Output Adapter grava uma representação de arquivos submetidos a crawl no disco em um local especificado. Selecione esse adaptador configurando o parâmetro `class` e a chave `config` como a seguir.

    Um parâmetro adicional, `output_directory`, seleciona o diretório no qual a representação de dados submetidos a crawl deve ser gravada.

```
class - "com.ibm.watson.crawler.testoutputadapter.TestOutputAdapter"

config - "test"

output_directory - "/tmp/crawler-test-output"`
```
{: codeblock}

-   **`retry`** - especifica as opções para tentar novamente em caso de tentativas com falha de envio por push para o adaptador de saída.

    -   `max_attempts` - número máximo de novas tentativas. O valor padrão é `10`
    -   `delay` - quantia mínima de atraso entre tentativas, em segundos. O valor padrão é `2`
    -   `exponent_base` - fator que determina o crescimento do tempo de atraso sobre cada tentativa com falha. O valor padrão é `2`

    A fórmula é:

        **`d(nth_retry) - delay * (exponent_base ^ nth_retry)`**

    Por exemplo, as configurações padrão com um atraso de 1 segundo e um expoente de base 2 fazem com que a segunda nova tentativa, ou seja, a terceira tentativa, atrase 2 segundos em vez de 1 e que a próxima tentativa atrase 4 segundos.

        `d(0) - 1 * (2 ^ 0)` - 1 segundo
        `d(1) - 1 * (2 ^ 1)` - 2 segundos
        `d(2) - 1 * (2 ^ 2)` - 4 segundos

    Assim, com as configurações padrão, um envio será tentado até 10 vezes, aguardando no máximo cerca de 1.022 segundos, ou seja, um pouco mais de 17 minutos. Esse tempo é aproximado porque há um tempo adicional incluído para evitar que múltiplos reenvios sejam executados simultaneamente. Este tempo "difuso" é de até 10%, de modo que a última nova tentativa no exemplo anterior pode atrasar até 7,7 segundos. O tempo de espera não inclui o tempo gasto conectando-se ao serviço, fazendo upload de dados ou aguardando por uma resposta.

    O valor de `output_timeout` tem precedência sobre o tempo de espera aqui: se o tempo de espera total de nova tentativa exceder essa configuração, o envio falhará, mesmo que tenha sido tentado novamente.
    {: tip}

### Opções adicionais de gerenciamento de crawl
{: #additional-crawl-management-options}

-   **`full_node_debugging`** - ativa o modo de depuração; os valores possíveis são `true` ou `false`.

    **Importante:** isso colocará os dados completos de cada documento submetido a crawl nos logs.   

-   **`logging.log4j.configuration_file`*** - o arquivo de configuração a ser usado para criação de log. No arquivo de amostra `crawler.conf`, essa opção é definida em `logging.log4j` e seu valor padrão é `log4j_custom.properties`. Essa opção deve ser definida de maneira semelhante, independentemente se usar o arquivo `.properties` ou `.conf`.   
-   **`shutdown_timeout`** - especifica o valor de tempo limite, em minutos, antes de encerrar o aplicativo. O valor padrão é `10`.   
-   **`output_limit`** - o número mais alto de itens indexáveis que o Crawler tentará enviar simultaneamente para o adaptador de saída. Isso pode ser limitado ainda mais pelo número de núcleos disponíveis para fazer o trabalho. Ele informa que em um determinado ponto qualquer no máximo "x" itens indexáveis serão enviados ao adaptador de saída que está aguardando o retorno. O valor padrão é `10`.   
-   **`input_limit`** - limita o número de URLs que podem ser solicitadas por meio do adaptador de entrada de uma vez. O valor padrão é  ` 30 `.   
-   **`output_timeout`** - a quantia de tempo, em segundos, antes que o Data Crawler desista de uma solicitação ao adaptador de saída e, em seguida, remova o item da fila do adaptador de saída para permitir mais processamento. O valor padrão é `1200`.

    Considerações devem ser fornecidas para as restrições impostas pelo adaptador de saída, já que essas restrições podem estar relacionadas com os limites definidos aqui. O `output_limit` definido está relacionado à quantia de objetos indexáveis que podem ser enviados ao adaptador de saída de uma vez. Quando um objeto indexável é enviado ao adaptador de saída, ele está "dentro do horário", conforme definido pela variável `output_timeout`. É possível que o próprio adaptador de saída tenha um regulador que o impeça de processar tantas entradas quantas ele recebe. Por exemplo, o adaptador de saída de orquestração pode ter um conjunto de conexões,configurável para conexões HTTP para o serviço. Se ele for padronizado como 8, por exemplo, e se você configurar o `output_limit` para um número maior que 8, então haverá processos, dentro do horário, aguardando sua vez para serem executados. Em seguida, podem ocorrer tempos limites.   
-   **`num_threads`** - o número de encadeamentos paralelos que podem ser executados de uma vez. Esse valor pode ser um número inteiro, que especifica o número de encadeamentos paralelos diretamente, ou pode ser uma sequência com o formato `"xNUM"`, especificando o fator de multiplicação do número de processadores disponíveis, por exemplo, `"x1.5"`. O valor padrão é `"30"`

## Configurando opções de serviço
{: #configuring-service-options}

O serviço do {{site.data.keyword.discoveryshort}} instrui o crawler como gerenciar arquivos submetidos a crawl quando usar o serviço do {{site.data.keyword.discoveryfull}}.

Para acessar o manual no produto para o arquivo `discovery-service.conf`, com as informações mais atualizadas, digite o comando a seguir no diretório de instalação do Crawler:

  ```bash
  man discovery_service.conf
  ```
  {: pre}
{: tip}

As opções padrão podem ser mudadas diretamente abrindo o arquivo `config/discovery/discovery_service.conf` e definindo os valores a seguir, específicos para seu caso de uso:

-   **`http_timeout`** - o tempo limite, em segundos, para a operação de leitura/índice do documento; o padrão é `125`.
-   **`proxy_host_port`** - (opcional) ao executar o crawler de dados atrás de um firewall, pode ser necessário configurar o nome do host do proxy e o número da porta do proxy para que o crawler de dados converse com o serviço do {{site.data.keyword.discoveryshort}}. O valor padrão para essa opção é uma sequência vazia e, se precisar mudá-lo, o valor deverá estar no formato
`"<host>:<port>"`.
-   **`concurrent_upload_connection_limit`** - o número de conexões simultâneas permitidas para fazer upload de documentos. O padrão é `2`.

    **Nota:** ao usar o Orchestration Service Output Adapter, esse número deve ser maior que ou igual ao `output_limit` definido ao configurar opções de crawl.   

-   **`base_url`** - a URL para a qual os documentos submetidos a crawl serão enviados. Para a liberação atual do serviço do {{site.data.keyword.discoveryshort}}, o valor é `https://gateway.watsonplatform.net/discovery/api`.   
-   **`environment_id`** - o local de sua coleção de documentos submetidos a crawl na URL base.   
-   **`collection_id`** - o nome da coleção de documentos que você configurou no serviço do {{site.data.keyword.discoveryshort}}.
-   **`api_version`** - somente para uso interno. Data da última mudança de versão da API.   
-   **`configuration_id`** - o nome do arquivo de configuração que o serviço do {{site.data.keyword.discoveryshort}} utiliza.
-   **`apikey`** - Credencial para autenticar no local de sua coleção de documentos submetidos a crawl.

O {{site.data.keyword.discoveryshort}} Service Output Adapter pode enviar estatísticas para que o {{site.data.keyword.IBM}} entenda e atenda melhor seus usuários. As opções a seguir podem ser configuradas para a variável `send_stats`:

-   **`jvm`** - as estatísticas da Java virtual machine (JVM) enviadas incluem o fornecedor e a versão Java, conforme relatado pela JVM usada para executar o Data Crawler. O valor é `true` ou `false`. O valor padrão é `true`.
-   **`os`** - as estatísticas do sistema operacional (OS) enviadas incluem o nome, a versão e a arquitetura do OS, conforme relatado pela JVM usada para executar o Data Crawler. O valor é `true` ou `false`. O valor padrão é `true`.
