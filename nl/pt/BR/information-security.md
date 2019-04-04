---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-01-10"

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

# Segurança de informações
{: #information-security}

A IBM está comprometida em fornecer aos nossos clientes e parceiros soluções inovadoras de privacidade de dados, segurança e controle.
{: shortdesc}

**Aviso:**
os clientes são responsáveis por assegurar sua própria conformidade com várias leis e regulamentações, incluindo o Regulamento Geral sobre a Proteção de Dados da União Europeia. Os clientes são os únicos responsáveis por obter aconselhamento de consultoria jurídica competente quanto à identificação e interpretação de quaisquer leis e regulamentos relevantes que possam afetar os negócios dos clientes e quaisquer ações que os clientes possam precisar tomar para cumprir tais leis e regulamentações.

Os produtos, serviços e outros recursos descritos aqui não são adequados para todas as situações do cliente e podem ter disponibilidade restrita. A IBM não fornece aviso jurídico, contábil ou de auditoria nem representa ou garante que os seus serviços ou produtos assegurarão que os clientes estejam em conformidade com qualquer lei ou regulamentação.

Se você precisar solicitar suporte do GDPR para os recursos do {{site.data.keyword.cloud}} {{site.data.keyword.watson}} que forem criados

-   Na União Europeia (UE), veja [Solicitando suporte para recursos do IBM Cloud Watson criados na União Europeia](/docs/services/watson/getting-started-gdpr-sar.html#request-EU).
-   Fora da UE, veja [Solicitando suporte para recursos fora da União Europeia](/docs/services/watson/getting-started-gdpr-sar.html#request-non-EU).

## Regulamento Geral sobre a Proteção de Dados (GDPR) da União Europeia
{: #gdpr}

A IBM está comprometida em fornecer aos nossos clientes e parceiros soluções inovadoras de privacidade de dados, segurança e controle para auxiliá-los em sua jornada para a conformidade com GDPR.

Saiba mais sobre a própria jornada de prontidão GDPR da IBM e nossas capacidades e ofertas de GDPR para suportar sua jornada de conformidade [aqui ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/gdpr){: new_window}.

## Rotulando e excluindo dados no  {{site.data.keyword.discoveryshort}}
{: #gdpr-discovery}

O serviço {{site.data.keyword.discoveryshort}} inclui uma API para rotular dados por chamada.

Com essa API, é possível:

- Rotular seus dados com um ID de cliente.
- Excluir todos os dados para um ID de cliente específico, incluindo avisos relacionados.

Os dados são rotulados incluindo um `customer_id` de sua escolha (veja as restrições em [Como rotular dados](/docs/services/discovery?topic=discovery-information-security#labeling)) no cabeçalho `X-Watson-Metadata` opcional. O {{site.data.keyword.discoveryshort}}  pode, então, excluí-lo por  ` customer_id `.

Em qualquer chamada REST, um cabeçalho opcional `X-Watson-Metadata` pode ser enviado com pares `field=value` separados por ponto e vírgula, em que atualmente somente `customer_id` é persistido. Incluindo esse `customer_id` no cabeçalho `X-Watson-Metadata`, a solicitação indica que ela contém dados que pertencem a esse `customer_id`.

`customer_id`s são exclusivos dentro de uma única instância de serviço do {{site.data.keyword.discoveryshort}}. Ele NÃO é exclusivo por ambiente ou coleção. Eles não devem incluir dados pessoais.

**Nota:** os recursos experimentais e beta não são destinados ao uso com um ambiente de produção e, portanto, não é garantido que funcionem como esperado ao rotular e excluir dados. Os recursos experimentais e beta não devem ser usados ao implementar uma solução que requer a rotulagem e a exclusão de dados.

## Métodos que suportam a rotulagem de dados
{: #pi_methods}

As informações armazenadas a seguir podem ser excluídas usando um `customer_id` se o `customer_id` foi especificado quando as informações foram originalmente incluídas usando o método associado:

- consultas (`/v1/environments/{environment_id}/collections/{collection_id}/query`) Somente quando usado com os parâmetros `passages` ou `natural_langual_language_query`
- eventos (`/v1/events`)
- documentos (`/v1/environments/{environment_id}/collections/{collection_id}/documents`)
- avisos (`/v1/environments/{environment_id}/collections/{collection_id}/notices`) Somente `notices` de ingestão são rotulados.
- Entidades do Knowledge Graph (`/v1/environments/{environment_id}/collections/{collection_id}/query_entities`)
- Relações de Gráficos de Conhecimento (`/v1/environments/{environment_id}/collections/{collection_id}/query_relations`)
- dados de treinamento (`/v1/environments/{environment_id}/collections/{collection_id}/training_data`)

As informações armazenadas a seguir não são rotuladas explicitamente e não podem ser excluídas especificando o `customer_id`. Os dados pessoais não são suportados nestes campos.

Quaisquer campos de sequência (incluindo, mas não se limitando a `name` e `description`) dos itens armazenados a seguir:
- configurações
- coleções
- ambientes

## Rotulando dados
{: #labeling}

Ao alimentar documentos, inclua o cabeçalho `X-Watson-Metadata` usando as operações `POST /v1/environments/{environment_id}/collections/{collection_id}/documents` ou `POST /v1/environments/{environment_id}/collections/{collection_id}/documents/ID`. O campo `customer_id` é incluído no `extracted_metadata` dos documentos. Seu aplicativo deve ser configurado para fornecer um `customer_id` no cabeçalho `X-Watson-Metadata` ao executar qualquer operação.

Opcionalmente, é possível incluir o campo `customer_id` com a parte de formulário de multipartes `metadata` em vez de usar o cabeçalho `X-Watson-Metadata`.

**Nota:** se seus documentos já tiverem sido alimentados, será necessário realimentá-los para incluir o cabeçalho `X-Watson-Metadata` e o `customer_id`.

**Nota:** se você especificar um `customer_id` na parte de formulário de multipartes do `metadata` E no cabeçalho `X-Watson-Metadata` para o mesmo documento, o `customer_id` no cabeçalho `X-Watson-Metadata` será usado.

Restrições:

- O valor do cabeçalho `X-Watson-Metadata` não pode exceder 4 kilobytes de texto.
- O cabeçalho `X-Watson-Metadata` deve conter uma lista separada por ponto e vírgula de pares `field=value`. O `field` e o `value` não devem conter ponto e vírgula (`;`) ou sinais de igual (`=`).
- Os `customer_id`s são exclusivos em cada instância do {{site.data.keyword.discoveryshort}}. Ele NÃO é exclusivo por ambiente ou coleção.
- Um `customer_id` não pode ter mais de 256 caracteres de comprimento.
- Se um `customer_id` contiver somente espaço em branco ou estiver completamente vazio, ele será tratado como se o `customer_id` não fosse fornecido de forma alguma e nenhuma mensagem de erro será retornada.

### Rotulando dados com o Discovery Tooling
{: #labelingtooling}

Os dados podem ser rotulados com o campo `customer_id` ao usar o conjunto de ferramentas do {{site.data.keyword.discoveryshort}}. Clique em ![Detalhes do ambiente](images/env_icon.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> e insira o `customer_id` no campo **Rótulo de dados do GDPR**. Quando esse campo estiver configurado, todos os dados transferidos por upload usando esta sessão do navegador serão rotulados com o `customer_id` especificado, esse campo deverá ser mudado manualmente se o ID de cliente associado for mudado.

A inclusão de um `customer_id` com o campo **Rótulo de dados do GDPR** rotulará os documentos, os avisos, as entidades do Knowledge Graph, as relações do Knowledge Graph e os dados de treinamento dentro desse domínio de URL desse ponto em diante, incluindo cada instância sob esse domínio. Quaisquer ações (incluindo uploads de documentos) que ocorreram no conjunto de ferramentas do {{site.data.keyword.discoveryshort}} antes de incluir o campo **Rótulo de dados do GDPR** não serão rotuladas.

**Nota:** se você alternar domínios, navegadores, esvaziar o cache do navegador ou iniciar uma sessão incógnita depois de especificar seu `customer_id` usando o campo **Rótulo de dados do GDPR** do conjunto de ferramentas do {{site.data.keyword.discoveryshort}}, o `customer_id` não será retido e seus dados não serão rotulados. Se os domínios ou os navegadores tiverem que ser alternados, insira novamente o `customer_id` no campo **Rótulo de dados do GDPR**.

### Rotulando documentos usando o Crawler de dados
{: #labelingdc}

Se quaisquer documentos já tiverem sido submetidos a crawl com o Data Crawler, será necessário efetuar novamente o crawl deles para incluir o cabeçalho `X-Watson-Metadata` e `customer_id`.

1. Atualize sua configuração de adaptador de saída do {{site.data.keyword.discoveryshort}} Data Crawler para incluir o `customer_id`. Consulte  [ Configurando o adaptador de saída ](/docs/services/discovery?topic=discovery-configuring-the-data-crawler#output-adapter).
1. Planejar um crawl. Os documentos são enviados ao {{site.data.keyword.discoveryshort}} usando o cabeçalho `X-Watson-Metadata` e os documentos serão rotulados com o `customer_id` configurado.

## Excluindo dados rotulados
{: #deletingdata}

Os dados devem ser rotulados com um `customer_id` para excluí-los posteriormente.

1. Use a operação `DELETE /v1/user_data` e forneça o `customer_id` dos dados que você deseja excluir. `DELETE /v1/user_data` exclui todos os dados associados a um `customer_id` específico dentro dessa instância de serviço, conforme especificado em [Métodos que suportam dados de identificação](/docs/services/discovery?topic=discovery-information-security#pi_methods). Veja também a [Referência da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#delete-labeled-data){: new_window}

As exclusões são executadas de forma assíncrona. Não é possível rastrear o progresso das exclusões.

Para assegurar que todo o conteúdo rotulado seja removido corretamente, `user_delete` deve ser executado após as contagens de `processing` e `pending` para todas as coleções em seu ambiente retornarem `0`.

Se um `customer_id` não existente for fornecido, nada será excluído, mas uma resposta `200 - OK` será retornada.

Os ambientes e coleções não serão rotulados com um `customer_id`, mesmo se um cabeçalho `X-Watson-Metadata` for incluído na solicitação para criar o ambiente ou a coleção. Somente os documentos individuais em uma coleção dentro de um ambiente são rotulados. Portanto, quando os dados são excluídos, os ambientes e coleções individuais NÃO são excluídos.

Não é possível excluir dados rotulados usando o conjunto de ferramentas do {{site.data.keyword.discoveryshort}}.
