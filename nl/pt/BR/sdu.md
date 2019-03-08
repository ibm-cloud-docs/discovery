---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-10"

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

# Smart Document Understanding
{: #sdu}

O Smart Document Understanding (SDU) é uma nova maneira de anotar seus documentos no {{site.data.keyword.discoveryfull}}. 

O editor simplifica o treinamento de modelos de conversão customizados. A customização de como seus documentos são indexados no Discovery melhorará as respostas retornadas para seu aplicativo.

A SDU está em liberação beta. Um comunicado explicando os recursos beta pode ser localizado [aqui](/docs/services/discovery/release-notes.html#beta-features).

## Tipos de documentos e navegadores suportados
{: #doctypes}

Tipos de documentos suportados: PDF, Word, HTML. Os documentos JSON são suportados pelo {{site.data.keyword.discoveryfull}}, mas não são abertos no editor do SDU, porque eles são documentos estruturados.

Navegadores suportados para esta liberação beta: Chrome e Firefox

## Como anotar seus documentos
{: #annotate}

Para abrir o editor do Smart Document Understanding:

1. Abra  {{site.data.keyword.discoveryfull}}  usando o link beta.
1. Abra uma coleção de dados privados e, na tela **Gerenciar dados**, clique em ** Acessar as configurações de dados**. 
1. Na tela **Configurações de dados**, haverá duas guias: **Extrair campos** e **Enriquecer campos**.

   - ** Extrair campos **  contém o editor de SDU. Essa guia substitui as guias **Converter** e **Normalizar** em sua tela original do {{site.data.keyword.discoveryshort}}. 
   - **Enriquecer campos** é idêntico à guia **Enriquecer** na tela original. Para obter mais informações sobre enriquecimentos, veja [Incluindo enriquecimentos](/docs/services/discovery/building.html#adding-enrichments). A opção **Fazer upload de documentos de amostra** não está disponível em **Enriquecer campos**, porque ela não é necessária.

1. Vinte (20) documentos de sua coleção serão carregados automaticamente sob a guia **Extrair campos**, no editor do Smart Document Understanding.

A barra de ferramentas na parte superior permitirá:
- Escolher um documento
- Navegar o documento exibido
- Ajustar a visualização da página (`single page view`, `zoom in`, `zoom out`), `clear changes` e `export/import models`. Clique em `single page view` para alternar para uma tela que exibirá suas anotações e o documento separadamente. 

### Anotando um documento no editor do SDU
{: #documents}

**Nota:** as tabelas são anotadas em uma etapa separada.

Veja [Melhores práticas para rotular documentos e tabelas](/docs/services/discovery/sdu.html#bestpractices) antes de iniciar a anotação.

1. Um conjunto padrão de campos aparecerá à direita de seu documento. (Para o beta, não é possível criar campos customizados, mas esse recurso estará disponível no futuro.) Os campos disponíveis são `answer`, `author`, `footer`, `header`, `question`, `subtitle`, `table_of_contents`, `text` e `title`.
1. Clique em um nome de campo à direita para ativá-lo.
1. Clique no conteúdo que representa esse campo no editor do SDU. Ele será destacado. 
   - Alternativamente, é possível selecionar um nome de campo à direita e arrastá-lo para o conteúdo no editor do SDU. 
   - Para limpar uma mudança, clique no botão **Limpar mudança** na barra de ferramentas.
1. Clique em **Enviar**.
   **Nota:** conforme você anota, o Watson está aprendendo e iniciará a previsão de anotações. Continue anotando até que o Watson identifique os campos corretamente e consistentemente.
1. Quando você tiver concluído a anotação, clique em **Aplicar mudanças à coleção**. A tela  ** Fazer upload de seus documentos **  é aberta. (Isso mudará após beta.) Agora é possível fazer upload de seus documentos para que as configurações atualizadas sejam aplicadas à coleção inteira. Depois que o upload for concluído, você será redirecionado para a tela **Gerenciar dados**.


Campo | Definição  
------ | ------ 
resposta | Em um par de Q/A (geralmente em um FAQ), a resposta para a pergunta.
autor | Nome do autor (ou autores).
rodapé | Use essa tag para denotar meta informações sobre o documento (como o número da página ou referências), que aparecem na parte inferior da página.
cabeçalho | Use essa tag para denotar meta informações sobre o documento que aparecem na parte superior da página.
pergunta | Em um par de Q/A (geralmente em um FAQ), a pergunta.
subtítulo | O título secundário do documento que está sendo anotado. Use esse rótulo apenas uma vez por documento.
índice-de-conteúdo | Use essa tag em listagens no índice de documento.
text | Use essa tag para o texto de cópia padrão, incluindo parágrafos, definições ou qualquer conjunto de palavras que não seja um título, parte de uma tabela, resposta, autor, subtítulo, cabeçalho ou rodapé. 
title | O título principal do documento que está sendo anotado. Use esse rótulo apenas uma vez por documento.

### Anotando uma tabela no editor do SDU
{: #tables} 

1. Selecione o campo `table` à direita, em seguida, selecione a tabela no editor do SDU. 
1. Passe o mouse sobre a tabela no editor do SDU para exibir o botão **Anotar tabela**. Clique no botão para abrir o editor de tabela.
1. Primeiro, destaque a tabela:
   - Selecione o campo `column`.
   - Clique em uma coluna na tabela para ativá-la.
   - Selecione o campo  ` linha ` .
   - Clique em uma linha na tabela para ativá-la.

   O esboço da tabela aparecerá na visualização da tabela à esquerda.

   **Nota:** é possível clicar em **Prever** para visualizar uma predição do modelo de sua anotação de tabela.
1. Segundo, rotule o conteúdo dentro da tabela.
1. Quando você tiver concluído a anotação da tabela, clique em **Anotação pronta**.
1. Clique em **Aplicar mudanças à coleção**. A tela  ** Fazer upload de seus documentos **  é aberta. (Isso mudará após beta.) Depois que o upload for concluído, você será redirecionado para a tela **Gerenciar dados**.

Campo | Definição  
------ | ------ 
corpo da tabela | Qualquer célula que não seja de cabeçalho contendo informações
cabeçalho da coluna | A célula de título (se presente) para cada coluna na tabela 
cabeçalho de múltiplas colunas | Qualquer célula de título que abrange mais de uma coluna
título da subseção | O cabeçalho da coluna para a coluna de títulos de linha (se presente)
cabeçalho da linha | O rótulo da linha (se presente) para cada linha na tabela
cabeçalho de multilinhas | Qualquer rótulo da linha que abranja mais de uma linha

## Melhores práticas para rotular documentos e tabelas
{: #bestpractices}

- Siga todas as diretrizes e use rotulagem consistente em todos os documentos
- Não rotular espaço em branco
- Não rotular diagramas e imagens
- Não trate **negrito**, _itálico_ ou sublinhado de forma diferente, rotule com base no contexto, não no estilo. 
- Ao rotular um documento, trabalhe da primeira página até a última. Cada página deve ser enviada, mesmo que nada tenha sido rotulado. 
- Se você rotular incorretamente um item, escolha outro rótulo para o item para sobrescrever o primeiro.
- As páginas podem ser enviadas a qualquer momento. Assegure-se de que toda a rotulagem apropriada esteja completa antes de enviar.
- Não use a função de zoom em seu navegador ao rotular documentos.
- Os documentos e tabelas que parecem ter um texto sobrepondo outro texto são considerados "sobrepostos duplos" e não podem ser anotados. Relate esses documentos para seu administrador.
- Os documentos e tabelas que contêm múltiplas colunas de texto em uma única página não podem ser anotados. Relate esses documentos para seu administrador.
- As notas de rodapé devem ser marcadas somente quando elas aparecem na parte inferior da página e são referenciadas no corpo principal do texto no documento.
- As notas que aparecem em seções ou listas (por exemplo, explicitamente chamadas de "Notas") devem ser rotuladas como `text`.
- Se você não tiver certeza de que a tabela foi rotulada corretamente e que a área de janela de visualização se tornou não responsiva, a página deve ser recarregada em seu navegador e a tabela rotulada novamente para assegurar a exatidão.

