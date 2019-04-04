---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-02-08"

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

# Informações Iniciando
{: #getting-started}

Neste curto tutorial, apresentamos o conjunto de ferramentas do
{{site.data.keyword.discoveryshort}}
e percorreremos o processo de criação e de procura de uma coleção de dados privados.
{: shortdesc}

Se você preferir trabalhar na API, veja [Introdução à API](/docs/services/discovery?topic=discovery-gs-api#gs-api).
{: tip}

## Antes de Começar
{: #before-you-begin-tool}
{: hide-dashboard}

É necessária uma instância de serviço para iniciar.
{: hide-dashboard}

1.  {: hide-dashboard} Acesse a [página do {{site.data.keyword.discoveryshort}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/catalog/services/discovery) no catálogo do {{site.data.keyword.cloud_notm}}.

    A instância de serviço será criada no grupo de recursos **padrão** se você não escolher um diferente, e ela *não poderá* ser mudada posteriormente. Esse grupo é suficiente para os propósitos de experimentar o serviço.

    Se você estiver criando uma instância para uso mais robusto, saiba mais sobre [grupos de recursos ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/docs/resources/bestpractice_rgs.html#bp_resourcegroups){: new_window}.
1.  {: hide-dashboard} Inscreva-se para obter uma conta gratuita do {{site.data.keyword.cloud_notm}} ou efetue login.
1.  {: hide-dashboard} Clique em  ** Criar **.

## Etapa 1: Ativar o conjunto de ferramentas
{: #launch-the-tooling}

Após você criar uma instância do serviço do {{site.data.keyword.discoveryshort}}, será levado para a sua lista de serviços.
{: hide-dashboard}

1.  {: hide-dashboard} Clique na instância de serviço do {{site.data.keyword.discoveryshort}} que você criou para acessar o painel de serviço.
1.  Na página **Gerenciar**, clique em **Ativar ferramenta**. Se for solicitado que você efetue login no conjunto de ferramentas, forneça suas credenciais do {{site.data.keyword.cloud_notm}}.

<!-- To do: Add screenshot for developer console -->

## Etapa 2: crie uma coleção
{: #create-a-collection-tool}

Sua primeira etapa no conjunto de ferramentas do {{site.data.keyword.discoveryshort}} é criar uma coleção de dados.

Uma coleção é um conjunto de seus documentos. *Por que eu iria querer mais de uma coleção?* Existem algumas razões:

- Talvez você queira múltiplas coleções para separar resultados para públicos diferentes.
- Os dados podem ser tão diferentes que não faz sentido consultá-los todos ao mesmo tempo.

A coleção de dados públicos e pré-enriquecidos do {{site.data.keyword.discoverynewsshort}} agora está disponível para uso. Ela está pronta para consultar e é possível começar a criar consultas nela imediatamente. Não é possível ajustar sua configuração ou incluir documentos no {{site.data.keyword.discoverynewsshort}}.

1.  Clique em ![Detalhes do ambiente](images/env_icon.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> e escolha **Criar ambiente**.
1.  Quando seu ambiente estiver pronto, clique no botão **Fazer upload de seus próprios dados**, em seguida, será possível **Nomear sua nova coleção**. Nomeie sua coleção  ** InstallDocs **.

    Ao criar uma coleção, em **Avançado**, você tem a opção de escolher um arquivo de configuração denominado **Configuração de contrato padrão**. Essa configuração suporta apenas o enriquecimento Classificação de elementos, que pode ser usado para extrair a parte, a natureza e a categoria de elementos em PDFs. Consulte [ Classificação de Elementos ](/docs/services/discovery?topic=discovery-element-classification#element-collection) para obter detalhes. Não escolha essa opção para este tutorial.

Também é possível efetuar crawl das origens de dados do Box, do Salesforce, do Microsoft SharePoint Online, do IBM Cloud Object Storage e do Microsoft SharePoint 2016 ou efetuar um crawl da web com o conjunto de ferramentas do {{site.data.keyword.discoveryshort}}. Clique no botão **Conectar uma origem de dados** e veja [Conectando-se a origens de dados](/docs/services/discovery?topic=discovery-sources#sources) para obter mais informações.
{: tip}

## Etapa 3: Fazer download do documento de amostra e fazer upload para a sua coleção
{: create-custom-configuration}

1.  Faça download desse documento PDF de amostra: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/watsonexplorerinstall.pdf" download>Watson Explorer Installation Guide <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo"></a>. Consulte [Tipos de documento suportados](/docs/services/discovery?topic=discovery-sdu#doctypes) para obter a lista completa de tipos de documento suportados no {{site.data.keyword.discoveryshort}}. 

    Em alguns navegadores, o link se abre em uma nova janela em vez de salvar localmente. Se isso ocorrer, selecione `Save as` no menu `File` de seu navegador para salvar uma cópia do arquivo.
    {: tip}

1.  Faça upload do documento para sua coleção. Arraste e solte-o em sua coleção ou clique em **procurar no computador** para fazer upload de documentos. Após a conclusão do upload, as informações a seguir são exibidas:
    -  O número de documentos (1).
    -  Os campos identificados a partir de seu documento. É necessário ver um campo identificado, `text`. Nós identificaremos campos adicionais em breve.
    -  Enriquecimentos aplicados ao seu documento. Os enriquecimentos Extração de entidade, Análise de sentimentos, Classificação de categoria e Identificação de conceito são aplicados automaticamente ao campo `text` pelo {{site.data.keyword.discoveryshort}}. Saiba mais sobre enriquecimentos  [ aqui ](/docs/services/discovery?topic=discovery-configservice#adding-enrichments)). 
    -  Consultas pré-construídas que podem ser executadas imediatamente.
1.  Vamos tentar uma consulta rápida de língua natural para o nível configurado. Clique em **Construir sua própria consulta** na parte inferior direita.
1.  Na tela **Construir consultas**, clique em **Procurar documentos** e, em seguida, **Usar a língua natural**. Insira `What are the minimum hardware requirements` e clique no botão **Executar consulta**. Clique na guia **JSON** à direita. O resultado não é tão preciso quanto poderia ser, assim, vamos melhorá-lo com o Smart Document Understanding.
1.  Clique no nome da coleção (**InstallDocs**) na parte superior esquerda para retornar para a tela **Visão geral**.  
 
## Etapa 4: Anotar seu documento
{: #upload-your-documents}

Para obter mais informações sobre como anotar documentos, consulte [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu).
{: tip}

1.  Clique em **Configurar dados** no canto superior direito. 
1.  Na tela **Configurar dados**, haverá três guias: **Identificar campos**, **Gerenciar campos** e **Enriquecer campos**.
1.  O `Guia de instalação do Watson Explorer` é exibido e está pronto para anotação na guia **Identificar campos**. Todos os campos disponíveis (`answer`, `author`, `footer`, `header`, `question`, `subtitle`, `table_of_contents`, `text` e `title`) são exibidos na lista **Rótulos de campo** à direita. Se você comprar um plano Advanced ou Premium, será possível criar seus próprios rótulos customizados.

    Como o documento inteiro é atualmente identificado como `text`, os marcadores no lado direito estão totalmente em amarelo. Conforme você anotar (e o sistema iniciar a previsão), as cores serão atualizadas.
    {: tip}

1.  Clique em `title` e, em seguida, selecione o marcador ao lado de `Installation and Integration Guide`. Clique no botão  ** Submeter página ** .
1.  Na visualização de página à esquerda, clique na página 3. Observe que o `title` já foi previsto para esta página. Clique no botão  ** Submeter página ** .
1.  Na página 4, selecione o rótulo `footer` e selecione o marcador ao lado do rodapé. Clique no botão  ** Submeter página ** .
1.  Nas páginas 5 e 6, anote os rodapés com o rótulo `footer`. Submeta cada página. Clique em mais algumas páginas. Você observará que o rodapé foi previsto corretamente pelo {{site.data.keyword.discoveryshort}}. Anote os `title`s (sem indentação esquerda) e os `subtitle`s (indentados) nas páginas 7, 9 e 10 e envie cada página individualmente.
1.  Clique em mais algumas páginas e verifique os títulos e os subtítulos previstos. Se algo precisar ser mudado, anote essas páginas e clique no botão **Enviar página**.
1.  Agora, clique na guia **Gerenciar campos** e em **Melhorar os resultados da consulta dividindo seus documentos** divida o documento com base no `subtitle`. 
1.  Por enquanto, fazer anotações é o suficiente. Clique no botão **Aplicar mudanças à coleção** na parte superior direita. A caixa de diálogo **Fazer upload de seus documentos** é exibida. Navegue para o arquivo `watsonexplorerinstall.pdf` original e faça upload dele. Isso se aplica a todas as anotações em seu índice. Após a conclusão da indexação, a tela **Visão geral** é aberta. Agora, você deve ver mais 30 documentos e quatro campos identificados por meio dos seus dados: `footer`, `subtitle`, `text` e `title`. (Se as mudanças não forem exibidas dentro de alguns minutos, atualize a janela do navegador.)

    É possível excluir campos (como `footer`) da indexação abrindo a guia **Gerenciar campos** e selecionando `off` para esse campo.
    {: tip}

## Etapa 5: Vamos consultar
{: #build-a-query}

1.  Clique em **Construir sua própria consulta** na parte inferior direita.
1.  Na tela **Construir consultas**, clique em **Procurar documentos** e, em seguida, **Usar a língua natural**. Insira `What are the minimum hardware requirements` e clique no botão **Executar consulta**. 
1.  Clique na guia **JSON** à direita. Consulte o  ` texto `  em  ` Resultados `. As respostas retornadas para a consulta são muito mais precisas.

Recursos adicionais:
-  Para saber mais sobre o esquema de dados de seus documentos, clique no ícone **Visualizar esquema de dados** no lado esquerdo ou clique na guia **JSON**. Consulte o [Esquema de dados de descoberta](/docs/services/discovery?topic=discovery-query-concepts#discovery-schema) para obter detalhes.
-  Clique no botão **Usar uma consulta de amostra** para testar as consultas de exemplo gravadas no {{site.data.keyword.discoveryshort}} Query Language.

## Próximos passos
{: #next-steps-tool}

Agora você tem uma instância de serviço do {{site.data.keyword.discoveryshort}} funcionando e
preenchida. Agora, é possível iniciar a customização de sua coleção incluindo mais documentos e enriquecimentos e anotando documentos adicionais. Consulte [Smart Document Understanding](/docs/services/discovery?topic=discovery-sdu#sdu) para obter mais informações.
