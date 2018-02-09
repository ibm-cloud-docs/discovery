---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-10"

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

# Incluindo conteúdo

Como decidir qual método de upload do documento será utilizado?
{: shortdesc}

-   Use o [API](/docs/services/discovery/getting-started.html) se você estiver integrando o upload de conteúdo com um aplicativo existente ou criando seu próprio mecanismo de upload customizado.
-   Use o [Conjunto de ferramentas do {{site.data.keyword.discoveryshort}}](/docs/services/discovery/getting-started-tool.html) se você quiser fazer upload rapidamente dos arquivos acessíveis localmente. Ao fazer upload de documentos usando o conjunto de ferramentas do {{site.data.keyword.discoveryshort}}, todos os documentos devem ter um nome de arquivo exclusivo. Se dois arquivos tiverem o mesmo nome, o original será sobrescrito quando a versão mais recente for transferida por upload. Se você prefere que documentos com o mesmo nome de arquivo coexistam em sua coleção, o ID do documento precisa ser especificado. Será possível especificar o ID do documento se você carregar documentos usando a API ou o Data Crawler.
-   Use o [Data Crawler](/docs/services/discovery/data-crawler.html) se você deseja ter um upload gerenciado de um número significativo de arquivos ou se você deseja extrair o conteúdo de um repositório suportado (como um banco de dados DB2).

## Incluindo conteúdo com a API ou conjunto de ferramentas

Considere o seguinte quando você estiver pronto para incluir documentos em sua coleção:

-   O tamanho máximo do arquivo que pode ser transferido por upload para o serviço do {{site.data.keyword.discoveryshort}} é 50 MB.

-   Os documentos de amostra não são incluídos automaticamente na coleção. Eles devem ser incluídos se você deseja que façam parte de sua coleção.

-   Ao criar uma coleção, você seleciona o idioma do documento (inglês é o padrão). Consulte [Suporte ao idioma](/docs/services/discovery/language-support.html) para obter a lista de idiomas. Seus documentos serão enriquecidos no idioma selecionado. Não combine idiomas dentro da mesma coleção.

-   É possível incluir documentos do Microsoft Word, PDF, HTML e JSON na sua coleção. **Nota:** os PDFs que são arquivos de imagem varridos não podem ser convertidos nem enriquecidos. 

-   Os documentos em sua coleção serão convertidos usando o arquivo de configuração fornecido, que é denominado Configuração Padrão, a menos que você escolha um arquivo de configuração diferente. Para obter informações sobre como criar um arquivo de configuração, consulte [Configuração customizada](/docs/services/discovery/building.html#custom-configuration).

-   Quando os documentos são transferidos por upload para uma coleta de dados, eles são convertidos e enriquecidos usando o arquivo de configuração escolhido para essa coleção. Se você decidir mais tarde que deseja mudar uma coleção para um arquivo de configuração diferente, será possível fazer isso, mas os documentos que já foram transferidos por upload permanecerão convertidos pelo arquivo de configuração original. Todos os documentos transferidos por upload depois de mudar o arquivo de configuração usarão o novo arquivo de configuração. Se você deseja que a coleção **inteira** use a nova configuração, será necessário criar uma nova coleção, escolher esse novo arquivo de configuração e fazer um novo upload de todos os documentos.

## Fazendo upload de documentos com o Discovery Tooling.

1.  Criar uma coleção. Consulte [Preparando o serviço para seus documentos](/docs/services/discovery/building.html#preparing-the-service-for-your-documents).
1.  Clique na coleção para abri-la.
1.  Clique em **Fazer upload de documentos** e comece a fazer upload de seus documentos por meio de arrastar e soltar ou procurar.

Seus documentos agora estão enfileirados para serem convertidos e enriquecidos. O tempo necessário depende do tamanho de sua coleção. Depois que ele é indexado e enriquecido, os detalhes da Coleção serão exibidos na seção **Visão geral**.

-   Datas de **Criação** e **Última atualização** (clique em **Utilizar esta coleção de API** para ver o `collection_id`, o `configuration_id` e o `environment_id`).
-   **Número de documentos** em sua coleção
-   **Configuração** - o nome do arquivo de configuração utilizado para converter esta coleção
-   **Erros e avisos**

## Fazendo upload de documentos com a API

Consulte [Introdução à API do {{site.data.keyword.discoveryshort}}](/docs/services/discovery/getting-started.html) para obter um tutorial passo a passo.

Para obter mais informações sobre a API, consulte a [Referência da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}.

1.  Use o método `POST /v1/environments/{environment_id}/collections` para criar uma coleção.
1.  Em seguida, use o método `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` para incluir documentos em sua coleção.

## Efetuando crawl de URLs

É possível efetuar crawl de URLs e indexá-las usando o {{site.data.keyword.IBM_notm}} {{site.data.keyword.watson}} {{site.data.keyword.discoveryshort}} Service [Indexando plug-in para o Apache Nutch ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/IBM-Watson/nutch-indexer-discovery).
Como o crawl não atualiza automaticamente, o procedimento precisará ser repetido periodicamente para manter o índice atualizado.
