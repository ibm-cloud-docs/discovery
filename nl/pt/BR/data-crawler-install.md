---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-03"

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

# Fazendo download e instalando o Data Crawler
{: #downloading-and-installing-the-data-crawler}

O Data Crawler coleta os dados brutos que são eventualmente utilizados para formar resultados da procura
para o serviço do {{site.data.keyword.discoveryshort}}. Ao efetuar crawl nos repositórios de dados, o
crawler faz download dos documentos e metadados, começando em uma URL inicial especificada pelo usuário. O crawler descobre documentos em uma hierarquia, ou de outra forma vinculados na URL inicial, e os
enfileira para recuperação.
{: shortdesc}

É possível usar o conjunto de ferramentas do {{site.data.keyword.discoveryshort}} ou a API para efetuar crawl em origens de dados do Box, Salesforce e Microsoft SharePoint Online. Consulte [Conectando-se a origens de dados](/docs/services/discovery/connect.html) para obter mais informações.
{: tip}

## Pré-requisito

-   Java Runtime Environment versão 8 ou superior

    A variável de ambiente `JAVA_HOME` deve ser configurada
corretamente ou não deve ser configurada para executar o Crawler.
    {: tip}
-   Red Hat Enterprise Linux 6 ou 7 ou Ubuntu Linux 15 ou 16. Para obter um desempenho ideal, o Data Crawler deve executar em sua própria instância do Linux, seja uma máquina virtual, um contêiner ou um hardware.

-   Mínimo de 2 GB RAM no Sistema Linux

## Faça download e instale o Data Crawler

1.  Abra um navegador e efetue login na sua conta do [{{site.data.keyword.Bluemix}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net){: new_window}.

1.  No seu painel do {{site.data.keyword.Bluemix_notm}}, selecione o serviço do {{site.data.keyword.discoveryshort}} criado anteriormente.

1.  Na seção **Automatizar o upload de conteúdo para o serviço Discovery**, clique no link apropriado para fazer download do Data Crawler para Linux nos formatos DEB, RPM e ZIP.

1.  Verifique se você está executando o Java Runtime Environment versão 8 ou superior. Execute o comando `java -version` e procure por **1.8**. Se você estiver executando algo anterior à versão **1.8**, será necessário fazer upgrade do Java instalando o Java Developer Kit (JDK) 8 no seu sistema de gerenciamento de pacote, por meio do website [IBM JDK ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/developerworks/java/jdk/){: new_window} ou por meio do [java.com ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.java.com){: new_window}.

    A variável de ambiente `JAVA_HOME` deve ser configurada corretamente ou não deve ser configurada para executar o Crawler.
    {: tip}

1.  Como administrador, use os comandos apropriados para instalar o arquivo que transferido por download:

    -   Em sistemas como o Red Hat e o CentOS que usam pacotes rpm, use um comando como o seguinte: `rpm -i /full/path/to/rpm/package/rpm-file-name`
    -   Em sistemas como o Ubuntu e o Debian que usam pacotes deb, use um comando como o seguinte: `dpkg -i /full/path/to/deb/package/deb-file-name`
    -   Os scripts do Crawler são instalados em `{installation_directory}/bin`; por exemplo, `/opt/ibm/crawler/bin`. Assegure-se de que `{installation_directory}/bin` esteja em sua variável de ambiente `PATH` para os comandos do Crawler trabalharem corretamente.

    Os scripts do Crawler também são instalados em `/usr/local/bin`, portanto, isso também pode ser incluído em sua variável de ambiente `PATH`.
    {: tip}
1.  Crie seu diretório ativo copiando o conteúdo do diretório `{installation_directory}/share/examples/config` para um diretório ativo em seu sistema, por exemplo, `/home/config`.

    **Aviso:** não modifique os arquivos de exemplo de configuração fornecidos diretamente. Copie-os e, em seguida, edite-os. Se você editar os arquivos de exemplo no local, sua configuração poderá ser substituída ao fazer upgrade do Data Crawler ou poderá ser removida ao desinstalá-lo.

    **Nota:** as referências no restante deste guia aos arquivos no diretório `config`, como `config/crawler.conf`, referenciam esse arquivo em seu diretório ativo, NÃO no diretório `{installation_directory}/share/examples/config` instalado.

1.  Agora você está pronto para [configurar o Data Crawler para conectar-se ao seu repositório](/docs/services/discovery/data-crawler-seeds.html)

## Estrutura do Data Crawler

O download do Data Crawler coloca as seguintes pastas em seu sistema:

-   `doc` - contém arquivos com informações sobre direitos autorais e licença.
-   `bin` - arquivos de script para executar o crawler.
-   `connectorFramework` - os arquivos neste diretório são aqueles que permitem conversar com seus dados, sejam dados internos dentro da empresa ou dados externos na web ou na nuvem.
-   `lib` - arquivos de biblioteca utilizados pelo crawler.
-   `Compartilhar`
    -   `doc` - fornece arquivos de documentação formatados com HTML ou Markdown.
    -   `examples/config` - arquivos que permitem informar ao crawler quais dados devem ser usados para seu crawl, o local para enviar sua coleção de dados submetidos a crawl quando o crawl tiver sido concluído e outras opções de gerenciamento de crawl.
    -   `man` - documentação do crawler da página de manual no produto.

## Limitações conhecidas nesta liberação

-   O Data Crawler pode ser interrompido ao executar o conector do sistema de arquivos com uma URL inválida ou ausente.
-   Configure o valor de `urls_to_filter` no arquivo `crawler.conf`, de forma que todas as URLs ou RegExes da lista de desbloqueio sejam incluídas em uma expressão RegEx única. Consulte [Configurando
opções de crawl](/docs/services/discovery/data-crawler-discovery.html#configuring-crawl-options) para obter mais informações.
-   O caminho para o arquivo de configuração aprovado na opção `-- config -c` deve ser um caminho qualificado. Ou seja, ele deve estar nos formatos relativos `config/crawler.conf` ou `./crawler.conf` ou no caminho absoluto `/path/to/config/crawler.conf`. A especificação somente de `crawler.conf` será possível apenas se o arquivo `orchestration_service.conf` estiver sequenciado em vez de referenciado usando `include` no arquivo `crawler.conf`.
