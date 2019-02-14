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
{:curl: #curl .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}

# Introdução à API
{: #gs-api}

Neste curto tutorial, apresentamos a API do {{site.data.keyword.discoveryshort}} e
percorreremos o processo de criação e de procura de uma coleção de dados privados.
{: shortdesc}

Se você preferir trabalhar no conjunto de ferramentas do {{site.data.keyword.discoveryshort}}, veja [Introdução](/docs/services/discovery/getting-started-tool.html).
{: tip}

## Antes de Começar
{: #before-you-begin}

- Crie uma instância do serviço:
    1.  Acesse a página [{{site.data.keyword.discoveryshort}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.{DomainName}/catalog/services/discovery){: new_window} no {{site.data.keyword.Bluemix_notm}} Catalog.
    1.  Inscreva-se para obter uma conta gratuita do {{site.data.keyword.Bluemix_notm}} ou efetue login.
    1.  Clique em  ** Criar **.
- Copie as credenciais para autenticar sua instância de serviço:
    1. No [painel do {{site.data.keyword.Bluemix_notm}}](https://console.{DomainName}/dashboard/apps), clique em sua instância de serviço do {{site.data.keyword.discoveryshort}} para acessar a página de painel do serviço {{site.data.keyword.discoveryshort}}.
    1.  Na página **Gerenciar**, clique em **Mostrar** para visualizar suas credenciais.
    1.  Copie os valores  ` apikey `  e  ` url ` .

    Em algumas instâncias, você se autenticar fornecendo autenticação básica. Se você vir `username` e `password` nas credenciais, use esses valores em vez de `"apikey":"{apikey_value}"` nos exemplos neste tutorial.
{: tip}

## Etapa 1: Crie um ambiente
{: #create-an-environment}

Em um shell bash ou um ambiente equivalente, como Cygwin com o aplicativo `curl` instalado, use o método `POST /v1/environments` para criar um ambiente. Pense no ambiente como o warehouse em que você está armazenando todas as suas caixas de documentos.

Este tutorial usa uma chave API para autenticação. Para usos de produção, certifique-se de revisar as [melhores práticas](/docs/services/watson/apikey-bp.html#api-bp) da chave API.
{: tip}

1.  Emita o seguinte comando para criar um ambiente chamado `my-first-environment`. Substitua `{apikey_value}` pela chave API copiada anteriormente:

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "https://gateway.watsonplatform.net/discovery/api/v1/environments?version=2017-11-07"
    ```
    {: pre}

    A API retorna informações, como seu ID de ambiente, o status do ambiente e a quantia de armazenamento
que seu ambiente está usando.

1.  Verifique o status do ambiente periodicamente até que você veja um status de `active`.
    - Emita uma chamada para o método `GET /v1/environments/{environment_id}` para
recuperar o status de seu ambiente. Substitua `{apikey_value}` e `{environment_id}` pelas suas informações:

    ```bash
    curl -u "apikey": "{1}/environments/ {2}{0}{1}{7}-11-07"
    ```
    {: pre}

    O status deve ser `active` antes de poder criar uma coleção.

## Etapa 2: crie uma coleção
{: #create-a-collection}

Agora que o ambiente está pronto, é possível criar uma coleção. Pense em uma coleção como uma caixa na qual você armazena os documentos em seu ambiente.

1.  Primeiramente, é necessário o ID de sua configuração padrão. Para localizar seu
`configuration_id` padrão, use o método `GET /v1/environments/{environment_id}/configurations`. Substitua `{apikey_value}` e `{environment_id}` pelas suas informações:

    ```bash
      curl -u "apikey":"{apikey_value}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07
    ```
    {: pre}
1.  Use o método `POST /v1/environments/{environment_id}/collections`
para criar uma coleção chamada **my-first-collection**. Substitua `{apikey_value}`, `{environment_id}` e `{configuration_id}` pelas suas informações:

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d '{"name": "my-first-collection", "description": "exploring collections", "configuration_id":"{configuration_id}" , "language": "en_us"}' https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections?version=2017-11-07
    ```
    {: pre}

    A API retorna informações, como seu ID de coleção, o status da coleção e a quantia de armazenamento que sua
coleção está usando.
1.  Verifique o status da coleção periodicamente até que você veja um status de `active`.
    - Emita uma chamada para o método `GET /v1/environments/{environment_id}/collections/{collection_id}` para recuperar o status da sua coleção.  Novamente, substitua `{apikey_value}`, `{environment_id}` e `{configuration_id}` por suas informações:

    ```bash
    curl -u "apikey": "{1}/environments/ {2}{0}{1}{7}-11-07
    ```
    {: pre}

## Etapa 3: Fazer download dos documentos de amostra
{: #download-sample-documents}

Faça download desses documentos de amostra: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc1.html" download>test-doc1.html <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc2.html" download>test-doc2.html <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo" class="style-scope doc-content"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc3.html" download>test-doc3.html <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo" class="style-scope doc-content"></a> e <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/test-doc4.html" download>test-doc4.html <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo" class="style-scope doc-content"></a>.

**Nota:** em alguns navegadores, os links anteriores serão abertos em uma nova janela em vez de salvar localmente. Se isso ocorrer, selecione `Save as` no menu `File` de seu navegador para salvar uma cópia do arquivo.

## Etapa 4: Fazer upload dos documentos
{: #upload-the-documents}

1.  Agora, inclua os documentos de exemplo na sua coleção. Este exemplo faz upload do documento **test-doc1.html** para sua coleção. Substitua `{apikey_value}`, `{environment_id}` e `{configuration_id}` por suas informações. Modifique o local do documento de amostra para apontar para o local em que você salvou o arquivo `test-doc1.html`.
    - Use o método `POST /v1/environments/{environment_id}/collections/{collection_id}/documents`:

        ```bash
        curl -X POST -u "apikey":"{apikey_value}" -F "file=@test-doc1.html" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/documents?version=2017-11-07
        ```
        {: pre}

    Como alternativa, use um dos SDKs listados na [Referência da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}:
    - Java:

      ```java
      Discovery discovery = new Discovery("2017-11-07");
      discovery.setEndPoint("https://gateway.watsonplatform.net/discovery/api/v1");
      IamOptions options = new IamOptions.Builder()
        .apiKey ("{")
        .build();
      discovery.setIamCredentials(options);
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
        version='2017-11-07',
        api_key='{apikey_value}'
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
        version_date: '2017-11-07',
        iam_apikey: '{apikey_value}',
      });

      var file = fs.readFileSync('{/path/to/file}');

      discovery.addDocument({ environment_id: '{environment_id}', collection_id: '{collection_id}', file: file },
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

O exemplo a seguir retorna todas as entidades que são chamadas **IBM**. Substitua `{apikey_value}`, `{environment_id}` e `{configuration_id}` pelas suas informações:

```bash
curl -u "apikey":"{apikey_value}" 'https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-11-07&query=enriched_text.entities.text:IBM'
```
{: pre}

## Próximos passos
{: #next-steps}

Você consultou com êxito os documentos no ambiente e na coleção criada. Agora é possível começar a customizar sua coleção incluindo mais documentos e enriquecimentos e customizando as configurações de conversão.

- Leia sobre a API na [Referência da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/){: new_window}
- [ Configure ](/docs/services/discovery/building.html)  seu serviço
- Aprenda sobre o  [ autenticando com o IAM ](/docs/services/watson/getting-started-iam.html)
