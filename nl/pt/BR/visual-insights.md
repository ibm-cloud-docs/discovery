---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-30"

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

# Watson Discovery Visual Insights
{: #visual-insights}

{{site.data.keyword.discoveryfull}} Visual Insights é um recurso experimental que pode ser usado para explorar visualmente as conexões identificadas pelo entendimento do {{site.data.keyword.discoveryshort}} de elementos de semântica, relações, conceitos e mais.

É possível usar o {{site.data.keyword.discoveryfull}} Visual Insights para saber mais sobre suas coleções, antes de usar o {{site.data.keyword.discoveryshort}} para criar consultas que podem ser integradas em seu novo aplicativo ou solução existente que apontará os usuários às informações que eles precisam.

Durante a liberação experimental, o Visual Insights está disponível apenas em ambientes públicos.

**Renúncia de responsabilidade:** o Visual Insights é um recurso experimental, o que significa que ele pode ser instável, pode mudar frequentemente e pode ser descontinuado em um curto prazo. Ele é fornecido para poder avaliar sua funcionalidade. Ele não deve fornecer o mesmo nível de desempenho ou de compatibilidade que os recursos liberados geralmente fornecem. Ele não é projetado para uso em um ambiente de produção e qualquer uso é sob sua responsabilidade. Consulte [Recursos Beta/Experimental](/docs/services/discovery/release-notes.html#beta-features) para obter detalhes.

## Um tour rápido do Visual Insights
{: #quick-tour-visual-insights}

![Tour rápido do Discovery Visual Insights](images/discovery-visualinsights-quicktour.png)

A tela do Visual Insights é dividida em 4 áreas principais.

### Barra de procura
{: #search-bar}

É possível consultar coleções do {{site.data.keyword.discoveryshort}} usando a **Barra de procura** na parte superior.

- Se você efetuou login com suas credenciais do {{site.data.keyword.Bluemix_notm}}, todas as coleções das instâncias do {{site.data.keyword.discoveryshort}} associadas à sua conta estarão disponíveis na lista suspensa de coleção ({{site.data.keyword.discoverynewsfull}} por padrão). Se você não estiver com login efetuado, apenas a coleção do {{site.data.keyword.discoverynewsfull}} estará disponível.
- Escolha sua coleção, insira sua consulta (por exemplo, `Qual é neutralidade de rede`) na caixa de procura e clique no botão **Procurar** para procurar. Para coleções grandes, possivelmente levará um minuto ou mais para que os resultados sejam exibidos. É possível filtrar sua procura clicando nos botões `documents`, `concepts`, `people`, `locations`, `organizations` ou `companies`.
- É possível, opcionalmente, selecionar qualquer item nos resultados exibidos (entidade, conceito ou documento) clicando no ícone ![ícone de Consulta](images/discovery-query-icon.png) no cabeçalho.
- Se uma coleção privada for selecionada e nenhuma consulta tiver sido inserida, até 1.000 documentos da coleção serão exibidos na [Área de janela Detalhes](/docs/services/discovery/visual-insights.html#details-pane). Se a coleção do {{site.data.keyword.discoverynewsshort}} for escolhida e nenhuma consulta tiver sido inserida, uma seleção de 100 artigos recentes será exibida.

### Exibição de rede
{: #network-display}

O painel central sob a barra de procura é a **Exibição de rede**. Essa é a visualização interativa de seus resultados da consulta.

- **Exibição de rede** é uma representação gráfica dos documentos, entidades e conceitos extraídos dos resultados da consulta. Os nós rosa representam documentos e os azuis representam entidades ou conceitos. Cada nó de documento está ligado a todos os nós de entidades e de conceito que foram detectados nesse documento pelo {{site.data.keyword.discoveryshort}}. Quanto mais semelhantes forem os documentos, mais próximo eles serão localizados um do outro na visualização.
- Passar o mouse sobre qualquer nó na **Exibição de rede** exibe seu título associado e destaca seus links para outros nós.
- Clicar em qualquer nó exibe informações sobre esse nó na [Área de janela Detalhes](/docs/services/discovery/visual-insights.html#details-pane).

### Área de janela Detalhes
{: #details-pane}

À direita da Exibição de rede se encontra a **Área de janela Detalhes**.

- A área de janela Detalhes fornece mais detalhes sobre cada documento, incluindo sua classificação e data (se disponível), um trecho curto (com a opção para abrir o documento completo), bem como entidades e conceitos que estão vinculados.
- Se um nó que não é de documento for selecionado na Exibição de rede, as informações sobre esse nó serão exibidas na parte superior da área de janela Detalhes.
- Clicar em qualquer uma das entidades ou conceitos vinculados na área de janela Detalhes seleciona o nó correspondente na Exibição de rede.

### Área de janela Navegação
{: #navigation-pane}

À esquerda da Exibição de rede se encontra a **Área de janela Navegação**. Essa área de janela fornece uma visão geral de nuvem de tag dos termos mais comuns extraídos dos resultados da consulta na coleção escolhida. Quanto maior o termo, mais comum ele é nos resultados da consulta.

- A seleção de qualquer termo na nuvem de tag o torna rosa e destaca todos os documentos na exibição de rede que estejam associados a ele. A área de janela Detalhes exibe a lista de documentos destacados. Os outros termos na nuvem de tag agora indicam seus relacionamentos com o termo selecionado:
  - Termos esmaecidos não estão associados a nenhum dos documentos destacados.
  - Quando um termo se torna violeta, ele está associado a todos os documentos destacados e não é útil ao tentar distinguir entre os documentos.
  - Os termos que permanecem azuis estão associados a alguns dos, mas não a todos os documentos destacados e podem, portanto, ser usados para refinar ainda mais o conjunto de documentos destacados. A seleção de um desses termos reduz o conjunto de documentos destacados para apenas aqueles que estejam associados às duas tags e amplia a exibição de rede até a região na qual os documentos estão localizados. Este método pode ser usado para refinar um grande conjunto de documentos para um conjunto menor com apenas alguns cliques.
- Para desmarcar um termo selecionado, clique no termo novamente. Para desmarcar todos os termos selecionados, clique em um local em branco entre as palavras na nuvem de tag. Clicar em uma tag cinza limpará a seleção existente e selecionará esse termo.
- Os tipos e contagens dos documentos, pessoas, conceitos, organizações, locais e as empresas são exibidos acima da nuvem de tag. Clique em qualquer um deles para filtrar a nuvem de tag e a visualização da Exibição de rede.

## Utilizando o Visual Insights
{: #using-visual-insights}

É possível usar o Visual Insights para consultar o {{site.data.keyword.discoverynewsfull}} sem efetuar login. Para usar o Visual Insights com suas próprias coleções, é necessária:

- Uma conta do {{site.data.keyword.Bluemix_notm}} que contenha uma instância do {{site.data.keyword.discoveryshort}}.
- Uma ou mais coleções nessa instância do {{site.data.keyword.discoveryshort}} que foram melhoradas com o enriquecimento [Extração de entidade](/docs/services/discovery/building.html#entity-extraction), mais, opcionalmente, qualquer um dos enriquecimentos [Identificação de Conceito](/docs/services/discovery/building.html#concept-tagging), [Extração de Palavra-chave](/docs/services/discovery/building.html#keyword-extraction), [Extração de Relacionamento](/docs/services/discovery/building.html#relation-extraction) e [Classificação de Categoria](/docs/services/discovery/building.html#category-classification). Outros enriquecimentos podem ser incluídos, mas não serão representados pelo Visual Insights.

Mais informações sobre {{site.data.keyword.discoveryshort}} e como iniciar gratuitamente, consulte [Watson {{site.data.keyword.discoveryshort}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/watson/services/discovery/){: new_window}.

Quando você possui uma conta do {{site.data.keyword.Bluemix_notm}}, uma instância do {{site.data.keyword.discoveryshort}} e uma ou mais coletas preenchidas, suas coleções são exibidas no Visual Insights ao efetuar login.

Efetuando login no Visual Insights

1. Abra o [{{site.data.keyword.discoveryshort}} Visual Insights ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://visual-insights.bluemix.net){: new_window}.
1. Clique no ícone ![Ícone do perfil](images/discovery-profile-icon.png) na barra de procura.
1. Insira seu ID e senha do {{site.data.keyword.Bluemix_notm}}. Dentro de alguns instantes suas coleções estarão disponíveis para seleção na Barra de procura.

## Fornecendo feedback
{: #providing-feedback}

Estamos interessados em seu feedback no {{site.data.keyword.discoveryshort}} Visual Insights. Para acessar o link de feedback, clique no ícone ![Ícone de informações](images/discovery-info-icon.png) no cabeçalho.
