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

# Conectando-se às Origens de Dados
{: #sources}

O serviço {{site.data.keyword.discoveryshort}} permite que você se conecte e efetue crawl de documentos por meio de origens remotas.
{: shortdesc}

É possível conectar-se a uma origem de dados e puxar documentos em um planejamento (se desejado) para o serviço {{site.data.keyword.discoveryshort}}, configurando uma coleção para associar a essa origem. Cada coleção poderá ser configurada com uma origem de dados se o conjunto de ferramentas do {{site.data.keyword.discoveryshort}} estiver sendo usado. Se a API estiver sendo usada, será possível enviar documentos de múltiplas origens de dados para uma única coleção. O serviço {{site.data.keyword.discoveryshort}} puxa documentos da origem de dados usando um processo chamado crawling. Crawling é o processo de procurar e recuperar sistematicamente documentos do local de início especificado. Somente os itens especificados explicitamente são submetidos a crawl pelo serviço {{site.data.keyword.discoveryshort}}. Os tipos de origens de dados a seguir podem ser submetidos a crawl:

-  [Box](/docs/services/discovery?topic=discovery-sources#connectbox)
-  [ Salesforce ](/docs/services/discovery?topic=discovery-sources#connectsf)
-  [ Microsoft SharePoint Online ](/docs/services/discovery?topic=discovery-sources#connectsp)
-  [Microsoft SharePoint 2016 No local](/docs/services/discovery?topic=discovery-sources#connectsp_op)
-  [ Crawl da web ](/docs/services/discovery?topic=discovery-sources#connectwebcrawl)  (beta)
-  [ IBM Cloud Object Storage ](/docs/services/discovery?topic=discovery-sources#connectcos)

A conexão com uma origem de dados pode ser executada usando o conjunto de ferramentas do {{site.data.keyword.discoveryshort}} ou a API. O conjunto de ferramentas do {{site.data.keyword.discoveryshort}} fornece um método simplificado de conexão que requer menos entendimento dos sistemas de origem e a API fornece uma interface mais granular e altamente configurável que requer um entendimento maior da origem à qual você está se conectando. A visão geral do processo a seguir permite que você saiba quais seções deste documento devem ser lidas em seguida.

1.  Leia os [Requisitos gerais da origem](/docs/services/discovery?topic=discovery-sources#gen_req) para obter um entendimento geral do que será necessário.
2.  Leia os requisitos específicos para seu sistema de origem:
    -  [Box](/docs/services/discovery?topic=discovery-sources#connectbox)
    -  [ Salesforce ](/docs/services/discovery?topic=discovery-sources#connectsf)
    -  [ Microsoft SharePoint Online ](/docs/services/discovery?topic=discovery-sources#connectsp)
    -  [Microsoft SharePoint 2016 No local](/docs/services/discovery?topic=discovery-sources#connectsp_op)
    -  [ Crawl da web ](/docs/services/discovery?topic=discovery-sources#connectwebcrawl)  (beta)
    -  [ IBM Cloud Object Storage ](/docs/services/discovery?topic=discovery-sources#connectcos)
3.  Leia as instruções de configuração de origem com base em sua opção de configuração:
    -  [ Utilizando o conjunto de ferramentas ](/docs/services/discovery?topic=discovery-sources#source_tooling)
    -  [ Usando a API ](/docs/services/discovery?topic=discovery-sources#source_api)

Se você selecionar uma origem de dados no local, deverá primeiro instalar e configurar o IBM Secure Gateway. Veja [Instalando o IBM Secure Gateway para dados no local](/docs/services/discovery?topic=discovery-sources#gateway) para obter mais informações.

## Requisitos Gerais de Origem
{: #gen_req}

Os requisitos gerais a seguir se aplicam a todas as origens de dados:

-  O limite de tamanho do arquivo de documento individual para o Box, o Salesforce, o SharePoint Online, o SharePoint 2016, o IBM Cloud Object Storage e o Web Crawl é 10 MB.
-  Serão necessários as credenciais e os locais de arquivo (ou URLs) para cada origem de dados - estes são geralmente fornecidos por um desenvolvedor/administrador do sistema da origem de dados.
-  Será necessário saber de quais recursos da origem de dados será efetuado crawl. Isso pode ser fornecido pelo administrador de origem. Ao efetuar crawl do Box ou Salesforce, uma lista de recursos disponíveis é apresentada ao configurar uma origem usando o conjunto de ferramentas do {{site.data.keyword.discoveryshort}}.
-  Se estiver usando o conjunto de ferramentas do {{site.data.keyword.discoveryshort}}, uma coleção poderá ser configurada com uma origem de dados única. Se estiver usando a API, os documentos de múltiplas origens de dados poderão ser enviados para uma única coleção.
-  Efetuar crawl de uma origem de dados usará recursos (chamadas API) da origem de dados. O número de chamadas API depende do número de documentos que precisam ser submetidos a crawl. Um nível apropriado de licença de serviço (por exemplo, Enterprise) deve ser obtido para a origem de dados e o administrador do sistema de origem deve ser consultado.
-  Os crawls de origem do {{site.data.keyword.discoveryshort}} não excluem documentos que estão armazenados em uma coleção. Quando uma origem é submetida a crawl novamente, novos documentos são incluídos, o documento atualizado é modificado para a versão atual e os documentos excluídos permanecem como a última versão armazenada.
-  Os tipos de arquivo a seguir podem ser ingeridos pelo {{site.data.keyword.discoveryshort}}; todos os outros tipos de documento são ignorados:

Coleta | Planos Lite | Planos avançados 
---------------- | ------------------------------ | ------------------------------------------- 
Coleções existentes criadas especificamente para o {{site.data.keyword.discoveryfull}} antes da liberação do [Smart Document Understanding (SDU)](/docs/services/discovery?topic=discovery-release-notes#22jan19) | Microsoft Word, PDF, HTML, JSON | Microsoft Word, PDF, HTML, JSON     
Coleções criadas após a liberação do [SDU](/docs/services/discovery?topic=discovery-sdu#sdu) | PDF, Word, PowerPoint, Excel, JSON \ *, HTML \ * | PDF, Word, PowerPoint, Excel, PNG\*\*, TIFF\*\*, JPG\*\*, JSON\*, HTML\* 
    
\* Os documentos JSON e HTML são suportados pelo {{site.data.keyword.discoveryfull}}, mas não podem ser editados usando o editor do SDU. Para mudar a configuração de docs HTML e JSON, é necessário usar a API. Para obter mais informações, veja a [Referência de API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery/){: new_window}.

\*\* Os arquivos de imagem individual (PNG, TIFF, JPG) serão escaneados e o texto (se houver) será extraído. As imagens PNG, TIFF e JPEG integradas a arquivos PDF, Word, PowerPoint e Excel também serão escaneadas e o texto (se houver) será extraído.

## Box
{: #connectbox}

Será necessário criar um novo aplicativo Box customizado para se conectar ao {{site.data.keyword.discoveryfull}}. O aplicativo Box que você cria requer nível Corporativo ou acesso ao nível do Aplicativo.

-  Se você não for o administrador do Box para a sua organização, o [acesso ao **nível de Aplicativo**](/docs/services/discovery?topic=discovery-sources#applevelbox) será recomendado. Você precisará que um administrador aprove seu aplicativo.
-  Se você for o administrador do Box para a sua organização, o [acesso ao **nível Corporativo**](/docs/services/discovery?topic=discovery-sources#entlevelbox) será recomendado.

As etapas para configurar o acesso ao Box poderão mudar se houver uma atualização do Box. Consulte a [Documentação do desenvolvedor do Box ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.box.com/){: new_window} para obter atualizações.
{: note}

### Configurando o acesso ao nível do aplicativo
{: #applevelbox}

1.   Navegue para `https://app.box.com/developers/console` (use a URL do Box da sua empresa) e clique em **Criar novo app**.
1.   Na tela **Criar um novo aplicativo**, selecione **Integração corporativa** e clique em **Avançar**.
1.   Na tela **Método de autenticação**, selecione **OAuth 2.0 com JWT (Autenticação de servidor)** e clique em **Avançar**.
1.   Dê um nome ao seu app e clique no botão **Criar app**. Depois que o seu app do Box tiver sido criado, clique em **Visualizar o seu app**.
1.   Ao visualizar seu aplicativo, selecione **Acesso ao aplicativo** como **Aplicativo**. É possível usar os seus usuários gerenciados existentes à medida que você continua; não é necessário criar novos.
1.   Role para baixo até a seção **Escopos do aplicativo** da página e ative as caixas de seleção a seguir: 
     - `Read and write all folders stored in Box`
     - `Manage Users`
1.   Role para baixo até a seção **Recursos avançados** e ative as alternâncias a seguir:
     - `Perform Actions as Users`
     - `Generate User Access Tokens` 
1.  Clique no botão  ** Salvar mudanças ** .

As próximas poucas etapas exigirão assistência do Administrador da conta do Box da sua organização. Se você não for o Administrador do Box de sua organização, poderá identificar o Administrador abrindo o console do desenvolvedor do Box e olhando em **Configurações da conta** > **Detalhes da conta** > **Configurações**.

1.  [Etapa do administrador] Autorize o identificador de cliente de seu aplicativo em `https://app.box.com/master/settings/openbox` clicando no botão **Autorizar novo aplicativo**.
1.  [Etapa do administrador] Digite o **ID do cliente** em `https://app.box.com/developers/console` no campo **Chave de API** e, em seguida, clique no botão **Autorizar**.
1.  [Etapa do administrador] Recupere um token do desenvolvedor para o aplicativo. Para fazer isso, navegue até `https://app.box.com/developers/console`, role para a seção **Token do desenvolvedor** e gere seu token.
1.  Agora que o aplicativo foi autorizado pelo administrador, navegue até `https://developer.box.com/reference#page-create-an-enterprise-user` e crie um usuário do aplicativo usando a página de referência da API.

   Exemplo de curl para criar um usuário do aplicativo:

   ```bash
    curl https://api.box.com/2.0/users -H "Authorization: Bearer ACCESS_TOKEN" -d '{"name": "NedStark", "is_platform_access_only": true}' -X POST
   ```
   {: pre}

1.  Copie os conteúdos do campo **id** recém-gerado e forneça-os ao não administrador que está conectando o aplicativo Box ao {{site.data.keyword.discoveryfull}}.
1.  Depois que o usuário do aplicativo é criado, as pastas nas quais você deseja executar crawl precisam ser compartilhadas com o usuário do aplicativo, que deve receber permissões de `Viewer` nessas pastas. Isso requer o nome de login do usuário do aplicativo da resposta do comando curl acima. Exemplo: ` "login" :"AppUser_737729_jmUo@boxdevedition.com" `.
1.  Retorne para o console do desenvolvedor do Box `https://app.box.com/developers/console` e role até a seção **Incluir e gerenciar chaves públicas**. Clique em **Gerar o par de chaves pública/privada** e faça download de seu arquivo de par de chaves. Abra o arquivo.
1.  No arquivo de par de chaves, recorte e cole os campos a seguir no conjunto de ferramentas do {{site.data.keyword.discoveryshort}}.
    -  ` client_id `
    -  ` enterprise_id `
    -  `client_secret` 
    -  ` public_key_id ` 
    -  ` private_key ` 
    -  ` passphrase ` 

### Configurando o acesso ao nível Corporativo
{: #entlevelbox}

1.  Navegue para `https://app.box.com/developers/console` (use a URL do Box da sua empresa) e clique em **Criar novo app**.
1.  Na tela **Criar um novo aplicativo**, selecione **Integração corporativa** e clique em **Avançar**.
1.  Na tela **Método de autenticação**, selecione **OAuth 2.0 com JWT (Autenticação de servidor)** e clique em **Avançar**.
1.  Dê um nome ao seu app e clique no botão **Criar app**. Depois que o seu app do Box tiver sido criado, clique em **Visualizar o seu app**.
1.  Ao visualizar seu aplicativo, selecione **Acesso ao aplicativo** como **Corporativo**. É possível usar os seus usuários gerenciados existentes à medida que você continua; não é necessário criar novos.
1.  Role para baixo até a seção **Escopos do aplicativo** da página e ative as caixas de seleção a seguir: 
    - `Read and write all folders stored in Box`
    - `Manage Users`
    - ` Gerenciar propriedades corporativas `
1.  Role para baixo até a seção **Recursos avançados** e ative as alternâncias a seguir:
    - `Perform Actions as Users`
    - `Generate User Access Tokens` 
1.  Clique no botão  ** Salvar mudanças ** .

`Refresh` é suportado apenas com o acesso ao nível Corporativo.
{: note}

Se você mudar as configurações do aplicativo Box, `autorize novamente` seu aplicativo para que as mudanças entrem em vigor.
{: tip}

As próximas poucas etapas exigirão assistência do Administrador da conta do Box da sua organização. Se você não for o Administrador do Box de sua organização, poderá identificar o Administrador abrindo o console do desenvolvedor do Box e olhando em **Configurações da conta** > **Detalhes da conta** > **Configurações**.

1.  [Etapa do administrador] Autorize o identificador de cliente do seu aplicativo navegando até **Console administrativo** > **Configurações corporativas** > **Aplicativos** e role para `Custom applications`. URL de exemplo: ` https://app.box.com/master/settings/openbox `.
1.  [Etapa do administrador] Digite o **ID do cliente** em `https://app.box.com/developers/console` no campo **Chave de API** e, em seguida, clique no botão **Autorizar**.
1.  Retorne para o console do desenvolvedor do Box `https://app.box.com/developers/console` e role até a seção **Incluir e gerenciar chaves públicas**. Clique em **Gerar o par de chaves pública/privada** e faça download de seu arquivo de par de chaves. Abra o arquivo.
1.  No arquivo de par de chaves, recorte e cole os campos a seguir no conjunto de ferramentas do {{site.data.keyword.discoveryshort}}.
    -  ` client_id `
    -  ` enterprise_id `
    -  `client_secret` 
    -  ` public_key_id ` 
    -  ` private_key ` 
    -  ` passphrase ` 

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
-  `site_collection_path` - O `site_collection_path` da origem à qual essas credenciais se conectam.
-  `username` - o `client_id` da origem à qual essas credenciais se conectam. Esse usuário deve ter acesso a todos os sites e listas que precisam sofrer crawl e ser indexados.
-  `password` - a `password` da origem à qual essas credenciais se conectam. Esse valor nunca é retornado e é usado apenas ao criar ou modificar credenciais.

Ao identificar as credenciais, pode ser útil consultar a [documentação do desenvolvedor do Microsoft SharePoint ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.microsoft.com/en-us/sharepoint/dev/){: new_window}.

Outros itens a serem observados ao efetuar crawl do Microsoft SharePoint Online:

-  Para executar crawl do SharePoint, a conta do `Crawl User` deve ter permissões de `SiteCollection Administrator`.
-  Ao efetuar crawl do SharePoint, você precisará da lista de caminhos de coleta do site do SharePoint cujo crawl você deseja efetuar. O {{site.data.keyword.discoveryshort}} não suporta caminhos de pasta como uma entrada.

## Crawl da web
{: #connectwebcrawl}

Esse recurso beta pode ser usado em websites públicos de crawl que não requerem uma senha. É possível selecionar a frequência com que você gostaria que o {{site.data.keyword.discoveryshort}} sincronizasse com os websites, o idioma e o número de hops.

-  `Sync my data` - É possível optar por sincronizar a cada 5 minutos, por hora, diariamente, semanalmente ou mensalmente. 
-  `Select language` - Escolha o idioma dos websites na lista de idiomas suportados. Veja [Suporte ao idioma](/docs/services/discovery?topic=discovery-language-support#supported-languages) para obter a lista de idiomas suportados pelo {{site.data.keyword.discoveryshort}}. É recomendado criar uma coleção separada para cada idioma.
-  `URL group to sync` - Insira sua URL e clique no sinal de mais para incluí-la no grupo de URLs. Para especificar as **Configurações de crawl** para esse grupo de URLs, clique no ícone ![Cog](images/icon_settings.png). É possível configurar o **Máximo de hops**, que é o número de links consecutivos a serem seguidos da URL inicial (a URL inicial é `0`). O número padrão de hops é `2` e o máximo é `20` (se estiver usando a API, o máximo será `1000`). 

Para essa liberação beta, o número de páginas da web submetidas a crawl será limitado, portanto, o crawler da web pode não executar crawl em todos os websites especificados e atingir o número máximo de hops.
{: note}

Se você requerer diferentes **Configurações de crawl** para outras URLs, clique em **Incluir grupo de URLs** e crie um novo grupo. É possível criar quantos grupos de URLs você precisar.
{: tip}

## SharePoint 2016 On-Premise
{: #connectsp_op}

O Microsoft SharePoint 2016 (também conhecido como SharePoint Server 2016) é uma origem de dados no local. Para conectar-se a ele, deve-se primeiro instalar e configurar o IBM Secure Gateway. Veja [Instalando o IBM Secure Gateway para dados no local](/docs/services/discovery?topic=discovery-sources#gateway) para obter mais informações.
{: note}

As credenciais a seguir são necessárias para se conectar a uma origem de dados do SharePoint 2016 e elas devem ser obtidas de seu administrador do SharePoint:

-  `username` - o `client_id` da origem à qual essas credenciais se conectam. Esse usuário deve ter acesso a todos os sites e listas que precisam sofrer crawl e ser indexados.
-  `password` - a `password` da origem à qual essas credenciais se conectam. Esse valor nunca é retornado e é usado apenas ao criar ou modificar credenciais.
-  `web_application_url` - A `web_application_url` do SharePoint 2016. Por exemplo, https://sharepointwebapp.com:8443. Se a porta não for fornecida, ela será padronizada para a porta `80` para http e para a porta `443` para https.
-  `domain` - O `domain` da conta do SharePoint 2016.

Ao identificar as credenciais, pode ser útil consultar a [documentação do desenvolvedor do Microsoft SharePoint ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.microsoft.com/en-us/sharepoint/dev/){: new_window}.

Outros itens a observar ao executar crawl do Microsoft SharePoint 2016:

-  Para executar crawl do SharePoint 2016, a conta `Crawl User` deve ter permissões de `SiteCollection Administrator`.
-  Ao efetuar crawl do SharePoint, você precisará da lista de caminhos de coleta do site do SharePoint cujo crawl você deseja efetuar. O {{site.data.keyword.discoveryshort}} não suporta caminhos de pasta como uma entrada.

## IBM Cloud Object Storage
{: #connectcos}

Ao conectar-se a uma origem do IBM Cloud Object Storage, as credenciais a seguir são necessárias. Elas devem ser obtidas de seu administrador do IBM Cloud Object Storage:

-  `endpoint` - O `endpoint` usado para interagir com os dados do IBM Cloud Object Storage.
-  `access_key_id` - `access_key_id` obtido quando a instância do IBM Cloud Object Storage foi criada.
-  `secret_access_key` - `secret_access_key` para assinar solicitações obtidas quando a instância de armazenamento do IBM Cloud Object foi criada.

Depois que essas informações são inseridas, é possível escolher com que frequência você gostaria de sincronizar seus dados e selecionar os depósitos nos quais sincronizar.

Outros itens a observar ao executar crawl do IBM Cloud Object Storage:

-  Esse conector não suporta executar crawl de terminais privados.
-  Haverá um pequeno problema de desempenho se todos os depósitos forem selecionados. Nesse caso, pode haver um atraso antes que os documentos concluam a indexação.

## Usando o conjunto de ferramentas
{: #source_tooling}

A conexão a uma origem de dados usando o conjunto de ferramentas do {{site.data.keyword.discoveryshort}} é executada criando uma coleção especificamente para uma origem. Execute as etapas a seguir para criar uma coleção de origem e efetuar crawl dela:

1.  Na página **Gerenciar dados** do conjunto de ferramentas do {{site.data.keyword.discoveryshort}}, selecione **Conectar uma origem de dados**.
2.  Selecione a origem de dados à qual você deseja se conectar. Se você tiver selecionado uma origem de dados no local, primeiro será necessário instalar o IBM Secure Gateway. Consulte [Instalando o IBM Secure Gateway para dados no local](/docs/services/discovery?topic=discovery-sources#gateway) para obter mais informações. 
3.  Insira suas credenciais de origem e clique em conectar. Suas credenciais de origem devem ser obtidas com o administrador do sistema de origem.
4.  Escolha de quais dados você deseja efetuar crawl e com que frequência deseja sincronizá-los. Opções de sincronização:
    -  A cada cinco minutos: é executado a cada cinco minutos
    -  Por hora: é executado a cada hora
    -  Diariamente: é executado todos os dias entre as horas 0h e 6h no fuso horário especificado
    -  Semanalmente: é executado toda semana no domingo entre horas 0h e 6h no fuso horário especificado
    -  Mensal: é executado todo mês no primeiro domingo do mês entre as horas 0h e 6h no fuso horário especificado
    
    Status de crawl de exemplo:
    
    ```json
    "crawl_status" : {
    "source_crawl": {
      "status" : "completed",
      "next_crawl" : "2019-02-10T05:00:00-05:00"
    }
    ```
5.  Clique em **Salvar e sincronizar objetos** para iniciar o crawling de sua origem de dados. Em seguida, você é redirecionado para a tela de status da coleção que é atualizada conforme os documentos são incluídos na coleção.

O crawl sincronizará os dados inicialmente e, em seguida, na frequência especificada.
**Nota:** se você modificar qualquer coisa na tela **Configurações de sincronização** e, em seguida, clicar em **Salvar e sincronizar objetos**, um crawl será iniciado (ou reiniciado se um já estiver em execução) nesse momento.

## Usando a API
{: #source_api}

Use o processo a seguir para criar uma coleção conectada a uma origem de dados usando a API.

Se você planejar se conectar a uma origem de dados no local, primeiro precisará instalar o IBM Secure Gateway. Consulte [Instalando o IBM Secure Gateway para dados no local](/docs/services/discovery?topic=discovery-sources#gateway) para obter mais informações. 

O exemplo a seguir usa a origem de dados do SharePoint.

1.  Crie credenciais para a origem à qual você está se conectando usando a [API de credenciais de origem ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#create-credentials){: new_window}. Registre o **credential_id** retornado das credenciais recém-criadas.
2.  Crie uma nova configuração usando a [API de configuração ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#add-configuration){: new_window}. Essa configuração deve conter um objeto **source** que define o que deve ser submetido a crawl. O objeto **source** deve conter o **credential_id** que você registrou anteriormente.
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
3.  Crie uma nova coleção usando a [API de coleções ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/discovery#create-a-collection){: new_window}. O objeto que define a coleção deve conter o **configuration_id** que você registrou anteriormente.

O crawl de origem se inicia assim que a coleção é criada e, em seguida, novamente na frequência especificada.
**Nota:** se você modificar qualquer coisa no objeto **source** da configuração, um novo crawl será iniciado (ou reiniciado se um já estiver em execução) nesse momento.

### Especificando um  ` customer_id `
{: #source_customer_id}

Um campo `customer_id` em um documento alimentado do {{site.data.keyword.discoveryshort}} pode ser usado para excluir conteúdo com base no `customer_id` usando o método **user-data** na API. Os documentos recebidos de uma origem de dados não são designados automaticamente a um `customer_id` quando alimentados. Se seu aplicativo requer que um `customer_id` seja definido, é possível especificar que um (ou mais) dos campos recebidos do sistema de origem sejam copiados e usados como um `customer_id`. Para fazer isso, deve-se modificar a configuração que está sendo usada para conectar-se à origem.

1.  Execute uma consulta de amostra e identifique qual campo você deseja usar como um `customer_id`.
2.  Modifique a configuração. Será necessário incluir uma seção **Normalização** para criar o campo `customer_id`.
    -  No conjunto de ferramentas, navegue até sua coleção e clique no link **editar** na seção de configuração. Em seguida, clique na guia **Normalização** e inclua em uma normalização de **cópia** para criar o campo `customer_id`. Em seguida, clique em **Aplicar e salvar**.
![Normalização de cópia](images/norm_copy.png)
    -  Ao usar a API, inclua o objeto a seguir na matriz **normalizações**:
       ```json
       {
         "operation" : "copy",
         "source_field" : "{original_field_name}",
         "destination_field" : "customer_id"
       }
       ```
       {: codeblock}
3.  O próximo crawl planejado incluirá o campo `customer_id` em todos os documentos. Se você desejar que um crawl seja iniciado imediatamente, modifique a configuração de origem (**Configurações de sincronização** no conjunto de ferramentas).

Consulte [Segurança de informações](/docs/services/discovery?topic=discovery-information-security#information-security) para obter mais informações e informações sobre a exclusão com base no `customer_id`.

## Instalando o IBM Secure Gateway para dados no local 
{: #gateway}

Para se conectar a uma origem de dados no local, primeiro é necessário fazer download, instalar e configurar o IBM Secure Gateway. Depois de ter instalado o IBM Secure Gateway para sua primeira origem de dados no local, não será necessário repetir esse processo.

1.  Na página **Gerenciar dados** do conjunto de ferramentas do {{site.data.keyword.discoveryshort}}, selecione **Conectar uma origem de dados**.
1.  Selecione a origem de dados à qual você deseja se conectar. Ao selecionar uma origem de dados no local, acesse a seção **Conectar-se à rede no local** e clique no botão **Fazer conexão**.
1.  Na tela **Fazer download e instalar o Secure Gateway Client**, faça download da versão apropriada do IBM Secure Gateway.
1.  Depois de ter concluído o download, clique no botão **Fazer download do Secure Gateway e continuar**. Durante a instalação, será necessário o **ID do gateway** e o **Token** fornecidos na tela quando solicitado pelo Secure Gateway Client. Consulte [Instalando o cliente ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/docs/services/SecureGateway/securegateway_install.html#installing-the-client){: new_window} na documentação do Secure Gateway para obter instruções de instalação.
1.  Na máquina que estiver executando o Secure Gateway Client, abra o painel do Secure Gateway em http://localhost:9003.
1.  Clique em  ** incluir ACL **  no painel. Inclua a URL de terminal de cada coleção do SharePoint na lista **Permitir acesso**. Por exemplo, nome de host: `mycompany.sharepoint.com` e porta: `80`.
1.  Retorne para o conjunto de ferramentas do {{site.data.keyword.discoveryshort}} e clique em **Continuar**. Se a conexão for bem-sucedida, você verá a mensagem `Connection successful`. Se a conexão não foi bem-sucedida, abra o painel do Secure Gateway e verifique se os terminais na lista **Permitir acesso** estão corretos.

Após a conexão ser bem-sucedida, será possível começar a inserir as credenciais para a origem de dados no local.

## Conexão da origem de dados e isolamento de dados
{: #source_isolation}

[Conectar-se a origens de dados externas](/docs/services/discovery?topic=discovery-sources#sources) reduz o isolamento de dados de sua instância de serviço porque os dados em trânsito entre a origem e o serviço não podem ser isolados. Todos os outros isolamentos (em repouso, administração, consulta) permanecem na íntegra. Toda a comunicação em andamento entre os serviços e as origens de dados é criptografada usando o TLS v1.2. As chaves privadas para os certificados do TLS são criptografadas em repouso usando AES-256-GCM. Os certificados de serviço expiram a cada três anos e as listas de revogação de certificado são atualizadas mensalmente. Todas as credenciais são enviadas por meio de uma conexão criptografada usando o TLS v1.2 e criptografadas em repouso usando AES-256. As conexões com essas origens de dados usam qualquer protocolo seguro suportado por essas origens de dados.
