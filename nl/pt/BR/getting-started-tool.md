---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-18"

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
{:download: .download}

# Informações Iniciando
{: #getting-started}

Neste curto tutorial, apresentamos o conjunto de ferramentas do
{{site.data.keyword.discoveryshort}}
e percorreremos o processo de criação e de procura de uma coleção de dados privados.
{: shortdesc}

Se você preferir trabalhar na API, veja [Introdução à API](/docs/services/discovery/getting-started.html).
{: tip}

## Antes de Começar
{: #before-you-begin}

Será necessária uma instância de serviço para iniciar.

<!-- Remove the text marked `download` after there's no g-s tab in the catalog dashboard -->


Você criou sua instância de serviço. Clique em  ** Gerenciar ** e, em seguida,  ** Abrir ferramenta **. Acesse a
[Etapa 2](/docs/services/discovery/getting-started-tooling.html#create-a-collection).
{: download tip}

Se você criou uma instância de serviço do {{site.data.keyword.discoveryshort}}, tudo estará pronto para esses pré-requisitos. Acesse a  [ Etapa 1 ](/docs/services/discovery/getting-started-tool.html#launch-the-tooling).

1.  Acesse a página [{{site.data.keyword.discoveryshort}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.{DomainName}/catalog/services/discovery){: new_window} no {{site.data.keyword.Bluemix_notm}} Catalog.
1.  Inscreva-se para obter uma conta gratuita do {{site.data.keyword.Bluemix_notm}} ou efetue login.
1.  Clique em  ** Criar **.


## Etapa 1: Ativar o conjunto de ferramentas
{: #launch-the-tooling}

Depois de criar uma instância do serviço {{site.data.keyword.discoveryshort}}, você chegará ao [painel do {{site.data.keyword.Bluemix_notm}}](https://console.{DomainName}/dashboard). Clique em sua instância de serviço do {{site.data.keyword.discoveryshort}} para acessar o painel do serviço {{site.data.keyword.discoveryshort}}.

Na página **Gerenciar**, clique em **Abrir ferramenta**.

<!-- To do: Add screenshot for developer console -->

Se for solicitado a efetuar login no conjunto de ferramentas, forneça suas credenciais do {{site.data.keyword.Bluemix_notm}}.

Se você não estiver em uma página de detalhes do projeto para o serviço do {{site.data.keyword.discoveryshort}}, acesse a página {{site.data.keyword.watson}} Developer Console [Projetos ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.{DomainName}/developer/watson/projects) e selecione o projeto.
{: tip}

<!-- Remove this text after dedicated instances have the Developer Console: begin -->

{{site.data.keyword.Bluemix_dedicated_notm}}: selecione sua instância de serviço no Painel para ativar o conjunto de ferramentas.

<!-- Remove this text after dedicated instances have the Developer Console: end -->

## Etapa 2: crie uma coleção
{: #create-a-collection}

Sua primeira etapa no conjunto de ferramentas do {{site.data.keyword.discoveryshort}} é criar uma coleção de dados.

Uma coleção é um conjunto de seus documentos. *Por que eu iria querer mais de uma coleção?* Existem algumas razões:

- Talvez você queira múltiplas coleções para separar resultados para públicos diferentes.
- Os dados podem ser tão diferentes que não faz sentido consultá-los todos ao mesmo tempo.

A coleção de dados públicos e pré-enriquecidos do {{site.data.keyword.discoverynewsshort}} agora está disponível para uso. Ela está pronta para consultar e é possível começar a criar consultas nela imediatamente. Não é possível ajustar sua configuração ou incluir documentos no {{site.data.keyword.discoverynewsshort}}.

1.  Clique em ![Cog](images/icon_settings.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> e escolha **Criar ambiente**.
1.  Quando seu ambiente estiver pronto, clique no botão **Fazer upload de seus próprios dados**, em seguida, será possível **Nomear sua nova coleção**. Nomeie sua coleção e escolha **Configuração padrão** em **Selecionar uma configuração a ser aplicada** (é possível mudar a configuração posteriormente).

Há outra configuração disponível denominada **Configuração de contrato padrão** que suporta Classificação de elementos, que pode ser usada para extrair a parte, a natureza e a categoria de elementos em PDFs. Consulte  [ Classificação de Elementos ](/docs/services/discovery/element-classification.html#element-collection)  para obter detalhes.

Também é possível efetuar crawl das origens de dados Box, Salesforce e Microsoft SharePoint Online com o conjunto de ferramentas do {{site.data.keyword.discoveryshort}}. Clique no botão **Conectar uma origem de dados** e veja [Conectando-se a origens de dados](/docs/services/discovery/connect.html) para obter mais informações.
{: tip}

## Etapa 3: Criar uma configuração customizada
{: create-custom-configuration}

Depois que sua coleção é criada, é possível iniciar imediatamente o upload do conteúdo usando a área de upload, mas queremos criar e testar uma configuração customizada.

1.  Clique em **Alternar** ao lado do nome da coleção e escolha **Criar uma nova configuração**. Nomeie sua configuração e clique em **Criar**.
1.  Depois de criar sua configuração, é possível customizá-la:
    1.  Faça download do documento de amostra
<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html
<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo" class="style-scope doc-content"></a>.
    1.  Use o painel **Fazer upload de documentos de amostra** para fazer upload do documento de amostra. Após o upload, é possível clicar no link do nome do documento para visualizar a transformação.
1.  Agora é hora de ajustar a configuração. Para esta tarefa, você muda os enriquecimentos para que sejam aplicados a cada documento:
    1.  Clique na seção **Enriquecer** da configuração. Observe o JSON gerado à direita da tela. Role para baixo até a seção *enriched_text* e observe que ela contém muitos *conceitos*.
    1.  Em seguida, remova o enriquecimento de texto denominado *conceitos* clicando no
**X** ao lado dele e, em seguida, clique em **Aplicar e Salvar**.
    1.  Por fim, consulte o JSON novamente. Observe como a saída foi mudada e que ela não inclui mais *conceitos*.

## Etapa 4: Fazer upload de seus documentos
{: #upload-your-documents}

Quando você está satisfeito com a conversão customizada de seu documento de amostra, é hora de alimentar o conteúdo real em sua coleção.

1. Faça download destes três documentos de amostra:
<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html
<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo" class="style-scope doc-content"></a>,
<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html
<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo" class="style-scope doc-content"></a>,
<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html
<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo" class="style-scope doc-content"></a>.
1.  Clique em ![Ícone dearquivo](images/icon_yourData.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} -->

e selecione sua coleção.
1.  Certifique-se de que a configuração customizada criada esteja listada em **Configuração**. Se não estiver, clique em **Alternar** ao lado do nome da configuração e selecione-a.
1.  Clique no botão **Fazer upload de documentos** e comece a fazer upload dos quatro documentos de amostra: test-doc1.html, teste-doc2.html, teste-doc3.html e teste-doc4.html.
1.  Aguarde os documentos serem transferidos por upload. O status de seus documentos é exibido na seção **Visão geral**.

## Etapa 5: Construir uma consulta
{: #build-a-query}

1.  Clique em ![Ícone de consulta](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> para abrir a página de consulta. Selecione sua coleção e clique em **Introdução**.
1.  Na tela **Construir consultas**, clique em **Procurar por documentos** e, em seguida, **Usar o {{site.data.keyword.discoveryshort}} Query Language**:
    - Para procurar por resultados com entidades denominadas "IBM":
        1.  Clique em **Campo** e selecione `enriched_text.entities.text`. Selecione `contains` para **Operador** e `IBM` para **Valor**. A consulta `enriched_text.entities.text:IBM` é exibida no **Visual Query Builder**.
        1.  Clique em **Executar consulta**. A consulta retorna 4 resultados.
    - Para procurar por resultados com entidades denominadas "Watson":
        1.  Clique em **Campo** e selecione `enriched_text.entities.text`. Selecione `contains` para o **Operador** e `watson` para **Value**. A consulta `enriched_text.entities.text:watson` é exibida no **Visual Query Builder**.
        1.  Clique em **Executar consulta**. A consulta retorna 2 resultados.
    - Para procurar por resultados com ambas as entidades denominadas "Watson" e "Slack":
        1.  Clique em **Campo** e selecione `enriched_text.entities.text`. Selecione `contains` para o **Operador** e `watson` para **Value**. Clique em **Incluir regra** e, em seguida, repita suas seleções, mas escolha o **Valor** de `Slack`. A consulta `enriched_text.entities.text:watson,enriched_text.entities.text:Slack` é exibida no **Visual Query Builder**.
        1.  Clique em **Executar consulta**. A consulta retorna 1 resultado.

    Clique em **Editar na linguagem de consulta** para construir consultas usando o
{{site.data.keyword.discoveryshort}} Query Language. Para saber mais sobre o
{{site.data.keyword.discoveryshort}} Query Language, veja
[Referência de consulta](/docs/services/discovery/query-reference.html) e
[Conceitos de consulta](/docs/services/discovery/using.html).
1.  Os resultados de sua consulta são exibidos na seção **Resultados**:
    - A guia **Resumo** fornece uma visão geral dos resultados da consulta.
    - A guia **JSON** exibe os resultados completos do JSON.

    Para consultas listadas, a guia **Resumo** exibe as passagens de documento (em ordem de relevância) primeiramente, seguido pelos nomes dos documentos localizados e, depois, pelos resultados por enriquecimento. **Passagens** são trechos curtos relevantes extraídos dos documentos completos retornados pela sua consulta.

    O link **URL de consulta** fornecido nas guias
**JSON** e **Resumo** está pronto para uso em seu aplicativo.

    Também é possível clicar em **Usar linguagem natural** e gravar uma consulta de linguagem natural, como "parcerias do IBM Watson". Para saber mais sobre consultas de linguagem natural, veja [Consulta de linguagem natural](/docs/services/discovery/query-parameters.html#nlq).

    O Watson pode ser treinado para melhorar os resultados das consultas de linguagem natural, consulte [Melhorando a relevância de resultados com o conjunto de ferramentas](/docs/services/discovery/train-tooling.html).

    Recursos adicionais:
    - Para saber mais sobre o esquema de dados de seus documentos, clique em **Visualizar
esquema de dados** ou clique na guia **JSON**. Consulte [O esquema de dados do Discovery](/docs/services/discovery/using.html#discovery-schema)
para obter detalhes.
    - Se estiver editando no {{site.data.keyword.discoveryshort}} Query Language, clique nos
ícones **?** ao lado de qualquer um dos campos **Insira a consulta
aqui** para obter mais exemplos.

## Próximos passos
{: #next-steps}

Agora você tem uma instância de serviço do {{site.data.keyword.discoveryshort}} funcionando e
preenchida. Agora é possível começar a customizar sua coleção incluindo mais documentos e enriquecimentos e
customizando as configurações de conversão.
