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
{:gif: data-image-type='gif'}

# Smart Document Understanding
{: #sdu}

O Smart Document Understanding (SDU) é uma nova maneira de treinar o {{site.data.keyword.discoveryfull}} para extrair campos customizados em seus documentos. Customizar como seus documentos são indexados no {{site.data.keyword.discoveryshort}} melhorará as respostas retornadas por seu aplicativo.

Com o SDU, você anota campos em seus documentos para treinar modelos de conversão customizados. À medida que você anota, o Watson está aprendendo e iniciará a previsão de anotações. Os modelos SDU podem ser exportados e usados em outras coleções. 

## Tipos de documentos e navegadores suportados
{: #doctypes}

Tipos de documento suportados para o Smart Document Understanding: 
-  Planos Lite: PDF, Word, PowerPoint, Excel, JSON\*, HTML\*
-  Planos Advanced: PDF, Word, PowerPoint, Excel, PNG \ * \ *, TIFF \ * \ *, JPG \ * \ *, JSON \ *, HTML \ * 

\* Os documentos JSON e HTML são suportados pelo {{site.data.keyword.discoveryfull}}, mas não podem ser editados usando o editor do SDU. Para mudar a configuração de docs HTML e JSON, é necessário usar a API. Para obter mais informações, veja a [Referência de API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery/){: new_window}.

\*\* Os arquivos de imagem individual (PNG, TIFF, JPG) serão escaneados e o texto (se houver) será extraído. As imagens PNG, TIFF e JPEG integradas a arquivos PDF, Word, PowerPoint e Excel também serão escaneadas e o texto (se houver) será extraído.

Navegadores Suportados: Chrome e Firefox.

## Usando o editor do Smart Document Understanding
{: #annotate}

O editor do SDU está disponível somente para novas coleções que contêm tipos de documento suportados e não têm o enriquecimento Classificação de elementos aplicado. As coleções privadas existentes usarão o método de configuração original. Se quiser usar o editor do SDU em uma coleção existente, será necessário criar uma nova coleção e fazer upload desses documentos para ela. Se você não desejar usar o editor do SDU, será possível definir a sua configuração usando a API. Consulte a [Referência de API![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery/){: new_window}.
{: important}

As funções do editor do SDU estão disponíveis apenas no conjunto de ferramentas do {{site.data.keyword.discoveryshort}}; elas não estão disponíveis na API.
{: note}

Navegando no editor do Smart Document Understanding:

Se você ainda não tiver criado uma instância e um ambiente do {{site.data.keyword.discoveryshort}}, consulte [Introdução](/docs/services/discovery?topic=discovery-getting-started#getting-started) para obter instruções.
{: tip}

1. Na tela **Gerenciar dados**, clique no botão **Fazer upload de seus próprios dados** e crie uma nova coleção privada no {{site.data.keyword.discoveryshort}}.
1. Se você desejar, arraste e solte documentos em sua coleção ou clique em **procurar no computador** para fazer upload de documentos. Após o upload ser concluído, essas informações são exibidas:
   -  Os campos identificados a partir de seus documentos.
   -  Enriquecimentos aplicados a seus documentos. Os enriquecimentos Extração de entidade, Análise de sentimentos, Classificação de categoria e Identificação de conceito são aplicados automaticamente ao campo `text` pelo {{site.data.keyword.discoveryshort}} (a menos que você esteja importando documentos usando um conector). É possível incluir (ou remover) enriquecimentos adicionais para o campo `text`.
   -  Consultas pré-construídas que podem ser executadas imediatamente.
1. Clique em **Configurar dados** no canto superior direito. 
1. Na tela **Configurar dados**, haverá três guias: **Identificar campos**, **Gerenciar campos** e **Enriquecer campos**.

   - **Identificar campos** contém o editor do SDU. Essa guia substitui as guias **Converter** e **Normalizar** na tela original do {{site.data.keyword.discoveryshort}}. 
   - **Gerenciar campos** lista todos os campos indexados (todos os campos são indexados por padrão). Desative qualquer campo que você não deseja indexar. Por exemplo, seus PDFs podem conter um cabeçalho ou um rodapé em execução que não tem informações úteis, portanto, é possível excluir esses campos do índice. Também é possível dividir documentos aqui, com base nos campos. Consulte [Dividindo documentos](/docs/services/discovery?topic=discovery-sdu#splitting).
   - **Enriquecer campos** é idêntico à guia **Enriquecer** na tela original. Para obter mais informações sobre enriquecimentos, veja [Incluindo enriquecimentos](/docs/services/discovery?topic=discovery-configservice#adding-enrichments). A opção **Fazer upload de documentos de amostra** não está disponível com coleções do SDU.

   Se você não fez upload de nenhum documento anteriormente, retorne para a tela **Visão geral** clicando no nome de sua coleção na parte superior esquerda ou clique no ícone ![Gerenciar dados](/images/icon_yourData.png) e escolha a sua coleção. Arraste e solte documentos em sua coleção ou clique em **procurar no computador**. Depois de ter feito um upload inicial, o botão **Fazer upload de documentos** aparecerá na parte superior direita.
   {: important}

   Ao usar o Smart Document Understanding, somente o campo `text` pode ser enriquecido. Não tente enriquecer nenhum outro campo.
   {: important}

1. Abra a guia  ** Identificar campos ** . Um máximo de vinte (20) documentos de sua coleção serão carregados automaticamente no editor do Smart Document Understanding.

A barra de ferramentas na parte superior permitirá:
- Escolha um documento para anotar
- Navegar o documento exibido
- Ajustar a visualização da página (`single page view`, `zoom in`, `zoom out`), `clear changes` e `export/import models`. Clique em `single page view` para alternar a exibição. É possível visualizar suas anotações e documento separadamente ou juntos.

Também é possível efetuar crawl das origens de dados do Box, do Salesforce, do Microsoft SharePoint Online, do IBM Cloud Object Storage e do Microsoft SharePoint 2016 ou efetuar um crawl da web com o conjunto de ferramentas do {{site.data.keyword.discoveryshort}}. Clique no botão **Conectar uma origem de dados** e veja [Conectando-se a origens de dados](/docs/services/discovery?topic=discovery-sources#sources) para obter mais informações. Se você criar uma coleção usando esse método, nenhum enriquecimento será aplicado automaticamente.
{: tip}

## Como anotar um documento
{: #documents}

**Nota:** as tabelas são anotadas em uma etapa separada.

Veja [Melhores práticas para anotar em documentos e tabelas](/docs/services/discovery?topic=discovery-sdu#bestpractices) antes de começar a anotar.

1. Um conjunto padrão de campos aparecerá à direita de seu documento. Os campos disponíveis são `answer`, `author`, `footer`, `header`, `question`, `subtitle`, `table_of_contents`, `text` e `title`. Se quiser criar um ou mais novos rótulos de campo customizados, clique em **Criar novo**. Você está limitado ao seguinte número de rótulos customizados: Planos Lite - `0`, planos Advanced - `5`, planos Premium - `20`.
1. Clique em um rótulo de campo à direita para ativá-lo.
1. Clique no conteúdo que representa esse campo no editor do SDU. Ele será destacado. 
   - Como alternativa, é possível selecionar um rótulo de campo à direita e arrastá-lo para o conteúdo no editor do SDU. 
   - Para limpar uma mudança, clique no botão **Limpar mudança** na barra de ferramentas.
1. Clique em **Enviar**.
   **Nota:** conforme você anota, o Watson está aprendendo e iniciará a previsão de anotações. Continue anotando até que o Watson identifique os campos corretamente e consistentemente.
1. Quando você tiver concluído a anotação, clique em **Aplicar mudanças à coleção**. A tela  ** Fazer upload de seus documentos **  é aberta. Refazer upload dos documentos em sua coleção. Depois que o upload for concluído, você será redirecionado para a tela **Gerenciar dados**.

Campo | Definição  
------ | ------ 
resposta | Em um par de Q/A (geralmente em um FAQ), a resposta para a pergunta.
autor | Nome do autor (ou autores).
rodapé | Use essa tag para denotar meta informações sobre o documento (como o número da página ou referências), que aparecem na parte inferior da página.
cabeçalho | Use essa tag para denotar meta informações sobre o documento que aparecem na parte superior da página.
pergunta | Em um par de Q/A (geralmente em um FAQ), a pergunta.
subtítulo | O título secundário do documento que está sendo anotado. 
Table_of_contents | Use essa tag em listagens no índice de documento.
Texto | Use essa tag para o texto de cópia padrão, incluindo parágrafos, definições ou qualquer conjunto de palavras que não seja um título, parte de uma tabela, resposta, autor, subtítulo, cabeçalho ou rodapé. 
title | O título principal do documento que está sendo anotado.

## Como anotar uma tabela
{: #tables}

A anotação de tabela está em liberação beta. Um comunicado explicando os recursos beta pode ser localizado [aqui](/docs/services/discovery?topic=discovery-release-notes#beta-features).
{: important}

Veja [Melhores práticas para anotar em documentos e tabelas](/docs/services/discovery?topic=discovery-sdu#bestpractices) antes de começar a anotar.

1. Selecione o campo `table` do lado direito do editor do SDU e, em seguida, selecione a tabela no documento. 
1. Passe o mouse sobre a tabela para exibir o botão **Anotar tabela**. Clique no botão para abrir o editor de tabela.
1. Primeiro, destaque a tabela:
   - Selecione o campo `column`.
   - Clique em uma coluna na tabela para ativá-la.
   - Selecione o campo  ` linha ` .
   - Clique em uma linha na tabela para ativá-la.

   O esboço da tabela aparecerá na visualização da tabela à esquerda.

   **Nota:** à medida que você anota tabelas, o Watson está aprendendo e iniciará as anotações de previsão.
1. Segundo, rotule o conteúdo dentro da tabela.
1. Quando você tiver concluído a anotação da tabela, clique em **Anotação pronta**.
1. Clique em **Aplicar mudanças à coleção**. A tela  ** Fazer upload de seus documentos **  é aberta. Refazer upload dos documentos em sua coleção. Depois que o upload for concluído, você será redirecionado para a tela **Gerenciar dados**.

Use esse vídeo como um guia ![vídeo de anotação de tabela](images/SDU_table_demo.gif){: gif}

Campo | Definição  
------ | ------ 
corpo | Qualquer célula que não seja de cabeçalho contendo informações
cabeçalho da coluna | A célula de título (se presente) para cada coluna na tabela 
cabeçalho de múltiplas colunas | Qualquer célula de título que abrange mais de uma coluna
título da linha | O cabeçalho da coluna para a coluna de títulos de linha (se presente)
cabeçalho da linha | O rótulo da linha (se presente) para cada linha na tabela
cabeçalho de multilinhas | Qualquer rótulo da linha que abranja mais de uma linha

## Dividindo documentos
{: #splitting}

A guia **Gerenciar campos** contém a opção para **Melhorar os resultados da consulta dividindo seus documentos**. Essa opção permite dividir seus documentos em segmentos com base em um nome de campo. Uma vez dividido, cada segmento é um documento separado que será enriquecido, indexado e retornado como um resultado da consulta separado. 

Documentos são divididos com base em um nome de campo único, por exemplo: `title`, `author`, `question`. 

Considerações:

  - O número de segmentos por documento é limitado a `250`. Qualquer conteúdo do documento restante após `249` segmentos será armazenado no segmento `250`.

  - Cada segmento conta até o limite de documento de seu plano. O {{site.data.keyword.discoveryshort}} indexará segmentos até que o limite de plano seja atingido. Veja [Planos de precificação de descoberta](/docs/services/discovery?topic=discovery-discovery-pricing-plans#discovery-pricing-plans) para obter os limites do documento.

  - Metadados em PDF e Word, assim como quaisquer metadados customizados, são extraídos e incluídos no índice com cada segmento. Cada segmento de um documento incluirá metadados idênticos.

  - Se um documento dividido tiver sido atualizado e precisar ser transferido por upload novamente, ele deverá ser substituído usando o método [Atualizar documento ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#update-a-document){: new_window}. O documento deve ser transferido por upload usando o método POST da API `/environments/{environment_id}/collections/{collection_id}/documents/{document_id}`, especificando os conteúdos do campo `parent_id` de um dos segmentos atuais como a variável de caminho `{document_id}`. Todos os segmentos serão sobrescritos, a não ser que a versão atualizada do documento tenha menos seções totais do que a original. Esses segmentos mais antigos permanecerão no índice e poderão ser excluídos individualmente usando a API. Consulte a [Referência da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#delete-a-document){: new_window} para obter detalhes. 

## Importando e exportando modelos
{: #import}

Após definir um modelo com o editor do SDU, será possível salvá-lo e reutilizá-lo em outras coleções.

É possível importar ou exportar o seu modelo de SDU completo usando a barra de ferramentas na parte superior do editor. Clique no último ícone e escolha `Import model` ou `Export model`.

Os modelos exportados têm a extensão de arquivo `.sdumodel`. 

Um modelo importado é destinado a ser usado sem nenhuma anotação adicional. O modelo será completamente sobrescrito se você continuar anotando depois de importá-lo. Se você planeja importar um modelo em uma nova coleção, é uma boa prática criar uma nova coleção que contenha apenas um documento, importar o modelo e, em seguida, fazer upload do restante de seus documentos.

## Melhores práticas para anotar documentos e tabelas
{: #bestpractices}

A anotação de tabela está em liberação beta. Um comunicado explicando os recursos beta pode ser localizado [aqui](/docs/services/discovery?topic=discovery-release-notes#beta-features).
{: important}

- Siga todas as diretrizes e use rotulagem consistente em todos os documentos
- Não rotular espaço em branco
- Usar os rótulos de `image` em imagens e diagramas
- Não trate o texto em **negrito**, em _itálico_ ou sublinhado de forma diferente. Rotule com base no contexto, não no estilo. 
- Ao rotular um documento, trabalhe da primeira página até a última.
- Se você rotular incorretamente um item, escolha outro rótulo para o item para sobrescrever o primeiro.
- As páginas podem ser enviadas a qualquer momento. Assegure-se de que toda a rotulagem apropriada esteja completa antes de enviar.
- Os documentos e tabelas que parecem ter um texto sobrepondo outro texto são considerados "sobrepostos duplos" e não podem ser anotados. Relate esses documentos para seu administrador.
- Os documentos e tabelas que contêm múltiplas colunas de texto em uma única página não podem ser anotados. Relate esses documentos para seu administrador.
- As notas de rodapé devem ser rotuladas apenas quando aparecem na parte inferior da página e são mencionadas no corpo principal do texto no documento.
- As notas que aparecem em seções ou listas (por exemplo, chamadas explicitamente como "Notas") devem ser rotuladas como `text`.
- Se você não tiver certeza de que a tabela foi rotulada corretamente e que a área de janela de visualização se tornou não responsiva, a página deve ser recarregada em seu navegador e a tabela rotulada novamente para assegurar a exatidão.

