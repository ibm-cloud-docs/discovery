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
{:curl: #curl .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}

# Introdução à API

Neste curto tutorial, apresentamos a API do {{site.data.keyword.discoveryshort}} e
percorreremos o processo de criação e de procura de uma coleção de dados privados.
{: shortdesc}

## Antes de Começar
{: #before-you-begin}

- Crie uma instância do serviço:
    - {: download} Se estiver vendo isso, você criou sua instância de serviço. Agora, obtenha suas credenciais.
    - Crie um projeto por meio de um serviço:
        1.  Acesse a página {{site.data.keyword.watson}} Developer Console [Services ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.{DomainName}/developer/watson/services){: new_window}.
        1.  Selecione {{site.data.keyword.discoveryshort}}, clique em **Incluir serviços** e inscreva-se em uma conta grátis do {{site.data.keyword.Bluemix_notm}} ou efetue login.
        1.  Digite `discovery-tutorial` como o nome do projeto e clique em **Criar projeto**.
- Copie as credenciais para autenticar sua instância de serviço:
    - {: download} No painel de serviço (que você está olhando):
        1.  Clique na guia **Credenciais de serviço**.
        1.  Clique em **Visualizar credenciais** em **Ações**.
        1.  Copie os valores de `username`, `password` e `url` .
        {: download}
    - No seu projeto **Tutorial de descoberta** no Developer Console, copie os
valores de `username`, `password` e `url` para
`"discovery"` na seção **Credenciais**.

<!-- Remove this text after dedicated instances have the Developer Console: begin -->

Se você usa o {{site.data.keyword.Bluemix_dedicated_notm}}, crie sua instância de serviço na página [{{site.data.keyword.discoveryshort}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.{DomainName}/catalog/services/discovery/){: new_window} no catálogo. 
Para obter detalhes sobre como localizar suas credenciais de serviço, consulte
[Credencias
de serviço para serviços do Watson ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/watson/getting-started-credentials.html#getting-credentials-manually){: new_window}.

<!-- Remove this text after dedicated instances have the Developer Console: end -->

## Etapa 1: Crie um ambiente
{: #create-an-environment}

Em um shell bash ou ambiente equivalente, como Cygwin, use o método `POST /v1/environments` para criar um ambiente. Pense no ambiente como o warehouse em que você está armazenando todas as suas caixas de documentos.

1.  Emita o seguinte comando para criar um ambiente chamado `my-first-environment`. 
Substitua `{username}` e `{password}` pelas credenciais de serviço que
você copiou anteriormente:

    ```bash
    curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    A API retorna informações, como seu ID de ambiente, o status do ambiente e a quantia de armazenamento
que seu ambiente está usando.

1.  Verifique o status do ambiente periodicamente até que você veja um status de
`ready`.
    - Emita uma chamada para o método `GET /v1/environments/{environment_id}` para
recuperar o status de seu ambiente. Substitua `{username}`, `{password}` e `{environment_id}` por suas informações:

    ```bash
    curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}?version=2017-11-07
    ```
    {: pre}

    O status deve ser `ready` para poder criar uma coleção.

## Etapa 2: crie uma coleção
{: #create-a-collection}

Agora que o ambiente está pronto, é possível criar uma coleção. Pense em uma coleção como uma caixa na qual você armazena os documentos em seu ambiente.

1.  Primeiramente, é necessário o ID de sua configuração padrão. Para localizar seu
`configuration_id` padrão, use o método `GET /v1/environments/{environment_id}/configurations`. Substitua `{username}`, `{password}` e `{environment_id}` por suas informações:

    ```bash
      curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07
    ```
    {: pre}
1.  Use o método `POST /v1/environments/{environment_id}/collections`
para criar uma coleção chamada **my-first-collection**.
Substitua `{username}`, `{password}`, `{environment_id}` e `{configuration_id}` por suas informações:

    ```bash
    curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{"name": "my-first-collection", "description": "exploring collections", "configuration_id":"{configuration_id}" , "language": "en_us"}' https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07
    ```
    {: pre}

    A API retorna informações, como seu ID de coleção, o status da coleção e a quantia de armazenamento que sua
coleção está usando.
1.  Verifique o status da coleção periodicamente até ver um status de `online`.
    - Emita uma chamada para o método `GET /v1/environments/{environment_id}/collections/{collection_id}` para recuperar o status da sua coleção. Novamente, substitua `{username}`, `{password}`,
`{environment_id}` e `{configuration_id}` pelas suas informações: 

    ```bash
    curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07
    ```
    {: pre}

## Etapa 3: Fazer download dos documentos de amostra
{: #download-sample-documents}

Faça download desses documentos de amostra: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo" class="style-scope doc-content"></a> e <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo" class="style-scope doc-content"></a>.

## Etapa 4: Fazer upload dos documentos
{: #upload-the-documents}

1.  Agora, inclua os documentos de exemplo na sua coleção. Este exemplo faz upload do documento **test-doc1.html** para sua coleção. Substitua `{username}`, `{password}`, `{environment_id}` e `{configuration_id}` pelas suas insformações. Modifique o local do documento de amostra para apontar para o local em que você salvou o arquivo `test-doc1.html`.
    - Use o método `POST /v1/environments/{environment_id}/collections/{collection_id}/documents`:

        ```bash
        curl -X POST -u "{username}":"{password}" -F "file=@test-doc1.html" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2017-11-07
        ```
        {: pre}

    Como alternativa, use um dos SDKs listados na [Referência da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}:
    - Java:

      ```java
      Discovery discovery = new Discovery("2017-11-07");
      discovery.setEndPoint("https://gateway.watsonplatform.net/discovery/api/v1");
      discovery.setUsernameAndPassword("{username}", "{password}");
      String environmentId = "{environment_id}";
      String collectionId = "{collection_id}";
      String documentJson = "{\"field\":\"value\"}";
      InputStream documentStream = new ByteArrayInputStream(documentJson.getBytes());

      CreateDocumentRequest.Builder builder = new CreateDocumentRequest.Builder(environmentId, collectionId);
      builder.inputStream(documentStream, HttpMediaType.APPLICATION_JSON);
      CreateDocumentResponse createResponse = discovery.createDocument(builder.build()).execute();
      ```
      {: codeblock}

    - Python:

      ```python
      import sys
import os
import json
from watson_developer_cloud import DiscoveryV1

      discovery = DiscoveryV1(
username="{username}",
password="{password}",
version="2017-11-07"
)

      with open((os.path.join(os.getcwd(), '{path_element}', '{filename}' as fileinfo:
        add_doc = discovery.add_document('{environment_id}', '{collection_id}', file_info=fileinfo)
      print(json.dumps(add_doc, indent=2))
      ```
      {: codeblock}

    - Node.js:

      ```javascript
      var DiscoveryV1 = require('watson-developer-cloud/discovery/v1');
      var fs = require('fs');

      var discovery = new DiscoveryV1({
        username: '{username}',
password: '{password}',
version_date: '2017-11-07'
});

      var file = fs.readFileSync('{/path/to/file}');

      discovery.addDocument(('{environment_id}', '{collection_id}', file),
      function(error, data) {
        console.log(JSON.stringify(data, null, 2));
}
      );
      ```
      {: codeblock}

1.  Repita esse processo para cada um dos 3 outros arquivos de amostra.

## Etapa 5: Consultar sua coleção
{: #query-your-collection}

Finalmente, use o método `GET /v1/environments/{environment_id}/collections/{collection_id}/query` para procurar sua coleção de documentos.

O exemplo a seguir retorna todas as entidades que são chamadas **IBM**. Substitua `{username}`, `{password}`, `{environment_id}` e `{configuration_id}` por suas informações:

```bash
curl -u "{username}":"{password}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}*/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

## Próximos passos
{: #next-steps}

Você consultou os documentos e criou a coleção com sucesso no ambiente. Agora é possível começar a customizar sua coleção incluindo mais documentos e enriquecimentos e customizando as configurações de conversão. Para obter mais informações sobre a API, consulte a [Referência da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}.
