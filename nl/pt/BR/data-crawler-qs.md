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

# Introdução ao Data Crawler
{: #getting-started-with-the-data-crawler}

Este tópico explica como usar o Data Crawler para alimentar arquivos de seu sistema de arquivos local,
para uso com o serviço do {{site.data.keyword.discoveryfull}}.
{: shortdesc}

O Data Crawler deve ser usado apenas para efetuar crawl de compartilhamentos de arquivo ou bancos de dados; em todos os outros casos, é necessário usar o conector apropriado do {{site.data.keyword.discoveryshort}}. Veja [Conectando a origens de dados](/docs/services/discovery?topic=discovery-sources#sources) para obter detalhes. A assistência não será mais fornecida para o Data Crawler se você estiver usando-o com uma origem de dados suportada pelos conectores do {{site.data.keyword.discoveryshort}}.
{: important}

Antes de tentar esta tarefa, crie uma instância do serviço do {{site.data.keyword.discoveryshort}}
no {{site.data.keyword.Bluemix}}. Para concluir este guia, será necessário usar as credenciais que
estão associadas à instância do serviço que você criou.

## Crie um ambiente
{: #dc-create-environment}

Use o método bash POST /v1/environments para criar um ambiente. Pense no ambiente como o warehouse em que você está armazenando todas as suas caixas de documentos. O exemplo a seguir cria um ambiente que é chamado `my-first-environment`:

Substitua  ` { `  por suas credenciais de serviço.

(Para obter informações mais detalhadas sobre o uso de credenciais {apikey}, consulte [Introdução à API](/docs/services/discovery?topic=discovery-gs-api#gs-api).)

```bash
curl -X POST -u "apikey:{apikey}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
```
{: pre}

A API
retorna uma resposta que inclui informações, como seu ID de ambiente, status do ambiente e quanto armazenamento o ambiente está usando. Não vá para a próxima etapa até que o status do ambiente seja `ready`. Ao criar o ambiente, se o status retornar `status:pending`, use o método `GET /v1/environments/{environment_id}` para verificar o status até que esteja pronto. Neste exemplo, substitua `{apikey}` por suas credenciais de serviço e substitua `{environment_id}` por seu ID de ambiente que foi retornado quando você criou o ambiente.

```bash
curl -u "apikey: {1}/environments/ {2}{0}{1}{7}-11-07
```
{: pre}

## Crie uma coleção
{: #dc-create-collection}

Em seguida, use o método `POST
/v1/environments/{environment_id}/collections` para
criar uma coleção. Pense em uma coleção como uma caixa na qual você armazena os documentos em seu ambiente. Este exemplo cria uma coleção que é chamada
`my-first-collection` no ambiente que você criou na etapa anterior e usa a configuração padrão a seguir:

-   Substitua  ` { `  por suas credenciais de serviço.
-   Substitua `{environment_id}` pelo ID do ambiente que você criou na etapa 1.

Antes de
criar uma coleção, deve-se obter o ID de sua configuração padrão. Para
localizar seu `configuration_id` padrão, use o método
`GET /v1/environments/{environment_id}/configurations`:

```bash
curl -u "apikey: {1}/environments/ {2}{0}{1}{7}-11-07
```
{: pre}

Depois de ter o ID de configuração padrão, use-o para criar sua
coleção. Substitua `{configuration_id}` pelo ID de configuração padrão para o seu ambiente.

```bash
curl -X POST -u "apikey:{apikey}" -H "Content-Type: application/json" -d '{"name": "my-first-collection", "description": "exploring collections", "configuration_id":"{configuration_id}" , "language": "en_us"}' https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07
```
{: pre}

A API retorna uma resposta que inclui informações, como o ID e o status da coleção e a quantia de armazenamento que ela está usando. Não vá para a próxima etapa até que o status da sua coleção seja `online`. Ao criar a coleção, se o status retornar
`status:pending`, use o método `GET /v1/environments/{environment_id}/collections/{collection_id}`
para verificar o status até que ele seja ready. Neste exemplo, substitua `{apikey}` por suas credenciais de serviço, substitua `{environment_id}` por seu ID de ambiente e substitua `{collection_id}` pelo ID de coleção que foi retornado anteriormente nessa etapa.

```bash
curl -u "apikey: {1}/environments/ {2}{0}{1}{7}-11-07
```
{: pre}

## Faça download de documentos de exemplo
{: #dc-download-documents}

Faça download destes documentos:

-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo"></a>
-   <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo"></a>

## Faça download e instale o Data Crawler
{: #download-and-install-the-data-crawler}

1.  Verifique seus pré-requisitos do sistema

    -   Java Runtime Environment versão 8 ou superior

        **Nota:** a variável de ambiente `JAVA_HOME`
deve ser configurada corretamente ou não deve ser configurada para executar o Crawler.
    -   Red Hat Enterprise Linux 6 ou 7 ou Ubuntu Linux 15 ou 16. Para obter um desempenho ideal, o Data Crawler deve executar em sua própria instância do Linux, seja uma máquina virtual, um contêiner ou um hardware.
    -   Mínimo de 2 GB RAM no Sistema Linux

1.  Abra um navegador e efetue login [em sua conta do {{site.data.keyword.Bluemix_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/){: new_window}.
1.  No seu painel do {{site.data.keyword.Bluemix_notm}}, selecione o serviço do {{site.data.keyword.discoveryshort}} criado anteriormente.
1.  Em **Automatizar o upload de conteúdo para o serviço Discovery**, selecione o link de download apropriado para seu sistema (DEB, RPM ou ZIP) para fazer download do Data Crawler.
1.  Como administrador, use os comandos apropriados para instalar o arquivo que transferido por download:

    -   Em sistemas como o Red Hat e o CentOS que usam pacotes rpm, use um comando como o seguinte: `rpm -i /full/path/to/rpm/package/rpm-file-name`
    -   Em sistemas como o Ubuntu e o Debian que usam pacotes deb, use um comando como o seguinte: `dpkg -i /full/path/to/deb/package/deb-file-name`
    -   Os scripts do Crawler são instalados em `{installation directory}/bin`; por exemplo,
`/opt/ibm/crawler/bin`. Assegure-se de que `{installation_directory}/bin` esteja em sua variável de ambiente `PATH` para os comandos do Crawler trabalharem corretamente.

    Os scripts do Crawler também são instalados em `/usr/local/bin`, portanto, isso
também pode ser incluído em sua variável de ambiente `PATH`.
    {: tip}

## Crie seu diretório ativo
{: #dc-working-directory}

Copie o conteúdo do diretório `{installation_directory}/share/examples/config`
para um diretório ativo em seu sistema, por exemplo, `/home/config`.

**Aviso:** não modifique os arquivos de exemplo de configuração fornecidos diretamente. Copie-os e, em seguida, edite-os. Se você editar os arquivos de exemplo no local, sua configuração poderá ser substituída ao fazer upgrade do Data Crawler ou poderá ser removida ao desinstalá-lo.

**Observação:** as referências neste guia aos arquivos no diretório `config`, tal como `config/crawler.conf`, referem-se ao arquivo em seu diretório de trabalho e NÃO no diretório `{installation_directory}/share/examples/config` instalado.

## Configure opções de crawl
{: #dc-configure-crawl-options}

Para configurar o Data Crawler para efetuar crawl em seu repositório, deve-se especificar quais
arquivos do sistema local que você deseja efetuar crawl e para qual
serviço do {{site.data.keyword.discoveryshort}}
deseja enviar a coleção de arquivos submetidos a crawl, uma vez que o crawl foi concluído.

1.  **`filesystem-seed.conf`** - abra o
arquivo `seeds/filesystem-seed.con` em um editor de texto. Modifique o
atributo `value` diretamente no atributo `name-"url"` para o
caminho de arquivo que você deseja efetuar crawl. Por exemplo: `value-"sdk-fs:
///TMP/MY_TEST_DATA/"`

    **Observação:** as URLs devem ser iniciadas com `sdk-fs://`. Portanto, para efetuar crawl, por exemplo, `/home/watson/mydocs`, o valor dessa URL seria
`sdk-fs:///home/watson/mydocs` - a terceira / é necessária!

    Salve e feche o arquivo.

1.  **`discovery_service.conf`** - abra o
arquivo `discovery/discovery_service.conf` em um editor de texto. Modifique os valores a
seguir, específicos para o serviço do {{site.data.keyword.discoveryshort}} que você criou
anteriormente no {{site.data.keyword.Bluemix_notm}}:

    -   `environment_id` - Seu ID de ambiente do serviço do {{site.data.keyword.discoveryshort}}.
    -   `collection_id` - Seu ID de coleção do serviço do {{site.data.keyword.discoveryshort}}.
    -   `configuration_id` - Seu ID de configuração do serviço do {{site.data.keyword.discoveryshort}}.
    -   `configuration` - O local do caminho completo deste arquivo `discovery_service.conf`, por exemplo, `/home/config/discovery/discovery_service.conf`.
    -   ` apikey ` -Credencial para seu serviço do  {{site.data.keyword.discoveryshort}} .
1.  **`crawler.conf`** - abra o
arquivo `config/crawler.conf` em um editor de texto.

    -   Configure as opções `output_adapter` `class` e `config` para o serviço do {{site.data.keyword.discoveryshort}} como a seguir:

        ```bash
        classe - "com.ibm.watson.crawler.discoveryserviceoutputadapter.DiscoveryServiceOutputAdapter"

        configuração - "discovery_service"

        discovery_service {
          incluir "discovery/discovery_service.conf" }
        ```
        {: pre}

1.  Após modificar esses arquivos, você está pronto para efetuar crawl em seus dados.

## Efetue crawl de seus dados
{: #dc-crawl}

Execute o comando a seguir: `crawler crawl --config [config/crawler.conf]`

Isso executará um crawl com o arquivo de configuração `crawler.conf`.

**Nota:** o caminho para o arquivo de configuração aprovado na opção
`-- config` deve ser um caminho qualificado. Ou seja, ele deve estar em formatos relativos,
como `config/crawler.conf` ou `./crawler.conf` ou em um caminho
absoluto, como `/path/to/config/crawler.conf`.

## Procure seus documentos
{: #dc-search}

Finalmente, use o método `GET /v1/environments/{environment_id}/collections/{collection_id}/query`
para procurar sua coleção de documentos. O exemplo a seguir retorna
todas as entidades que são chamadas `IBM`:

-   Substitua  ` { `  por suas credenciais de serviço.
-   Substitua `{environment_id}` pelo ID do ambiente que você criou na etapa 1.
-   Substitua `{collection_id}` pelo ID da coleção que você criou na etapa 2.

```bash
curl -u "apikey:{apikey}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&query-enriched_text.entities.text:IBM'
```
{: pre}

## Resultados
{: #dc-results}

Agora você consultou documentos em um ambiente e criou sua coleção com sucesso. Agora é possível começar
a customização incluindo mais documentos na coleção.
