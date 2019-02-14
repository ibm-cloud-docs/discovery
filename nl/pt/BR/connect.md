---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-14"

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

# Conectando-se às Origens de Dados
{: #sources}

O serviço {{site.data.keyword.discoveryshort}} permite que você se conecte e efetue crawl de documentos por meio de origens remotas.
{: shortdesc}

É possível conectar-se a uma origem de dados e puxar documentos em um planejamento (se desejado) para o serviço {{site.data.keyword.discoveryshort}}, configurando uma coleção para associar a essa origem. Cada coleção pode ser configurada com uma origem de dados. O serviço {{site.data.keyword.discoveryshort}} puxa documentos da origem de dados usando um processo chamado crawling. Crawling é o processo de procurar e recuperar sistematicamente documentos do local de início especificado. Somente os itens especificados explicitamente são submetidos a crawl pelo serviço {{site.data.keyword.discoveryshort}}. Os tipos de origens de dados a seguir podem ser submetidos a crawl:

-  [Box](/docs/services/discovery/connect.html#connectbox)
-  [ Salesforce ](/docs/services/discovery/connect.html#connectsf)
-  [ Microsoft SharePoint Online ](/docs/services/discovery/connect.html#connectsp)

A conexão com uma origem de dados pode ser executada usando o conjunto de ferramentas do {{site.data.keyword.discoveryshort}} ou a API. O conjunto de ferramentas do {{site.data.keyword.discoveryshort}} fornece um método simplificado de conexão que requer menos entendimento dos sistemas de origem e a API fornece uma interface mais granular e altamente configurável que requer um entendimento maior da origem à qual você está se conectando. A visão geral do processo a seguir permite que você saiba quais seções deste documento devem ser lidas em seguida.

1.  Leia os [Requisitos gerais da origem](/docs/services/discovery/connect.html#gen_req) para obter um entendimento geral do que será necessário.
2.  Leia os requisitos específicos para seu sistema de origem:
    -  [Box](/docs/services/discovery/connect.html#connectbox)
    -  [ Salesforce ](/docs/services/discovery/connect.html#connectsf)
    -  [ Microsoft SharePoint Online ](/docs/services/discovery/connect.html#connectsp)
3.  Leia as instruções de configuração de origem com base em sua opção de configuração:
    -  [ Utilizando o conjunto de ferramentas ](/docs/services/discovery/connect.html#source_tooling)
    -  [ Usando a API ](/docs/services/discovery/connect.html#source_api)

## Requisitos Gerais de Origem
{: #gen_req}

Os requisitos gerais a seguir se aplicam a todas as origens de dados:

-  O limite de tamanho do arquivo de documento individual para Box, Salesforce e SharePoint Online é de 10 MB.
-  Serão necessários as credenciais e os locais de arquivo (ou URLs) para cada origem de dados - estes são geralmente fornecidos por um desenvolvedor/administrador do sistema da origem de dados.
-  Será necessário saber de quais recursos da origem de dados será efetuado crawl. Isso pode ser fornecido pelo administrador de origem. Ao efetuar crawl do Box ou Salesforce, uma lista de recursos disponíveis é apresentada ao configurar uma origem usando o conjunto de ferramentas do {{site.data.keyword.discoveryshort}}.
-  Efetuar crawl de uma origem de dados usará recursos (chamadas API) da origem de dados. O número de chamadas depende do número de documentos submetidos a crawl. Um nível apropriado de serviço (por exemplo, Enterprise) deve ser obtido para a origem de dados e o administrador do sistema de origem consultado.
-  Os tipos de arquivos a seguir podem ser alimentados pelo {{site.data.keyword.discoveryshort}}, todos os outros tipos de documento são ignorados:
   -  Microsoft Word
   -  PDF
   -  HTML
   -  JSON
-  Os crawls de origem do {{site.data.keyword.discoveryshort}} não excluem documentos que estão armazenados em uma coleção. Quando uma origem é submetida a crawl novamente, novos documentos são incluídos, o documento atualizado é modificado para a versão atual e os documentos excluídos permanecem como a última versão armazenada.

## Box
{: #connectbox}

Ao conectar-se a uma origem Box, assegure-se de que a instância à qual você planeja se conectar seja um plano Corporativo ou superior.

Configurando uma conta do Box para trabalhar com o {{site.data.keyword.discoveryshort}}:

1.  Crie um novo aplicativo customizado do Box em `https://app.box.com/developers/console` (use a URL do Box da sua empresa).
1.  Em seguida, execute um dos seguintes procedimentos:
    - Selecione **Acesso ao aplicativo** de `Enterprise` e, em seguida, continue usando os usuários gerenciados existentes.
      OR
    - Selecione **Acesso ao aplicativo** de `Application` e, em seguida, crie um `Application User` com o aplicativo recém-criado usando a [API do Box ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.box.com/reference#create-app-user){: new_window}.
1.  Ative os seguintes  ** Escopos de Aplicativo **:
    - `Read and Write All Folders Stored In Box`
    - `Manage Users`
1.  Ative os  ** Advanced Features ** a seguir
    - `Perform Actions as Users`
    - `Generate User Access Tokens`
1.  Faça com que o administrador autorize seu ID de cliente de aplicativo `https://app.box.com/master/settings/openbox` digitando o `Client ID` de `https://app.box.com/developers/console` no campo `API Key`.
1.  Gere o `public/private keypair` (será transferido por download em seu computador).
1.  Abra o arquivo transferido por download e copie/cole os campos no {{site.data.keyword.discoveryshort}}. Remova `\n` de nova linha final no término do `privateKey` ao copiar para o {{site.data.keyword.discoveryshort}}.

**Nota:** o {{site.data.keyword.discoveryshort}} não suporta o crawling de aplicativo customizado como ele próprio (não é possível personificar você mesmo). 

As credenciais a seguir são necessárias para se conectar a uma origem Box, elas devem ser obtidas com seu administrador do Box (a menos que você já as tenha obtido pela configuração de um aplicativo customizado do Box usando as etapas anteriores):

-  `client_id` - o `client_id` da origem à qual essas credenciais se conectam.    
-  `enterprise_id` - o `enterprise_id` do site do Box ao qual essas credenciais se conectam.
-  `client_secret` - o `client_secret` da origem à qual essas credenciais se conectam. Esse valor nunca é retornado e é usado apenas ao criar ou modificar credenciais.
-  `public_key_id` - o `public_key_id` da origem à qual essas credenciais se conectam. Esse valor nunca é retornado e é usado apenas ao criar ou modificar credenciais.
-  `private_key` - o `private_key` da origem à qual essas credenciais se conectam. Esse valor nunca é retornado e é usado apenas ao criar ou modificar credenciais.
-  `passphrase` - o `passphrase` da origem à qual essas credenciais se conectam. Esse valor nunca é retornado e é usado apenas ao criar ou modificar credenciais.

Ao identificar as credenciais, pode ser útil consultar a [documentação do desenvolvedor do Box ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.box.com/){: new_window}.

Outros itens a serem considerados ao efetuar crawl do Box:

-  As notas do Box são armazenadas no formato JSON, portanto, quaisquer notas do Box nas pastas especificadas serão alimentadas pelo {{site.data.keyword.discoveryshort}}.
-  Ao usar a API, será necessário ter uma lista de IDs de pastas e o ID do proprietário associado para cada pasta em que você deseja efetuar crawl. O conjunto de ferramentas do {{site.data.keyword.discoveryshort}} permite que você navegue e selecione em qual conteúdo será efetuado crawl.

## Salesforce
{: #connectsf}

Ao conectar-se a uma origem Salesforce, assegure-se de que a instância à qual você planeja se conectar seja um plano Corporativo ou superior.

As credenciais a seguir são necessárias para se conectar a uma origem Salesforce, elas devem ser obtidas com o administrador do Salesforce:
-  `url` - a `url` da origem à qual essas credenciais se conectam.
-  `username` - o `username` da origem à qual essas credenciais se conectam.
-  `password` - a `password` consiste na senha do Salesforce e em um token de segurança da Salesforce válido concatenado. Esse valor nunca é retornado e é usado apenas ao criar ou modificar credenciais.

Ao identificar as credenciais, pode ser útil consultar a [documentação do desenvolvedor do Salesforce ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.salesforce.com/docs/){: new_window}.

Outros itens a serem observados ao efetuar crawl do Salesforce:

-  Os artigos de conhecimento serão submetidos a crawl somente se sua **version** for `published` e seu idioma for `en-us`.
-  Ao usar a API, será necessário ter uma lista de objetos do Salesforce dos quais você deseja efetuar crawl. O conjunto de ferramentas do {{site.data.keyword.discoveryshort}} permite que você navegue e selecione em qual conteúdo será efetuado crawl.


## SharePoint Online
{: #connectsp}

Ao conectar-se a uma origem Microsoft SharePoint Online, assegure-se de que a instância à qual você planeja se conectar seja um plano Corporativo (E1) ou superior.

As credenciais a seguir são necessárias para se conectar a uma origem SharePoint Online, elas devem ser obtidas do administrador do SharePoint:

-  `organization_url` - a ` organization_url` da origem à qual essas credenciais se conectam.
-  `site_collection.path` - o `site_collection.path` da origem à qual essas credenciais se conectam.
-  `username` - o `client_id` da origem à qual essas credenciais se conectam.
-  `password` - a `password` da origem à qual essas credenciais se conectam. Esse valor nunca é retornado e é usado apenas ao criar ou modificar credenciais.

Ao identificar as credenciais, pode ser útil consultar a [documentação do desenvolvedor do Microsoft SharePoint ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.microsoft.com/en-us/sharepoint/dev/){: new_window}.

Outros itens a serem observados ao efetuar crawl do Microsoft SharePoint Online:

-  Ao efetuar crawl do SharePoint, será necessário ter uma lista de caminhos de coleção de sites do SharePoint dos quais você deseja efetuar crawl. O conjunto de ferramentas do {{site.data.keyword.discoveryshort}} permite que você navegue e selecione em qual conteúdo será efetuado crawl. Para efetuar crawl de seu site inteiro do SharePoint Online, não selecione múltiplos caminhos (URLs) neste campo. Nesse cenário, insira um `/` no campo `site_collection.path`.

## Usando o conjunto de ferramentas
{: #source_tooling}

A conexão a uma origem de dados usando o conjunto de ferramentas do {{site.data.keyword.discoveryshort}} é executada criando uma coleção especificamente para uma origem. Execute as etapas a seguir para criar uma coleção de origem e efetuar crawl dela:

1.  Na página **Gerenciar dados** do conjunto de ferramentas do {{site.data.keyword.discoveryshort}}, selecione **Conectar uma origem de dados**.
2.  Selecione a origem de dados à qual você deseja se conectar.
3.  Insira suas credenciais de origem e clique em conectar. Suas credenciais de origem devem ser obtidas com o administrador do sistema de origem.
4.  Escolha de quais dados você deseja efetuar crawl e com que frequência deseja sincronizá-los.
5.  Clique em **Salvar e sincronizar objetos** para iniciar o crawling de sua origem de dados. Em seguida, você é redirecionado para a tela de status da coleção que é atualizada conforme os documentos são incluídos na coleção.

O crawl sincronizará os dados inicialmente e, em seguida, na frequência especificada.
**Nota:** se você modificar qualquer coisa na tela **Configurações de sincronização** e, em seguida, clicar em **Salvar e sincronizar objetos**, um crawl será iniciado (ou reiniciado se um já estiver em execução) nesse momento.

## Usando a API
{: #source_api}

Use o processo a seguir para criar uma coleção conectada a uma origem de dados usando a API.
1.  Crie credenciais para a origem à qual você está se conectando usando a [API de credenciais de origem ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#credentials-api){: new_window}. Registre o **credential_id** retornado das credenciais recém-criadas.
2.  Crie uma nova configuração usando a [API de configuração ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#configurations-api){: new_window}. Essa configuração deve conter um objeto **source** que define o que deve ser submetido a crawl. O objeto **source** deve conter o **credential_id** que você registrou anteriormente.
    ```json
    "source" : {
      "type" : "salesforce",
      "credential_id" : "{credential_id}",
      "schedule" : {
        "enabled" : true,
        "time_zone" : "America/New_York",
        "frequency" : "weekly"
      },
      "options" : {
         "site_collections": [ {
         "site_collection_path" : "/sites/TestSiteA",
         "limit" : 10
         } ]
      }
    }
    ```
    {: codeblock}
    Registre o **configuration_id** retornado da configuração recém-criada.
3.  Crie uma nova coleção usando a [API de coleções ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#configurations-api){: new_window}. O objeto que define a coleção deve conter o **configuration_id** que foi registrado anteriormente.

O crawl de origem se inicia assim que a coleção é criada e, em seguida, novamente na frequência especificada.
**Nota:** se você modificar qualquer coisa no objeto **source** da configuração, um novo crawl será iniciado (ou reiniciado se um já estiver em execução) nesse momento.

## Especificando um  ` customer_id `
{:# source_customer_id}

Um campo `customer_id` em um documento alimentado do {{site.data.keyword.discoveryshort}} pode ser usado para excluir conteúdo com base no `customer_id` usando o método **user-data** na API. Os documentos recebidos de uma origem de dados não são designados automaticamente a um `customer_id` quando alimentados. Se seu aplicativo requer que um `customer_id` seja definido, é possível especificar que um (ou mais) dos campos recebidos do sistema de origem sejam copiados e usados como um `customer_id`. Para fazer isso, deve-se modificar a configuração que está sendo usada para conectar-se à origem.

1.  Execute uma consulta de amostra e identifique qual campo você deseja usar como um `customer_id`.
2.  Modifique a configuração. Será necessário incluir uma seção **Normalização** para criar o campo `customer_id`.
    -  No conjunto de ferramentas, navegue até sua coleção e clique no link **editar** na seção de configuração. Em seguida, clique na guia **Normalização** e inclua em uma normalização de **cópia** para criar o campo `customer_id`. Em seguida, clique em **Aplicar e salvar**.
![Normalização de cópia](images/norm_copy.png)
    -  Ao usar a API, inclua o objeto a seguir na matriz **normalizações**"
       ```json
       {
         "operation" : "copy",
         "source_field" : "{original_field_name}",
         "destination_field" : "customer_id"
       }
       ```
       {: codeblock}
3.  O próximo crawl planejado incluirá o campo `customer_id` em todos os documentos. Se você desejar que um crawl seja iniciado imediatamente, modifique a configuração de origem (**Configurações de sincronização** no conjunto de ferramentas).

Veja [Segurança de informações ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.bluemix.net/docs/services/discovery/information-security.html){: new_window} para obter mais informações e informações sobre a exclusão com base no `customer_id`.
