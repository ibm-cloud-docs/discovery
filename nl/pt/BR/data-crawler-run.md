---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-18"

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

# Efetuando crawl de seu repositório de dados
{: #crawling-your-data-repository}

Após configurar as opções do crawler corretamente, será possível executar um crawl em seu repositório de dados.
{: shortdesc}

Nunca execute o crawler como `root`, a menos que você precisa de acesso aos arquivos
que somente o `root` pode ler.
{: tip}

Execute o comando a seguir: `crawler`

O crawler solicita a documentação que explica o que fazer. É possível executar um crawl de teste ou
executar um crawl, além de outras opções de crawl.

## Executando um crawl de teste

Execute o comando a seguir: `crawler testit`

Isso executa um crawl de teste, que efetua crawl somente da URL inicial e exibe quaisquer URLs
enfileiradas. Se a URL inicial resultar em conteúdo indexável (por exemplo, for um documento), então esse
conteúdo será enviado ao adaptador de saída e o conteúdo será impresso na tela. Se a recuperação da URL
inicial fizer com que as URLs sejam enfileiradas, essas URLs serão exibidas e nenhum conteúdo será enviado ao
adaptador de saída. Por padrão, cinco URLs enfileiradas são exibidas.

Também é possível especificar um arquivo de configuração customizado como uma opção para o comando
crawl, por exemplo: `crawler testit --config [config/myconfigfile.conf]`

O caminho para o arquivo de configuração passado na opção `--config` deve ser um caminho qualificado. Ou seja, ele deve estar em formatos relativos, como `config/myconfigfile.conf` ou `./myconfigfile.conf` ou em um caminho absoluto como `/path/to/config/myconfigfile.conf`.

Além disso, é possível configurar o limite para o número de URLs enfileiradas que são exibidas como uma
opção para o comando testit, por exemplo: `crawler testit --limit [number]`

## Executando um crawl

Execute o seguinte comando: `crawler crawl`

Isso executa um crawl com o arquivo de configuração padrão (`crawler.conf`).

Também é possível especificar um arquivo de configuração customizado como uma opção para o comando crawl,
por exemplo: `crawler crawl --config [config/myconfigfile.conf]`

O caminho para o arquivo de configuração passado na opção `--config` deve ser um caminho qualificado. Ou seja, ele deve estar em formatos relativos, como `config/myconfigfile.conf` ou `./myconfigfile.conf` ou em um caminho absoluto como `/path/to/config/myconfigfile.conf`.

## Reiniciando um crawl

Execute o seguinte comando: `crawler restart`

Esse comando executa um crawl de reinicialização iniciando um novo crawl com o arquivo de configuração
padrão (`crawler.conf`).

Também é possível especificar um arquivo de configuração customizado como uma opção para o comando de
reinicialização, por exemplo: `crawler restart --config [config/myconfigfile.conf]`

O caminho para o arquivo de configuração passado na opção `--config` deve ser um caminho qualificado. Ou seja, ele deve estar em formatos relativos, como `config/myconfigfile.conf` ou `./myconfigfile.conf` ou em um caminho absoluto como `/path/to/config/myconfigfile.conf`.

## Continuando um crawl

Execute o seguinte comando: `crawler resume`

Este comando continua um crawl do ponto em que ele parou com o arquivo de configuração padrão
(`crawler.conf`).

Também é possível especificar um arquivo de configuração customizado como uma opção para o comando de
continuação, por exemplo: `crawler resume --config [config/myconfigfile.conf]`

O caminho para o arquivo de configuração passado na opção `--config` deve ser um caminho qualificado. Ou seja, ele deve estar em formatos relativos, como `config/myconfigfile.conf` ou `./myconfigfile.conf` ou em um caminho absoluto como `/path/to/config/myconfigfile.conf`.

## Atualizando um crawl

Execute o seguinte comando: `crawler refresh`

O comando atualiza um crawl anterior com o arquivo de configuração padrão
(`crawler.conf`).

Também é possível especificar um arquivo de configuração customizado como uma opção para o comando de
atualização, por exemplo: `crawler refresh --config [config/myconfigfile.conf]`

O caminho para o arquivo de configuração passado na opção `--config` deve ser um caminho qualificado. Ou seja, ele deve estar em formatos relativos, como `config/myconfigfile.conf` ou `./myconfigfile.conf` ou em um caminho absoluto como `/path/to/config/myconfigfile.conf`.
