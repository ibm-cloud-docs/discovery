---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-25"

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

# Configurando opções do conector e de valor inicial

Ao efetuar crawl de dados, o crawler primeiramente identifica o tipo de repositório de dados (conector)
e o local de início especificado pelo usuário (valor inicial) para começar o download de informações.
{: shortdesc}

**Importante:** ao utilizar o Data Crawler, as configurações de segurança do
repositório de dados são ignoradas.

Valores iniciais são os pontos de início de um crawl e são usados pelo Data Crawler para recuperar dados
do recurso que é identificado pelo conector. Geralmente, os valores iniciais configuram URLs para acessar
recursos baseados em protocolo, como compartilhamentos de arquivos, compartilhamentos SMB, bancos de dados e
outros repositórios de dados que são acessíveis por vários protocolos. Além disso, diferentes URLs de
valores iniciais possuem diferentes recursos. Os valores iniciais também podem ser específicos do repositório,
para ativar a execução de crawl de aplicativos de terceiros específicos, tais como sistemas Customer
Relationship Management (CRM), sistemas Product Life Cycle (PLC), sistemas de gerenciamento de conteúdo
(CMS), aplicativos baseados em nuvem e aplicativos de bancos de dados na web.

Para efetuar crawl de seus dados corretamente, assegure-se de que o Crawler esteja
configurado corretamente para ler seu repositório de dados. O Data Crawler fornece conectores para suportar a
coleta de dados nos seguintes repositórios:

-   [Sistema de
arquivos](/docs/services/discovery/data-crawler-seeds.html#configuring-filesystem-crawl-options)
-   [Bancos de
dados, por meio de JDBC](/docs/services/discovery/data-crawler-seeds.html#configuring-database-crawl-options)
-   [CMIS (Content Management Interoperability Services)](/docs/services/discovery/data-crawler-seeds.html#configuring-cmis-crawl-options)
-   [Compartilhamentos
de arquivo SMB (Server Message Block), CIFS (Common Internet Filesystem) ou Samba](/docs/services/discovery/data-crawler-seeds.html#configuring-smbcifssamba-crawl-options)
-   [SharePoint
e SharePoint Online](/docs/services/discovery/data-crawler-seeds.html#configuring-sharepoint-crawl-options)
-   [Box](/docs/services/discovery/data-crawler-seeds.html#configuring-box-crawl-options)

Um modelo de configuração do conector também é fornecido, o que permite customizar um conector.

Para configurar seu conector, faça o seguinte:

1.  Abra o arquivo no diretório `connectors` que corresponde ao repositório
ao qual você está se conectando (por exemplo, `filesystem.conf` é o arquivo de configuração para o
conector do sistema de arquivos) em um editor de texto.

1.  Modifique os valores que sejam apropriados para seu repositório:

    -   [Sistema
de arquivos](/docs/services/discovery/data-crawler-seeds.html#filesystem-crawl-options)
    -   [Bancos de
Dados, por meio de JDBC](/docs/services/discovery/data-crawler-seeds.html#database-crawl-seed)
    -   [CMIS (Content Management Interoperability Services)](/docs/services/discovery/data-crawler-seeds.html#cmis-crawl-options)
    -   [Compartilhamentos
de arquivo SMB (Server Message Block), CIFS (Common Internet Filesystem) ou Samba](/docs/services/discovery/data-crawler-seeds.html#smb-cifs-samba-crawl-options)
    -   [SharePoint
e SharePoint Online](/docs/services/discovery/data-crawler-seeds.html#sharepoint-crawl-options)
    -   [Box](/docs/services/discovery/data-crawler-seeds.html#box-crawl-options)
1.  Salve e feche o arquivo.
1.  Repita para o arquivo `-seed.conf` no diretório `connectors/seeds`
que corresponde ao repositório ao qual você está se conectando (por exemplo,
`filesystem-seed.conf` é o arquivo de configuração de valor inicial (a que conectar-se)
para o conector de sistema de arquivos) em um editor de texto.
1.  Continue com [configurando o Data
Crawler para conectar-se ao {{site.data.keyword.discoveryshort}}](/docs/services/discovery/data-crawler-discovery.html).

Para acessar o manual no produto para os arquivos de configuração do conector e de valor inicial, com as
informações mais atualizadas, digite os seguintes comandos no diretório de instalação do Crawler:
-   Para obter opções de configuração do conector:
    ```bash
    man crawler-options.conf
    ```
    {: pre}
-   Para obter opções de configuração de valor inicial de crawl:
    ```bash
    man crawler-seed.conf
    ```
    {: pre}


## Configurando opções de crawl de sistema de arquivos
{: #filesystem-crawl-options}

O conector do sistema de arquivos permite efetuar o crawl de arquivos locais para a instalação do Data
Crawler.

### Configurando o conector do sistema de arquivos

A seguir estão as opções de configuração básica que são necessárias para usar o conector do
sistema de arquivos. Para configurar esses valores, abra o arquivo
`config/connectors/filesystem.conf` e modifique os valores a seguir, que são específicos para
seus casos de uso:

-   **`protocol`** - O nome do protocolo do conector usado para o crawl. Use `sdk-fs` para esse conector.
-   **`collection`** - Esse atributo é usado para descompactar arquivos temporários. O valor padrão é `crawler-fs`
-   **`logging-config`** - Especifica o arquivo usado para configurar as opções de criação de log; ele deve ser formatado como uma sequência XML `log4j`.
-   **`classname`** - Classe Java para o conector. O valor para
usar esse conector deve ser `plugin:filesystem.plugin@filesystem`.

### Configurando o valor inicial de crawl do sistema de arquivos

Os valores a seguir podem ser configurados para o arquivo de valor inicial de crawl do sistema de
arquivos. Para configurar esses valores, abra o arquivo `config/seeds/filesystem-seed.conf` e
defina os valores a seguir, que são específicos para os casos de uso:

-   **`url`** - lista separada por quebras de linha de arquivos e
pastas para efetuar crawl. Os usuários do UNIX podem usar um caminho como `/usr/local/`.

    **Observação:** as URLs devem ser iniciadas com `sdk-fs://`. Portanto, para efetuar crawl, por exemplo, `/home/watson/mydocs`, o valor dessa URL seria
`sdk-fs:///home/watson/mydocs` - a terceira `/` é necessária!

    Os sistemas de arquivos usados por sistemas de computadores do tipo Linux, UNIX e UNIX
podem conter tipos especiais de arquivos, como nós e arquivos de dispositivo de bloco e de caracteres que
representam canais nomeados, que não podem ser submetidos a crawl porque eles não contêm dados, mas servem como
pontos de acesso de dispositivo ou de E/S. A tentativa de efetuar crawl desses arquivos gera erros
durante o crawl. Para evitar esses erros, é necessário excluir o diretório `/dev` em qualquer
crawl de nível superior em um sistema de arquivos do tipo Linux, UNIX ou UNIX. Se ele estiver presente no sistema
no qual você está efetuando crawl, também será necessário excluir diretórios do sistema temporários, como
`/proc`, `/sys` e `/tmp`, que contêm arquivos temporários
e informações do sistema.   **`hops`** - Somente uso interno.   **`default-allow`** - Somente uso interno.
    {: tip}

## Configurando opções de crawl do banco de dados

O conector de banco de dados permite efetuar crawl de um banco de dados executando um comando SQL
customizado e criando um documento por linha (registro) e um elemento de conteúdo por coluna (campo). É
possível especificar uma coluna a ser usada como uma chave exclusiva, bem como uma coluna que contenha um
registro de data e hora que representa a data da última modificação de cada registro. O conector recupera
todos os registros do banco de dados especificado e também pode estar restrito às tabelas, junções,
e assim por diante, específicas na instrução SQL.

O conector do banco de dados permite efetuar crawl dos bancos de dados a seguir:

-   {{site.data.keyword.IBM}} DB2
-   MySQL
-   Oracle PostgreSQL
-   Microsoft SQL Server
-   Sybase
-   Outros bancos de dados compatíveis com SQL, por meio de um driver compatível com JDBC 3.0

O conector recupera todos os registros da tabela e do banco de dados especificados.

***Drivers JDBC*** - o conector do banco de dados é enviado com o
driver Oracle JDBC (Java Database Connectivity) versão 1.5. Todos os drivers JDBC de terceiros fornecidos com
o Data Crawler estão localizados no diretório
`connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` de sua
instalação do Data Crawler, no qual é possível incluí-los, removê-los e modificá-los conforme necessário. Também é possível usar a configuração `extra_jars_dir` no
arquivo `crawler.conf` para especificar outro local.

***Drivers DB2 JDBC*** - o Data Crawler não é fornecido com os
drivers JDBC para DB2 devido a problemas de licenciamento. No entanto, todas as instalações do DB2 nas quais
você instalou o suporte JDBC incluem os arquivos JAR que o Data Crawler requer, a fim de poder efetuar crawl
de uma instalação do DB2. Para efetuar crawl de uma instância do DB2, deve-se copiar estes arquivos para o
diretório apropriado em sua instalação do Data Crawler, para que o conector do banco de dados possa
utilizá-los. Para permitir que o Data Crawler efetue crawl de uma instalação do DB2, localize os
arquivos JAR `db2jcc.jar` e de licença (geralmente, `db2jcc_license_cu.jar`)
em sua instalação do DB2 e copie esses arquivos para o subdiretório
`connectorFramework/crawler-connector-framework-#.#.#/lib/java/database` do
diretório de instalação do seu Data Crawler ou é possível usar a configuração
`extra_jars_dir` no arquivo `crawler.conf` para especificar outro local.

***Drivers JDBC MySQL*** - o Data Crawler não é fornecido com os
drivers JDBC para MySQL devido a possíveis problemas de licença, caso eles foram entregues como parte
do produto. No entanto, o download do arquivo JAR que contém os drivers JDBC MySQL e a integração desse arquivo
JAR em sua instalação do Data Crawler são muito fáceis de fazer:

1.  Use um navegador da web para visitar o site de download do MySQL e localize a origem e o link de
download binário para o formato de archive que você deseja usar (geralmente zip para sistemas Microsoft
Windows ou um tarball compactado com gzip para sistemas Linux). Clique nesse link para iniciar o processo de
download. O registro pode ser necessário.
1.  Use um comando archive-file-name ou tar zxf archive-file-name de descompactação de arquivo zip
apropriado para extrair o conteúdo desse archive, com base no tipo e no nome do archive que você faz download.
1.  Mude para o diretório que foi extraído do archive e copie o arquivo JAR deste
diretório para o subdiretório `connectorFramework/crawler-connector-framework-#.#.#/lib/java/database`
do diretório de instalação do seu Data Crawler ou é possível usar a configuração
`extra_jars_dir` no arquivo `crawler.conf` para especificar
outro local.

### Configurando o conector do banco de dados

A seguir estão as opções de configuração básica que são necessárias para usar o conector do banco de
dados. Para configurar esses valores, abra o arquivo config/connectors/database.conf e modifique os
valores a seguir, que são específicos para seus casos de uso:

-   **`protocol`** - O nome do protocolo do conector usado para o crawl. O valor para esse conector é baseado no sistema de banco de dados a ser acessado.
-   **`collection`** - Esse atributo é usado para descompactar arquivos temporários.
-   **`classname`** - Classe Java para o conector. O valor para
usar esse conector deve ser `plugin:database.plugin@database`.
-   **`logging-config`** - Especifica o arquivo usado para configurar as opções de criação de log; ele deve ser formatado como uma sequência XML `log4j`.

### Configurando o valor inicial de crawl do banco de dados
{: #database-crawl-seed}

Os valores a seguir podem ser configurados para o arquivo inicial de crawl do banco de dados. Para configurar esses valores, abra o arquivo `config/seeds/database-seed.conf` e defina
os valores a seguir, que são específicos para os casos de uso:

-   **`url`** - a URL da tabela ou da visualização a ser recuperada. Define sua URL inicial do banco de dados SQL customizado. A estrutura é:

    -   `database-system://host:port/database?[per=num]&[sql=SQL]`

    O teste de uma URL inicial mostra todas as URLs enfileiradas. Por exemplo, o teste da URL a
seguir para um banco de dados que contém 200 registros:
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?per=100&sql=select%20*%20from%20vessel&`

    mostra as URLs enfileiradas a seguir:
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=0&`
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=100&`
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?key-val=200&`

    O teste da URL a seguir mostra os dados recuperados da linha 43:
    -   `sqlserver://test.mycompany.com:1433/WWII_Navy/?per-1&key-val=43`
-   **`hops`** - Somente uso interno.
-   **`default-allow`** - Somente uso interno.
-   **`user-password`** - credenciais para o sistema de banco de
dados. O nome de usuário e a senha precisam ser separados por um `:` e a senha deve ser
criptografada usando o programa vcrypt fornecido com o Data Crawler. Por exemplo:
`username:[[vcrypt/3]]passwordstring`
-   **`max-data-size`** - tamanho máximo dos dados para um
documento. Esse é o maior bloco de memória que será carregado de uma vez. Aumente esse limite somente se você tiver memória suficiente em seu computador.
-   **`filter-exact-duplicates`** - somente para uso interno.
-   **`timeout`** - somente para uso interno.
-   **`jdbc-class`** (opção do extensor) - quando especificada,
essa sequência substitui a classe JDBC usada pelo conector quando `(other)` é escolhido
como o sistema de banco de dados.
-   **`connection-string`** (opção do extensor) - quando
especificada, essa sequência substitui a sequência de conexões JDBC gerada automaticamente. Isso permite fornecer uma configuração mais detalhada sobre a conexão com o banco de dados, como balanceamento
de carga ou conexões SSL. Por exemplo: `jdbc:netezza://127.0.0.1:5480/databasename`
-   **`save-frequency-for-resume`** (opção do extensor) -
especifica o nome de uma coluna ou de um rótulo associado para poder continuar um crawl ou executar uma
atualização parcial. O valor inicial salva o nome dessa coluna em intervalos regulares conforme ele continua
com o crawl e o salva novamente quando a última linha de seu banco de dados é submetida a crawl. Ao continuar o
crawl ou atualizá-lo, o crawl inicia com a linha que é identificada no valor salvo para este campo

## Configurando opções de crawl do CMIS
{: #cmis-crawl-options}

O conector CMIS (Content Management Interoperability Services) permite efetuar crawl de repositórios
CMS (Content Management System) habilitados para CMIS, como Alfresco, Documentum ou
{{site.data.keyword.IBM}} Content Manager, e indexar os dados que eles contêm.

### Configurando o conector CMIS

A seguir estão as opções de configuração básica que são necessárias para usar o conector CMIS. Para
configurar esses valores, abra o arquivo `config/connectors/cmis.conf` e defina os
valores a seguir, que são específicos para os casos de uso:

-   **`protocol`** - O nome do protocolo do conector usado para o crawl. O valor para usar esse conector deve ser `cmis:document`.
-   **`collection`** - Esse atributo é usado para descompactar arquivos temporários.
-   **`dns`** - opção não utilizada.
-   **`classname`** - Classe Java para o conector. Use
`plugin:cmis-v1.1.plugin@connector` para esse conector.
-   **`logging-config`** - Especifica o arquivo usado para configurar as opções de criação de log; ele deve ser formatado como uma sequência XML `log4j`.
-   **`endpoint`** - a URL do terminal em serviço de um repositório
compatível com CMIS. Por exemplo, as estruturas da URL para SharePoint são:

    -   Para ligação AtomPub: `http://yourserver/_vti_bin/cmis/rest?getRepositories`
    -   Para ligação de WebServices: `http://yourserver/_vti_bin/cmissoapwsdl.aspx`
-   **`username`** - o nome do usuário do repositório
CMIS usado para acessar o conteúdo. Esse usuário deve ter acesso a todas as pastas e documentos de destino a
serem submetidos a crawl e indexados.
-   **`password`** - a senha do repositório CMIS usada para acessar
o conteúdo. A senha NÃO deve ser criptografada; ela deve ser fornecida em texto simples.
-   **`repositoryid`** - o ID do repositório CMIS usado para acessar
o conteúdo para esse repositório específico.
-   **`bindingtype`** - identifica qual tipo de ligação deve ser
usado para conectar-se a um repositório CMIS. O valor pode ser AtomPub ou WebServices.
-   **`authentication`** - identifica qual tipo de mecanismo de
autenticação deve ser usado ao entrar em contato com um repositório compatível com CMIS: Autenticação HTTP
Básica, NTLM ou WS-Security (token do nome de usuário).
-   **`enable-acl`** - permite recuperar as ACLs para dados
submetidos a crawl. Se você não estiver preocupado com a segurança dos documentos nesta coleção, a desativação
dessa opção aumentará o desempenho por não solicitar essas informações com o documento e por não recuperar e
codificar essas informações. O valor é true ou false.
-   **`user-agent`** - Um cabeçalho enviado ao servidor ao efetuar crawl em documentos.
-   **`method`** - o método (GET ou POST) pelo qual os parâmetros
serão passados.
-   **`url-logging`** - A extensão para a qual as URLs com crawl são registradas. Os valores possíveis são:

    -   `full-logging` - Registre todas as informações sobre a URL.
    -   `refined-logging` - Basta registrar as informações necessárias para navegar no log do crawler e para que o conector funcione corretamente; esse é o valor padrão.
    -   `minimal-logging` - Basta registrar a quantidade mínima de informações necessárias para que o conector funcione corretamente.

    Configurar essa opção como `minimal-logging` reduzirá o tamanho dos logs e ganhará um leve aumento de desempenho devido à E/S menor associada com a minimização da quantidade de dados que estão sendo registrados.
-   **`ssl-version`** - Especifica uma versão de SSL para usar para conexões HTTPS. Por padrão, o protocolo mais forte disponível é usado.

### Configurando o valor inicial de crawl do CMIS

Os valores a seguir podem ser configurados para o arquivo inicial de crawl do CMIS. Para configurar
esses valores, abra o arquivo `config/seeds/cmis-seed.conf` e modifique os valores a seguir,
que são específicos para os casos de uso:

-   **`url`** - a URL de uma pasta do repositório CMIS a ser
usada como um ponto de início do crawl, por exemplo:
`cmis://alfresco.test.com:8080/alfresco/cmisatom?folderToProcess-workspace://SpacesStore/guid`

    Para efetuar crawl na pasta raiz, é necessário fornecer a URL como:
`cmis://alfresco.test.com:8080/alfresco/cmisatom?folderToProcess-`
-   **`at`** - opção não utilizada.
-   **`default-allow`** - Somente uso interno.

## Configurando opções de crawl SMB/CIFS/Samba
{: #smb-cifs-samba-crawl-options}

O conector Samba permite efetuar crawl dos compartilhamentos de arquivos Server Message Block (SMB) e
Common Internet Filesystem (CIFS). Esse tipo de compartilhamento é comum em redes Windows e também é
fornecido por meio do projeto de software livre Samba.

### Configurando o conector Samba

A seguir estão as opções de configuração básica que são necessárias para usar o conector Samba. Para
configurar esses valores, abra o arquivo `config/connectors/samba.conf` e defina os
valores a seguir, que são específicos para os casos de uso:

-   **`protocol`** - O nome do protocolo do conector usado para o crawl. O valor para usar esse conector é smb.
-   **`collection`** - Esse atributo é usado para descompactar arquivos temporários.
-   **`classname`** - Classe Java para o conector. O valor para
usar esse conector deve ser `plugin:smb.plugin@connector`.
-   **`logging-config`** - Especifica o arquivo usado para configurar as opções de criação de log; ele deve ser formatado como uma sequência XML `log4j`.
-   **`username`** - o nome do usuário do Samba com o qual
autenticar-se. Se fornecido, o domínio e a senha também devem ser fornecidos. Se não fornecido, a conta
guest é usada.
-   **`password`** - a senha para autenticar-se com o Samba. Se o
nome do usuário for fornecido, isso será necessário. A senha deve ser criptografada usando o programa vcrypt enviado com o Data Crawler.
-   **`archive`** - permite que o conector Samba efetue crawl
e indexe arquivos que estejam compactados em archives. O valor é true ou false; o valor padrão é false.
-   **`max-policies-per-handle`** - especifica o número máximo de
políticas do Local Security Authority (LSA) que podem ser abertas para uma única manipulação de RPC. Essas
políticas definem as permissões de acesso que são necessárias para consultar ou modificar um sistema
específico sob várias condições. O valor padrão para essa opção é 255.
-   **`crawl-fs-metadata`** - a ativação dessa opção faz com que
o Data Crawler inclua um documento VXML contendo os metadados de sistema de arquivos disponíveis sobre o
arquivo (data de criação, data da última modificação, atributos do arquivo, etc.).
-   **`enable-arc-connector`** - opção não utilizada.
-   **`disable-indexes`** - lista separada por quebras de linha de
índices a serem desativados, o que pode resultar em um crawl mais rápido, por exemplo:

    -   `disable-url-index`
    -   `disable-error-state-index`
    -   `disable-crawl-time-index`
-   **`exact-duplicates-hash-size`** - configura o tamanho da
hashtable usada para resolver duplicatas exatas. Tenha muito cuidado ao modificar esse número. O valor
selecionado deve ser primo e tamanhos maiores podem fornecer consultas mais rápidas, mas exigem mais
memória, enquanto que tamanhos menores podem diminuir a velocidade dos crawls, mas reduzem substancialmente o
uso da memória.
-   **`user-agent`** - opção não utilizada.
-   **`timeout`** - opção não utilizada
-   **`n-concurrent-requests`** - o número de solicitações que
serão enviadas em paralelo para um único endereço IP. O padrão é `1`.
-   **`enqueue-persistence`** - opção não utilizada.

### Configurando o valor inicial de crawl do Samba

Os valores a seguir podem ser configurados para o arquivo inicial de crawl do Samba. Para configurar
esses valores, abra o arquivo `config/seeds/samba-seed.conf` e defina os valores a
seguir, que são específicos para os casos de uso:

-   **`url`** - uma lista separada por quebras de linha de
compartilhamentos para efetuar crawl, por exemplo:

    ```
    smb://share.test.com/office
    smb://share.test.com/cash/money/change
    smb://share.test.com/C$/Program Files
    ```
    {: codeblock}

-   **`hops`** - Somente uso interno.
-   **`default-allow`** - Somente uso interno.

## Configurando opções de crawl do SharePoint
{: #sharepoint-crawl-options}

**Importante:** o conector SharePoint requer o Microsoft SharePoint Server 2007 (MOSS
2007), o SharePoint Server 2010, o SharePoint Server 2013 ou o SharePoint Online.

O conector SharePoint permite efetuar crawl de objetos SharePoint e indexar as informações que eles contêm. Um objeto, como um documento, perfil do usuário, coleção de site, blog, item da lista, lista de associação,
página de diretório, etc., pode ser indexado com seus metadados associados. Para obter itens e
documentos da lista, os índices podem incluir anexos.

O conector SharePoint respeita o atributo `noindex` em todos os objetos do
SharePoint, independentemente de seu tipo específico (blogs, documentos, perfis de usuário, etc.). Um único
documento é retornado para cada resultado.
{: tip}

**Importante:** a conta do SharePoint que você usa para efetuar crawl de seus sites do
SharePoint deve ter pelo menos privilégios de acesso de leitura integral.

### Configurando o conector SharePoint

A seguir estão as opções de configuração básica que são necessárias para usar o conector SharePoint. Para configurar esses valores, abra o arquivo `config/connectors/sharepoint.conf` e modifique
os valores a seguir, que são específicos para os casos de uso:

-   **`protocol`** - O nome do protocolo do conector usado para o crawl. O valor para usar esse conector é `io-sp`.
-   **`collection`** - Esse atributo é usado para descompactar arquivos temporários.
-   **`classname`** - Classe Java para o conector. Use
`plugin:io-sharepoint.plugin@connector` para esse conector.
-   **`logging-config`** - Especifica o arquivo usado para configurar as opções de criação de log; ele deve ser formatado como uma sequência XML `log4j`.
-   **`seed-url-type`** - identifica para qual tipo de objeto
SharePoint as URLs iniciais fornecidas apontam: coleções de sites ou aplicativos da web (também conhecidos como servidores
virtuais).

    -   `Site Collections` - se o Tipo de URL inicial for configurado para
Site Collections, então somente os filhos da coleção de site referenciados pela URL serão submetidos a crawl.
    -   `Web Applications` - se o tipo de URL inicial for configurado para Web
Applications, então todas as coleções de site (incluindo seus filhos) pertencentes aos aplicativos da web
referenciados por cada URL serão submetidas a crawl.
-   **`auth-type`** - o mecanismo de autenticação a ser usado ao
entrar em contato com o servidor SharePoint: `BASIC`, `NTLM2`,
`KERBEROS` ou `CBA`. O tipo de autenticação padrão é
`NTLM2`.
-   **`spUser`** - o nome do usuário do SharePoint utilizado para
acessar o conteúdo. Esse usuário deve ter acesso a todos os sites e listas de destino a serem submetidos a
crawl e indexados e deve poder recuperar e resolver as permissões associadas. É melhor inseri-lo com o nome de
domínio, como: `MYDOMAIN\\Administrator`.
-   **`spPassword`** - a senha do usuário do SharePoint utilizada
para acessar o conteúdo. A senha deve ser criptografada usando o programa vcrypt enviado com o Data Crawler.
-   **`cba-sts`** - a URL para o terminal Security Token Service
(STS) ao qual tentar autenticar o usuário de crawl. Para locais do SharePoint com ADFS, esse deve ser o
terminal ADFS. Se o Tipo de Autenticação está configurado como CBA (Claims Based Authentication), então
esse campo é obrigatório.
-   **`cba-realm`** - o identificador do Relying Party Trust
a ser usado ao solicitar um token de segurança por meio do STS. Isso às vezes é conhecido como o
valor "AppliesTo" ou o "Realm". Para o SharePoint Online, essa deve ser a URL para a raiz da instância do
SharePoint Online (por exemplo, `https://mycompany.sharepoint.com`). Para o ADFS, esse é o
valor do ID para o Relying Party Trust entre o SharePoint e o ADFS (por exemplo,
`"urn:SHAREPOINT:adfs"`).
-   **`everyone-group`** - quando especificado, esse nome de grupo
é usado nas ACLs quando o acesso deve ser fornecido a todos. Esse campo é obrigatório quando o crawl de perfis do usuário está ativado.

    **Nota:** a segurança não é respeitada pelo serviço Retrieve and Rank.

-   **`user-profile-master-url`** - a URL base que o conector usa
para construir links para perfis do usuário. Ela deve ser configurada para apontar para o formato de exibição
para perfis do usuário. Se o token `%FIRST_SEED%` for encontrado, ele será substituído pela
primeira URL inicial. Necessário quando o crawl de perfis do usuário está ativado.
-   **`urls`** - lista separada por quebras de linha de URLs de HTTP
de aplicativos da web ou coleções de sites SharePoint para efetuar crawl.
-   **`ehcache-config`** - opção não utilizada.
-   **`method`** - O método (`GET` ou `POST`) pelo qual os parâmetros serão transmitidos.
-   **`cache-types`** - opção não utilizada.
-   **`cache-size`** - opção não utilizada.
-   **`enable-acl`** - ativa o crawl de perfis do usuário do
SharePoint; os valores são `true` ou `false`; o valor padrão é
`false`.

### Configurando o valor inicial de crawl do SharePoint

Os valores adicionais a seguir podem ser configurados para o arquivo inicial de crawl do SharePoint. Para configurar esses valores, abra o arquivo `config/seeds/sharepoint-seed.conf` e
defina os valores a seguir, que são específicos para os casos de uso:

-   **`url`** - lista separada por quebras de linha de
URLs de aplicativos da web ou de coleções de sites SharePoint para efetuar crawl. Por exemplo:

    ```
    io-sp://a.com
    io-sp://b.com:83/site
    io-sp://c.com/site2
    ```
    {: codeblock}

    Os subsites desses sites também serão submetidos a crawl (a menos que sejam excluídos por outras
regras de crawling).

-   **`filter-url`** - lista separada por quebras de linha de URLs
de aplicativos da web ou de coleções de sites SharePoint para efetuar crawl. Por exemplo:

    ```
    http://a.com
    http://b.com:83/site
    http://c.com/site2
    ```
    {: codeblock}

-   **`hops`** - Somente uso interno.
-   **`n-concurrent-requests`** - somente para uso interno.
-   **`delay`** - somente para uso interno.
-   **`default-allow`** - Somente uso interno.
-   **`seed-protocol`** - configura o protocolo inicial para filhos
da coleção de site. Necessário quando o protocolo de coleção de sites é SSL, HTTP ou HTTPS. Esse valor deve
ser configurado da mesma forma que o protocolo da coleção de site.

## Configurando opções de crawl do Box

O Box Connector permite efetuar crawl da instância do Enterprise Box e indexar as informações que ele
contém.

### Configurando o Box Connector

A seguir estão as opções de configuração básica que são necessárias para usar o Box Connector. Para
configurar esses valores, abra o arquivo `config/connectors/box.conf` e modifique os valores
a seguir, que são específicos para os casos de uso:

-   **`protocol`** - O nome do protocolo do conector usado para o crawl. O valor para usar esse conector é `caixa`.
-   **`classname`** - Classe Java para o conector. Use
`plugin:box.plugin@connector` para esse conector.
-   **`logging-config`** - Especifica o arquivo usado para configurar as opções de criação de log; ele deve ser formatado como uma sequência XML `log4j`.
-   **`box-crawl-seed-url`** - a URL base para o Box. O valor para
esse conector é `box://app.box.com/`.

    É possível efetuar crawl de diferentes tipos de URLs, por exemplo:

    -   Para efetuar crawl de uma empresa inteira: `box://app.box.com/`
    -   Para efetuar crawl de uma pasta específica:
`box://app.box.com/user/USER_ID/folder/FOLDER_ID/FolderName`
    -   Para efetuar crawl de um usuário específico: `box://app.box.com/user/USER_ID/`
-   **`client-id`** - insira o ID do cliente fornecido pelo Box
quando você criou o aplicativo Box.
-   **`client-secret`** - insira o segredo do cliente fornecido pelo
Box quando você criou o aplicativo Box.
-   **`path-to-private-key`** - esse é o local, no sistema de
arquivos local, da Chave Privada que faz parte do par de chaves pública-privada gerado para comunicação com o Box.
-   **`kid`** - especifique o ID da Chave Pública. Essa é a outra
metade do par de chaves pública-privada gerado para comunicação com o Box.
-   **`enterprise-id`** - a empresa na qual seu aplicativo foi
autorizado. O ID da Empresa é listado na página principal do Box Administration Console.
-   **`enable-acl`** - somente para uso interno. Permite
recuperação de ACLs para dados submetidos a crawl.
-   **`user-agent`** - Um cabeçalho enviado ao servidor ao efetuar crawl em documentos.
-   **`method`** - O método (`GET` ou `POST`) pelo qual os parâmetros serão transmitidos.
-   **`url-logging`** - A extensão para a qual as URLs com crawl são registradas. Os valores possíveis são:

    -   `full-logging` - Registre todas as informações sobre a URL.
    -   `refined-logging` - Basta registrar as informações necessárias para navegar no log do crawler e para que o conector funcione corretamente; esse é o valor padrão.
    -   `minimal-logging` - Basta registrar a quantidade mínima de informações necessárias para que o conector funcione corretamente.

    Configurar essa opção como `minimal-logging` reduzirá o tamanho dos logs e ganhará um leve aumento de desempenho devido à E/S menor associada com a minimização da quantidade de dados que estão sendo registrados.
-   **`ssl-version`** - Especifica uma versão de SSL para usar para conexões HTTPS. Por padrão, o protocolo mais forte disponível é usado.

### Configurando o valor inicial de crawl do Box
{: #box-crawl-options}

Os valores adicionais a seguir podem ser configurados para o arquivo inicial de crawl Box. Para
configurar esses valores, abra o arquivo `config/seeds/box-seed.conf` e defina os
valores a seguir, que são específicos para os casos de uso:

-   **`url`** - a URL a ser usada como o ponto de início do crawl. O valor padrão é `box://app.box.com/`.
-   **`default-allow`** - Somente uso interno.

## Limitações

O Box Connector possui algumas limitações:

-   Comentários ou Tarefas sobre arquivos não são recuperados.
-   O corpo do conteúdo do Notes é recuperado como JSON. A conversão adicional de dados do Notes pode
ser necessária.
-   Documentos individuais não podem ser recuperados por meio de Test-It. Somente URLs iniciais,
URLs de pasta e URLs do usuário podem ser recuperadas por meio de Test-It.
