---

copyright:
  years: 2015, 2018, 2019
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

# Incluindo conteúdo
{: #addcontent}

Como decidir qual método de upload do documento será utilizado?
{: shortdesc}

-   Use o [API](/docs/services/discovery?topic=discovery-gs-api#gs-api) se você estiver integrando o upload de conteúdo com um aplicativo existente ou criando seu próprio mecanismo de upload customizado.
-   Use o [conjunto de ferramentas do {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-getting-started#getting-started) se desejar fazer upload rapidamente de arquivos acessíveis localmente.
    Ao fazer upload de documentos usando o conjunto de ferramentas do {{site.data.keyword.discoveryshort}}, todos os documentos devem ter um nome de arquivo exclusivo. Se dois arquivos tiverem o mesmo nome, o original será sobrescrito quando a versão mais recente for transferida por upload. Se você prefere que documentos com o mesmo nome de arquivo coexistam em sua coleção, o ID do documento precisa ser especificado. Será possível especificar o ID do documento se você carregar documentos usando a API ou o Data Crawler.
-   Use a API ou o conjunto de ferramentas do {{site.data.keyword.discoveryshort}} para se conectar às origens de dados do Box, do Salesforce, do Microsoft SharePoint Online, do IBM Cloud Object Storage e do Microsoft SharePoint 2016 ou execute um crawl da web. Consulte [Conectando-se a origens de dados](/docs/services/discovery?topic=discovery-sources#sources) para obter mais informações.
-   Use o [Data Crawler](/docs/services/discovery?topic=discovery-adding-content-with-data-crawler#adding-content-with-data-crawler) se você deseja ter um upload gerenciado de um número significativo de arquivos ou se você deseja extrair o conteúdo de um repositório suportado (como um banco de dados DB2).

## Incluindo conteúdo com a API ou conjunto de ferramentas
{: #adding-content-with-the-api-or-tooling}

Considere o seguinte quando você estiver pronto para incluir documentos em sua coleção:

-   O tamanho máximo do arquivo que pode ser transferido por upload para o serviço do {{site.data.keyword.discoveryshort}} é 50 MB.
-   Os documentos de amostra não são incluídos automaticamente na coleção. Eles devem ser incluídos se você deseja que façam parte de sua coleção. (Aplica-se somente a coleções criadas antes da liberação do [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu).)
-   Somente os primeiros 50.000 caracteres de cada campo JSON selecionado para enriquecimento serão enriquecidos.
-   Ao criar uma coleção, você seleciona o idioma do documento (inglês é o padrão). Consulte [Suporte ao idioma](/docs/services/discovery?topic=discovery-language-support#language-support) para obter a lista de idiomas. Seus documentos serão enriquecidos no idioma selecionado. Não combine idiomas dentro da mesma coleção.
-   Os tipos de arquivo a seguir podem ser ingeridos pelo {{site.data.keyword.discoveryshort}}; todos os outros tipos de documento são ignorados:

Coleta | Planos Lite | Planos avançados 
---------------- | ------------------------------ | ------------------------------------------- 
Coleções existentes criadas especificamente para o {{site.data.keyword.discoveryfull}} antes da liberação do [Smart Document Understanding (SDU)](/docs/services/discovery?topic=discovery-release-notes#22jan19) | Microsoft Word, PDF, HTML, JSON | Microsoft Word, PDF, HTML, JSON     
Coleções criadas após a liberação do [SDU](/docs/services/discovery?topic=discovery-sdu#sdu) | PDF, Word, PowerPoint, Excel, JSON \ *, HTML \ * | PDF, Word, PowerPoint, Excel, PNG\*\*, TIFF\*\*, JPG\*\*, JSON\*, HTML\* 
    
\* Os documentos JSON e HTML são suportados pelo {{site.data.keyword.discoveryfull}}, mas não podem ser editados usando o editor do SDU. Para mudar a configuração de docs HTML e JSON, é necessário usar a API. Para obter mais informações, veja a [Referência de API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery/){: new_window}.

\*\* Os arquivos de imagem individual (PNG, TIFF, JPG) serão escaneados e o texto (se houver) será extraído. As imagens PNG, TIFF e JPEG integradas a arquivos PDF, Word, PowerPoint e Excel também serão escaneadas e o texto (se houver) será extraído.
-   Os documentos em sua coleção serão convertidos usando a configuração atual, a menos que você escolha um arquivo de configuração diferente. Para obter informações sobre como criar um arquivo de configuração, consulte [Configuração customizada](/docs/services/discovery?topic=discovery-configservice#custom-configuration). (Aplica-se somente a coleções criadas antes da liberação do [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu).)
-   Quando os documentos são transferidos por upload para uma coleta de dados, eles são convertidos e enriquecidos usando o arquivo de configuração escolhido para essa coleção. Se você decidir mais tarde que deseja mudar uma coleção para um arquivo de configuração diferente, será possível fazer isso, mas os documentos que já foram transferidos por upload permanecerão convertidos pelo arquivo de configuração original. Todos os documentos transferidos por upload depois de mudar o arquivo de configuração usarão o novo arquivo de configuração. Se você deseja que a coleção **inteira** use a nova configuração, será necessário criar uma nova coleção, escolher esse novo arquivo de configuração e fazer um novo upload de todos os documentos. (Se estiver usando o [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu), será solicitado que você faça um novo upload de seus documentos depois de clicar no botão **Aplicar mudanças na coleção**.)
-   Não é possível especificar o `data type` (por exemplo: `text` ou `date`) de campos. Durante a ingestão do documento, se for detectado um campo que ainda não existe no índice, o {{site.data.keyword.discoveryshort}} detectará automaticamente o `data type` desse campo com base no valor do campo para o primeiro documento indexado.
-   Um documento pode falhar ao ser alimentado devido a uma incompatibilidade de tipo
entre os dados no documento atual e os dados semelhantes em um documento alimentado anteriormente. Por exemplo, um campo pode ser digitado como uma `data` em um documento e como uma
`sequência` em um documento subsequente, impedindo que o documento subsequente seja
indexado corretamente.
-   Se você planeja usar a tokenização customizada (disponível atualmente somente para coleções em japonês ao usar a API do {{site.data.keyword.discoveryshort}}), o dicionário de tokenização para sua coleção deve ser incluído antes de fazer upload de documentos.

## Fazendo upload de documentos com o Discovery Tooling.
{: #upload_tooling}

1.  Criar uma coleção. Consulte [Preparando o serviço para seus documentos](/docs/services/discovery?topic=discovery-configservice#preparing-the-service-for-your-documents).
1.  Clique na coleção para abri-la.
1.  Clique em **Fazer upload de documentos** e comece a fazer upload de seus documentos por meio de arrastar e soltar ou procurar.

Seus documentos agora estão enfileirados para serem convertidos e enriquecidos. O tempo necessário depende do tamanho de sua coleção. Depois que ele é indexado e enriquecido, os detalhes da Coleção serão exibidos na seção **Visão geral**.

-   **Campos identificados** em sua coleção (somente o Smart Document Understanding).
-   Datas de **Criação** e **Última atualização** (clique em **Utilizar esta coleção de API** para ver o `collection_id`, o `configuration_id` e o `environment_id`).
-   **Número de documentos** em sua coleção
-   **Configuração** - O nome do arquivo de configuração usado para converter essa coleção (somente para coleções criadas antes da liberação do [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu)).
-   **Erros e avisos**

Para obter informações sobre como se conectar às origens de dados do Box, do Salesforce, do Microsoft SharePoint Online, do IBM Cloud Object Storage e do Microsoft SharePoint 2016 ou como executar um crawl da web com o conjunto de ferramentas do {{site.data.keyword.discoveryshort}}, consulte [Conectando-se às origens de dados](/docs/services/discovery?topic=discovery-sources#sources).


## Fazendo upload de documentos com a API
{: #upload_api}

Consulte [Introdução à API do {{site.data.keyword.discoveryshort}}](/docs/services/discovery?topic=discovery-gs-api#gs-api) para obter um tutorial passo a passo.

Para obter mais informações sobre a API, consulte a [Referência da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery/){: new_window}.

1.  Use o método `POST /v1/environments/{environment_id}/collections` para criar uma coleção.
1.  Em seguida, use o método `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` para incluir documentos em sua coleção.

## Efetuando crawl de URLs
{: #crawl_urls}

É possível efetuar crawl de URLs e indexá-las usando o {{site.data.keyword.IBM_notm}} {{site.data.keyword.watson}} {{site.data.keyword.discoveryshort}} Service [Indexando plug-in para o Apache Nutch ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/IBM-Watson/nutch-indexer-discovery). Como o crawl não atualiza automaticamente, o procedimento precisará ser repetido periodicamente para manter o índice atualizado. 

Você também tem a opção de usar o conector Web Crawl beta. Consulte  [ Conectando-se a origens de dados ](/docs/services/discovery?topic=discovery-sources#connectwebcrawl).
